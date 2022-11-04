# CentOS 7

## 配置国内 yum 源

[阿里云官方镜像站](https://developer.aliyun.com/mirror/ "aliyun")

### 1. 备份

```bash
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

### 2. 下载阿里云源

#### centos6

```bash
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-6.repo
```

#### centos7

```bash
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
```

#### centos8

```bash
wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo
```

### 3. 生成缓存

```bash
# yum clean all

# yum makecache
```
