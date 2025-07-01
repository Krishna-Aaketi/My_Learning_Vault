## 1.Create a new text file and write user input to it
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 1.Write a C program to create a new text file and write user input to it    *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
int main(void)
{
  int fd,ref,len;
  char buf[100];
  printf("Enter a string:\n");
  scanf("%[^\n]",buf);           // be careful while using this format specifier --string length <= size-1
  len=strlen(buf);
  printf("%d\n",len);
  fd=open("file.txt",O_CREAT|O_RDWR|O_TRUNC,0666); //O_CREAT use for if file is not exist then its create
  printf("%d\n",fd);                               //O_RDWR use for write and file operation on files
                                                   // O_TRUNC use for previous content removes 
  if(fd<0)                                   // open system call return -1 open system call is failed 
  {
    printf("open system call failed\n");
    return 0;
  }
  ref=write(fd,buf,strlen(buf));                //write system return number of bytes written
  printf("%d\n",ref);
  if(ref<0)                                    // write system call return -1 write system call is failed
  {
    printf("Write system call is failed\n");
    return 0;
  }
  close(fd);                      //  close fd other than next runtime open system call fails
  return 0;
}
```
## 2.Open an existing text file and display its contents 
```c
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
```
## 3.Create a new directory in the current directory?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 3.Implement a C program to create a new directory named "Test" in the current directory?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

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
```
## 4.Check if a file exists in the current directory
```c
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
```
## 5.rename a file ?
```c
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
```
## 6.Delete a file named "delete_me.txt"?
```c
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
```
## 7.Copy the contents of one file to another?  
```c
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
```
### 8.Move a file from one directory to another?
```c
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
```
### 9.List all files in the current directory?
```c
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
```
### 10.Get the size of a file named "file.txt"?
```c
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
```
### 11.Check if a directory exists in the current directory?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 11.Develop a C program to check if a directory named "Test" exists in the current directory?  *    
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

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
```
### 12.Create a new directory named "Backup" in the parent directory? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 12.Implement a C program to create a new directory named "Backup" in the parent directory?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

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
```
### 13.Recursively list all files and directories in a given directory?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 13. Write a C program to recursively list all files and directories in a given directory? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */

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
```
### 14.Delete all files in a directory named "Temp"? 
```c
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
### 15.Count the number of lines in a file named "data.txt"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 15.Implement a C program to count the number of lines in a file named "data.txt"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>

int main(void) 
{
  FILE *fp;
  char ch;
  int line_count = 0;
  // Open the file in read mode
  fp = fopen("message.txt", "r");
  if (fp == NULL) 
  {
    perror("Error opening file");
    return 1;
  }
  // Read character by character and count '\n'
  while ((ch = fgetc(fp)) != EOF) 
  {	  
    if (ch == '\n') 
    {       
      line_count++;
    }
  }
  fclose(fp);
  printf("Total number of lines: %d\n", line_count);
  return 0;
}
```
### 16.Append "Goodbye!" to the end of an existing file named "message.txt"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 16.Write a C program to append "Goodbye!" to the end of an existing file named "message.txt"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 
#include <stdio.h>

int main(void) 
{
  FILE *fp;
  // Open file in append mode
  fp = fopen("message.txt", "a");
  if (fp == NULL) 
  {
    perror("Error opening file");
    return 1;
  }
  // Append "Goodbye!" to the file
  fprintf(fp, "Goodbye!\n");
  fclose(fp);
  printf("Text appended successfully.\n");
  return 0;
}
```
### 17.Change the permissions of a file named "file.txt" to readonly?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 17.Implement a C program to change the permissions of a file named "file.txt" to readonly? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>

int main(void) 
{
  const char *filename = "message.txt";
  // Set file permission to read-only: 0444 (r--r--r--) write:(-w--w--w-) 0222
  if (chmod(filename, 0444) == 0) 
  {
    printf("Permissions changed to read-only successfully.\n");
  }
  else 
  {
    perror("Failed to change file permissions");
    return 1;
  }
  return 0;
}
```
### 18.Change the ownership of a file named "file.txt" to the user "user1"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 18. Write a C program to change the ownership of a file named "file.txt" to the user "user1"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>
#include <pwd.h>

int main(void) 
{
  const char *filename = "message.txt";
  const char *username = "user1";
  struct passwd *pw = getpwnam(username); //user account information
  if (pw == NULL) 
  {
    perror("User not found");
    return 1;
  }
  // Change owner to user1, keep group unchanged (-1)
  if (chown(filename, pw->pw_uid, -1) == 0)   //pw_uid
  {
    printf("Ownership changed to '%s' successfully.\n", username);
  }
  else
  {
    perror("Failed to change file ownership");
     return 1;
  }
  return 0;
}
```
### 19.Get the last modified timestamp of a file named "file.txt"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 19. Develop a C program to get the last modified timestamp of a file named "file.txt"?    *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <sys/stat.h>
#include <time.h>

