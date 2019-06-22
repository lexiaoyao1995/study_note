~~~java
public static void main(String[] args) throws Exception {

		int[] nums = {1,5,9,2,8,1,7,8,7,3,6};
		int[] a= {12,3,1};
		int[] c;
		boolean equals = Arrays.equals(nums, a);//判断数组是否相等
		c=Arrays.copyOf(nums, nums.length);//数组拷贝
		Arrays.sort(nums);//从小到大排序
		int search = Arrays.binarySearch(nums, 5);//二分排序
    List<String> asList = Arrays.asList("i like my country".split(" "));//将数组转集合
		
	}
~~~



~~~java
List<Integer> list = new ArrayList<Integer>();
		list.add(22);
		list.add(33);
		list.add(34);
		list.add(21);
		
		//集合排序，泛型为基本数据类型
		Collections.sort(list);
		
		//最大最小值
		Integer max = Collections.max(list);
		Integer min = Collections.min(list);
		
		//搜索
		int binarySearch = Collections.binarySearch(list, 33);
		
		
		
		System.out.println(list);
~~~

