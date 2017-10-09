---
title: aaaSet de MySQL en una VM de Linux en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall Hola MySQL de la pila en una máquina virtual de Linux (RedHat o Ubuntu familia SO) en Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a>¿Cómo tooinstall MySQL en Azure
En este artículo, aprenderá cómo tooinstall y configurar MySQL en una máquina virtual de Azure ejecutan Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>Instalación de MySQL en la máquina virtual
> [!NOTE]
> Ya debe tener una máquina virtual de Microsoft Azure ejecutan Linux en orden toocomplete este tutorial. Vea la [tutorial de la máquina virtual de Linux de Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate y configurar una VM de Linux con `mysqlnode` como nombre de la máquina virtual de Hola y `azureuser` como usuario antes de continuar.
> 
> 

En este caso, utilice puerto 3306 como Hola puerto de MySQL.  

Conectar toohello VM de Linux que creó mediante putty. Si se trata de hello primera vez que use la máquina virtual de Linux de Azure, vea cómo toouse putty conectarse tooa VM de Linux [aquí](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Usaremos repositorio paquete tooinstall MySQL5.6 como un ejemplo de este artículo. En realidad, MySQL5.6 tiene un mejor rendimiento MySQL5.5.  Puede encontrar más información [aquí](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/):

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>Cómo tooinstall MySQL5.6 en Ubuntu
Usaremos aquí la máquina virtual de Linux con Ubuntu de Azure.

* Paso 1: Instalar un servidor MySQL 5.6 cambiar demasiado`root` usuario:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Instalación de mysql-server 5.6:
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    Durante la instalación, verá un poping de la ventana de cuadro de diálogo seguridad tooask se tooset MySQL raíz contraseña a continuación y se necesita establecer Hola contraseña aquí.
  
    ![imagen](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    Contraseña de entrada hello tooconfirm de nuevo.

    ![imagen](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* Paso 2: Iniciar sesión en el servidor MySQL
  
    Una vez finalizada la instalación del servidor MySQL, el servicio MySQL se inicia automáticamente. Puede iniciar sesión en el servidor MySQL con el usuario `root` .
    Usar hello por debajo de la contraseña de toologin y entrada de comando.
  
             #[root@mysqlnode ~]# mysql -uroot -p
* Paso 3: Administrar Hola ejecutando el servicio MySQL
  
    (a) Obtener el estado del servicio MySQL
  
             #[root@mysqlnode ~]# service mysql status
  
    (b) Iniciar el servicio MySQL
  
             #[root@mysqlnode ~]# service mysql start
  
    (c) Detener el servicio MySQL
  
             #[root@mysqlnode ~]# service mysql stop
  
    (d) reinicie el servicio de MySQL de Hola
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>¿Cómo tooinstall MySQL en la familia de sistemas operativos de Red Hat que CentOS, Oracle Linux
Aquí usaremos la máquina virtual de Linux con CentOS u Oracle Linux.

* Paso 1: Agregar Hola MySQL Yum repositorio conmutador demasiado`root` usuario:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Descargue e instale el paquete de la versión de Hola MySQL:
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* Paso 2: Editar por debajo del repositorio de archivos tooenable Hola MySQL para descargar el paquete de MySQL5.6 Hola.
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    Actualice cada valor de este toobelow de archivo:
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* Paso 3: Instalación de MySQL desde el repositorio de MySQL Install MySQL:
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    Se instalará el paquete RPM MySQL y todos los paquetes relacionados.
* Paso 4: Administrar Hola ejecutando el servicio MySQL
  
    (a) comprobar estado de servicio de Hola de servidor de MySQL de hello:
  
           #[root@mysqlnode ~]#service mysqld status
  
    (b) Compruebe si está ejecutando el servidor de puerto de MySQL de hello predeterminado:
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    (c) inicie Hola MySQL server:

           #[root@mysqlnode ~]#service mysqld start

    (d) detener el servidor de MySQL de hello:

           #[root@mysqlnode ~]#service mysqld stop

    (e) establecer MySQL toostart cuando el arranque de sistema de hello:

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>¿Cómo tooinstall MySQL en SUSE Linux
Aquí usaremos la máquina virtual de Linux con OpenSUSE.

* Paso 1: Descargar e instalar el servidor MySQL
  
    Cambiar demasiado`root` usuario a través de comando siguiente:  
  
           #sudo su -
  
    Descargar e instalar el paquete MySQL:
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* Paso 2: Administrar Hola ejecutando el servicio MySQL
  
    (a) comprobar estado de Hola de servidor de MySQL de hello:
  
           #[root@mysqlnode ~]# rcmysql status
  
    (b) Compruebe si Hola puerto predeterminado del servidor de MySQL de hello:
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    (c) inicie Hola MySQL server:

           #[root@mysqlnode ~]# rcmysql start

    (d) detener el servidor de MySQL de hello:

           #[root@mysqlnode ~]# rcmysql stop

    (e) establecer MySQL toostart cuando el arranque de sistema de hello:

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>siguiente paso
Buscar más información de uso y sobre MySQL [aquí](https://www.mysql.com/).

