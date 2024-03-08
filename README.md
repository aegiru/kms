<div align="center">

<img src="https://raw.githubusercontent.com/aegiru/kms/main/k8s.png" align="center" width="192px" height="144px"/>


### **kms**

_**K**inda **M**ediocre **S**elf-hosting_

</div>

---

## 🧾 Overview

This is a mono repository for my Kubernetes cluster, based on onedr0p's excellent [home-ops](https://github.com/onedr0p/home-ops) and [cluster-template](https://github.com/onedr0p/cluster-template) repos. I'd like to use it for learning how to properly utilise clusterization as well as Infrastructure as Code, all while actually having it do something genuinely useful for me.

---

## ⛵ Kubernetes

Due to currently running on relatively low-power machines, I opted to use [k3s](https://k3s.io/) as it's much more lightweight than regular k8s, while still providing all the necessary functionality. ~~Definitely not because it's the default choice in the template listed above.~~

### Installation

The cluster is deployed on Debian 12 (bookworm) installations, using the generic cloud images found on [Debian's Official Cloud Images list](https://cloud.debian.org/images/cloud/). Chosen mainly for being very lightweight, which is key given the hardware it's deployed on (listed further down below).

### Core Components

- [cert-manager](https://github.com/cert-manager/cert-manager): Responsible for SSL certificates for services within my cluster.
- [cilium](https://github.com/cilium/cilium): Internal Kubernetes container networking interface.
- [cloudflared](https://github.com/cloudflare/cloudflared): Exposing certain ingresses through a Cloudflare tunnel.
- [external-dns](https://github.com/kubernetes-sigs/external-dns): Syncing DNS records with a DNS provider.
- [ingress-nginx](https://github.com/kubernetes/ingress-nginx): Ingress controller using NGINX as a load balancer and a reverse proxy.
- [sops](https://github.com/getsops/sops): Managed secrets for Kubernetes which are commited to Git.

### GitOps

[Flux](https://github.com/fluxcd/flux2) watches for changes in the [kubernetes/apps](./kubernetes/apps/) folder, and applies them to the cluster automatically.

---

## ☁️ Cloud Dependencies

Part of the reason why this set-up is (highly) mediocre from a self-hosted point of view, is that nothing is **_truly_** self-hosted. Everything runs on Oracle Cloud Infrastructure, solely because their free offerings server-wise are more than enough for me. ~~My current ISP's limited upload is not related in the slightest.~~ The reason why Oracle isn't free is that I pay for 300 GB of drive space - 100 GB more than they allow you to use for free.

| Service                                   | Use                                          | Cost            |
|-------------------------------------------|----------------------------------------------|-----------------|
| [Oracle](https://www.oracle.com/cloud/)   | Hardware                                     | ~$5 / mo        |
| [Cloudflare](https://www.cloudflare.com/) | Domain                                       | ~$5 / year      |
| [GitHub](https://github.com/)             | Hosting this repo and continuous integration | Free            |
|                                           |                                              | Total: ~$6 / mo |

---

## ⚙️ "Hardware"

| Device         | Count | Disk Space | vCores | Threads | RAM   | Operating System | Purpose                               |
|----------------|-------|------------|--------|---------|-------|------------------|---------------------------------------|
| Ampere A1      | 1     | 300 GB     | 4      | 4       | 24 GB | Debian           | Kubernetes Controller / Everything    |

---

## 🤝 Gratitude and Thanks

I'd like to thank [Techno Tim](https://github.com/timothystewart6), and his Discord community for help. His YouTube channel has been a great starting point and (together with [r/selfhosted](https://www.reddit.com/r/selfhosted/)) has served as a goal to strive towards and a source of ~~jealousy~~ _motivation_. Huge thanks to [onedr0p](https://github.com/onedr0p) for his repos, and the [Home Operations](https://discord.gg/home-operations) Discord community for withstanding my murderously boring and unexpected problems in regards to actually setting this thing up.
