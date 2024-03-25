the `fork()` system call copies (almost) exactly the parent process. when the `fork()` method is called we get two identical processes.

it returns the process id of the child to the parent parent process while the child process receives 0. if the returned value is less than 0, then there is some error.

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
  printf(">> current process (pid: %d)\n", (int) getpid()); // eg, 123

  // creates an identical copy of the current process
  int rc = fork(); 

  // parent process will run the code below with rc=124 (pid of child)
  // child process will run the code below with rc=0
  if (rc < 0) {
    printf("xx forking failed...\n");
    exit(1);
  }
  else if (rc == 0) {
    // child process
    printf(">> child process (pid: %d)\n", (int) getpid()); // 124
    
  } else {
    // parent process
    printf(">> parent process (pid: %d) (rc: %d)\n", (int) getpid(), rc); // 123
  }
  
  return 0;
}
```

### wait() syscall
the `wait()` syscall will wait till another process if finished executing, then return a value (ie, continue execution).

in our case, if we call `wait()`  in our parent process, two things might happen
1. child process might execute first, in that case, child process will print first
2. parent process might execute first, in that case, it will wait and child process will execute and print first, then child process will complete and parent process will print.

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
  printf(">> current process (pid: %d)\n", (int) getpid()); // eg, 123

  // creates an identical copy of the current process
  int rc = fork(); 

  // parent process will run the code below with rc=124 (pid of child)
  // child process will run the code below with rc=0
  if (rc < 0) {
    printf("xx forking failed...\n");
    exit(1);
  }
  else if (rc == 0) {
    // child process
    printf(">> child process (pid: %d)\n", (int) getpid()); // 124
    
  } else {
    // parent process
    int rc_wait = wait(NULL);
    printf(">> parent process (pid: %d) (rc: %d) (rc_wait: %d)\n", (int) getpid(), rc, rc_wait); // 123
  }
  
  return 0;
}
```

### exec() syscall
The exec syscall is used to run any command. It has many variants like execvp, execl, etc.

```c
// exec syscall is used to run other command
// the code below prints out this file
char *comnd[3];
comnd[0] = strdup("head");
comnd[1] = strdup("fork.c");
comnd[2] = NULL;

printf(">> command: ");
for (int i=0; comnd[i] != NULL; i++) {
    printf("%s ", comnd[i]);
}
    
printf("\n>> Contents of %s:\n", comnd[1]);
execvp(comnd[0], comnd);
```

Here, we run `head fork.c` using the `execvp` syscall.

The exec syscall overwrites the static data from the mentioned executable (eg, in this case the `head` command). It also re-initialises the heap and other parts of memory.

Thus, it does not create a new process; rather, it transforms the currently running program.

### kill() syscall
The kill or killall syscall is used to kill a particular process.

```
kill(process_id, kill_signal)
```

kill signals:
- SIGINT -> interrupts the process, so that the program can exit on its own
- SIGKILL -> forcefully terminates a process