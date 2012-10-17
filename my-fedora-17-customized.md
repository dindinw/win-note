
Fix vbox guest addition install
-------------------------------
fedora do not install the linux kernal header by default, it required by compiling the virtual box guest addition.

~~~~~~~~~~~~~~~~~~~~
$ su -
# yum install gcc 
# yum install kernal-devel-3.3.4-5.fc17.x86_64
~~~~~~~~~~~~~~~~~~~~

Git
---

### Installation

Show fedora 17 shipped git version

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ yum info git
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

version 1.7.11.7. i think it's ok.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ yum install git
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### Setup Git env

set up name and email
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ git config --global user.name "Alex Wu"
$ git config --global user.email wuyiding@gmail.com
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

set up ssh-key when connect to GitHub 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ cd ~/.ssh
$ ssh-keygen -t rsa -C "wuyiding@gmail.com"
$ cat id_rsa.pub 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Setup auto-completion and color
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ git config --global color.ui true
$ source /etc/bash_completion.d/git
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Colorize the bash prompt (you may wan to add it to .bash_rc )
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ export GIT_EDITOR=vim
$ export GIT_PS1_SHOWDIRTYSTATE=true
$ export GIT_PS1_SHOWUNTRACKEDFILES=true
$ PS1='\u@\h:\w$(__git_ps1 " [\[\e[0;32m\]%s\[\e[0m\]]")\$ '
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

