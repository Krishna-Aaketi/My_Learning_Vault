## ----------------------Create Thread programms------
 
### 1.Prints "Hello, World!"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 1.Write a C program to create a thread that prints "Hello, World!"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread(void *arg);
int main(void)
{
  pthread_t t_id;                                               // Thread ID
  if(pthread_create(&t_id,NULL,create_thread,"Hello World")!=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(t_id,NULL);                                      // wait for the thread to finish
  printf("main thread id=%u\n",(unsigned int)pthread_self());   // get pthread id
  printf("process id=%u\n",getpid());                           // get process id
}

void *create_thread(void *arg)                                // thread function
{
  char *ptr=(char *)(arg);
  printf("%s\n",ptr);
  printf("process id=%u\n",getpid());                        //get process id
  return 0;
}
```
## 2.Multiple threads,each printing its own message? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 2.Write a c program to create multiple threads,each printing its own message? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread1(void *arg);
void *create_thread2(void *arg);
void *create_thread3(void *arg);
void *create_thread4(void *arg);
int main(void)
{
  pthread_t tid1,tid2,tid3,tid4;                    // Threads ID
  if(pthread_create(&tid1,NULL,create_thread1,NULL)!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  if(pthread_create(&tid2,NULL,create_thread2,NULL)!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  if(pthread_create(&tid3,NULL,create_thread3,NULL)!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  if(pthread_create(&tid4,NULL,create_thread4,NULL)!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }    
  pthread_join(tid1,NULL);                          //wait for the thread to finish
  pthread_join(tid2,NULL);                            
  pthread_join(tid3,NULL);                           
  pthread_join(tid4,NULL);                            
  return 0;
}

void *create_thread1(void *arg)                                // threads function 
{                         
  printf("I am 1st Thread function:Hi\n");                      
  pthread_exit(0);                                             // To terminate thread function
}

void *create_thread2(void *arg)                                // thread function 
{                         
  printf("I am 2nd Thread function:Hi\n");                       
  pthread_exit(0);
}

void *create_thread3(void *arg)                                // thread function 
{                         
  printf("I am 3rd Thread function:Hi\n");                     
  pthread_exit(0);
}

void *create_thread4(void *arg)                                // thread function 
{                         
  printf("I am 4th Thread function:Hi\n");                        
  pthread_exit(0);
}
```
## 3.Print numbers from 1 to 10 concurrently?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 3.Develop a C program to create two threads that print numbers from 1 to 10 concurrently? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid1,tid2;                                             // Thread ID
  if(pthread_create(&tid1,NULL,create_thread,"thread_1")!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  if(pthread_create(&tid2,NULL,create_thread,"thread_2")!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid1,NULL);                               // wait for the thread to finish
  pthread_join(tid2,NULL);                              // wait for the thread to finish
  printf("main thread id=%u\n",(unsigned int)pthread_self()); // get pthread id 
  printf("process id=%u\n",getpid());    // get process id
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  char *str=(void *)(arg);
  int i=0;
  for(i=0;i<=10;i++)
  {
    printf("%s:%d\n",str,i);
  }  
}

```
## 4.Calculates the factorial of a given number? 
```c

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 4.Implement a C program to create a thread that calculates the factorial of a given number? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;                   // Thread
  int number=0;
  if(pthread_create(&tid,NULL,create_thread,NULL)!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  int factorial=1,number=0,i;
  printf("Enter Number:");
  scanf("%d",&number);
  if(number<0)
  {
    printf("only 0< values\n");
    pthread_exit(0);
  }
  for(i=1;i<=number; i++)
  {
    factorial *= i;
  }
  printf("factorial=%d\n",factorial);
} 

```
## 5.Print their thread IDs?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 5.Write a C program to create two threads that print their thread IDs?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid1,tid2;                               // Thread
  if(pthread_create(&tid1,NULL,create_thread,"thread_1")!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  if(pthread_create(&tid2,NULL,create_thread,"thread_2")!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid1,NULL);                          // wait for the thread to finish
  pthread_join(tid2,NULL);                          // wait for the thread to finish
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  char *str=(char *)arg;
  printf("%s:%ld\n",str,pthread_self());
} 

```
## 6.Prints the sum of two numbers?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 *6.Develop a C program to create a thread that prints the sum of two numbers? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>
 
struct two_args
{
  int a;
  int b;
};

void *create_thread(void *arg);

int main(void)
{
  struct two_args nums;
  pthread_t tid;                                    // Thread
  printf("Enter Numbers :");
  scanf("%d%d",&nums.a,&nums.b);
  if(pthread_create(&tid,NULL,create_thread,(void *)&nums)!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  struct two_args *nums=(struct two_args *)arg;	
  printf("sum=%d\n",(nums->a)+(nums->b));
} 
```
## 7.Calculates the square of a number?  
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 7.Implement a C program to create a thread that calculates the square of a number?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>
 
void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  int num;
  printf("Enter Numbers :");
  scanf("%d",&num);
  if(pthread_create(&tid,NULL,create_thread,(void *)&num)!=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  int num=*(int *)arg;	
  printf("square=%d\n",num*num);
} 
```
## 8.Prints the current date and time?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 8.Write a C program to create a thread that prints the current date and time? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include<stdio.h>
#include<time.h>
#include<pthread.h>
 
void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  pthread_create(&tid,NULL,create_thread,NULL);     // Create the thread
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  time_t now;
  struct tm *current_time;
  time(&now);
  current_time=localtime(&now);
  printf("time=%s\n",asctime(current_time));
} 
```
## 9.Checks if a number is prime?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 9.Develop a C program to create a thread that checks if a number is prime?    *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
 
void *create_thread(void *arg);

int main(void)
{
  int num;
  int *flag;
  pthread_t tid;
  printf("Enter Number:");
  scanf("%d",&num);
  pthread_create(&tid,NULL,create_thread,(void *)&num);     // Create the thread
  pthread_join(tid,(void **)&flag);                      // wait for the thread to finish
  if(*flag==0)
  {
    printf("Given number is not prime\n");
  }
  else
  {
    printf("Given number is prime\n");
  }
  free(flag);
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  int *ptr=(int *)malloc(sizeof(int));
  int num=*(int *)arg;
  if(ptr==NULL)
  {
    printf("Malloc failed\n");
    pthread_exit(0);
  }
  int i=0;
  if(num <=0)
  {
    *ptr=0;
    return ptr;
  }
  *ptr=1;
  for(i=2; i*i <=num; ++i)
  {
    if(num%i==0)
    {
      *ptr=0;
      return ptr;
      break;
    }
  }
  return ptr;
} 
```
## 10.Checks if a given string is a palindrome? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
 * 10.Implement a C program to create a thread that checks if a given string is a palindrome?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
 
void *create_thread(void *arg);

int main(void)
{
  char str[100];
  int *flag;
  pthread_t tid;
  printf("Enter string(99<):");
  scanf("%s",str);
  if(pthread_create(&tid,NULL,create_thread,(void *)str)!=0)     // Create the thread
  {
    printf("thread Creation is failed\n");
    return 7;
  }
  pthread_join(tid,(void **)&flag);                      // wait for the thread to finish
  if(*flag==0)
  {
    printf("Given string is not palindrome\n");
  }
  else
  {
    printf("Given string is palindrome\n");
  }
  free(flag);
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  int *ptr=(int *)malloc(sizeof(int));
  char *str=(char *)arg;
  int len=0,i=0;
  if(ptr==NULL)
  {
    printf("Malloc failed\n");
    pthread_exit(0);
  }
  *ptr=1;
  for(i=0; i<len;i++)
  {
    if(str[i]==str[--len])
    {
      *ptr=0;
      return ptr;
      break;
    }
  }
  return ptr;
} 
```
### 11.Prints "Hello, World!" with thread synchronization?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 11.Write a C program to create a thread that prints "Hello, World!" with thread synchronization?*
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

pthread_mutex_t lock;
void *create_thread(void *arg);
int main(void)
{
  pthread_t t_id;      // Thread ID
  if(pthread_mutex_init(&lock,NULL)!=0)
  {
    printf("Mutex is failed\n");
    return 0;
  }
  if(pthread_create(&t_id,NULL,create_thread,"Hello World")!=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(t_id,NULL);                                    // wait for the thread to finish
  printf("main thread id=%u\n",(unsigned int)pthread_self()); // get pthread id
  printf("process id=%u\n",getpid());                         // get process id
  pthread_mutex_destroy(&lock);
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  char *ptr=(char *)(arg);
  pthread_mutex_lock(&lock);
  printf("%s\n",ptr);
  pthread_mutex_unlock(&lock);
  printf("process id=%u\n",getpid());                        //get process id
  return 0;
}
```
## 12.Print their thread IDs and synchronize their output
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 12.Develop a C program to create two threads that print their thread IDs and synchronize their output *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

pthread_mutex_t lock;                  // syncronization mechanism
void *create_thread(void *arg);

int main(void)
{
  if(pthread_mutex_init(&lock,NULL) !=0)
  {
    printf("mutex lock is failed\n");
    return 0;
  }
  pthread_t tid1,tid2;                               // Thread
  pthread_create(&tid1,NULL,create_thread,"Thread_1");     // Create the thread
  pthread_create(&tid2,NULL,create_thread,"Thread_2");     // Create the thread
  pthread_join(tid1,NULL);                          // wait for the thread to finish
  pthread_join(tid2,NULL);                        
  pthread_mutex_destroy(&lock);
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  char *str=(char *)arg;
  pthread_mutex_lock(&lock);
  printf("%s:%ld\n",str,pthread_self());
  pthread_mutex_unlock(&lock);
} 
```
## 13.Random numbers and synchronizes access to a shared buffer?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 13.Implement a C program to create a thread that generates random numbers and synchronizes access to a shared buffer? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

void *create_thread(void *arg);
pthread_mutex_t lock;                  // syncronization mechanism
int buf[100];

int main(void)
{
  if(pthread_mutex_init(&lock,NULL) !=0)
  {
    printf("mutex lock is failed\n");
    return 0;
  }
  pthread_t tid1,tid2;                               // Thread
  pthread_create(&tid1,NULL,create_thread,NULL);     // Create the thread
  pthread_join(tid1,NULL);                          // wait for the thread to finish
  pthread_mutex_destroy(&lock);
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  int i=0,size=10,num,min=10,max=50;
  while(i<size)
  {
    num=rand() % (max -min + 1);
    pthread_mutex_lock(&lock);
    buf[i]=num;
    i++;
    pthread_mutex_unlock(&lock);
  }
  for(i=0;i<size;i++)
  {
    printf("%d\n",buf[i]);
  }
} 
```
## 14.Performs addition of two numbers with mutex locks?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 14.Write a C program to create a thread that performs addition of two numbers with mutex locks? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>
 
struct two_args
{
  int a;
  int b;
};

pthread_mutex_t lock;
void *create_thread(void *arg);

int main(void)
{
  struct two_args nums;
  pthread_t tid;                                    // Thread
  printf("Enter Numbers :");
  scanf("%d%d",&nums.a,&nums.b);
  if(pthread_mutex_init(&lock,NULL) !=0)
  {
    printf("mutex lock is failed\n");
    return 0;
  }
  pthread_create(&tid,NULL,create_thread,(void *)&nums);     // Create the thread
  pthread_join(tid,NULL);                       // wait for the thread to finish
  pthread_mutex_destroy(&lock);
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  struct two_args *nums=(struct two_args *)arg;	
  pthread_mutex_lock(&lock);
  printf("sum=%d\n",(nums->a)+(nums->b));
  pthread_mutex_unlock(&lock);
  pthread_exit(0);
} 

```
## 15.Increment and decrement a shared variable,respectively, using mutex locks?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 15.Implement a C program to create two threads that increment and decrement a shared variable,  *
 * respectively, using mutex locks?                                                                *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

pthread_mutex_t lock;
int num=0;
void *create_thread1(void *arg);
void *create_thread2(void *arg);

int main(void)
{
  pthread_t tid1,tid2;                                     // Thread
  if(pthread_mutex_init(&lock,NULL) !=0 )
  {
    printf("mutex is failed\n");
    return 17;
  }  
  pthread_create(&tid1,NULL,create_thread1,"increment_Thread");     // Create the thread
  pthread_create(&tid2,NULL,create_thread2,"decrement_Thread");     // Create the thread
  pthread_join(tid1,NULL);                          // wait for the thread to finish
  pthread_join(tid2,NULL);             
  pthread_mutex_destroy(&lock);
  return 0; 
}

void *create_thread1(void *arg)                                // thread function 
{
  int i=0;
  char *str=(char *)arg;
  while(i<4)
  {
    pthread_mutex_lock(&lock);
    printf("%s:%d\n",str,num++);
    sleep(5);
    pthread_mutex_unlock(&lock);
    i++;
  }
} 

void *create_thread2(void *arg)                                // thread function 
{
  char *str=(char *)arg;
  int i=0;
  while(i<4)
  {
    pthread_mutex_lock(&lock);
    printf("%s:%d\n",str,num--);
    pthread_mutex_unlock(&lock);
    i++;
  }
} 
```
## 16.reads input from the user and synchronizes access to shared resources
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 16.Develop a C program to create a thread that reads input from the user and synchronizes     *
 * access to shared resources?                                                                   *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

pthread_mutex_t lock;
char str[100];
void *create_thread(void *arg);
int main(void)
{
  if(pthread_mutex_init(&lock,NULL) !=0)
  {
    printf("Mutex lock is failed\n");
    return 0;
  }
  pthread_t t_id;                                             // Thread ID
  pthread_create(&t_id,NULL,create_thread,NULL);     // Create the thread
  pthread_join(t_id,NULL);         // wait for the thread to finish
  pthread_mutex_destroy(&lock);
}

void *create_thread(void *arg)                                // thread function 
{
  printf("Enter string:\n");
  pthread_mutex_lock(&lock);
  scanf("%s",str);
  printf("the string is %s\n",str);
  pthread_mutex_unlock(&lock);
  return 0;
}
```
## 17.Prints prime numbers up to a given limit with mutex locks?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 17.Implement a C program to create a thread that prints prime numbers up to a given limit with mutex locks? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
 
pthread_mutex_t lock;
void *create_thread(void *arg);

int main(void)
{
  int num;
  int *flag;
  pthread_t tid;
  printf("Enter Number:");
  scanf("%d",&num);
  if(pthread_mutex_init(&lock,NULL) != 0)
  {
    printf("Mutex lock failed\n");
  }
  pthread_create(&tid,NULL,create_thread,(void *)&num);     // Create the thread
  pthread_join(tid,NULL);         // wait for the thread to finish
  pthread_mutex_destroy(&lock);
  printf("\n");
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  int num=*(int *)arg,i=0,j=0,flag;
  if(num <=0)
  {
    pthread_exit(0);
  }
  for(j=2; j<=num ;j++)
  {
    flag=1;
    for(i=2; i*i <=j; ++i)
    {
      if(j%i==0)
      {
	flag=0;
        continue;
      }
    }
    if(flag==1)
    {
      pthread_mutex_lock(&lock);
      printf("%d ",j);
      pthread_mutex_unlock(&lock);
    }
  }
} 

```
## 18.calculates the sum of Fibonacci numbers up to a given limit mutex locks 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 18.Implement a C program to create a thread that calculates the sum of              *
 * Fibonacci numbers up to a given limit using dynamic programming with mutex locks?   *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

#define MAX 100

pthread_mutex_t lock;

// Shared structure to pass data and store result
struct Data 
{
    int limit;
    long long sum;
};

void *create_thread(void *arg); 

int main(void) 
{
  pthread_t tid;
  struct Data data;
  printf("Enter the Fibonacci limit(n): ");
  scanf("%d", &data.limit);
  if(data.limit < 0 || data.limit >= MAX)
  {
     printf("Please enter a limit between 0 and %d.\n", MAX - 1);
     return 1;
  }
  if(pthread_mutex_init(&lock, NULL) != 0)
  {
    printf("Mutex init failed\n");
    return 1;
  }
  pthread_create(&tid, NULL,create_thread, (void *)&data);
  pthread_join(tid, NULL);
  printf("Sum of first %d Fibonacci numbers is: %lld\n", data.limit, data.sum);
  pthread_mutex_destroy(&lock);
  return 0;
}

// Thread function
void *create_thread(void *arg) 
{
  struct Data *data = (struct Data *)arg;
  int limit = data->limit,i=0;
  long long fib[MAX];
  fib[0] = 0;
  fib[1] = 1;
  pthread_mutex_lock(&lock);
  data->sum = fib[0] + fib[1];
  for (i = 2; i <= limit; i++) 
  {
    fib[i] = fib[i-1] + fib[i-2];
    data->sum += fib[i];
  }
  pthread_mutex_unlock(&lock);
  pthread_exit(NULL);
}
```
### 19.Given year is a leap year using dynamic programming with mutex locks?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 19.Write a C program to create a thread that checks if a given year is a leap year using  *
 * dynamic programming with mutex locks?                                                     *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

pthread_mutex_t lock;

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  int year;
  printf("Enter the year: ");
  scanf("%d", &year);
  if(year <= 0)
  {
     printf("Please enter Positive values\n");
     return 1;
  }
  if(pthread_mutex_init(&lock, NULL) != 0)
  {
    printf("Mutex init failed\n");
    return 1;
  }
  pthread_create(&tid, NULL,create_thread, (void *)&year);
  pthread_join(tid, NULL);
  pthread_mutex_destroy(&lock);
  return 0;
}

// Thread function
void *create_thread(void *arg)
{
  int year=*(int *)arg;
  if(((year%4==0) && (year%100 !=0)) || (year % 400 ==0))
  {
    pthread_mutex_lock(&lock);
    printf("Given year is leap year\n");
    pthread_mutex_unlock(&lock);
  }
  else
  {
    printf("Given year is not a leap year\n");
  }
  pthread_exit(NULL);
}
```
### 20.Checks if a given string is a palindrome using dynamic programming with mutex locks?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 20.Write a C program to create a thread that checks if a given string is a palindrome using *
 * dynamic programming with mutex locks?                                                       *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
#include<string.h>

pthread_mutex_t lock;
void *create_thread(void *arg);

int main(void)
{
  char str[100];
  pthread_t tid;
  printf("Enter string(99<):");
  scanf("%s",str);
  if(pthread_mutex_init(&lock,NULL) != 0)
  {
    printf("mutex lock is failed\n");
    return 0;
  }
  pthread_create(&tid,NULL,create_thread,(void *)str);     // Create the thread
  pthread_join(tid,NULL);                      // wait for the thread to finish
  pthread_mutex_destroy(&lock);
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  int *ptr=(int *)malloc(sizeof(int));
  char *str=(char *)arg;
  int len=strlen(str),i=0;
  if(ptr==NULL)
  {
    printf("Malloc failed\n");
    pthread_exit(0);
  }
  *ptr=1;
  pthread_mutex_lock(&lock);
  for(i=0; i<len;i++)
  {
    if(str[i] !=str[--len])
    {
      *ptr=0;
      break;
    }
  }
  if((*ptr)==0)
  {
    printf("Given string is not palindrome\n");
  }
  else
  {
    printf("Given string is palindrome\n");
  }
  free(ptr);
  pthread_mutex_unlock(&lock);
}
```
### 21.Selection sort on an array of integers?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 *21.Implement a C program to create a thread that performs selection sort on an array of integers?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;                                    // Thread
  int status=0;
  status=pthread_create(&tid,NULL,create_thread,NULL);     // Create the thread
  if(status != 0)
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0;
}
void *create_thread(void *arg)
{
  int i,j,temp,index,n,a[100];
  printf("Enter number of elements :\n");
  scanf("%d",&n);
  printf("Enter elements :\n");
  for(i=0;i<n; i++)
  {
    scanf("%d",&a[i]);
  }
  for(i=1;i<n-1;i++)
  {
    index=0;
    for(j=1;j<=n-i;j++)
    {
      if(a[index]<a[j])
      {
        index=j;
      }
    }
    temp=a[j-1];
    a[j-1]=a[index];
    a[index]=temp;
  }
  for(i=0;i<n; i++)
  {
    printf("%d\n",a[i]);
  }
  pthread_exit(0);
}
```
### 22.Calculates the area of a triangle?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 22.Develop a C program to create a thread that calculates the area of a triangle? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

struct two_args
{
  float b;
  float h;
};

void *create_thread(void *arg);

int main(void)
{
  struct two_args nums;
  pthread_t tid;                                    // Thread
  printf("Enter base and height:");
  scanf("%f%f",&nums.b,&nums.h);
  pthread_create(&tid,NULL,create_thread,(void *)&nums);     // Create the thread
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  struct two_args *nums=(struct two_args *)arg;
  printf("area of triangle=%.2f\n",0.5*(nums->b)*(nums->h));
}
```
### 23.Calculates the sum of squares of numbers from 1 o 100? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 23.Write a C program to create a thread that calculates the sum of                *
 * squares of numbers from 1 o 100?                                                  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;                                    // Thread
  pthread_create(&tid,NULL,create_thread,NULL);     // Create the thread
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int i=3,num=100,sum=0,j=0;
  while(i<=num)
  {
    for(j=2;j<9;j++)
    {
      if(j*j==i)
      {
        sum +=i;
        printf("%d ",i);
      }
    }
    i++;
  }
  printf("sum of square=%d\n",sum);
}
```
### 24. Generates a random array of integers?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 24.Write a C program to create a thread that generates a random array of integers?*
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>
#include<stdlib.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;                                    // Thread
  int status=0;
  status=pthread_create(&tid,NULL,create_thread,NULL);     // Create the thread
  if(status != 0)
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  int a[10],i=0;
  while(i<10)
  {
    a[i]=rand() %100 ;
    i++;
  }
  for(i=0; i<10; i++)
  {
    printf("%d\n",a[i]);
  }
}
```
### 25.Babble Sort on array of integer
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 *25.Implement a C program to create a thread that performs bubble sort on an array of integers? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;                                    // Thread
  int status=0;
  status=pthread_create(&tid,NULL,create_thread,NULL);     // Create the thread
  if(status != 0)
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  int a[100],n,i=0,temp,j=0;
  printf("Enter number of elements :\n");
  scanf("%d",&n);
  while(i<n)
  {
    scanf("%d",&a[i]);
    i++;
  }
  for(i=0; i<n; i++)
  {
    for(j=1;j<n-i; j++)
    {
      if(a[j]<a[j-1])
      {
        temp=a[j];
        a[j]=a[j-1];
        a[j-1]=temp;
      }
    }
  }
  for(i=0;i<n; i++)
  {
    printf("%d\n",a[i]);
  }
  pthread_exit(0);
}
```
### 26.Greatest common divisor (GCD) of two numbers?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 26.Develop a C program to create a thread that calculates the greatest common divisor (GCD) of two numbers? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;                                    // Thread
  int status=0;
  status=pthread_create(&tid,NULL,create_thread,NULL);     // Create the thread
  if(status != 0)
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int a,b,temp;
  printf("Enter two numbers:");
  scanf("%d%d",&a,&b);
  while(b !=0)
  {
    temp=b;
    b= a % b;
    a=temp;
  }
  printf("%d\n",a);
  pthread_exit(0);
}
```
### 27.Sum of Fibonacci numbers up to a given limit?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 27.Write a C program to create a thread that calculates the sum of Fibonacci numbers up to a given limit? *               
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

#define MAX 100


void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  int num,status;
  printf("Enter the Fibonacci limit(n): ");
  scanf("%d",&num);
  if(num <0)
  {
     printf("Please enter positive numbers\n" );
     return 1;
  }
  status= pthread_create(&tid, NULL,create_thread, (void *)&num);
  if(status !=0)
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid, NULL);
  return 0;
}


// Thread function
void *create_thread(void *arg)
{
  int num=*(int *)arg;
  int c,a=0,b=1,sum=0;
  if(num >=1)
  {
    sum =1;
  }
  while((c=a+b) <= num)
  {
    sum += c;
    a=b;
    b=c;
  }
  printf("%d\n",sum);
  pthread_exit(NULL);
}
 
```
### 28.Sum of even numbers from 1 to 100?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 28.Implement a C program to create a thread that calculates the sum of even numbers from 1 to 100?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  int status;
  pthread_t tid;                                    // Thread
  status=pthread_create(&tid,NULL,create_thread,NULL);     // Create the thread
  if(status !=0)
  {
    printf("Thread creation is failed\n");
    return 2;
  }
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 1;
}