int main(void) 
{
  const char *filename = "message.txt";
  struct stat file_stat;
  if(stat(filename, &file_stat) == -1)
  {
    perror("stat");
    return 1;
  }
  // Convert last modified time to readable format
  printf("Last modified time of %s: %s", filename, ctime(&file_stat.st_mtime));
  return 0;
}
```
### 20.Create a temporary file and write some data to it?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 20. Implement a C program to create a temporary file and write some data to it? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>

int main() 
{
  // Create a temporary file
  FILE *temp_file = tmpfile();
  if (temp_file == NULL) 
  {
    perror("Failed to create temporary file");
    return 1;
  }
  // Write data to the temporary file
  const char *data = "This is temporary data.\n";
  fputs(data, temp_file);
  // Rewind the file pointer to read from beginning
  rewind(temp_file);
  // Read back the data
  char buffer[100];
  printf("Reading from temporary file:\n");
  while (fgets(buffer, sizeof(buffer), temp_file) != NULL) 
  {
    printf("%s", buffer);
  }
  // Temporary file will be deleted automatically on closing
  fclose(temp_file);
  return 0;
}
```
### 21.Check if a given path refers to a file or a directory?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 *21. Write a C program to check if a given path refers to a file or a directory?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <sys/stat.h>

int main(void) 
{
  const char *path = "/mnt/c/viven/linux/files/basic_io_calls";  // Change this to your target path
  struct stat path_stat;
  // Get file/directory information
  if (stat(path, &path_stat) != 0) 
  {
    perror("stat");
    return 1;
  }
  // Check type
  if (S_ISREG(path_stat.st_mode)) 
  {
    printf("The path '%s' is a regular file.\n", path);
  }
  else if (S_ISDIR(path_stat.st_mode)) 
  {
    printf("The path '%s' is a directory.\n", path);
  }
  else 
  {
    printf("The path '%s' is neither a regular file nor a directory.\n", path);
  }
  return 0;
}
```
### 23.Create a hard link named "hardlink.txt" to a file named "source.txt"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 22. Develop a C program to create a hard link named "hardlink.txt" to a file named "source.txt"?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <unistd.h>

int main(void) 
{
  const char *source = "message.txt";
  const char *hardlink = "hardlink.txt";  //A hard link is an additional directory entry that points to the same inode
                                          //(i.e., the same data on disk) as the original file.
  // Attempt to create the hard link
  if (link(source, hardlink) == 0) 
  {
    printf("Hard link '%s' created for '%s'\n", hardlink, source);
  }
  else 
  {
    perror("Failed to create hard link");
  }
  return 0;
}
```
### 23.Read and display the contents of a CSV file named "data.csv"
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
 * 23. Implement a C program to read and display the contents of a CSV file named "data.csv"?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 
#include <stdio.h>
#include <stdlib.h>

int main(void) 
{
  FILE *fp = fopen("data.csv", "r");  // Open the CSV file in read mode
  char buffer[1024];
  if (fp == NULL) 
  {
    perror("Unable to open file");
    return 1;
  }
  printf("Contents of data.csv:\n\n");
  while (fgets(buffer, sizeof(buffer), fp)) 
  {
    printf("%s", buffer);  // Print each line (row) of the CSV file
  }
  fclose(fp);
  return 0;
}
```
### 24.Get the absolute path of the current working directory?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 24. Write a C program to get the absolute path of the current working directory?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <unistd.h>
#include <limits.h>

int main(void) 
{
  char cwd[PATH_MAX];  // Buffer 4096 size to store the current working directory path
  if (getcwd(cwd, sizeof(cwd)) != NULL) 
  {
    printf("Current working directory: %s\n", cwd);
  }
  else
  {
    perror("getcwd() error");
    return 1;
  }
  return 0;
}
```
### 25.Get the size of a directory
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 25. Develop a C program to get the size of a directory named "Documents"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <string.h>
#include <sys/stat.h>
#include <unistd.h>

long get_directory_size(const char *path); 

int main(void) 
{
  const char *dirname = "destination";
  long size = get_directory_size(dirname);
  printf("Total size of directory '%s': %ld bytes\n", dirname, size);
  return 0;
}

