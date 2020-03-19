# Kubernetes Setup Using Ansible and Vagrant

## From

`https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/`

## To Run

- `vagrant up`

## To Stop

- `vagrant destroy -f`

## To Access

- `vagrant ssh <node>`

## Patches

### Metrics Server

```bash
- vagrant ssh k8s-master
- git clone https://github.com/kubernetes-sigs/metrics-server.git
- vi deploy/kubernetes/metrics-server-deployment.yaml (source: https://github.com/kubernetes-sigs/metrics-server/issues/278)
  (+) - hostNetwork: true
  (+) - restartPolicy: Always
  - containers
    - args:
      (+) - --kubelet-insecure-tls
      (+) - --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
      (+) - --metric-resolution=30s
```