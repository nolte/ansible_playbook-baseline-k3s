# K3S Baseline Installation

Simple Playbook for Quick [rancher/k3s](https://github.com/rancher/k3s) installation, use the Glaxy Role [PyratLabs/ansible-role-k3s](https://github.com/PyratLabs/ansible-role-k3s).Using [Ansible](https://ansible.com),[packer.io](https://www.packer.io) and [Vagrant](https://www.vagrantup.com).

## Motivation

For the different Services like [nolte/personal-storage-infrastructure](https://github.com/nolte/personal-storage-infrastructure) or [nolte/minecraft-infrastructure](https://github.com/nolte/minecraft-infrastructure), i need a new and a little bit more Flexible Environment like "VirtualMachines".

For Development we need a Lightweight infrastructure, so we split the Installation and Configuration in two Different Parts. First the Basement [k3s](https://k3s.io/), on a prepared Host for the preparation we use a commons Playbook like [nolte/ansible_playbook-baseline-online-server](https://github.com/nolte/ansible_playbook-baseline-online-server). This Baseline can be package with [packer.io](https://www.packer.io), to a reuseable Vagrant Box.

The Baseline Box will be used for testing different sets of Services, like [prometheus](https://prometheus.io/) or [keycloak](https://www.keycloak.org/) in a seperated Environment. Usefull for Testing new Tools or Deployment ways.

## Usage

### Local Vagrant Box

The Local Vagrant box is a good way for develop new Box versions. 

```bash
vagrant ssh k3snode
```

```bash
new_ip=$(vagrant ssh -c "ip address show eth0 | grep 'inet ' | sed -e 's/^.*inet //' -e 's/\/.*$//'")
```


### Package a Vagrant Box

You can create a reuseable Vagrant box with [packer.io](https://www.packer.io/), this makes it easy to start different Projects with the same basement. 

```bash
cd local
packer build k3s-node.json
```

### Depends with vendir

```sh
vendir sync
```
