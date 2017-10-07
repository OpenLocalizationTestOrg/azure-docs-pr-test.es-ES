---
title: "aaaMigrate un tooSQL de base de datos de servidor de SQL Server en una máquina virtual | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomigrate un usuario local de la base de datos tooSQL Server en una máquina virtual de Azure."
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>Migrar un tooSQL de base de datos de servidor de SQL Server en una máquina virtual de Azure

Hay una serie de métodos toomigrate un tooSQL de la base de datos de usuario de SQL Server local Server en una máquina virtual de Azure. En este artículo se tratan diversos métodos brevemente y se recomienda mejor método para diversos escenarios de Hola.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>¿Cuáles son los métodos de migración principal de hello?
métodos de migración principal Hola son:

* Realizar copia de seguridad local mediante la compresión y manualmente el archivo de copia de seguridad de copia hello en hello máquina virtual de Azure
* Realizar una copia de seguridad tooURL y restauración en la máquina virtual de Azure desde la dirección URL de Hola Hola
* Separar y, a continuación, copie Hola datos y registro archivos tooAzure almacenamiento de blobs y, a continuación, adjuntar tooSQL Server en VM de Azure de dirección URL
* Convertir físico local máquina VHD tooHyper-V, cargar el almacenamiento de blobs de tooAzure e implementar, a continuación, tal y como nueva máquina virtual utilizando carga VHD
* Enviar la unidad de disco duro de envío con el servicio de importación y exportación de Windows
* Si tiene una implementación AlwaysOn local, use hello [Asistente para agregar réplica de Azure](../classic/sql-onprem-availability.md) toocreate una réplica en Azure y, a continuación, la conmutación por error, que señala la instancia de base de datos de Azure de toohello de usuarios
* Usar SQL Server [la replicación transaccional](https://msdn.microsoft.com/library/ms151176.aspx) tooconfigure hello Azure SQL Server de la instancia como un suscriptor y, a continuación, deshabilite la replicación, que señala la instancia de base de datos de Azure de toohello de usuarios

> [!TIP]
> También puede usar estas mismas bases de datos de toomove de técnicas entre las máquinas virtuales de SQL Server en Azure. Por ejemplo, no hay ningún tooupgrade forma una VM de la imagen de la Galería de SQL Server desde una tooanother/edición de la versión. En este caso, debe crear una nueva VM de SQL Server con la nueva versión o edición de hello y, a continuación, utilice una de las técnicas de migración de hello en este artículo toomove las bases de datos. 

## <a name="choosing-your-migration-method"></a>Elección del método de migración
Para el rendimiento de la transferencia de datos óptima, migrar los archivos de base de datos de hello en hello VM de Azure mediante un archivo de copia de seguridad comprimido.

toominimize tiempo de inactividad durante el proceso de migración de base de datos de hello, use opciones Hola AlwaysOn u Hola la replicación transaccional.

Si no es posible toouse Hola por encima de los métodos, migrar manualmente la base de datos. Con este método, se normalmente se empieza con una copia de seguridad de base de datos seguida de una copia de copia de seguridad de base de datos de hello en Azure y, a continuación, realizar una restauración de base de datos. Puede copiar los archivos de base de datos de Hola a sí mismos en Azure y, después, conéctelas. Existen varios métodos para llevar a cabo este proceso manual de migración de una base de datos a una VM de Azure.

> [!NOTE]
> Cuando se actualiza tooSQL Server 2014 o SQL Server 2016 desde versiones anteriores de SQL Server, debe considerar si es necesario realizar cambios. Se recomienda solucionar todas las dependencias de características no admitidas por hello nueva versión de SQL Server como parte de su proyecto de migración. Para obtener más información sobre los escenarios y las ediciones de hello admite, consulte [actualizar tooSQL Server](https://msdn.microsoft.com/library/bb677622.aspx).

Hello en la tabla siguiente muestra cada uno de los métodos de migración principal de Hola y describe cuándo es apropiado más el uso de Hola de cada método.

| Método | Versión de base de datos de origen | Versión de base de datos de destino | Restricción del tamaño de copia de seguridad de la base de datos de origen | Notas |
| --- | --- | --- | --- | --- |
| [Realizar copia de seguridad local mediante la compresión y manualmente el archivo de copia de seguridad de copia hello en hello máquina virtual de Azure](#backup-and-restore) |SQL Server 2005 o superior |SQL Server 2005 o superior |[Límite de almacenamiento de máquina virtual de Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Se trata de una técnica muy sencilla y probada para mover bases de datos entre máquinas. |
| [Realizar una copia de seguridad tooURL y restauración en la máquina virtual de Azure desde la dirección URL de Hola Hola](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 o superior |SQL Server 2012 SP1 CU2 o superior |< 12,8 TB para SQL Server 2016, de lo contrario < 1 TB | Este método es simplemente otra manera toomove Hola archivo de copia de seguridad toohello máquinas virtuales con almacenamiento de Azure. |
| [Separar y, a continuación, copie Hola datos y registro archivos tooAzure almacenamiento de blobs y, a continuación, adjuntar tooSQL Server en máquina virtual de Azure de dirección URL](#detach-and-attach-from-url) |SQL Server 2005 o superior |SQL Server 2014 o superior |[Límite de almacenamiento de máquina virtual de Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Utilice este método cuando planee demasiado[almacenar estos archivos con el servicio de almacenamiento de blobs de Azure de hello](https://msdn.microsoft.com/library/dn385720.aspx) y conéctelas tooSQL Server ejecuta en una máquina virtual de Azure, especialmente con las bases de datos muy grandes |
| [Convertir en local máquina V tooHyper discos duros virtuales, cargar el almacenamiento de blobs de tooAzure y, a continuación, implementar una nueva máquina virtual mediante VHD cargado](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 o superior |SQL Server 2005 o superior |[Límite de almacenamiento de máquina virtual de Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Se utiliza si [seguir usando su propia licencia de SQL Server](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), al migrar una base de datos que se va a ejecutar en una versión anterior de SQL Server o al sistema a migrar y las bases de datos de usuario conjuntamente como parte de Hola migración de base de datos depende de otra bases de datos de usuario o las bases de datos del sistema. |
| [Envío de unidad de disco duro con el servicio de importación y exportación de Windows](#ship-hard-drive) |SQL Server 2005 o superior |SQL Server 2005 o superior |[Límite de almacenamiento de máquina virtual de Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Hola de uso [servicio de importación y exportación de Windows](../../../storage/common/storage-import-export-service.md) cuando es demasiado lento, como con bases de datos muy grandes manual copy (método) |
| [Use Hola Asistente para agregar réplica de Azure](../classic/sql-onprem-availability.md) |SQL Server 2012 o superior |SQL Server 2012 o superior |[Límite de almacenamiento de máquina virtual de Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Minimiza el tiempo de inactividad; utilícelo cuando tenga una implementación local de AlwaysOn |
| [Uso de la replicación transaccional de SQL Server](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 o superior |SQL Server 2005 o superior |[Límite de almacenamiento de máquina virtual de Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Utilice esta opción cuando tenga tiempo de inactividad de toominimize y no tiene una implementación local de AlwaysOn |

## <a name="backup-and-restore"></a>Copia de seguridad y restauración
La base de datos con la compresión de copia de seguridad copie toohello de copia de seguridad de hello VM y, a continuación, restaure la base de datos de Hola. Si el archivo de copia de seguridad es mayor que 1 TB, debe seccionar porque Hola tamaño máximo de un disco de máquina virtual es 1 TB. Usar hello siguiendo los pasos generales toomigrate una base de datos de usuario con este método manual:

1. Realizar una ubicación de base de datos completa tooan copia de seguridad local.
2. Crear o cargar una máquina virtual con la versión de Hola de SQL Server deseado.
3. Configure la conectividad según sus requisitos. Vea [conectar tooa Máquina Virtual de SQL Server en Azure (Administrador de recursos)](virtual-machines-windows-sql-connect.md).
4. Copiar la máquina virtual de los archivos de copia de seguridad tooyour mediante el comando de copia remota de escritorio, el Explorador de Windows u Hola desde un símbolo del sistema.

## <a name="backup-toourl-and-restore"></a>TooURL copia de seguridad y restauración
En lugar de copia de seguridad tooa de archivos local, puede usar hello [tooURL copia de seguridad](https://msdn.microsoft.com/library/dn435916.aspx) y, a continuación, restaurar a partir de la dirección URL toohello máquina virtual. Con SQL Server 2016, conjuntos de copia de seguridad con bandas se admiten, se recomiendan para obtener un rendimiento y requiere los límites de tamaño de hello tooexceed por blob. Para las bases de datos muy grandes, Hola uso de hello [servicio de importación y exportación de Windows](../../../storage/common/storage-import-export-service.md) se recomienda.

## <a name="detach-and-attach-from-url"></a>Desasociación y asociación desde una dirección URL
Separar los archivos de registro y base de datos y transferirlos demasiado[almacenamiento de blobs de Azure](https://msdn.microsoft.com/library/dn385720.aspx). A continuación, adjuntar base de datos de Hola de dirección URL de hello en la VM de Azure. Utilice esta opción si desea tooreside de archivos de base de datos física hello en almacenamiento de blobs. Esto podría ser útil para bases de datos muy grandes. Usar hello siguiendo los pasos generales toomigrate una base de datos de usuario con este método manual:

1. Separar Hola los archivos de base de datos de instancia de base de datos local de Hola.
2. Copiar archivos de base de datos de hello desconectado en el almacenamiento de blobs de Azure con hello [utilidad de línea de comandos de AZCopy](../../../storage/common/storage-use-azcopy.md).
3. Adjuntar archivos de base de datos de Hola desde la instancia de SQL Server toohello Hola de dirección URL de Azure en hello VM de Azure.

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>Convertir tooVM y cargar tooURL e implementar como nueva máquina virtual
Utilice este método toomigrate todas las bases de datos de usuario y del sistema en una máquina de virtual local tooAzure de instancia de SQL Server. Usar hello siguiendo los pasos generales toomigrate una instancia completa de SQL Server con este método manual:

1. Convert físico o virtual máquinas tooHyper-V discos duros virtuales mediante el uso de [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).
2. Cargar archivos de disco duro virtual tooAzure almacenamiento mediante hello [cmdlet Add-AzureVHD](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3. Implementar una nueva máquina virtual mediante Hola cargar VHD.

> [!NOTE]
> toomigrate toda una aplicación, considere el uso de [Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Envío de unidad de disco duro
Hola de uso [método de servicio de importación y exportación de Windows](../../../storage/common/storage-import-export-service.md) tootransfer grandes cantidades de datos de archivo tooAzure almacenamiento de blobs en situaciones donde la carga a través de la red de hello es muy caro o no es posible. Con este servicio, enviar uno o más unidades de disco duro que contiene ese centro de datos de Azure de tooan de datos, donde los datos estarán cargan tooyour cuenta de almacenamiento.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo ejecutar SQL Server en Azure Virtual Machines, consulte [Información general sobre SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

Para obtener instrucciones sobre cómo crear una máquina Virtual de Azure SQL Server desde una imagen capturada, consulte [sugerencias y trucos en 'clonar' máquinas virtuales de SQL Azure de imágenes capturadas](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) Hola blog de ingenieros de SQL Server de CSS.

