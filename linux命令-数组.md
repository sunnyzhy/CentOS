# linux 命令 - 数组

## 判断数组是否包含某个元素

方法1：

```bash
#!/bin/sh

dir=/usr/local
array=($dir/*)
var=$dir"/etc"

echo "${array[@]}" | grep -wq "$var" &&  echo "yes" || echo "no"
```

方法2：

```bash
#!/bin/sh

dir=/usr/local
array=($dir/*)
var=$dir"/etc"

for i in ${array[@]}
do
        if [ $i == $var  ]
        then
                echo "yes"
                break
        fi
done
```

方法3：

**判断删除 $var 后的数组是否与原数组相同，不同则表明包含该元素；相同（没有 $var 可删除）则表明不包含该元素。**

```bash
#!/bin/sh

dir=/usr/local
array=($dir/*)
var=$dir"/etc"

if [[ ${array[@]/$var/} != ${array[@]} ]]
then
        echo "yes"
else
        echo "no"
fi
```
