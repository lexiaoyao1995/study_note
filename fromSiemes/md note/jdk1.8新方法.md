~~~java
package demo;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.function.Consumer;
import java.util.function.IntUnaryOperator;

public class Test01 {
	public static void main(String[] args) {
		
		Map<String, String> map = new HashMap<String, String>();
		map.put("key1", "value1");
		map.put("key2", "value1");
		map.put("key3", "value1");
		
		List<String> listT = new ArrayList<>();
		
		map.forEach((t,u)->{;
			System.out.println(t);
			listT.add(t);
		});
//		map.forEach(new BiConsumer<String, String>() {
//
//			@Override
//			public void accept(String t, String u) {
//				// TODO Auto-generated method stub
//				System.out.println(t);
//				listT.add(t);
//			}
//			
//		});
		
		List<Integer> list = new ArrayList<Integer>();
		list.add(1);
		list.add(2);
		list.add(3);
		list.add(4);
		
		int[] ints = new int[5];
		Arrays.setAll(ints, new IntUnaryOperator() {

			@Override
			public int applyAsInt(int operand) {
				// TODO Auto-generated method stub
				return operand;
			}
			
		});
		list.forEach(new Consumer<Integer>() {

			@Override
			public void accept(Integer t) {
				// TODO Auto-generated method stub
				System.out.println(t);
			}
			
		});
		
		for(int i : ints) {
			System.out.println(i);
		}
		
		
		
	}
	
	//list.add(1);
	
}

~~~

~~~java
package demo;

import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

/**
 * stream
 * @author zg
 * @date 2019年1月23日
 */
public class Test01 {
	public static <T> void main(String[] args) {
		List<String> list = new ArrayList<String>() {
			{
				add("Asd");
				add("Aqq");
				add("qwe");
				
			}
		};
		
		
		String[] array = list.stream().filter(new Predicate<String>() {

			@Override
			public boolean test(String t) {
				// TODO Auto-generated method stub
				return t.startsWith("A");
			}
		}).toArray(String[]::new);//string[]::new jdk8新特性 调用string[]的构造方法
		
		

		for(String integer : array) {
			System.out.println(integer);
		}
		
		
		list.forEach(i->System.out.println(i));
		
		//Stream<String> stream = list.stream();
		

	}

	// list.add(1);

}

~~~

