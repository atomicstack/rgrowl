use these scripts and a bit of ssh wizardry and you can send growl
notifications to your local desktop from a remote console over an
ssh tunnel (or many).

works really well with ProxyCommand and ControlMaster:

http://benno.id.au/blog/2006/06/08/ssh_proxy_command
http://www.anchor.com.au/blog/2010/02/ssh-controlmaster-the-good-the-bad-the-ugly/

configure RemoteForward+ControlMaster everywhere and you can SSH into 
anything, from anything, and continue to use rgrowl without a hitch.

================================================================================
installation
================================================================================

1. install growl (http://growl.info)
2. put growlnotify somewhere in your $PATH (it's in the growl dmg)
3. start up the server on your mac, which accepts incoming notifications
   from your ssh tunnel and feeds them into growl:

   screen -S rgrowl_server -dm $PATH/rgrowl_server

4. add this to your .ssh/config:

   Host *
     RemoteForward 12340 localhost:12340

5. put the rgrowl script onto your remote server:

   scp $PATH/rgrowl $host:bin/

6. ssh in and send a test notification back to your desktop:

   mac:~$ ssh box
   box:~$ sleep 5 && rgrowl hello $USER

7. configure ssh appropriately and even this will work:

   mac:~$ ssh -t gw1 ssh -t gw2 ssh -t gw3 rgrowl HI