long get_directory_size(const char *path) 
{
  struct dirent *entry;
  struct stat statbuf;
  char fullpath[1024];
  long total_size = 0;
  DIR *dir = opendir(path);
  if (!dir) 
  {
    perror("opendir failed");
    return 0;
  }
  while ((entry = readdir(dir)) != NULL) 
  {
    // Skip "." and ".."
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
       continue;
    snprintf(fullpath, sizeof(fullpath), "%s/%s", path, entry->d_name);
    if (stat(fullpath, &statbuf) == -1) 
    {
      perror("stat failed");
      continue;
    }
    if (S_ISDIR(statbuf.st_mode)) 
    {
      // Recursively get size of subdirectories
      total_size += get_directory_size(fullpath);
    }
    else if (S_ISREG(statbuf.st_mode)) 
    {
      // Add size of regular file
      total_size += statbuf.st_size;
    }
  }
  closedir(dir);
  return total_size;
}
```
### 26.Recursively copy all files and directories from one directory to another?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 26. Implement a C program to recursively copy all files and directories from one directory to another?  *  
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/stat.h>
#include <unistd.h>
#include <fcntl.h>
#include <dirent.h>
#include <errno.h>

void copy_file(const char *src, const char *dst); 
void copy_directory(const char *src_dir, const char *dst_dir); 

int main(void) 
{
  const char *source = "source_dir";
  const char *destination = "destination_dir";
  copy_directory(source, destination);
  printf("All contents copied from '%s' to '%s'\n", source, destination);
  return 0;
}

void copy_file(const char *src, const char *dst) 
{
  int in, out;
  char buffer[4096];
  ssize_t bytes;
  in = open(src, O_RDONLY);
  if (in < 0) 
  {
    perror("open src");
    return;
  }
  out = open(dst, O_WRONLY | O_CREAT | O_TRUNC, 0644);
  if (out < 0) 
  {
    perror("open dst");
    close(in);
    return;
  }
  while ((bytes = read(in, buffer, sizeof(buffer))) > 0) 
  {
    write(out, buffer, bytes);
  }
  close(in);
  close(out);
}

void copy_directory(const char *src_dir, const char *dst_dir) 
{
  struct dirent *entry;
  DIR *dir = opendir(src_dir);
  if (!dir) 
  {
    perror("opendir");
    return;
  }
  mkdir(dst_dir, 0755); // Create destination directory if not exists
  while ((entry = readdir(dir)) != NULL) 
  {
    char src_path[1024];
    char dst_path[1024];
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
       continue;
    snprintf(src_path, sizeof(src_path), "%s/%s", src_dir, entry->d_name);
    snprintf(dst_path, sizeof(dst_path), "%s/%s", dst_dir, entry->d_name);
    struct stat statbuf;
    stat(src_path, &statbuf);
    if (S_ISDIR(statbuf.st_mode)) 
    {
      copy_directory(src_path, dst_path);  // Recursive call
    }
    else if (S_ISREG(statbuf.st_mode)) 
    {
      copy_file(src_path, dst_path);       // Copy file
    }
  }
  closedir(dir);
}
```
### 27.Get the number of files in a directory
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 27. Write a C program to get the number of files in a directory named "Images"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <sys/stat.h>
#include <string.h>

int main(void) 
{
  DIR *dir;
  struct dirent *entry;
  struct stat file_stat;
  int count = 0;
  const char *dirname = "destination";
  dir = opendir(dirname);
  if (dir == NULL) 
  {
    perror("opendir failed");
    return 1;
  }
  while ((entry = readdir(dir)) != NULL) 
  {
    // Skip . and ..
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
       continue;
    char path[1024];
    snprintf(path, sizeof(path), "%s/%s", dirname, entry->d_name);
    if (stat(path, &file_stat) == 0 && S_ISREG(file_stat.st_mode)) 
    {
      count++;
    }
  }
  closedir(dir);
  printf("Number of regular files in '%s': %d\n", dirname, count);
  return 0;
}
```
### 28.create a FIFO in the current directory? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
 * 28. Develop a C program to create a FIFO (named pipe) named "myfifo" in the current directory?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 
#if 0
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <errno.h>
#include <sys/ipc.h>

int main(void) 
{
  //const char *fifo_path = "myfifo";
  // Create the FIFO with read-write permissions for owner, group, and others
  if (mkfifo("myfifo", 0666) < 0)
  {
    if (errno == EEXIST) 
    {
      printf("FIFO  already exists.\n");
    } 
    else
    {
      perror("mkfifo failed");
      exit(EXIT_FAILURE);
    }
  }
  else
  {
    printf("FIFO  created successfully.\n");
  }
  return 0;
}
#endif

#include<stdio.h>
#include<sys/ipc.h>

int main(void)
{
  int ret=mkfifo("myfifo",0666);
  if(ret<0)
  {
    printf("error in creating the fifo\n");
    return -1;
  }
  printf("fifo is created\n");
  return 0;
}
```
### 29.Read data from a FIFO named "myfifo"? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 29. Implement a C program to read data from a FIFO named "myfifo"?  * 
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>

