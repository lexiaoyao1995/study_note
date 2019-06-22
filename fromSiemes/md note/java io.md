### java io流

1、inputstream 和 outputstream

~~~java
		String path = "D:\\date\\test.txt";
		String path1 = "D:\\date\\test1.txt";
		FileInputStream fis = null;
		FileOutputStream fos = null;

		try {
			fis = new FileInputStream(path);
			fos = new FileOutputStream(path1);
			byte[] bytes = new byte[1024];
			int n = 0;
			while ((n = fis.read(bytes)) != -1) {

				String str = new String(bytes, 0, n);
				System.out.println(str);
				fos.write(bytes, 0, n);
			}
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				fis.close();
				fos.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
		
~~~

2、bufferedstream

bufferedstream是在input/outputstream的基础上再次封装一层，加快读取速度。bufferedoutputstream的write后，需要flush，把buffer里的数据，写入到out中

~~~java
package demo;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class Test {
	public static void main(String[] args) {

		String path = "D:\\date\\test.txt";
		String path1 = "D:\\date\\test1.txt";
		FileInputStream fis = null;
		FileOutputStream fos = null;
		
		BufferedInputStream bis = null;
		BufferedOutputStream bos = null;

		try {
			fis = new FileInputStream(path);
			fos = new FileOutputStream(path1);
			bis=new BufferedInputStream(fis);
			bos=new BufferedOutputStream(fos);
			byte[] bytes = new byte[1024];
			int n = 0;
			while ((n = bis.read(bytes)) != -1) {

				String str = new String(bytes, 0, n);
				System.out.println(str);
				bos.write(bytes, 0, n);
			}
			bos.flush();
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				fis.close();
				fos.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}

		
		
		
	}
}

~~~

3、filereader和filewriter

filereader可以直接一个char一个char地读取数据

filewriter可以直接用write向文件中输出数据

~~~java
package demo;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;

public class Test {
	public static void main(String[] args) throws Exception {

		String path = "D:\\date\\test.txt";
		String path1 = "D:\\date\\test1.txt";

		FileReader reader = null;
		FileWriter writer = null;
		try {
			reader = new FileReader(path);
			writer = new FileWriter(path1);
			char[] ch = new char[1024];
			int len = 0;
			while ((len = reader.read(ch)) != -1) {
				String string = new String(ch, 0, len);
				System.out.println(string);
			}
			
			writer.write("asdweasdae");

		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			writer.close();
			reader.close();
		}

	}
}

~~~

