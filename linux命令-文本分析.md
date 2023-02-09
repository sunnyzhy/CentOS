# linux 命令 - 文本分析

## awk

显示第 n 列:

```bash
awk '{print $n}'
```

显示第 n 行:

```bash
awk 'NR==n{print}'
```

从第 n 行起显示:

```bash
awk 'NR>n{print}'
```

从第 m 行起，显示第 n 列:

```bash
awk 'NR>m{print $n}'
```
