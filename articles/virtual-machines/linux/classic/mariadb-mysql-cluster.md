---
title: "aaaRun un MariaDB (MySQL) del clúster en Azure | Documentos de Microsoft"
description: "Creación de un clúster MariaDB + Galera MySQL en Azure Virtual Machines"
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>Clúster MariaDB (MySQL): tutorial de Azure
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico. Este artículo trata el modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar modelos de hello Azure Resource Manager.

> [!NOTE]
> Clúster de MariaDB Enterprise ahora está disponible en hello Azure Marketplace. nueva oferta de Hello implementará automáticamente un clúster de MariaDB Galera en el Administrador de recursos de Azure. Debe usar la nueva oferta de Hola de [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).
>
>

Este artículo muestra cómo toocreate una con varios maestros [Galera](http://galeracluster.com/products/) clúster de [MariaDBs](https://mariadb.org/en/about/) (un reemplazo e inmediata robusta, escalable y confiable para MySQL) toowork en un entorno de alta disponibilidad en Azure máquinas virtuales.

## <a name="architecture-overview"></a>Introducción a la arquitectura
Este artículo describe cómo hello toocomplete siguiendo los pasos:

- Crear un clúster de tres nodos.
- Discos de datos de hello independiente del disco de sistema operativo de Hola.
- Crear discos de datos de hello en configuración de RAID-0/particionados tooincrease e/s por segundo.
- Use de carga del equilibrador de carga de Azure toobalance Hola para hello tres nodos.
- toominimize repetitiva de trabajo, crear una imagen de máquina virtual que contiene MariaDB + Galera y utilizarlo toocreate Hola otro máquinas virtuales del clúster.

![Arquitectura del sistema](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> En este tema usa hello [CLI de Azure](../../../cli-install-nodejs.md) herramientas, por lo que debe toodownload seguro de ellos y conéctelos correspondiente toohello instrucciones de tooyour suscripción de Azure. Si necesita un comandos de toohello de referencia disponibles en hello CLI de Azure, vea hello [referencia de comandos de CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). También necesitará demasiado[crear una clave SSH para la autenticación] y tome nota de la ubicación del archivo PEM Hola.
>
>

## <a name="create-hello-template"></a>Crear plantilla de Hola
### <a name="infrastructure"></a>Infraestructura
1. Crear un grupo de afinidad toohold recursos de hello juntos.

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. Cree una red virtual.

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. Crear un toohost de cuenta de almacenamiento nuestro todos los discos. No debería colocar más de 40 discos muy utilizados en hello mismo tooavoid de cuenta de almacenamiento alcanza el límite de la cuenta de almacenamiento de hello 20.000 e/s por segundo. En este caso, está por debajo de ese límite, por lo que podrá almacenar todo el contenido en la misma cuenta para simplificar el trabajo de Hola.

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. Buscar el nombre de Hola de imagen de máquina virtual de hello CentOS 7.

        azure vm image list | findstr CentOS
   salida de Hello será similar a `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.

   Use ese nombre en hello siguiendo el paso.
5. Crear plantilla de VM de Hola y reemplace /path/to/key.pem por ruta de acceso de Hola dónde ha almacenado Hola genera PEM SSH clave.

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. Adjuntar datos de 500 GB cuatro discos toohello máquina virtual para su uso en la configuración de RAID de Hola.

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. Utilizar SSH toosign en toohello plantilla máquina virtual que creó al mariadbhatemplate.cloudapp.net:22 y conectarse con su clave privada.

### <a name="software"></a>Software
1. Obtener la raíz de Hola.

        sudo su

2. Instalar compatibilidad con RAID:

    a. Instale mdadm.

              yum install mdadm

    b. Crear configuración de RAID0/bandas de hello con un sistema de archivos EXT4.

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. Crear el directorio de punto de montaje de Hola.

              mkdir /mnt/data
    d. Recuperar Hola UUID del dispositivo RAID de hello recién creado.

              blkid | grep /dev/md0
    e. Edite /etc/fstab.

              vi /etc/fstab
    f. Agregar automáticamente de hello dispositivo tooenable montar en el reinicio, reemplazando Hola UUID con valor de hello obtenido de hello anterior **blkid** comando.

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    g. Monte la nueva partición de Hola.

              mount /mnt/data

3. Instale MariaDB.

    a. Crear archivo de hello MariaDB.repo.

                vi /etc/yum.repos.d/MariaDB.repo

    b. Rellenar el archivo de repositorio de hello con hello siguen contenido:

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. tooavoid entra en conflicto, quite postfijo existente y las bibliotecas de mariadb.

           yum remove postfix mariadb-libs-*
    d. Instale MariaDB con Galera.

           yum install MariaDB-Galera-server MariaDB-client galera

4. Mueva el dispositivo de bloque de hello MySQL datos directory toohello RAID.

    a. Copie el directorio actual de MySQL de hello en su nueva ubicación y quitar el directorio anterior Hola.

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. Establecer permisos para el nuevo directorio de hello en consecuencia.

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. Crear un vínculo simbólico que apunta Hola antiguo toohello nueva ubicación del directorio en hello partición RAID.

           ln -s /mnt/data/mysql /var/lib/mysql

5. Porque [SELinux interfiere con las operaciones del clúster hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), es necesario toodisable para hello sesión actual. Editar `/etc/selinux/config` toodisable para reinicios posteriores.

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. Valide las ejecuciones de MySQL.

   a. Inicie MySQL.

           service mysql start
   b. Proteger la instalación de MySQL de hello, establecer contraseña de la raíz de hello, quita el inicio de sesión de los usuarios anónimos toodisable raíz remota y quitar base de datos de prueba de Hola.

           mysql_secure_installation
   c. Cree un usuario en la base de datos de Hola para las operaciones del clúster y, opcionalmente, para las aplicaciones.

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. Detenga MySQL.

            service mysql stop
7. Cree un marcador de posición de configuración.

   a. Editar Hola MySQL configuración toocreate un marcador de posición para la configuración de clúster de Hola. No Reemplace hello  **`<Variables>`**  o quite ahora. Eso sucederá después de que cree una máquina virtual desde esta plantilla.

            vi /etc/my.cnf.d/server.cnf
   b. Editar hello  **[galera]**  sección y desactive.

   c. Editar hello **[mariadb]** sección.

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. Abra los puertos necesarios en firewall de hello mediante FirewallD en CentOS 7.

   * MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * Volver a cargar Hola firewall:`firewall-cmd --reload`

9. Optimizar el sistema de hello para el rendimiento. Para más información, consulte la [estrategia de optimización del rendimiento](optimize-mysql.md).

   a. Modifique el archivo de configuración de MySQL de Hola de nuevo.

            vi /etc/my.cnf.d/server.cnf
   b. Editar hello **[mariadb]** anexar Hola siguen contenido y la sección:

   > [!NOTE]
   > Se recomienda que innodb\_buffer\_pool_size sea el 70 % de la memoria de su máquina virtual. En este ejemplo, se se estableció en 2,45 GB de tamaño mediano Hola VM de Azure con 3,5 GB de RAM.
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. Detener MySQL, deshabilitar el servicio MySQL no se ejecuten en tooavoid inicio interrumpir clúster Hola al agregar un nodo y desaprovisionar máquina Hola.

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. Capturar Hola VM a través del portal de Hola. (Actualmente, [emitir #1268 en herramientas de Azure CLI hello](https://github.com/Azure/azure-xplat-cli/issues/1268) describe los hechos de Hola que imágenes capturadas con herramientas de hello Azure CLI no capturan Hola adjuntada los discos de datos.)

    a. Apagar la máquina de Hola a través del portal de Hola.

    b. Haga clic en **capturar** y especifique el nombre de la imagen de hello como **mariadb-galera-image**. Proporcione una descripción y seleccione "He ejecutado waagent".
      
      ![Captura de máquina virtual de Hola](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>Crear clúster Hola
Cree tres máquinas virtuales con plantilla de hello creado y, a continuación, configurará e iniciará el clúster de Hola.

1. Crear Hola primera CentOS 7 VM de hello mariadb-galera-imagen de la imagen que ha creado, a proporcionar Hola siguiente información:

 - Nombre de la red virtual: mariadbvnet
 - Subred: mariadb
 - Tamaño de la máquina: mediana
 - Nombre de servicio de nube: mariadbha (o cualquier nombre que desee toobe tiene acceso a través de mariadbha.cloudapp.net)
 - Nombre de la máquina: mariadb1
 - Nombre del usuario: azureuser
 - Acceso de SSH: habilitado
 - Pasar el archivo de hello SSH certificado PEM y reemplazando /path/to/key.pem por ruta de acceso de Hola dónde ha almacenado Hola generan la clave SSH PEM.

   > [!NOTE]
   > siguientes comandos Hello se dividen una en varias líneas por motivos de claridad, pero debe especificar cada uno de ellos como una sola línea.
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. Cree dos más máquinas virtuales mediante la conexión de servicio en la nube mariadbha toohello. Cambiar el nombre de VM de Hola y Hola puerto tooa único puerto SSH no entra en conflicto con otras máquinas virtuales en Hola mismo servicio en la nube.

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  Para MariaDB3:

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. Dirección IP tooget Hola interna de cada una de las máquinas virtuales de hello tres, necesitará para el paso siguiente de hello:

    ![Obtención de la dirección IP](./media/mariadb-mysql-cluster/IP.png)
4. Use toosign SSH en máquinas virtuales de toohello tres y editar el archivo de configuración de hello en cada uno de ellos.

        sudo vi /etc/my.cnf.d/server.cnf

    Quite  **`wsrep_cluster_name`**  y  **`wsrep_cluster_address`**  mediante la eliminación de hello  **#**  al principio de Hola de línea de saludo.
    Además, reemplace  **`<ServerIP>`**  en  **`wsrep_node_address`**  y  **`<NodeName>`**  en  **`wsrep_node_name`**  con hello IP de la máquina virtual de direcciones y su nombre, respectivamente, y quite el comentario de dichas líneas así.
5. Iniciar el clúster de hello en MariaDB1 y permitir su ejecución en el inicio.

        sudo service mysql bootstrap
        chkconfig mysql on
6. Inicie MySQL en MariaDB2 y MariaDB3 y deje que se ejecute en el inicio.

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>Clúster de Hola de equilibrio de carga
Al crear máquinas virtuales de hello en clúster, se agrega en un conjunto de disponibilidad denominado clusteravset tooensure que se colocan en distintos dominios de error y actualización y que Azure no nunca mantenimiento en todos los equipos a la vez. Esta configuración cumple los requisitos de hello toobe admite Hola contrato de nivel de servicio de Azure (SLA).

Ahora use las solicitudes de toobalance de equilibrador de carga de Azure entre tres nodos de Hola.

Ejecute hello siga los comandos en su equipo mediante el uso de hello CLI de Azure.

estructura de parámetros de comando de Hello es:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

Hola CLI establece a Hola carga equilibrador sondeo intervalo too15 segundos, lo que pueden resultar un poco demasiado largos. Cambiar en el portal de hello en **extremos** para cualquiera de las máquinas virtuales de Hola.

![Edición del extremo](./media/mariadb-mysql-cluster/Endpoint.PNG)

Seleccione **Hola Reconfigure Load-Balanced establecer**.

![Volver a configurar Equilibrio de carga de hello conjunto](./media/mariadb-mysql-cluster/Endpoint2.PNG)

Cambio **intervalo de sondeo** too5 segundos y guarde los cambios.

![Cambio del intervalo de sondeo](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>Validar clúster Hola
se realiza el trabajo duro Hola. clúster de Hello ahora debería estar accesible en `mariadbha.cloudapp.net:3306`, que alcanza el equilibrador de carga de Hola y enrutar las solicitudes entre Hola tres máquinas virtuales de forma perfecta y eficaz.

Use los favoritos tooconnect de cliente de MySQL, o conéctese desde uno de hello tooverify de máquinas virtuales que funciona este clúster.

     mysql -u cluster -h mariadbha.cloudapp.net -p

A continuación, cree una base de datos y rellénela con algunos datos.

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

base de datos de Hello creó devuelve hello en la tabla siguiente:

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
En este artículo, creó un clúster MariaDB+Galera de alta disponibilidad de tres nodos en Azure Virtual Machines con CentOS 7. máquinas virtuales de Hello son carga equilibrada con el equilibrador de carga de Azure.

Es recomendable toolook en [toocluster de otra manera MySQL en Linux](mysql-cluster.md) y formas demasiado[optimizar y probar el rendimiento de MySQL en máquinas virtuales de Linux de Azure](optimize-mysql.md).

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[crear una clave SSH para la autenticación]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
