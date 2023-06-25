# 安装 firefox

firefox 官网: ```http://www.firefox.com.cn/```

## 卸载 firefox

```bash
# yum remove -y firefox

# whereis firefox
firefox: /usr/lib64/firefox

# rm -rf /usr/lib64/firefox
```

## 安装 firefox

```bash
# tar -xjvf Firefox-latest-x86_64.tar.bz2

# mv firefox /opt

# ln -s /opt/firefox/firefox /usr/local/bin/firefox

# whereis firefox
firefox: /usr/local/bin/firefox
```
