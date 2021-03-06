![Kubernetes Logo](https://s28.postimg.org/lf3q4ocpp/k8s.png)

##Deploy a production ready kubernetes cluster

If you have questions, join us on the [kubernetes slack](https://slack.k8s.io), channel **#kargo**.

- Can be deployed on **AWS, GCE, Azure, OpenStack or Baremetal**
- **High available** cluster
- **Composable** (Choice of the network plugin for instance)
- Support most popular **Linux distributions**
- **Continuous integration tests**


To deploy the cluster you can use :

[**kargo-cli**](https://github.com/kubespray/kargo-cli) <br>
**Ansible** usual commands and [**inventory builder**](https://github.com/kubernetes-incubator/kargo/blob/master/contrib/inventory_builder/inventory.py) <br>
**vagrant** by simply running `vagrant up` (for tests purposes) <br>


*  [Requirements](#requirements)
*  [Kargo vs ...](docs/comparisons.md)
*  [Getting started](docs/getting-started.md)
*  [Ansible inventory and tags](docs/ansible.md)
*  [Deployment data variables](docs/vars.md)
*  [DNS stack](docs/dns-stack.md)
*  [HA mode](docs/ha-mode.md)
*  [Network plugins](#network-plugins)
*  [Vagrant install](docs/vagrant.md)
*  [CoreOS bootstrap](docs/coreos.md)
*  [Downloaded artifacts](docs/downloads.md)
*  [Cloud providers](docs/cloud.md)
*  [OpenStack](docs/openstack.md)
*  [AWS](docs/aws.md)
*  [Azure](docs/azure.md)
*  [Large deployments](docs/large-deployments.md)
*  [Upgrades basics](docs/upgrades.md)
*  [Roadmap](docs/roadmap.md)

Supported Linux distributions
===============

* **Container Linux by CoreOS**
* **Debian** Jessie
* **Ubuntu** 16.04
* **CentOS/RHEL** 7

Note: Upstart/SysV init based OS types are not supported.

Versions of supported components
--------------------------------

[kubernetes](https://github.com/kubernetes/kubernetes/releases) v1.5.1 <br>
[etcd](https://github.com/coreos/etcd/releases) v3.0.6 <br>
[flanneld](https://github.com/coreos/flannel/releases) v0.6.2 <br>
[calicoctl](https://github.com/projectcalico/calico-docker/releases) v0.23.0 <br>
[canal](https://github.com/projectcalico/canal) (given calico/flannel versions) <br>
[weave](http://weave.works/) v1.8.2 <br>
[docker](https://www.docker.com/) v1.12.5 <br>
[rkt](https://coreos.com/rkt/docs/latest/) v1.21.0 <br>

Note: rkt support as docker alternative is limited to control plane (etcd and
kubelet). Docker is still used for Kubernetes cluster workloads and network
plugins' related OS services. Also note, only one of the supported network
plugins can be deployed for a given single cluster.

Requirements
--------------

* The target servers must have **access to the Internet** in order to pull docker images.
* The **firewalls are not managed**, you'll need to implement your own rules the way you used to.
in order to avoid any issue during deployment you should disable your firewall.
* The target servers are configured to allow **IPv4 forwarding**.
* **Copy your ssh keys** to all the servers part of your inventory.
* **Ansible v2.2 (or newer) and python-netaddr**


## Network plugins
You can choose between 4 network plugins. (default: `calico`)

* [**flannel**](docs/flannel.md): gre/vxlan (layer 2) networking.

* [**calico**](docs/calico.md): bgp (layer 3) networking.

* [**canal**](https://github.com/projectcalico/canal): a composition of calico and flannel plugins.

* **weave**: Weave is a lightweight container overlay network that doesn't require an external K/V database cluster. <br>
(Please refer to `weave` [troubleshooting documentation](http://docs.weave.works/weave/latest_release/troubleshooting.html)).

The choice is defined with the variable `kube_network_plugin`. There is also an
option to leverage built-in cloud provider networking instead.
See also [Network checker](docs/netcheck.md).

## CI Tests

![Gitlab Logo](https://s27.postimg.org/wmtaig1wz/gitlabci.png)

[![Build graphs](https://gitlab.com/kargo-ci/kubernetes-incubator__kargo/badges/master/build.svg)](https://gitlab.com/kargo-ci/kubernetes-incubator__kargo/pipelines) </br>

CI/end-to-end tests sponsored by Google (GCE), and [teuto.net](https://teuto.net/) for OpenStack.
See the [test matrix](docs/test_cases.md) for details.
