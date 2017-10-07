---
title: "aaaPerformance prácticas recomendadas para SQL Server en Azure | Documentos de Microsoft"
description: "Ofrece prácticas recomendadas para optimizar el rendimiento de SQL Server en máquinas virtuales de Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Procedimientos recomendados para mejorar el rendimiento de SQL Server en Máquinas virtuales de Azure

## <a name="overview"></a>Información general

En este tema se ofrecen prácticas recomendadas para optimizar el rendimiento de SQL Server en máquina virtual de Microsoft Azure. Mientras se ejecuta SQL Server en máquinas virtuales de Azure, se recomienda que siga usando Hola el mismo rendimiento de base de datos para la optimización opciones que son aplicable tooSQL servidor en el entorno de servidor local. Sin embargo, rendimiento de Hola de una base de datos relacional en una nube pública depende de muchos factores, como el tamaño de Hola de una máquina virtual y la configuración de Hola Hola de discos de datos.

Al crear imágenes de SQL Server, [considere la posibilidad de aprovisionamiento de las máquinas virtuales en el portal de Azure hello](virtual-machines-windows-portal-sql-server-provision.md). Aprovisionado en hello Portal con el Administrador de recursos de las máquinas virtuales de SQL Server implementa todas estas prácticas recomendadas, incluida la configuración de almacenamiento de Hola.

En este artículo se centra en la obtención de hello *mejor* rendimiento para SQL Server en máquinas virtuales de Azure. Si su carga de trabajo no es menos exigente, podría no necesitar todas las optimizaciones enumeradas a continuación. Tenga en cuenta sus necesidades de rendimiento y patrones de carga de trabajo a medida que evalúe estas recomendaciones.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>Lista de comprobación rápida

Hola mostramos una lista de comprobación rápida para un rendimiento óptimo de SQL Server en máquinas virtuales de Azure:

