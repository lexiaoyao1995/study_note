### 字符串编码

~~~c#
byte[] sdb8 = System.Text.Encoding.GetEncoding(1252).GetBytes(SDB_8_org);
~~~

1252为编码格式的code

~~~C#
   byte[] sdb8 = System.Text.Encoding.Default.GetBytes(SDB_8_org);
~~~

default与windows的设置的地区关联

~~~c#
Encoding coding = Encoding.Default;
~~~

可以查看当前的coding对象。