void *create_thread(void *arg)                                // thread function
{
  int i=2,num=100,sum=0;
  while(i<=num)
  {
    if(i%2==0)
    {
      sum +=i;
    }
    i++;
  }
  printf("sum of square=%d\n",sum);
  pthread_exit(0);
}
```
###  29.Factorial of a given number using iteration? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 29.Develop a C program to create a thread that calculates the factorial of a given number using iteration?  *             
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;                   // Thread
  int number=0;
  number=pthread_create(&tid,NULL,create_thread,NULL);     // Create the thread
  if(number !=0)
  {
    printf("thread creation is failed\n");
    pthread_exit(0);
  }
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  int factorial=1,number=0,i;
  printf("Enter Number:");
  scanf("%d",&number);
  if(number<0)
  {
    printf("only 0< values\n");
    pthread_exit(0);
  }
  for(i=1;i<=number; i++)
  {
    factorial *= i;
  }
  printf("factorial=%d\n",factorial);
}
```
### 30.Checks if a given year is a leap year?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 30.Write a C program to create a thread that checks if a given year is a leap year?       *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>


void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  int year;
  printf("Enter the year: ");
  scanf("%d", &year);
  if(year <= 0)
  {
     printf("Please enter Positive values\n");
     return 1;
  }
  if(pthread_create(&tid, NULL,create_thread, (void *)&year) != 0)
  {
    printf("Thread creation is failed\n");
    return 1;
  }
  pthread_join(tid, NULL);
  return 0;
}
// Thread function
void *create_thread(void *arg)
{
  int year=*(int *)arg;
  if(((year%4==0) && (year%100 !=0)) || (year % 400 ==0))
  {
    printf("Given year is leap year\n");
  }
  else
  {
    printf("Given year is not a leap year\n");
  }
  pthread_exit(NULL);
}
```
### 31.Performs multiplication of two matrices? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 31.Implement a C program to create a thread that performs multiplication of two matrices? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>


void *create_matrices_thread(void *arg);

int main(void)
{
  pthread_t tid;
  if(pthread_create(&tid, NULL,create_matrices_thread,NULL) != 0)
  {
    printf("Thread creation is failed\n");
    return 1;
  }
  pthread_join(tid, NULL);
  return 0;
}

// Thread function
void *create_matrices_thread(void *arg)
{
  int arr1[10][10],arr2[10][10],i,j,n,m,mul[10][10];
  printf("Enter number of rows and columns(<10):");
  scanf("%d%d",&m,&n);
  printf("Enter elements for 1st matrices\n");
  for(i=0;i<m;i++)
  {
    for(j=0;j<n; j++)
    {
      scanf("%d",&arr1[i][j]);
    }
  }
  printf("Enter elements for 2nd matrices\n");
  for(i=0;i<m;i++)
  {
    for(j=0;j<n; j++)
    {
      scanf("%d",&arr2[i][j]);
    }
  }
  for(i=0;i<m;i++)
  {
    for(j=0;j<n; j++)
    {
      mul[i][j]= (arr1[i][j]) * (arr2[i][j]);
    }
  }
  for(i=0;i<m;i++)
  {
    for(j=0;j<n; j++)
    {
      printf("%d ",arr1[i][j]);
    }
    printf("\t");
    for(j=0;j<n; j++)
    {
      printf("%d ",arr2[i][j]);
    }
    printf("\t");
    for(j=0;j<n; j++)
    {
      printf("%d ",mul[i][j]);
    }
    printf("\t");
    printf("\n");
  }
  pthread_exit(NULL);
}
```
### 32.Calculates the average of numbers from 1 to 100?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 *32.Develop a C program to create a thread that calculates the average of numbers from 1 to 100?*
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_avg_of_numbers_thread(void *arg);

