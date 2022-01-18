
## Docker Desktop Alternatives.

TLDR; If its legal and viable please continue to use Docker Desktop and sponsor their developers. If you are part of business that is not paying for the use seat then this guide would be helpful.

https://www.docker.com/pricing
The Docker Subscription Service Agreement has been updated.

The [Docker Subscription Service Agreement](https://www.docker.com/legal/docker-subscription-service-agreement) includes a change to the terms for Docker Desktop

- It remains free for small businesses (fewer than 250 employees AND less than $10 million in annual revenue), personal use, education, and non-commercial open source projects.

- It requires a paid subscription (Pro, Team or Business), for as little as $5 per user per month, for professional use in larger businesses.

- The effective date of these terms is August 31, 2021. There is a grace period until **January 31, 2022** for those that will require a paid subscription to use Docker Desktop.

- The Docker Pro, Docker Team, and Docker Business subscriptions now include commercial use of Docker Desktop.
Check out the [FAQ](https://www.docker.com/pricing/faq) for more information. Or read the [latest blog](https://www.docker.com/blog/updating-product-subscriptions/).


## Alternatives
This instruction have been tested on macOS Mojave.
To be able to run docker or any container runtime on macOS, you would end up using a Linux Virtual Machine (VM).

All alternatives provide a way to build, create, and run containers on a Linux VM.

- [Podman](https://github.com/containers/podman)
- [Rancher Desktop](https://github.com/rancher-sandbox/rancher-desktop)
- [Minikube](https://github.com/kubernetes/minikube)
- [Lima/Nerdctl VM](https://github.com/containerd/nerdctl)
- [buildkit-machine](https://github.com/developer-guy/buildkit-machine)
- Ubuntu Multipass VM
- Vagrant VM



### Podman

The Mac client is available through Homebrew:

```
brew install podman
```

To start the Podman-managed VM:
```
podman machine init
podman machine start
podman machine list
```

You can then verify the installation information using:
```
podman info
```

Run nginx
```
podman run --rm -p 8080:8080 --network bridge quay.io/bitnami/nginx
```

Install podman-compose
```
pip3 install https://github.com/containers/podman-compose/archive/devel.tar.gz
```

>Notes
Using `Ctrl+C` doesn't stop and delete containers, you need to follow up with `podman ps` or `podman-compose down`

### Rancher Desktop

Download from https://github.com/rancher-sandbox/rancher-desktop/releases and move to Applications.

Double click on Applications and grant access to update network settings.

Go to Supporting Utilities and check the box for `/usr/local/bin/nerdctl`

Rancher Desktop provides the ability to build, push, and pull images. You can use contaierd or docker/moby for container runtime. If using containerd you would use `nerdclt` CLI and if you use docker you will use the `docker` CLI. For more information on images see https://docs.rancherdesktop.io/images

```
nerdctl build
nerdctl ps
nerdctl run
```



### Minikube

Install minikube
```
brew install minikube
```

Create minikube vm with profile `docker` with no kubernetes
```
minikube start -p docker --no-kubernetes
```

Use `minikube image` to build images like
```
minikube -p docker image build .
```

Use docker from inside the VM
```
minkube ssh
docker
```

Use docker from outside the VM
```
eval $(minikube docker-env)
```
Then use `docker` CLI

### Lima VM

```
brew install lima
limactl start
lima nerdctl run -d --name nginx -p 127.0.0.1:8080:80 nginx:alpine
```

See https://github.com/lima-vm/lima/tree/master/examples for other Lima VM distros and container runtimes.


### Vagrant VM
### Ubuntu Multipass VfM
