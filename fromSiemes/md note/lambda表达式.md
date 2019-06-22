### lambda表达式

本质就是匿名函数

~~~java
package demo1;

import java.util.Arrays;
import java.util.function.IntToLongFunction;

public class MainClass {

	public static void main(String[] args) {
		long[] data = new long[10];
		Arrays.setAll(data, new IntToLongFunction() {
			
			@Override
			public long applyAsLong(int value) {
				// TODO Auto-generated method stub
				return 2*value;
			}
		});
//		Arrays.setAll(data, i->i);
		for (long l : data) {
			System.out.println(l);
		}
	}
	
}

~~~