int main(void)
{
  pthread_t tid;                                                         // Thread
  if(pthread_create(&tid,NULL,create_avg_of_numbers_thread,NULL) !=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                                            // wait for the thread to finish
  return 0;
}

void *create_avg_of_numbers_thread(void *arg)                                // thread function
{
  int i=0,num=100;
  float avg,sum=0;
  while(i<=num)
  {
    sum +=i;
    i++;
  }
  avg=(sum/num);
  printf("%.2f avg of total sum=%.1f\n",avg,sum);
}
```
### 33.Generates a random string?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 33.Implement a C program to create a thread that generates a random string?   *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<pthread.h>
#include<time.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  char str[100];
  char *ret;
  printf("Enter characters:");
  scanf("%s",str);
  if(pthread_create(&tid,NULL,create_thread,(void *)str)!=0)   // Create the thread
  {
    perror("thread creation is failed\n");
    return 0;
  }
  if(pthread_join(tid,(void **)&ret) != 0 )    // wait for the thread to finish
  {
    printf("Join is failed\n");
    return 2;
  }
  printf("the random string is %s\n",ret);
  free(ret);
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  char *ptr=malloc(sizeof(char)*11);
  char *str;
  int size,i=0,len=10;
  if(ptr==NULL)
  {
    printf("Malloc is failed\n");
    pthread_exit(NULL);
  }
  str=(char *)arg;
  size=strlen(str);
  srand(time(NULL));                          // Seed the random number generator
  for(i=0; i< len; i++)
  {
    *(ptr+i)=str[rand() % size];
  }
  *(ptr+i)='\0';
  pthread_exit(ptr);
}         
```
### 34.Checks if a given number is a perfect square?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 34.Write a C program to create a thread that checks if a given number is a perfect square?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  int num,ret;
  printf("Enter Numbers :");
  scanf("%d",&num);
  if(pthread_create(&tid,NULL,create_thread,(void *)&num)!=0)   // Create the thread
  {
    perror("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,&ret);    // wait for the thread to finish
  if(ret != 0)
    printf ("Given number is not perfect\n");
  else
    printf("Given number is perfect\n");
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int *
  int num=*(int *)arg;
  if(num<=0)
  {
    printf("Enter valid number\n");
    pthread_exit(7);
  }
  pthread_exit(num & (num-1));
}
```
### 35.Calculates the sum of digits of a given number
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 35.Write a C program to create a thread that calculates the sum of digits of a given number *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  int *ret=0;
  pthread_t tid;
  int num;
  printf("Enter Numbers :");
  scanf("%d",&num);
  pthread_create(&tid,NULL,create_thread,(void *)&num);     // Create the thread
  pthread_join(tid,(void *)&ret);                // wait for the thread to finish
  printf("%d\n",*ret);
  free(ret);
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int *sum=(int *)malloc(sizeof(int));
  int num=*(int *)arg,rem=0;
  *sum=0;
  while(num)
  {
    rem=num%10;
    (*sum)=(*sum)+rem;
    num /=10;
  }
  pthread_exit(sum);
}
```
### 36.Factorial of a given number using recursion 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 36.Implement a C program to create a thread that calculates the factorial of a given number *
 * using recursion                                                                             *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

void *create_thread(void *arg);

long long fact(int n)
{
    if (n == 1 || n == 0 )
    {
      return 1;
    }
    return n * fact(n - 1);
}

int main(void)
{
  pthread_t tid;
  int num;
  long long *result;
  printf("Enter a positive number: ");
  scanf("%d", &num);
  if(num < 0)
  {
    printf("Factorial not defined for negative numbers.\n");
    return 1;
  }
  if(pthread_create(&tid, NULL, create_thread, (void *)&num) != 0)
  {
    perror("Thread creation failed");
    return 2;
  }
  if(pthread_join(tid, (void **)&result) != 0)
  {
    perror("Thread join failed");
    return 3;
  }
  printf("Factorial of %d is %lld\n", num, *result);
  free(result);
  return 0;
}

void *create_thread(void *arg)
{
  int num = *(int *)arg;
  long long *res = malloc(sizeof(long long));
  if (res == NULL)
  {
    perror("Memory allocation failed");
    pthread_exit(NULL);
  }
  *res = fact(num);
   pthread_exit(res);
}          
```
### 37.Finds the maximum element in an array?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 37.Develop a C program to create a thread that finds the maximum element in an array?       *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

struct node
{
  int num;
  int arr[100];
};
void *create_thread(void *arg);

int main(void)
{
  int i=0;
  int *ret=0;
  pthread_t tid;
  struct node data;
  printf("Enter Numbers :");
  scanf("%d",&data.num);
  printf("Enter elements:");
  for(i=0;i<data.num;i++)
  {
    scanf("%d",&data.arr[i]);
  }
  if(pthread_create(&tid,NULL,create_thread,(void *)&data) !=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,(void *)&ret);                // wait for the thread to finish
  printf("maximum value =%d\n",*ret);
  free(ret);
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int i=0;
  int *temp=(int *)malloc(sizeof(int));
  if(temp==NULL)
  {
    printf("malloc is failed\n");
    pthread_exit(0);
  }
  struct node *data=(struct node *)arg;
  *temp=data->arr[0];
  for(i=0;i<data->num;i++)
  {
    if(*temp < data->arr[i])
    {
      *temp=data->arr[i];
    }
  }
  pthread_exit(temp);
}
```
### 40.Calculates the average of numbers in an array?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 40.Develop a C program to create a thread that calculates the average of numbers in an array? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

struct node
{
  int num;
  int arr[100];
};
void *create_thread(void *arg);

int main(void)
{
  int i=0;
  float *ret=0;
  pthread_t tid;
  struct node data;
  printf("Enter Numbers :");
  scanf("%d",&data.num);
  printf("Enter elements:");
  for(i=0;i<data.num;i++)
  {
    scanf("%d",&data.arr[i]);
  }
  if(pthread_create(&tid,NULL,create_thread,(void *)&data) !=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,(void **)&ret);                // wait for the thread to finish
  printf("avg of element in array =%.2f\n",*ret);
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int i=0;
  float sum=0;
  float *temp=(float *)malloc(sizeof(float));
  struct node *data=(struct node *)arg;
  for(i=0;i<data->num;i++)
  {
    sum=sum+(data->arr[i]);
  }
  *temp=(sum/data->num);
  pthread_exit(temp);
}
```
### 42.Checks if a number is even or odd?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 42.Implement a C program to create a thread that checks if a number is even or odd?         *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  int *ret=0;
  pthread_t tid;
  int num;
  printf("Enter Numbers :");
  scanf("%d",&num);
  if(pthread_create(&tid,NULL,create_thread,(void *)&num) !=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,(void *)&ret);                // wait for the thread to finish
  if(*ret==1)
   printf("Given number is Odd\n");
  else
   printf("Given number is Even\n");
  free(ret);
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  int *flag=(int *)malloc(sizeof(int));
  int num=*(int *)arg,rem=0;
  if(num%2==0)
  {
    *flag=0;
  }
  else
  {
    *flag=1;
  }
  pthread_exit(flag);
}

```
### 43.Calculates the sum of elements in an array? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 43.Develop a C program to create a thread that calculates the sum of elements in an array?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

struct node
{
  int num;
  int arr[100];
};
void *create_thread(void *arg);

int main(void)
{
  int i=0;
  int *ret=0;
  pthread_t tid;
  struct node data;
  printf("Enter Numbers :");
  scanf("%d",&data.num);
  printf("Enter elements:");
  for(i=0;i<data.num;i++)
  {
    scanf("%d",&data.arr[i]);
  }
  if(pthread_create(&tid,NULL,create_thread,(void *)&data) !=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,(void *)&ret);                // wait for the thread to finish
  printf("sum =%d\n",*ret);
  free(ret);
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int i=0;
  int *sum=(int *)malloc(sizeof(int));
  struct node *data=(struct node *)arg;
  for(i=0; i < data->num; i++)
  {
    *sum += data->arr[i];
  }
  pthread_exit(sum);
}
```
### 44.Calculates the factorial of numbers from 1 to 10?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 44.Write a C program to create a thread that calculates the factorial of numbers from 1 to 10?*
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  int *ret=0;
  pthread_t tid;
  int num;
  if(pthread_create(&tid,NULL,create_thread,NULL) !=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,(void *)&ret);                // wait for the thread to finish
  printf("factorial of 1 to 10=%d\n",*ret);
  free(ret);
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  int i;
  int *fact=(int *)malloc(sizeof(int));
  *fact=1;
  if(fact==NULL)
  {
    printf("malloc is failed\n");
    pthread_exit(0);
  }
  for(i=1;i<=10;i++)
  {
    (*fact) = (*fact) *i;
  }
  pthread_exit(fact);
}
```
### 48.Searches for a given number in an array?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 48.Write a C program to create a thread that searches for a given number in an array?       *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

struct node
{
  int num;
  int arr[10];
  int key;
};
void *create_thread(void *arg);

int main(void)
{
  int i=0;
  int *ret=0;
  pthread_t tid;
  struct node data;
  printf("Enter Numbers :");
  scanf("%d",&data.num);
  printf("Enter elements:");
  for(i=0;i<data.num;i++)
  {
    scanf("%d",&data.arr[i]);
  }
  printf("Enter key Numbers :");
  scanf("%d",&data.key);
  if(pthread_create(&tid,NULL,create_thread,(void *)&data) !=0)   // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,(void *)&ret);     // wait for the thread to finish
  if(*ret==0)
  {
    printf("given number is not present in array\n");
  }
  else
  {
    printf("given number is present in array\n");
  }
  free(ret);
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int i=0;
  struct node *data=(struct node *)arg;
  int *temp=(int *)malloc(sizeof(int));
  if(temp==NULL)
  {
    printf("malloc is failed\n");
    pthread_exit(0);
  }
  for(i=0;i<data->num;i++)
  {
    if(data->key == data->arr[i])
    {
      *temp=1;
      break;
    }
    else
    {
      *temp=0;
    }
  }
  pthread_exit(temp);
}
```
### 49.Reverses a given string? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 49.Develop a C program to create a thread that reverses a given string?     *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
#include<string.h>

void *create_thread(void *arg);

int main(void)
{
  char str[100];
  char *ret;
  pthread_t tid;
  printf("Enter string(99<):");
  scanf("%s",str);
  if(pthread_create(&tid,NULL,create_thread,(void *)str) !=0)     // Create the thread
  {
    printf("thread_creation is failed\n");
    return 0;
  }
  pthread_join(tid,(void **)&ret);     // wait for the thread to finish
  printf("%s\n",ret);
  free(ret);
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  char *s=(char *)malloc(sizeof(char)*100);
  char *str=(char *)arg;
  int len=strlen(str),i=0;
  if(s==NULL)
  {
    printf("Malloc failed\n");
    pthread_exit(0);
  }
  for(i=0; i<len;i++)
  {
    s[i]=str[len-1-i];
  }
  s[i]='\0';
  pthread_exit((void *)s);
}
```
### 51.Performs addition of two matrices?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 51.Write a C program to create a thread that performs addition of two matrices?           *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

struct array
{
  int m;
  int n;
  int arr1[10][10];
  int arr2[10][10];
  int add[10][10];
};

void *create_matrices_thread(void *arg);

int main(void)
{
  int i,j;
  pthread_t tid;
  struct array data;
  printf("Enter number of rows and columns(<10):");
  scanf("%d %d",&data.m,&data.n);
  printf("Enter elements for 1st matrices\n");
  for(i=0;i<data.m;i++)
  {
    for(j=0;j<data.n; j++)
    {
      scanf("%d",&data.arr2[i][j]);
    }
  }
  if(pthread_create(&tid, NULL,create_matrices_thread,(void *)&data) != 0)
  {
    printf("Thread creation is failed\n");
    return 1;
  }
  pthread_join(tid,NULL);
  return 0;
}

// Thread function
void *create_matrices_thread(void *arg)
{
  struct array *data=(struct array *)arg;
  int i,j;
  for(i=0;i<data->m;i++)
  {
    for(j=0;j<data->n; j++)
    {
      {
      data->add[i][j]= (data->arr1[i][j]) + (data->arr2[i][j]);
    }
  }
  for(i=0;i<data->m;i++)
  {
    for(j=0;j<data->n; j++)
    {
      printf("%d ",data->arr1[i][j]);
    }
    printf("\t");
    for(j=0;j<data->n; j++)
    {
      printf("%d ",data->arr2[i][j]);
    }
    printf("\t");
    for(j=0;j<data->n; j++)
    {
      printf("%d ",data->add[i][j]);
    }
    printf("\t");
    printf("\n");
  }
  pthread_exit(NULL);
}
```
### 52.calculates the length of a given string?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 52.Develop a C program to create a thread that calculates the length of a given string? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
#include<string.h>

void *create_thread(void *arg);

int main(void)
{
  char str[100];
  int *len;
  pthread_t tid;
  printf("Enter string(99<):");
  scanf("%s",str);
  if(pthread_create(&tid,NULL,create_thread,(void *)str) !=0)     // Create the thread
  {
    printf("thread_creation is failed\n");
    return 0;
  }
  pthread_join(tid,(void **)&len);     // wait for the thread to finish
  printf("%d\n",*len);
  free(len);
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int *len=(int *)malloc(sizeof(int));
  char *str=(char *)arg;
  int i=0;
  if(len==NULL)
  {
    printf("Malloc failed\n");
    pthread_exit(0);
  }
  while(str[i])
  {
    i++;
  }
  *len=i;
  pthread_exit((void *)len);
}
```
### 53.Each thread should print "Hello, World!" along with its thread ID
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 53.Write a C program to create two threads using pthreads library. Each thread should print *
 * "Hello, World!" along with its thread ID?                                                   *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid1,tid2;                                             // Thread ID
  if(pthread_create(&tid1,NULL,create_thread,"thread_1_hello_world")!= 0)     // Create the thread
  {
    printf("thread 1 creation is failed\n");
    return 0;
  }
  if(pthread_create(&tid2,NULL,create_thread,"thread_2_hello_world")!= 0)     // Create the thread
  {
    printf("thread 2 creation is failed\n");
    return 0;
  }
  pthread_join(tid1,NULL);                          // wait for the thread to finish
  pthread_join(tid2,NULL);                          // wait for the thread to finish
  printf("main thread id=%u\n",(unsigned int)pthread_self()); // get pthread id
  printf("process id=%u\n",getpid());    // get process id
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  char *str=(void *)(arg);
  printf("%s and id=%u\n",str,(unsigned int)pthread_self()); // get pthread id
}
```
### 55.Create two threads that increment a shared variable using mutex locks
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 55.Write a C program to demonstrate thread synchronization using mutex locks. Create two        *
 * threads that increment a shared variable using mutex locks to ensure proper synchronization?    *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<pthread.h>

pthread_mutex_t lock;
int num=10;
void *create_thread(void *arg);

int main(void)
{
  pthread_t tid1,tid2;                                     // Thread
  if(pthread_mutex_init(&lock,NULL) !=0 )
  {
    printf("mutex is failed\n");
    return 17;
  }
  if(pthread_create(&tid1,NULL,create_thread,"increment_Thread1")!=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  if(pthread_create(&tid2,NULL,create_thread,"increment_Thread2")!=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid1,NULL);                          // wait for the thread to finish
  pthread_join(tid2,NULL);
  pthread_mutex_destroy(&lock);
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int i=0;
  char *str=(char *)arg;
  while(i<10)
  {
    pthread_mutex_lock(&lock);
    printf("%s:%d\n",str,num++);
    pthread_mutex_unlock(&lock);
    i++;
  }
}
```
### 56.Create two threads that increment a shared variable using semaphore.
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 56.Write a C program to demonstrate thread synchronization using semaphore. Create two          *
 * threads that increment a shared variable using mutex locks to ensure proper synchronization?    *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<semaphore.h>
#include<pthread.h>

sem_t sem;
int num=10;
void *create_thread(void *arg);

int main(void)
{
  pthread_t tid1,tid2;                                           // Thread
  if(sem_init(&sem,0,1) !=0 )
  {
    printf("semaphore is failed\n");
    return 17;
  }
  if(pthread_create(&tid1,NULL,create_thread,"increment_Thread1")!=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 10;
  }
  if(pthread_create(&tid2,NULL,create_thread,"increment_Thread2")!=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 7;
  }
  pthread_join(tid1,NULL);                          // wait for the thread to finish
  pthread_join(tid2,NULL);
  sem_destroy(&sem);
  return 6;
}

void *create_thread(void *arg)                                // thread function
{
  int i=0;
  char *str=(char *)arg;
  while(i<10)
  {
    sem_wait(&sem);
    printf("%s:%d\n",str,num++);
    sem_post(&sem);
    i++;
  }
}
```
### 59.Infinite loop and cancels it after a certain condition is met from the main thread?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 59.Write a C program to demonstrate thread cancellation.  Create a thread that runs             *
 * an infinite loop and cancels it after a certain condition is met from the main thread?          *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  // Create the thread
  if(pthread_create(&tid, NULL,create_thread, NULL) != 0)
  {
    perror("Thread creation failed");
    return 1;
  }
  sleep(5);
  printf("Main thread cancelling the worker thread...\n");
  if (pthread_cancel(tid) != 0)
  {
    perror("Failed to cancel thread");
    return 1;
  }
  // Wait for the thread to terminate
  if (pthread_join(tid, NULL) != 0)
  {
    perror("Failed to join thread");
    return 1;
  }
  printf("Thread cancelled successfully.\n");
  return 0;
}

void *create_thread(void *arg)
{
  while(printf("Thread running...\n"))
  {
    sleep(1);  // sleep
  }
  return NULL;
}
```
### 61.
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 61.Write a C program to create a thread that prints the even numbers between 1 and 20?      *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  if(pthread_create(&tid,NULL,create_thread,NULL) !=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                // wait for the thread to finish
  return 0;
}

void *create_thread(void *arg)                                // thread function
{
  int i=1,rem=0;
  for(i=1;i<=20;i++)
  {
    if(i%2==0)
    {
      printf("%d ",i);
    }
  }
  printf("\n");
  pthread_exit(0);
}
```
###
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 63.Implement a C program to create a thread that calculates the sum of squares of           *
 * numbers from 1 to 10                                                                        *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

void *create_thread(void *arg);

int main(void)
{
  pthread_t tid;
  if(pthread_create(&tid,NULL,create_thread,NULL) !=0)     // Create the thread
  {
    printf("thread creation is failed\n");
    return 0;
  }
  pthread_join(tid,NULL);                // wait for the thread to finish
  return 0;
}
void *create_thread(void *arg)                                // thread function
{
  int i=1,sum=0;
  while((i*i)<=10)
  {
    sum += (i*i);
    i++;
  }
  printf("%d\n",sum);
  pthread_exit(0);
}

```
