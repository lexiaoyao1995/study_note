~~~java
package observerDemo;

public class Main {

	public static void main(String[] args) throws Exception {
		new Main().new B().name();
	}

	interface A {
		public default void name() {
			System.out.println("def");
		};

		public static void name1() {
			System.out.println("asd");
		}
	}

	class B implements A {

	}

}
~~~

在jdk1.8中，接口可以有默认default方法体，以及静态方法的实现