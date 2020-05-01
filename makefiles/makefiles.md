[Source](https://opensource.com/article/18/8/what-how-makefile)
# Makefiles
A *Makefile* defines a set of tasks to be executed and is required by the *make* utility. For example you may have to use *make* to compile a program from source code.

# Basic examples
Define a *Makefile* with the following content:
```makefile
say_hello:
  echo "Hello World"
```

Launch a terminal and run

```zsh
$make
echo "Hello World"
Hello World
```

In the example above ```say_hello``` is called the **target** and behaves like a function name. The **dependencies** follow the target but here we did not define any. The command ```echo "Hello World"``` is called the **recipe**. The *recipe* uses the *dependencies* to make a *target*. Together the *target*, *dependencies* and *recipe* make a **rule**.
```makefile
target: dependencies
  recipe
```

In the context of compiling a target might be a binary file that depends on other source files. A *dependencie* can also be a *target* that depends on other *dependencies*
```makefile
final_target: sub_target final_target.c
  Recipe-to-create-final-target
sub_target: subtarget.c
  Recipe-to-create-sub-target
```

But it is not necessary for the target to be a file - it can also just be a name as in our first example. We call these **phony target**.

You can hide the *recipe* when running make by adding the ```@``` operator right before the *recipe*
```makefile
say_hello:
  @echo "Hello World
```
Launch a terminal and run
```zsh
$make
Hello World
```

To increase the utility of our first example let us add some *phony targets* called *generate* and *clean* to the *Makefile*:
```makefile
say_hello:
  @echo "Hello World"
generate:
  @echo "Creating empty text files..."
  touch file-{1..10}.txt
clean:
  @echo "Cleaning up..."
  rm *.txt
```

By default running *makes* calls the first *target* which is often called the *default goal*. For this reason the first *target* defined in a *Makefile* is often named *all* to call other targets. We can override this behavior using a special *phony target* called ```.DEFAULT_GOAL```.
```makefile
.DEFAULT_GOAL := generate
say_hello:
  @echo "Hello World"
generate:
  @echo "Creating empty text files..."
  touch file-{1..10}.txt
clean:
  @echo "Cleaning up..."
  rm *.txt
```
This will run the ```generate``` target as the default.

In most uses cases you want to call multiple targets - that is why most *Makefiles* include a target named ```all``` which can call as many targets as needed
```makefile
all: say_hello generate
say_hello:
  @echo "Hello World"
generate:
  @echo "Creating empty text files..."
  touch file-{1-..10}.txt
clean:
  @echo "Cleaning up..."
  rm *.txt
```
Before running make, let's include another special phony target, .PHONY, where we define all the targets that are not files. ```make``` will run its recipe regardless of whether a file with that name exists or what its last modification time is. Here is the complete makefile:
```makefile
.PHONY: all say_hello generate clean
all: say_hello generate
say_hello:
  @echo "Hello World"
generate:
  @echo "Creating empty text files..."
  touch file-{1-..10}.txt
clean:
  @echo "Cleaning up..."
  rm *.txt
```
The ```make``` command will run ```say_hello``` and ```generate```. Note that it is good practice to run ```clean``` manually.

# Advanced Exampels
## Define Variables
In projects the *targets* and *dependencies* are often replaced with variables.
Use the ```=``` operator the define a variable
```makefile
CC = gcc
hello: hello.c
${CC} hello.c -o hello
```
This expands to
```makefile
gcc hello.c -o hello
```
Both ```${CC}``` and ```$(CC)``` resolve a to ```gcc```.

The variable defined by the ```=``` operator is called *recursive expanded variable* which may cause a infinite loop if one tries to reassign a variable to itself
```makefile
CC = gcc
CC = ${CC}
```
Launch a terminal and run
```zsh
$make
Makefile:8: *** Recursive variable 'CC' references itself (eventually).  Stop.
```
To avoid this scenario, we can use the := operator (this is also called the *simply expanded variable*). We should have no problem running the makefile below:
```makefile
CC := gcc
CC := ${CC}

all:
    @echo ${CC}
```

Below is a *Makefile*, assuming it is placed in a directory having a single foo.c file to complile it:
```makefile
# Usage:
# make 				# compile all binary
# make clean 	# remove all binaries and objects

.PHONY = all clean

CC = gcc
LINKERFLAG = -lm

SRCS := foo.c
BINS := foo

all: foo

foo: foo.o
	@echo "Checking..."
	${CC} ${LINKERFLAG} foo.o -o foo

foo.o: foo.c
	@echo "Creating object..."
	${CC} -c foo.c

clean:
	@echo "Cleaning up..."
	rm -rvf foo.o foo
```

# Specail Syntax
- A semicolon on the line with the target-dependencies is the first line to execute for this rule
  ```
  The commands of a rule consist of shell command lines to be executed one by one. Each command line must start with a tab, except that the first command line may be attached to the target-and-prerequisites line with a semicolon in between.
  ```
  ```makefile
  target: dependencies; recipe
  ```