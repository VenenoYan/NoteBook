单例模式也称为单件模式、单子模式，意图是保证**一个类仅有一个实例**，并提供一个访问它的全局访问点，该实例被所有程序模块共享。有很多地方需要这样的功能模块，如系统的日志输出。

面对单例模式适用的情况，可能会优先考虑使用全局或者静态变量的方式，这样比较简单，也是没学过设计模式的人所能想到的最简单的方式了。


### 基本思路

定义一个单例类，使用类的私有静态指针变量指向类的唯一实例，并用一个公有的静态方法获取该实例。<br>
**构造函数、拷贝构造函数和赋值构造函数都要是私有化以防被用户代码随意创建**
#### **两种模式**
1. 
“恶汉”：实例化类时就创建静态实例
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
        //改进:双重检查
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
内部类:存在什么时候释放的问题          良
```C++
class testsingle{
    private:
        class testhold{
            static testsingle *instance = new testsingle();
            ～testhold(){
                delete instance;
            }
        }
    public:
        static testsingle *getinstance(){
            return this.testsingle.instance;
        }
}
```
1. 
局部静态变量：必须把拷贝构造函数和赋值构造函数都要是私有化，否则违反单例原则       良
```C++
class singleton{
    private:
        singleton();
        singleton(const singleton &);
        singleton & operator =(const singleton &);
    public:
        static singleton & getinstance(){
            static singleton instance;
            return instance;
        }
}

```
1. 
线程安全、异常安全，可以做以下扩展                      好
```C++
class Lock
{
    private:       
    	CCriticalSection m_cs;
    public:
    	Lock(CCriticalSection  cs) : m_cs(cs)
    	{
    		m_cs.Lock();
    	}
    	~Lock()
    	{
    		m_cs.Unlock();
    	}
};
class Singleton
{
    private:
    	Singleton();
    	Singleton(const Singleton &);
    	Singleton& operator = (const Singleton &);
    public:
    	static Singleton *Instantialize();
    	static Singleton *pInstance;
    	static CCriticalSection cs;
};
Singleton* Singleton::pInstance = 0;
Singleton* Singleton::Instantialize()
{
	if(pInstance == NULL)
	{   //double check
		Lock lock(cs);           //用lock实现线程安全，用资源管理类，实现异常安全
		//使用资源管理类，在抛出异常的时候，资源管理类对象会被析构，析构总是发生的无论是因为异常抛出还是语句块结束。
		if(pInstance == NULL)
		{
			pInstance = new Singleton();
		}
	}
	return pInstance;
}```