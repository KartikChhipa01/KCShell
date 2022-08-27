# KCSH
KCSH is a simple implementation of shell in C. It demonstrates the basics of how shell works. Since its purpose is demonstration (not completeness of features, it has many limitations. KCSH runs in interactive mode.
KCSH is most rudimentary shell and is structured as the following loop:
1. The shell runs continuously and displays a prompt of the format (pwd:~$) where pwd stands for the **present work directory**
2. The shell reads input one at a time
3. Parse the input into program name and an array of parameters
4. Use $fork()$ system call to spawn a new child process 
    * The child process uses $execvp()$ system call to launch specified program
    * The parent process uses $wait()$ system call to wait for child process to terminate
5. Once the child process finishes. The shell repeates the loop.
6. The only builtin commands are `exit`, `cd`, `history`

Aditionally implemented functions to change the color of the prompt
## Running 
Use `gcc kcsh.c -o kcsh` to compile and then use `./kcsh` to run the shell 
To Test for pipeline run the command `ping -c 5 www.google.com | grep rtt` in the shell window
## Internal Commands Implemented
* **history [argument optional]** command displays all the commands entered by the user in the shell window. A file is created to store all the commands entered so that history does not get destroyed even after closing the shell. Argument accepts a numeric value and displays the last K number of commands entered. `working`
* **pwd** displays the present work directory `working`
* **cd [dir (..)/dir]** is used to nevigate through the directories `working`
* **exit** command is used to escape from the shell `working`
* **ls [-l optional]** command is used to list all the files and sub directories in the present directory `working`

* **mkdir** creates a directory at the specified, if complete path not specified then creates a directory at pwd with the specified name `working`
* **rmdir** removes specified directory, if complete path not specified then removes the specified directory at pwd `working`
* **env** lists all the environment parameters. `working`
* **clear** clears the shell screen `working`
Rest other commands are executed using $execvp()$ command `working`
## Foreground and Background Processes
The kcsh shell also knows how to launch the programs in foreground and background. Using **&** at the end of the command will run the program in background more. For example try running **sleep 3** and **sleep 3 &** command in the shell and observe the outcome. `working`
**Note :** Foreground and background processes **not working** for pipelined commands
## Parsing 
Two kind of parsing is performed. Parsing is performed separately when the input contains pipes and when the input does not contains pipe. Parsing of the input is performed using the $strtok()$ function.
## Limitation
* No functionality to execute previously executed command or to browse the previously executed command using tab and arrow key. 
* Commands must be on a single line
* Arguments must be separated by whitespaces
* No quoting arguments or escaping whitespaces
* Multiple pipeline commands not executing properly


## License
This code is in the public domain (see [UNLICENSE](UNLICENSE) for more details). This means you can use, modify, and distribute it without any restriction. I appreciate, but don't require, acknowledgement in derivative works.
