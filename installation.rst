.. codeauthor:: apallier

=======================================
Cobbler Installation on Centos/Redhat 7
=======================================

:Cobbler version: 2.6.0
:Linux version: Centos/Redhat 7.0

.. note:: 

   Official installation doc:  `<http://cobbler.github.io/manuals/2.6.0/2/2/2_-_RHEL_and_CentOS.html>`_  

Steps
-----

.. highlight:: shell

#. Set SELinux to "permissive" mode (`Doc <http://www.crypt.gen.nz/selinux/disable_selinux.html#DIS3>`_)

#. EPEL repo configuration: ::

      sudo rpm -Uvh http://mir01.syntis.net/epel//7/x86_64/e/epel-release-7-5.noarch.rpm      

#. Installation ::
    
      yum install pykickstart cobbler cobbler-web

#. Activate TFTP ::

      vim /etc/xinetd.d/tftp
      #   disable = yes                    <- Change this line to "no"
      chkconfig tftp on

   .. note:: 
         
      Configuration may be different according to Linux breed

#. Configure the firewall: ::
 
      # For TFTP:
      firewall-cmd --direct --permanent --add-rule ipv4 filter INPUT 0 -p tcp --dport 69 -j ACCEPT
      firewall-cmd --direct --permanent --add-rule ipv4 filter INPUT 0 -p udp --dport 69 -j ACCEPT
      # For HTTP
      firewall-cmd --direct --permanent --add-rule ipv4 filter INPUT 0 -p tcp --dport 80 -j ACCEPT
      firewall-cmd --direct --permanent --add-rule ipv4 filter INPUT 0 -p tcp --dport 443 -j ACCEPT
      # For Cobbler XML-RPC
      firewall-cmd --direct --permanent --add-rule ipv4 filter INPUT 0 -p tcp --dport 25150 -j ACCEPT
      firewall-cmd --direct --permanent --add-rule ipv4 filter INPUT 0 -p tcp --dport 25151 -j ACCEPT
      
      firewall-cmd --reload
      
   .. note::
   
      If you want to check these rules are correctly saved: ::
      
          firewall-cmd --permanent --direct --get-rules ipv4 filter INPUT

#. (optional) If you want to use command "cobbler replicate", you have to configure ``rsync`` ::
   
      $ vi /etc/xinetd.d/rsync
      
      # default: off
      # description: The rsync server is a good addition to an ftp server, as it \
      #      allows crc checksumming etc.
      service rsync
      {
         disable= no # change
         flags= IPv6
         socket_type= stream
         wait= no
         user= root
         server= /usr/bin/rsync
         server_args= --daemon
         log_on_failure+= USERID
      }

      $ chkconfig rsync on
      
   .. note::
   
      Help here: http://www.server-world.info/en/note?os=CentOS_6&p=rsync
         
  
#. Cobbler configuration: ::
   
      vim /etc/cobbler/settings
    
   Change following lines: ::
      
      # manage_rsync: 0   <---- set to 1 to enable Cobbler's RSYNC management features.
      # server: 127.0.0.1 <---- set to the real Cobbler ip address.
      # anamon_enabled: 0 <---- set to 1 to enable Anamon log.
      # next_server: 127.0.0.1 <---- set to the real Cobbler ip address.
      
#. Start Cobbler service: ::

      service cobblerd start
      chkconfig cobblerd on
      
      service httpd start
      chkconfig httpd on

#. Download loaders: ::

      cobbler get-loaders
     
#. (optional) If you want to change the WEB interface password (cobbler/cobbler): ::
      
      openssl passwd -1 -salt 'random-phrase-here' 'your-password-here'
      
   And put the key in /etc/cobbler/settings: ::
   
      # default_password_crypted: "$1$company$prqgnhJ6izx5.S9FVItCB/"
      
   Then change the web user interface setting: ::
   
      htdigest /etc/cobbler/users.digest "Cobbler" cobbler

#. Sync all: ::
   
      cobbler sync       

.. note::

   You can check your installation with: ::
      
      cobbler check