int main() 
{
  int fd;
  char buffer[1024];
  ssize_t bytesRead;
  // Open the FIFO for reading only
  fd = open("myfifo", O_RDONLY);
  if (fd < 0) 
  {
    perror("Failed to open FIFO for reading");
    exit(EXIT_FAILURE);
  }
  printf("Reading data from FIFO:\n");
  while ((bytesRead = read(fd, buffer, sizeof(buffer) - 1)) > 0) 
  {
    buffer[bytesRead] = '\0';  // Null-terminate the string
    printf("Received: %s", buffer);
  }
  if (bytesRead == -1) 
  {
    perror("read");
  }
  close(fd);
  return 0;
}
```
### 30.Truncate a file named "file.txt" to a specified length?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 30. Write a C program to truncate a file named "file.txt" to a specified length?  * 
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <unistd.h>   // for truncate()
#include <stdlib.h>   // for exit()

int main(void) 
{
  const char *filename = "file2.txt";
  off_t new_length = 10;  // Truncate the file to 10 bytes
  if (truncate(filename, new_length) == 0) 
  {
    printf("File '%s' truncated to %ld bytes successfully.\n", filename, (long)new_length);
  }
  else
  {
    perror("truncate failed");
    exit(EXIT_FAILURE);
  }
  return 0;
}
```
### 31.Search for a specific string in a file and display the line number(s)
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 31. Develop a C program to search for a specific string in a file named "data.txt" and display the line number(s) where it occurs?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <string.h>

int main(void)
{
  FILE *fp;
  char line[1024];
  char keyword[100];
  int line_num = 0;
  int found = 0;
  // Input string to search
  printf("Enter string to search: ");
  scanf("%s", keyword);
  // Open file
  fp = fopen("message.txt", "r");
  if (fp == NULL) 
  {
    perror("Failed to open file");
    return 1;
  }
  // Read lines one by one
  while (fgets(line, sizeof(line), fp) != NULL) 
  {
    line_num++;
    if (strstr(line, keyword) != NULL)
    {
      printf("Found '%s' on line %d: %s", keyword, line_num, line);
      found = 1;
    }
  }
  fclose(fp);
  if (!found)
  {
    printf("'%s' not found in file.\n", keyword);
  }
  return 0;
}
```
### 32.Get the file type (regular file, directory,symbolic link, etc.) of a given path?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 32. Implement a C program to get the file type (regular file, directory,symbolic link, etc.) of a given path? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <sys/stat.h>
#include <unistd.h>

int main(void) 
{
  struct stat fileStat;
  char path[256];
  // Get input path from user
  printf("Enter the path: ");
  scanf("%s", path);
  // Use lstat to get file info (handles symbolic links too)
  if(lstat(path, &fileStat) == -1) 
  {
    perror("lstat failed");
    return 1;
  }
  // Determine the file type
  if (S_ISREG(fileStat.st_mode))
     printf("It is a regular file.\n");
  else if (S_ISDIR(fileStat.st_mode))
     printf("It is a directory.\n");
  else if (S_ISLNK(fileStat.st_mode))
     printf("It is a symbolic link.\n");
  else if (S_ISCHR(fileStat.st_mode))
     printf("It is a character device file.\n");
  else if (S_ISBLK(fileStat.st_mode))
     printf("It is a block device file.\n");
  else if (S_ISFIFO(fileStat.st_mode))
     printf("It is a FIFO/pipe.\n");
  else if (S_ISSOCK(fileStat.st_mode))
     printf("It is a socket.\n");
  else
     printf("Unknown file type.\n");
     return 0;
}
```
### 33.Create a new empty file named "empty.txt"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 33. Write a C program to create a new empty file named "empty.txt"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main(void)
{
  int fd;
  // Open or create the file with write-only mode and permission 0644
  fd = open("empty.txt", O_CREAT | O_WRONLY | O_TRUNC, 0644);
  if (fd < 0) 
  {
    perror("File creation failed");
    return 1;
  }
  printf("File 'empty.txt' created successfully.\n");
  close(fd);
  return 0;
}
```
### 34.Get the permissions (mode) of a file named "file.txt"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 34. Develop a C program to get the permissions (mode) of a file named "file.txt"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>

int main(void) 
{
  struct stat fileStat;
  // Get file information
  if (stat("file2.txt", &fileStat) < 0) 
  {
    perror("stat failed");
    return 1;
  }
  printf("Permissions for 'file.txt':\n");
  // File type
  printf( (S_ISDIR(fileStat.st_mode)) ? "d" : "-");
  // Owner permissions
  printf( (fileStat.st_mode & S_IRUSR) ? "r" : "-");
  printf( (fileStat.st_mode & S_IWUSR) ? "w" : "-");
  printf( (fileStat.st_mode & S_IXUSR) ? "x" : "-");
  // Group permissions
  printf( (fileStat.st_mode & S_IRGRP) ? "r" : "-");
  printf( (fileStat.st_mode & S_IWGRP) ? "w" : "-");
  printf( (fileStat.st_mode & S_IXGRP) ? "x" : "-");
  // Others permissions
  printf( (fileStat.st_mode & S_IROTH) ? "r" : "-");
  printf( (fileStat.st_mode & S_IWOTH) ? "w" : "-");
  printf( (fileStat.st_mode & S_IXOTH) ? "x" : "-");
  printf("\n");
  return 0;
}
```
### 35.Recursively delete a directory named "Temp" and all its contents?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 35. Implement a C program to recursively delete a directory named "Temp" and all its contents?  *                     
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
#include <errno.h>


