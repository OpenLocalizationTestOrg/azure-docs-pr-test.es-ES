---
title: "un almacén de datos de Azure - local y con redundancia geográfica aaaRestore | Documentos de Microsoft"
description: "Información general de opciones de restauración de base de datos de Hola para recuperar una base de datos en el almacén de datos de SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>Restauración de SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Información general][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

SQL Data Warehouse ofrece restauraciones locales y geográficas como parte de sus funcionalidades de recuperación ante desastres de almacenamiento de datos. Utilice toorestore de copias de seguridad de almacenamiento de datos la restauración de tooa de almacenamiento de datos de punto en la región principal de hello, o usar región geográfica diferente de tooa de toorestore copias de seguridad con redundancia geográfica. Este artículo explica detalles Hola de restauración de un almacén de datos.

## <a name="what-is-a-data-warehouse-restore"></a>¿Qué es una restauración de almacenamiento de datos?
Una restauración de almacenamiento de datos es un nuevo almacenamiento de datos que se crea a partir de una copia de seguridad de un almacenamiento de datos existente o eliminado. almacenamiento de datos restaurada de Hello vuelve a crea el almacenamiento de datos de copia de seguridad de hello en un momento determinado. Como SQL Data Warehouse es un sistema distribuido, una restauración de almacenamiento de datos se crea a partir de muchos archivos de copia de seguridad que se almacenan en blobs de Azure. 

La restauración de las bases de datos es una parte esencial de cualquier estrategia de recuperación ante desastres y continuidad empresarial, ya que vuelve a crear los datos tras daños o eliminaciones accidentales.

Para más información, consulte:

* [Copias de seguridad de SQL Data Warehouse](sql-data-warehouse-backups.md)
* [Información general acerca de la continuidad empresarial](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Puntos de restauración de almacenamiento de datos
Como una ventaja del uso de almacenamiento Premium de Azure, almacenamiento de datos de SQL utiliza almacenamiento de datos principal de Hola de toobackup de instantáneas de Blob de almacenamiento de Azure. Cada instantánea tiene un punto de restauración que representa el tiempo de hello instantánea Hola iniciado. toorestore un almacenamiento de datos, puede seleccionar un punto de restauración y emite un comando de restauración.  

Almacenamiento de datos de SQL siempre restaura nuevo almacenamiento de datos de hello tooa copia de seguridad. Puede mantener el almacenamiento de datos restaurada de Hola y Hola actual o eliminar uno de ellos. Si desea que tooreplace Hola actual almacenamiento de datos con hello restaura el almacén de datos, puede cambiar el nombre.

Si necesita toorestore un almacenamiento de datos eliminada o en pausa, puede [crear una incidencia de soporte técnico](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>Restauración con redundancia geográfica
Puede restaurar la región de tooany de almacenamiento de datos admite el almacenamiento de datos de SQL Azure en el nivel de rendimiento elegido. Tenga en cuenta que 9000 y 18000 DWU no se admiten en todas las regiones durante la vista previa de Hola.

> [!NOTE]
> restauración de tooperform un con redundancia geográfica que debe no optó por esta característica.
> 
> 

## <a name="restore-timeline"></a>Escala de tiempo de restauración
Puede restaurar un punto de restauración disponible de base de datos tooany de hello últimos siete días. Las instantáneas iniciar cada cuatro horas tooeight y están disponibles durante siete días. Cuando una instantánea tiene una antigüedad superior a siete días, caduca y su punto de restauración ya no está disponible.

## <a name="restore-costs"></a>Costos de restauración
cargo de almacenamiento de Hello para el almacén de datos restaurados Hola se factura a velocidad de hello almacenamiento Premium de Azure. 

Si hace una pausa un almacenamiento de datos restaurada, se le cobra por almacenamiento a velocidad de hello almacenamiento Premium de Azure. ventaja de Hello de la pausa no es que se le cobrará para recursos informáticos de hello DWU.

Para más información sobre los precios de SQL Data Warehouse, consulte [Precios de SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Usos de la restauración
uso principal de Hola de restauración del almacén de datos es toorecover datos después de la pérdida accidental de datos o daños.

También puede utilizar tooretain de restauración del almacén de datos una copia de seguridad durante más de siete días. Una vez restaurada la copia de seguridad de hello, tiene almacenamiento de datos de hello en línea y puede pausarla indefinidamente toosave gastos de proceso. base de datos pausado Hola incurre en gastos de almacenamiento a velocidad de almacenamiento de Azure Premium Hola. 

## <a name="related-topics"></a>Temas relacionados
### <a name="scenarios"></a>Escenarios
* Para ver una introducción a la continuidad empresarial, consulte [Información general sobre la continuidad empresarial](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

tooperform un almacenamiento de datos de restauración, restaurar con:

* Azure portal, vea [restaurar un almacenamiento de datos con hello portal de Azure](sql-data-warehouse-restore-database-portal.md)
* Cmdlets de PowerShell; consulte [Restaurar un almacenamiento de datos mediante cmdlets de PowerShell](sql-data-warehouse-restore-database-powershell.md).
* Las API de REST, vea [restaurar un almacén de datos mediante las API de REST de Hola](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
