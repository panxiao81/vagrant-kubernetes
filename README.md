# Quick Setup a Kubernetes cluster lab Environment with Vagrant and Kubeadm

## Prerequistes

1. Vagrant
2. 8 GiB+ RAM
3. Ansible

## Usage

### For macOS and Linux User

You could install Ansible use package manager or pip.

```sh
# Install Ansible first, You could use a virtual environment

git clone https://github.com/panxiao81/vagrant-kubernetes
cd vagrant-kubernetes/
pip install -r requirements.txt

# You could change variables in provisioning/group_vars/all/all.yml
vim provisioning/group_vars/all/all.yml
vagrant up
```

### For Windows User

Since Ansible cannot use Windows as a controller, I will change the provisioner from `ansible` to `ansible_local` to support windows in the future.

Or you can try to use Vagrant and Ansible in WSL 2, But That's not tested.

## TODO

- [ ] Documentation
- [ ] Switch provisioner to ansible_local
- [ ] Add more network plugin support like calico
- [ ] Add Ingress Controller
- [ ] Add CSI Plugin

## Special Thanks To

- [Vagrant](https://www.vagrantup.com/) by Hashicorp
- [Ansible](https://www.ansible.com/) by Red Hat
- [Kubernetes](https://kubernetes.io/) by CNCF
- [Kubespray](https://github.com/kubernetes-sigs/kubespray)
