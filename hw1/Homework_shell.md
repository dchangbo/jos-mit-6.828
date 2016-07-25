<html>
<head>
<title>Homework: shell</title>
<link rel="stylesheet" href="homework.css" type="text/css" />
</head>
<body>

# Homework: shell

<p>This assignment will make you more familiar with the Unix system call
interface and the shell by implementing several features in a small shell, which
we will refer to as the 6.828 shell.  You can do this assignment on any
operating system that supports the Unix API (a Linux Athena machine, your laptop
with Linux or MacOS, etc.).  Submit your 6.828 shell to the [submission web site](https://ccutler.scripts.mit.edu/6.828/handin.py/)
as a text file with the name "hwN.c", where N is the homework number as listed
on the schedule.

<p>Read Chapter 0 of the [xv6 book](../xv6/book-rev8.pdf).

<p>If you are not familiar with what a shell does, do the [Unix
hands-on](http://web.mit.edu/6.033/www/assignments/handson-unix.html) from 6.033.

<p>Download the [6.828 shell](sh.c), and look it
over. The 6.828 shell contains two main parts: parsing shell commands and
implementing them. The parser recognizes only simple shell commands such as the
following:

<pre>
ls > y
cat < y | sort | uniq | wc > y1
cat y1
rm y1
ls |  sort | uniq | wc
rm y
</pre>
Cut and paste these commands into a file <tt>t.sh</tt>

<p>To compile <tt>sh.c</tt>, you need a C compiler, such as gcc.  On Athena, you
can type:
<pre>
$ add gnu
</pre>
to make gcc available.
If you are using your own computer, you may have to install gcc.

<p>Once you have a gcc, you can compile the skeleton shell as follows:
<pre>
$ gcc sh.c
</pre>
which produce an <tt>a.out</tt> file, which you can run:
<pre>
$ ./a.out < t.sh
</pre>
This execution will print error messages because you have not implemented several features. In
the rest of this assignment you will implement those features.

## Executing simple commands

<p>Implement simple commands, such as:
<pre>
$ ls
</pre>

<p> The parser already builds an <tt>execcmd</tt> for you, so the only code you
have to write is for the ' ' case in <tt>runcmd</tt>. You might find it useful
to look at the manual page for exec; type "man 3 exec", and read about
<tt>execv</tt>.  Print an error message when exec fails.

<p>To test your program, compile and run the resulting a.out:
<pre>
6.828$./a.out
</pre>

This prints a prompt and waits for input.  <tt>sh.c</tt> prints as prompt
<tt>6.828$</tt> so that you don't get confused with your computer's shell.

Now type to your shell:
<pre>
6.828$ ls
</pre>

<p>Your shell should print an error message (unless there is a program named
<tt>ls</tt> in your working directory).  Now type to your shell:

<pre>
6.828$ /bin/ls
</pre>

<p>This should execute the program <tt>/bin/ls</tt>, which should print out the
file names in your working directory.  You can stop the 6.828 shell by tying
ctrl-d, which should put you back in your computer's shell.

<p>You may want to change the 6.828 shell to always try <tt>/bin</tt>, if the program
doesn't exist in the current working directory, so that below you don't have to
type "/bin" for each program.  If you are ambitious you can implement support
for a <tt>PATH</tt> variable.

## I/O redirection

<p>Implement I/O redirection commands so that you can run:
<pre>echo "6.828 is cool" > x.txt
cat < x.txt
</pre>

<p>The parser already recognizes ">" and "<", and builds a <tt>redircmd</tt> for
you, so your job is just filling out the missing code in <tt>runcmd</tt> for
those symbols. You might find the man pages for open and close useful

<p>Make sure you print an error message if one of the system calls you are using fails.

<p>Make sure your implementation runs correctly with the above test input.  A
common error is to forget to specify the permission with which the file must be
created (i.e., the 3rd argument to open).

## Implement pipes

<p>Implement pipes so that you can run command pipelines such as:
<pre>
$ ls | sort | uniq | wc
</pre>

<p>The parser already recognizes "|", and builds a <tt>pipecmd</tt> for you, so
the only code you must write is for the '|' case in <tt>runcmd</tt>.  You might
find the man pages for pipe, fork, close, and dup useful.

<p>Test that you can run the above pipeline. The <tt>sort</tt> program may be in
the directory <tt>/usr/bin/</tt> and in that case you can type the absolute
pathname <tt>/usr/bin/sort</tt> to run sort.  (In your computer's shell you can
type <tt>which sort</tt> to find out which directory in the shell's search path
has an executable named "sort".)

<p>Now you should be able the following command correctly:
<pre>
6.828$ a.out < t.sh
</pre>

<p>Make sure you use the right absolute pathnames for the programs.

<p>Don't forget to submit your solution to the [submission web site](https://ccutler.scripts.mit.edu/6.828/handin.py/), with or without
challenge solutions.

## Challenge exercises

<p>You can add any feature of your choice to your shell.  But, you may want consider
the following as a start:

All of these require making changing to the parser and the <tt>runcmd</tt>
function.

</body>
</html>