---
title: rendimiento de MySQL en Linux aaaOptimize | Documentos de Microsoft
description: "Obtenga información acerca de cómo toooptimize MySQL ejecutando en una máquina virtual (VM) Azure ejecutan Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>Optimización del rendimiento de MySQL en máquinas virtuales de Azure con Linux
Existen muchos factores que afectan al rendimiento de MySQL en Azure, tanto en la configuración de selección de software y hardware virtual. Este artículo se centra en la optimización del rendimiento a través del almacenamiento, el sistema y las configuraciones de base de datos.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico. Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para obtener información acerca de las optimizaciones de VM de Linux con el modelo del Administrador de recursos de hello, consulte [optimizar la VM de Linux en Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>Uso de RAID en una máquina virtual de Azure
El almacenamiento es el factor clave Hola que afecta al rendimiento de la base de datos en entornos de nube. Tooa en comparación con uno de los discos, RAID puede proporcionar un acceso más rápido a través de simultaneidad. Para más información, consulte [Niveles RAID estándar](http://en.wikipedia.org/wiki/Standard_RAID_levels).   

El rendimiento de E/S de disco, así como el tiempo de respuesta de las E/S pueden mejorarse con RAID. Nuestras pruebas de laboratorio muestran que se puede duplicar el rendimiento de E/S de disco y tiempo de respuesta de E/S puede reducirse a la mitad por término medio cuando se duplica el número Hola de discos RAID (de toofour dos, cuatro tooeight, etcetera). Consulte el [Apéndice A](#AppendixA) para más información.  

Además, la E/S de toodisk MySQL mejora el rendimiento al aumentar Hola nivel RAID.  Consulte el [Apéndice B](#AppendixB) para obtener más información.  

Puede que le interese el tamaño del fragmento de tooconsider Hola. En general, cuando el tamaño de fragmento es mayor, obtiene una menor sobrecarga, especialmente para las operaciones de escritura de mayor envergadura. Sin embargo, cuando el tamaño del fragmento de hello es demasiado grande, podría agregar una sobrecarga adicional que le impide al aprovechar la posibilidad de RAID. tamaño predeterminado actual de Hello es 512 KB, lo que demuestra toobe óptimo para los entornos de producción más generales. Consulte el [Apéndice C](#AppendixC) para más información.   

Existen límites en cuanto al número de discos que puede agregar para los distintos tipos de máquinas virtuales. Estos límites se detallan en [Tamaños de máquinas virtuales y servicios en la nube de Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Necesitará cuatro datos adjuntos discos toofollow Hola RAID ejemplo en este artículo, aunque puede elegir tooset de RAID con menos discos.  

En este artículo se da por supuesto que ya ha creado una máquina virtual Linux y que MYSQL está instalado y configurado. Para obtener más información acerca de cómo empezar, vea cómo tooinstall MySQL en Azure.  

### <a name="set-up-raid-on-azure"></a>Configuración de RAID en Azure
Hello pasos siguientes muestran cómo toocreate RAID en Azure mediante el uso de hello portal de Azure. También puede configurar RAID mediante scripts de Windows PowerShell.
En este ejemplo, configuraremos RAID 0 con 4 discos.  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a>Agregar una máquina virtual de datos disco tooyour
Hola portal de Azure, vaya a Panel de toohello y seleccione hello toowhich de máquina virtual que desee tooadd un disco de datos. En este ejemplo, la máquina virtual de hello es mysqlnode1.  

<!--![Virtual machines][1]-->

Haga clic en **Discos** y luego haga clic en **Asociar nuevo**.

![Agregar disco a máquinas virtuales](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

Cree un nuevo disco de 500 GB. Asegúrese de que **preferencia de caché de Host** se establece demasiado**ninguno**.  Cuando haya terminado, haga clic en **Aceptar**.

![Acoplar disco vacío](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


Esta acción agrega un disco vacío a la máquina virtual. Repita este paso tres veces más para que disponga de 4 discos de datos para RAID.  

Puede ver Hola agrega las unidades en la máquina virtual de hello examinando el registro de mensajes de Hola kernel. Por ejemplo, toosee esto en Ubuntu, Hola de uso siguiente comando:  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a>Crear RAID con hello discos adicionales
Hello pasos siguientes describen cómo demasiado[configurar RAID de software en Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Si está utilizando el sistema de archivos de hello XFS, ejecute hello siguientes pasos después de haber creado RAID.
>
>

tooinstall XFS en Debian, Ubuntu o lleva de Linux, Hola de uso siguiente comando:  

    apt-get -y install xfsprogs  

tooinstall XFS en Fedora, CentOS o RHEL, Hola de uso siguiente comando:  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>Configurar una nueva ruta de acceso de almacenamiento
Usar hello después comando tooset una nueva ruta de acceso de almacenamiento:  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a>Copiar Hola datos toohello nuevo almacenamiento ruta de acceso original
Usar hello comando toocopy datos toohello nuevo almacenamiento la ruta de acceso:  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a>Modificar los permisos por lo que puede tener acceso MySQL (lectura y escritura) disco de datos de Hola
Use los siguientes comandos toomodify permisos de hello:  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a>Ajustar la E/S de disco de hello algoritmo de programación
Linux implementa cuatro tipos de algoritmos de programación de E/S:  

* Algoritmo NOOP (sin operación)
* Algoritmo de fecha límite (fecha límite)
* Algoritmo de cola justa (CFQ)
* Algoritmo de período de presupuesto (antelación)  

Puede seleccionar a diferentes programadores de E/S en rendimiento de toooptimize escenarios diferentes. En un entorno de acceso aleatorio por completo, no hay una diferencia significativa entre hello CFQ y algoritmos de fecha límite para el rendimiento. Recomendamos que establezca tooDeadline de entorno de base de datos de MySQL de hello para la estabilidad. Si hay un elevado volumen de E/S secuenciales, el algoritmo CFQ puede reducir el rendimiento de las E/S de disco.   

De SSD y otros equipos, NOOP o fecha límite puede lograr un rendimiento mejor que el programador predeterminado de Hola.   

Núcleo de toohello anteriores 2.5, Hola predeterminado E/S programación algoritmo es fecha límite. A partir de kernel hello 2.6.18, CFQ pasara a ser de algoritmo de programación de E/S Hola de forma predeterminada.  Puede especificar esta configuración en tiempo de arranque de kernel o modificar esta configuración de forma dinámica cuando se ejecuta el sistema de Hola.  

Hola siguiente ejemplo muestra cómo toocheck y establezca Hola predeterminado programador toohello NOOP el algoritmo de familia de distribución Debian Hola.  

### <a name="view-hello-current-io-scheduler"></a>Programador de E/S de vista Hola actual
Programador de hello tooview ejecute hello siguiente comando:  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

Se muestra después de salida, lo que indica el programador actual hello:  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a>Cambiar Hola actual dispositivo (/ dev/sda) del algoritmo de programación de hello i/OS
Ejecute hello después de dispositivo actual de comandos toochange hello:  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> Establecer este valor solo para /dev/sda no es útil. Debe establecerse en todos los discos de datos donde reside la base de datos de Hola.  
>
>

Debería ver Hola después de salida, que indica que se ha recompilado grub.cfg correctamente y programador predeterminado Hola ha sido actualizada tooNOOP:  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Para hello familia de distribución de Red Hat, necesita Hola solo el siguiente comando:

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>Configurar las opciones de las operaciones de archivos de sistema
Una práctica recomendada es hello toodisable *atime* característica de registro en el sistema de archivos de Hola. Atime es Hola última hora de acceso de archivo. Cada vez que se tiene acceso a un archivo, los registros de sistema de archivo Hola Hola marca de tiempo en el registro de hello. Sin embargo, esta información no suele usarse. Por lo tanto, se puede deshabilitar si no es necesaria. Esto reducirá el tiempo total de acceso al disco.  

toodisable atime registro, necesita toomodify Hola archivo sistema configuración archivo/etc / fstab y agregar hello **noatime** opción.  

Por ejemplo, edite el archivo/etc/fstab de hello vim, agregando hello noatime tal y como se muestra en el siguiente ejemplo de Hola:  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

A continuación, vuelva a montar el sistema de archivos de hello con hello siguiente comando:  

    mount -o remount /RAID0

Hola de prueba modifica el resultado. Cuando se modifica el archivo de prueba de hello, no se actualiza la hora de acceso de Hola. Hola siguientes ejemplos se muestra el código de hello aspecto antes y después de la modificación.

Antes:        

![El código antes de la modificación del acceso.][5]

Después:

![El código después de la modificación del acceso.][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a>Aumentar Hola número máximo de identificadores de sistema de alta simultaneidad
MySQL es una base de datos de alta simultaneidad. número predeterminado de Hola de identificadores simultáneas es 1024 para Linux, que no siempre es suficiente. Usar hello siguiendo los pasos tooincrease Hola máximo simultáneas identificadores de simultaneidad elevada toosupport de hello sistema de MySQL.

### <a name="modify-hello-limitsconf-file"></a>Modificar el archivo de hello limits.conf
Hola tooincrease máximo permitido identificadores simultáneas, agregue Hola después de cuatro líneas en el archivo de hello /etc/security/limits.conf. Tenga en cuenta que 65536 es el número máximo de Hola que Hola sistema puede admitir.   

    * soft nofile 65536
    * hard nofile 65536
    * soft nproc 65536
    * hard nproc 65536

### <a name="update-hello-system-for-hello-new-limits"></a>Actualizar sistema de Hola para los nuevos límites de Hola
sistema de hello tooupdate, ejecute hello siguientes comandos:  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a>Asegúrese de que se actualizan los límites de Hola durante el arranque
Hola Put después de comandos de inicio en el archivo de hello /etc/rc.local por lo que aplicará al arrancar el sistema.  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>Optimización de la base de datos de MySQL
tooconfigure MySQL en Azure, puede usar Hola misma estrategia de optimización del rendimiento se usa en una máquina local.  

Hola reglas de optimización de E/S principales son:   

* Aumentar el tamaño de la caché de Hola.
* Reducir el tiempo de respuesta de E/S.  

configuración del servidor de MySQL de toooptimize, puede actualizar el archivo my.cnf de hello, que es el archivo de configuración predeterminado de Hola para equipos cliente y servidor.  

Hello siguientes elementos de configuración son Hola factores principales que afectan al rendimiento de MySQL:  

* **innodb_buffer_pool_size**: grupo de búferes de hello contiene datos almacenados en búfer y el índice de Hola. Normalmente, esto se establece too70 porcentaje de memoria física.
* **innodb_log_file_size**: se trata de tamaño del registro de hello puesta al día. Utilice tooensure de registros de puesta al día que las operaciones de escritura son rápidos, confiable y recuperable después de un bloqueo. Esto se establece too512 MB, lo que le proporcionará una gran cantidad de espacio para las operaciones de escritura de registro.
* **max_connections**: a veces, las aplicaciones no cierran las conexiones correctamente. Un valor mayor Hola servidor tendrá más tiempo toorecycle ralentizó conexiones. Hola número máximo de conexiones es 10 000, pero Hola recomienda máximo es 5000.
* **Innodb_file_per_table**: esta configuración habilita o deshabilita la capacidad de Hola de InnoDB toostore tablas en archivos independientes. Activar Hola opción tooensure que se pueden aplicar varias operaciones de administración avanzadas eficazmente. Desde un punto de vista del rendimiento, puede acelerar la transmisión de espacio de tabla de Hola y optimizar el rendimiento de administración de restos de Hola. Hola recomienda el valor de esta opción es ON.</br></br>
Desde MySQL 5.6, saludo predeterminado es ON, por lo que no se requiere ninguna acción. Para las versiones anteriores, la configuración predeterminada de hello es OFF. Hola debe cambiarse antes de que se cargan datos, porque solo las tablas recién creadas se ven afectadas.
* **innodb_flush_log_at_trx_commit**: valor predeterminado de hello es 1, con hello ámbito establecido too0 ~ 2. valor predeterminado de Hello es opción más adecuado de Hola para base de datos de MySQL independiente. configuración de Hola de 2 habilita Hola mayoría integridad de los datos y es adecuado para Master en MySQL clúster. valor de Hola de 0 permite pérdida de datos, lo que puede afectar la confiabilidad (en algunos casos con un mejor rendimiento) y es adecuado para esclavo en MySQL clúster.
* **Innodb_log_buffer_size**: búfer de registro de hello permite toorun de transacciones sin necesidad de tooflush Hola registro toodisk antes de hello las transacciones se confirman. Sin embargo, si no hay objeto binario grande o un campo de texto, caché Hola se consumirán rápidamente y se activará la E/S de disco frecuentes. Es mejor aumentar tamaño de búfer de hello si la variable de estado de Innodb_log_waits no es 0.
* **query_cache_size**: Hola mejor opción es toodisable desde el principio de Hola. Establecer too0 query_cache_size (es decir, valor predeterminado de hello en MySQL 5.6) y usar otra toospeed métodos consultas.  

Vea [apéndice D](#AppendixD) para ver una comparación de rendimiento antes y después de la optimización de Hola.

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a>Activar el registro de consultas lentas de MySQL de hello para el análisis del cuello de botella de rendimiento de Hola
registro de consultas lentas de MySQL de Hola puede ayudarle a identificar las consultas lentas de Hola de MySQL. Después de habilitar el registro de consultas lentas de MySQL de hello, también puede usar herramientas de MySQL como **mysqldumpslow** tooidentify Hola cuello de botella.  

De manera predeterminada, no está habilitado. Activar el registro de consultas lentas Hola puede consumir recursos de la CPU. Se recomienda habilitar esta opción de forma temporal para solucionar los cuellos de botella de rendimiento. tooturn en el registro de consultas lentas hello:

1. Modificar el archivo my.cnf de hello agregando Hola siguiente líneas toohello final:

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. Reinicie el servidor de MySQL de Hola.

        service  mysql  restart

3. Compruebe si la configuración de hello es surten efecto mediante el uso de Hola **mostrar** comando.

![Registro de consultas lentas ON][7]   

![Resultados del registro de consultas lentas][8]

En este ejemplo, puede ver que esa característica de consultas lentas Hola se ha activado. A continuación, puede usar hello **mysqldumpslow** herramienta toodetermine cuellos de botella de rendimiento y optimizar el rendimiento, como la adición de índices.

## <a name="appendices"></a>Apéndices
siguiente Hola es datos de prueba de rendimiento de ejemplo generados en un entorno de laboratorio de destino. Proporcionan información general de tendencia de datos de rendimiento de hello diferentes enfoques de optimización del rendimiento. Hola resultados podrían variar en diferentes versiones de entorno o el producto.

### <a name="AppendixA"></a>Apéndice A  
**Rendimiento del disco (E/S por segundo) con los distintos niveles de RAID**

![E/S por segundo de disco con los distintos niveles de RAID][9]

**Comandos de prueba**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> carga de trabajo de Hola de esta prueba utiliza 64 subprocesos, tratando de límite superior de hello tooreach de RAID.
>
>

### <a name="AppendixB"></a>Apéndice B  
**Comparación de rendimiento de MySQL con los distintos niveles de RAID**   
(sistema de archivos XFS)

![Comparación de rendimiento de MySQL con los distintos niveles de RAID][10]  
![Comparación de rendimiento de MySQL con los distintos niveles de RAID][11]

**Comandos de prueba**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

**Comparación de rendimiento (OLTP) de MySQL con los distintos niveles de RAID**  
![Comparación de rendimiento (OLTP) de MySQL con los distintos niveles de RAID][12]

**Comandos de prueba**

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a>Apéndice C   
**Comparación de rendimiento (E/S por segundo) de disco con distintos tamaños de fragmento**  
(sistema de archivos XFS)

![][13]

**Comandos de prueba**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

el tamaño de archivo Hello utilizados para esta prueba es 30 GB y 1 GB, respectivamente, con RAID 0 (4 discos) XFS sistema de archivos.

### <a name="AppendixD"></a>Apéndice D  
**Comparación de rendimiento de MySQL antes y después de la optimización**  
(sistema de archivos XFS)

![Comparación de rendimiento de MySQL antes y después de la optimización][14]

**Comandos de prueba**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**opción de configuración de Hola para predeterminado y la optimización es como sigue:**

| parameters | Valor predeterminado | Optimización |
| --- | --- | --- |
| **innodb_buffer_pool_size** |None |7 GB |
| **innodb_log_file_size** |5 MB |512 MB |
| **max_connections** |100 |5.000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 MB |128 MB |
| **query_cache_size** |16 MB |0 |

Para obtener más [parámetros de configuración de optimización](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), consulte toohello [instrucciones oficiales de MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).  

  **Entorno de prueba**  

| Hardware | Detalles |
| --- | --- |
| CPU |Procesador AMD Opteron(tm) 4171 HE/4 núcleos |
| Memoria |14 GB |
| Disco |10 GB/disco |
| SO |Ubuntu 14.04.1 LTS |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

