### Hash规则的集合是如何判断是否重复的

两个条件：

1、hashcode相等

2、equals返回为true

必须同时满足才存不进去

~~~java
package d12;

public class Person {
	private String name;
	private int age;
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	@Override
	public boolean equals(Object obj) {
		// TODO Auto-generated method stub
		return true;
	}
	@Override
	public int hashCode() {
		// TODO Auto-generated method stub
		return 1;
		//return (int) Math.floor(Math.random()*100);
	}	
}
~~~

### 关于重写HashCode和equals

结论：一般是同时重写HashCode和equals

在集合查找时，hashcode能大大降低对象比较次数，提高查找效率

1、相同的对象（equals为true）必须具有相等的hashcode

2、hashcode相同的对象，不一定equals为true