# Spring中ClassPathXmlApplicationContext类的简单使用

一、简单的用ApplicationContext做测试的话,获得Spring中定义的Bean实例(对象).可以用:

	ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
	RegisterDAO registerDAO = (RegisterDAO)ac.getBean("RegisterDAO");

如果是两个以上:

	ApplicationContext ac = new ClassPathXmlApplicationContext(new String[]{"applicationContext.xml","dao.xml"});

或者用通配符:

	ApplicationContext ac = new ClassPathXmlApplicationContext("classpath:/*.xml");


二、ClassPathXmlApplicationContext[只能读放在web-info/classes目录下的配置文件]和FileSystemXmlApplicationContext的区别

classpath:前缀是不需要的,默认就是指项目的classpath路径下面;
如果要使用绝对路径,需要加上file:前缀表示这是绝对路径;

对于FileSystemXmlApplicationContext:
默认表示的是两种:

1.没有盘符的是项目工作路径,即项目的根目录;
2.有盘符表示的是文件绝对路径.

如果要使用classpath路径,需要前缀classpath:

	public class HelloClient {

	  protected static final Log log = LogFactory.getLog(HelloClient.class);

	  public static void main(String[] args) {
	    // Resource resource = new ClassPathResource("appcontext.xml");
	    // BeanFactory factory = new XmlBeanFactory(resource);

	    // 用classpath路径
	    // ApplicationContext factory = new ClassPathXmlApplicationContext("classpath:appcontext.xml");
	    // ApplicationContext factory = new ClassPathXmlApplicationContext("appcontext.xml");

	    // ClassPathXmlApplicationContext使用了file前缀是可以使用绝对路径的
	    // ApplicationContext factory = new ClassPathXmlApplicationContext("file:F:/workspace/example/src/appcontext.xml");

	    // 用文件系统的路径,默认指项目的根路径
	    // ApplicationContext factory = new FileSystemXmlApplicationContext("src/appcontext.xml");
	    // ApplicationContext factory = new FileSystemXmlApplicationContext("webRoot/WEB-INF/appcontext.xml");

	    // 使用了classpath:前缀,这样,FileSystemXmlApplicationContext也能够读取classpath下的相对路径
	    // ApplicationContext factory = new FileSystemXmlApplicationContext("classpath:appcontext.xml");
	    // ApplicationContext factory = new FileSystemXmlApplicationContext("file:F:/workspace/example/src/appcontext.xml");

	    // 不加file前缀
	    ApplicationContext factory = new FileSystemXmlApplicationContext("F:/workspace/example/src/appcontext.xml");
	    IHelloWorld hw = (IHelloWorld)factory.getBean("helloworldbean");
	    log.info(hw.getContent("luoshifei"));
	  }
	}





refs:  
[Spring中ClassPathXmlApplicationContext类的简单使用](http://www.blogjava.net/xcp/archive/2011/06/22/352821.html)  