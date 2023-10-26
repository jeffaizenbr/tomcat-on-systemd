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
