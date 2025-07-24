## Kuberffy - Kubernetes K3S Setup

A lightweight Kubernetes cluster

---

### System Overview

| Node Type     | Hostname | Location | Operating System  | CPU                      | RAM                   |
|:--------------|:---------|:---------|:------------------|:-------------------------|:----------------------|
| Control Plane | arch     | Homelab  | Arch Linux        | Intel N100 @ 3.40 GHz × 4 | 8 GB LPDDR5 @ 4800 MHz |

---

### Apps

| App          | Description                                                      |
|:-------------|:-----------------------------------------------------------------|
| AdGuard Home | Network-wide software for blocking ads and trackers.             |
| ConvertX     | Self-hosted online file converter.                               |
| Dashdot      | Modern and customizable server dashboard.                        |
| Picoshare    | Minimalist, easy-to-host service for sharing images and files.   |
| PostgreSQL   | Powerful, open-source relational database system.                |
| SearXNG      | Privacy-respecting, free internet metasearch engine.             |
| Slimserve    | Minimalistic and efficient static file server.                   |

---

### Prerequisites

- Root access

---

### Installation

Install K3S using the official installation script:

```bash
curl -sfL https://get.k3s.io | sh -
```

Verify the K3S service is running:

```bash
sudo systemctl status k3s
```

---

### Configuration

Copy the K3S kubeconfig file to your home directory for `kubectl` access:

```bash
mkdir -p ~/.kube
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
sudo chown $(id -u):$(id -g) ~/.kube/config
```

Test cluster access:

```bash
kubectl get nodes
kubectl get pods -A
```

---

### Deployments

1. Clone this repo and cd

```bash
git clone https://github.com/erffy/k3s.git && cd k3s
```

2. Apply Kubernetes manifests using:

```bash
kubectl apply -k .
```

This deploys the configured services and applications on your cluster.

---

### Usage

Some handy kubectl commands:

- Check cluster info:

  ```bash
  kubectl cluster-info
  ```

- List nodes:

  ```bash
  kubectl get nodes
  ```

- List pods across all namespaces:

  ```bash
  kubectl get pods -A
  ```

- View pod logs:

  ```bash
  kubectl logs <pod-name>
  ```

---

### Troubleshooting

- If `kubectl` shows connection refused, ensure your kubeconfig is correctly configured.  
- Restart K3s service if needed:

  ```bash
  sudo systemctl restart k3s
  sudo journalctl -u k3s -f
  ```

---

### Credits ❤️

- [saveside/honeypot](https://github.com/saveside/honeypot)
- [mt190502/k8s](https://github.com/mt190502/k8s)