int delete_directory(const char *path); 

int main(void) 
{
  const char *target_dir = "Temp";
  if (delete_directory(target_dir) == 0) 
  {
    printf("Directory '%s' deleted successfully.\n", target_dir);
  }
  else
  {
    printf("Failed to delete directory '%s'.\n", target_dir);
  }
  return 0;
}

int delete_directory(const char *path) 
{
  struct dirent *entry;
  DIR *dir = opendir(path);
  if (dir == NULL) 
  {
    perror("opendir failed");
    return -1;
  }
  while ((entry = readdir(dir)) != NULL) 
  {
    char full_path[1024];
    // Skip "." and ".."
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;
    snprintf(full_path, sizeof(full_path), "%s/%s", path, entry->d_name);
    struct stat st;
    if (stat(full_path, &st) == -1) 
    {
      perror("stat failed");
      closedir(dir);
      return -1;
    }
    if (S_ISDIR(st.st_mode)) 
    {
      // Recursively delete subdirectory
      if (delete_directory(full_path) == -1) 
      {
        closedir(dir);
        return -1;
      }
    }
    else
    {
      // Delete file
      if (remove(full_path) == -1) 
      {
        perror("remove file failed");
        closedir(dir);
        return -1;
      }
    }
  }
  closedir(dir);
  // Remove the empty directory
  if (rmdir(path) == -1) 
  {
    perror("rmdir failed");
    return -1;
  }
  return 0;
}
```
### 36.Read and display the first 10 lines of a file named "log.txt"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 36. Write a C program to read and display the first 10 lines of a file named "log.txt"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>

int main(void) 
{
  FILE *fp;
  char buffer[1024];
  int line_count = 0;
  fp = fopen("36_read_dispaly_first_10_lines.c", "r");
  if (fp == NULL)
  {
    perror("Failed to open file");
    return 1;
  }
  while (fgets(buffer, sizeof(buffer), fp) != NULL)
  {
    printf("%s", buffer);
    line_count++;
    if (line_count >= 10)
       break;
  }
  fclose(fp);
  return 0;
}
```
### 37.read data from a text file and write it to another file in reverse order? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 37. Develop a C program to read data from a text file named "input.txt" and write it to another file named "output.txt" in reverse order? * 
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>

int main(void) 
{
  FILE *in_fp, *out_fp;
  long file_size;
  char ch;
  // Open input file in read mode
  in_fp = fopen("des_file.txt", "r");
  if (in_fp == NULL)
  {
    perror("Failed to open input.txt");
    return 1;
  }
  // Open output file in write mode
  out_fp = fopen("output.txt", "w");
  if (out_fp == NULL)
  {
    perror("Failed to open output.txt");
    fclose(in_fp);
    return 1;
  }
  // Move to end to find file size
  fseek(in_fp, 0, SEEK_END);                  // fseek() -Moves the file position indicator to a given byte in the file.
  file_size = ftell(in_fp);                   //  SEEK_END -Moves the file pointer to the end of file.
  // Read from end and write to output    //ftell()-Returns the current file pointer position (here, it gives the file size after fseek to end).  
  for (long i = file_size - 1; i >= 0; i--) 
  {
    fseek(in_fp, i, SEEK_SET);                       //SEEK_SET -Moves the file pointer to the i-th byte from the beginning
    ch = fgetc(in_fp);                           
    fputc(ch, out_fp);
  }
  printf("Data written to output.txt in reverse order.\n");
  fclose(in_fp);
  fclose(out_fp);
  return 0;
}
```
### 38.create a new directory with the current date in the format "YYYY-MM-DD"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 38. Implement a C program to create a new directory named with the current date in the format "YYYY-MM-DD"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <time.h>
#include <sys/stat.h>
#include <string.h>
#include <errno.h>

int main(void) 
{
  time_t now;
  struct tm *timeinfo;
  char dirname[20];
  // Get current time
  time(&now);
  timeinfo = localtime(&now);
  // Format time as "YYYY-MM-DD"
  strftime(dirname, sizeof(dirname), "%Y-%m-%d", timeinfo);
  // Create the directory with 0755 permissions
  if (mkdir(dirname, 0755) == 0) 
  {
    printf("Directory '%s' created successfully.\n", dirname);
  }
  else
  {
    perror("Directory creation failed");
  }
  return 0;
}
```
### 39.Read and display the contents of a "binary.bin"?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 39. Write a C program to read and display the contents of a binary file named "binary.bin"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>

