---
title: Almacenamiento de datos de SQL Azure (portal de Azure) aaaRestore | Documentos de Microsoft
description: Tareas de Azure Portal para restaurar Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>Restauración de Azure SQL Data Warehouse (Portal)
> [!div class="op_single_selector"]
> * [Información general][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
En este artículo, aprenderá cómo toorestore almacenamiento de datos de SQL Azure mediante el uso de Hola portal de Azure.

## <a name="before-you-begin"></a>Antes de empezar
**Compruebe la capacidad DTU**. Cada instancia de SQL Data Warehouse está hospedada en un servidor SQL Server (por ejemplo, myserver.database.windows.net) que tiene una cuota de unidad de rendimiento de datos (DTU) predeterminada. Para poder restaurar el almacén de datos SQL, compruebe que SQL server tiene restante suficiente cuota DTU para la base de datos de Hola que va a restaurar. toolearn la cuota de DTU de toocalculate o toorequest más Dtu, consulte [solicitar un cambio de cuota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Restauración de una base de datos activa o en pausa
toorestore una base de datos:

1. Inicie sesión en toohello [portal de Azure][Azure portal].
2. En el panel izquierdo de hello, seleccione **examinar**y, a continuación, seleccione **servidores SQL Server**.

    ![Seleccione Examinar > Servidores SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Busque el servidor y, a continuación, selecciónelo.

    ![Seleccione el servidor](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. Buscar instancia Hola de almacenamiento de datos de SQL que desee toorestore de y, a continuación, selecciónelo.

    ![Seleccionar instancia de Hola de toorestore de almacenamiento de datos SQL](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. Hola parte superior de hoja de almacén de datos de hello, seleccione **restaurar**.

    ![Seleccione Restaurar](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Especifique un nuevo **nombre de base de datos**.
7. Seleccione hello más reciente **punto de restauración**.

   Asegúrese de que elegir punto de restauración más reciente de Hola. Dado que los puntos de restauración se muestran en hora Universal coordinada (UTC), opción predeterminada de hello podría no ser punto de restauración más reciente de Hola.

      ![Seleccione un punto de restauración](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. Seleccione **Aceptar**.
9. se iniciará el proceso de restauración de base de datos de Hola y puede usar **notificaciones** toomonitor proceso de Hola.

> [!NOTE]
> Una vez finalizada la restauración de hello, puede configurar la base de datos recuperada siguiendo [configurar la base de datos después de la recuperación][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>Restauración de una base de datos eliminada
toorestore una base de datos eliminada:

1. Inicie sesión en toohello [portal de Azure][Azure portal].
2. En el panel izquierdo de hello, seleccione **examinar**y, a continuación, seleccione **servidores SQL Server**.

    ![Seleccione Examinar > Servidores SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Busque el servidor y, a continuación, selecciónelo.

    ![Seleccione el servidor](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Desplácese hacia abajo toohello **Operations** sección en la hoja del servidor.
5. Seleccione hello **elimina las bases de datos** icono.

    ![Icono de hello seleccione eliminado las bases de datos](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Hola seleccione elimina base de datos que desea toorestore.

    ![Seleccione una base de datos toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Especifique un nuevo **nombre de base de datos**.

    ![Agregar un nombre de base de datos de Hola](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. Seleccione **Aceptar**.
9. se iniciará el proceso de restauración de base de datos de Hola y puede usar **notificaciones** toomonitor proceso de Hola.

> [!NOTE]
> consulta de la base de datos una vez finalizada la restauración de hello, tooconfigure [configurar la base de datos después de la recuperación][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Pasos siguientes
toolearn acerca de las características de continuidad de negocio Hola de ediciones de base de datos de SQL Azure, lea hello [información general sobre la continuidad de negocio de base de datos de SQL Azure][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
