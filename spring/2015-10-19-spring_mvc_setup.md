# spring mvc 

## 1. 在 web.xml 中配置 spring servlet

	<web-app>
	    <servlet>
	        <servlet-name>example</servlet-name>
	        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	        <load-on-startup>1</load-on-startup>
	    </servlet>

	    <servlet-mapping>
	        <servlet-name>example</servlet-name>
	        <url-pattern>/example/*</url-pattern>
	    </servlet-mapping>

	</web-app>

根据 DispatcherServlet 的配置， Spring MVC  在 WEB-INF 目录中找一个叫 [servlet-name]-servlet.xml 的文件， 创建文件中定义的 bean, 这里定义的 bean 会覆盖全局范围内定义的同名bean. 
*多个 xml 文件中配置的 bean 是都能取到的*
*scan扫描的bean，默认的名字是类名首字母变为小写*

## 2. 在 [servlet-name]-servlet.xml 中定义 controler 对应的类
方法 1 ：配置 component-scan 标签，自动扫描.
`<context:component-scan>` 标签可以配置多个，扫描不同的包。

	<?xml version="1.0" encoding="UTF-8"?>
	<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
		xmlns:context="http://www.springframework.org/schema/context"
		xsi:schemaLocation="http://www.springframework.org/schema/beans 
			http://www.springframework.org/schema/beans/spring-beans.xsd 
			http://www.springframework.org/schema/context
			http://www.springframework.org/schema/context/spring-context-3.0.xsd">

		<!-- package, 注意这里的通配符是表示 base package, 不是类 -->
		<context:component-scan base-package="com.ison.*"></context:component-scan>
	</beans>

方法 2 ：手动配置每一个需要的 bean
*用手动配置的方法，类中的 service, dao 什么的也需要手动配置好，要不然都是空指针异常*， 扫描的如果annotation标记了的会自动配置

	<?xml version="1.0" encoding="UTF-8"?>
	<beans xmlns="http://www.springframework.org/schema/beans">
		<bean class="com.ison.web.action.ParserAction" />
	</beans>


## 3. Controller 中用@Controller 和 @RequestMapping("/resume") 定义访问路径
@Controller 默认不是 @Scope("prototype") 的， 需要的话可以设置为 prototype


	import org.springframework.stereotype.Controller;
	import org.springframework.web.bind.annotation.RequestMapping;
	import org.springframework.web.bind.annotation.ResponseBody;

	@Controller
	@Scope("prototype")
	@RequestMapping("/resume")
	public class ParserAction {

		@RequestMapping("upload")
		@ResponseBody
		public String upload() {
			return "abssdcd";
		}

		@ResponseBody
		public String test1() {
			return "test1";
		}

		@ResponseBody
		public String test2() {
			return "test2";
		}
	}

## 4.  Spring MVC 的请求参数获取

通过@PathVariabl注解获取路径中传递参数

     @RequestMapping(value = "/{id}/{str}")
     public ModelAndView helloWorld(@PathVariable String id,
             @PathVariable String str) {
         System.out.println(id);
         System.out.println(str);
         return new ModelAndView("/helloWorld");
     }
用@ModelAttribute注解获取POST请求的FORM表单数据

	 <form method="post" action="hao.do">
	 a: <input id="a" type="text"   name="a"/>
	 b: <input id="b" type="text"   name="b"/>
	 <input type="submit" value="Submit" />
	 </form>

JAVA pojo

     public class Pojo{
	     private String a;
	     private int b;
	     ...
     }
 

JAVA controller
            
    @RequestMapping(method = RequestMethod.POST)
    public String processSubmit(@ModelAttribute("pojo") Pojo pojo) { 
        return "helloWorld";
    }
直接用HttpServletRequest获取

     @RequestMapping(method = RequestMethod.GET)
     public String get(HttpServletRequest request, HttpServletResponse response) {
         System.out.println(request.getParameter("a"));
         return "helloWorld";
     }

用注解@RequestParam绑定请求参数a到变量a
当请求参数a不存在时会有异常发生,可以通过设置属性required=false解决,
例如: @RequestParam(value="a", required=false)

     @RequestMapping(value = "/requestParam", method = RequestMethod.GET)
     public String setupForm(@RequestParam("a") String a, ModelMap model) {
         System.out.println(a);
         return "helloWorld";}
