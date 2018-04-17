## Despligues en Magnolia :rocket:

#### Revisión del entorno

Para un despliegue normal debemos tener instalado Java, Tomcat y Unzip para descomprimir el WAR. Verificamos el estado:

```console
ubuntu@ip-XX-XX-X-XX:/$ java -version
openjdk version "1.8.0_162"
OpenJDK Runtime Environment (build 1.8.0_162-8u162-b12-0ubuntu0.16.04.2-b12)
OpenJDK 64-Bit Server VM (build 25.162-b12, mixed mode)
ubuntu@ip-XX-XX-X-XX:/$
```

```console
ubuntu@ip-XX-XX-X-XX:/$ sudo systemctl status tomcat8.service
● tomcat8.service - LSB: Start Tomcat.
   Loaded: loaded (/etc/init.d/tomcat8; bad; vendor preset: enabled)
   Active: active (running) since Tue 2018-04-17 12:56:36 CEST; 4h 9min ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 28
   Memory: 69.6M
      CPU: 16.684s
   CGroup: /system.slice/tomcat8.service
           └─20075 /usr/lib/jvm/default-java/bin/java -Djava.util.logging.config.file=/var/lib/tomcat8/conf/logging.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLog

Apr 17 12:56:31 ip-10-19-0-10 systemd[1]: Starting LSB: Start Tomcat....
Apr 17 12:56:31 ip-10-19-0-10 tomcat8[20048]:  * Starting Tomcat servlet engine tomcat8
Apr 17 12:56:36 ip-10-19-0-10 tomcat8[20048]:    ...done.
Apr 17 12:56:36 ip-10-19-0-10 systemd[1]: Started LSB: Start Tomcat..
lines 1-14/14 (END)
```

#### Magnolia :four_leaf_clover:

Revisamos el estado de la carpeta _/opt/magnolia_ y debemos tener en cuenta que el usario debe ser Tomcat:

```console
ubuntu@ip-XX-XX-X-XX:/opt/magnolia$ ls -ltra
total 40
drwxr-xr-x  2 ubuntu ubuntu 6144 Apr 10 15:13 lib
drwxr-xr-x  2 ubuntu ubuntu 6144 Apr 10 15:13 temp
drwxr-xr-x  2 ubuntu ubuntu 6144 Apr 10 15:13 webapp
drwxr-xr-x  2 ubuntu ubuntu 6144 Apr 10 15:13 work
drwxr-xr-x  2 ubuntu ubuntu 6144 Apr 11 15:02 bin
drwxr-x---  2 ubuntu ubuntu 6144 Apr 11 15:04 webapps
drwxr-xr-x 10 ubuntu ubuntu 6144 Apr 11 15:04 .
drwx------  3 ubuntu ubuntu 6144 Apr 11 15:43 conf
drwxr-xr-x  2 ubuntu ubuntu 6144 Apr 17 12:52 logs
drwxr-xr-x  3 root   root   4096 Apr 17 12:53 ..
```
#### Tomcat :smirk_cat:

Revisamos el estado de la carpeta de Tomcat según nuestra versión será _/var/lib/tomcat8_

```console
ubuntu@ip-XX-XX-X-XX:/var/lib/tomcat8$ ls -ltra
total 16
drwxr-xr-x  2 tomcat8 tomcat8 4096 Sep 28  2017 lib
lrwxrwxrwx  1 root    root      19 Sep 28  2017 work -> ../../cache/tomcat8
lrwxrwxrwx  1 root    root      17 Sep 28  2017 logs -> ../../log/tomcat8
lrwxrwxrwx  1 root    root      12 Sep 28  2017 conf -> /etc/tomcat8
drwxr-xr-x 44 root    root    4096 Apr 17 12:56 ..
drwxr-xr-x  4 root    root    4096 Apr 17 12:56 .
drwxrwxr-x  3 tomcat8 tomcat8 4096 Apr 17 12:56 webapps
ubuntu@ip-XX-XX-X-XX:/var/lib/tomcat8$
```

Revisamos la carpeta _webapps_ del Tomcat: En esta estructura podremos tene para la Author una carpeta llamada _magnoliaAuthor_ con un enlace a _/opt/magnolia/webapps/magnolia_ pero también puede tener esta estructura para su correcto funcionamiento tanto en Author como en Public:

```console
ubuntu@ip-XX-XX-X-XX:/var/lib/tomcat8/webapps$ ls -ltra
total 12
drwxr-xr-x 4 root    root    4096 Apr 17 12:56 ..
drwxr-xr-x 3 root    root    4096 Apr 17 12:56 ROOT
drwxrwxr-x 3 tomcat8 tomcat8 4096 Apr 17 12:56
```
#### Context para nuestro RDS :file_folder:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
Licensed to the Apache Software Foundation (ASF) under one
or more
contributor license agreements. See the NOTICE file
distributed with
this work for additional information regarding copyright
ownership.
The ASF licenses this file to You under the Apache License,
Version 2.0
(the "License"); you may not use this file except in
compliance with
the License. You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0
Unless required by applicable law or agreed to in writing,
software
distributed under the License is distributed on an "AS IS"
BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express
or implied.
See the License for the specific language governing
permissions and
limitations under the License.
-->
<!-- The contents of this file will be loaded for each web
application -->
<Context>
<!-- Default set of monitored resources -->
<WatchedResource>WEB-INF/web.xml</WatchedResource>
<!-- Uncomment this to disable session persistence across
Tomcat restarts -->
<!--
<Manager pathname="" />
-->
<!-- Uncomment this to enable Comet connection tacking
(provides events
on session expiration as well as webapp lifecycle)
-->
<!--
<Valve
className="org.apache.catalina.valves.CometConnectionManagerVa
lve" />
-->
<Resource name="jdbc/Magnolia" auth="Container"
url="jdbc:mysql://companydb-pro.c9euvbaddq7b.eu-west-1.rds.amazonaws.com:3306/mag_author"
username="XXXX" password="YYYYY" type="javax.sql.DataSource" driverClassName="com.mysql.jdbc.Driver"
maxTotal="200" maxIdle="50" minIdle="15" initialSize="15" validationQuery="SELECT 1"
removeAbandonedOnBorrow="true" removeAbandonedOnMaintenance="true" testOnReturn="true"
testOnBorrow="true"/>
```
