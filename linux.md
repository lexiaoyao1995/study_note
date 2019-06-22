### 如何查找特定的文件

面试里常用的方式

1、find ~ -name "target3.java" ：精确查找文件

2、find ~ -name "target*" : 模糊查询文件

3、find ~ -iname “target*” ：不区分大小写

4、man find  关于find指令的使用说明



### 检索文件内容

grep   查找文件里符合条件的字符串



grep 'contern' path  在path里查找包含的字段

grep -o '[0-9]' 可使用正则表达

grep -v 'con' 过滤掉，不显示



### 对文件内容做统计

awk



### 批量替换文本内容

sed