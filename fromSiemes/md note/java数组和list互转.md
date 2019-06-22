~~~java
package demo;

import java.util.ArrayList;
import java.util.Arrays;

public class Main {

	public static void main(String[] args) {
		Character[] characters = { '1', '2' };

		ArrayList<Character> list = new ArrayList<>(Arrays.asList(characters));

		Character[] characters2 = list.toArray(new Character[list.size()]);
	}
}
~~~

注意：

数组必须是**类的数组**，包括包装类，基本类型的数组不可以转。