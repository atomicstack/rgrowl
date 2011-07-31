1. install growl (http://growl.info)
2. put growlnotify somewhere in your $PATH (it's in the growl dmg)
3. start up the server: screen -S rgrowl_server -dm $PATH/rgrowl_server
4. add this to your .ssh/config:

Host *
  RemoteForward 12340 localhost:12340

5. scp $PATH/rgrowl $host:bin/
6. ssh box
7. box:~$ sleep 5 && rgrowl hello world
