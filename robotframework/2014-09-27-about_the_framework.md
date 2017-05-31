# 关于框架选用



>Test automation architect at ING

>If you are referring to unit testing, I am not sure how much real difference there would be. But if you mean other types of test like system and acceptance testing, as I suspect, you will want to take a close look at tools like FitNesse, Cucumber and Robot Framework. These support ATDD (Acceptance Test Driven Development) / BDD (Behavior Driven Development) and will allow you to write test cases at a much more natural abstraction level than a unit test engine. These in turn are incarnations of what is sometimes called Domain Specific Test Languages, which include high level keywords, also supported by some commercials tools (not all of them very successfully, though). Let me know if you have further questions.

>Good luck,

>Martin Gijsen
Test automation architect 
[which framework goes well with Selenium Junit or TestNG ?? ](http://www.linkedin.com/groups/which-framework-goes-well-Selenium-961927.S.38913259)

>目前，所在项目的自动化测试框架是基于STAF/STAX的拓展，围绕STAX执行引擎，扩展了测试用例的创建、管理（挑选执行那些测试用例：按照模块，标签）、Log、Report功能，由Java来实现的。这是一个关键字驱动的测试，测试用例由一个个关键字组成记录每一关键字的执行结果。同时，测试用例和测试数据相分离，把测试用例中一些可能变换的数据抽离出来，用宏替代，避免hard-coding，避免因为一些环境因素的变换而导致测试用例的fail，对自动化框架而言，稳定还是蛮重要的。

>STAF是一个开源、跨平台、支持多编程语言的框架，以Services 的形式提供一些常用功能，比如跨网络传出文件、远程启停一个程序、测试用例的执行引擎服务等。在我们的框架中用到了其中两个services,一个是 FILE SYSTEM用于在test client 和test server之间传文件，另一个便是STAX 测试用例执行引擎。
[自动化测试整理 --- STAF/STAX & Robot Framework](http://www.cnblogs.com/matt123/archive/2012/07/18/2598416.html)  

>In comparison JBehave seems to be very lightweight on first sight (and also on second sight). There is the description of the testcases in BDD-format on one side and the implementation of the required test functionality in Java on the other side. Both parts can be easily connected using Maven.
[Automated Acceptance-Testing using JBehave](https://blog.codecentric.de/en/2011/03/automated-acceptance-testing-using-jbehave/)  