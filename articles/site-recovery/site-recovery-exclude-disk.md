---
title: "discos aaaExclude de protección mediante el uso de Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo y por qué tooexclude VM discos de la replicación para escenarios de tooAzure de VMware y Hyper-V tooAzure."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>Excluir discos de la replicación
Este artículo describe cómo tooexclude discos de la replicación. Esta exclusión puede optimizar el ancho de banda de replicación de hello consumido u optimizar los recursos del lado de destino de Hola que utilizan estos discos. característica de Hola se admite para escenarios de tooAzure de VMware y Hyper-V tooAzure.

## <a name="prerequisites"></a>Requisitos previos

De manera predeterminada, se replican todos los discos de una máquina. tooexclude un disco de la replicación, debe instalar manualmente Hola servicio de movilidad en la máquina de hello antes de habilitar la replicación si se están replicando desde tooAzure de VMware.


## <a name="why-exclude-disks-from-replication"></a>¿Por qué excluir discos de la replicación?
A menudo es necesario excluir discos de replicación porque:

- datos de Hola que creadas en el disco de hello excluido no son importantes o no necesitan toobe replicado.

- Recursos de red y almacenamiento de toosave que desee por no replicar este renovación.

## <a name="what-are-hello-typical-scenarios"></a>¿Cuáles son los escenarios típicos de hello?
Encontrará ejemplos específicos de datos renovados que son estupendos candidatos para la exclusión. Algunos ejemplos son los escribe tooa archivo de paginación (pagefile.sys) y escribe el archivo de tempdb toohello de Microsoft SQL Server. Dependiendo de la carga de trabajo de Hola y el subsistema de almacenamiento de hello, archivo de paginación de hello puede registrar una cantidad significativa de renovación. Sin embargo, replicar estos datos de hello sitio primario tooAzure sería consumen muchos recursos. Por lo tanto, puede usar Hola después de la replicación de toooptimize de pasos de una máquina virtual con un único disco virtual que tiene el sistema operativo de Hola y el archivo de paginación de hello:

1. Dividir el disco virtual única de hello en dos discos virtuales. Un disco virtual con sistema operativo de Hola y Hola otro tiene un archivo de paginación de Hola.
2. Excluir el disco del archivo de paginación de hello de la replicación.

De forma similar, puede utilizar Hola siguiendo los pasos toooptimize un disco con ambos tempdb de Microsoft SQL Server de Hola a memoria y Hola archivo de base de datos del sistema:

1. Mantener base de datos de sistema de Hola y tempdb en dos discos diferentes.
2. Excluir el disco de tempdb de hello de la replicación.

## <a name="how-tooexclude-disks-from-replication"></a>¿Cómo tooexclude discos de la replicación?

### <a name="vmware-tooazure"></a>TooAzure de VMware
Siga hello [habilitar la replicación](site-recovery-vmware-to-azure.md) tooprotect una máquina virtual desde el portal de Azure Site Recovery Hola de flujo de trabajo. En el paso cuarto de Hola de flujo de trabajo de hello, usar hello **tooREPLICATE disco** discos tooexclude de columna de la replicación. De forma predeterminada se seleccionan todos los discos para la replicación. Desactive la casilla de verificación de Hola de discos que desea tooexclude de replicación y, a continuación, completa Hola pasos tooenable.

