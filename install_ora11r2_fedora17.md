Oracle 11gR2 Installation Guild under Fedora 17
===============================================

Pre Requirement
---------------

### 1. Memory

Using fellowing command to show avaible memory under install machine.

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
it's okey.

11R2 require more share memory, using fellowing command to check share memory. 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$ df -h /dev/shm/
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           1.5G  256K  1.5G   1% /dev/shm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Downlaod
--------
   * http://download.oracle.com/otn/linux/oracle11g/R2/linux_11gR2_database_1of2.zip
   * http://download.oracle.com/otn/linux/oracle11g/R2/linux_11gR2_database_2of2.zip

Installation Step
-----------------


