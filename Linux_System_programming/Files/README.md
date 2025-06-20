## 1. Create a Text File and Write User Input
```c
// C program to create a new text file and write user input to it
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>

int main(void)
{
  int fd, ref, len;
  char buf[100];

  printf("Enter a string:\n");
  scanf("%[^\n]", buf); // captures input until newline (avoid buffer overflow)

  len = strlen(buf);
  printf("Length: %d\n", len);

  // O_CREAT: create if it doesn't exist
  // O_RDWR: read and write access
  // O_TRUNC: truncate file to 0 length if it exists
  fd = open("file.txt", O_CREAT | O_RDWR | O_TRUNC, 0666);
  printf("File descriptor: %d\n", fd);

  if(fd < 0)
  {
    printf("open system call failed\n");
    return 0;
  }

  // write returns number of bytes written
  ref = write(fd, buf, strlen(buf));
  printf("Bytes written: %d\n", ref);

  if(ref < 0)
  {
    printf("Write system call failed\n");
    return 0;
  }

  close(fd); // always close file descriptors
  return 0;
}


/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 2.Develop a C program to open an existing text file and display its contents  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>

int main(void)
{
  int fd,ref,len;
  char buf[100];
  fd=open("file.txt",O_RDWR,0666); 
  if(fd<0)                                   
  {
    printf("open system call failed\n");
    return 0;
  }
  while((ref=read(fd, buf, sizeof(buf)-1)) > 0)
  {
    buf[ref]='\0';	  
    printf("%s",buf);
  }
  if(ref<0)
  {
    printf("read system call is failed\n");
    close(fd);
  }
  close(fd);                     
  return 0;
}

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 3.Implement a C program to create a new directory named "Test" in the * 
 *  current directory?                                                   *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#if 0                     // conditional compilation if it is 0 not execute
#include <stdlib.h>
#include <stdio.h>

int main(void) 
{
    int status;
    status = system("mkdir Test");
    if (status == 0)
    {
      printf("Directory created using system()!\n");
    }
    else
    {
      printf("Failed to create directory.\n");
    }
    return 0;
}
#endif
# if 1                      //if value is non zero value its execute
#include <stdio.h>
#include <unistd.h>
#include <sys/syscall.h>
#include <sys/stat.h>                     

int main(void) 
{
    int result;
    // SYS_mkdir is the syscall number for mkdir
    result = syscall(SYS_mkdir, "Test", 0777);
    if (result == 0)
    {
        printf("Directory 'Test' created successfully.\n");
    }
    else
    {
        perror("syscall mkdir failed"); //error message
    }
    return 0;
}
#endif

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 4.Write a C program to check if a file named "sample.txt" exists in the current directory?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <unistd.h>
#include <sys/syscall.h>
#include <sys/stat.h>

int main(void) 
{
  if(access("Test", F_OK)==0)
  {
    printf("File is are there\n");
  }
  else
  {
      perror("No such file or directory\n");
  }
  return 0;
}

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 5. Develop a C program to rename a file from "oldname.txt" to "newname.txt"?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

int main(void) 
{
  // Attempt to rename the file
  if (rename("rename_file.c", "5_rename_file.c") == 0) 
  {
     printf("File renamed successfully.\n");
  }
  else
  {
     perror("Error renaming file");
  }
  return 0;
}


/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 6. Implement a C program to delete a file named "delete_me.txt"?    *  
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

int main(void) 
{
  // remove the file
  if (remove("a.out") == 0) 
  {
     printf("File renamed successfully.\n");
  }
  else
  {
     perror("Error renaming file");
  }
  return 0;
}


/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 7. Write a C program to copy the contents of one file to another?           * 
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>

int main(void)
{
  int src_fd,des_fd,read_ref,write_ref,len;
  char buf[100];
  src_fd=open("src_file.txt",O_RDONLY); // source file must be exist
  printf("src_fd=%d\n",src_fd);                                                                      
  if(src_fd<0) 
  {
    printf("open system call failed\n");
    return 0;
  }
  des_fd=open("des_file.txt",O_CREAT|O_WRONLY|O_TRUNC,0666); 
  printf("des_fd=%d\n",des_fd);                                                                      
  if(des_fd<0) 
  {
    printf("open system call failed\n");
    close(src_fd);
    return 0;
  }
  while((read_ref=read(src_fd,buf,sizeof(buf)))>0)
  { 
    write_ref=write(des_fd,buf,read_ref);
    if(write_ref !=read_ref)
    {
      perror("write system call is failed\n");
      close(src_fd);
      close(des_fd);
      return 0;
    }
  }
  if(read_ref==0)
  {
    printf("Read from file is done\n");
  }
  else
  {
    perror("write system call is failed\n");
    close(src_fd);
    close(des_fd);
    return 0;
  }
}

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 8.Develop a C program to move a file from one directory to another?   *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>

int main(void) 
{
  char *old_path="src_file.txt";
  char *new_path="../destination/des.txt";
  // Attempt to rename the file
  if (rename(old_path,new_path) == 0) 
  {
     printf("File renamed successfully.\n");
  }
  else
  {
     perror("Error renaming file");
  }
  return 0;
}

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 9. Implement a C program to list all files in the current directory?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>

int main(void)
{
  struct dirent *dir_entry;  // Pointer for directory entry
  // Open the current directory
  DIR *dir_stream = opendir(".");  //DIR for directory stream 
  if (dir_stream == NULL)
  {
    perror("Could not open current directory");
    return 1;
  }
  printf("Files in the current directory:\n");
  while ((dir_entry = readdir(dir_stream)) != NULL)
  {
    printf("%s\n", dir_entry->d_name); //structure member
  }
  closedir(dir_stream);
  return 0;
}

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 10. Write a C program to get the size of a file named "file.txt"?     *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>

int main(void)
{
  struct stat file_stat;        //structure stat -- it stores file type,size,permissions
  if (stat("10_size_of_file.c", &file_stat) == -1) //stat is a system call 
  {
    perror("stat failed");
    return 1;
  }
  printf("Size of file.txt: %ld bytes\n", file_stat.st_size); 
  return 0;
}

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 11.Develop a C program to check if a directory named    *
 * "Test" exists in the current directory?                 *    
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>

int main(void)
{
  struct stat st; 
  // Check if "source" exists and is a directory
  if (stat("source", &st) == 0 && S_ISDIR(st.st_mode))  //S_ISDIR macro defination
  {
    printf("Directory 'source' exists in the current directory.\n");
  }
  else
  {
    printf("Directory 'source' does NOT exist in the current directory.\n");
  }
  return 0;
}

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 12.Implement a C program to create a new directory named "Backup" *
 * in the parent directory?                                          *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>

int main(void)
{
    int status;

    // Create directory in the parent directory
    status = mkdir("../Backup", 0777);

    if (status == 0)
    {
        printf("Directory 'Backup' created successfully in parent directory.\n");
    }
    else
    {
        perror("Failed to create directory");
    }

    return 0;
}

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 13. Write a C program to recursively list all files and           *
 * directories in a given directory?                                 *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */


#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <sys/stat.h>
#include <string.h>

void listFiles(const char *basePath);

int main(void)
{
    const char *path = ".";  // Starting from current directory
    printf("Listing files in: %s\n", path);
    listFiles(path);
    return 0;
}

void listFiles(const char *basePath)
{
  char path[1000];
  struct dirent *dp;
  DIR *dir = opendir(basePath);
  // Unable to open directory
  if (!dir)
      return;
  while ((dp = readdir(dir)) != NULL)
  {
    // Skip "." and ".."
    if (strcmp(dp->d_name, ".") == 0 || strcmp(dp->d_name, "..") == 0)
      continue;
    // Build full path
    snprintf(path, sizeof(path), "%s/%s", basePath, dp->d_name);
    printf("%s\n", path);
    // If it's a directory, recursively call
    struct stat statbuf;
    if (stat(path, &statbuf) == 0 && S_ISDIR(statbuf.st_mode))
    {
      listFiles(path);
    }
  }
  closedir(dir);
}

/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 14. Develop a C program to delete all files in a directory named "Temp"?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <unistd.h>
#include <string.h>
#include <sys/stat.h>

int main(void) 
{
  const char *dir_path = "./destination";  // Path to Temp directory
  DIR *dir = opendir(dir_path);
  struct dirent *entry;
  char filepath[1024];
  struct stat statbuf;
  if(!dir) 
  {
    perror("Unable to open directory");
    return 1;
  }
  while ((entry = readdir(dir)) != NULL) 
  {
    // Skip "." and ".."
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
       continue;
    // Construct full file path
    snprintf(filepath, sizeof(filepath), "%s/%s", dir_path, entry->d_name);
    // Check if it's a file (not directory)
    if (stat(filepath, &statbuf) == 0 && S_ISREG(statbuf.st_mode)) 
    {            
      if (remove(filepath) == 0) 
      {
        printf("Deleted file: %s\n", filepath);
      }
      else
      {
        perror("Failed to delete file");
      }
    }
  }
  closedir(dir);
  return 0;
}
```
