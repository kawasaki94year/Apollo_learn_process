# 一、Delet docker group
## 1.Stop Docker server
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
