# Домашнее задание к занятию «Установка Kubernetes»

### Цель задания

Установить кластер K8s.

### Чеклист готовности к домашнему заданию

1. Развёрнутые ВМ с ОС Ubuntu 20.04-lts.


### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Инструкция по установке kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/).
2. [Документация kubespray](https://kubespray.io/).

-----

### Задание 1. Установить кластер k8s с 1 master node

```
user@master-node:~$ git clone https://github.com/kubernetes-sigs/kubespray
Cloning into 'kubespray'...
remote: Enumerating objects: 79074, done.
remote: Counting objects: 100% (242/242), done.
remote: Compressing objects: 100% (127/127), done.
remote: Total 79074 (delta 165), reused 115 (delta 115), pack-reused 78832 (from 4)
Receiving objects: 100% (79074/79074), 25.14 MiB | 26.05 MiB/s, done.
Resolving deltas: 100% (44717/44717), done.
```

```
(venv) user@master-node:~/kubespray$ pip3 install -r requirements.txt
Collecting ansible==9.13.0 (from -r requirements.txt (line 1))
  Downloading ansible-9.13.0-py3-none-any.whl.metadata (8.0 kB)
Collecting cryptography==44.0.0 (from -r requirements.txt (line 3))
  Downloading cryptography-44.0.0-cp39-abi3-manylinux_2_28_x86_64.whl.metadata (5.7 kB)
Collecting jmespath==1.0.1 (from -r requirements.txt (line 5))
  Downloading jmespath-1.0.1-py3-none-any.whl.metadata (7.6 kB)
Collecting netaddr==1.3.0 (from -r requirements.txt (line 7))
  Downloading netaddr-1.3.0-py3-none-any.whl.metadata (5.0 kB)
Collecting ansible-core~=2.16.14 (from ansible==9.13.0->-r requirements.txt (line 1))
  Downloading ansible_core-2.16.14-py3-none-any.whl.metadata (6.9 kB)
Collecting cffi>=1.12 (from cryptography==44.0.0->-r requirements.txt (line 3))
  Downloading cffi-1.17.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (1.5 kB)
Collecting jinja2>=3.0.0 (from ansible-core~=2.16.14->ansible==9.13.0->-r requirements.txt (line 1))
  Downloading jinja2-3.1.5-py3-none-any.whl.metadata (2.6 kB)
Collecting PyYAML>=5.1 (from ansible-core~=2.16.14->ansible==9.13.0->-r requirements.txt (line 1))
  Downloading PyYAML-6.0.2-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (2.1 kB)
Collecting packaging (from ansible-core~=2.16.14->ansible==9.13.0->-r requirements.txt (line 1))
  Downloading packaging-24.2-py3-none-any.whl.metadata (3.2 kB)
Collecting resolvelib<1.1.0,>=0.5.3 (from ansible-core~=2.16.14->ansible==9.13.0->-r requirements.txt (line 1))
  Downloading resolvelib-1.0.1-py2.py3-none-any.whl.metadata (4.0 kB)
Collecting pycparser (from cffi>=1.12->cryptography==44.0.0->-r requirements.txt (line 3))
  Downloading pycparser-2.22-py3-none-any.whl.metadata (943 bytes)
Collecting MarkupSafe>=2.0 (from jinja2>=3.0.0->ansible-core~=2.16.14->ansible==9.13.0->-r requirements.txt (line 1))
  Downloading MarkupSafe-3.0.2-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (4.0 kB)
Downloading ansible-9.13.0-py3-none-any.whl (51.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 51.5/51.5 MB 4.0 MB/s eta 0:00:00
Downloading cryptography-44.0.0-cp39-abi3-manylinux_2_28_x86_64.whl (4.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.2/4.2 MB 18.3 MB/s eta 0:00:00
Downloading jmespath-1.0.1-py3-none-any.whl (20 kB)
Downloading netaddr-1.3.0-py3-none-any.whl (2.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.3/2.3 MB 28.2 MB/s eta 0:00:00
Downloading ansible_core-2.16.14-py3-none-any.whl (2.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.3/2.3 MB 21.4 MB/s eta 0:00:00
Downloading cffi-1.17.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (479 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 479.4/479.4 kB 21.8 MB/s eta 0:00:00
Downloading jinja2-3.1.5-py3-none-any.whl (134 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 134.6/134.6 kB 7.6 MB/s eta 0:00:00
Downloading PyYAML-6.0.2-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (767 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 767.5/767.5 kB 23.3 MB/s eta 0:00:00
Downloading resolvelib-1.0.1-py2.py3-none-any.whl (17 kB)
Downloading packaging-24.2-py3-none-any.whl (65 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 65.5/65.5 kB 2.8 MB/s eta 0:00:00
Downloading pycparser-2.22-py3-none-any.whl (117 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 117.6/117.6 kB 2.7 MB/s eta 0:00:00
Downloading MarkupSafe-3.0.2-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (23 kB)
Installing collected packages: resolvelib, PyYAML, pycparser, packaging, netaddr, MarkupSafe, jmespath, jinja2, cffi, cryptography, ansible-core, ansible
Successfully installed MarkupSafe-3.0.2 PyYAML-6.0.2 ansible-9.13.0 ansible-core-2.16.14 cffi-1.17.1 cryptography-44.0.0 jinja2-3.1.5 jmespath-1.0.1 netaddr-1.3.0 packaging-24.2 pycparser-2.22 resolvelib-1.0.1
```

user@master-node:~/kubespray$ declare -a IPS=(10.129.0.11 10.129.0.23 10.129.0.41 10.129.0.15 10.129.0.16)
(venv) user@master-node:~/kubespray$ CONFIG_FILE=inventory/mycluster/hosts.yaml python3 contrib/inventory_builder/inventory.py ${IPS[@]}
DEBUG: Adding group all
DEBUG: Adding group kube_control_plane
DEBUG: Adding group kube_node
DEBUG: Adding group etcd
DEBUG: Adding group k8s_cluster
DEBUG: Adding group calico_rr
DEBUG: adding host node1 to group all
DEBUG: adding host node2 to group all
DEBUG: adding host node3 to group all
DEBUG: adding host node4 to group all
DEBUG: adding host node5 to group all
DEBUG: adding host node1 to group etcd
DEBUG: adding host node2 to group etcd
DEBUG: adding host node3 to group etcd
DEBUG: adding host node1 to group kube_control_plane
DEBUG: adding host node2 to group kube_control_plane
DEBUG: adding host node1 to group kube_node
DEBUG: adding host node2 to group kube_node
DEBUG: adding host node3 to group kube_node
DEBUG: adding host node4 to group kube_node
DEBUG: adding host node5 to group kube_node

(venv) user@master-node:~/kubespray$ cat inventory/mycluster/hosts.yaml
all:
  hosts:
    master-node:
      ansible_host: 10.129.0.16
      ip: 10.129.0.16
      access_ip: 10.129.0.16
    worker-node-1:
      ansible_host: 10.129.0.15
      ip: 10.129.0.15
      access_ip: 10.129.0.15
    worker-node-2:
      ansible_host: 10.129.0.11
      ip: 10.129.0.11
      access_ip: 10.129.0.11
    worker-node-3:
      ansible_host: 10.129.0.23
      ip: 10.129.0.23
      access_ip: 10.129.0.23
    worker-node-4:
      ansible_host: 10.129.0.41
      ip: 10.129.0.41
      access_ip: 10.129.0.41
  children:
    kube_control_plane:
      hosts:
        master-node:
    kube_node:
      hosts:
        worker-node-1:
        worker-node-2:
        worker-node-3:
        worker-node-4:
    etcd:
      hosts:
        master-node:
    k8s_cluster:
      children:
        kube_control_plane:
        kube_node:
    calico_rr:
      hosts: {}


(venv) user@master-node:~/kubespray$ ansible-playbook -i inventory/mycluster/hosts.yaml cluster.yml -b -v
.
.
.
PLAY RECAP **********************************************************************************************************************************
master-node                : ok=620  changed=133  unreachable=0    failed=0    skipped=1111 rescued=0    ignored=6
worker-node-1              : ok=411  changed=81   unreachable=0    failed=0    skipped=664  rescued=0    ignored=1
worker-node-2              : ok=411  changed=82   unreachable=0    failed=0    skipped=660  rescued=0    ignored=1
worker-node-3              : ok=411  changed=81   unreachable=0    failed=0    skipped=660  rescued=0    ignored=1
worker-node-4              : ok=411  changed=81   unreachable=0    failed=0    skipped=660  rescued=0    ignored=1

Thursday 26 December 2024  12:01:38 +0000 (0:00:00.263)       0:15:36.945 *****
===============================================================================
download : Download_file | Download item ------------------------------------------------------------------------------------------- 105.41s
kubernetes/control-plane : Kubeadm | Initialize first master ------------------------------------------------------------------------ 53.50s
download : Download_container | Download image if required -------------------------------------------------------------------------- 34.58s
kubernetes/preinstall : Update package management cache (APT) ----------------------------------------------------------------------- 25.23s
network_plugin/calico : Wait for calico kubeconfig to be created -------------------------------------------------------------------- 23.47s
kubernetes/preinstall : Ensure ping package ----------------------------------------------------------------------------------------- 22.66s
kubernetes/preinstall : Install packages requirements ------------------------------------------------------------------------------- 21.38s
kubernetes/kubeadm : Join to cluster ------------------------------------------------------------------------------------------------ 18.50s
download : Download_file | Download item -------------------------------------------------------------------------------------------- 16.82s
download : Download_container | Download image if required -------------------------------------------------------------------------- 15.11s
download : Download_container | Download image if required -------------------------------------------------------------------------- 14.19s
network_plugin/calico : Calico | Copy calicoctl binary from download dir ------------------------------------------------------------ 13.02s
container-engine/containerd : Download_file | Download item ------------------------------------------------------------------------- 11.43s
container-engine/runc : Download_file | Download item ------------------------------------------------------------------------------- 11.33s
download : Download_file | Download item -------------------------------------------------------------------------------------------- 11.30s
download : Download_container | Download image if required -------------------------------------------------------------------------- 11.08s
container-engine/crictl : Download_file | Download item ----------------------------------------------------------------------------- 10.90s
container-engine/nerdctl : Download_file | Download item ---------------------------------------------------------------------------- 10.77s
kubernetes/node : Install | Copy kubelet binary from download dir -------------------------------------------------------------------- 8.54s
download : Download_file | Download item --------------------------------------------------------------------------------------------- 8.01s


```
user@master-node:~$ sudo apt-get update
Hit:1 http://archive.ubuntu.com/ubuntu noble InRelease
Get:2 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Get:3 http://archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]
Get:4 http://archive.ubuntu.com/ubuntu noble-backports InRelease [126 kB]
Get:5 http://security.ubuntu.com/ubuntu noble-security/main amd64 Components [7,220 B]
Get:6 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 Components [151 kB]
Get:7 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Components [52.0 kB]
Get:8 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Components [208 B]
Get:9 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 Components [208 B]
Get:10 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 Components [309 kB]
Get:11 http://archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Components [212 B]
Get:12 http://archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Components [940 B]
Get:13 http://archive.ubuntu.com/ubuntu noble-backports/main amd64 Components [208 B]
Get:14 http://archive.ubuntu.com/ubuntu noble-backports/universe amd64 Components [11.7 kB]
Get:15 http://archive.ubuntu.com/ubuntu noble-backports/restricted amd64 Components [216 B]
Get:16 http://archive.ubuntu.com/ubuntu noble-backports/multiverse amd64 Components [212 B]
Fetched 912 kB in 1s (1,091 kB/s)
Reading package lists... Done
user@master-node:~$ sudo apt-get install -y apt-transport-https ca-certificates curl gpg
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
apt-transport-https is already the newest version (2.7.14build2).
ca-certificates is already the newest version (20240203).
ca-certificates set to manually installed.
curl is already the newest version (8.5.0-2ubuntu10.6).
gpg is already the newest version (2.4.4-2ubuntu17).
gpg set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 3 not upgraded.
user@master-node:~$ sudo mkdir -p -m 755 /etc/apt/keyrings
user@master-node:~$ curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
user@master-node:~$ echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /
```

```
user@master-node:~$ sudo apt-get install containerd
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  runc
The following NEW packages will be installed:
  containerd runc
0 upgraded, 2 newly installed, 0 to remove and 3 not upgraded.
Need to get 47.2 MB of archives.
After this operation, 179 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 runc amd64 1.1.12-0ubuntu3.1 [8,599 kB]
Get:2 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 containerd amd64 1.7.19+really1.7.12-0ubuntu4.2 [38.6 MB]
Fetched 47.2 MB in 3s (16.7 MB/s)
Selecting previously unselected package runc.
(Reading database ... 128047 files and directories currently installed.)
Preparing to unpack .../runc_1.1.12-0ubuntu3.1_amd64.deb ...
Unpacking runc (1.1.12-0ubuntu3.1) ...
Selecting previously unselected package containerd.
Preparing to unpack .../containerd_1.7.19+really1.7.12-0ubuntu4.2_amd64.deb ...
Unpacking containerd (1.7.19+really1.7.12-0ubuntu4.2) ...
Setting up runc (1.1.12-0ubuntu3.1) ...
Setting up containerd (1.7.19+really1.7.12-0ubuntu4.2) ...
Processing triggers for man-db (2.12.0-4build2) ...
Scanning processes...
Scanning linux images...

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
```

```
user@master-node:~$ sudo sysctl --system
* Applying /usr/lib/sysctl.d/10-apparmor.conf ...
* Applying /etc/sysctl.d/10-bufferbloat.conf ...
* Applying /etc/sysctl.d/10-console-messages.conf ...
* Applying /etc/sysctl.d/10-ipv6-privacy.conf ...
* Applying /etc/sysctl.d/10-kernel-hardening.conf ...
* Applying /etc/sysctl.d/10-magic-sysrq.conf ...
* Applying /etc/sysctl.d/10-map-count.conf ...
* Applying /etc/sysctl.d/10-network-security.conf ...
* Applying /etc/sysctl.d/10-ptrace.conf ...
* Applying /etc/sysctl.d/10-zeropage.conf ...
* Applying /usr/lib/sysctl.d/50-pid-max.conf ...
* Applying /usr/lib/sysctl.d/99-protect-links.conf ...
* Applying /etc/sysctl.d/99-sysctl.conf ...
* Applying /etc/sysctl.d/k8s.conf ...
* Applying /etc/sysctl.conf ...
kernel.apparmor_restrict_unprivileged_userns = 1
net.core.default_qdisc = fq_codel
kernel.printk = 4 4 1 7
net.ipv6.conf.all.use_tempaddr = 2
net.ipv6.conf.default.use_tempaddr = 2
kernel.kptr_restrict = 1
kernel.sysrq = 176
vm.max_map_count = 1048576
net.ipv4.conf.default.rp_filter = 2
net.ipv4.conf.all.rp_filter = 2
kernel.yama.ptrace_scope = 1
vm.mmap_min_addr = 65536
kernel.pid_max = 4194304
fs.protected_fifos = 1
fs.protected_hardlinks = 1
fs.protected_regular = 2
fs.protected_symlinks = 1
net.ipv4.ip_forward = 1
kernel.keys.root_maxbytes = 25000000
kernel.keys.root_maxkeys = 1000000
kernel.panic = 10
kernel.panic_on_oops = 1
vm.overcommit_memory = 1
vm.panic_on_oom = 0
net.ipv4.ip_local_reserved_ports = 30000-32767
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-arptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
net.ipv4.ip_forward = 1
kernel.keys.root_maxbytes = 25000000
kernel.keys.root_maxkeys = 1000000
kernel.panic = 10
kernel.panic_on_oops = 1
vm.overcommit_memory = 1
vm.panic_on_oom = 0
net.ipv4.ip_local_reserved_ports = 30000-32767
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-arptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
```

```
user@master-node:~$ sudo kubeadm init --apiserver-advertise-address=10.129.0.16 --apiserver-cert-extra-sans=84.201.164.45 --pod-network-cidr=10.244.0.0/16
I1227 09:44:55.516555   85427 version.go:256] remote version is much newer: v1.32.0; falling back to: stable-1.29
[init] Using Kubernetes version: v1.29.12
[preflight] Running pre-flight checks
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local master-node] and IPs [10.96.0.1 10.129.0.16 84.201.164.45]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [localhost master-node] and IPs [10.129.0.16 127.0.0.1 ::1]
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [localhost master-node] and IPs [10.129.0.16 127.0.0.1 ::1]
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "super-admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
[control-plane] Creating static Pod manifest for "kube-scheduler"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Starting the kubelet
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests". This can take up to 4m0s
[apiclient] All control plane components are healthy after 16.501460 seconds
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config" in namespace kube-system with the configuration for the kubelets in the cluster
[upload-certs] Skipping phase. Please see --upload-certs
[mark-control-plane] Marking the node master-node as control-plane by adding the labels: [node-role.kubernetes.io/control-plane node.kubernetes.io/exclude-from-external-load-balancers]
[mark-control-plane] Marking the node master-node as control-plane by adding the taints [node-role.kubernetes.io/control-plane:NoSchedule]
[bootstrap-token] Using token: dvtmhx.zy812di1g5hp9nt5
[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] Configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] Configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
[kubelet-finalize] Updating "/etc/kubernetes/kubelet.conf" to point to a rotatable kubelet client certificate and key
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 10.129.0.16:6443 --token dvtmhx.zy812di1g5hp9nt5 \
        --discovery-token-ca-cert-hash sha256:ef930918689cd5f12be54e4c6bcdcda3da08af1ac27af5df52da3484135ca3b9
```

```
user@worker-node-3:~$ sudo kubeadm join 10.129.0.16:6443 --token dvtmhx.zy812di1g5hp9nt5         --discovery-token-ca-cert-hash sha256:ef930918689cd5f12be54e4c6bcdcda3da08af1ac27af5df52da3484135ca3b9
[preflight] Running pre-flight checks
[preflight] Reading configuration from the cluster...
[preflight] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -o yaml'
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Starting the kubelet
[kubelet-start] Waiting for the kubelet to perform the TLS Bootstrap...

This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.

user@worker-node-3:~$
```

```
user@master-node:~$ kubectl get nodes
NAME            STATUS   ROLES           AGE     VERSION
master-node     Ready    control-plane   3h12m   v1.29.10
worker-node-1   Ready    <none>          12m     v1.29.10
worker-node-2   Ready    <none>          12m     v1.29.10
worker-node-3   Ready    <none>          11m     v1.29.10
worker-node-4   Ready    <none>          10m     v1.29.10
```

```
user@master-node:~$  kubectl get po -A
NAMESPACE     NAME                                  READY   STATUS              RESTARTS   AGE
kube-system   coredns-76f75df574-dhpcb              0/1     ContainerCreating   0          3h12m
kube-system   coredns-76f75df574-msqcj              0/1     ContainerCreating   0          3h12m
kube-system   etcd-master-node                      1/1     Running             0          3h12m
kube-system   kube-apiserver-master-node            1/1     Running             0          3h12m
kube-system   kube-controller-manager-master-node   1/1     Running             0          3h12m
kube-system   kube-proxy-cb9g9                      1/1     Running             0          12m
kube-system   kube-proxy-cwf4f                      1/1     Running             0          11m
kube-system   kube-proxy-djdx2                      1/1     Running             0          13m
kube-system   kube-proxy-kmp6f                      1/1     Running             0          3h12m
kube-system   kube-proxy-pnrrv                      1/1     Running             0          12m
kube-system   kube-scheduler-master-node            1/1     Running             0          3h12m
```

1. Подготовка работы кластера из 5 нод: 1 мастер и 4 рабочие ноды.
2. В качестве CRI — containerd.
3. Запуск etcd производить на мастере.
4. Способ установки выбрать самостоятельно.

## Дополнительные задания (со звёздочкой)

**Настоятельно рекомендуем выполнять все задания под звёздочкой.** Их выполнение поможет глубже разобраться в материале.   
Задания под звёздочкой необязательные к выполнению и не повлияют на получение зачёта по этому домашнему заданию. 

------
### Задание 2*. Установить HA кластер

1. Установить кластер в режиме HA.
2. Использовать нечётное количество Master-node.
3. Для cluster ip использовать keepalived или другой способ.

### Правила приёма работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl get nodes`, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.
