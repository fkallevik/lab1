##Important Instructions

Please preserve the structure of this file, as it will subjected to *partial*
automatic analysis. **Only insert your answers by replacing the text `YOUR ANSWER HERE`; do not delete anything else.** 

Please use [markdown](https://help.github.com/articles/markdown-basics) formating to typeset code and Unix commands with the backtick character, for example, `ls -la`, or if you want to write code blocks, each line should be indented with four spaces, as done in the code below:

    #include <stdio.h>
    
    int main(void) {
    	printf("Hello, world!\n");
    	return 0;
    }


##Exercises from the online Unix tutorial

###Exercise 1a

Make another directory inside the `unixstuff` directory called `backups`

**Answer:** `mkdir unixstuff/backups`

###Exercise 1b

Use the commands `cd`, `ls` and `pwd` to explore the file system.

(Remember, if you get lost, type `cd` by itself to return to your home-directory)

**Answer:** `cd opsys`; `cd labs\lab1`; `ls -a`; `cd ~`; `pwd`

###Exercise 2a

Create a backup of your `science.txt` file by copying it to a file called `science.bak`

**Answer:** `cp science.txt science.bak`

###Exercise 2b

Create a directory called `tempstuff` using `mkdir`, then remove it using the `rmdir` command.

**Answer:** `mkdir tempstuff`; `rmdir tempstuff`

###Exercise 3a

Using the above method, create another file called `list2` containing the following fruit: orange, plum, mango, grapefruit. Read the contents of `list2`.

**Answer:**
`cat > list2`
`orange`
`plum`
`mango`
`grapefruit`
`^D`
`cat list2`

###Exercise 3b

Using pipes, display all lines of `list1` and `list2` containing the letter `p`, and sort the result.

**Answer:** `cat list1 list2 | grep p | sort`

###Exercise 5a

Try changing access permissions on the file `science.txt` and on the directory `backups`.

Use `ls -l` to check that the permissions have changed.

**Answer:**
`chmod 664 science.txt`
`chmod ug=rw backups`
`ls -l`

##Shell questions

1. What option with the command `rm` is required to remove a directory?
  - **Answer:** `rm -r`
1. What is the command used to display the manual pages for any command?
  - **Answer:** `man`
1. What command will show the first 5 lines of an input file?
  - **Answer:** `head -n5 filename`
1. What command can be used to rename a file?
  - **Answer:** `mv`
1. What option can we given to `ls` to show the hidden files?
  - **Answer:** `ls -a`
1. What will the command `cat -n file` do?
  - **Answer:** It will output the contents of the file with line numbers.
1. What will the command `echo -n hello` do?
  - **Answer:** It will output *hello* to the start of the next line
1. What command will display s list of the users who currently logged in in the system?
  - **Answer:** `who`
1. How do you change password on your account?
  - **Answer:** `sudo passwd typeyourpassword`
1. How can you list a file in reverse order?
  - **Answer:** `tac filename`
1. What does the `less` command do?
  - **Answer:** Shows you the contents of a file
1. With `less` how do you navigate?
  - **Answer:** `You can use the up, down, space, enter, j, k, pageup, pagedown and many more. Type `less --help` to display the ways to navigate.
1. What command will display the running processes of the current user?
  - **Answer:** `ps` / `jobs`
1. What command can be used to find the process(es) consuming the most CPU?
  - **Answer:** `top`

##vi questions
1. How do we save a file in `vi` and continue working?
  - **Answer:** Press `Esc` to enter COMMAND mode, and type `:w filename`
1. What command/key is used to start entering text?
  - **Answer:** `i`
1. What are the different modes the editor can be in?
  - **Answer:** COMMAND, INSERT
1. What command can be used to place the cursor at the beginning of line 4?
  - **Answer:** `:4`
1. What will `dd` command do (in command-mode)?
  - **Answer:** Delete the current line
1. How do you undo the most recent changes?
  - **Answer:** By pressing `u` in COMMAND mode
1. How do you move back one word?
  - **Answer:** `b`

##The C Language and Make tool Questions

1. How do you use `gcc` to only produce the `.o` file?  What is the difference between generating only the `.o` file, and building the `hello` executable done in the previous compilation above?
  - **Answer:** Use the -c switch, like so: `gcc hello.c -c` The difference is that this way you don`t execute the *linking step*
1. Give the command for compiling with `debug` enabled instead of normal compilation for the two examples shown in Listing 2 and Listing 3. Explain how to turn debugging on/off for the two cases.
  - **Answer:** The command for compiling with debug enabled for *Listing 2* is `gcc -D DEBUG filename.c -o filename`. 
  If you don`t want debugging enabled for listing 2 just compile without the debug flag. In *Listing 3* you change the debug variable in the source code and recompile the program.
1. Give a brief pros and cons discussion for the two methods to add debug code shown in Listing 2 and Listing 3.
  - **Answer:**
  1. Listing 2
    * Pros
      * You can decide at compile time whether you want the debug code to be included.
      * You don`t have to edit source-code.
    * Cons
      * Can`t enable debugging at application run-time.
  2. Listing 3
    * Pros
      * The application itself can decide to enable the debugging time in run-time.
    * Cons
      * Increases file-size whether the debug code is used or not.
1. Provide the command for generating the *map* file. Which of the `gcc` tools is responsible for producing a *map* file?
  - **Answer:** 'gcc filename.c -Wl,-Map=mapname.map' - The gcc *Linker* is responsible for producing the *map* file.
1. What is the content of each of the sections in a *map* file. Explain briefly.
  - **Answer:** *.data* contains initialized variables, *.rodata* contains constants and *.bss* uninitialized variables
1. Rewrite `hello.c` to produce entries in the *map* file for `.data`, `.bss`, and `.rodata`. Hint: This can be done by adding one variable for each type to the file.
  - **Answer:** 'int a = 0;', 'int b = 2;', 'const int c = 3;' 
1. Add the following function to `hello.c`: `double multiply(double x1, double x2)`, which returns `x1*x2`. Use `gcc` to generate an assembly code listing for the program, and examine the assembly code. What assembly instructions are used to do this? Repeat this task, but now replace `double` with `float`. Explain!
  - **Answer:** 'movsd/mulsd' is used for 64-bit doubles, and 'movss/mulss' for 32-bit floats.
1. How does `make` know if a file must be recompiled?
  - **Answer:** By checking the timestamp for last modification.
1. Provide a `make` command to use a file named `mymakefile` instead of the default `makefile`.
  - **Answer:** 'make -f mymakefile'
1. How do you implement an *include guard*, and why is it needed?
  - **Answer:** 
    '#ifndef TEST_H'
    '#define TEST_H % 
    // CODE GOES HERE
    '#endif'

     *Include guards prevent the compiler from seeing the same content again (multiple inclusion) in the same translation unit*

##Library Task

Insert your code between the brackets `{}`:
```c
#include <stdio.h>
#include <stdlib.h>

double tab_sort_sum( double *tab, int tableSize);

int main(int argc, char *argv[])
{
    double min = 0;
    double max = 100;
    int tableSize;

    if (argc < 2) {
        return 0;
    }

    sscanf(argv[1], "%d", &tableSize);

    if (argc > 2) {
        sscanf(argv[2], "%d", &min);
    }

    if (argc > 3) {
        sscanf(argv[3], "%d", &max);
    }
    int i;
    double tab[tableSize];

    for ( i = 0; i < tableSize; i++ ) {
    tab[i] = min + (rand() % (int)(max - min + 1));
    }

    double sum = tab_sort_sum(tab, tableSize);

    printf("Sum: %.4f\n", sum); 

    for (i = 0; i < tableSize; i++) {
        printf("%f\n", tab[i]);
    }
}

int compareDouble( const void* item1, const void* item2 )
{
	if ( *(double*)item1 < *(double*)item2 ) return -1;
	if ( *(double*)item1 == *(double*)item2 ) return 0;
	if ( *(double*)item1 > *(double*)item2 ) return 1;
}


double tab_sort_sum( double *tab, int tableSize)
{
	int i;
	double sum = 0;

	qsort (tab, tableSize, sizeof(double), compareDouble);

	for(i=0;i<tableSize;i++)
		sum=sum+tab[i];
	return sum;
}
```