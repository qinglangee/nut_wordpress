# testng 数据提供

test 方法中可以有参数，  提供参数有两种方式， xml 或 data provider。
xml 提供比较简单的数据， data provider 提供比较复杂或需要生成、读取的数据。


## Data Provider



	// 这个方法会向所有声明 Data Provider 是 "test1" 的测试方法提供数据
	@DataProvider(name = "test1")
	public Object[][] createData1() {
	 return new Object[][] {
	   { "Cedric", new Integer(36) },
	   { "Anne", new Integer(37)},
	 };
	}
	 

	// 这个方法声明它的数据由名为 "test1" 的 Data Provider 来提供
	@Test(dataProvider = "test1")
	public void verifyData1(String n1, Integer n2) {
	 System.out.println(n1 + " " + n2);
	} 




refs:  
[testng 英文文档][1]  



[1]: http://testng.org/doc/documentation-main.html