| Ámbito | Optimizaciones |
| --- | --- |
| [Tamaño de VM](#vm-size-guidance) |[DS3](../../virtual-machines-windows-sizes-memory.md) o superior para la edición SQL Enterprise.<br/><br/>[DS2](../../virtual-machines-windows-sizes-memory.md) o superior para las ediciones SQL Standard y Web. |
| [Almacenamiento](#storage-guidance) |Use [Almacenamiento premium](../../../storage/common/storage-premium-storage.md). Solo se recomienda el almacenamiento estándar en fases de desarrollo o pruebas.<br/><br/>Mantener hello [cuenta de almacenamiento](../../../storage/common/storage-create-storage-account.md) y VM de SQL Server en hello misma región.<br/><br/>Deshabilitar Azure [almacenamiento con redundancia geográfica](../../../storage/common/storage-redundancy.md) (georreplicación) en la cuenta de almacenamiento de Hola. |
| [Discos](#disks-guidance) |Use un mínimo de 2 [discos P30](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) (1 para archivos de registro; 1 para archivos de datos y TempDB).<br/><br/>Evite el uso del sistema operativo o de discos temporales para el registro o almacenamiento de bases de datos.<br/><br/>Habilitar la memoria caché de lectura en discos de hello hospeda los archivos de datos de Hola y TempDB.<br/><br/>No habilite el almacenamiento en caché en discos que hospeda el archivo de registro de hello.<br/><br/>Importante: Detener el servicio de SQL Server de hello al cambiar la configuración de la caché de Hola para un disco de máquina virtual de Azure.<br/><br/>Seccione varios rendimiento de E/S de tooget aumentado de discos de datos de Azure.<br/><br/>Formato con tamaños de asignación documentados. |
| [E/S](#io-guidance) |Habilite la compresión de páginas de bases de datos.<br/><br/>Habilite la inicialización instantánea de archivos para archivos de datos.<br/><br/>Limite o deshabilite el crecimiento automático de la base de datos de Hola.<br/><br/>Deshabilite la reducción automática de la base de datos de Hola.<br/><br/>Mueva todos los discos de toodata de las bases de datos, incluidas bases de datos del sistema.<br/><br/>Mover error registro y seguimiento de archivo directorios toodata discos de SQL Server.<br/><br/>Configure ubicaciones predeterminadas para los archivos de base de datos y de copia de seguridad.<br/><br/>Habilite páginas bloqueadas.<br/><br/>Aplique correcciones de rendimiento de SQL Server. |
| [Características específicas](#feature-specific-guidance) |Realizar una copia de almacenamiento de tooblob directamente. |

Para obtener más información sobre *cómo* y *¿por qué* toomake estas optimizaciones, revise los detalles de Hola e instrucciones indicadas en las secciones siguientes se.

## <a name="vm-size-guidance"></a>Orientación sobre el tamaño de máquina virtual

Para aplicaciones confidenciales de rendimiento, se recomienda que utilice siguiente hello [tamaños de máquinas virtuales](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**: DS3 o versiones posteriores
* **Ediciones de SQL Server Standard y Web**: DS2 o versiones posteriores

## <a name="storage-guidance"></a>Orientación sobre el almacenamiento

Las máquinas virtuales de la serie DS (además de las series DSv2 y GS) admiten [Premium Storage](../../../storage/common/storage-premium-storage.md). Almacenamiento premium es aconsejable para cargas de trabajo de producción.

> [!WARNING]
> El almacenamiento estándar presenta un ancho de banda y unas latencias variables, de modo que solo se recomienda para cargas de trabajo de desarrollo o de prueba. En las cargas de trabajo de producción conviene usar Almacenamiento premium.

Además, recomendamos que cree su cuenta de almacenamiento de Azure en hello mismo centro de datos como los retrasos de transmisión de tooreduce de máquinas virtuales de SQL Server. Al crear una cuenta de almacenamiento, deshabilite la replicación geográfica ya que no se garantiza el orden de escritura coherente entre varios discos. En su lugar, considere la posibilidad de configurar una tecnología de recuperación ante desastres de SQL Server entre dos centros de datos de Azure. Para más información, consulte [Alta disponibilidad y recuperación ante desastres para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="disks-guidance"></a>Orientación sobre los discos

En una máquina virtual de Azure hay tres tipos de disco principales:

* **Disco del sistema operativo**: cuando se crea una máquina Virtual de Azure, plataforma Hola asociará al menos un disco (con la etiqueta hello **C** unidad) toohello VM para el disco del sistema operativo. El disco es un VHD almacenado como blob en páginas en almacenamiento.
* **Disco temporal**: máquinas virtuales de Azure contienen otro disco denominado disco temporal de hello (con la etiqueta hello **d.**: unidad). Se trata de un disco en el nodo de Hola que puede usarse para el espacio de desecho.
* **Discos de datos**: también se puede adjuntar discos adicionales tooyour virtual machine como discos de datos y estos se almacenarán en el almacenamiento como blobs en páginas.

Hello las secciones siguientes describen recomendaciones sobre el uso de estos discos diferentes.

### <a name="operating-system-disk"></a>Disco del sistema operativo

Un disco del sistema operativo es un VHD que se puede arrancar y montar como una versión en ejecución de un sistema operativo y está etiquetado como la unidad **C** .

Almacenamiento en caché de la directiva en el disco del sistema operativo de Hola de manera predeterminada, es **lectura/escritura**. Para aplicaciones confidenciales de rendimiento, se recomienda utilizar discos de datos en lugar de disco del sistema operativo Hola. Vea la sección de hello en discos de datos siguiente.

### <a name="temporary-disk"></a>Disco temporal

Hola unidad de almacenamiento temporal, etiquetada como hello **d.**: unidad, no es persistente tooAzure el almacenamiento de blobs. No almacene los archivos de base de datos de usuario o de archivos de registro de transacciones de usuario en hello **d.**: unidad.

Para la serie D, Dv2-series y máquinas virtuales de serie G, unidad temporal de hello en estas máquinas virtuales está basado en SSD. Si la carga de trabajo hace un uso intensivo de TempDB (por ejemplo, para los objetos temporales o combinaciones complejas), almacenamiento de TempDB en hello **d.** unidad podría dar lugar a un mayor rendimiento de TempDB y menor latencia de TempDB.

En las máquinas virtuales que admiten Premium Storage(series DS, DSv2 y GS), se recomienda almacenar TempDB en un disco que admita Premium Storage y que tenga habilitado el almacenamiento en caché de lectura. No hay una excepción toothis recomendación; Si el uso de TempDB es escritura intensiva, puede lograr un rendimiento más alto mediante el almacenamiento de TempDB en el equipo local de hello **d.** unidad, que también está basada en SSD en estos tamaños de máquina.

### <a name="data-disks"></a>Discos de datos

* **Usar discos de datos para los archivos de datos y de registro**: como mínimo, utilice almacenamiento Premium 2 [P30 discos](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) donde un disco contiene los archivos de registro de Hola y Hola otro contiene datos de Hola y los archivos de TempDB. Cada disco de almacenamiento Premium proporciona un número de IOPs y ancho de banda (MB/s) según su tamaño, como se describe en el artículo siguiente de hello: [usando almacenamiento Premium para discos](../../../storage/common/storage-premium-storage.md).

* **Seccionamiento de discos**: para disfrutar de un mayor rendimiento, puede agregar más discos de datos y usar el seccionamiento de discos. número de hello toodetermine de discos de datos, debe tooanalyze número de Hola de IOPS y ancho de banda necesario para los archivos de registro y para los datos y los archivos de TempDB. Observe que diferentes tamaños de máquinas virtuales tienen distintos límites en serie de Hola de IOPs y ancho de banda compatible, consulte las tablas de hello en IOPS por [tamaño de máquina virtual](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Usar hello siguientes instrucciones:

  * Para Windows 8/Windows Server 2012 o posterior, use [espacios de almacenamiento](https://technet.microsoft.com/library/hh831739.aspx) con hello siguientes instrucciones:

      1. Conjunto Hola intercalar (tamaño de stripe) too64 KB (65536 bytes) para las cargas de trabajo OLTP y de 256 KB (262144 bytes) para el impacto de rendimiento de las cargas de trabajo tooavoid debido toopartition desalineación de almacenamiento de datos. Esta característica debe establecerse con PowerShell.
      1. Establezca recuento de columnas = número de discos físicos. Use PowerShell (no la interfaz de usuario del Administrador del servidor) al configurar más de 8 discos. 

    Por ejemplo, hello después de PowerShell crea un nuevo grupo de almacenamiento con hello intercalar tamaño too64 KB y Hola el número de columnas too2:

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Para Windows 2008 R2 o versiones anteriores, puede usar discos dinámicos (volúmenes seccionados del SO) y tamaño de sección de hello siempre es 64 KB. Tenga en cuenta que esta opción es obsoleta a partir de Windows 8/Windows Server 2012. Para obtener información, vea la declaración de soporte técnico de hello en [servicio de disco Virtual se encuentra en transición tooWindows API de administración de almacenamiento](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx).

  * Si su carga de trabajo no es intensiva de registro y no necesita IOP dedicadas, puede configurar solo un grupo de almacenamiento. De lo contrario, cree dos grupos de almacenamiento, uno para los archivos de registro de hello y otro grupo de almacenamiento para los archivos de datos de Hola y TempDB. Determinar el número de Hola de discos asociados a cada grupo de almacenamiento en función de sus expectativas de carga. Tenga en cuenta que diferentes tamaños de máquina virtual permiten diferentes números de discos de datos conectados. Para más información, consulte [Tamaños de las máquinas virtuales Linux en Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

  * Si no están usando almacenamiento Premium (escenarios de desarrollo y pruebas), recomendación de hello es el número máximo de hello tooadd de discos de datos admitidos por la [tamaño de máquina virtual](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y usar la creación de bandas en disco.

* **Directiva de caché**: discos de datos para el almacenamiento Premium, habilitar la memoria caché de lectura en los discos de datos de hello hospedaje sólo los archivos de datos y TempDB. Si no usa el Almacenamiento premium, no habilite el almacenamiento en caché en los discos de datos. Para obtener instrucciones acerca de cómo configurar la caché de disco, vea Hola temas siguientes: [Set-AzureOSDisk](https://msdn.microsoft.com/library/azure/jj152847) y [Set-AzureDataDisk](https://msdn.microsoft.com/library/azure/jj152851.aspx).

  > [!WARNING]
  > Detenga el servicio de SQL Server de hello al cambiar la configuración de caché de Hola de posibilidad de Hola de tooavoid de discos de máquina virtual de Azure de cualquier daño de la base de datos.

* **Tamaño de unidad de asignación de NTFS**: al formatear el disco de datos de hello, se recomienda que use un tamaño de unidad de asignación de 64 KB para los archivos de datos y de registro, así como en TempDB.

* **Prácticas recomendadas de administración de discos**: al quitar un disco de datos o cambiar su memoria caché escribe, detenga el servicio de SQL Server de Hola durante el cambio de Hola. Cuando la configuración de almacenamiento en caché de hello es cambiado en el disco de SO hello, Azure detiene Hola VM, cambia el tipo de caché de Hola y reinicia Hola máquina virtual. Cuando se cambia la configuración de la caché de Hola de un disco de datos, Hola VM no se detiene, pero el disco de datos de Hola se separa de hello VM durante Hola cambiar y, a continuación, volver a adjuntar.

  > [!WARNING]
  > Hola de toostop error servicio de SQL Server durante estas operaciones puede ocasionar daños en base de datos.

## <a name="io-guidance"></a>Orientación sobre E/S

* Hola obtener los mejores resultados con el almacenamiento Premium se obtienen cuando se paraleliza la aplicación y las solicitudes. Almacenamiento Premium está diseñado para escenarios donde la profundidad de cola de E/S de hello es mayor que 1, por lo que verá poca o ninguna ganancias de rendimiento para solicitudes de serie de un único subproceso (incluso si están intensivas de almacenamiento). Por ejemplo, esto podría afectar a los resultados de pruebas de un único subproceso de Hola de herramientas de análisis de rendimiento, como SQLIO.

* Recuerde que también puede usar la [compresión de páginas de bases de datos](https://msdn.microsoft.com/library/cc280449.aspx) , ya que puede ayudarle a mejorar el rendimiento de las cargas de trabajo intensivas de E/S. Sin embargo, la compresión de datos Hola puede aumentar el consumo de CPU de hello en el servidor de base de datos de Hola.

* Considere la posibilidad de habilitar la instantánea de archivos inicialización tooreduce Hola tiempo necesario para la asignación de archivo inicial. ventajas de tootake de inicialización instantánea de archivos, conceda a cuenta de servicio de SQL Server (MSSQLSERVER) Hola con SE_MANAGE_VOLUME_NAME y agréguela toohello **realizar tareas de mantenimiento del volumen** directiva de seguridad. Si está utilizando una imagen de plataforma de SQL Server para Azure, cuenta de servicio de hello predeterminada (NT Service\MSSQLSERVER) no se agrega toohello **realizar tareas de mantenimiento del volumen** directiva de seguridad. En otras palabras, la inicialización instantánea de archivos no se habilita en una imagen de plataforma de SQL Server Azure. Después de agregar toohello de cuenta de servicio de SQL Server de hello **realizar tareas de mantenimiento del volumen** directiva de seguridad, reinicie el servicio de SQL Server de Hola. Puede haber consideraciones de seguridad para usar esta característica. Para obtener más información, consulte [Inicialización de archivos de base de datos](https://msdn.microsoft.com/library/ms175935.aspx).

* **crecimiento automático** se considera toobe apenas una contingencia para el crecimiento inesperado. No administre su crecimiento de datos y registros a diario con el crecimiento automático. Si usa el crecimiento automático, aumente previamente archivo hello con conmutador de tamaño de Hola.

* Asegúrese de que **autoshrink** es tooavoid deshabilitado una sobrecarga innecesaria que puede afectar negativamente al rendimiento.

* Mueva todos los discos de toodata de las bases de datos, incluidas bases de datos del sistema. Para más información, consulte [Mover bases de datos del sistema](https://msdn.microsoft.com/library/ms345408.aspx).

* Mover error registro y seguimiento de archivo directorios toodata discos de SQL Server. Para llevar esto a cabo en el Administrador de configuración de SQL Server, haga clic con el botón secundario en la instancia de SQL Server y seleccione Propiedades. Hello configuración del archivo de registro y seguimiento de errores puede cambiarse en hello **parámetros de inicio** Hola ficha directorio de volcado de memoria especificado en hello **avanzadas** Hola de ficha siguiente captura de pantalla muestra dónde toolook para parámetro de inicio de registro de errores de Hola.

    ![Captura de pantalla de registro de errores de SQL](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* Configure ubicaciones predeterminadas para los archivos de base de datos y de copia de seguridad. Uso de las recomendaciones de hello en este tema y realizar cambios de hello en la ventana de propiedades de servidor de Hola. Para obtener instrucciones, consulte [Hola ver o cambiar las ubicaciones predeterminadas para los datos y archivos de registro (SQL Server Management Studio)](https://msdn.microsoft.com/library/dd206993.aspx). Hello captura de pantalla siguiente muestra dónde toomake estos cambios.

    ![Archivos de copia de seguridad y de registro de datos de SQL](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* Habilitar bloquea páginas tooreduce E/S y las actividades de paginación. Para obtener más información, consulte [habilitar Hola opción Bloquear páginas en memoria (Windows)](https://msdn.microsoft.com/library/ms190730.aspx).

* Si está ejecutando SQL Server 2012, instale la actualización acumulativa 10 del Service Pack 1. Esta actualización contiene la revisión de hello para el bajo rendimiento de e/s al ejecutar select en la instrucción de la tabla temporal en SQL Server 2012. Para obtener información, consulte este [artículo de Knowledge Base](http://support.microsoft.com/kb/2958012).

* Considere la posibilidad de comprimir los archivos de datos cuando se transfieren dentro y fuera de Azure.

## <a name="feature-specific-guidance"></a>Orientación sobre las características específicas

Algunas implementaciones pueden lograr ventajas de rendimiento adicionales mediante técnicas de configuración más avanzadas. Hello siguiente lista resalta algunas características de SQL Server que pueden ayudar a mejorar el rendimiento tooachieve:

* **Copia de seguridad de almacenamiento de tooAzure**: al realizar copias de seguridad para SQL Server en máquinas virtuales de Azure, puede usar [tooURL de copia de seguridad de SQL Server](https://msdn.microsoft.com/library/dn435916.aspx). Esta característica está disponible a partir de SQL Server 2012 SP1 CU2 y es recomendable para realizar copias de seguridad toohello adjuntada los discos de datos. Cuando se copia de seguridad/restauración a/desde el almacenamiento de Azure, siga las recomendaciones de hello proporcionadas en [copias de seguridad de SQL Server tooURL las prácticas recomendadas y solución de problemas y restauración de copias de seguridad se almacenan en el almacenamiento de Azure](https://msdn.microsoft.com/library/jj919149.aspx). También puede automatizar estas copias de seguridad con [copia de seguridad automatizada para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).

    TooSQL anterior Server 2012, puede usar [tooAzure herramienta de copia de seguridad de SQL Server](https://www.microsoft.com/download/details.aspx?id=40740). Esta herramienta puede ayudar a rendimiento de copia de seguridad de tooincrease con varios destinos de copia de seguridad de las bandas.

* **Archivos de datos de SQL Server en Azure**: esta nueva característica, [Archivos de datos de SQL Server en Azure](https://msdn.microsoft.com/library/dn385720.aspx), está disponible a partir de SQL Server 2014. La ejecución de SQL Server con archivos de datos en Azure muestra características de rendimiento comparables con el uso de discos de datos de Azure.

## <a name="next-steps"></a>Pasos siguientes

Para ver prácticas recomendadas de seguridad, vea [Consideraciones de seguridad para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-security.md).

Revise otros temas de la máquina virtual de SQL Server en [Información general de SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).
