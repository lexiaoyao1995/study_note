## socket

### 网络的基础知识

**需要**	ip	协议（TCP/IP）	端口号

应用层协议有http   ftp（文件传输）  smtp（邮件）   telnet（远程登录）

#### 端口

1、用于区分不同应用程序

2、端口范围0-65535，其中0-1023为系统所保留

3、ip+端口号 组成了socket

4、http：80   ftp：21  telnet：23

#### java支持

1、InetAddress类：用于标识网络上的硬件资源

2、URL

3、Sockets：使用tcp

4、Datagram：使用udp

### Java中InetAddress的应用

主要用于表示ip地址

~~~java
	InetAddress host = InetAddress.getLocalHost();
		byte[] address = host.getAddress();
		System.out.println(Arrays.toString(address));
		System.out.println(host);
		System.out.println(host.getHostName());
		
		
		InetAddress address2 = InetAddress.getByName("ST_123-347E");
		System.out.println(address2);
~~~

### URL

~~~java
package demo;
/**
 * URL
 * @author zg
 * @date 2019年1月17日
 */

import java.net.MalformedURLException;
import java.net.URL;

public class Test02 {
	public static void main(String[] args) throws MalformedURLException {
		URL url = new URL("http://www.baidu.com");
		URL otherurl = new URL(url, "/test");
		System.out.println(otherurl.getProtocol());
		System.out.println(otherurl.getHost());
		//如果未指定端口号，则使用默认端口号，此时getPort返回值是-1
		System.out.println(otherurl.getPort());
	}
}

~~~

url获取网页内容

~~~java
package demo;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URL;

public class Test03 {
	public static void main(String[] args) throws Exception {
		URL url = new URL("http://www.siemens.com");
		InputStream stream = url.openStream();
		InputStreamReader inputStreamReader = new InputStreamReader(stream);
		BufferedReader bReader = new BufferedReader(inputStreamReader);
		String data = bReader.readLine();
		while(data!=null) {
			System.out.println(data);
			data=bReader.readLine();
		}
		bReader.close();
		inputStreamReader.close();
		stream.close();
		
		
	}
}

~~~

### socket

客户端的socket类

服务器的ServiceSocket类

#### 实现步骤

1、建立servicesocket和socket

2、打开连接到socket的输入输出流

3、按照协议对socket进行读写操作

4、关闭输入输出流，关闭socket

~~~java
package demo;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.PrintWriter;
import java.net.Socket;

public class Client {

	public static void main(String[] args) {
		try {
//		1、创建客户端socket，指定服务器地址和端口
			Socket socket = new Socket("localhost",8888);
			
			OutputStream outputStream = socket.getOutputStream();//获取字节输出流
			PrintWriter pWriter = new PrintWriter(outputStream);
			pWriter.write("username:admin password:123");
			pWriter.flush();
			
		
			socket.shutdownOutput();//关闭输出流
			
			//获取服务器的响应信息
			InputStream inputStream = socket.getInputStream();
			
			BufferedReader bReader = new BufferedReader(new InputStreamReader(inputStream));
			
			String data ;

			while((data=bReader.readLine())!=null) {
				System.out.println(data);
			}
			socket.shutdownInput();
			
			inputStream.close();
			
			bReader.close();
			
			pWriter.close();
			outputStream.close();
			socket.close();
			
			
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}

~~~

~~~java
package demo;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class Server {

	public static void main(String[] args) throws Exception {
		// 1、创建一个服务器端socket
		ServerSocket serverSocket = new ServerSocket(8888);
		// 2、调用accept方法开始监听，等待客户连接
		System.out.println("waiting for connecting");
		Socket socket = serverSocket.accept();
		// 3、实现数据的交互
		InputStream inputStream = socket.getInputStream();

		InputStreamReader isReader = new InputStreamReader(inputStream);// 将字节流包装为字符流
		BufferedReader reader = new BufferedReader(isReader);
		String data;

		while ((data = reader.readLine()) != null) {
			System.out.println(data);
		}

		// 获取输出流响应请求
		
		socket.shutdownInput();// 关闭输入流
		
		OutputStream outputStream = socket.getOutputStream();
		PrintWriter pWriter = new PrintWriter(outputStream);
		pWriter.write("welcome");
		pWriter.flush();

		socket.shutdownOutput();
		Thread.sleep(3000);
		
		// 关闭相关的资源
		pWriter.close();
		outputStream.close();

		reader.close();
		isReader.close();
		inputStream.close();
		socket.close();
		serverSocket.close();

	}
}

~~~

一定要关闭socket.shutdownInput();// 关闭输入流

**关闭流**