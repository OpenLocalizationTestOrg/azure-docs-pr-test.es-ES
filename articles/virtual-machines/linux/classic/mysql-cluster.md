---
title: aaaClusterize MySQL con conjuntos de carga equilibrada | Documentos de Microsoft
description: "Configurar un equilibrio de carga, la alta disponibilidad Linux MySQL clúster creado con el modelo de implementación clásica de hello en Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>Usar conjuntos de carga equilibrada tooclusterize MySQL en Linux
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico. Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. A [plantilla del Administrador de recursos](https://azure.microsoft.com/documentation/templates/mysql-replication/) está disponible si necesita toodeploy un clúster de MySQL.

Este artículo explora y Hola distintos enfoques disponibles toodeploy basados en Linux servicios de alta disponibilidad en Microsoft Azure, exploración de alta disponibilidad del servidor de MySQL como instrucciones detalladas muestra. En [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)hay un vídeo disponible que ilustra este enfoque.

Describiremos una solución de alta disponibilidad de MySQL de un solo maestro y dos nodos independientes basada en DRBD, Corosync y Pacemaker. Solamente se ejecuta un nodo MySQL en cada momento. Lectura y escritura de hello recursos DRBD son también un nodo de tooonly limitado a la vez.

No es necesario para una solución VIP como informes LV, dado que va a utilizar conjuntos de carga equilibrada en tooprovide round robin funcionalidad y punto de conexión de detección de Microsoft Azure, eliminación y recuperación correcta de hello VIP. Hola VIP es una dirección IPv4 globalmente enrutable asignada por Microsoft Azure al servicio en la nube Hola crearlo.

Hay otras posibles arquitecturas para MySQL, como, por ejemplo, NBD Cluster, Percona, Galera y diversas soluciones middleware que incluyen, al menos, una disponible como máquina virtual en [VM Depot](http://vmdepot.msopentech.com). Siempre que estas soluciones se pueden replicar en unidifusión y multidifusión o difusión y no dependen del almacenamiento compartido o varias interfaces de red, escenarios de hello deben ser fácil toodeploy en Microsoft Azure.

Estas arquitecturas de agrupación en clústeres pueden ampliarse tooother productos como PostgreSQL y OpenLDAP de un modo similar. Por ejemplo, este procedimiento de equilibro de carga independiente se probó correctamente con OpenLDAP multimaestro y puede verlo en nuestro blog de Channel 9.

## <a name="get-ready"></a>Prepárese
Necesita Hola siguiente recursos y la capacidad de:

  - Una Microsoft Azure cuenta con una suscripción válida, toocreate capaz de al menos dos máquinas virtuales (extra se usó en este ejemplo)
  - Una red y una subred
  - Un grupo de afinidad
  - Un conjunto de disponibilidad
  - Hola capacidad toocreate discos duros virtuales en Hola misma región que el servicio de nube de Hola y conéctelas toohello máquinas virtuales de Linux

### <a name="tested-environment"></a>Entorno probado
* Ubuntu 13.10
  * DRBD
  * MySQL Server
  * Corosync y Pacemaker

### <a name="affinity-group"></a>Grupo de afinidad
Crear un grupo de afinidad para la solución de hello debe iniciar sesión en el portal de Azure clásico toohello seleccionar **configuración**y la creación de un grupo de afinidad. Recursos asignados que se crean con posterioridad se asignarán toothis grupo de afinidad.

### <a name="networks"></a>Redes
Se crea una nueva red y se crea una subred dentro de la red de Hola. En este ejemplo se usa una red 10.10.10.0/24 con una sola subred /24 dentro.

### <a name="virtual-machines"></a>Máquinas virtuales
Hola primera Ubuntu 13.10 VM se crea mediante una imagen de la Galería de Ubuntu Endorsed y se denomina `hadb01`. Se crea un nuevo servicio de nube en proceso de hello, denominado hadb. Este nombre muestra hello compartido, naturaleza con equilibrio de carga que el servicio de hello tendrán cuando se agregan más recursos. Hola creación de `hadb01` está sin incidentes y se rellena mediante el portal de Hola. Se crea automáticamente un punto de conexión de SSH, y se selecciona la nueva red de Hola. Ahora puede crear un conjunto de disponibilidad para hello las máquinas virtuales.

Después de hello primera máquina virtual se crea (técnicamente, cuando se crea el servicio de nube de hello), crear Hola segunda máquina virtual, `hadb02`. Para hello segunda máquina virtual, utilizar Ubuntu 13.10 VM de hello galería mediante el portal de hello, pero usar un servicio de nube existente, `hadb.cloudapp.net`, en lugar de crear uno nuevo. conjunto de red y la disponibilidad de Hello debe seleccionarse automáticamente. También se creará un extremo SSH.

Después de que se han creado dos máquinas virtuales, tome nota del puerto SSH de Hola para `hadb01` (puerto TCP 22) y `hadb02` (asignado automáticamente por Azure).

### <a name="attached-storage"></a>Almacenamiento acoplado
Adjuntar un tooboth de disco nuevas máquinas virtuales y crear discos de 5 GB en proceso de Hola. discos de Hola se hospedan en el contenedor VHD de hello en uso para los discos de sistema operativo principal. Después de que se crean y se adjuntan discos, no hay ningún toorestart necesidad Linux porque kernel Hola ver Hola nuevo dispositivo. Este dispositivo suele ser `/dev/sdc`. Comprobar `dmesg` para la salida de hello.

En cada máquina virtual, cree una partición utilizando `cfdisk` (partición primaria, de Linux) y escribir Hola nueva tabla de partición. No cree un sistema de archivos en esta partición.

## <a name="set-up-hello-cluster"></a>Configurar el clúster de Hola
Utilice APT tooinstall Corosync, marcapasos y DRBD en ambas máquinas virtuales Ubuntu. toodo con `apt-get`, ejecute hello código siguiente:

    sudo apt-get install corosync pacemaker drbd8-utils.

No instale MySQL en este momento. Debian y Ubuntu scripts de instalación se inicializarán en un directorio de datos de MySQL en `/var/lib/mysql`, pero porque el directorio de hello será reemplazado por un sistema de archivos DRBD, necesita tooinstall MySQL más adelante.

Comprobar (mediante el uso de `/sbin/ifconfig`) que ambas máquinas virtuales usan direcciones de subred 10.10.10.0/24 de Hola y que puede hacer ping entre sí por su nombre. También puede usar `ssh-keygen` y `ssh-copy-id` toomake seguro ambas máquinas virtuales pueden comunicarse a través de SSH sin necesidad de una contraseña.

### <a name="set-up-drbd"></a>Configure DRBD
Crear un recurso DRBD que usa subyacente hello `/dev/sdc1` partición tooproduce un `/dev/drbd1` recursos que se ha dado formato mediante ext3 y usar en los nodos principales y secundarios.

1. Abra `/etc/drbd.d/r0.res` y Hola copia siguiendo la definición de recursos en ambas máquinas virtuales:

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. Inicializar recursos hello mediante `drbdadm` en ambas máquinas virtuales:

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. En Hola VM principal (`hadb01`), forzar (principal) de la propiedad de recurso DRBD de hello:

        sudo drbdadm primary --force r0

Si examina el contenido de Hola de/proc/drbd (`sudo cat /proc/drbd`) en ambas máquinas virtuales, debería ver `Primary/Secondary` en `hadb01` y `Secondary/Primary` en `hadb02`, coherentes con la solución de hello en este momento. disco de 5 GB de Hola se sincroniza en la red de 10.10.10.0/24 de hello en ningún toocustomers de forma gratuita.

Después de haber sincronizado disco hello, puede crear sistema de archivos de hello en `hadb01`. Para realizar pruebas, hemos usado ext2, pero Hola sigue código creará un sistema de archivos ext3:

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>Montar hello DRBD recurso
Está ahora listo toomount hello DRBD recursos `hadb01`. Debian y productos derivados usan `/var/lib/mysql` como directorio de datos de MySQL. Dado que no tiene instalado MySQL, cree el directorio de Hola y montar hello DRBD recurso. tooperform esta opción, ejecute hello siguiente código de `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>Instalación de MySQL
Ahora está listo tooinstall MySQL en `hadb01`:

    sudo apt-get install mysql-server

Para `hadb02`, tiene dos opciones. Puede instalar a mysql server, que se crean /var/lib/mysql, rellenar con un nuevo directorio de datos y, a continuación, quite el contenido de Hola. tooperform esta opción, ejecute hello siguiente código de `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

segunda opción de Hello es toofailover demasiado`hadb02` y, a continuación, instalar servidor mysql no existe. Las secuencias de comandos de instalación dará cuenta de instalación existente de hello y no toque.

Ejecución hello código en siguiente `hadb01`:

    sudo drbdadm secondary –force r0

Ejecución hello código en siguiente `hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

Si no tiene pensado toofailover DRBD ahora, Hola primera opción es más fácil aunque sin duda es menos elegante. Después de configurar esto, puede comenzar a trabajar en su base de datos MySQL. Ejecución hello código en siguiente `hadb02` (o cualquiera de los servidores de hello está activo, según tooDRBD):

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> Esta última instrucción eficazmente deshabilita la autenticación de usuario de la raíz de hello en esta tabla. Las instrucciones GRANT de producción deben reemplazar esto y solamente se incluye por motivos ilustrativos.

Si desea que las consultas de toomake desde máquinas virtuales de hello exterior (que es el propósito de Hola de esta guía), también necesita tooenable redes para MySQL. En ambas máquinas virtuales, abra `/etc/mysql/my.cnf` y vaya demasiado`bind-address`. Cambiar dirección de hello en 127.0.0.1 too0.0.0.0. Después de guardar el archivo hello, emitir una `sudo service mysql restart` en su objeto principal actual.

### <a name="create-hello-mysql-load-balanced-set"></a>Crear conjunto de equilibrio de carga de MySQL de Hola
Volver atrás toohello portal, vaya demasiado`hadb01`y elija **extremos**. toocreate un extremo, elija MySQL (TCP 3306) de la lista desplegable de Hola y seleccione **conjunto con equilibrio de carga nueva creación**. Extremo de carga equilibrada de nombre hello `lb-mysql`. Establecer **tiempo** too5 segundos, mínimos.

Después de crear el punto de conexión de hello, vaya demasiado`hadb02`, elija **extremos**y crear un punto de conexión. Elija `lb-mysql`y, a continuación, seleccione MySQL desde la lista desplegable de Hola. También puede utilizar Hola CLI de Azure para este paso.

Ahora tienes todo lo que necesita para una operación manual del clúster de Hola.

### <a name="test-hello-load-balanced-set"></a>Probar el conjunto de equilibrio de carga de Hola
Las pruebas se pueden realizar desde un equipo externo usando cualquier cliente MySQL, o bien mediante ciertas aplicaciones, como phpMyAdmin ejecutada como un sitio web de Azure. En este caso, utiliza una herramienta de línea de comandos de MySQL en otro cuadro de Linux:

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>Conmutación por error manual
Puede simular conmutaciones por error cerrando MySQL, cambiando el rol principal de DRBD e iniciando MySQL de nuevo.

tooperform esta tarea, ejecute hello siguiente código de hadb01:

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

Después en hadb02:

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

Una vez realizada la conmutación por error manualmente, puede repetir la consulta remota, que debe funcionar perfectamente.

## <a name="set-up-corosync"></a>Configuración de Corosync
Corosync es Hola subyacente clúster infraestructura necesaria para marcapasos toowork. Para el latido (y otros métodos como Ultramonkey), Corosync es una división de las funcionalidades CRM de hello, mientras marcapasos permanecen tooHeartbeat más similar en la funcionalidad.

restricción principal Hola para Corosync en Azure es que Corosync prefiere multidifusión a través de difusión a las comunicaciones de unidifusión, pero las redes de Microsoft Azure solo admite unidifusión.

Por suerte, Corosync tiene un modo de unidifusión activo. Hola única restricción real es que, dado que todos los nodos no se comunican entre sí, es necesario nodos de hello toodefine en los archivos de configuración, incluidas las direcciones IP. Podemos usar archivos de ejemplo de Hola Corosync de unidifusión y cambio enlazan la dirección, listas de nodos y directorios de registro (Ubuntu usa `/var/log/corosync` al uso de archivos de ejemplo de Hola a `/var/log/cluster`) y permitir a las herramientas de quórum.

> [!NOTE]
> Utilice siguiente hello `transport: udpu` hello y directiva definir manualmente las direcciones IP para ambos nodos.

Ejecución hello código en siguiente `/etc/corosync/corosync.conf` para ambos nodos:

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

Copie este archivo de configuración en ambas VM e inicie Corosync en los dos nodos:

    sudo service start corosync

Justo después de iniciar el servicio de hello, clúster Hola se debe establecer en anillo actual de Hola y debe estar constituido quórum. Podemos comprobar esta funcionalidad si examina los registros o ejecutando el siguiente código de hello:

    sudo corosync-quorumtool –l

Verá toohello similar de salida después de imagen:

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>Configuración de Pacemaker
Usa marcapasos Hola toomonitor de clúster para los recursos, define cuando los elementos dejan de funcionar y cambia esos toosecondaries de recursos. Entre las diferentes posibilidades que existen, los recursos se pueden definir desde un conjunto de scripts disponibles o desde scripts LSB (de tipo init).

Queremos marcapasos demasiado "propio" hello DRBD recurso, punto de montaje de hello y servicio de MySQL Hola. Si marcapasos pueden activar y desactivar DRBD, montar y desmontar y, a continuación, iniciar y detener MySQL Hola derecha orden cuando algo mal ocurre con hello principal, el programa de instalación está completa.

Cuando instalé por primera vez Pacemaker, la configuración debe ser suficientemente sencilla, algo como lo siguiente:

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. Compruebe la configuración de hello ejecutando `sudo crm configure show`.
2. A continuación, cree un archivo (como `/tmp/cluster.conf`) con hello recursos siguientes:

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. Cargar archivo hello en configuración de Hola. Solo necesita toodo esto en un nodo.

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. Asegúrese de que Pacemaker se inicia durante el arranque en ambos nodos:

        sudo update-rc.d pacemaker defaults

5. Mediante el uso de `sudo crm_mon –L`, compruebe que uno de los nodos se ha convertido en maestro de hello para el clúster de Hola y todos los recursos de Hola está ejecutando. Puede usar toocheck de montaje y ps que ejecutan recursos Hola.

Hola siguiente captura de pantalla muestra `crm_mon` con un nodo detenido (salida seleccionando Ctrl + C):

![crm_mon node stopped](./media/mysql-cluster/image002.png)

Esta captura de pantalla muestra ambos nodos, uno maestro y otro subordinado:

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a>Prueba
Ya puede llevar a cabo una simulación de conmutación por error automática. Hay dos toodo formas esto: flexibles y forzados.

Hello forma parcial con la función de cierre del clúster de hello: ``crm_standby -U `uname -n` -v on``. Si usa esto en el patrón de hello, esclavo hello tiene sobre. Recuerde tooset esta toooff atrás. Si no lo hace, crm_mon mostrará un nodo en espera.

Hello malas se va a cerrar hacia abajo Hola VM principal (hadb01) mediante el portal de Hola o cambiando Hola runlevel en hello VM (es decir, detener, cierre). Esto ayuda a Corosync y marcapasos mediante señales ir del patrón Hola hacia abajo. Puede probarlo (es útil para las ventanas de mantenimiento), pero también puede forzar el escenario de hello inmovilizando Hola máquina virtual.

## <a name="stonith"></a>STONITH
Debe ser posible tooissue un apagado de máquina virtual a través de hello Azure CLI en lugar de una secuencia de comandos STONITH que controla un dispositivo físico. Puede usar `/usr/lib/stonith/plugins/external/ssh` como base y habilitar STONITH en la configuración del clúster de Hola. Debe instalarse globalmente CLI de Azure y configuración de publicación de Hola y se debe cargar el perfil de usuario del clúster de Hola.

Está disponible en el código de ejemplo para el recurso de hello [GitHub](https://github.com/bureado/aztonith). Cambiar configuración del clúster de hello agregando Hola después demasiado`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> script de Hola no realiza comprobaciones de arriba/abajo. recurso de Hello original SSH tenía 15 comprobaciones de ping, pero el tiempo de recuperación para una máquina virtual de Azure puede ser más variables.

## <a name="limitations"></a>Limitaciones
Hola siguientes limitaciones se aplica:

* Hola de script de recursos DRBD linbit que administra DRBD como un recurso en usos marcapasos `drbdadm down` al apagar un nodo, incluso si solo se va nodo hello en espera. Esto no es lo ideal porque esclavo hello no va a sincronizar recursos DRBD de Hola a pesar de master Hola lo escribe. Si master hello no amablemente, esclavo Hola puede asumir un estado anterior del sistema de archivos. Hay dos formas posibles de resolver este problema:
  * Aplicando un comando `drbdadm up r0` en todos los nodos del clúster mediante un guardián local (sin clústeres)
  * Editar el script de Hola linbit DRBD, asegurándose de que `down` en no se llama`/usr/lib/ocf/resource.d/linbit/drbd`
* equilibrador de carga de Hello necesita toorespond de al menos cinco segundos, por lo que las aplicaciones deben ser compatible con clústeres y ser más tolerante a errores de tiempo de espera. También pueden ayudar otras arquitecturas, como las colas de la aplicación y middlewares de consulta.
* MySQL para la optimización es tooensure necesario que realiza la escritura a un ritmo administrable y memorias caché son toodisk vaciado con tanta frecuencia como toominimize posible pérdida de memoria.
* Escribir el rendimiento depende en VM de interconexión de conmutador virtual de hello porque se trata de mecanismo de hello DRBD tooreplicate Hola dispositivo usado.
