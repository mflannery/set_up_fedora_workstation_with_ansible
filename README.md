# How I set up my fedora workstation servers

I finally got around to creating an ansible playbook that will set up my Fedora workstation servers exactly how I like them.  This works with Fedora 39 and Gnome 45 though I would expect it should work with other recent versions of Fedora as well. Here are the steps for getting a Fedora workstation up and running quickly.  This playbook assumes you have LUKS encrypted your drive and you have a tang server running in your network.  If you haven't done both of these, you either need to do them or comment out the section called "Set up automatic unlock". 

1. Install Fedora workstation onto a PC.
2. Go into settings (click the top right corner of the Gnome desktop and then click on the gear)
3. Choose sharing
4. Turn on Remote Login
5. On another PC, have ansible installed.  In my case I have a Fedora server that I use as my ansible control server.  I installed ansible with `sudo dnf install ansible`.
6. On this Ansible PC, ensure you have the following Ansible roles installed from Ansible Galaxy
   * linux_system_roles
   * jaredhocutt.gnome_extensions
   * community.general
8. On this Ansible PC, pull down the playbook file named genericplaybook.yaml located in this github repository and save it as playbook.yaml.  Next, download the inventory.ini file.
9. Edit the inventory.ini file and replace the IP address in the "workstation" section with the IP address of your new, base Fedora Workstation system.
10. Edit the playbook.  Search for PASSWORD.  <LUKS PASSWORD> is the password to unlock your HDD at boot.  <VNC PASSWORD> is the password you want to use VNC/XRDP.  <USERNAME> is the username of the person running the playbook.  I think these can be variablized but I haven't tried it yet.  DO NOT INCLUDE THE BRACES <> WITH THE PASSWORDS OR USERNAMES BUT LEAVE QUOTES IF THEY ARE THERE.  Save the file.
11. Run this playbook with `ansible-playbook --ask-become-pass -i inventory.ini playbook.yaml`
