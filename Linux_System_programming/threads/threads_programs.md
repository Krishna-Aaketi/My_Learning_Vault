## -------------------------------------------------------------------Create Thread Programms-------------------------------------------------------------------------------
 
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
  pthread_t t_id;                                             // Thread ID
  pthread_create(&t_id,NULL,create_thread,"Hello World");     // Create the thread
  pthread_join(t_id,NULL);                                    // wait for the thread to finish
  printf("main thread id=%u\n",(unsigned int)pthread_self()); // get pthread id
  printf("process id=%u\n",getpid());                         // get process id
}

void *create_thread(void *arg)                                // thread function
{
  char *ptr=(char *)(arg);
  printf("%s\n",ptr);
  printf("process id=%u\n",getpid());                        //get process id
  return 0;
}
```
### 2.Multiple threads,each printing its own message? 
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
  pthread_create(&tid1,NULL,create_thread1,NULL);   // Create the thread
  pthread_create(&tid2,NULL,create_thread2,NULL);     
  pthread_create(&tid3,NULL,create_thread3,NULL);     
  pthread_create(&tid4,NULL,create_thread4,NULL);     
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
### 3.Print numbers from 1 to 10 concurrently?
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
  pthread_create(&tid1,NULL,create_thread,"thread_1");     // Create the thread
  pthread_create(&tid2,NULL,create_thread,"thread_2");     // Create the thread
  pthread_join(tid1,NULL);                          // wait for the thread to finish
  pthread_join(tid2,NULL);                          // wait for the thread to finish
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
### 4.Calculates the factorial of a given number? 
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
  pthread_create(&tid,NULL,create_thread,NULL);     // Create the thread
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
### 5.Print their thread IDs?
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
  pthread_create(&tid1,NULL,create_thread,"Thread_1");     // Create the thread
  pthread_create(&tid2,NULL,create_thread,"Thread_2");     // Create the thread
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
### 6.Prints the sum of two numbers?
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
  pthread_create(&tid,NULL,create_thread,(void *)&nums);     // Create the thread
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  struct two_args *nums=(struct two_args *)arg;	
  printf("sum=%d\n",(nums->a)+(nums->b));
} 
```
### 7.Calculates the square of a number?  
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
  pthread_create(&tid,NULL,create_thread,(void *)&num);     // Create the thread
  pthread_join(tid,NULL);                          // wait for the thread to finish
  return 0; 
}

void *create_thread(void *arg)                                // thread function 
{
  int num=*(int *)arg;	
  printf("square=%d\n",num*num);
} 
```
### 8.Prints the current date and time?
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
### 9.Checks if a number is prime?
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
### 10.Checks if a given string is a palindrome? 
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
  pthread_create(&tid,NULL,create_thread,(void *)str);     // Create the thread
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

void *create_thread(void *arg);
int main(void)
{
  pthread_t t_id;                                             // Thread ID
  pthread_create(&t_id,NULL,create_thread,"Hello World");     // Create the thread
  pthread_join(t_id,NULL);                                    // wait for the thread to finish
  printf("main thread id=%u\n",(unsigned int)pthread_self()); // get pthread id 
  printf("process id=%u\n",getpid());                         // get process id 
}

void *create_thread(void *arg)                                // thread function 
{
  char *ptr=(char *)(arg);                          
  printf("%s\n",ptr);
  printf("process id=%u\n",getpid());                        //get process id
  return 0;
}

```
### 12.Print their thread IDs and synchronize their output
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
### 13.Random numbers and synchronizes access to a shared buffer?
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
### 14.Performs addition of two numbers with mutex locks?
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
### 15.Increment and decrement a shared variable,respectively, using mutex locks?
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
### 16.reads input from the user and synchronizes access to shared resources
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
  pthread_mutex_unlock(&lock);
  printf("the string is %s\n",str);
  return 0;
}
```
### 17.Prints prime numbers up to a given limit with mutex locks?
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
### 18.calculates the sum of Fibonacci numbers up to a given limit mutex locks 
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
