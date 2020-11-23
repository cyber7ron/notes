# radare2

**Common r2 flags options** :

`-A` : analyze the binary upon entering the r2 console.

`-d` : enable the debugger

`-w` : open file in write mod

`-` : enter console without opening a file.


**Analyzation**

Generally all analyzation commands start with the letter `a`. If you want to list all possible commands that can be done with your starting letter(s) you add a question mark to the end. For example a? would output ab,aa,ac along with a description on what each command does.

`aaa` : ananlyze everything

`af` : analyze function

`afl` : list of functions

**information**

`i` is a command that shows general information of the binary. Like `a` it has many sub commands each with varying degrees of specificity.

`ia` : show all info about file

`izz` : show every string in binary

`iM` : address main funciton

`j` : if added in end of every cmd , get json output format.

`ie` : get entrypoint of the file

**Navigation**

`s` : print current memory address

`s` `addrs` : go to specific point in memory

`s+ 5` : go 5 bytes forward

`s- 12` : go 12 byte backward

`s-` : undo previous seek

`s main` : go to address of main function

`sr rax` : go to the address of the rax register.

**Printing**

`p` is a command that shows data in a myriad of formats. The command is useful for when you want to get information about what is happening in memory, and get some of the data that's contained in memory as well. 

With the `p` command it is also useful to know about the `@` symbol in radare. The `@` symbol is used to specify that something is an address in memory, for example if you wanted to specify you were talking about the memory address of the main function you would use `<command>@main`


`px` : print hex output of where you currently are in memory.

`pd` : print the diassembly of current memory.

`pd @ main` : disassemble main function.

`pxe` : print emoji hexdump

`pC` : disassemble in column format

`pdf` @functin_name : disaasemble function


**Debugging**

Debug mode allows you to set breakpoints and offers a lot of options to not only navigate through your binary, but to analyze the data that goes in and out of the registers as well.

`db` : set a breakpoint

`dr` : print out values of all registers.

`dc` : run program until it ends or hit next breakpoint.

`ds` : step throught the binary one line at a time.

`ds 2` : go forth 2 lines in binary.

`dbi` : list out indexes and memory addresses of all breakpoints.

**Visual Mode**

allows the assembly to more human readable and provides a lot of options to enhance the visual appeal of radare and can definitely improve efficiency. Therefore I would state it's a valuable tool that you should know how to use. All commands involving visual mode start with `v`

`vV` : enter graph mode

`:` :run normal radare cmd inside visual mode

`q` : go back to the regular radare shell.

`s` : step throught the binary inside visual mode.

`;` : add comment.

**Write Mode**

Occasionally you might end up in a situation where a task is impossible to solve with the current instructions. For example take this code

```c
int val = 4;
if(val ==5){
	printf("%s","You win!");
}

```
You will never be able to get it to print out You win! because under normal circumstances val will never be set equal to 5. This is where write mode comes in, it allows you to change instructions so you can get certain conditions to execute. All commands involving write mode start with `w`

