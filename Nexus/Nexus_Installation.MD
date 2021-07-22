# Nexus Installation
Nexus is one a artifact repository which helps to store your build outcomes.  

### Follow this article in **[Youtube](https://www.youtube.com/watch?v=83AGz9huJGo)
### Prerequisites

1. EC2 instance with java 
```sh
# sudo yum search java | grep -i openjdk
# sudo yum install -y java-1.8.0-openjdk 
# sudo java -version
```
2. Adjust security group to allow traffice to port 8081/tcp which is the default port for nexus

### Implementation steps 

Download and setup nexus stable version
```sh 
cd /opt
wget https://sonatype-download.global.ssl.fastly.net/nexus/3/nexus-3.0.2-02-unix.tar.gz
tar -zxvf  nexus-3.0.2-02-unix.tar.gz
mv /opt/nexus-3.0.2-02 /opt/nexus

#for latest version you can download it from https://download.sonatype.com/nexus/3/latest-unix.tar.gz
```

As a good security practice, it is not advised to run nexus service as root. so create new user called nexus and grant sudo access to manage nexus services 
```sh 
sudo adduser nexus
sudo passwd nexus
# visudo \\ nexus   ALL=(ALL)       NOPASSWD: ALL
sudo chown -R nexus:nexus /opt/nexus
```

Open /opt/nexus/bin/nexus.rc file, uncomment run_as_user parameter and set it as following.
```sh 
vi /opt/nexus/bin/nexus.rc
run_as_user="nexus" (file shold have only this line)
```

Add nexus as a service at boot time
```sh
sudo ln -s /opt/nexus/bin/nexus /etc/init.d/nexus
#Run as a service help : https://help.sonatype.com/repomanager3/installation/run-as-a-service
```
Login as a nexus user and start service
```sh
su - nexus
service nexus start
```

Login nexus server from browser on port 8081

http://<Nexus_server>:8081

Use default credentials to login 

username : admin  
password : admin123

latest version on nexus shall have a default username : admin and default password in that directory cat /opt/sonatype-work/nexus3/admin.password


### Troubleshooting

service is not starting?
 - make sure you are trying to start service with nexus user. 
- check java installation

Unable to access nexus URL?
- make sure port 8081 is opened in security group. 

### Next Steps
- [x] [Configure Users & Groups in Jenkins](https://youtu.be/jZOqcB32dYM)
- [x] [Secure your Jenkins Server](https://youtu.be/19FmJumnkDc)
- [x] [Jenkins Plugin Installation](https://youtu.be/p_PqPBbjaZ4)
- [x] [Jenkins Master-Slave Configuration](https://youtu.be/hwrYURP4O2k)
