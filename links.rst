.. codeauthor:: apallier

===================================================
Useful links for Cobbler installation/configuration
===================================================
 
Installation/Configuration
--------------------------

* Installation on Redhat : `<https://access.redhat.com/documentation/en-US/Red_Hat_Network_Satellite/5.3/html/Reference_Guide/ch-cobbler.html#s2-cobbler-reqs-check>`_

* Update Cobbler : `<http://sappyit.blogspot.fr/2015/03/update-cobbler-server.html>`_

* Managing DHCP: `<http://cobbler.github.io/manuals/2.6.0/3/4/1_-_Managing_DHCP.html>`_

* Importing a distribution: http://docs.fedoraproject.org/en-US/Fedora/13/html/Installation_Guide/sn-cobbler-import.html

* Usage with Subversion:
   * http://consultancy.edvoncken.net/index.php/HOWTO_Set_up_a_Subversion_repository_for_provisioning
   * Keyring: 
      * http://technicalprose.blogspot.fr/2011/06/using-subversion-with-gnome-keyring.html
      * http://kenneho.net/2011/01/30/using-svn-client-and-gnome-keyring-in-ssh-sessions/
      * http://blog.purplecarrot.co.uk/2013/10/subversion-and-gnome-keyring-daemon.html
      * http://unix.stackexchange.com/questions/89550/subversion-svn-doesnt-store-passwords-in-gnome-keyring
      * http://stackoverflow.com/questions/3824513/svn-encrypted-password-store
    
Usage
-----
 
* Kickstart:
   * Doc: `<http://cobbler.github.io/manuals/2.6.0/3/5_-_Kickstart_Templating.html>`_
   * Making the kickstart file available: https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Installation_Guide/s1-kickstart2-putkickstarthere.html
   * Tips and tricks for anaconda and kickstart: http://wiki.centos.org/fr/TipsAndTricks/KickStart

* Trigger:
   * Doc: `<http://cobbler.github.io/manuals/2.6.0/4/4/1_-_Triggers.html>`_
   * Writing a trigger: http://www.ithiriel.com/content/2010/03/29/writing-install-triggers-cobbler

* API:
   * API XMLRPC: https://fedorahosted.org/cobbler/wiki/CobblerXmlrpc
   * API Python: https://fedorahosted.org/cobbler/wiki/CobblerApi
