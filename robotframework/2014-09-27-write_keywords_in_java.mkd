# 用Java写关键词 (测试用例)

## 首先, 写一个Java类

	package com.robot;

	import java.util.Stack;

	/**
	 * This is an example for a Keyword Library for the Robot Framework.
	 * @author thomas.jaspers
	 */
	public class SimpleTest {
	    
	    /** This means the same instance of this class is used throughout
	     *  the lifecycle of a Robot Framework test execution.
	     */
	    public static final String ROBOT_LIBRARY_SCOPE = "GLOBAL";    
	    
	    //</editor-fold>
	    /** The Functionality to be tested */
	    private Stack<String> testStack;
	    
	    public void createAnEmptyStack() {
	        testStack = new Stack<String>();
	    }
		public void addAnElement(String element) {
	        testStack.push(element);
	    }
	    public void removeLastElement() {
	        testStack.pop();
	    }
	    public void elementShouldBeAtPosition(String element, int pos) 
	            throws Exception {
	        if (testStack.search(element) != pos) {
	            throw new Exception("Wrong position: " + testStack.search(element));
	        }
	    }
	 
	}
## 把classes打成jar包

## 写一个testcase

	*** Setting ***
	Documentation  This is a demo Testsuite that uses the SampleLibrary (own keyword implementation).
	Suite Setup
	Suite Teardown
	Library  com.robot.SimpleTest
	*** Testcases ***
	Basic Stack Functionality
		Create an Empty Stack
		Add an Element  Java
		Add an Element  C++
		Remove last Element
		The last Element should be  Java
	Stack Search
		Create an empty Stack
		Add an Element  Java
		Add an Element  C++
		Add an Element  PHP
		Element should be at Position  Java  3
## 运行时要设置classpath

	export CLASSPATH=$CLASSPATH:robot_simple.jar
	jybot --outputdir output sample.txt
# get Sample Project

	git clone https://github.com/ThomasJaspers/Robot-Framework-Sample-Project.git

refs:  
[writing keyword libraries in java](https://blog.codecentric.de/en/2012/06/robot-framework-tutorial-writing-keyword-libraries-in-java/)  
[Robot Framework Sample Project](https://github.com/ThomasJaspers/Robot-Framework-Sample-Project)  
