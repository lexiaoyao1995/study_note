### 关于深拷贝和浅拷贝

深拷贝就是对象里面的对象也有完整的拷贝体。

浅拷贝就是对象里面的对象只是简单地引用，只有一个成员类的实例。所以改变一个成员类，其他的也会变

~~~java
package demo1;

public class Address implements Cloneable {

	private String city;
	private String street;

	public String getCity() {
		return city;
	}

	public void setCity(String city) {
		this.city = city;
	}

	public String getStreet() {
		return street;
	}

	public void setStreet(String street) {
		this.street = street;
	}

	@Override
	protected Object clone() throws CloneNotSupportedException {
		// TODO Auto-generated method stub
		return super.clone();
	}

	@Override
	public String toString() {
		return "Address [city=" + city + ", street=" + street + "]";
	}

}



package demo1;

public class Person implements Cloneable {
	private String name;
	private Integer age;
	private Address address;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Integer getAge() {
		return age;
	}

	public void setAge(Integer age) {
		this.age = age;
	}

	public Address getAddress() {
		return address;
	}

	public void setAddress(Address address) {
		this.address = address;
	}

	@Override
	public String toString() {
		return "Person [name=" + name + ", age=" + age + ", address=" + address + "]";
	}

	@Override
	public Person clone() throws CloneNotSupportedException {
		Person cloned = (Person) super.clone();
		cloned.address = (Address) address.clone();
		return cloned;
	}

	public Person(String name, Integer age) {
		super();
		this.name = name;
		this.age = age;
	}

}



package demo1;

public class Main {

	public static void main(String[] args) throws CloneNotSupportedException {
		Person p1 = new Person("qwe",16);
		Address address = new Address();
		address.setCity("chengdu");
		address.setStreet("street");
		p1.setAddress(address);
		
		Person clone = (Person) p1.clone();
		
		p1.setAge(10);
		address.setCity("we");
        //改变p1不会影响clone对象
		System.out.println(p1);
		System.out.println(clone);
		
	}
}

~~~

~~~tex
Person [name=qwe, age=10, address=Address [city=we, street=street]]
Person [name=qwe, age=16, address=Address [city=chengdu, street=street]]
~~~

​	上述代码是深拷贝，每一个Person对象都有单独的address对象，所有第二个Person的address不会改变。浅拷贝就会改变。