int main(void) 
{
  FILE *file;
  unsigned char buffer[16];  // Read in chunks of 16 bytes
  size_t bytesRead;
  int offset = 0;
  file = fopen("binary.bin", "rb");
  if (file == NULL) 
  {
    perror("Error opening binary file");
    return 1;
  }
  printf("Contents of binary.bin in hexadecimal:\n\n");
  while ((bytesRead = fread(buffer, sizeof(unsigned char), sizeof(buffer), file)) > 0) 
  {
    printf("0x%04X : ", offset);
    for (size_t i = 0; i < bytesRead; i++) 
    {
      printf("%02X ", buffer[i]);
    }
    printf("\n");
    offset += bytesRead;
  }
  fclose(file);
  return 0;
}
```
### 40.Get the size of the largest file in a directory?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 40. Develop a C program to get the size of the largest file in a directory?   *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
#include <limits.h>


off_t get_largest_file_size(const char *path, char *largest_file_path);

int main(void) 
{
  const char *directory = ".";  // current directory
  char largest_file[PATH_MAX] = {0};
  off_t size = get_largest_file_size(directory, largest_file);
  if (size >= 0)
  {
    printf("Largest file: %s\n", largest_file);
    printf("Size: %ld bytes\n", size);
  }
  else
  {
    printf("Failed to determine largest file.\n");
  }
  return 0;
}

off_t get_largest_file_size(const char *path, char *largest_file_path) 
{
  struct dirent *entry;
  struct stat file_stat;
  DIR *dir = opendir(path);
  if (dir == NULL) 
  {
    perror("opendir failed");
    return -1;
  }
  off_t max_size = 0;
  char full_path[PATH_MAX];
  while ((entry = readdir(dir)) != NULL) 
  {
    // Ignore "." and ".."
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
       continue;
    snprintf(full_path, sizeof(full_path), "%s/%s", path, entry->d_name);
    if (stat(full_path, &file_stat) == -1) 
    {
      perror("stat failed");
      continue;
    }
    if (S_ISDIR(file_stat.st_mode)) 
    {
      // Recurse into subdirectory
      off_t sub_size = get_largest_file_size(full_path, largest_file_path);
      if (sub_size > max_size) 
      {
        max_size = sub_size;
      }
    }
    else if (S_ISREG(file_stat.st_mode)) 
    {
      // It's a regular file
      if (file_stat.st_size > max_size) 
      {
        max_size = file_stat.st_size;
        strcpy(largest_file_path, full_path);
      }
    }
  }
  closedir(dir);
  return max_size;
}
```
### 41.Check if a file named "data.txt" is readable? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 41. Implement a C program to check if a file named "data.txt" is readable?  * 
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <unistd.h>

int main(void) 
{
  const char *filename = "message.txt";
  // Use access() with R_OK to check readability
  if (access(filename, R_OK) == 0)
  {
     printf("The file \"%s\" is readable.\n", filename);
  }
  else
  {
    perror("File check failed");
  }
  return 0;
}
```
### 42.Directory "Logs" and move all files with the ".log" extension into it? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
 * 42. Write a C program to create a new directory named "Logs" and move all files with the ".log" extension into it?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 
 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>

int main(void) 
{
  DIR *d;
  struct dirent *dir;
  char src_path[512], dest_path[512];
  // Step 1: Create "Logs" directory if it doesn't exist
  if (mkdir("Logs", 0777) == -1) 
  {	 
    perror("mkdir");
    // Continue anyway in case it already exists
  }
  else
  {
    printf("Directory 'Logs' created successfully.\n");
  }
  // Step 2: Open current directory
  d = opendir(".");
  if (d == NULL)
  {
    perror("opendir");
    return 1;
  }
  // Step 3: Read directory entries
  while ((dir = readdir(d)) != NULL) 
  {
    // Skip . and ..
    if (strcmp(dir->d_name, ".") == 0 || strcmp(dir->d_name, "..") == 0)
        continue;
    // Check for ".log" extension
    if (strstr(dir->d_name, ".log") != NULL &&
            strcmp(dir->d_name + strlen(dir->d_name) - 4, ".log") == 0) 
    {
      // Construct source and destination paths
      snprintf(src_path, sizeof(src_path), "./%s", dir->d_name);
      snprintf(dest_path, sizeof(dest_path), "./Logs/%s", dir->d_name);
      // Move the file
      if (rename(src_path, dest_path) == 0) 
      {
        printf("Moved: %s --> Logs/\n", dir->d_name);
      }
      else
      {
         perror("rename");
      }
    }
  }
  closedir(d);
  return 0;
}
```
### 43.Check if a file "config.ini" is writable?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 43. Develop a C program to check if a file named "config.ini" is writable?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <unistd.h>

