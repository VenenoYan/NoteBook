单例模式也称为单件模式、单子模式，意图是保证**一个类仅有一个实例**，并提供一个访问它的全局访问点，该实例被所有程序模块共享。有很多地方需要这样的功能模块，如系统的日志输出。

面对单例模式适用的情况，可能会优先考虑使用全局或者静态变量的方式，这样比较简单，也是没学过设计模式的人所能想到的最简单的方式了。


### 基本思路

定义一个单例类，使用类的私有静态指针变量指向类的唯一实例，并用一个公有的静态方法获取该实例。<br>
**构造函数、析构函数（一般不写）、拷贝构造函数和赋值构造函数都要是私有化以防被用户代码随意创建**
#### **两种模式**
1. 
“恶汉”：实例化类时就创建静态实例
```C++
class testsingle{
    private:
        static testsingle * instance = new testsingle();    //全局：线程安全，初始化时是单线程
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
“懒汉”：第一次使用时才创建实例(存在多线程安全的问题)－－－－延迟初始化：函数被调用时其才会被创建
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
                    instance=new singelton();           ／／函数被调用时其才会被创建，一直到程序结束
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
            return this.testhold.instance;
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
            static singleton instance;          //延迟初始化：函数被调用时其才会被创建，一直到程序结束
            return instance;
        }
}
```
**问题**：
这是由局部静态变量的实际实现所决定的。为了能满足局部静态变量只被初始化一次的需求，很多编译器会<br>通过一个全局的标志位记录该静态变量是否已经被初始化的信息。那么，对静态变量进行初始化的伪码就变成下面<br>这个样子：
```C++
bool flag = false;
if (!flag)
{
    flag = true;
    staticVar = initStatic();
}```
“那么在第一个线程执行完对flag的检查并进入if分支后，第二个线程将可能被启动，从而也进入if分支。这样，两个线程都将执行对静态变量的初始化。
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
1. 
升级：有几个类型都需要实现为Singleton，复用上述代码
```C++
template <typename T>
class Singleton
{
public:
    static T& Instance()
    {
        if (m_pInstance == NULL)
        {
            Lock lock;
            if (m_pInstance == NULL)
            {
                m_pInstance = new T();
                atexit(Destroy);
            }
            return *m_pInstance;
        }
        return *m_pInstance;
    }
protected:
    Singleton(void) {}
    ~Singleton(void) {}
private:
    Singleton(const Singleton& rhs) {}
    Singleton& operator = (const Singleton& rhs) {}
    void Destroy()
    {
        if (m_pInstance != NULL)
            delete m_pInstance;
        m_pInstance = NULL;
    }
    static T* volatile m_pInstance;
};
　
template <typename T>
T* Singleton<T>::m_pInstance = NULL;
　
使用：
class SingletonInstance : public Singleton<SingletonInstance>…
“在需要重用该Singleton实现时，我们仅仅需要从Singleton派生并将Singleton的泛型参数设置为该类型即可。”```