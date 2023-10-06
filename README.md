# OS-EX.6-IMPLEMENTATION-OF-INTER-PROCESS-COMMUNICATION-USING-PIPE
## AIM:
To Write C program to illustrate IPC using pipes mechanisms.

## ALGORITHM:
### Step 1:
Create a pipe (pipe(fd)).

### Step 2:
Fork a child process (child_pid = fork()).

### Step 3:
In the child process: 1. Close the read end of the pipe (close(fd[0])). 2. Write a message to the pipe (write(fd[1], message, strlen(message) + 1)). 3. Close the write end of the pipe (close(fd[1])). 4. Exit the child process (exit(EXIT_SUCCESS)).

### Step 4:
In the parent process: 1. Close the write end of the pipe (close(fd[1])). 2. Read a message from the pipe (read(fd[0], received_message, sizeof(received_message))). 3. Close the read end of the pipe (close(fd[0])). 4. Print the received message (printf("Parent received: %s\n", received_message)). 5. Parent process continues execution.

### Step 6:
End of the program (return 0 in the parent process).

## PROGRAM:
```
#include <stdio.h>
 #include<stdlib.h>
 #include<string.h>
 #include<sys/types.h>
 #include<sys/wait.h>
 #include<unistd.h>
int main()
{
int fd[2],child; char a[10];
printf("\n Enter the string:");
scanf("%s",a);
pipe(fd);
child=fork();
if(!child)
{
close(fd[0]);
write(fd[1],a,5); wait(0);
}
else
 {close(fd[1]);
read(fd[0],a,5);
printf("The string received from pipe is: %s",a);
}
return 0;
}
```
## OUTPUT:
![5](https://github.com/naveenaakumarasamy/OS-EX.6-IMPLEMENTATION-OF-INTER-PROCESS-COMMUNICATION-USING-PIPE/assets/113497406/ed4af795-7421-4fe1-ac68-3d0a02127f3f)

## Result:
This output confirms that the parent process successfully received and printed the message sent by the child process through the pipe, demonstrating inter-process communication using pipes.
