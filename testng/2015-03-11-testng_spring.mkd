# testng 与 spring 结合

spring 为 testng 提供了测试集成接口类  `AbstractTestNGSpringContextTests`. 进行单元测试的时只要test类继承该类，就可以方便的使用spring注入。  

除此以外，对测试类spring beanfactory缓存，使得多个测试类之间可以共享同一个的beanfactory实例，从而减少了重复生成beanfactory，提高了运行效率。  

继承该类的测试用例在spring管理的事务中进行，测试完后对数据库的记录不会造成任何影响。你对数据库进行一些操作后，它会自动把数据库回滚，这样就保证了你的测试对于环境没有任何影响



	@ContextConfiguration   
	(locations={"classpath:exp-user-spring-service-test.xml"})
	public class UserServiceImplTest extends AbstractTestNGSpringContextTests{
		
		@Autowired
		private UserService userService;

		public UserService getUserService() {
			return userService;
		}

		public void setUserService(UserService userService) {
			this.userService = userService;
		}

		@Test
		public void getUser() {
			Userinfo user = userService.getUser(1L);
			System.out.println(user);
			Assert.assertEquals(user.getUserName(), "zhch");
		}
	}



refs:  
[spring和testng的整合 ](http://blog.csdn.net/blackchoc/article/details/5711860)  