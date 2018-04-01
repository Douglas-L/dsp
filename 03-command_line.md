# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

> >
* show current working directory path - pwd #print working directory
* creating a directory - mkdir <Directory> 
* deleting a directory - rmdir <Directory>
* creating a file using `touch` command - touch <file>
* deleting a file - rm <file>
* renaming a file - mv <source> <newname>
* listing hidden files ls -a
* copying a file from one directory to another - cp <source> <destination>
* look up manual for command - man <command>
* concatenate - join files but can also use to view files - cat <file>

---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`  

> >
1. 'ls' lists a directory's contents
2. 'ls -a' lists a directory's contents, including hidden entries.
3. 'ls -l' uses a long listing format, giving additional information on permissions, time modified, owners, etc.
4. 'ls -lh' prints the list with  human readable file sizes.
5. 'ls -lah' is like -a, but in long listing format with human readable sizes.
6. 'ls -t' sorts the list by modification time, newest first.
7. 'ls -Glp' is like -l but with the group names omitted, and a / indicator is appended to directories.

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

> >
1. 'ls -r' lists files in reverse order.
2. 'ls -R' displays subdirectories as well.
3. 'ls -d' displays only directories.
4. 'ls -1' displays each entry on a line.
5. 'ls -m' displays files by file timestamp. comma-separated list.

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

> > xargs takes an input list and runs a command for every item in the list. 
 For example, to remove the .md suffix from all of the markdown files in dsp, i can use **basename -s .md -a *.md | xargs -n1 -i mv {}.md {}**. The basename command generates a list of strings of the file names without the .md suffix. This is then fed into the xargs command, which applies the mv command to each argument in the list of strings.  


