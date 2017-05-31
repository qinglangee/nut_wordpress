# testng  注解

Testng 在 Eclipse 中运行， 先装一个 testng插件

## @Test
标注一个测试方法


    @Test
    public void countContentBasic() {
		System.out.println(123);
    }
    @Test(enabled = false)  // 暂时停用一个测试方法
    public void countContentBasic() {
		System.out.println(123);
    }

## @BeforeClass
在整个类的测试方法运行之前运行一次的准备方法

	@BeforeClass
	public void init(){
		// 初始化
		context = new ClassPathXmlApplicationContext(new String[] { "conf/content-war-dubbo-service-test.xml" });
		context.start();
		textCategoryService = (ContentTextCategoryService) context.getBean("textCategoryService");
	}