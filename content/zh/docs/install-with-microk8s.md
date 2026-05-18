# 使用 klts 替换 Canonical MicroK8s 的 kubelet

## 环境准备

**操作系统**: CentOS 7

**K8s 版本**: 1.19

## 获取 kubelet 二进制文件

```bash
$ wget https://github.com/klts-io/kubernetes-lts/raw/rpm-v1.19.16-lts.1/x86_64/kubelet-1.19.16-lts.1.x86_64.rpm

cp ./usr/bin/kubelet kubelet-1.19.16-lts.bin
```

## 获取 api-server 二进制文件

## 下载并解压 snap 文件

```bash
$ snap download microk8s --channel=1.19/stable
Fetching snap "microk8s"
Fetching assertions for "microk8s"
Install the snap with:
   snap ack microk8s_2530.assert
   snap install microk8s_2530.snap
   
$ ls -1 .
microk8s_2530.assert  
microk8s_2530.snap
kubelet-1.19.16-lts.bin
```
## 替换二进制文件
```bash
$ unsquashfs microk8s_2530.snap
Parallel unsquashfs: Using 8 processors
4112 inodes (10516 blocks) to write
...
created 3896 files
created 478 directories
created 212 symlinks
created 0 devices
created 0 fifos

$ ls .
kubelet-1.19.16-lts.bin
microk8s_2530.assert
microk8s_2530.snap
squashfs-root

$ mv squashfs-root/kubelet .squashfs-root/kubelet.bak
$ cp kubelet-1.19.16-lts.bin squashfs-root/kubelet
$ ls -lh squashfs-root/kubelet*
-rwxr-xr-x 1 root root 109M Dec 24 09:45 squashfs-root/kubelet
-rwxr-xr-x 1 root root 106M Sep 28 07:56 squashfs-root/kubelet.bak
```

## 压制 snap 文件

```bash
$ mksquashfs squashfs-root microk8s_2530_lts.snap
Parallel mksquashfs: Using 8 processors
Creating 4.0 filesystem on microk8s_2530_lts.snap, block size 131072.


Exportable Squashfs 4.0 filesystem, gzip compressed, data block size 131072
	compressed data, compressed metadata, compressed fragments, compressed xattrs
	duplicates are removed
Filesystem size 287906.33 Kbytes (281.16 Mbytes)
	29.37% of uncompressed filesystem size (980256.53 Kbytes)
Inode table size 66984 bytes (65.41 Kbytes)
	37.48% of uncompressed inode table size (178697 bytes)
Directory table size 46934 bytes (45.83 Kbytes)
	45.58% of uncompressed directory table size (102960 bytes)
Number of duplicate files found 337
Number of inodes 4587
Number of files 3897
Number of fragments 345
Number of symbolic links  212
Number of device nodes 0
Number of fifo nodes 0
Number of socket nodes 0
Number of directories 478
Number of ids (unique uids + gids) 1
Number of uids 1
	root (0)
Number of gids 1
	root (0)
    
$ ls -1.
kubelet-1.19.16-lts.bin
microk8s_2530.assert
microk8s_2530.snap
microk8s_2530_lts.snap
squashfs-root
```

## 安装本地 snap 文件

<p class="callout warning">因为没有 signature, 所以只能加 --dangerous 参数强制安装</p>

```bash
$ snap ack microk8s_2530.assert

$ snap install microk8s_2530_lts.snap --classic --dangerous
microk8s v1.19.15 installed

$ microk8s kubectl get no
NAME       STATUS     ROLES    AGE   VERSION
master-1   NotReady   <none>   50s   v1.19.16-lts.1
```
参考 [1. 部署单机](https://docs.piraeus.daocloud.io/books/microk8s/page/1) 修改 Mirror 后

```bash
$ kubectl get no
NAME                             STATUS   ROLES    AGE   VERSION
jump.internal.chinacloudapp.cn   Ready    <none>   13m   v1.19.16-lts.1

$ snap services microk8s | grep -w active
microk8s.daemon-apiserver             enabled  active    -
microk8s.daemon-apiserver-kicker      enabled  active    -
microk8s.daemon-cluster-agent         enabled  active    -
microk8s.daemon-containerd            enabled  active    -
microk8s.daemon-control-plane-kicker  enabled  active    -
microk8s.daemon-controller-manager    enabled  active    -
microk8s.daemon-kubelet               enabled  active    -
microk8s.daemon-proxy                 enabled  active    -
microk8s.daemon-scheduler             enabled  active    -
```
