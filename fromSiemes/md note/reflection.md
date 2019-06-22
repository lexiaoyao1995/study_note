### 反射

#### Class的两种常用构造方法

pojo Person

~~~java
package demo;

public class Person {
	static {
		System.out.println("这个是静态代码");
	}
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
	
	public Person() {
		System.out.println("构造方法");
	}
	public void speak() {
		System.out.println("speak");
	}
	@Override
	public String toString() {
		return "Person [name=" + name + ", age=" + age + "]";
	}
	
}

~~~

~~~java
package demo;

public class Main {


    public static void main(String[] args) throws Exception {
        Class class1 = Person.class;//不会执行Person静态代码

        Class class2 = Class.forName("demo.Person");//会执行Person静态代码
        Person person1 = (Person) class1.newInstance();
        person1.speak();
    }

}

~~~

#### Method

~~~java
public static void main(String[] args) throws Exception {
	
		Class class2 = Class.forName("demo.Person");//会执行Person静态代码
		Method[] methods = class2.getMethods();
		for (Method method : methods) {
			String name = method.getName();
			//System.out.println(name);
		}
		
		Method method = class2.getDeclaredMethod("speak");
		method.invoke(class2.newInstance());
	}

~~~





