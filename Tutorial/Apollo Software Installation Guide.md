# Apollo Software Installation Guide
1) Run the following commands to clone Apollo's GitHub Repo(there are two ways):  

(1) using SSH        
```
git clone git@github.com:ApolloAuto/apollo.git  
```
(2) using HTTPS       
```
git clone https://github.com/ApolloAuto/apollo.git 
```
2) checkout the latest branch:  
```
cd apollo    
git checkout master
```
# Installation Problem
## 1.If you run the command `bash docker/scripts/dev_into.sh` and it shows 
```
To run a command as administrator (user "root"), use "sudo <command>".See "man sudo_root" for details.
```
you need 
```
touch ~/.sudo_as_admin_successful
```
