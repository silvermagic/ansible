### 说明

本文档使用docker-compose来自动构建kolla-ansible部署openstack环境的部署节点，docker使用host网络，所以请确保host网段和openstack节点网段相同

### 目将录结构

```
### 目录树
# tree -L 2
.
├── docker-compose.yml
├── kolla
│   ├── Dockerfile
│   ├── nginx.repo
│   ├── rpms
│   └── wheels
├── README.md
└── registry
    └── Dockerfile
```

### 制作yum本地源

```
### 将需要做成yum源的软件包放入"kolla/rpms"目录，yum本地源默认url路径为"http://<deploy ip>/rpms"
```

### 构建Wheels包

```
# pip install wheel
# git clone https://github.com/openstack/kolla-ansible.git -b stable/ocata
# cd kolla-ansible
# pip wheel --wheel-dir=../kolla/wheels .
```

### 构建docker源

```
### 在host主机上创建目录用于存放docker源文件，kolla-ansible需要的docker源文件可以使用kolla-build编译或直接下载现成的
# mkdir -p /opt/registry
# tar zxf centos-source-registry-ocata.tar.gz -C /opt/registry
```

### 编辑kolla-ansible配置文件

```
# vim kolla-ansible/etc/globals.yml
# vim kolla-ansible/ansible/inventory/multinode
```

### 启动容器

```
# docker-compose up
```

### 执行kolla-ansible

```
# docker exec -it kolla bash
# kolla-genpwd
# kolla-ansible -i /inventory/multinode deploy
```
