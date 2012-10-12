Install I wanted
----------------

1. vim
The default vim has no xterm-clip support. instead to install the vim-gtk.

	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
	$ sudo apt-get install vim-gtk
	$ vim --version|grep xterm
	$ sudo apt-get install ctags
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2. Gnomo Session fallback
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
	$ sudo apt-get install gnome-session-fallback  
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

3. Synaptic Software manager
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
	$ sudo apt-get install synaptic
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

4. Video dirvers 
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
	$ sudo apt-get install ubuntu-restricted-extras
	~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Remove Disliked feature
-----------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ sudo apt-get autoremove appmenu-gtk appmenu-gtk3 appmenu-qt

# overlay scollbar

$ sudo apt-get remove liboverlay-scrollbar3-0.2-0

# ubuntuone
$ sudo apt-get purge ubuntuone-client* python-ubuntuone-storage*
$ sudo apt-get purge ubuntuone*
$ sudo apt-get remove --purge ubuntuone-client

# software centre
$ sudo apt-get remove software-center
$ sudo apt-get autoremove software-center
$ sudo apt-get purge software-center

# remove gnome docs
$ sudo apt-get purge gnome-user-guide

# thunderbird
$ sudo apt-get purge thunderbird
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Other Clean UP
--------------

1. show what big

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ dpkg-query -Wf '${Installed-Size}\t${Package}\n'|sort -n
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2. remove unused linux images

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ uname -r
$ dpkg --list | grep linux-image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bug fix
-------

1. Gnome panel
(from http://ubuntuforums.org/showthread.php?t=1987735)

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ sudo sed -i'.old' -e's/StartupNotify=true/StartupNotify=false/' /usr/share/applications/nautilus.desktop 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Look likes
-----------

UI theme

go to 'system-settings'->'Appearance'->'Theme'->select 'Radiance' (I perfer bright than dark :-)

My terminal format 

  * font 
   Edit -> Profile Perferences -> unselect 'use the system fixed width font' -> select 'Ubuntu Mono 12' (I used to it since 10.04)

  * ls time format
    $ echo "export TIME_STYLE=long-iso" >> ~/.bashrc



Dev Env
-------

1. Git

The 12.04 has not git shipped, the version found by apt-cache is 1.7.9.5

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ apt-cache show ^git-all|grep Version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Which is a bit litter older than i expected, I may need to build newest by myself. but first we need to install it anyway.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ sudo apt-get install git-core
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Connect with GitHub 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# set up global
$ git config --global user.name "Alex Wu"
$ git config --global user.email wuyiding@gmail.com
	
# ssh
$ cd ~/.ssh
$ ssh-keygen -t rsa -C "wuyiding@gmail.com"
$ cat id_rsa.pub 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Setup auto-completion and color

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ sudo apt-get install bash-completion # not need, already installed by default under ubuntu, you may need to restart a shell to let it work.
$ git config --global color.ui true
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Colorize the bash prompt (you may wan to add it to .bash_rc )

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ export GIT_EDITOR=vim
$ export GIT_PS1_SHOWDIRTYSTATE=true
$ export GIT_PS1_SHOWUNTRACKEDFILES=true
$ PS1='\u@\h:\w$(__git_ps1 " [\[\e[0;32m\]%s\[\e[0m\]]")\$ '
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

3. .vimrc

4. .bashrc
   

