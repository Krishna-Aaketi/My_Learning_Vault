## ------------------------------Bitwise Programs-----------------------------
### 1.Assign value between m to n bits
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * write a c program to assign value between m to n bits     *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

int main(void)
{
  int num=0xFFFFFFFF,m,n,mask,value;
  printf("Enter Value:");
  scanf("%d",&value);
  printf("Enter m,n bits:");
  scanf("%d%d",&m,&n);
  mask = (((unsigned)1 << (n - m + 1)) - 1) << m;
  num &= ~(mask);
  num |=(value<<m);
  printf("set=%X\n", num);
  return 0;
}
```
### 2.Bit is set or not in a number?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * How to check if a particular bit is set or not in a number? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

int main(void)
{
  int num,bit;
  printf("Enter Number:");
  scanf("%d",&num);
  printf("Enter bit:");
  scanf("%d",&bit);
  (num & (1 << bit)) ? printf("Bit is Set\n") : printf("Bit is Reset\n");
  return 0;
}
```
### 3.Bit is set or not in a number in macro
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * How to check if a particular bit is set or not in a number in macro *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#define BIT_IS_SET_OR_NOT(num,bit) (num & (1 << bit))

int main(void)
{
  int num,bit;
  printf("Enter Number:");
  scanf("%d",&num);
  printf("Enter bit:");
  scanf("%d",&bit);
  if(BIT_IS_SET_OR_NOT(num,bit))
    printf("Bit is Set\n");
  else
    printf("Bit is Reset\n");
  return 0;
}
```
### 4.Convert decimal to binary in given number
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * write a c program to convert decimal to binary in given number  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

int main(void)
{
  int num,i=0,total_bits=0;
  printf("Enter Number:");
  scanf("%d",&num);
  total_bits=(sizeof(num)*8-1);
  for(i=total_bits; i>=0; i--)
  {
    printf("%u ",((num>>i)&1));
  }
  printf("\n");
  return 0;
}
```
### 5.Count leading zeros and tailing zeros in the given number
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * write a c program count leading zeros and tailing zeros in the given number       *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

int main(void)
{
  int num,t_count=0,l_count,i;
  printf("Enter Number:");
  scanf("%d",&num);
  for(i=0; i<(sizeof(int)*8);i++)
  {
    if((num & 1)==0)
    {
      t_count++;
    }
    else
    {
      for(  ;i<(sizeof(int)*8); i++)
      {
        if((num & 1)==0)
        {
          l_count++;
        }
        else
        {
          l_count=0;
        }
        num >>=1;
      }
    }
    num >>=1;
  }
  printf("Leading zero's=%d Tails zero's=%d\n",l_count,t_count);
  return 0;
}
```
### 6.Count number of set and reset bits in give number
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * write a c program count number of set and reset bits in give number       *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */
#include <stdio.h>

int main(void)
{
  int num,i=0,ones=0,zeros=0;
  printf("Enter Number:");
  scanf("%d",&num);
  for(i=0; i< (8*sizeof(int)); i++)
  {
    if(num & 1)
    {
      ones++;
    }
    else
    {
      zeros++;
    }
    num >>=1;
  }
  printf("one's=%d zero's=%d\n",ones,zeros);
  return 0;
}
```
### 7.Count number of bits in give number
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * write a c program count number of bits in give number       *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */
#if 1
#include <stdio.h>

int main(void)
{
    int num,count=0;
    printf("Enter Number:");
    scanf("%d",&num);
    while(num)
    {
      if(num & 1)
      {
        count++;
      }
      num >>=1;
    }
    printf("%d\n",count);
    return 0;
}
#endif

#if 0
#include <stdio.h>

int main(void)
{
    int num,count=0,i;
    printf("Enter Number:");
    scanf("%d",&num);
    for(i=0; i<32; i++)
    {
      if((1<<i)& num)
      {
        count++;
      }
    }
    printf("%d\n",count);
    return 0;
}
#endif
```
### 8.
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * Write a c program to interchange the first 4bits with next 4bits bytes in 32 bit Integer Variable *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */
```
### 9.Given number is even or odd
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
 * write a c program to given number is even or odd      *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

int main(void)
{
    int num,bit;
    printf("Enter Number:");
    scanf("%d",&num);
    if(num & 1)
    {
      printf("Number is odd\n");
    }
    else
    {
      printf("Number is even\n");
    }
    return 0;
}
```
### 10.Given number is power of 2 or not 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * write a c program to check power of 2 or not in given number  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

int main(void)
{
    int num,bit=0;
    printf("Enter Number:");
    scanf("%d",&num);
    bit= ((num !=0) && (num & (num-1)));
    if(bit == 1)
    {
      printf("Given number is not power of 2\n");
    }
    else
    {
      printf("Given number is power of 2\n");
    }
    return 0;
}
```
