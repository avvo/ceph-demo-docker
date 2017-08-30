# Demo container

This Dockerfile may be used to bootstrap a Ceph cluster with all the Ceph daemons running.

**/!\ THIS CONTAINER IS NOT RECOMMENDED FOR PRODUCTION USAGE /!\**

The main purpose of this container is to quickly get a Ceph cluster up and running by reducing all the setup steps. The container provides all the Ceph daemons, so you can rapidly start playing with Ceph.

## Usage

- `MON_NAME` is the name of the monitor (DEFAULT: hostname)
- `MON_IP` is the IP address of the monitor (public)
- `RGW_NAME` is the name of rados gateway instance (DEFAULT: hostname)
- `RGW_CIVETWEB_PORT` is the port of the rados gateway (DEFAULT: 80)
- `CLUSTER` is the name of the cluster (DEFAULT: ceph)
- `CEPH_PUBLIC_NETWORK` is the network where the OSD should communicate
- `CEPH_DEMO_UID`, `CEPH_DEMO_ACCESS_KEY`, `CEPH_DEMO_SECRET_KEY`, and `CEPH_DEMO_BUCKET` can be used to auto-provision an account.

Commonly, you will want to bind-mount your host's `/etc/ceph` into the container. You'll also want to retain the IP during reboots and upgrades since it's written to the ceph.conf file.

### Docker Compose
```YAML
version: '2'
services:
  ceph:
    image: docker.avvo.com/ceph-demo:luminous
    volumes:
    - /etc/ceph:/etc/ceph
    labels:
      io.rancher.scheduler.affinity:host_label: facing=db
      io.rancher.container.pull_image: always
```

### Rancher Compose
```YAML
version: '2'
services:
  ceph:
    retain_ip: true
```

