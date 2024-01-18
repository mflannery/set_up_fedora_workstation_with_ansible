# How I set up my fedora workstation servers

I finally got around to creating an ansible playbook that will set up my Fedora workstation servers exactly how I like them.  This works with Fedora 39 and Gnome 45 though I would expect it should work with other recent versions of Fedora as well. Here are the steps for getting a Fedora workstation up and running quickly.  This playbook assumes you have LUKS encrypted your drive and you have a tang server running in your network.  If you haven't done both of these, you either need to do them or comment out the section called "Set up automatic unlock".  

1. Install Fedora workstation onto a PC.
2. Go into settings (click the top right corner of the Gnome desktop and then click on the gear)
3. Choose sharing
4. Turn on Remote Login
5. On another PC, have ansible installed.  In my case I have a Fedora server that I use as my ansible control server.  I installed ansible with `sudo dnf install ansible`.
6. On this other PC, pull down the playbook file and create an inventory.ini file.  If you need help with the inventory file, google it.
7. Edit the playbook.  There are two <CHANGE ME> strings where and 1 <PASSWORD> where you need to put in the LUKS unlock password for your system, put in the correct values for your user.
8. Run this playbook with `ansible-playbook --ask-become-pass -i inventory.ini playbook.yaml`
