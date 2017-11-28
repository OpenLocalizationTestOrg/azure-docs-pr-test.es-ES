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
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="66c62-103">Restauración de instancias de Almacenamiento de datos SQL de Azure (API de REST)</span><span class="sxs-lookup"><span data-stu-id="66c62-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="66c62-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="66c62-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="66c62-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="66c62-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="66c62-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="66c62-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="66c62-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="66c62-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="66c62-108">En este artículo, aprenderá cómo toorestore un uso de almacenamiento de datos de SQL Azure Hola API de REST.</span><span class="sxs-lookup"><span data-stu-id="66c62-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="66c62-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="66c62-109">Before you begin</span></span>
<span data-ttu-id="66c62-110">**Compruebe la capacidad DTU**.</span><span class="sxs-lookup"><span data-stu-id="66c62-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="66c62-111">Cada instancia de Almacenamiento de datos SQL está hospedada en un servidor SQL Server (p. ej., myserver.database.windows.net) que tiene una cuota de DTU predeterminada.</span><span class="sxs-lookup"><span data-stu-id="66c62-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="66c62-112">Para poder restaurar un almacén de datos de SQL, compruebe que Hola que su SQL server tiene restante suficiente cuota DTU para base de datos de Hola que se va a restaurar.</span><span class="sxs-lookup"><span data-stu-id="66c62-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="66c62-113">toolearn cómo necesarios toocalculate DTU o toorequest más DTU, consulte [solicitar un cambio de cuota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="66c62-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="66c62-114">Restauración de una base de datos activa o en pausa</span><span class="sxs-lookup"><span data-stu-id="66c62-114">Restore an active or paused database</span></span>
<span data-ttu-id="66c62-115">toorestore una base de datos:</span><span class="sxs-lookup"><span data-stu-id="66c62-115">toorestore a database:</span></span>

1. <span data-ttu-id="66c62-116">Obtener lista de Hola de puntos de restauración de base de datos mediante la operación de puntos de restauración de base de datos de Get hello.</span><span class="sxs-lookup"><span data-stu-id="66c62-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="66c62-117">Comenzar la restauración mediante el uso de hello [crear solicitud de restauración de base de datos] [ Create database restore request] operación.</span><span class="sxs-lookup"><span data-stu-id="66c62-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="66c62-118">Un seguimiento del estado de saludo de la restauración mediante hello [estado de la operación de base de datos] [ Database operation status] operación.</span><span class="sxs-lookup"><span data-stu-id="66c62-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="66c62-119">Una vez finalizada la restauración de hello, puede configurar la base de datos recuperada siguiendo [configurar la base de datos después de la recuperación][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="66c62-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="66c62-120">Restauración de una base de datos eliminada</span><span class="sxs-lookup"><span data-stu-id="66c62-120">Restore a deleted database</span></span>
<span data-ttu-id="66c62-121">toorestore una base de datos eliminada:</span><span class="sxs-lookup"><span data-stu-id="66c62-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="66c62-122">Enumerar todas las bases de datos eliminadas restaurables mediante hello [lista pueden restaurar bases de datos eliminadas] [ List restorable dropped databases] operación.</span><span class="sxs-lookup"><span data-stu-id="66c62-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="66c62-123">Obtenga detalles de Hola para base de datos de hello eliminado desea toorestore mediante hello [Get restaurable quita base de datos] [ Get restorable dropped database] operación.</span><span class="sxs-lookup"><span data-stu-id="66c62-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="66c62-124">Comenzar la restauración mediante el uso de hello [crear solicitud de restauración de base de datos] [ Create database restore request] operación.</span><span class="sxs-lookup"><span data-stu-id="66c62-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="66c62-125">Un seguimiento del estado de saludo de la restauración mediante hello [estado de la operación de base de datos] [ Database operation status] operación.</span><span class="sxs-lookup"><span data-stu-id="66c62-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="66c62-126">consulta de la base de datos una vez finalizada la restauración de hello, tooconfigure [configurar la base de datos después de la recuperación][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="66c62-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="66c62-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66c62-127">Next steps</span></span>
<span data-ttu-id="66c62-128">toolearn acerca de las características de continuidad de negocio de Hola de ediciones de base de datos de SQL Azure, lea hello [información general sobre la continuidad de negocio de base de datos de SQL Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="66c62-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
