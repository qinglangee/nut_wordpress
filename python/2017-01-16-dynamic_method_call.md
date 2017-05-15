# 动态方法调用

下面是类的示例，  module 同类类似， module 的方法相当于静态方法

    #!/usr/bin/python  
    #coding: UTF-8  
    """ 
    @author: CaiKnife 
     
    根据函数名称动态调用 
    """  
      
    def do_foo():  
        print "foo!"  
      
    def do_bar():  
        print "bar!"  
      
    class Print():  
        def do_foo(self):  
            print "foo!"  
      
        def do_bar(self):  
            print "bar!"  
     
        @staticmethod  
        def static_foo():  
            print "static foo!"  
     
        @staticmethod  
        def static_bar():  
            print "static bar!"  
      
    def main():  
        obj = Print()  
      
        func_name = "do_foo"  
        static_name = "static_foo"  
        eval(func_name)()  
        getattr(obj, func_name)()  
        getattr(Print, static_name)()  
      
        func_name = "do_bar"  
        static_name = "static_bar"  
        eval(func_name)()  
        getattr(obj, func_name)()  
        getattr(Print, static_name)()  
      
    if __name__ == '__main__':  
        main()  