# mina入门示例

## 时间服务器示例
mina时间服务器
服务器框架:

	package com.zhch.example.mina.quickstart;

	import java.io.IOException;
	import java.net.InetSocketAddress;
	import java.nio.charset.Charset;

	import org.apache.mina.core.service.IoAcceptor;
	import org.apache.mina.core.session.IdleStatus;
	import org.apache.mina.filter.codec.ProtocolCodecFilter;
	import org.apache.mina.filter.codec.textline.TextLineCodecFactory;
	import org.apache.mina.filter.logging.LoggingFilter;
	import org.apache.mina.transport.socket.nio.NioSocketAcceptor;

	public class MinaTimeServer {
		public static int PORT = 12222;
		public static void main(String[] args) throws IOException {
			// new 一个接口
			IoAcceptor acceptor = new NioSocketAcceptor();

			// 添加过滤器
			acceptor.getFilterChain().addLast("logger", new LoggingFilter());
			acceptor.getFilterChain().addLast("codec", new ProtocolCodecFilter(new TextLineCodecFactory(Charset.forName("UTF-8"))));
			
			// 设置handler, 这是主要的处理逻辑所在
			acceptor.setHandler(  new TimeServerHandler() );
			

			// 配置acceptor
	        acceptor.getSessionConfig().setReadBufferSize( 2048 );
	        acceptor.getSessionConfig().setIdleTime( IdleStatus.BOTH_IDLE, 10 );
	        
	        // 绑定端口号
	        acceptor.bind( new InetSocketAddress(PORT) );
		}
	}
处理程序 :

	package com.zhch.example.mina.quickstart;

	import java.util.Date;

	import org.apache.mina.core.service.IoHandlerAdapter;
	import org.apache.mina.core.session.IdleStatus;
	import org.apache.mina.core.session.IoSession;

	public class TimeServerHandler extends IoHandlerAdapter {
		// 错误处理函数
		@Override
		public void exceptionCaught(IoSession session, Throwable cause) throws Exception {
			cause.printStackTrace();
		}

		// 消息处理函数 
		@Override
		public void messageReceived(IoSession session, Object message) throws Exception {
			String str = message.toString();
			if (str.trim().equalsIgnoreCase("quit")) {
				session.close();
				return;
			}

			Date date = new Date();
			session.write(date.toString());
			System.out.println("Message written...");
		}

		// session空闲 
		@Override
		public void sessionIdle(IoSession session, IdleStatus status) throws Exception {
			System.out.println("IDLE " + session.getIdleCount(status));
		}
	}

一般的, mina程序分为三层

* I/O Service - 执行IO操作  Performs actual I/O
* I/O Filter Chain - 过滤器链,过滤内容  Filters/Transforms bytes into desired Data Structures and vice-versa
* I/O Handler - 执行真正的业务逻辑  Here resides the actual business logic

Client 端也分三层

* IO connector
* filter
* IO handler

## 关闭session进入 TIME_WAIT 状态
在 filter中加入以下代码, 设置 so_linger的值为0

    public void sessionCreated(NextFilter nextFilter, IoSession session) throws Exception {
        SocketSessionConfig conf = (SocketSessionConfig)session.getConfig();
        conf.setSoLinger(0); // 可以设置 time_wait的时间
    	nextFilter.sessionCreated(session);
    }

refs:
[Quick Start Guide][1]  
[MINA based Application Architecture][2]  
[Client Architecture][3]  


[1]: http://mina.apache.org/mina-project/quick-start-guide.html
[2]: http://mina.apache.org/mina-project/userguide/ch2-basics/application-architecture.html
[3]: http://mina.apache.org/mina-project/userguide/ch2-basics/client-architecture.html