int main(void) 
{
  char *filename = "config.ini";
  // Check write permission using access()
  if (access(filename, W_OK) == 0) 
  {
    printf("The file \"%s\" is writable.\n", filename);
  }
  else 
  {
    perror("Access check failed");
    printf("The file \"%s\" is not writable.\n", filename);
  }
  return 0;
}
```
### 44.Read the contents of a text file and execute the instructions as shell commands? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 44. Implement a C program to read the contents of a text file named "instructions.txt" and execute the instructions as shell commands?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include<stdio.h>
#include<stdlib.h>

int main(void)
{
  FILE *fd;
  fd=fopen("instruction.txt","r");
  if(fd==NULL)
  {
    printf("File open failed");
    return 1;
  }
  char cmd[256];
  while(fgets(cmd,sizeof(cmd),fd))
  {
    system(cmd);
  }
  fclose(fd);
  return 0;
}
```
### 45.Get the number of hard links to a file 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 45. Write a C program to get the number of hard links to a file named "file.txt"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>

int main(void)
{
  struct stat fileStat;
  // Get file stats
  if (stat("file2.txt", &fileStat) < 0)
  {
    perror("stat() failed");
    return 1;
  }
  // Display number of hard links
  printf("Number of hard links to file.txt: %lu\n", (unsigned long)fileStat.st_nlink);
  return 0;
}
```
### 46.Copy the contents of all text files in a directory into a single file
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 46. Develop a C program to copy the contents of all text files in a directory into a single file named "combined.txt"?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * / 

#include <stdio.h>
#include <dirent.h>
#include <string.h>
#include <stdlib.h>

int main(void) 
{
  DIR *dir;
  struct dirent *entry;
  FILE *src, *dest;
  char buffer[1024];
  dir = opendir(".");
  if (dir == NULL)
  {
    perror("Failed to open current directory");
    return 1;
  }
  dest = fopen("combined.txt", "w");
  if (dest == NULL)
  {
    perror("Failed to open combined.txt");
    closedir(dir);
    return 1;
  }
  while ((entry = readdir(dir)) != NULL)
  {
    // Check for .txt extension and exclude combined.txt itself
    if (strstr(entry->d_name, ".c") != NULL && strcmp(entry->d_name, "combined.txt") != 0)
    {
      src = fopen(entry->d_name, "r");
      if (src == NULL) 
      {
        perror("Failed to open source file");
        continue;
      }
      size_t n;
      while ((n = fread(buffer, 1, sizeof(buffer), src)) > 0)
      {	      
	fwrite(buffer, 1, n, dest);    
      }
      fclose(src);
    }
  }
  fclose(dest); 
  closedir(dir);
  printf("All text files have been combined into combined.txt\n");
  return 0;
}
```
### 47.Recursively calculate the total size of all files in a directory and its subdirectories?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
 * 47. Implement a C program to recursively calculate the total size of all files in a directory and its subdirectories? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>

long long get_directory_size(const char *path);

int main(void)
{
  const char *target_directory = ".";  // current directory
  long long total_size = get_directory_size(target_directory);
  printf("Total size of all files: %lld bytes\n", total_size);
  return 0;
}

