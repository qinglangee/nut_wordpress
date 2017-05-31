# logback 手册
##    Chapter 1: Introduction to logback
打印logger状态

	public class HelloWorld2 {

	  public static void main(String[] args) {
	    Logger logger = LoggerFactory.getLogger("chapters.introduction.HelloWorld2");
	    logger.debug("Hello world.");

	    // print internal state
	    LoggerContext lc = (LoggerContext) LoggerFactory.getILoggerFactory();
	    StatusPrinter.print(lc);
	  }
	}
输出 

>12:49:22.203 [main] DEBUG chapters.introduction.HelloWorld2 - Hello world.
12:49:22,076 |-INFO in ch.qos.logback.classic.LoggerContext[default] - Could NOT find resource [logback.groovy]
12:49:22,078 |-INFO in ch.qos.logback.classic.LoggerContext[default] - Could NOT find resource [logback-test.xml]
12:49:22,093 |-INFO in ch.qos.logback.classic.LoggerContext[default] - Could NOT find resource [logback.xml]
12:49:22,093 |-INFO in ch.qos.logback.classic.LoggerContext[default] - Setting up default configuration.

##    [Chapter 2: Architecture][2]
Logger, Appenders and Layouts

*Logger*
root Logger  `Logger rootLogger = LoggerFactory.getLogger(org.slf4j.Logger.ROOT_LOGGER_NAME);`
Logger 的 level 如果没设置的话， 就继承它最近的一个非空祖先的 level.

Example 3

	Logger name 	Assigned level 	Effective level
	root 	DEBUG 	DEBUG
	X 	    INFO 	INFO
	X.Y 	none 	INFO
	X.Y.Z 	ERROR 	ERROR
同样的名字总是返回同一个 Logger 对象

	// x,y 是同一个对象
	Logger x = LoggerFactory.getLogger("wombat"); 
	Logger y = LoggerFactory.getLogger("wombat");

*Appender* 
日志的输出方向
日志 是向上面的所有 Appender 传输的，子 Logger 的日志会写到父 Logger 的 appender 中，但如果 additivity flag 设置为 false, 日志就不向上级 Appender 传输。
*Layout*
日志的输出格式
##    Chapter 3: Configuration

##    Chapter 4: Appenders

##    Chapter 5: Encoders

##    Chapter 6: Layouts

##    Chapter 7: Filters

##    Chapter 8: Mapped Diagnostic Contexts

##    Chapter 9: Logging Separation

##    Chapter 10: JMX Configurator

##    Chapter 11: Joran

##    Chapter 12: Groovy Configuration

##    Chapter 13: Migration from log4j

##    Chapter 14: Receivers

##    Chapter 15: Using SSL

## other

参考资料:
[Reasons to prefer logback over log4j][1]

[1]: http://logback.qos.ch/reasonsToSwitch.html
[2]: http://logback.qos.ch/manual/architecture.html