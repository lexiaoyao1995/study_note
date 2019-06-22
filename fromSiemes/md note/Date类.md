### 概述

Date类负责时间的表示。利用从1970.1.1 00:00:00到当前时间的毫秒值计时。

Calender类是一个工具类，负责对Date类进行修改等操作，以及从Date类中提取年月日等时间的特定信息。

DateFormat类负责时间的转换，比如读取特定格式的字符串，转换成Date对象，或者将Date对象按照指定的格式转换成字符串。

SimpleDateFormat是转换字符串和Date对象最常用的类。

~~~java
public static void main(String[] args) throws Exception {


		Date date = new Date();
		
		Calendar calendar = Calendar.getInstance();
		calendar.setTime(date);
	
		int i = calendar.get(Calendar.YEAR);
		int j = calendar.get(Calendar.MONTH);
		
		SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd");
		String format = simpleDateFormat.format(date);//格式化时间
		String dateString = "2015-7-10";
		
		
		Date date2 = simpleDateFormat.parse(dateString);//解析时间
		
		
		System.out.println(date);
		System.out.println("year is "+i);
		System.out.println("mouth is "+j);
		System.out.println(format);
		System.out.println(date2);
		
	}
~~~

>Tue Dec 18 16:07:43 GMT 2018
>year is 2018
>mouth is 11
>2018-12-18
>Fri Jul 10 00:00:00 BST 2015