![Excluir los discos de la replicación y habilitar la replicación de conmutación por recuperación de VMware tooAzure](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * Puede excluir solo los discos que ya tienen instalado el servicio de movilidad de Hola. Necesita servicio de movilidad de toomanually instalación hello, porque Hola servicio de movilidad solo se instala utilizando el mecanismo de inserción de hello después de la replicación está habilitada.
> * Solo se pueden excluir los discos básicos de la replicación. No se pueden excluir los discos dinámicos ni del sistema operativo.
> * Una vez habilitada la replicación, no puede agregar ni quitar discos de la replicación. Si desea tooadd o excluir un disco, necesita toodisable protección de máquina de hello y, a continuación, vuelva a habilitarla.
> * Si excluye un disco que se necesita para una aplicación toooperate, después de la conmutación por error tooAzure, necesitará el disco de Hola de toocreate manualmente en Azure para que pueda ejecutar la aplicación hello replicado. O bien, puede integrar la automatización de Azure en un disco de recuperación plan toocreate Hola durante la conmutación por error de la máquina de Hola.
> * Máquina virtual Windows: no se producirá una conmutación por recuperación de los discos creados manualmente en Azure. Por ejemplo, si realiza la conmutación por error de tres discos y crea dos directamente en Azure Virtual Machines, solo los tres discos que se conmutaran por error se conmutarán por recuperación. No se incluyen discos que haya creado manualmente en la conmutación por recuperación o en reprotección de tooAzure local.
> * Máquina virtual Linux: se producirá una conmutación por recuperación de los discos creados manualmente en Azure. Por ejemplo, si realiza una conmutación por error de tres discos y crea dos directamente en Azure Virtual Machines, los cinco experimentarán conmutación por recuperación. No se pueden excluir discos creados manualmente de la conmutación por recuperación.
>

### <a name="hyper-v-tooazure"></a>TooAzure de Hyper-V
Siga hello [habilitar la replicación](site-recovery-hyper-v-site-to-azure.md) tooprotect una máquina virtual desde el portal de Azure Site Recovery Hola de flujo de trabajo. En el paso cuarto de Hola de flujo de trabajo de hello, usar hello **tooREPLICATE disco** discos tooexclude de columna de la replicación. De forma predeterminada se seleccionan todos los discos para la replicación. Desactive la casilla de verificación de Hola de discos que desea tooexclude de replicación y, a continuación, completa Hola pasos tooenable.

![Excluir los discos de la replicación y habilitar la replicación de conmutación por recuperación de Hyper-V tooAzure](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * De la replicación solo se pueden excluir discos básicos. No se pueden excluir los discos del sistema operativo. Se recomienda no excluir discos dinámicos. Azure Site Recovery no se puede identificar qué disco duro virtual (VHD) es básico o dinámico en máquina virtual de hello invitado.  Si no se excluyen todos los discos de los volúmenes dinámicos dependientes, disco dinámico protegido de Hola se convierte en un disco con errores en una máquina virtual de conmutación por error y hello datos en ese disco no están accesibles.
> * Una vez habilitada la replicación, no puede agregar ni quitar discos de la replicación. Si desea que tooadd o excluir un disco, se necesita protección toodisable para la máquina virtual de hello y, a continuación, vuelva a habilitarla.
> * Si excluye un disco que se necesita para una aplicación toooperate, después de la conmutación por error tooAzure necesitará toocreate Hola disco manualmente en Azure para que pueda ejecutar la aplicación hello replicado. O bien, puede integrar la automatización de Azure en un disco de recuperación plan toocreate Hola durante la conmutación por error de la máquina de Hola.
> * No se producirá una conmutación por recuperación de los discos creados manualmente en Azure. Por ejemplo, si se producirá un error en más de tres discos y crear dos discos directamente en máquinas virtuales de Azure, solo tres discos que se han conmutado por error desde Azure tooHyper-V. No se incluyen discos que se hayan creado manualmente en la conmutación por recuperación o en la replicación inversa de Hyper-V tooAzure.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>Escenarios completos de exclusión de discos
Veamos característica disco toounderstand Hola exclusión de dos escenarios:

- Disco de la base de datos tempdb de SQL Server
- Disco del archivo de paginación (pagefile.sys)

### <a name="exclude-hello-sql-server-tempdb-disk"></a>Excluir el disco de tempdb de SQL Server de Hola
Veamos una máquina virtual de SQL Server con una base de datos tempdb que se puede excluir.

nombre de Hola de disco virtual de hello es SalesDB.

Discos de máquina virtual de origen de hello son los siguientes:


**Nombre del disco** | **Sistema operativo invitado** | **Unidad** | **Tipo de datos en el disco de Hola**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco del sistema operativo
DB-Disk1| Disk1 | D:\ | Base de datos del sistema SQL y Database1 del usuario
DB-disco 2 (disco de hello excluidos de la protección) | Disk2 | E:\ | Archivos temporales
DB-disco 3 (disco de hello excluidos de la protección) | Disk3 | F:\ | Base de datos de tempdb SQL (ruta de acceso de carpeta (F:\MSSQL\Data\) < /br/>< /br/> anote la ruta de acceso de carpeta de hello antes de la conmutación por error.
DB-Disk4 | Disk4 |G:\ |Database2 del usuario

Dado que la renovación de datos en dos discos de máquina virtual de hello es temporal, al mismo tiempo que protege la máquina virtual de hello SalesDB, excluir el disco 2 y disco3 de la replicación. Azure Site Recovery no replicará esos discos. En la conmutación por error, los discos no estará presentes en la máquina de conmutación por error de hello en Azure.

Los discos de máquina virtual de Azure después de la conmutación por error de hello son los siguientes:

**Sistema operativo invitado** | **Unidad** | **Tipo de datos en el disco de Hola**
--- | --- | ---
DISK0 | C:\ | Disco del sistema operativo
Disk1 | E:\ | Almacenamiento temporal < /br / >< /br / > Azure agrega este disco y asigna la primera letra de unidad disponible Hola.
Disk2 | D:\ | Base de datos del sistema SQL y Database1 del usuario
Disk3 | G:\ | Database2 del usuario

Dado que disco 2 y disco3 se han excluido de la máquina virtual de hello SalesDB, E: es primera letra de unidad hello en lista de hello disponibles. Azure asigna el volumen de almacenamiento temporal de toohello E:. Para todos los discos de saludo replican, permanecen letras de unidad de Hola Hola igual.

Disco 3, que era el disco de tempdb SQL de hello (ruta de acceso de carpeta de tempdb F:\MSSQL\Data\), se ha excluido de la replicación. Hola disco no está disponible en la máquina virtual de conmutación por error de Hola. Como resultado, Hola servicio SQL está en un estado detenido y necesita la ruta de acceso de F:\MSSQL\Data de Hola.

Hay dos toocreate de formas de esta ruta de acceso:

- Agregar un disco nuevo y asignar la ruta de acceso de carpeta de tempdb.
- Use un disco de almacenamiento temporal existente para la ruta de acceso de carpeta de hello tempdb.

#### <a name="add-a-new-disk"></a>Incorporación de un disco nuevo:

1. Anote las rutas de acceso de Hola de SQL tempdb.mdf y tempdb.ldf antes de la conmutación por error.
2. De hello portal de Azure, agregar una nueva máquina virtual de disco toohello conmutación por error con hello igual o aumentar el tamaño como del disco de tempdb SQL de origen de hello (disco 3).
3. Inicie sesión en toohello máquina virtual de Azure. Desde la consola de administración (diskmgmt.msc) de disco de hello, Hola inicializar y formato recién había agregado disco.
4. Asignar Hola misma letra que se usó por disco de tempdb SQL de hello (F:) de la unidad.
5. Cree una carpeta de tempdb en hello volumen F: (F:\MSSQL\Data).
6. Iniciar el servicio SQL de Hola Hola consola del servicio.

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>Use un disco de almacenamiento temporal existente para la ruta de acceso de carpeta de hello SQL tempdb:

1. Abra el símbolo del sistema.
2. Ejecute SQL Server en modo de recuperación Hola desde línea de comandos.

        Net start MSSQLSERVER /f / T3608

3. Ejecute hello después sqlcmd toochange Hola tempdb toohello nueva ruta de acceso.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Detenga el servicio de Microsoft SQL Server de Hola.

        Net stop MSSQLSERVER
5. Iniciar servicio de Microsoft SQL Server de Hola.

        Net start MSSQLSERVER

Consulte toohello siguiendo las directrices de Azure para el disco de almacenamiento temporal:

* [Uso de SSD en máquinas virtuales de Azure toostore TempDB de SQL Server y extensiones de grupo de búferes](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Procedimientos recomendados para SQL Server en Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-tooan-on-premises-host"></a>Conmutación por recuperación (de host local de Azure tooan)
Ahora debemos tener claro discos Hola que se replican Cuando la conmutación por error del host de Hyper-V o VMware locales tooyour de Azure. Los discos creados manualmente en Azure no se replicarán. Por ejemplo, si realiza la conmutación por error de tres discos y crea dos directamente en Azure Virtual Machines, solo los tres discos que se conmutaran por error se conmutarán por recuperación. No se incluyen discos que se hayan creado manualmente en la conmutación por recuperación o en reprotección de tooAzure local. No replica los hosts de tooon local de disco de almacenamiento temporal de Hola.

#### <a name="failback-toooriginal-location-recovery"></a>Recuperación de la ubicación de conmutación por recuperación toooriginal

En el ejemplo anterior de hello, configuración de disco de máquina virtual de Azure de hello es la siguiente:

**Sistema operativo invitado** | **Unidad** | **Tipo de datos en el disco de Hola**
--- | --- | ---
DISK0 | C:\ | Disco del sistema operativo
Disk1 | E:\ | Almacenamiento temporal < /br / >< /br / > Azure agrega este disco y asigna la primera letra de unidad disponible Hola.
Disk2 | D:\ | Base de datos del sistema SQL y Database1 del usuario
Disk3 | G:\ | Database2 del usuario


#### <a name="vmware-tooazure"></a>TooAzure de VMware
Cuando la conmutación por recuperación se realiza la ubicación original de toohello, configuración de disco de máquina virtual de conmutación por recuperación de hello no tiene discos excluidos. Los discos que se han excluido de VMware tooAzure no estará disponibles en la máquina virtual de conmutación por recuperación de Hola.

Después de la conmutación por error planeada desde Azure local tooon VMware, discos de máquina virtual de VMWare hello (ubicación original) son los siguientes:

**Sistema operativo invitado** | **Unidad** | **Tipo de datos en el disco de Hola**
--- | --- | ---
DISK0 | C:\ | Disco del sistema operativo
Disk1 | D:\ | Base de datos del sistema SQL y Database1 del usuario
Disk2 | G:\ | Database2 del usuario

#### <a name="hyper-v-tooazure"></a>TooAzure de Hyper-V
Cuando la conmutación por recuperación es la ubicación original de toohello, Hola conmutación por recuperación máquina virtual disco configuración permanece Hola igual que el de la configuración original del disco de máquina virtual de Hyper-V. Los discos que se han excluido de tooAzure de sitio de Hyper-V están disponibles en la máquina virtual de conmutación por recuperación de Hola.

Después de la conmutación por error planeada de Hyper-V de Azure tooon-local, discos de máquina virtual de Hyper-V hello (ubicación original) son los siguientes:

**Nombre del disco** | **Sistema operativo invitado** | **Unidad** | **Tipo de datos en el disco de Hola**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | Disco del sistema operativo
DB-Disk1 | Disk1 | D:\ | Base de datos del sistema SQL y Database1 del usuario
DB-Disk2 (disco excluido) | Disk2 | E:\ | Archivos temporales
DB-Disk3 (disco excluido) | Disk3 | F:\ | Base de datos tempdb de SQL (ruta de acceso de carpeta): F:\MSSQL\Data\)
DB-Disk4 | Disk4 | G:\ | Database2 del usuario


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>Excluir Hola paginación (pagefile.sys) del archivo disco

Veamos una máquina virtual con un disco del archivo de paginación que se puede excluir.
Hay dos casos.

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>Caso 1: el archivo de paginación de hello está configurado en hello unidad D:
Esta es la configuración de disco de hello:


**Nombre del disco** | **Sistema operativo invitado** | **Unidad** | **Tipo de datos en el disco de Hola**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco del sistema operativo
DB-Disco1 (disco de hello excluidos de la protección de hello) | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Datos del usuario 1
DB-Disk3 | Disk3 | F:\ | Datos del usuario 2

Estos son configuración de archivo de hello paginación en la máquina virtual de origen de hello:

![Configuración del archivo de paginación en la máquina virtual de origen](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


Después de la conmutación por error de la máquina virtual de Hola de VMware tooAzure o tooAzure de Hyper-V, los discos de máquina virtual de Azure Hola son los siguientes:

**Nombre del disco** | **Sistema operativo invitado** | **Unidad** | **Tipo de datos en el disco de Hola**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco del sistema operativo
DB-Disk1 | Disk1 | D:\ | Almacenamiento temporal</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Datos del usuario 1
DB-Disk3 | Disk3 | F:\ | Datos del usuario 2

Ya se ha excluido Disco1 (D:), D: es primera letra de unidad hello en lista de hello disponibles. Azure asigna el volumen de almacenamiento temporal de toohello D:. Como D: está disponible en la máquina virtual de Azure hello, Hola configuración del archivo paginación Hola de hello máquina virtual permanece igual.

Estos son configuración de archivo paginación hello en hello máquina virtual de Azure:

![Configuración del archivo de paginación en la máquina virtual de Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>Caso 2: archivo de paginación de hello está configurado en otra unidad (distintos de la unidad D:)

Esta es la configuración de disco de máquina virtual de origen de hello:

**Nombre del disco** | **Sistema operativo invitado** | **Unidad** | **Tipo de datos en el disco de Hola**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco del sistema operativo
DB-Disco1 (disco de hello excluidos de la protección) | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Datos del usuario 1
DB-Disk3 | Disk3 | F:\ | Datos del usuario 2

Estos son configuración de archivo de hello paginación en la máquina virtual de hello local:

![Configuración de máquina virtual de hello local de archivo de paginación](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

Después de la conmutación por error de la máquina virtual de Hola de tooAzure VMware/Hyper-V, los discos de máquina virtual de Azure Hola son los siguientes:

**Nombre del disco**| **Sistema operativo invitado**| **Unidad** | **Tipo de datos en el disco de Hola**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |Disco del sistema operativo
DB-Disk1 | Disk1 | D:\ | Almacenamiento temporal</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Datos del usuario 1
DB-Disk3 | Disk3 | F:\ | Datos del usuario 2

Porque D: es la primera letra de unidad Hola de lista disponibles hello, Azure asigna el volumen de almacenamiento temporal de toohello D:. Para todos los discos de saludo replican, sigue siendo de letra de unidad de Hola Hola igual. Porque Hola G: disco no está disponible, el sistema de hello usará la unidad C: de Hola para hello archivo de paginación.

Estos son configuración de archivo paginación hello en hello máquina virtual de Azure:

![Configuración del archivo de paginación en la máquina virtual de Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>Pasos siguientes
Después de que la implementación esté configurada y en ejecución, [obtenga más información](site-recovery-failover.md) sobre los diferentes tipos de conmutación por error.
