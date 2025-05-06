#for read wright creat in single code
#include <fcntl.h> 
#include <unistd.h> 
 
int main() { 
 int fd; 
  char buffer[100]; 
 
    // Create and write to the file 
    fd = open("file.txt", O_CREAT | O_WRONLY, 0777); 
    write(fd, "Hello, System Calls!\n", 21); 
    close(fd); 
    // Open and read the file 
    fd = open("file.txt", O_RDONLY); 
    read(fd, buffer, sizeof(buffer)); 
    write(1, buffer, sizeof(buffer));                     // Print to terminal (stdout) 
    close(fd); 
    return 0; 
} 



1 Example on lseek.
 #include <stdio.h> 
#include <fcntl.h> 
#include <unistd.h> 
int main() 
{ 
int fd; 
char buffer[20]; 
fd = open("testfile.txt", O_RDWR | O_CREAT , 0666); 
write(fd, "Hello, world",13); 
lseek(fd, 0, SEEK_SET);    // lseek() → Moves the file pointer. 
read(fd, buffer,13); 
lseek(fd,6, SEEK_SET);        
write(fd, "chatgpt", 7); 
close(fd); 
return 0; 
} 
//SEEK_SET is a constant used in the lseek() function to set the file pointer to a specific position from the beginning of the file. 
After running the program, testfile.txt will contain:   Hello ,chatgpt 
Example -2 on lseek 
#include <stdio.h> 
#include <fcntl.h> 
#include <unistd.h> 
int main() 
{ 
int fd = open("testfile1.txt", O_RDWR | O_CREAT, 0666); 
lseek(fd,0, SEEK_END);                             
write(fd, "Kumar" ,5); 
lseek(fd,5,SEEK_END); 
close(fd); 
return 0; 
} 
=======Stat========  
#include <stdio.h> 
    //SEEK_END → Moves the pointer relative to the end of the file. 
#include <sys/stat.h>   //#include <sys/stat.h> → Includes file status information functions, such as stat(). 
int main() 
{ 
struct stat s;   //The stat structure stores information about a file, such as:st_size → File size (in bytes). 
stat("testfile.txt", &s); 
printf("size: %ld bytes\n", s.st_size);   //s.st_size contains the file size in bytes 
return 0; 
} 
========chmod============ 
#include <stdio.h>  
#include <sys/stat.h>  
int main()  
{  
chmod("testfile.txt", 0777); // Set full read, write, execute permissions  
printf("Permissions changed.\n");  
return 0;  
} 
=====Hard Link (link() system call)======= 
 
#include <unistd.h> 
 
int main() { 
    link("original.txt", "hardlink.txt");   
    return 0; 
} 
 
=======Symbolic (Soft) Link (symlink() system call)====== 
 
#include <unistd.h> 
 
int main() { 
    symlink("original.txt", "symlink.txt");   
    return 0; 
} 



    
