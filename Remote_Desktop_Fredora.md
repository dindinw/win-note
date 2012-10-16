Setup sshd for console login
----------------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
[alex@fedora17-vm ~]$ su -
Password: 
[root@fedora17-vm ~]# service sshd restart
Redirecting to /bin/systemctl  restart sshd.service
[root@fedora17-vm ~]# iptables -I INPUT -p tcp --dport ssh -j ACCEPT

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Install vnc server
------------------
refs:
  * http://home.roadrunner.com/~computertaijutsu/rhvnc.html
  * http://www.server-world.info/en/note?os=Fedora_17&p=x&f=2
  * http://fedorasolved.org/Members/zdenek/tigervnc-server

NOTE: (Important!)
  SSH access is needed. Ensure the remote system with VNC server has allowed SSH services in its firewall. If you want to connect from internet to your VNC server that is behind the firewall of your local network, set up proper port forwarding of SSH port to VNC server so all incoming SSH requests are routed from internet to your VNC server.

1. Install VNC Server

~~~~~~~~~~~~~~~~~~~~~~
# yum -y install tigervnc-server
cp /etc/sysconfig/vncservers /etc/sysconfig/vncservers.backup  (obsolated, the vncservers file replaed by)
# THIS FILE HAS BEEN REPLACED BY /lib/systemd/system/vncserver@.service

# exit
# vncserver 



