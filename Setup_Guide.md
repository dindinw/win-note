Windows Dev Enviorment Setup For a Lazy Programmer
==================================================

1. Setup Git
------------
download from http://git-scm.com/download/win
  
  * remove "Windows Explorer integration" option (maybe useful but I dislike it)
  * select "Use Git Bash Only" (a must)
  * select "Checkout windows, commit unix" (a very good feature)

After setup, we got a bash shell with newest git support. It is good but not enough.
pros
  * we got a bash shell. it is easier and samller than Cygwin. (I used before)
cons
  * not gcc installed
  * some tool installed are old than I expected. ex. grep is 2.4.2, which is no `--color` support  

2. Install MingGW
-----------------
download form http://nuwen.net/mingw.html
It is not a orignal distro, but it easy and up_to_date, for a lzay guy like me.
I use the withoug-git one . (only 19.4 MB) the newest gcc 4.7.2 already included
http://nuwen.net/files/mingw/mingw-9.4-without-git.exe

unzip to C:\TOOLS,  (C:\TOOLS is my default installation place for All my dev tools)

3. Integated git bash with MingGW
---------------------------------
It is the insterested part. 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ junction "C:\Program Files\Git\local" "C:\TOOLS\MinGW"

$ gcc --version
gcc.exe (GCC) 4.7.2

$ /bin/grep --version
grep (GNU grep) 2.4.2

$ grep --version
C:\Program Files\Git\local\bin\grep.exe (GNU grep) 2.10

$ which grep
/usr/local/bin/grep
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  * `junction` command from "Sysinternal Suite" (already ship with newer version of Windows)
  * I run command under git bash shell, The bash style path is not work for `junction`, you must use windows style.
  * we can find the 2.10 version of grep is perfered, that is what exactly I want. 


4. Setup Vim 
------------
The git for windows installed a vim version under `/share/vim` folder (`C:\Program Files (x86)\Git\share`), I would like my installed gvim version under windows. So we do the junction tip again.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
cd /share
mv vim vim-msysgit-shipped
junction "C:\Program Files (x86)\Git\share\vim" "C:\Program Files (x86)\Vim"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


