Vagrant para Hadoop, Spark and Hive
=========================================

# Introduccion

Proyecto Vagrant para correr un nodo con los siguientes componentes:

* Hadoop 
* Hive 
* HBase 
* Spark  
* Tez 

# Inicio rapido


1. Descargar e instalar [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Descargar e instalar [Vagrant](http://www.vagrantup.com/downloads.html).
3. Clonar este repo
6. En la terminal entrar al directorio del proyecto clonado (probablemente `cd vagrant-hadoop-spark-hive`).
7. Correr `vagrant up --provider=virtualbox` to create the VM using virtualbox as a provider.
8. La primera vez va a tardar mas en iniciar, debe descargar todos los componentes. Siguientes corridas seran mas rapidas
9. Ejecutar ```vagrant ssh``` para entrar en la VM.
10. En caso de tener problemas con ```ssh``` se puede desde la interfaz de VirtualBox click derecho en ```node1``` > Show

User: vagrant
Pass: vagrant

# Versiones
Se pueden definir las versiones de los componentes en `scripts/versions.sh`

COmbinaciones de versiones que funcionan: -

1. Spark-2.1.1 basado en: -
    * Hadoop 2.7.3
    * Hive 1.2.2
    * Spark 2.1.1
    * Tez 0.8.5
    * Sqoop 1.4.6
    * Pig 0.17.0
    * flume 1.7.0
    * Zeppelin 0.8.0 (with Spark/scala, md, file and JDBC interpreters)


2. (Por default) Spark-2.3.0 basado en: -
    * Hadoop 2.7.6
    * Hive 2.3.3
    * Spark 2.3.0
    * Tez 0.9.1
    * Sqoop 1.4.6
    * Pig 0.17.0
    * flume 1.7.0
    * Zeppelin 0.8.0 (with Spark/scala, md, file and JDBC interpreters)

# Servicios
El nodo correra los siguientes servicios:

* HDFS NameNode + DataNode
* YARN ResourceManager/NodeManager + JobHistoryServer + ProxyServer
* Hive metastore y server2
* Spark history server
* Hbase server

# Interfaces web

Disponibles en :

* YARN resource manager:  (http://node1:8088)
* HBase: (http://node1:16010)
* Job history:  (http://node1:19888/jobhistory/)
* HDFS: (http://node1:50070/dfshealth.html)
* Spark history server: (http://node1:18080)
* Spark context UI (if a Spark context is running): (http://node1:4040)

Sustituir `node1` por la ip de la maquina virtual si es necesario.

# Carpetas compartidas

Por defecto se monta toda la carpeta del proyecto en `/vagrant`
Ademas se monta la carpeta `./starter-datasets` en `/home/vagrant/starter-datasets`




# Uso de la VM

Para apagar sin perder lo que hay en la VM: -

```
vagrant halt
```

o

```
vagrant suspend
```

Para encender la VM utilizar `vagrant up`

Para borrar la VM: -

```
vagrant destroy
```

Luego de destruir, `vagrant up` vuelve a generar la VM. Los componentes quedan cacheadas en la carpeta del proyecto, no se descargaran de nuevo


# Como cerrar servicios 

```
$ vagrant ssh
$ sudo -sE
$ /vagrant/scripts/stop-spark.sh
$ /vagrant/scripts/stop-hbase.sh
$ /vagrant/scripts/stop-hadoop.sh

```

# Agradecimientos

[Alex Holmes](https://github.com/alexholmes)
[Matheus Cunha](https://github.com/matheuscunha)
[Martin Robson](https://github.com/martinprobson)