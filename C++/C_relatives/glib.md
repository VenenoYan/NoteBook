##GObject对象系统

简单的说，GObject对象系统是一个建立在GLIB基础上的，用C语言完成的，具有跨平台特色的、灵活的、可扩展的、非常容易映射到其它语言的面向对象的框架。如果你是一个C语言的执着的追随者，你没有理由不研究一下它。
####前言

大多数现代的计算机语言都带有自己的类型和对象系统，并附带算法结构。正象GLib提供的基本类型和算法结构（如链表、哈希表等）一样，GObject的对象系统提供了一种灵活的、可扩展的、并容易映射（到其它语言）的面向对象的C语言框架。它的实质可以概括为：
* 
一个通用类型系统，用来注册任意的、轻便的、单根继承的、并能推导出任意深度的结构类型的界面，它照顾组合对象的定制、初始化和内存管理，类结构，保持对象的父子关系，处理这些类型的动态实现。也就是说，这些类型的实现是在运行时重置和卸载的；
* 
一个基本类型的实现集，如整型，枚举型和结构型等；
* 
一个基本对象体系之上的基本对象类型的实现的例子--GObject基本类型；
* 
一个信号系统，允许用户非常灵活的自定义虚的或重载对象的方法，并且能充当非常有效力的通知机制；
* 
一个可扩展的参数/变量体系，支持所有的能被用作处理对象属性或其它参数化类型的基本的类型。 

####类型（GType）与对象（GObject）

GLib中最有特色的是它的对象系统--GObject System，它是以Gtype为基础而实现的一套单根继承的C语言的面向对象的框架。

GType 是GLib 运行时类型认证和管理系统。GType API 是GObject的基础系统，所以理解GType是理解GObject的关键。Gtype提供了注册和管理所有基本数据类型、用户定义对象和界面类型的技术实现。（注意：在运用任一GType和GObject函数之前必需运行g_type_init()函数来初始化类型系统。）

为实现类型定制和注册这一目的，所有类型必需是静态的或动态的这二者之一。静态的类型永远不能在运行时加载或卸载，而动态的类型则可以。静态类型由g_type_register_static()创建，通过GTypeInfo结构来取得类型的特殊信息。动态类型则由g_type_register_dynamic()创建，用GTypePlugin结构来取代GTypeInfo，并且还包括g_type_plugin_*()系列API。这些注册函数通常只运行一次，目的是取得它们返回的专有类的类型标识。

还可以用g_type_register_fundamental来注册基础类型，它同时需要GTypeInfo和GTypeFundamentalInfo两个结构，事实上大多数情况下这是不必要的，因为系统预先定义的基础类型是优于用户自定义的。

（本文重点介绍创建和使用静态的类型。）
####对象的定义

在GObject系统中，对象由三个部分组成：

    对象的ID标识（唯一，无符号长整型，所有此类对象共同的标识）；
    对象的类结构（唯一，结构型，由对象的所有实例共同拥有）；
    对象的实例（多个，结构型，对象的具体实现）。 

基于GObject的对象到底是什么样的呢？下面是基于GObject的简单对象 -- Boy的定义代码：
```C
/* boy.h */
#ifndef __BOY_H__
#define __BOY_H__
#include <glib-object.h>
#define BOY_TYPE (boy_get_type())
#define BOY(obj) (G_TYPE_CHECK_INSTANCE_CAST((obj),BOY_TYPE,Boy))
typedef struct _Boy Boy;
typedef struct _BoyClass BoyClass;
struct _Boy {
GObject parent;
//
gint age;
gchar *name;
void (*cry)(void);
};
struct _BoyClass {
GObjectClass parent_class;
//
void (*boy_born)(void);
};
GType	boy_get_type(void);
Boy*  boy_new(void);
int	boy_get_age(Boy *boy);
void	boy_set_age(Boy *boy, int age);
char* boy_get_name(Boy *boy);
void	boy_set_name(Boy *boy, char *name);
Boy*  boy_new_with_name(gchar *name);
Boy*  boy_new_with_age(gint age);
Boy*  boy_new_with_name_and_age(gchar *name, gint age);
void  boy_info(Boy *boy);
#endif /* __BOY_H__*/
```
这是一段典型的C语言头文件定义，包括编译预处理，宏定义，数据结构定义和函数声明；首先要看的是两个数据结构对象Boy和BoyClass，

