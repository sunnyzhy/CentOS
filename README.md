# CentOS 7
## 配置国内 yum 源
[阿里云官方镜像站](https://developer.aliyun.com/mirror/ "aliyun")

### 1. 备份
```bash
# mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

### 2. 下载新的 CentOS-Base.repo 到 /etc/yum.repos.d/
```bash
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
```

### 3. 生成缓存
```bash
# yum clean all

# yum makecache
```
