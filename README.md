Download Link: https://assignmentchef.com/product/solved-cs211-project3-maze-solving
<br>
<h1></h1>

For this project, write a C program that will find its way through a maze using the depth-first search algorithm.  This program takes input from a file where the filename is specified in the command line arguments.  The input file will only contain two integer values per line of input:

<ul>

 <li>The first valid line gives the size of the 2-D maze (the number of rows given by the first number, then the number of columns given by the second number), valid values are &gt;= 1</li>

 <li>The second valid line gives the coordinates of the starting position in the maze</li>

 <li>The third valid line gives the coordinates of the ending position in the maze</li>

 <li>The remaining valid lines in the file give the coordinates of blocked positions in the maze</li>

</ul>




If the command line arguments do not contain a valid filename, you should print an error message to STANDARD ERROR and quit the program.  This could be because there was not a name given or the name given did not match that of a valid file.  If the command line arguments contains multiple names, we leave it up to you to come up with a “good solution”.  Ideas on such a “good solution” could be:

<ul>

 <li>Use one of the names as the input file and proceed (pick which name makes most sense to use – i.e. use the first filename given or use the last filename given).</li>

 <li>Give an error message stating that too many names were given and quit.</li>

 <li>Run the program to solve the maze given with each filename.</li>

</ul>




The following shows an example of such an input file.  The coordinates are given with the row listed first and the column listed second.  A maze of NxM has rows numbered from 1 to N and columns number from 1 to M.




10 20

1 1

10 20

5 1

4 2

3 3

<ul>

 <li>10</li>

 <li>9</li>

 <li>8</li>

 <li>7</li>

 <li>6</li>

 <li>5</li>

 <li>4</li>

 <li>3</li>

</ul>







The above input creates the following maze will 11 blocked positions:




size: 10, 20 start: 1, 1 end: 10, 20




**********************

*s……..*……….*

*……..*………..*

*..*….*…………*

*.*….*………….*

**….*…………..*

*….*……………*

*…*…………….*

*..*……………..*

*………………..*

*……………….e*

**********************




The blocked positions and the edges of the above maze are filled in with *’s. The start position is filled in with an ‘s’. The end position in filled in with an ‘e’. The other positions are filled in with periods.




You may assume that the input will always have two integer values per line; however, the values may be out of range.  If an invalid value is given on an input line, print a descriptive error message to STANDARD ERROR, ignore those two input values and continue processing input using the next line of input.  Any value of zero or less is invalid in this program.  For a coordinate value in the maze, valid value range from 1 to the maximum row size or column size.  Also, the starting and ending positions of the maze must never be blocked.  Since errors may exist:

<ul>

 <li>The size of the maze is on the first valid line of input.</li>

 <li>The starting position of the maze is the second valid line of input.</li>

 <li>The ending position of the maze is the third valid line of input.</li>

</ul>




If the file ends before getting 3 valid lines of input, print out an error message to STANDARD ERROR and quit the program.




Input with invalid values is shown below.  The comments on each line are not part of the input, but there to help explain the error.




10 0           =&gt; Invalid: Maze sizes must be greater than 0

15 7           =&gt; Maze becomes size 15 x 7

10 20          =&gt; Invalid: column 20 is outside range from 1 to 7

5 1             =&gt; Starting position is at position 5, 1

24 2           =&gt; Invalid: row 24 is outside of range from 1 to 15

3 3             =&gt; Ending position is at position 3, 3

<ul>

 <li>10      =&gt; Invalid: column 10 is outside range from 1 to 7</li>

 <li>9      =&gt; Invalid: column 9 is outside range from 1 to 7</li>

 <li>8      =&gt; Invalid: column 8 is outside range from 1 to 7</li>

 <li>7</li>

 <li>6</li>

 <li>1      =&gt; Invalid: attempting to block starting position</li>

 <li>5</li>

 <li>4</li>

</ul>

The algorithm you are to use to find a path through the maze is a Depth First Search.  You MUST use the following form Depth First Search.  You are NOT allowed to use a recursive version of the depth first search (since you are required to use your own linked list stack to solve this).