结构类型_Boy是Boy对象的实例，就是说我们每创建一个Boy对象，也就同时创建了一个Boy结构。Boy对象中的parent表示此对象的父类，GObject系统中所有对象的共同的根都是GObject类，所以这是必须的；其它的成员可以是公共的，这里包括表示年龄的age，表示名字的name和表示方法的函数指针cry，外部代码可以操作或引用它们。

结构类型_BoyClass是Boy对象的类结构，它是所有Boy对象实例所共有的。BoyClass中的parent_class是GObjectClass，同GObject是所有对象的共有的根一样，GObejctClass是所有对象的类结构的根。在BoyClass中我们还定义了一个函数指针boy_born，也就是说这一函数指针也是所有Boy对象实例共有的，所有的Boy实例都可以调用它；同样，如果需要的话，你也可以在类结构中定义其它数据成员。

其余的函数定义包括三种，一种是取得Boy对象的类型ID的函数boy_get_type，这是必须有的；另一种是创建Boy对象实例的函数boy_new和boy_new_with_*，这是非常清晰明了的创建对象的方式，当然你也可以用g_object_new函数来创建对象；第三种是设定或取得Boy对象属性成员的值的函数boy_get_*和boy_set_*。正常情况下这三种函数都是一个对象所必需的，另外一个函数boy_info用来显示此对象的当前状态。

宏在GObject系统中用得相当广泛，也相当重要，这里我们定义了两个非常关键的宏，BOY_TYPE宏封装了boy_get_type函数，可以直接取得并替代Boy对象的ID标识；BOY(obj)宏是G_TYPE_CHECK_INSTANCE_CAST宏的再一次封装，目的是将一个Gobject对象强制转换为Boy对象，这在对象的继承中十分关键，也经常用到。

####对象的实现

下面的代码实现了上面的Boy对象的定义：
```C
/* boy.c */
#include "boy.h"
enum { BOY_BORN, LAST_SIGNAL };
static gint boy_signals[LAST_SIGNAL] = { 0 };
static void boy_cry (void);
static void boy_born(void);
static void boy_init(Boy *boy);
static void boy_class_init(BoyClass *boyclass);
GType boy_get_type(void)
{
	static GType boy_type = 0;
	if(!boy_type)
	{
		static const GTypeInfo boy_info = {
			sizeof(BoyClass),
			NULL,NULL,
			(GClassInitFunc)boy_class_init,
			NULL,NULL,
			sizeof(Boy),
			0,
			(GInstanceInitFunc)boy_init
		};
		boy_type = g_type_register_static(G_TYPE_OBJECT,"Boy",&boy_info,0);
	}
	return boy_type;
}
static void boy_init(Boy *boy)
{
	boy->age = 0;
	boy->name = "none";
	boy->cry = boy_cry;
}
static void boy_class_init(BoyClass *boyclass)
{
	boyclass->boy_born = boy_born;
	boy_signals[BOY_BORN] = g_signal_new("boy_born",
				BOY_TYPE,
				G_SIGNAL_RUN_FIRST,
				G_STRUCT_OFFSET(BoyClass,boy_born),
				NULL,NULL,
				g_cclosure_marshal_VOID__VOID,
				G_TYPE_NONE, 0, NULL);
}
Boy *boy_new(void)
{
	Boy *boy;
	boy = g_object_new(BOY_TYPE, NULL);
	g_signal_emit(boy,boy_signals[BOY_BORN],0);
	return boy;
}
int boy_get_age(Boy *boy)
{
	return boy->age;
}
void boy_set_age(Boy *boy, int age)
{
	boy->age = age;
}
char *boy_get_name(Boy *boy)
{
	return boy->name;
}
void boy_set_name(Boy *boy, char *name)
{
	boy->name = name;
}
Boy*  boy_new_with_name(gchar *name)
{
	Boy* boy;
	boy = boy_new();
	boy_set_name(boy, name);
	return boy;
}
Boy*  boy_new_with_age(gint age)
{
	Boy* boy;
	boy = boy_new();
	boy_set_age(boy, age);
	return boy;
}
Boy *boy_new_with_name_and_age(gchar *name, gint age)
{
	Boy *boy;
	boy = boy_new();
	boy_set_name(boy,name);
	boy_set_age(boy,age);
	return boy;
}
static void boy_cry (void)
{
	g_print("The Boy is crying ......\n");
}
static void boy_born(void)
{
	g_print("Message : A boy was born .\n");
}
void  boy_info(Boy *boy)
{
	g_print("The Boy name is %s\n", boy->name);
	g_print("The Boy age is %d\n", boy->age);
}
```
在这段代码中，出现了实现Boy对象的关键函数，这是在Boy对象的定义中未出现的，也是没必要出现的。就是两个初始化函数，boy_init和boy_class_init，它们分别用来初始化实例结构和类结构。它们并不被在代码中明显调用，关键是将其用宏转换为地址指针，然后赋值到GTypeInfo结构中，然后由GType系统自行处理，同时将它们定义为静态的也是非常必要的。

