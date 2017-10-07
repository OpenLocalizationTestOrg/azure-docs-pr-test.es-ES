---
title: aaaRestore un almacenamiento de datos de SQL Azure (API de REST) | Documentos de Microsoft
description: Tareas de la API de REST para restaurar una instancia de Almacenamiento de datos SQL de Azure.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a>Restauración de instancias de Almacenamiento de datos SQL de Azure (API de REST)
> [!div class="op_single_selector"]
> * [Información general][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

En este artículo, aprenderá cómo toorestore un uso de almacenamiento de datos de SQL Azure Hola API de REST.

## <a name="before-you-begin"></a>Antes de empezar
**Compruebe la capacidad DTU**. Cada instancia de Almacenamiento de datos SQL está hospedada en un servidor SQL Server (p. ej., myserver.database.windows.net) que tiene una cuota de DTU predeterminada.  Para poder restaurar un almacén de datos de SQL, compruebe que Hola que su SQL server tiene restante suficiente cuota DTU para base de datos de Hola que se va a restaurar. toolearn cómo necesarios toocalculate DTU o toorequest más DTU, consulte [solicitar un cambio de cuota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Restauración de una base de datos activa o en pausa
toorestore una base de datos:

1. Obtener lista de Hola de puntos de restauración de base de datos mediante la operación de puntos de restauración de base de datos de Get hello.
2. Comenzar la restauración mediante el uso de hello [crear solicitud de restauración de base de datos] [ Create database restore request] operación.
3. Un seguimiento del estado de saludo de la restauración mediante hello [estado de la operación de base de datos] [ Database operation status] operación.

> [!NOTE]
> Una vez finalizada la restauración de hello, puede configurar la base de datos recuperada siguiendo [configurar la base de datos después de la recuperación][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Restauración de una base de datos eliminada
toorestore una base de datos eliminada:

1. Enumerar todas las bases de datos eliminadas restaurables mediante hello [lista pueden restaurar bases de datos eliminadas] [ List restorable dropped databases] operación.
2. Obtenga detalles de Hola para base de datos de hello eliminado desea toorestore mediante hello [Get restaurable quita base de datos] [ Get restorable dropped database] operación.
3. Comenzar la restauración mediante el uso de hello [crear solicitud de restauración de base de datos] [ Create database restore request] operación.
4. Un seguimiento del estado de saludo de la restauración mediante hello [estado de la operación de base de datos] [ Database operation status] operación.

> [!NOTE]
> consulta de la base de datos una vez finalizada la restauración de hello, tooconfigure [configurar la base de datos después de la recuperación][Configure your database after recovery].
> 
> 

## <a name="next-steps"></a>Pasos siguientes
toolearn acerca de las características de continuidad de negocio de Hola de ediciones de base de datos de SQL Azure, lea hello [información general sobre la continuidad de negocio de base de datos de SQL Azure][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
