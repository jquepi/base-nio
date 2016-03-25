# BaseNIO
***

After learning [ApacheMina](http://mina.apache.org/),we provide this java Non-blocking IO (**NIO**) mini framework. Thanks for MINA's so excellent work.

Using this frame，you can build a TCP server for accepting TCP client channel connection request. and that , process socket read\write.

and others. we also provide TCP client and UDP server\client. details in those codes */src/main/java/test*

##Important notice

Basenio does not implements any protocol base on tcp or udp, It transfer all data by **BYTE** for what is whether server or client. and so,  you must package any protocol what you want


##How to use

> Firstly you must deeply read the demo codes in **/src/main/java/test**> 

* get all source codes, and then use MAVEN build a jar package ,import this jar package to your project.
* directly use we provided the lastest release jar.

##Application Scenario

* high performance TCP server based on byte protocol.
* One flexible TCP client that can connect to a tcp server , and transfer byte data.
* A UDP client that send a bound byte message .
* UDP server listen udp port ,receive byte message. and others, it can be used to a UDP broadcast.

##Example
*the following codes is a TCP server usage , please look up other usages in domo sample。*

	package test;
	import java.net.InetSocketAddress;
	import com.polarlight.commons.basenio.io.NioSocketServerAccepter;

	public class ServerDemo {

		public static void main(String[] args) throws InterruptedException {
			try {
				/** initialize instance **/
				NioSocketServerAccepter nioserv = new NioSocketServerAccepter();
				/**set callback object*/
				nioserv.setHandler(new ServerHandler());
				/**set session buffer size (byte)*/
				nioserv.setSessionBufSize(1024);
				/**session idle timespan (ms)*/
				nioserv.setMaxSessionIdleMS(30000 * 1000);
				/*server startup*/
				nioserv.bind(new InetSocketAddress("0.0.0.0", 4567));
				/*this is only a explain for using shutdown method */
				Thread.sleep(1000000);
				nioserv.shutdown();
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	}