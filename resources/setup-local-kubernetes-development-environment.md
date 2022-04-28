---
description: How to setup a local development environment for Kubernetes using K3S.
---

# Setup Local Kubernetes Development Environment

## Requirements

- We assume kubectl is already installed on the local machine

## Install K3S

First of all, to be able to develop for Kubernetes, we need to install its lightweight cousin called K3S [as documented on its website](https://k3s.io/):

```shell
curl -sfL https://get.k3s.io | sh -
```

## Configure K3S

Since we are going to use k3s for local development, its fine to enable access for the current logged in user additionaly to root. To do so, we set the `K3S_KUBECONFIG_MODE` environment variable for the K3S daemonj to `644`:

```shell
# Add custom configuration for k3s:
$ sudo systemctl edit k3s

# Type the lines below into the editor, save and close when your done.
# This will write to /etc/systemd/system/k3s.service.d/override.conf:
[Service]
Environment="K3S_KUBECONFIG_MODE=644"

# Make sure to restart k3s after this configuration change:
$ sudo systemctl restart k3s
```

Finally, I'll like to start k3s only on demand, therefore I'm disabling the autostart at boot time:

```shell
sudo systemctl disable k3s
```

## Test connection to K3S

Now everything is in place and you should be able to connect to K3s:

```shell
$ k3s kubectl get namespaces
NAME              STATUS   AGE
default           Active   20m
kube-system       Active   20m
kube-public       Active   20m
kube-node-lease   Active   20m
```

## Integrate with kubectl and K9S

To make things easier to work with, you can add the local k3s connection to the default kubectl configuration file.
This allows even third party tools such as [K9S](https://k9scli.io/) to manage your local deployment without any further configuration needed.

To do so, copy the following parts from the `/etc/rancher/k3s/k3s.yaml` to the `~/.kube/config` file - and make sure to change the name from `default` to `k3s-local` to avoid any future confusion:

```yaml
# /etc/rancher/k3s/k3s.yaml
#clusters:
- cluster:
    server: https://127.0.0.1:6443
    certificate-authority-data: ...
  name: k3s-local
#contexts:
- context:
    cluster: k3s-local
    user: k3s-local
  name: k3s-local
#users:
users:
- name: k3s-local
  user:
    client-certificate-data: ...
    client-key-data: ...
```

Now you can test if everything still works with:

```shell
$ kubectl get namespaces
NAME              STATUS   AGE
default           Active   100m
kube-system       Active   100m
kube-public       Active   100m
kube-node-lease   Active   100m
```

You should now also be able to connect to the local k3s using any other tool - for example K9S. Please note: If you are executing K9S using the Docker container, you also want to set the `--net=host` flag so it actually can connect to the k3s running on the host (outside of Docker):

```shell
docker run --rm -it -v ~/.kube/config:/root/.kube/config --net=host quay.io/derailed/k9s
```