GTypeInfo结构中定义了对象的类型信息，包括以下内容：

    包括类结构的长度（必需，即我们定义的BoyClass结构的长度）；
    基础初始化函数（base initialization function，可选）；
    基础结束化函数（base finalization function，可选）；

（以上两个函数可以对对象使用的内存来做分配和释放操作，使用时要用GBaseInitFunc和GBaseFinalizeFunc来转换为指针，本例中均未用到，故设为NULL。）
类初始化函数（即我们这里的boy_class_init函数，用GclassInit宏来转换，可选，仅用于类和实例类型）；
类结束函数（可选）；
实例初始化函数（可选，即我们这里的boy_init函数）；
最后一个成员是GType变量表（可选）。 

定义好GTypeInfo结构后就可以用g_type_register_static函数来注册对象的类型了。

g_type_register_static函数用来注册对象的类型，它的第一个参数是表示此对象的父类的对象类型，我们这里是G_TYPE_OBJECT，这个宏用来表示GObject的父类；第二个参数表示此对象的名称，这里为"Boy"；第三个参数是此对象的GTypeInfo结构型指针，这里赋值为&boyinfo；第四个参数是对象注册成功后返回此对象的整型ID标识。

g_object_new函数，用来创建一个基于G_OBJECT的对象，它可以有多个参数，第一个参数是上面说到的已注册的对象标识ID；第二个参数表示后面参数的数量，如果为0，则没有第三个参数；第三个参数开始类型都是GParameter类型，它也是一个结构型，定义为：
```C
struct GParameter{
		const gchar* name;
		GValue value;
	};
```
关于GValue，它是变量类型的统一定义，它是基础的变量容器结构，用于封装变量的值和变量的类型，可以GOBJECT文档的GVALUE部分。

####信号的定义和应用

在GObject系统中，信号是一种定制对象行为的手段，同时也是一种多种用途的通知机制。初学者可能是在GTK+中首先接触到信号这一概念的，事实上在普通的字符界面编程中也可以正常应用，这可能是很多初学者未曾想到的。

一个对象可以没有信号，也可以有多个信号。当有一或多个信号时，信号的名称定义是必不可少的，此时C语言的枚举类型的功能就凸显出来了，用LAST_SIGNAL来表示最后一个信号（不用实现的信号）是一种非常良好的编程风格。这里为Boy对象定义了一个信号BOY_BORN，在对象创建时发出，表示Boy对象诞生。

同时还需要定义静态的整型指针数组来保存信号的标识，以便于下一步处理信号时使用。

对象的类结构是所有对象的实例所共有的，我们将信号也定义在对象的类结构中，如此信号同样也是所有对象的实例所共有的，任意一个对象的实例都可以处理信号。因此我们有必要在在类初始化函数中创建信号（这也可能是GObject设计者的初衷）。函数g_signal_new用来创建一个新的信号，它的详细使用方法可以在GObject的API文档中找到。信号创建成功后，返回一个信号的标识ID，如此就可以用发射信号函数g_signal_emit向指定义对象的实例发射信号，从而执行相应的功能。

