Oracle 11gR2 Installation Guild under Fedora 17
===============================================

Pre Requirement
---------------

### 1. Physical Memory

Using fellowing command to show available memory under install machine.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ grep MemTotal /proc/meminfo
MemTotal:        2973644 kB
$ grep SwapTotal /proc/meminfo
SwapTotal:       5079036 kB
$ free
             total       used       free     shared    buffers     cached
Mem:       2973644    2806496     167148          0      36820    2215076
-/+ buffers/cache:     554600    2419044
Swap:      5079036          4    5079032
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Since we have 3G memory and 5G swap file, the memory requirements for installing Oracle Database 11g Release 2 (11.2):
   * Minimum: 1 GB of RAM
   * Recommended: 2 GB of RAM or more
It looks okay.

11R2 require more share memory, The size of the shared memory must be at least the greater of the MEMORY_MAX_TARGET and MEMORY_TARGET parameters for each Oracle instance on the computer. Check share memory by using fellowing commands. 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ df -h /dev/shm/
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           1.5G  256K  1.5G   1% /dev/shm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 2. Proinstalled Packages

#### 1. binutils

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ rpm -qa|grep binutils
b-2.22.52.0.1-10.fc17.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 2. libstdc

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ rpm -qa|grep compat-libstdc++-33
$ yum install compat-libstdc++-33.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 3. elftutils

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ rpm -qa|grep elfutils-libelf
elfutils-libelf-0.154-2.fc17.i686
$ rpm -qa|grep elfutils-libelf-devel
$ yum list elfutils-libelf-devel*
Loaded plugins: langpacks, presto, refresh-packagekit
Available Packages
elfutils-libelf-devel.i686                 0.154-2.fc17                  updates
elfutils-libelf-devel-static.i686              0.154-2.fc17              updates
$ yum install elfutils-libelf-devel.i686 elfutils-libelf-devel-static.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 4. gcc & glibc

Install gcc
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ yum install gcc
 gcc-4.7.2-2.fc17
 glibc-devel-2.15-57.fc17
 glibc-headers-2.15-57.fc17 
 kernel-headers-3.6.3-1.fc17
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Install gcc-c++
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ yum install gcc-c++ 
 gcc-c++-4.7.2-2.fc17.i686
 libstdc++-devel-4.7.2-2.fc17.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Checking glibc installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ rpm -qa |grep ^glibc-*
glibc-headers-2.15-57.fc17.i686
glibc-common-2.15-57.fc17.i686
glibc-2.15-57.fc17.i686
glibc-devel-2.15-57.fc17.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 
#### 5. K shell

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ yum install ksh
$ rpm -qa |grep ^ksh*
ksh-20120801-3.fc17.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 6. libaio devel 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ yum install libaio-devel
$ rpm -qa |grep ^libaio-*
libaio-0.3.109-5.fc17.i686
libaio-devel-0.3.109-5.fc17.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 8. make

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ rpm -qa |grep ^make-3*
make-3.82-13.fc17.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 9. sysstat

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ yum install sysstat
$ rpm -qa |grep ^sysstat*
sysstat-10.0.3-2.fc17.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 10. numa library 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ yum install numactl-devel
$ rpm -qa|grep numactl
numactl-libs-2.0.7-6.fc17.i686
numactl-devel-2.0.7-6.fc17.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 11. unixODBC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ yum install unixODBC unixODBC-devel
$ rpm -qa|grep unixODBC
unixODBC-devel-2.3.1-1.fc17.i686
unixODBC-2.3.1-1.fc17.i686
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Download
--------
Download 11.2.0.1 from Oracle OTN. Note: 11.2.0.3 require additional access to MOC.

### Links
   * http://download.oracle.com/otn/linux/oracle11g/R2/linux_11gR2_database_1of2.zip
   * http://download.oracle.com/otn/linux/oracle11g/R2/linux_11gR2_database_2of2.zip

### Check sum 
   * 2237015228 1285396902 linux_11gR2_database_1of2.zip
   * 2649514514 995359177 linux_11gR2_database_2of2.zip

### MD5 sum
   * 81e6288078b2b54068959b8df4ae789d  linux_11gR2_database_1of2.zip
   * aa4caca507ca0493444be84d0b11c647  linux_11gR2_database_2of2.zip


