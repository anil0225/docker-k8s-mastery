# Docker & Kubernetes Mastery: Architectural & Operational Deep Dive

Interactive architectural and operational mastery platform for **Docker and Linux Containers** and **Kubernetes Cluster Internals**, built with the exact interactive format as [kafka-mastery](https://anil0225.github.io/kafka-mastery).

Explore the exact kernel mechanics of containers (Namespaces, Cgroups, OverlayFS, OCI runtimes) and the distributed consensus and reconciliation loop of Kubernetes (API Server, etcd, Kube-Scheduler, Kubelet, CNI, CSI, and Service Mesh).

---

## Live Deployment

- **Live GitHub Pages**: [https://anil0225.github.io/docker-k8s-mastery/](https://anil0225.github.io/docker-k8s-mastery/)
- **GitHub Repository**: [https://github.com/anil0225/docker-k8s-mastery](https://github.com/anil0225/docker-k8s-mastery)

---

## Platform Architecture & Interactive Pages

The platform is structured into 7 deep, interactive architectural modules:

### 1. Live Cluster Simulation & Pod Orchestration Engine
- **Full Cluster Topology**: 
  - **Client & Ingress Tier**: L7 Ingress Controller (`https://api.k8s.local`), Service ClusterIP (`10.96.0.100`), dynamic endpoint mapping, and an interactive **Send HTTP Request** engine testing round-robin DNAT load balancing.
  - **Master Control Plane**: `kube-apiserver` (port 6443 TLS, RBAC, Mutating/Validating Admission Webhooks), `etcd v3` (Raft Consensus, MVCC Key-Value `/registry/pods/...`, live revision counter), `kube-scheduler` (Queue -> 2-Phase Filtering & Scoring), and `kube-controller-manager`.
  - **Worker Node Fleet**: 3 worker nodes (`worker-01`, `worker-02`, `worker-03`) with dynamic CPU and RAM usage bars, node status (`Ready`, `NotReady`, `Cordoned`), and visual pod allocation slots with real-time status dots.
  - **Pod Details Inspector**: Inspect any pod's IP, node assignment, restart count, readiness probes, and isolated kernel namespaces.
- **Interactive Cluster Chaos**:
  - `Simulate Worker 1 Crash`: Triggers heartbeat timeout, watch `NodeLifecycleController` mark node `NotReady` and evict pods to healthy surviving nodes.
  - `Cordon & Drain Node 2`: Sets `SchedulingDisabled` and safely evicts workloads before maintenance.
  - `Inject OOMKill (Exit 137)`: Injects memory leaks, triggering Linux kernel `SIGKILL` and exponential `CrashLoopBackOff`.
- **Reconciliation Pipeline Tracker**: Live step-by-step state machine from API Server -> etcd commit -> Scheduler bind -> Kubelet CRI -> CNI/CSI -> Readiness Probe.
- **Terminal Event Stream**: Real-time `kubectl get events -w` terminal log.

### 2. Deep Dive Labs Playground (with 5 Interactive Sub-Tabs)
- **1. Linux Namespaces & Syscalls**: Interactive toggle across 7 namespaces (`PID`, `NET`, `MNT`, `IPC`, `UTS`, `USER`, `CGROUP`), comparing host OS kernel process trees vs. container views with exact `clone()`, `unshare()`, and `setns()` syscall definitions.
- **2. Cgroups v2 & CFS CPU Throttling Calculator**: Interactive slider for `cpu.cfs_quota_us` vs. `cpu.cfs_period_us` (100ms period). Demonstrates why multi-threaded runtimes (Go/Java) consume quota in 15ms and get frozen by the kernel, causing p99 latency spikes.
- **3. OverlayFS (UnionFS) & Copy-on-Write (CoW)**: Interactive visual layer stack (`LowerDir`, `UpperDir`, `MergedDir`). Simulate file reads, Copy-on-Write edits, new file creation, and `.wh.*` whiteout tombstones.
- **4. OCI Hierarchy & containerd-shim**: Simulates containerd daemon crashes to demonstrate why `containerd-shim` allows containers to run with zero downtime during daemon upgrades.
- **5. Kube-Scheduler Predicates & Priorities Lab**: Test custom Pod CPU requests, `nodeSelector`, and taints/tolerations to watch candidate nodes get filtered and scored in real time.

### 3. Interactive Sequence Diagrams (with Animated SVG Lifelines & Playback)
- **Controls**: Next Step, Prev Step, Auto-Play (with timer and play/pause toggle), Reset, and step dots.
- **SVG Canvas**: Vertical lifelines, animated packet dots traveling across participants, protocol markers, and technical commentary.
- **3 Core Lifecycle Diagrams**:
  1. *Pod Creation & CRI Scheduling Lifecycle* (kubectl -> apiserver -> etcd -> scheduler -> kubelet -> containerd -> runc).
  2. *Service Routing & iptables DNAT Data Plane* (Client Pod -> veth -> netfilter PREROUTING -> VXLAN overlay -> Target Pod).
  3. *Graceful Termination & The SIGTERM Race Condition* (Demonstrating how `preStop: sleep 10` eliminates 502 Bad Gateway errors).

### 4. Production Architecture & Pattern Cookbook
- **Pattern 1: Multi-Stage Distroless Dockerfile** (1.2GB → 38MB, non-root UID 65532, zero CVE attack surface).
- **Pattern 2: Graceful Shutdown & preStop Hook** (Eliminating 502/504 errors during rolling updates).
- **Pattern 3: Native Restartable Sidecars (K8s 1.28+)** (`initContainers` with `restartPolicy: Always`).
- **Pattern 4: High-Availability PDB & Topology Spread Constraints** (Surviving full Availability Zone outages).

### 5. Senior SRE Incident Triage Runbooks
- Interactive scenario cards with root cause architecture, symptoms, copyable diagnostic commands, and production YAML fixes:
  - **Incident A: CrashLoopBackOff & Container Exit Codes** (Exit 137 OOMKilled, 143 SIGTERM, 1 App Crash, 127 Command Not Found).
  - **Incident B: ImagePullBackOff & Multi-Arch Mismatch** (Apple Silicon ARM64 vs AMD64 exec format error).
  - **Incident C: Pending Pods & Scheduling Deadlocks** (Resource exhaustion, untolerated taints, PVC zone affinity conflicts).
  - **Incident D: CoreDNS & ndots:5 Amplification** (Conntrack table exhaustion, UDP packet drops, `single-request-reopen` fix).

### 6. Architecture Planning & Capacity Sizing Calculator
- **Dynamic Capacity Sizer**: Calculates true Node Allocatable (deducting `kube-reserved`, `system-reserved`, and eviction thresholds), max safe pods per node, and minimum required HA worker nodes (N+1 AZ buffer).
- **12-Point Cloud-Native Production Readiness Scorecard**: Interactive audit checklist grading manifests from Grade A+ down to high outage risk.

### 7. Embed & Integration Guide (Google Sites & Confluence)
- One-click copyable `<iframe>` embed code.
- Step-by-step guide for embedding directly into **Google Sites**, Confluence, Notion, and internal developer portals.

---

## Local Development

Open `index.html` in any modern web browser:

```bash
git clone https://github.com/anil0225/docker-k8s-mastery.git
cd docker-k8s-mastery
start index.html # On Windows
```
