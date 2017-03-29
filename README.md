# GIT and BASH Scripting
## BASH Scripting (Maxwell)
A script for a movie or play contains information for actors, such as dialogue or stage directions. Similarly, a BASH script contains a list of commands for a UNIX computer to execute. BASH scripts are used to automate computer tasks by stringing together a list of commands in one script file.
 
Anything that can be typed into a command line, such as the ls or cp commands, can be typed into a BASH script and run as such. It is important to note that BASH scripting is intended for automating tasks, not for programming.
 
BASH stands for Bourne Again SHell. It is central to modern Linux distributions and is the industry standard for Linux command lines. Chances are, if you use a Linux terminal, you are using Bash.
 
BASH scripts consist of two main components, the shebang and the script. The shebang (#!) is a character sequence that indicates the path to the program's interpreter, which runs the script. For BASH scripts, the shebang would look like #!/bin/bash (which is the path to the bash interpreter). Next is the script, or the actual sequence of commands to be run. These can be common Unix commands or installed user programs. BASH scripts are often saved with a .sh extension, but because Linux is an extension-agnostic operating system, any extension will work. A sample BASH script (filename: printHello.sh) can look like this:

~~~~
#Prints hello (this is a code comment, not a shebang)
 
#!/bin/bash
echo Hello World!
~~~~

Then, navigate to the directory where it's saved and type:
'./printHello.sh'

printHello.sh is your saved shell script, and ./ is shorthand that tells the terminal where your script file is. (Alternatively, you can type the entire path to your script, such as: /home/maxwell/printHello.sh)
 
The path to native Linux commands like ls and cp is stored in the $PATH environment variable (hence, why you can type ls and cp in the terminal), but the path to your script isn't in the $PATH variable. Therefore, you have to tell the terminal where your script is.

### When to use (and not to use)
BASH scripting is useful for automating various computer tasks that would be much harder/impossible to do by hand. For instance, if you have to ping every IP address in your subnet, you don't have to/shouldn't ping all 255 IP addresses by hand. Instead, you could write a simple script like such:
~~~~
#!/bin/bash
for i in {1..255}
do
ping "192.168.1.$i"
done
~~~~

But, you shouldn't use BASH scripting when you require cross-platform compatibility or speed. BASH scripting only works on Linux systems with a BASH interpreter and require other system-specific dependencies. BASH also requires more overhead than C++ and therefore runs slower. In those cases, you should write code in C++ or Python.

### Real World Applications
BASH scripting is incredibly useful for system administration, especially in server rooms with lots and lots of computers that run Linux. It's an incredibly easy way to, say, install packages and dependencies. Also, power users can speed up their computer usage by writing BASH scripts for common computer tasks.
 
Linux computers can also schedule tasks (defined by scripts) in the rc.local file. For instance, I have a Raspberry Pi that prints my daily to-do list on a receipt printer. I have a Python program that does this, and I run the Python program in a BASH script. Then, I edited the rc.local file to run the BASH script every day at 3:30 PM (when I get home), so I have a fresh to-do list every day!

### How To Use
All BASH scripts start off with a shebang. This is not only a cool sound effect, but it's a sequence of characters that indicates the location of the BASH compiler. This sequence would look like this on most Unix computers:

'#!/bin/bash'
Comments can be used in BASH scripts, and they are delineated by the hash sign, as shown below:
~~~~ 
# I can write a Shakespearean sonnet in here!
# awesome!
~~~~
BASH supports variables, and BASH doesn't require a type definition (kinda like Python). With BASH, you can set a variable and read the variable. It's important to note that there's different syntax for each operation.

*Setting a variable:
~~~~
a=5 # sets the variable a to 5. NOTE: No spaces!
name="Maxwell Yun" # I'm declaring a string, so I must use single quotes (for literal values) or double quotes (which allow for substitutions)
~~~~ 
*Reading a variable:
'echo $a # prints the value of a'
BASH also lets you read command line arguments, passed in when the script is run. These arguments are treated like read-only variables. To access the command line arguments, read the variable $1 (first command line argument) through $9 (ninth command line argument).
 
Or, you can prompt the user for values using the read command. The 'read' command prompts the user for input and saves the user's input to a variable.
~~~~
#!/bin/bash
echo How much wood could a woodchuck chuck if a woodchuck could chuck wood?
read var
echo A woodchuck can chuck $var tree(s) of wood.
~~~~

BASH supports arithmetic math using the 'let' or the 'expr' commands. With the 'let' command, you must store the result of your arithmetic in a variable. The 'expr' command simply prints the arithmetic or string result.
~~~~
let a=5+4
let "b = 4 * 5" # notice that we've used quotation marks in order to use spaces
echo $a # prints 9
echo $b # prints 20
 
expr 5 + 4 # prints 9
expr "5 + 4" # prints 5 + 4, quotation marks indicate that this is to be interpreted literally
a=$( expr 10 - 3 ) # should set the value of a to 7
~~~~
For more advanced BASH scripts, if, for, and while loops are supported. The if loop takes in a binary condition (e.g. is 5 greater than 4?), and executes code if the condition is true. BASH also supports 'else if' statements if additional conditions are to be evaluated. = and != work similar to other programming languages, but BASH has special keywords to evaluate numbers and files.
~~~~
-gt: Greater than
(($a > $b)): a is greater than b
-lt: Less than
(($a < $b)): a is less than b
-ge: Greater than or equal to
(($a >= $b)): a is greater than or equal to b
-le: Less than or equal to
(($a <= $b)): a is less than or equal to b
-eq: Equal to
-ne: Not equal to
 
-a: Logical and
-o: Logical or
~~~~ 
It's important to note that the = symbol literally compares strings. Thus, it's not used for determining if numbers are equal.
 
To cut to the chase, a sample if statement is here.
~~~~
#!/bin/bash
echo Please input your age here:
read age

if [$age -lt 13] # note that you're reading a variable here. First conditional
then # indicates the code that you'll run if the above condition is true
echo You're in elementary or middle school.
elif [$age -ge 13 -o $age -le 18]
then
echo You're in high school.
elif [$age -gt 18 -o $age -le 23]
then
echo You're in college.
else
echo You're an adult!
fi # indicates the end of the if block
~~~~

While loops are similar in syntax to if statements. They run the code contained while an expression is true. It's important to note that if the expression is always true, then the code will run in an infinite loop, hogging your system resources. A program to print "n bottles of beer on the wall" is listed below:
~~~~
#!/bin/bash
a=100
while [$a -gt 0]
do
echo $a bottles of beer on the wall
let a=a-1
done
~~~~
Please note the a = a - 1 statement in the while loop. The while loop will iterate through the code in the do block as long as its condition is true. a = a - 1 decreases the value of a until a equals zero. When a = 0, then the while loop's condition is no longer true, and the loop stops running.
 
Without a = a - 1, your code will print "100 bottles of beer on the wall" forever or until your computer runs out of resources.
 
For loops iterate through each element in a list or a predefined range and run the contained code for each iteration. An example that prints :99 bottles of beer on the wall" in reverse is here:
~~~~
#!/bin/bash
 
for var in {1..99} # Iterates through the values 1 - 99
do
echo $var bottles of beer on the wall
done
~~~~
I've briefly touched on the basic programming aspects of BASH scripting. When BASH scripting, a knowledge of programming, and Linux commands are joined together, you have quite a formidable set of tools. BASH scripting is used to automate many system tasks. Matter of fact, Linux systems run BASH scripts when booting (/etc/rc.local) in order to start the right services. With BASH, you'll go far.
 
### Efficiency: Depends on what programs/utilities you use inside your BASH script. However, it's important to note that while BASH scripts are convenient, they're much slower, runtime-wise, than a dedicated program.


