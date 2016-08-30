1. 
实现一个固定长的队列，要求线程安全。
```C++
#include <iostream>
#include <pthread.h>
#include <unistd.h>
using namespace std;

struct Node
{
    void * data;
    struct Node *next;
};


struct QNode
{
    struct Node *front;
    struct Node *tail;
    unsigned int len;
};


struct Qlist
{
    struct QNode *qlist;
    pthread_mutex_t m_lock;
};


class MyQueue
{
   public:
       MyQueue();
       int Push(void *pData);
       void* Pop();
       ~MyQueue();
   private:
       struct Qlist *m_qlist;
};


MyQueue::MyQueue()
{
    m_qlist = (struct Qlist *)malloc(sizeof(struct Qlist));
    m_qlist->qlist = (struct QNode *)malloc(sizeof(struct QNode));


    cout<< "Create Qlist" <<endl;


    if(m_qlist->qlist != NULL)
    {
        m_qlist->qlist->front = NULL;
        m_qlist->qlist->tail = NULL;
        m_qlist->qlist->len = 0;
    }
    pthread_mutex_init(&m_qlist->m_lock,NULL);
}


int MyQueue::Push(void *pData)
{
    struct Node *INode = NULL;
    if(NULL == m_qlist )
    {
        cout<< "Push Tail please initialize the list"<<endl;
        return -1;
    }
    if(NULL == m_qlist->qlist)
    {
        m_qlist->qlist = (struct QNode *)malloc(sizeof(struct QNode));
    }


    INode = (struct Node *)malloc(sizeof(struct Node));
    INode->data = pData;
    INode->next = NULL;
    cout<< "push lock "<<endl;
    pthread_mutex_lock(&m_qlist->m_lock);
    cout<<"push "<<(char*)INode->data;
    if(m_qlist->qlist->tail != NULL)
    {
        m_qlist->qlist->tail->next = INode;
        m_qlist->qlist->tail = INode;
    }
    else //if(m_qlist->qlist->tail == NULL)
    {
        m_qlist->qlist->front = m_qlist->qlist->tail =  INode;
    }
    m_qlist->qlist->len++;
    pthread_mutex_unlock(&m_qlist->m_lock);
    cout<<"push unlock"<<endl;
    cout<<endl; 
    return m_qlist->qlist->len;
}


void* MyQueue::Pop()
{
    void *pData;
    struct Node *pNode;


    if((NULL == m_qlist) || (0 >= m_qlist->qlist->len) || (m_qlist->qlist == NULL))
    {
        return NULL;
    }


    cout<< "Pop Head" <<endl;
    pthread_mutex_lock(&m_qlist->m_lock);
    
    m_qlist->qlist->len -= 1;
    pNode = m_qlist->qlist->front;
    pData = pNode->data;
    cout<<"pop "<<(char *)pData;
    m_qlist->qlist->front = m_qlist->qlist->front->next;


    if(m_qlist->qlist->len == 0)
    {
        m_qlist->qlist->tail = NULL;
    }
    free(pNode);
    pthread_mutex_unlock(&m_qlist->m_lock);
    cout<< "pop un_lock" <<endl;
    cout<<endl;
    return pData;
}


MyQueue::~MyQueue()
{
    struct Node *pNode = NULL;
    if(m_qlist == NULL)
        return ;
    
    cout<<"Destroy Queue list"<<endl;


    if(m_qlist != NULL)
    {
    
        while(m_qlist->qlist->len > 0)
        {


            pNode = m_qlist->qlist->front;


            cout<<"delete front: "<<(char *)(m_qlist->qlist->front->data);
            if(pNode->data != NULL)
            {


                free(pNode->data);
            }
            m_qlist->qlist->front = m_qlist->qlist->front->next;
            m_qlist->qlist->len--;
            free(pNode);
        }


        free(m_qlist->qlist);
        free(m_qlist);
    }
    pthread_mutex_destroy(&m_qlist->m_lock);
}


void *Thread_push(void *arg)
{
    MyQueue *tasklist = (MyQueue *)arg;
    char *buff;
    
    for(int i=0;i<4;i++)
    {
        buff = new char(10);
        sprintf(buff,"Msg %d\n",i);
        tasklist->Push(buff);
        sleep(2);
    }
    return (void *)0;
}


void *Thread_pop(void *arg)
{
    MyQueue *tasklist = (MyQueue *)arg;
    char *buff;


    for(int i=0;i<3;i++)
    {
        buff = (char *)tasklist->Pop();
        sleep(3);
    }
    return (void *)0;
}


int main()
{
    MyQueue taskQueue;


    pthread_t task_push;
    pthread_t task_pop;


    pthread_create(&task_push,NULL,Thread_push,&taskQueue);
    pthread_create(&task_pop,NULL,Thread_pop,&taskQueue);


    pthread_join(task_push,NULL);
    pthread_join(task_pop,NULL);


    return 0;
}


```