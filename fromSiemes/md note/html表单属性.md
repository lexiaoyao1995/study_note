### enctype

enctype属性规定在发送到服务器之前应该如何对表单进行编码

| 值                                | 描述                                                       |
| --------------------------------- | ---------------------------------------------------------- |
| application/x-www-form-urlencoded | 在发送前编码所有字符（默认）                               |
| multipart/form-data               | 不对字符编码。在使用包含文件上传控件的表单时，必须使用改值 |
| text/plain                        | 空格转换为“+”加号，但不对特殊字符编码                      |

### 表单元素

1、 文本类

~~~html
<input type = "text">
<input type = "password">
<input type = "hidden">
<textarea></textarea>
~~~

2、按钮类

~~~html
<input type="button" value="text"/>
<input type="submit" value="提交"/>
<input type="reset" value="text"/>
<input type="image"/>图片按钮
~~~

3、选择类

~~~html
<input type="radio">
<input type="check">
<select>
    <option val=“1”></option>
</select>
~~~