long long get_directory_size(const char *path)
{
  struct dirent *entry;
  struct stat statbuf;
  DIR *dir = opendir(path);
  long long total_size = 0;
  if (!dir) 
  {
    perror("Failed to open directory");
    return 0;
  }
  while ((entry = readdir(dir)) != NULL) 
  {
    char fullpath[1024];
    // Skip current and parent directory entries
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
        continue;
    snprintf(fullpath, sizeof(fullpath), "%s/%s", path, entry->d_name);
    if (stat(fullpath, &statbuf) == -1) 
    {
      perror("stat failed");
      continue;
    }
    if (S_ISDIR(statbuf.st_mode)) 
    {
      total_size += get_directory_size(fullpath); // Recurse into subdirectory
    }
    else if (S_ISREG(statbuf.st_mode)) 
    {
      total_size += statbuf.st_size; // Add file size
    }
  }
  closedir(dir);
  return total_size;
}
```
### 48.Get the number of bytes in a file named "data.bin"? 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 48. Write a C program to get the number of bytes in a file named "data.bin"?    *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>

int main(void)
{
  FILE *file = fopen("data.bin", "rb");  // Open in binary read mode
  if (file == NULL) 
  {
    perror("Error opening file");
    return 1;
  }
  // Move file pointer to end
  fseek(file, 0, SEEK_END);
  // Get current position, which is file size
  long size = ftell(file);
  fclose(file);
  if (size < 0) 
  {
    perror("ftell failed");
    return 1;
  }
  printf("Size of data.bin: %ld bytes\n", size);
  return 0;
}
```
### 49.Create a new directory named with the current timestamp
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 49. Develop a C program to create a new directory named with the current timestamp in the format "YYYY-MM-DD-HH-MM-SS"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <sys/stat.h>
#include <string.h>

int main(void) 
{
  time_t now;
  struct tm *timeinfo;
  char dir_name[100];
  // Get current time
  time(&now);
  timeinfo = localtime(&now);
  // Format: YYYY-MM-DD-HH-MM-SS
  strftime(dir_name, sizeof(dir_name), "%Y-%m-%d-%H-%M-%S", timeinfo);
  // Create directory
  if (mkdir(dir_name, 0777) == 0)
  {
    printf("Directory '%s' created successfully.\n", dir_name);
  }
  else
  {
    perror("mkdir failed");
    return 1;
  }
  return 0;
}
```
### 52.Open a file named "data.txt" in read mode and display its contents?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 52. Implement a C program to open a file named "data.txt" in read mode and display its contents?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>

int main(void) 
{
  FILE *fp;
  char ch;
  // Open the file in read mode
  fp = fopen("data.txt", "r");
  if (fp == NULL) 
  {
    perror("Failed to open file");
    return 1;
  }
  // Read and display each character
  while ((ch = fgetc(fp)) != EOF) 
  {
    putchar(ch);
  }
  // Close the file
  fclose(fp);
  return 0;
}
```
### 63.create a symbolic link 
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 63. Write a C program to create a symbolic link named "link.txt" to a file named "target.txt"?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <unistd.h>

int main(void) 
{
  const char *target = "target.txt";
  const char *symlink_name = "link.txt";
  if (symlink(target, symlink_name) == 0) 
  {
    printf("Symbolic link '%s' created to '%s'\n", symlink_name, target);
  }
  else
  {
    perror("Error creating symbolic link");
  }
  return 0;
}
```
### 78.Read and display the contents of a binary file
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 78. Implement a C program to read and display the contents of a binary file named "binary.bin"? *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>

int main(void) 
{
  FILE *file;
  unsigned char buffer[1024];
  size_t bytesRead, i;
  // Open the binary file for reading
  file = fopen("binary.bin", "rb");
  if (file == NULL) 
  {
    perror("Error opening file");
    return 1;
  }
  // Read and display the contents
  while ((bytesRead = fread(buffer, 1, sizeof(buffer), file)) > 0) 
  {
    for (i = 0; i < bytesRead; i++) 
    {
      printf("%c", buffer[i]);  // Prints as characters (might not be readable)
    }
  }
  fclose(file);
  return 0;
}
```
### 82.Read data from a binary file and display it in hexadecimal format?
```c
/* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
 * 82. Develop a C program to read data from a binary file named "data.bin" and display it in hexadecimal format?  *
 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */ 

#include <stdio.h>
#include <stdlib.h>

int main(void) 
{
  FILE *fp = fopen("", "rb");  // Open file in binary read mode
  if (fp == NULL)
  {
    perror("Failed to open data.bin");
    return 1;
  }
  unsigned char buffer[16];  // Buffer to read 16 bytes at a time
  size_t bytesRead;
  int offset = 0;
  while ((bytesRead = fread(buffer, sizeof(unsigned char), sizeof(buffer), fp)) > 0) 
  {
    printf("%08x  ", offset);  // Print offset in hexadecimal
    for (size_t i = 0; i < bytesRead; i++) 
    {
      printf("%02x ", buffer[i]);  // Print byte in hex
    }
    printf("\n");
    offset += bytesRead;
  }
  fclose(fp);
  return 0;
}
```
