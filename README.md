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