Installation Step
-----------------
### 1. Unzip
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ unzip linux_11gR2_database_1of2.zip
$ unzip linux_11gR2_database_2of2.zip
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The folder 'database' shown.

### 2. Fix Hosts file.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ h=$(hostname -A);ip=$(hostname -i); echo -e "$ip\t${h%?}.localdomain\t$h" |sudo tee -a /etc/hosts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The "/etc/hosts" file looks like
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ cat /etc/hosts
127.0.0.1		localhost.localdomain localhost
::1		localhost6.localdomain6 localhost6
192.168.1.169	home3.localdomain	home3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 3. Check&Set linux kenerl paramaters.

#### 1. semmsl, semmns, semopm, and semmni
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/sbin/sysctl -a | grep sem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This command displays the value of the semaphore parameters in the order listed.

#### 2. shmall, shmmax, and shmmni 	
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# /sbin/sysctl -a | grep shm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This command displays the details of the shared memory segment sizes.

#### 3. file-max 	
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# /sbin/sysctl -a | grep file-max
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This command displays the maximum number of file handles.

#### 4. ip_local_port_range 	
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# /sbin/sysctl -a | grep ip_local_port_range
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This command displays a range of port numbers.

#### 5. default rmem and maxi
rmem_default 	
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# /sbin/sysctl -a | grep rmem_default
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
rmem_max 	
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# /sbin/sysctl -a | grep rmem_max
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 6. default wmem and max
wmem_default 	
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# /sbin/sysctl -a | grep wmem_default
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
wmem_max 	
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# /sbin/sysctl -a | grep wmem_max
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 7. check aio-max-nr
aio-max-nr 	
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# /sbin/sysctl -a | grep aio-max-nr
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 8. Edit the /etc/sysctl.conf file
The recommend following setting by Oracle:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
fs.aio-max-nr = 1048576
fs.file-max = 6815744
# kernel.shmall = 2097152
kernel.shmmax = 4294967295
# kernel.shmmni = 4096
kernel.sem = 250 32000 100 128
net.ipv4.ip_local_port_range = 9000 65500
net.core.rmem_default = 262144
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 1048576
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 9. Activate new settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/sbin/sysctl -p
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


### 4. User&Group and Security Settings 

#### 1. Addd new group and user
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
groupadd oinstall
groupadd dba
groupadd oper

useradd -g oinstall -G dba,oper oracle
passwd oracle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


#### 2. Disable 'SELINUX'
NOTE: need a reboot to take effect.
Editing the "/etc/selinux/config" file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SELINUX=disabled
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 3. Config PAM limit

