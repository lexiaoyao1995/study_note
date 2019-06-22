~~~java
	private static boolean Binarysearch(int[] a, int target) {

		int low = 0;
		int high = a.length - 1;
		int middle;
		while (low <= high) {
			middle = (low + high) / 2;
			if (a[middle] == target) {
				return true;
			} else if (a[middle] > target) {
				high = middle - 1;
			} else {
				low = middle + 1;
			}
		}
		return false;

	}

	private static void bubbleSort(int[] a) {
		// TODO Auto-generated method stub
		for (int i = 1; i < a.length; i++) {
			for (int j = 0; j < a.length - i; j++) {
				if (a[j] > a[j + 1]) {
					int temp = a[j];
					a[j] = a[j + 1];
					a[j + 1] = temp;
				}
			}
		}
	}

	private static void quickSort(int[] a, int low, int high) {
		if (low > high) {
			return;
		}
		int i = low;
		int j = high;
		int standary = a[low];
		while (i < j) {
			while (i < j) {
				if (a[j] < standary) {
					break;
				}
				j--;
			}
			while (i < j) {
				if (a[i] > standary) {
					break;
				}
				i++;
			}
			if (i < j) {
				int temp = a[i];
				a[i] = a[j];
				a[j] = temp;
			}
		}

		a[low] = a[i];
		a[i] = standary;
		quickSort(a, low, i - 1);
		quickSort(a, i + 1, high);
	}
~~~

背包问题

~~~java
package demo;

import javax.swing.plaf.basic.BasicInternalFrameTitlePane.MaximizeAction;

public class MainTest {

	public static void main(String[] args) {

		int m = 10;
		int n = 3;
		int[] w = { 0, 3, 4, 5 };
		int[] p = { 0, 4, 5, 6 };

		int[][] c = solution(m, n, w, p);
		for (int i = 0; i < c.length; i++) {
			for (int j = 0; j < c[0].length; j++) {
				System.out.print(c[i][j] + "\t");
			}
			System.out.println();
		}

	}

	private static int[][] solution(int m, int n, int[] w, int[] p) {
		// TODO Auto-generated method stub
		int[][] c = new int[n + 1][m + 1];
		for (int i = 0; i < n + 1; i++) {
			c[i][0] = 0;
		}
		for (int j = 0; j < m + 1; j++) {
			c[0][j] = 0;
		}

		for (int i = 1; i < n + 1; i++) {
			for (int j = 1; j < m + 1; j++) {
				if (w[i] > j) {
					c[i][j] = c[i - 1][j];
				} else {
					c[i][j] = max(c[i - 1][j], c[i - 1][j - w[i]] + p[i]);
				}
			}
		}
		return c;
	}

	private static int max(int i, int j) {
		return i >= j ? i : j;
	}

}

~~~

最长上升子序列

~~~java
package demo;

public class MainTest {

	public static void main(String[] args) {

		int[] a = { 2, 7, 1, 5, 6, 4, 3, 8, 9 };

		int n = getLIS(a);

		System.out.println(n);

	}

	private static int getLIS(int[] a) {
		int[] d = new int[a.length];
		for (int i = 0; i < a.length; i++) {
			//初始化为1
			d[i] = 1;
			//遍历i之前比a[i]小的数，并以最大值更新d
			for (int j = 0; j < i; j++) {
				if (a[j] <= a[i] && d[i] <= d[j] + 1) {
					d[i] = d[j] + 1;
				}
			}
		}

		return d[d.length - 1];
	}

}
~~~

汉诺塔

~~~java
package demo;
//移动次数为2的n次方减1
public class Hanoi {

	public static void detail(int n,char x,char y,char z) {
		
		if (n==0) {
			return;
		}else {
			detail(n-1, x, z, y);
			System.out.println(x+"->"+y);
			detail(n-1, z, y, x);
		}
		
	}
	
	public static void main(String[] args) {
		char x= 'x',y='y',z='z';
		detail(3, x, y, z);
	}
	
}

~~~

~~~java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] sa = br.readLine().split(" ");
		int[] arrays = new int[sa.length];
		int k = 0;
		for (String string : sa) {
			arrays[k++] = Integer.parseInt(string);
		}
		int ans = 0;
		for (int i : arrays) {
			ans += i;
		}
		System.out.println(ans);
~~~

~~~java
package demo5;

public class Test {

	public static void main(String[] args) {

		int[] a = { 1, 2, 3 };

		fullSort(a, 0, a.length - 1);

	}

	private static void fullSort(int[] a, int start, int end) {
		// TODO Auto-generated method stub
		if (start == end) {
			for (int i : a) {
				System.out.print(i);
			}
			System.out.println();
			return;
		}
		for (int i = start; i <= end; i++) {
			swap(a, i, start);
			fullSort(a, start + 1, end);
			swap(a, i, start);
		}

	}

	private static void swap(int[] a, int i, int j) {
		// TODO Auto-generated method stub
		int t = a[i];
		a[i] = a[j];
		a[j] = t;
	}

}

~~~

死锁

~~~java
package demo5;

public class Test {

	public static String obj1 = "obj1";

