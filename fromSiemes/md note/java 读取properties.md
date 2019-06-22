### Java 读取properties

其中一种实用的方法

![](IMG/Captasdure.PNG)

~~~java
package demo1;

import java.util.ResourceBundle;

public class Main1 {

	public static void main(String[] args) {
		ResourceBundle resourceBundle = ResourceBundle.getBundle("test");
		String string = resourceBundle.getString("name");
		String string2 = resourceBundle.getString("age");
		String string3 = resourceBundle.getString("city");
		
		
		System.out.println(string);
		System.out.println(string2);
		System.out.println(string3);
		
		
	}
}

~~~

~~~tex
name=root
age=18
city=chengdu
~~~



~~~java
package demo1;

import java.util.ResourceBundle;

public class Utils {

	private static ResourceBundle resourceBundle = ResourceBundle.getBundle("test");

	public static String getName() {
		return resourceBundle.getString("name");
	}

	public static int getAge() {

		String string = resourceBundle.getString("age");

		Integer valueOf = Integer.valueOf(string);
		return valueOf;

	}

}

~~~

