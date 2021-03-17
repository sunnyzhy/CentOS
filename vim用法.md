# vim 用法

## 编辑
按 i 键

## 退出编辑
1. 按 esc 键
2. 退出并保存 :wq
3. 退出不保存 :q!
4. 退出 :q 

## 查找字符串
在非编辑模式，输入 /find_str

## 撤销
在非编辑模式，按 u 键撤销，按 ctrl + r 反撤销。

## Another program may be editing the same file
解决方法：
根据提示 Found a swap file by the name "xx.swp"

```bash
# rm -fr xx.swp
```
