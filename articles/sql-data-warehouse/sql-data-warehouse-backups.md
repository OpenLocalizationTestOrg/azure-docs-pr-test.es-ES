---
title: "copias de seguridad del almacenamiento de datos SQL aaaAzure - instantáneas, con redundancia geográfica | Documentos de Microsoft"
description: "Obtenga información acerca de las copias de seguridad de base de datos integrada de almacenamiento de datos de SQL que le permiten toorestore un punto de restauración del almacén de datos de SQL Azure tooa o una región geográfica diferente."
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a>Copias de seguridad de SQL Data Warehouse
SQL Data Warehouse ofrece copias de seguridad locales y geográficas como parte de sus funcionalidades de copia de seguridad de almacenamiento de datos. Aquí se incluyen instantáneas de Azure Storage Blob y almacenamiento con redundancia geográfica. Utilice toorestore de copias de seguridad de almacenamiento de datos la restauración de tooa de almacenamiento de datos de punto en la región principal de Hola o restaurar tooa otra región geográfica. Este artículo explica detalles Hola de copias de seguridad en el almacén de datos de SQL.

## <a name="what-is-a-data-warehouse-backup"></a>¿Qué es una copia de seguridad de almacenamiento de datos?
Una copia de seguridad del almacén de datos es datos de hello puede usar toorestore en un momento determinado de datos almacén tooa.  Como SQL Data Warehouse es un sistema distribuido, una copia de seguridad de almacenamiento de datos consta de muchos archivos que se almacenan en blobs de Azure. 

Las copias de seguridad de base de datos son una parte esencial de cualquier estrategia de recuperación ante desastres y continuidad del negocio, ya que protegen los datos de daños o eliminaciones accidentales. Para más información, consulte [Información general sobre la continuidad empresarial](../sql-database/sql-database-business-continuity.md).

## <a name="data-redundancy"></a>Redundancia de datos
SQL Data Warehouse protege los datos al almacenarlos en Azure Premium Storage con redundancia local (LRS). Esta característica de almacenamiento de Azure almacena varias copias sincrónicos datos Hola Hola local center tooguarantee transparente de los datos en protección de datos si se produce un error localizado. Gracias a la redundancia de datos, se garantiza que estos puedan sobrevivir a problemas de infraestructura, por ejemplo, errores de disco. Asimismo, asegura la continuidad empresarial mediante una infraestructura de alta disponibilidad con tolerancia a errores.

toolearn más información sobre:

* Almacenamiento Premium de Azure, consulte [Introducción tooAzure almacenamiento Premium](../storage/common/storage-premium-storage.md).
* Almacenamiento con redundancia local, consulte [Replicación de Azure Storage](../storage/common/storage-redundancy.md#locally-redundant-storage).

## <a name="azure-storage-blob-snapshots"></a>Instantáneas de Azure Storage Blob
Como una ventaja del uso de almacenamiento Premium de Azure, almacenamiento de datos de SQL utiliza almacenamiento de datos de Blob de almacenamiento de Azure instantáneas toobackup Hola localmente. Puede restaurar un punto de restauración de instantáneas de datos almacén tooa. Las instantáneas se inician como mínimo cada ocho horas y están disponibles durante siete días.  

toolearn más información sobre:

* Instantáneas de blobs de Azure, consulte [Creación de una instantánea de un blob](../storage/blobs/storage-blob-snapshots.md).

## <a name="geo-redundant-backups"></a>Copias de seguridad con redundancia geográfica
Cada 24 horas, almacenamiento de datos de SQL almacena el almacenamiento de datos completa de hello en almacenamiento estándar. Hello almacenamiento de datos completa se crea toomatch Hola momento de la última instantánea de Hola. almacenamiento estándar Hola pertenece tooa cuenta de almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS). característica de almacenamiento de Azure RA-GRS Hola replica Hola archivos de copia de seguridad tooa [centro de datos emparejado](../best-practices-availability-paired-regions.md). Esta replicación geográfica garantiza que puede restaurar el almacén de datos en caso de que no se puede obtener acceso a instantáneas de hello en su región primaria. 

Esta característica está activada de forma predeterminada. Si no desea que copias de seguridad con redundancia geográfica toouse, que puede [descartar] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn). 

> [!NOTE]
> En el almacenamiento de Azure, término hello *replicación* hace referencia toocopying archivos desde una ubicación tooanother. De SQL *replicación de base de datos* hace referencia a bases de datos de tookeeping toomultiple secundarias sincronizadas con una base de datos principal. 
> 
> 

> [!NOTE]
> No se pueden rechazar las copias de seguridad con redundancia geográfica con DWU 9000 y DWU 18000. 
>
> 

toolearn más información sobre:

