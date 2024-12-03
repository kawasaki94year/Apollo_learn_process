# 一、Delet docker group
## <font size="1"> 1.Stop Docker server</font>
```
sudo systemctl stop docker
```
## 2.Delet docker group
```
sudo groupdel docker
```
## 3.Delet docker user(If you have not user,It can't delet)
```
sudo gpasswd -d <username> docker
```
## 4.restart Docker server
```
sudo systemctl start docker
```
## 5.Verify Docker user whether delet 
```
grep docker /etc/group
```
# 二、Docker group
## 1. Creat Docker group
```
sudo groupadd docker
```
## 2.Add the user to the Docker group
```
sudo usermod -aG docker $USER
```
## 3.Re-login or reload user groups
```
newgrp docker
```
## 4.Verify the settings
```
groups XuWanLun
```
