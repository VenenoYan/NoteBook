单例模式也称为单件模式、单子模式，意图是保证**一个类仅有一个实例**，并提供一个访问它的全局访问点，该实例被所有程序模块共享。有很多地方需要这样的功能模块，如系统的日志输出。

面对单例模式适用的情况，可能会优先考虑使用全局或者静态变量的方式，这样比较简单，也是没学过设计模式的人所能想到的最简单的方式了。


### 基本思路

定义一个单例类，使用类的私有静态指针变量指向类的唯一实例，并用一个公有的静态方法获取该实例。**拷贝构造函数和赋值构造都要是私有化**
#### **两种模式**
1. 
“恶汉”：实例化类时就创建刚静态实例
```C++
class testsingle{
    private:
        static testsingle * instance = new testsingle();
        testsingle();
        testsingle(const testsingle &);
        testsingle & operator =(const testsingle &);
    public:
        static testsingle * getinstance(){
            return instance;
        }
}
```
1. 
“懒汉”：第一次使用时才创建实例(存在多线程安全的问题)
```C++
class singleton{
    private:
        static singelton * instance;
        singleton();
        singleton(const singleton &);
        singleton & operator =(const singleton &);
    public:
        static singleton *getinstance(){
            if (instance == NULL)
                instance = new Singleton();
            return instance;
        }     //不好，多线程会导致在判断NULL时创建多个实例
        //改进
        static singleton *getinstance(){
            if(instance==NULL){
                lock();
                if(instance==NULL){
                    instance=new singelton();
                }
                unlock();
                return instance;
            }
        }
}
```
## 解决思路：


1. 
内部类
```C++
class testsingle{
    private:
        class testhold{
            static testsingle *instance = new testsingle();
        }
    public:
        static testsingle *getinstance(){
            return this.testsingle.instance;
        }
}
```