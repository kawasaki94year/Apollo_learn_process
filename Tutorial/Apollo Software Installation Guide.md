# 一、Apollo Software Installation Guide
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
## 3.Start Apollo Development Docker Container
```
cd ${APOLLO_ROOT_DIR}
bash docker/scripts/dev_start.sh
```
If successful, you will see the following messages at the bottom of your screen:
```
[ OK ] Congratulations! You have successfully finished setting up Apollo Dev Environment.
[ OK ] To login into the newly created apollo_dev_michael container, please run the following command:
[ OK ]   bash docker/scripts/dev_into.sh
[ OK ] Enjoy!
```
## 4.Enter Apollo Development Docker Container
```
bash docker/scripts/dev_into.sh
```
## 5.Build Apollo inside Container
```
./apollo.sh build
```
or
```
./apollo.sh build_opt
```

# 二、Installation Problem
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
## 3.Server terminated abruptly (error code: 14, error message: 'Socket closed', log file: '/apollo/.cache/bazel/540135163923dd7d5820f3ee4b306b32/server/jvm.out')
modify apollo/scripts/apollo_base.sh Line 755 and 758:
```
Line 755:#job_args="--copt=-mavx2 --host_copt=-mavx2 --jobs=${count} --local_ram_resources=HOST_RAM*0.7"
Line 756:job_args="--copt=-mavx2 --host_copt=-mavx2 --jobs=2 --local_ram_resources=HOST_RAM*0.5"
```
```
Line 758:#job_args="--copt=-march=native --host_copt=-march=native --jobs=${count} --local_ram_resources=HOST_RAM*0.7  --copt=-fPIC --host_copt=-fPIC"
Line 759:job_args="--copt=-march=native --host_copt=-march=native --jobs=2 --local_ram_resources=HOST_RAM*0.5  --copt=-fPIC --host_copt=-fPIC"
```
