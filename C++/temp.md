##模板
* 
使用模板的目的就是能够让程序员编写与类型无关的代码。
1. 
模板的声明或定义只能在全局，命名空间或类范围内进行。即不能在局部范围，函数内进行，比如不能在main函数中声明或定义一个模板。
* 
不能“分离编译”

###函数模板
* 形式：
    ```C++
    template <typename T1,...,typename Tn>
    ret-type func(T1 &a,T2 &b,...)
    {}
    ```
* 调用：只能是参数推演，不能传递类型
    ```C++
    func(1,3);
    func(int,int);  //错误
    ```

###类模板
* 
形式：
    ```C++ 
    template<class data_obj>
    class other;    //前置声明：不带类型，只有类名
        
    template<typename T1,...typename Tn>
    class cname
    {
        template <typename T1,...typename Tn>
        ret-type func(T1 &a,T2 &b,...);
    }  //类中的类型用T1,...,Tn
    
    ```