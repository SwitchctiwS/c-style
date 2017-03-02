#c-style
Personal style guide for myself, becuase I forget it sometimes. Mostly has to do with directory structure.

##Variables, Brackets, Pointers
<ul>
<li>Java style K&R braces with Python style everything else</li>
<li>Pointer goes directly after type when used, but when declared it is attached to the type</li>
<li>`if` statements always have braces</li>
</ul>

###Example
```c
varible_name = 1 + 3 - 8;

int function_name(int* variable_name) {
	int var = *variable_name;

	if (var == -4) {
		foo();
	}

	bar();

	return 0;
}

```

##.c Files
<ul>
<li>Only include is its corresponding `.h` file</li>
<li>No defines</li>
</ul>

##.h Files
<ul>
<li>Has all `.h`includes needed for corresponding `.c` file</li>
<li>Do not include `main.h`</li>
<li><ol>
<li>Includes with anti-recursion provision</li>
<li>Defines</li>
<li>Function prototypes with description, parameters, and return</li>
</ol></li>
</ul>

###Example
```c
// Includes:
#ifndef STDIO_H
	#define STDIO_H
	#include <stdio.h>
#endif

// Defines:
#define PI 3.14159

// Function Prototypes:
/*Foos some bar
Params:
	bar -> help to foo

Returns:
	character that has been foo'd*/
char foo(int bar);
```

##Directories
<ul>
<li>Each "module" goes in separate directory that shares name with `.c` and `.h` files</li>
</ul>

###Example
```
                --- foo.c
                |
                |
                --- foo.h
                |
                | 
rnd ----- foo ----- makefile
      |
      |
      --- bar ----- bar.c
      |         |
      |         |
      |         --- bar.h
      |         |
      |         |
      |         --- makefile
      |
      --- main.c
      |
      |
      --- main.h 
      |
      |
      --- makefile
```

##Makefiles
<ul>
<li>`all` links to different directories with `cd`</li>
</ul>

###Example
For the above directory structure

rnd makefile
```
all:
	gcc -c main.c
	cd foo; make
	cd bar; make
	gcc main.o foo/foo.o bar/bar.o -o rnd.exe

clean:
	rm main.o rnd.exe
	cd foo; make clean
	cd bar; make clean
```

foo makefile
```
all:
	gcc -c foo.c

clean:
	rm foo.o
```

bar makefile
```
all:
	gcc -c bar.c

clean:
	rm bar.o
```
