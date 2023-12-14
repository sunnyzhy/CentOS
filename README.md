# CentOS

## 背景信息

- CentOS 系统每个大版本的维护期为 10 年
- CentOS Linux 7 作为 RHEL 7 的复刻版本于 2020 年 08 月 06 日停止更新，但会延续当前的支持计划，于 2024 年 06 月 30 日停止维护（EOL）
- CentOS Linux 8 作为 RHEL 8 的复刻版本，生命周期缩短，于 2021 年 12 月 31 日停止更新并停止维护（EOL）
- CentOS 官方不再提供 CentOS Linux 9 及后续版本，而是提供 CentOS Stream 版本

## CentOS 的变更历史

CentOS 处于红帽生态链的最下游，即 ```Fedora → RHEL → CentOS```。Fedora 作为新功能的试验场，其成果被收入以稳定性著称的 RHEL（Red Hat Enterprise Linux，红帽企业级操作系统）中，但使用 RHEL 是需要付出高昂的订阅费用的；而 CentOS 是依据开源协议，从 RHEL 源代码中去除商标部分后重新编译而成的系统，既继承了 RHEL 的优秀特性，又是完全免费的。换言之，真正好用的是红帽系统，而 CentOS 是它的免费替代品。

红帽在收购了 CentOS 项目后，随着 CentOS 更名为 CentOS Stream，它在生态链中的位置变成了 ```Fedora → CentOS Stream → RHEL```，即 CentOS Stream 反过来成为了 RHEL 的试验场，它仍然是一个可用的操作系统，却不再有以前那样能与 RHEL 比肩的稳定性了。红帽官方建议 CentOS 用户升级到 CentOS Stream，但也声明了并非为生产环境设计。

## CentOS 的替代产品

- ```Rocky Linux```: 由 CentOS 项目的原创始人 Gregory Kurtzer 启动的新项目
- ```AlmaLinux```: 由 CloudLinux 公司创建
- ```Oracle Linux```: 由甲骨文公司推出

```Rocky Linux``` 和 ```AlmaLinux``` 的定位相似，是以 100% 兼容原 CentOS 系统为目标的，而 ```Oracle Linux``` 包含甲骨文自己的功能改进，并提供付费的商业支持。
