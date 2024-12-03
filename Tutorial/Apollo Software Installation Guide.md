# Apollo Software Installation Guide
## 1.Run the following commands to clone Apollo's GitHub Repo(there are two ways):  

(1) using SSH        
```
git clone git@github.com:ApolloAuto/apollo.git  
```
(2) using HTTPS       
```
git clone https://github.com/ApolloAuto/apollo.git 
```
## 2.checkout the latest branch:  
```
cd apollo    
git checkout master
```
# Installation Problem
## 1.`To run a command as administrator (user "root"), use "sudo <command>".See "man sudo_root" for details.` 
when you occupied the warning that use this command `bash docker/scripts/dev_into.sh`,you need input the follow command on container terminal
```
touch ~/.sudo_as_admin_successful
```
## 2.`sudo: /usr/bin/sudo must be owned by uid 0 and have the setuid bit set`
If you use the command `./apollo build` had the error,you should   
1)Enter the docker container as root:
```
docker exec -u root -it <container_name> bash  
```
2)then run the follow commands:
```
ls -l  /usr/bin/sudo
chown root:root /usr/bin/sudo
chmod 4755 /usr/bin/sudo
```
3) run `./apollo.sh build` again it shows
```
sudo: error in /etc/sudo.conf, line 0 while loading plugin "sudoers_policy"
sudo: /usr/lib/sudo/sudoers.so must be owned by uid 0
sudo: fatal error, unable to load plugins
```
you need 
```
chmod 644 /usr/lib/sudo/sudoers.so
chown -R root /usr/lib/sudo
chown root:root /etc/sudoers
chown root:root /etc/sudoers.d/
chown root:root /var/lib/sudo/
chown root:root /etc/sudoers.d/README
```