<ul>

 <li>Mark all unblocked positions in the maze as “UNVISITED”</li>

 <li>push the start position’s coordinates on the stack</li>

 <li>mark the start position as “VISITED”</li>

 <li>While (stack is not empty and end has not been found) o if the coordinate at the Top of the Stack is the end position

  <ul>

   <li>then end has been found (break out of loop) o if the coordinate at the Top of the Stack has an unvisited (and unblocked) neighbor</li>

   <li>push the coordinates of one unvisited neighbor on the stack</li>

   <li>mark that one unvisited neighbor as visited o else</li>

   <li>pop the coordinate at the Top of the Stack</li>

  </ul></li>

 <li>If the stack is empty o The maze has no solution</li>

 <li>else o The items on the stack contain the coordinates of the solution from the end of the maze to the start of the maze.</li>

</ul>




When referring to neighbors, those positions will be the ones above, below, left or right of the current position (not diagonal). So for position x,y its neighbors are at:




<ul>

 <li>x+1, y</li>

 <li>x-1, y</li>

 <li>x, y+1</li>

 <li>x, y-1</li>

</ul>




Your program is to first output the size of the maze, the start and ending coordinates and an ASCII drawing of the maze.  The code <strong>maze.c</strong> does this for any maze of size 30X30 or less.  The maze.c program uses a static sized 2-D array; <strong>however, your program MUST use a dynamic 2-D array sized to reflect the maze size given in the input file.</strong>  You must also dynamically deallocate this array at the end of your program.  The maze.c program also does not do any error checking for invalid input, your program MUST check for invalid input.




Once the maze solving algorithm is run, you must then print out a message stating either:

<ul>

 <li>the maze has no solution or</li>

 <li>listing the coordinates of the locations of the path in the maze <strong>from the start of the maze to the end of the maze</strong> that was found by the algorithm. Note this means printing out the contents of the stack in reverse order.</li>

</ul>




The stack MUST use a linked list of coordinate values. <strong>The head of the linked list MUST NOT be global.  It must be declared as a local variable in main( ) or some other function.  </strong>You may create a structure to contain the head of the stack if you desire but again the initial instance of the structure must be a local variable.  The code for each stack operation MUST be done in its own function where the head is passed in as a parameter.  The only exception to this is that the initializing function may return a newly created instance.




You MUST write functions for the following operations (these are the “same” functions as Project 2):

<ul>

 <li>initializing the stack,</li>

 <li>checking if the stack is empty,</li>

 <li>pushing an element onto the stack,</li>

 <li>popping an element off of the stack,</li>

 <li>accessing the top element on the stack, and</li>

 <li>resetting the stack so that it is empty and ready to be used again.</li>

</ul>




These functions must NOT contain memory leaks!  Expect points deducted if your code fails in this regard.  (Valgrind will be used when grading.)




<h1>Command Line Argument: Debug Mode</h1>




Your program must be able to take one optional command line argument, the -d flag. When this flag is given, your program is to run in “debug” mode. When in this mode, your program is to display the coordinates of the maze positions as they are pushed onto the stack and popped off the stack if the Top of Stack coordinate does not have an unvisited (and unblocked) neighbor.  When the flag is not given, this debugging information should not be displayed.




Since the input file for the maze also comes from the command line arguments, you may not assume which order in which the command line arguments are given.  Thus the command line arguments may be given as:

<ul>

 <li>./a.out txt</li>

 <li>./a.out txt  -d</li>

 <li>./a.out -d  txt</li>

</ul>

One simple way to set up a “debugging” mode is to use a boolean variable which is set to true when debugging mode is turned on but false otherwise. Then using a simple if statement controls whether information should be output or not.

if ( debugMode == TRUE )  printf (” Debugging Information 
”);




Optional ways for writing this code can be seen on the course website.

<h2>Coding Style</h2>

Don’t forget to use good coding style when writing your program.  Good coding style makes your program easier to be read by other people as the compiler ignores these parts/differences in your code.  Elements of good code style include (but may not be limited to):

<ul>

 <li>Meaningful variable names</li>

 <li>Use of functions/methods</li>

 <li>Proper indentation</li>

 <li>Use of blank lines between code sections</li>

 <li>In-line comments</li>

 <li>Function/method header comments</li>

 <li>File header comments</li>

</ul>

The Code Review Checklist also hints at other elements of good coding style.