* Almacenamiento con redundancia geográfica, consulte [Replicación de Azure Storage](../storage/common/storage-redundancy.md).
* Almacenamiento de RA-GRS, consulte [Almacenamiento con redundancia geográfica con acceso de lectura](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).

## <a name="data-warehouse-backup-schedule-and-retention-period"></a>Programación de copia de seguridad de almacenamiento de datos y período de retención
Almacenamiento de datos SQL se crean instantáneas en los almacenes de datos en línea cada cuatro horas tooeight y conserva cada instantánea durante siete días. Puede restaurar la tooone de base de datos en línea de puntos de restauración de Hola Hola últimos siete días. 

toosee cuando se inicia la última instantánea de hello, ejecute esta consulta en el almacén de datos de SQL en línea. 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

Si necesita una instantánea de tooretain durante más de siete días, puede restaurar tooa de punto de restauración un nuevo almacén de datos. Una vez finalizada la restauración de hello, almacenamiento de datos SQL comienza a crear instantáneas en almacenamiento de datos nueva Hola. Si no realiza el nuevo almacén de datos de cambios toohello, instantáneas de hello permanecen vacías y, por tanto, el costo de instantánea de hello es mínimo. También puede pausar tookeep de base de datos de hello almacenamiento de datos SQL desde la creación de instantáneas.

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a>¿Qué ocurre retención de copia de seguridad de toomy mientras está en pausa el almacenamiento de datos?
SQL Data Warehouse no crea instantáneas y no caduca las copias de seguridad mientras un almacenamiento de datos está en pausa. antigüedad de la instantánea de Hello no cambia mientras está en pausa el almacenamiento de datos de Hola. Retención de instantáneas se basa en el número de Hola de días de almacenamiento de datos de hello está en línea, no los días de calendario.

Por ejemplo, si una instantánea se inicia el 1 de octubre a las 4 p.m. y almacenamiento de datos de Hola se detiene el 3 de octubre a las 4 p.m., instantánea de hello es dos días de antigüedad. Cada vez que se pone en línea el almacenamiento de datos de hello instantánea hello es dos días de antigüedad. Si el almacén de datos de Hola se pone en línea 5 de octubre a las 4 p.m., instantánea hello es dos días de antigüedad y permanece durante cinco días más.

Al almacenamiento de datos de hello vuelve a estar conectado, almacenamiento de datos SQL se reanuda nuevas instantáneas y expira instantáneas cuando tienen más de siete días de datos.

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a>¿Cuánto tiempo es período de retención de Hola para un almacenamiento de datos colocados?
Cuando se quita un almacén de datos, instantáneas de Hola y Hola data warehouse son guardan durante siete días y, a continuación, se quitan. Puede restaurar tooany de almacenamiento de datos de Hola Hola guardado de puntos de restauración.

> [!IMPORTANT]
> Si elimina una instancia SQL server lógica, todas las bases de datos que pertenecen la instancia de toohello también se eliminan y no se puede recuperar. No puede restaurar un servidor eliminado.
> 
> 

## <a name="data-warehouse-backup-costs"></a>Costos de la copia de seguridad del almacenamiento de datos
Hola total de costo para el almacén de datos principal y siete días a partir de las instantáneas de Blob de Azure es toohello redondeado más cercano TB. Por ejemplo, si el almacenamiento de datos es 1,5 TB y las instantáneas de hello usan 100 GB, se le facturará de 2 TB de datos a velocidades de almacenamiento Premium de Azure. 

> [!NOTE]
> Cada instantánea inicialmente está vacía y crece a medida que el almacén de datos principal de toohello de cambios. Todas las instantáneas aumentan de tamaño cuando cambia de almacenamiento de datos de Hola. Por lo tanto, los costos de almacenamiento de Hola para instantáneas crecen correspondiente de toohello de tasa de cambio.
> 
> 

Si usa almacenamiento con redundancia geográfica, recibirá un cargo de almacenamiento por separado. almacenamiento con redundancia geográfica Hola se factura a velocidad de hello estándar almacenamiento geográficamente redundante con acceso de lectura (RA-GRS).

Para más información sobre los precios de SQL Data Warehouse, consulte [Precios de SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="using-database-backups"></a>Uso de copias de seguridad de base de datos
uso principal de Hola para copias de seguridad del almacén de datos SQL es tooone de almacenamiento de datos de toorestore Hola Hola de puntos de restauración en el período de retención de Hola.  

* toorestore un almacén de datos SQL, consulte [restaurar un almacén de datos SQL](sql-data-warehouse-restore-database-overview.md).

## <a name="related-topics"></a>Temas relacionados
### <a name="scenarios"></a>Escenarios
* Para ver una introducción a la continuidad empresarial, consulte [Información general sobre la continuidad empresarial](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

* toorestore un almacenamiento de datos, vea [restaurar un almacén de datos SQL](sql-data-warehouse-restore-database-overview.md)

<!-- ### Tutorials -->

