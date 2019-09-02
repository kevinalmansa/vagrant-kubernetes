# vagrant-kubernetes
Vagrant configuration for Kind Kubernetes. This will configure and start
a 3 node Kubernetes cluster (docker-in-docker) using Kind.

The configuration can be expanded by modifying the Kind & Kubeadm config
within the Kind role.

## Requirements

To successfully run this, you must have installed on your host:
- Vagrant
- Vagrant Disk Size plugin
- Vagrant Reload

Ansible will run 'locally' in the VM and thus is not needed on the host.

To install Vagrant Disk Size plugin, run:

```sh
$ vagrant plugin install vagrant-disksize
```

To install Vagrant Reload, run:

```sh
$ vagrant plugin install vagrant-reload
```

## Provisioning

This machine has two provisioning scripts:
- Base
- Kubernetes

The base will install all dependencies such as golang, docker, kubectl. Kubernetes
will install Kind and run any role required for configuring the Kubernetes cluster.

This was required due to running Ansible in a local connection and not being
able to refresh the connection when adding a user to the docker group.

## How-To

Clone the repo and run the following command from within the repo:

```sh
$ vagrant up
```

That's it. You can now SSH into the machine and run kubectl:

```sh
$ vagrant ssh
$ export KUBECONFIG="$(kind get kubeconfig-path)"
$ kubectl cluster-info
```

To delete the VM:

```sh
$ vagrant destroy
```

## Logging

https://www.digitalocean.com/community/tutorials/how-to-set-up-an-elasticsearch-fluentd-and-kibana-efk-logging-stack-on-kubernetes

## Helm

Tiller is installed as cluster-admin role to allow it to install and remove services.

To initialize helm:

```sh
helm init --service-account tiller --history-max 200
```
