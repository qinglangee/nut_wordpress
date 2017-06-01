# maven 工程中配置运行textng测试


## 1. 添加pom 依赖
```
<dependency>
    <groupId>org.testng</groupId>
    <artifactId>testng</artifactId>
    <version>6.11</version>
    <scope>test</scope>
</dependency>
```

## 2. 测试类
在　src/test/java 中新建一个普通类，在要测试的方法上用 `@Test` 标注就可以了, 然后右键　Run as -> TestNG test
*在　maven 命令行运行`mvn test`需要类名是  xxxxTest的形式，testng 命令约定*
```
public class ProcessorTest {

    @Test
    public void test(){
        Assert.assertEquals("1", "1");
    }

}
```
## 3. 更多详细配置请参看
[Maven Surefire Plugin (and Examples)](http://maven.apache.org/surefire/maven-surefire-plugin/)  
[Maven Surefire Plugin Using TestNG][1]  
and  [testng 英文文档](http://testng.org/doc/documentation-main.html)  





refs:  
[Using TestNG][1]  



[1]: https://maven.apache.org/surefire/maven-surefire-plugin/examples/testng.html
