### 1.Dynamic memory allocation using malloc().
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 86. Write a C program to demonstrate dynamic memory allocation using malloc().*
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
int main(void)
{
  char *ptr;
  ptr=(char *)malloc(sizeof(char)*30);
  if(ptr==NULL)
  {
    printf("Malloc is failed\n");
    return 0;
  } 
  printf("Enter string (<30 characters):\n");
  scanf("%[^\n]",ptr);
  printf("%s\n",ptr);
  free(ptr);
  return 0;
}
```
### 2.Dynamic memory allocation using calloc()
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 87. Write a C program to dynamic memory allocation using calloc().*
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<stdlib.h>
int main(void)
{
  int *ptr;
  int i=0,n;
  printf("Enter Array size:");
  scanf("%d",&n);
  ptr=(int *)calloc(n,sizeof(int));
  if(ptr==NULL)
  {
    printf("Calloc is failed\n");
    return 0;
  }
  printf("Enter Array elements:\n");
  for(i=0;i<n;i++)
  {
    scanf("%d",&ptr[i]);
  }
  for(i=0; i<n; i++)
  {
    printf("%d ",ptr[i]);
  }
  printf("\n");
  free(ptr);
  return 0;
}
```
### 3.Dynamically allocated memory using realloc()
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 88.Write a C program to resize dynamically allocated memory using realloc() *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>

int main(void)
{
  int *arr;
  int n, i;
  printf("Enter number of elements: ");
  scanf("%d", &n);
  arr = (int *)malloc(n * sizeof(int));
  if (arr == NULL)
  {
    printf("Memory allocation failed!\n");
    return 1;
  }
  printf("Enter %d integers:\n", n);
  for (i = 0; i < n; i++)
  {
    scanf("%d", &arr[i]);
  }
  printf("Enter new size: ");
  scanf("%d", &n);  // reuse 'n' for new size
  arr = (int *)realloc(arr, n * sizeof(int));
  if (arr == NULL)
  {
    printf("Memory reallocation failed!\n");
    return 1;
  }
  printf("Enter new values for remaining elements (if any):\n");
  for (i = 0; i < n; i++)
  {
    printf("arr[%d]: ", i);
    scanf("%d", &arr[i]);
  }
  printf("All values after resizing:\n");
  for (i = 0; i < n; i++)
  {
    printf("%d ", arr[i]);
  }
  printf("\n");
  free(arr);
  return 0;
}
```
### 4.Memory for a linked list node dynamically
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
 * 89. Develop a program in C to allocate memory for a linked list node dynamically  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>

// Define the structure of a node
struct Node
{
  int data;
  struct Node* pnext;
};

struct node *phead;
int main(void)
{
  // Allocate memory for one node dynamically
  struct Node *pnew = (struct Node*)malloc(sizeof(struct Node));
  // Check if memory allocation was successful
  if (pnew == NULL)
  {
    printf("Memory allocation failed.\n");
    return 1;
  }
  // Assign data to the node
  pnew->data = 10;
  pnew->pnext = NULL;
  // Print the data stored
  printf("Data in the node: %d\n",pnew->data);

  // Free the allocated memory
  free(pnew);
  return 0;
}
```
### 5.Memory allocation using the first-fit algorithm
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 90. Implement a C program to simulate memory allocation using the first-fit algorithm *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

#define MAX_B 10
#define MAX_P 10

int main(void)
{
  int block_size[MAX_B],process_size[MAX_P],allocation[MAX_P];
  int block_count, process_count,i=0,j;
  printf("Enter number of memory blocks: ");
  scanf("%d", &block_count);
  printf("Enter size of each block:\n");
  for(i = 0; i < block_count; i++)
  {
    printf("Block %d: ", i + 1);
    scanf("%d", &block_size[i]);
  }
  printf("Enter number of processes: ");
  scanf("%d", &process_count);
  printf("Enter size of each process:\n");
  for(i = 0; i < process_count; i++)
  {
    printf("Process %d: ", i + 1);
    scanf("%d", &process_size[i]);
    allocation[i] = -1;
  }
  // First Fit Allocation
  for (i = 0; i < process_count; i++)
  {
    for (j = 0; j < block_count; j++)
    {
      if (block_size[j] >= process_size[i])
      {
        allocation[i] = j;
        block_size[j] -= process_size[i]; // reduce available size
        break;
      }
    }
  }
  // Output allocation results
  printf("\nProcess No.\tProcess Size\tBlock No.\n");
  for(i = 0;i < process_count;i++)
  {
    printf("%d\t\t%d\t\t", i + 1, process_size[i]);
    if (allocation[i] != -1)
    {
      printf("%d\n", allocation[i] + 1);
    }
    else
    {
      printf("Not Allocated\n");
    }

  }
  return 0;
}
```
###
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 91. Write a C program to simulate memory allocation using the best-fit algorithm      *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

```
### 7.Memory allocator using the buddy system.
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 94. Write a C program to implement a simple memory allocator using the buddy system.  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <math.h>

#define MAX_MEMORY 1024  // Total available memory

void buddy_system(int size);

int main(void)
{
  int request;
  printf("Enter the memory size to allocate (in bytes): ");
  if(scanf("%d", &request) != 1)
  {
    printf("Please enter an integer value.\n");
    return 1;
  }
  buddy_system(request);
  return 0;
}

void buddy_system(int size)
{
  if(size <= 0)
  {
    printf("size must be greater than 0\n");
    return;
  }
  if (size > MAX_MEMORY)
  {
    printf("Requested size exceeds total available memory (%d bytes).\n", MAX_MEMORY);
    return;
  }
  int power = 1;
  while (power < size)
     power *= 2;
  printf("Requested size: %d bytes\n", size);
  printf("Allocated size using Buddy System: %d bytes\n", power);
}
```