Resource Limits for the "oracle" User (see [oracle doc|http://docs.oracle.com/cd/E11882_01/install.112/e24321/pre_install.htm#autoId49] for details)
Add the following to the "/etc/security/limits.conf" file.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
oracle              soft    nproc   2047
oracle              hard    nproc   16384
oracle              soft    nofile  1024
oracle              hard    nofile  65536
oracle              soft    stack   10240
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add the following to the "/etc/pam.d/login" file.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
session    required     pam_limits.so
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 5. Prepare Required directories
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
mkdir -p /u01/app/oracle/product/11.2.0/db_1
chown -R oracle:oinstall /u01
chmod -R 775 /u01
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 6. Set Xhost
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
xhost +home3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 7. Change "/etc/redhat-release"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
su - 
cat /etc/redhat-release > /etc/redhat-release.fc17
cat /etc/redhat-release|sed -e "s/Fedora release 17 (Beefy Miracle)/redhat release 5/" > /etc/redhat-release.rhe5
mv -f /etc/redhat-release.rhe5 /etc/redhat-release
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 8. Modify ".bash_profile" for oracle user.
note: the $ORACLE_SID may need to customize.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# Oracle Settings
TMP=/tmp; export TMP
TMPDIR=$TMP; export TMPDIR

ORACLE_HOSTNAME=home3.localdomain; export ORACLE_HOSTNAME
ORACLE_UNQNAME=DB11G; export ORACLE_UNQNAME
ORACLE_BASE=/u01/app/oracle; export ORACLE_BASE
ORACLE_HOME=$ORACLE_BASE/product/11.2.0/db_1; export ORACLE_HOME
ORACLE_SID=ora11g; export ORACLE_SID
ORACLE_TERM=xterm; export ORACLE_TERM
PATH=/usr/sbin:$PATH; export PATH
PATH=$ORACLE_HOME/bin:$PATH; export PATH

LD_LIBRARY_PATH=$ORACLE_HOME/lib:/lib:/usr/lib; export LD_LIBRARY_PATH
CLASSPATH=$ORACLE_HOME/JRE:$ORACLE_HOME/jlib:$ORACLE_HOME/rdbms/jlib; export CLASSPATH

if [ $USER = "oracle" ]; then
  if [ $SHELL = "/bin/ksh" ]; then
    ulimit -p 16384
    ulimit -n 65536
  else
    ulimit -u 16384 -n 65536
  fi
fi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 9. Run "./runInstaller"
#### fix emagent error 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ls $ORACLE_HOME/sysman/lib/ins_emagent.mk
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Once the file exists, do:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
cat $ORACLE_HOME/sysman/lib/ins_emagent.mk|sed -e "s/\$(MK_EMAGENT_NMECTL)/\$(MK_EMAGENT_NMECTL) -lnnz11/" >  $ORACLE_HOME/sysman/lib/ins_emagent.mk.tmp
mv -f $ORACLE_HOME/sysman/lib/ins_emagent.mk.tmp $ORACLE_HOME/sysman/lib/ins_emagent.mk
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Post Installation
----------------

### 1. Restore "/etc/redhat-release"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# mv -f /etc/redhat-release.fc17 /etc/redhat-release
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 2. Set Oracle DB Start/Stop automatically

#### Edit the "/etc/oratab" file setting the restart flag for each instance to 'Y'.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ora11g:/u01/app/oracle/product/11.2.0/db_1:Y
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#### 11gR2 update
11gR2 deprecate the dbstart/dbshut script. we need to create script our own.

create "/etc/init.d/dbora" , which is the service control script.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#!/bin/sh
# chkconfig: 345 99 10
# description: Oracle auto start-stop script.
#
# Set ORA_OWNER to the user id of the owner of the 
# Oracle database software.

ORA_OWNER=oracle

case "$1" in
    'start')
        # Start the Oracle databases:
        # The following command assumes that the oracle login 
        # will not prompt the user for any values
        su - $ORA_OWNER -c "/home/oracle/scripts/startup.sh >> /home/oracle/scripts/startup_shutdown.log 2>&1"
        touch /var/lock/subsys/dbora
        ;;
    'stop')
        # Stop the Oracle databases:
        # The following command assumes that the oracle login 
        # will not prompt the user for any values
        su - $ORA_OWNER -c "/home/oracle/scripts/shutdown.sh >> /home/oracle/scripts/startup_shutdown.log 2>&1"
        rm -f /var/lock/subsys/dbora
        ;;
esac
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

set privileges to 750.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
chmod 750 /etc/init.d/dbora
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

add dbora to chkconfig (run levels and auto-start)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
chkconfig --add dbora
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

create "scripts" folder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# mkdir -p /home/oracle/scripts
# chown oracle.oinstall /home/oracle/scripts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

create "/home/oracle/scripts/startup.sh" 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#!/bin/bash

export ORACLE_SID=ora11g
ORAENV_ASK=NO
. oraenv
ORAENV_ASK=YES

# Start Listener
lsnrctl start

# Start Database
sqlplus / as sysdba << EOF
STARTUP;
EXIT;
EOF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

and "/home/oracle/scripts/shutdown.sh"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#!/bin/bash

export ORACLE_SID=ora11g
ORAENV_ASK=NO
. oraenv
ORAENV_ASK=YES

# Stop Database
sqlplus / as sysdba << EOF
SHUTDOWN IMMEDIATE;
EXIT;
EOF

# Stop Listener
lsnrctl stop
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

chmod and ownner
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
chmod u+x /home/oracle/scripts/startup.sh /home/oracle/scripts/shutdown.sh
chown oracle.oinstall /home/oracle/scripts/startup.sh /home/oracle/scripts/shutdown.sh
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Testing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
service dbora stop
service dbora start
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~




