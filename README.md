# Docker & Kubernetes Mastery: Architectural & Operational Deep Dive

Interactive architectural and operational mastery platform for **Docker and Linux Containers** and **Kubernetes Cluster Internals**.

Explore the exact kernel mechanics of containers (Namespaces, Cgroups, OverlayFS, OCI runtimes) and the distributed consensus and reconciliation loop of Kubernetes (API Server, etcd, Kube-Scheduler, Kubelet, CNI, CSI, and Service Mesh).

## Platform Capabilities

- **Interactive Control Plane & Pod Lifecycle Simulator**:
  - Step-by-step state machine trace from `kubectl apply` through API Server admission webhooks, etcd MVCC write, Kube-Scheduler filtering and scoring, Kubelet CRI dispatch, containerd/runc sandbox creation, CNI IPAM allocation, and startup/readiness probe checks.
  - Live node failure and evictions, replica scaling, and OOMKilled crash simulations.
- **Linux Kernel & Container Runtime Labs**:
  - **Namespaces & Process Isolation**: Visualizing `PID`, `NET`, `MNT`, `IPC`, `UTS`, `USER`, and `CGROUP` kernel syscalls (`clone`, `unshare`, `setns`), contrasting host vs. container PID trees.
  - **Cgroups v1/v2 & CFS Throttling**: Interactive `cpu.cfs_period_us` and `cpu.cfs_quota_us` slider calculating exact CPU throttle cycles, alongside memory high/max thresholds and OOM-killer priority scoring (`oom_score_adj`).
  - **OverlayFS Copy-on-Write (CoW)**: Interactive layer explorer (`LowerDir`, `UpperDir`, `MergedDir`, `WorkDir`) demonstrating file reads, writes, modifications, and whiteout (`.wh.*`) tombstones.
  - **OCI & CRI Architecture**: The complete execution hierarchy: `Docker CLI` → `dockerd` → `containerd` → `containerd-shim` → `runc` → `Linux Kernel`.
- **Kubernetes Networking & Storage Engine**:
  - **4-Tier Network Packet Flow Tracer**: Step-by-step packet tracer with real header transformations across Container-to-Container (localhost), Pod-to-Pod (CNI overlay/BGP routing), Pod-to-Service (iptables/eBPF DNAT/SNAT), and External-to-Pod (NodePort / Ingress).
  - **CSI Storage Engine**: Persistent Volume lifecycle from StorageClass dynamic provisioning, Node Stage/Publish, and host directory bind-mounts.
- **Production Architecture & Pattern Cookbook**:
  - Multi-stage Dockerfile optimization (slimming images from 1.2 GB to 38 MB using distroless and build cache mounts).
  - Zero-Downtime Deployment & Graceful Shutdown: Mitigating the `SIGTERM` vs. kube-proxy endpoint removal race condition with `preStop` hooks.
  - Native restartable sidecar containers, DaemonSets, StatefulSets, and PodDisruptionBudgets (PDB).
- **Advanced SRE Incident Triage Runbooks**:
  - **CrashLoopBackOff & Exit Codes**: Deep-dive into Exit 137 (OOM), 143 (SIGTERM), 1 (App error), 127 (Exec format / missing interpreter).
  - **ImagePullBackOff & ErrImagePull**: Root causes, private registry authentication, multi-arch manifest mismatches, and rate-limiting.
  - **Pending Pods & Scheduling Failures**: Resolving taints/tolerations, node affinity deadlock, and unbound PVCs.
  - **Silent CFS CPU Throttling**: Debugging p99 latency degradation despite low CPU averages.
  - **CoreDNS & Conntrack Exhaustion**: The `ndots:5` latency amplifier and DNS packet drop mitigations.
- **Cluster Capacity Sizing & Production Readiness Scorecard**:
  - Node allocatable calculator (accounting for `kube-reserved`, `system-reserved`, and eviction thresholds).
  - Workload packing and node count estimator with overcommit risk gauges.
  - 12-Factor Kubernetes Production Readiness Scorecard with real-time audit scoring.
- **Command Palette (`⌘K` or `/`)**:
  - Instant keyboard-driven lookup across all container concepts, Linux kernel syscalls, and production runbooks.

---

## Live Deployment

- **GitHub Pages**: [https://anil0225.github.io/docker-k8s-mastery](https://anil0225.github.io/docker-k8s-mastery)
- **Repository**: [https://github.com/anil0225/docker-k8s-mastery](https://github.com/anil0225/docker-k8s-mastery)

---

## Local Development & Viewing

Clone the repository and open `index.html` in any modern web browser:

```bash
git clone https://github.com/anil0225/docker-k8s-mastery.git
cd docker-k8s-mastery
# Open in your default browser:
# On Windows:
start index.html
# On macOS:
open index.html
# On Linux:
xdg-open index.html
```

No build tools, Node.js, or complex pipelines required. The platform is built as an ultra-fast, zero-dependency, single-page application powered by modern CSS, standard vanilla JavaScript ES6+, and Lucide icons.
