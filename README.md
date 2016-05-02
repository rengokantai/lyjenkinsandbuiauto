#### lyjenkinsandbuiauto
using centos.
#####3
check whether java is installed (here assume we have java7 installed)
```
which java
```

check port
```
cat /etc/services | grep 8080   # web caching service
```
install telnet
```
yum install telnet
telnet localhost 8080
```

using nmap to scan
```
yum install nmap
nmap -sT -O localhost
```
usingnetstat
```
netstat -anp | grep 8080
```
install java8  
[install java8 on centos](www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  
[bypass oracle](http://stackoverflow.com/questions/10268583/downloading-java-jdk-on-linux-via-wget-is-shown-license-page-instead)
```
 wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u73-b02/jdk-8u73-linux-x64.rpm
```
set alternatives
```
alternatives --install /usr/bin/java java /usr/java/latest/bin/java 200000
alternatives --install /usr/bin/javac java /usr/java/latest/bin/javac 200000
alternatives --install /usr/bin/jar jar /usr/java/latest/bin/jar 200000
alternatives --config java
```
set JAVA_HOME
```
cd /etc/rc.d
vim rc.local
```
edit
```
export JAVA_HOME="/usr/java/latest"
```
######4
```
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
sudo rpm --import http://pkg.jenkins-ci.org/redhat-stable/jenkins-ci.org.key
yum update
yum install jenkins
```
start
```
systemctl start jenkins.service
```
######6
configure global security  
enable security(disable remember me)-> Jenkins’ own user database(untick allow users to sign up)( Anyone can do anything) 
sign up-> logged-in users can do anything

######9
manage jenkins->backup manager->verbose mode no shutdown  
thin backup:  example
full backup
```
0 12 * * 1-5
```
diff backup
```
0 12 * * 7
```
######10
manage jenkins->manage nodes  
configure, # of executors=2  
node->new node->#of executors=4  
remote:/home/jenkins  