本例中每创建一个新的Boy对象，就会发射一次BOY_BORN信号，也就会执行一次我们定义的boy_born函数，也就输出一行"Message : A boy was born ."信息。

回页首
对象的属性和方法

对象实例所有的属性和方法一般都定义在对象的实例结构中，属性定义为变量或变量指针，而方法则定义为函数指针，如此，我们一定要定义函数为static类型，当为函数指针赋值时，才能有效。

回页首
对象的继承

以下为继承自Boy对象的Man对象的实现，Man对象在Boy对象的基础上又增加了一个属性job和一个方法bye。

#ifndef __MAN_H__
#define __MAN_H__
#include "boy.h"
#define MAN_TYPE  (man_get_type())
#define MAN(obj) (G_TYPE_CHECK_INSTANCE_CAST((obj),MAN_TYPE,Man))
typedef struct _Man Man;
typedef struct _ManClass ManClass;
struct _Man {
	Boy parent;
	char *job;
	void (*bye)(void);
};
struct _ManClass {
	BoyClass parent_class;
};
GType man_get_type(void);
Man*  man_new(void);
gchar* man_get_gob(Man *man);
void  man_set_job(Man *man, gchar *job);
Man*  man_new_with_name_age_and_job(gchar *name, gint age, gchar *job);
void man_info(Man *man);
#endif //__MAN_H__
/* man.c */
#include "man.h"
static void man_bye(void);
static void man_init(Man *man);
static void man_class_init(Man *man);
GType man_get_type(void)
{
	static GType man_type = 0;
	if(!man_type)
	{
		static const GTypeInfo man_info = {
			sizeof(ManClass),
			NULL, NULL,
			(GClassInitFunc)man_class_init,
			NULL, NULL,
			sizeof(Man),
			0,
			(GInstanceInitFunc)man_init
		};
		man_type = g_type_register_static(BOY_TYPE, "Man", &man_info, 0);
	}
	return man_type;
}
static void man_init(Man *man)
{
	man->job = "none";
	man->bye = man_bye;
}
static void man_class_init(Man *man)
{
}
Man*  man_new(void)
{
	Man *man;
	man = g_object_new(MAN_TYPE, 0);
	return man;
}
gchar* man_get_gob(Man *man)
{
	return man->job;
}
void  man_set_job(Man *man, gchar *job)
{
	man->job = job;
}
Man*  man_new_with_name_age_and_job(gchar *name, gint age, gchar *job)
{
	Man *man;
	man = man_new();
	boy_set_name(BOY(man), name);
	boy_set_age(BOY(man), age);
	man_set_job(man, job);
	return man;
}
static void man_bye(void)
{
	g_print("Goodbye everyone !\n");
}
void man_info(Man *man)
{
	g_print("the man name is %s\n", BOY(man)->name);
	g_print("the man age is %d\n", BOY(man)->age);
	g_print("the man job is %s\n", man->job);
}

关键在于定义对象时将父对象实例定义为Boy，父类设定为BoyClass，在注册此对象时将其父对象类型设为BOY_TYPE，在设定对象属性时如用到父对象的属性要强制转换下，如取得对象的name属性，就必须用BOY(obj)->name，因为Man本身没有name属性，而其父对象Boy有，所以用BOY宏将其强制为Boy类型的对象。

回页首
测试我们定义的对象

