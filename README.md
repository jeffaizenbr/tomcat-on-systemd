# tomcat-on-systemd

```bash
[Unit]
Description=Apache Tomcat Web Application Container
After=syslog.target network.target

[Service]
Restart=always
Type=forking
RemainAfterExit=yes

Environment="JAVA_HOME=/usr/lib/jvm/java-1.8.0"
Environment="CATALINA_PID=/opt/tomcat/temp/tomcat.pid"
Environment="CATALINA_HOME=/opt/tomcat"
Environment="CATALINE_BASE=/opt/tomcat"
Environment="CATALINA_TMPDIR=/opt/tomcat/temp"
Environment="CLASSPATH=/opt/tomcat/bin/bootstrap.jar:/opt/tomcat/bin/tomcat-juli.jar"
Environment="JAVA_OPTS=-Xmx28672m -Xms16384m -server -XX:+UseConcMarkSweepGC -XX:+UseParNewGC -XX:SurvivorRatio=20 -XX:+CMSParallelRemarkEnabled -Xrs"

#Environment="JAVA_OPTS=-Xmx28672m -Xms16384m -server -XX:+UseConcMarkSweepGC -XX:+UseParNewGC -XX:SurvivorRatio=20 -XX:+CMSParallelRemarkEnabled -Xrs"

ExecStart="/opt/tomcat/bin/startup.sh"
ExecStop="/opt/tomcat/bin/shutdown.sh"

User=root
Group=root

[Install]
WantedBy=multi-user.target
```


download tomcat
```bash
wget https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.96/bin/apache-tomcat-8.5.96.tar.gz
```


```bash
sudo mkdir /usr/local/tomcat
```



```bash
sudo ln -s /usr/local/tomcat/apache-tomcat-9.0.33 /usr/local/tomcat/tomcat
```


```bash
sudo useradd -r tomcat
sudo chown -R tomcat:tomcat /usr/local/tomcat

```


```bash
[Unit]
Description=Tomcat Server
After=syslog.target network.target

[Service]
Type=forking
User=tomcat
Group=tomcat

Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment='JAVA_OPTS=-Djava.awt.headless=true'
Environment=CATALINA_HOME=/usr/local/tomcat
Environment=CATALINA_BASE=/usr/local/tomcat
Environment=CATALINA_PID=/usr/local/tomcat/temp/tomcat.pid
Environment='CATALINA_OPTS=-Xms512M -Xmx1024M'
ExecStart=/usr/local/tomcat/bin/catalina.sh start
ExecStop=/usr/local/tomcat/bin/catalina.sh stop

[Install]
WantedBy=multi-user.target
```


```bash
```
