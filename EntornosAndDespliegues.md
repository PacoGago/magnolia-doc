## Despligues en Magnolia :rocket:

#### Revisión del entorno

#### Magnolia

Revisamos el estado de la carpeta _/opt/magnolia_ y debemos tener en cuenta que el usario debe ser Tomcat:

```console
ubuntu@ip-10-19-0-10:/opt/magnolia$ ls -ltra
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
#### Tomcat para Author como para Public

Revisamos el estado de la carpeta de Tomcat según nuestra versión será _/var/lib/tomcat8_

```console
ubuntu@ip-10-19-0-10:/var/lib/tomcat8$ ls -ltra
total 16
drwxr-xr-x  2 tomcat8 tomcat8 4096 Sep 28  2017 lib
lrwxrwxrwx  1 root    root      19 Sep 28  2017 work -> ../../cache/tomcat8
lrwxrwxrwx  1 root    root      17 Sep 28  2017 logs -> ../../log/tomcat8
lrwxrwxrwx  1 root    root      12 Sep 28  2017 conf -> /etc/tomcat8
drwxr-xr-x 44 root    root    4096 Apr 17 12:56 ..
drwxr-xr-x  4 root    root    4096 Apr 17 12:56 .
drwxrwxr-x  3 tomcat8 tomcat8 4096 Apr 17 12:56 webapps
ubuntu@ip-10-19-0-10:/var/lib/tomcat8$
```

Revisamos la carpeta _webapps_ del Tomcat: En esta estructura podremos tene para la Author una carpeta llamada _magnoliaAuthor_ con un enlace a _/opt/magnolia/webapps/magnolia_ pero también puede tener esta estructura para su correcto funcionamiento tanto en Author como en Public:

```console
ubuntu@ip-10-19-0-10:/var/lib/tomcat8/webapps$ ls -ltra
total 12
drwxr-xr-x 4 root    root    4096 Apr 17 12:56 ..
drwxr-xr-x 3 root    root    4096 Apr 17 12:56 ROOT
drwxrwxr-x 3 tomcat8 tomcat8 4096 Apr 17 12:56
```
