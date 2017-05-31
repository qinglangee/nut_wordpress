# struts result type 示例

## chain


	<package name="p1" extends="struts-default">
		<action name="a1" class="...">
			<resulttype = chain ">a2</result>
		</action>
		<action name="a2" class="...">
			<result type="chain">
				<param name = actionName ">a3</param>
				<param name = namespace ">/n2</param>
			</result>
		</action>
	</package>
	<package name="p2" namespace="/n2" extends="struts-default">
		<action name="a3" class="...">
			<result>/my.jsp</result>
		</action>
	</package>
p1包里的a1动作连接着a2动作，后者又连接另外一个包里的a3动作。在一条动作链里，允许把另一个包里的某个动作作为下一个动作，但是前提是必须正确的给出目标动作的namespace参数。
如果动作a-x连接着动作a-y，a-y将跟在a-x后面被压入valueStack栈，这将使a-y成为Object栈的栈顶对象。因此，这个动作可以再视图里访问。如果a-x和a-y有同名的属性，你可以用下面的OGNL表达式去访问a-y的那个属性：[0].propertyName或者propertyName。
如果你想访问a-x里的属性，那么请使用这样的表达式：[1].propertyName。
请注意，在使用动作链的时候，请三思后行，能不用就不用。因为他将把你的一整套连续的动作弄的很乱。如果你必须让动作a1把控制权转交给a2,应该先考虑是否可以把a2的某些代码放到某个辅助类的方法里供a1和a2调用。

## redirect


			<result name="toPK" type="redirect">
				http://www.l99.com/versus/send?type=${pkType}
			</result>

## redirectAction


			<result name="saveEdit" type="redirectAction" >
				view?_dashboardid=${_dashboardid}&amp;_accountid=${_accountid}
			</result>