#include <glib.h>
#include "boy.h"
#include "man.h"
int main(int argc, char *argv[])
{
	Boy *tom, *peter;
	Man *green, *brown;	
	g_type_init();//注意，初始化类型系统，必需
	tom = boy_new_with_name("Tom");
	tom->cry();
	boy_info(tom);
	peter = boy_new_with_name_and_age("Peter", 10);
	peter->cry();
	boy_info(peter);
	green = man_new();
	boy_set_name(BOY(green), "Green");
//设定Man对象的name属性用到其父对象Boy的方法
	boy_set_age(BOY(green), 28);
	man_set_job(green, "Doctor");
	green->bye();
	man_info(green);
	brown = man_new_with_name_age_and_job("Brown", 30, "Teacher");
	brown->bye();
	man_info(brown);
}
Makefile文件如下：
CC = gcc
all:
	$(CC) -c boy.c `pkg-config --cflags glib-2.0 gobject-2.0`
	$(CC) -c man.c `pkg-config --cflags glib-2.0 gobject-2.0`
	$(CC) -c main.c `pkg-config --cflags glib-2.0 gobject-2.0`
	$(CC) -o simple boy.o man.o main.o `pkg-config --libs glib-2.0 gobject-2.0`
执行make命令编译，编译结束后，执行./simple运行此测试程序，输出结果如下：
Message : A boy was born .
The Boy is crying ......
The Boy name is Tom
The Boy age is 0
Message : A boy was born .
The Boy is crying ......
The Boy name is Peter
The Boy age is 10
Goodbye everyone !
the man name is Green
the man age is 28
the man job is Doctor
Goodbye everyone !
the man name is Brown
the man age is 30
the man job is Teacher

Makefile中用到`pkg-config -cflags -libs gobject-2.0`，在GLIB中将线程（gthread），插件（gmoudle）和对象系统（gobject）这三个子系统区别对待，编译时要注意加入相应的参数。

本文只是概要的介绍了如何定义和实现GObject对象，GObject系统中还有很多相关内容，如：枚举和标识类型（Enumeration and flags types）；Gboxed，是Gtype系统中注册一种封装为不透明的C语言结构类型的机制；许多对象用到的参数对象都是C结构类型，使用者不必了解其结构的内部定义，即不透明，GBoxed即是实现这一功能的机制；标准的参数和变量类型的定义（Standard Parameter and Value Types）等，它们都以C语言来开发，是深入了解和掌握GObject的关键。

透过以上代码实现，我们还可以看出，以GLIB为基础的GTK+/GNOME开发环境所具有的独特的编程风格和独到的开发思想。这一点在长期的编程实践中会体验得更深刻。

有了GObject系统这一基础，GTK+通过它将X窗口环境中的控件（Widget）巧妙的封装起来，这使开发LINUX平台上的GUI应用程序更方便，更快捷。

以上代码在Redhat 8.0 Linux平台，GLIB2.2.1环境下编译通过。

回页首
感谢

本文的写作参考了中国LINUX论坛的网友hoyt的文章，可以在gtkvb.cffd.org.cn找到，在此表示感谢。
参考资料

    本文的所有代码可以在这里 下载。
    Thomas Hunger写的文章： Gobject tutorial
    中国 linux 论坛的网友 hoyt 的网页 http://gtkvb.cosoft.org.cn/上的文章
    与本文相关的另一篇文章 《浅析GLib》

条评论

请 登录 或 注册 后发表评论。

添加评论:

注意：评论中不支持 HTML 语法


有新评论时提醒我剩余 1000 字符

 共有评论 (2)

badly written.I guess the author didn't understand GObject tutorial himself.

由 Hwa 于 2011年06月17日发布

报告滥用

简单明了 学习gsteamer 的人需要看一下先

由 gogoer 于 2011年04月11日发布

报告滥用

    IBM Bluemix 资源中心
    IBM Bluemix 资源中心

    文章、教程、演示，帮助您构建、部署和管理云应用。
    developerWorks 中文社区
    developerWorks 中文社区

    立即加入来自 IBM 的专业 IT 社交网络。
    Bluemixathon 挑战赛
    Bluemixathon 挑战赛

    为灾难恢复构建应用，赢取现金大奖。

回页首

    帮助
    联系编辑
    提交内容
    订阅源

    新浪微博
    报告滥用
    使用条款
    第三方提示

    隐私条约
    浏览辅助
    IBM 教育学院教育培养计划
    IBM 创业企业全球扶持计划
    ISV 资源 (英语)

    dW 中国每周时事通讯

    选择语言：
    English
    中文
    日本語
    Русский
    Português (Brasil)
    Español
    Việt

IBM®
