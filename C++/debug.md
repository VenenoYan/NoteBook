
### 调试信息

输出方法有很多种,  例如直接用printf,  或者出错时使用perror,fprintf等将信息直接打印到终端上,在Qt上面一般使用qDebug，而守护进程则一般是使用syslog将调试信息输出到日志文件中等等...
宏 ##__VA_ARGS__, __FILE__, __LINE__ 和__FUNCTION__,下面介绍一下这几个宏:
　　1)  __VA_ARGS__ 是一个可变参数的宏，很少人知道这个宏，这个可变参数的宏是新的C99规范中新增的，目前似乎只有gcc支持（VC6.0的编译器不支持）。宏前面加上##的作用在于，当可变参数的个数为0时，这里的##起到把前面多余的","去掉的作用,否则会编译出错, 你可以试试。
　　2) __FILE__ 宏在预编译时会替换成当前的源文件名
　　3) __LINE__宏在预编译时会替换成当前的行号
　　4) __FUNCTION__宏在预编译时会替换成当前的函数名称
　　有了以上这几个宏，特别是有了__VA_ARGS__ ，调试信息的输出就变得灵活多了。
　　有时，我们想把调试信息输出到屏幕上，而有时则又想把它输出到一个文件中，可参考下面的例子：
```C++
//debug.c
#include <stdio.h>
#include <string.h>
//开启下面的宏表示程序运行在调试版本, 否则为发行版本, 这里假设只有调试版本才输出调试信息
#define _DEBUG
#ifdef _DEBUG
    //开启下面的宏就把调试信息输出到文件，注释即输出到终端
    #define DEBUG_TO_FILE
    #ifdef DEBUG_TO_FILE
        //调试信息输出到以下文件
        #define DEBUG_FILE "/tmp/debugmsg"
        //调试信息的缓冲长度
        #define DEBUG_BUFFER_MAX 4096
        //将调试信息输出到文件中
        #define printDebugMsg(moduleName, format, ...) {\
            char buffer[DEBUG_BUFFER_MAX+1]={0};\
            snprintf( buffer, DEBUG_BUFFER_MAX \
                    , "[%s] "format" File:%s, Line:%d\n", moduleName, ##__VA_ARGS__, __FILE__, __LINE__ );\
            FILE* fd = fopen(DEBUG_FILE, "a");\
            if ( fd != NULL ) {\
                fwrite( buffer, strlen(buffer), 1, fd );\
                fflush( fd );\
                fclose( fd );\
            }\
        }
    #else
        //将调试信息输出到终端
        #define printDebugMsg(moduleName, format, ...) \
                  printf( "[%s] "format" File:%s, Line:%d\n", moduleName, ##__VA_ARGS__, __FILE__, __LINE__ );
    #endif //end for #ifdef DEBUG_TO_FILE
#else
    //发行版本，什么也不做
    #define printDebugMsg(moduleName, format, ...)
#endif  //end for #ifdef _DEBUG
int main(int argc, char** argv)
{
    int data = 999;
    printDebugMsg( "TestProgram", "data = %d", data );
    return 0;
}```
 