	public static String obj2 = "obj2";

	public static void main(String[] args) {

		Thread a = new Thread(new Runnable() {
			@Override
			public void run() {
				// TODO Auto-generated method stub
				System.out.println("a running");
				while (true) {
					synchronized (obj1) {
						System.out.println("get obj1");
						try {
							Thread.sleep(3000);
						} catch (InterruptedException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						}
						synchronized (obj2) {
							System.out.println("get obj2");
						}
					}
				}
			}
		});

		Thread b = new Thread(new Runnable() {

			@Override
			public void run() {
				// TODO Auto-generated method stub
				System.out.println("b running");
				while (true) {
					synchronized (obj2) {
						System.out.println("get obj2");
						try {
							Thread.sleep(3000);
						} catch (InterruptedException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						}
						synchronized (obj1) {
							System.out.println("get obj1");
						}
					}
				}
			}
		});

		a.start();
		b.start();

	}
}

~~~

生成者消费者

~~~java
package observerDemo;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

public class Main {

	private static BlockingQueue<Integer> queue = new ArrayBlockingQueue<>(10);
	
	
	public static void main(String[] args) throws Exception {
	
		Main main = new Main();
		Producer producer = main.new Producer();
		Customer customer = main.new Customer();
		
		new Thread(producer).start();

		new Thread(customer).start();
		
	}
	
	class Producer implements Runnable{
		@Override
		public void run() {
			// TODO Auto-generated method stub
			while(true) {
				System.out.println("produce data");
				try {
					Thread.currentThread().sleep(1000);
				} catch (InterruptedException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				queue.offer(10);
			}
		}
	}
	
	class Customer implements Runnable{

		@Override
		public void run() {
			// TODO Auto-generated method stub
			while(true) {
				System.out.println("get data");
				try {
					Thread.currentThread().sleep(1000);
				} catch (InterruptedException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				try {
					System.out.println(queue.take());
				} catch (InterruptedException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
		}
		
	}
	
}

~~~

~~~java
堆排序
package observerDemo;

import java.util.Arrays;

public class Heapsize {

	private double A[];
	private int heapsize;

	private int parent(int i) {
		return (i - 1) / 2;
	}

	private int left(int i) {
		return 2 * i + 1;
	}

	private int right(int i) {
		return 2 * i + 2;
	}

	private void maxHeapify(int i) {
		int l = left(i);
		int r = right(i);
		int largest = i;
		if (l <= heapsize - 1 && A[l] > A[largest]) {
			largest = l;
		}
		if (r <= heapsize - 1 && A[r] > A[largest]) {
			largest = r;
		}
		if (largest != i) {
			double t = A[i];
			A[i] = A[largest];
			A[largest] = t;
			maxHeapify(largest);
		}
	}

	public void buildMaxHeap(double[] A) {
		this.A = A;
		this.heapsize = A.length;

		for (int i = parent(heapsize - 1); i >= 0; i--) {
			maxHeapify(i);
		}
	}

	public void heapSort(double[] A) {
		buildMaxHeap(A);
		int step = 1;
		for (int i = A.length - 1; i > 0; i--) {
			double temp = A[i];
			A[i] = A[0];
			A[0] = temp;
			heapsize--;
			System.out.println("step      : " + (step++) + Arrays.toString(A));
			maxHeapify(0);
			System.out.println("step after: " + (step) + Arrays.toString(A));
		}

	}

	public static void main(String[] args) {
		double[] a = { 3, 7, 2, 11, 3, 4, 9, 2, 18, 0 };
		Heapsize aHeapsize = new Heapsize();
		aHeapsize.heapSort(a);
		for (double d : a) {
			System.out.println(d);
		}
	}

}

~~~

归并

~~~java
package demo;

public class MinStack {

	public static void main(String[] args) {
		int[] arr = { 8, 4, 5, 7, 1, 3, 6, 2 };

		sort(arr);

		for (int i : arr) {
			System.out.println(i);
		}
	}

	private static void sort(int[] arr) {
		// TODO Auto-generated method stub
		int[] temp = new int[arr.length];// 在排序前，先建好一个长度等于原数组长度的临时数组，避免递归中频繁开辟新空间
		sort(arr, 0, arr.length - 1, temp);
	}

	private static void sort(int[] arr, int letf, int right, int[] temp) {
		// TODO Auto-generated method stub
		if (letf < right) {
			int mid = (letf + right) / 2;
			sort(arr, letf, mid, temp);
			sort(arr, mid + 1, right, temp);
			merge(arr, letf, mid, right, temp);
		}

	}

	private static void merge(int[] arr, int letf, int mid, int right, int[] temp) {

		int i = letf;
		int j = mid + 1;
		int t = 0;
		while (i <= mid && j <= right) {
			if (arr[i] <= arr[j]) {
				temp[t++] = arr[i++];
			} else {
				temp[t++] = arr[j++];
			}
		}
		while (i <= mid) {
			temp[t++] = arr[i++];
		}
		while (j <= right) {
			temp[t++] = arr[j++];
		}
		t = 0;
		while (letf <= right) {
			arr[letf++] = temp[t++];
		}
	}

}

~~~

