.. codeauthor:: apallier

=============
Cobbler usage
=============

.. warning::

   If you are not familiar with the Cobbler terminology, we strongly advise you to read the :ref:`glossary <glossary>` :)

General usage
-------------

When you create a new "system", Cobbler makes the following operations:

   * Reads the :term:`profile` used by the :term:`system` to create the installation ISO.
     The distribution (:term:`distro`) is defined in the profile.
   * Generates the :term:`kickstart`.
     The kickstart template is defined in the profile.
     The template is instantiate with the "profile" and the "system" informations.
   * The kickstart template may refer to several :term:`snippets <snippet>`.

How to view/modify a profile?
-----------------------------

#. Go to Cobbler
#. Open the "profiles" view:

   .. image:: images/cobbler_profiles_view.png

#. Choose a profile:

#. Edit the profile:

The "virtualization" tab allows to set hardware resources:

   .. image:: images/cobbler_profiles_virtualization.png
   
It may be used with `Koan <http://cobbler.github.io/manuals/2.6.0/6/3_-_Installing-virtual-guests.html>_` to deploy virtual machine.


How to view/modify the kickstart?
---------------------------------

#. Go to Cobbler
#. Open the "Kickstart Templates" view:

   .. image:: images/cobbler_kickstarts_view.png

#. Choose the kickstart
#. Edit the kickstart:

   .. image:: images/cobbler_kickstarts_edit.png
   

How to view/modify a snippet?
-----------------------------

#. Go to Cobbler
#. Open the "Snippets" view:

   .. image:: images/cobbler_snippets_view.png

#. Choose a snippet ``partitioning.conf``
#. Edit the snippet:

   .. image:: images/cobbler_snippets_edit.png


.. _glossary: 

Glossary
--------

.. glossary:: 
   :sorted:

   profile
      A profile contains all configurations of the infrastructure and the platform (:term:`distro`, CPU, RAM, Disk...).
      It's like a model/template that can be refered by a :term:`system`.
            
   system
      According the Cobbler terminology, a "system" contains the configuration of a particular machine.
      In other terms, it is an instance of a :term:`profile`. For example, it contains specific network informations of a machine (IP, gateway, hostname...)

   distro
      According to the Cobbler terminology, a "distro" is the configuration of an operating system. Ex: RHEL 6.5, Centos 7.2
   
   kickstart
      A file containing the answers to all the questions that would normally be asked during a typical OS installation (RHEL Linux type).
      Kickstart provides a way for users to automate any OS installation.
      
   snippet
      Snippets are a way of reusing common blocks of code between kickstarts. Its may be seen as function/macro. A snippet is saved in a separate file.
         