# Quick Setup a Kubernetes cluster lab Environment with Vagrant and Kubeadm

## Prerequistes

1. Vagrant
2. 8 GiB+ RAM
3. Ansible

## Usage

### For macOS and Linux User

You could install Ansible use package manager or pip.

```sh
git clone https://github.com/panxiao81/vagrant-kubernetes
vagrant up
```

### For Windows User

Since Ansible cannot use Windows as a controller, I will change the provisioner from `ansible` to `ansible_local` to support windows.
