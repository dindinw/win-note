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
binutils-2.22.52.0.1-10.fc17.i686
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


