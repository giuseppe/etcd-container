# etcd-container

Building etcd container for rhel, centos and atomic host:

```
# git clone https://github.com/aveshagarwal/etcd-container
# cd etcd-container
# docker build --rm -t etcd .
```
**Instructions for RHEL and CentOS**

Running etcd container

```
#docker run -d -p 4001:4001 -p 7001:7001 -p 2379:2379 -p 2380:2380 etcd
```

**Instructions for Atomic**

Installing etcd container on atomic host:

```
#atomic install etcd
```

Running etcd container on atomic host:

```
#atomic run etcd
```

Stopping etcd container on atomic host:

```
#atomic stop etcd
```

Uninstalling etcd container on atomic host:

```
#atomic uninstall etcd
```
# Running etcd container with runc

Create a top level `etcd-runc-container` directory

```
mkdir etcd-runc-container
cd etcd-runc-container
```

If etcd-container image is not already built with docker

```
# git clone https://github.com/aveshagarwal/etcd-container
# docker build --rm -t etcd etcd-container/
```
Create a tar of etcd container

```
docker export $(docker create etcd) > etcd.tar
```

Untar etcd.tar in rootfs dir 

```
mkdir rootfs
tar -C rootfs -xf etcd.tar
```

Copy `exports/config.json.template` to etcd-runc-container

```
cp rootfs/exports/config.json.template config.json
```

Run the etcd container with runc

```
runc start etcd
```
