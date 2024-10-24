# Linux-File-IO-Systems-locking
Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux IO Systems locking

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## 1.To Write a C program that illustrates files copying 

```
#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdlib.h>

int main() {
    char block[1024];
    int in, out;
    int nread;
    in = open("filecopy.c", O_RDONLY);
    out = open("file.out", O_WRONLY|O_CREAT, S_IRUSR|S_IWUSR);
    while((nread = read(in,block,sizeof(block))) > 0)
    write(out,block,nread);
    exit(0);
}
```
## OUTPUT
![WhatsApp Image 2024-10-19 at 20 21 12_deec5023](https://github.com/user-attachments/assets/84c35f00-3a03-4321-9343-6233de20b4a5)





## 2.To Write a C program that illustrates files locking
```
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/file.h>

int main (int argc, char* argv[]) {
    char* file = argv[1];
    int fd;
    struct flock lock;

    printf ("opening %s\n", file);

    /* Open a file descriptor to the file. */
    fd = open(file, O_WRONLY);

    // Acquire shared lock
    if (flock(fd, LOCK_SH) == -1) {
        printf("Error: Could not acquire shared lock\n");
    } else {
        printf("Acquiring shared lock using flock\n");
    }

    getchar(); // Wait for user input before upgrading lock

    // Non-atomically upgrade to exclusive lock (non-blocking mode)
    if (flock(fd, LOCK_EX | LOCK_NB) == -1) {
        printf("Error: Could not acquire exclusive lock\n");
    } else {
        printf("Acquiring exclusive lock using flock\n");
    }

    getchar(); // Wait for user input before unlocking

    // Release lock
    if (flock(fd, LOCK_UN) == -1) {
        printf("Error: Could not unlock\n");
    } else {
        printf("Unlocking\n");
    }

    close(fd);
    return 0;
}
```



## OUTPUT
![WhatsApp Image 2024-10-19 at 20 23 55_fe9108a6](https://github.com/user-attachments/assets/e5df2763-3afe-4b30-9321-41b1789f2e9d)





# RESULT:
The programs are executed successfully.
