---
title: "Restauración de un almacén de datos de Azure: local y con redundancia geográfica | Microsoft Docs"
description: "Información general de las opciones de restauración de bases de datos para recuperar una base de datos en Almacenamiento de datos SQL de Azure."
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
ms.openlocfilehash: ea42b7135d0695b66d569095e70bb3d9f8b9594b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="a4e98-103">Restauración de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a4e98-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a4e98-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="a4e98-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="a4e98-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="a4e98-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="a4e98-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a4e98-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="a4e98-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="a4e98-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="a4e98-108">SQL Data Warehouse ofrece restauraciones locales y geográficas como parte de sus funcionalidades de recuperación ante desastres de almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="a4e98-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="a4e98-109">Use copias de seguridad de almacenamiento de datos para restaurar el almacenamiento de datos a un punto de restauración en la región primaria o use copias de seguridad con redundancia geográfica para restaurar a una región geográfica diferente.</span><span class="sxs-lookup"><span data-stu-id="a4e98-109">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or use geo-redundant backups to restore to a different geographical region.</span></span> <span data-ttu-id="a4e98-110">En este artículo se explican los aspectos específicos de la restauración de un almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="a4e98-110">This article explains the specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="a4e98-111">¿Qué es una restauración de almacenamiento de datos?</span><span class="sxs-lookup"><span data-stu-id="a4e98-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="a4e98-112">Una restauración de almacenamiento de datos es un nuevo almacenamiento de datos que se crea a partir de una copia de seguridad de un almacenamiento de datos existente o eliminado.</span><span class="sxs-lookup"><span data-stu-id="a4e98-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="a4e98-113">El almacenamiento de datos restaurado vuelve a crear el de copia de seguridad en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="a4e98-113">The restored data warehouse re-creates the backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="a4e98-114">Como SQL Data Warehouse es un sistema distribuido, una restauración de almacenamiento de datos se crea a partir de muchos archivos de copia de seguridad que se almacenan en blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4e98-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="a4e98-115">La restauración de las bases de datos es una parte esencial de cualquier estrategia de recuperación ante desastres y continuidad empresarial, ya que vuelve a crear los datos tras daños o eliminaciones accidentales.</span><span class="sxs-lookup"><span data-stu-id="a4e98-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="a4e98-116">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="a4e98-116">For more information, see:</span></span>

* [<span data-ttu-id="a4e98-117">Copias de seguridad de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a4e98-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="a4e98-118">Información general acerca de la continuidad empresarial</span><span class="sxs-lookup"><span data-stu-id="a4e98-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="a4e98-119">Puntos de restauración de almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="a4e98-119">Data warehouse restore points</span></span>
<span data-ttu-id="a4e98-120">Una de las ventajas de usar Azure Premium Storage es que SQL Data Warehouse usa instantáneas de Azure Storage Blob para realizar la copia de seguridad del almacenamiento de datos principal.</span><span class="sxs-lookup"><span data-stu-id="a4e98-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the primary data warehouse.</span></span> <span data-ttu-id="a4e98-121">Cada instantánea tiene un punto de restauración que representa la hora de inicio de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="a4e98-121">Each snapshot has a restore point that represents the time the snapshot started.</span></span> <span data-ttu-id="a4e98-122">Para restaurar un almacenamiento de datos, elija un punto de restauración y emita un comando de restauración.</span><span class="sxs-lookup"><span data-stu-id="a4e98-122">To restore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="a4e98-123">SQL Data Warehouse siempre restaura la copia de seguridad en un nuevo almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="a4e98-123">SQL Data Warehouse always restores the backup to a new data warehouse.</span></span> <span data-ttu-id="a4e98-124">Puede mantener el almacenamiento de datos restaurado y el actual, o eliminar uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="a4e98-124">You can either keep the restored data warehouse and the current one, or delete one of them.</span></span> <span data-ttu-id="a4e98-125">Si desea reemplazar el almacenamiento de datos actual con el almacenamiento de datos restaurado, puede cambiar su nombre.</span><span class="sxs-lookup"><span data-stu-id="a4e98-125">If you want to replace the current data warehouse with the restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="a4e98-126">Si tiene que restaurar un almacenamiento de datos eliminado o en pausa, puede [crear una incidencia de soporte técnico](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="a4e98-126">If you need to restore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore the last available restore point.

Yes, for the next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps the data warehouse and its snapshots for seven days just in case you need the data. After seven days, you won't be able to restore to any of the restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="a4e98-127">Restauración con redundancia geográfica</span><span class="sxs-lookup"><span data-stu-id="a4e98-127">Geo-redundant restore</span></span>
<span data-ttu-id="a4e98-128">Puede restaurar el almacenamiento de datos en cualquier región que admita Azure SQL Data Warehouse en el nivel de rendimiento elegido.</span><span class="sxs-lookup"><span data-stu-id="a4e98-128">You can restore your data warehouse to any region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="a4e98-129">Tenga en cuenta que 9000 y 18000 DWU no se admiten en todas las regiones durante la versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="a4e98-129">Please note that 9000 and 18000 DWU are not supported in all regions during the preview.</span></span>

> [!NOTE]
> <span data-ttu-id="a4e98-130">Para llevar a cabo una restauración con redundancia geográfica no puede haber anulado esta característica.</span><span class="sxs-lookup"><span data-stu-id="a4e98-130">To perform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="a4e98-131">Escala de tiempo de restauración</span><span class="sxs-lookup"><span data-stu-id="a4e98-131">Restore timeline</span></span>
<span data-ttu-id="a4e98-132">Puede restaurar una base de datos a cualquier punto de restauración disponible de los últimos siete días.</span><span class="sxs-lookup"><span data-stu-id="a4e98-132">You can restore a database to any available restore point within the last seven days.</span></span> <span data-ttu-id="a4e98-133">Las instantáneas comienzan cada cuatro a ocho horas y están disponibles durante siete días.</span><span class="sxs-lookup"><span data-stu-id="a4e98-133">Snapshots start every four to eight hours and are available for seven days.</span></span> <span data-ttu-id="a4e98-134">Cuando una instantánea tiene una antigüedad superior a siete días, caduca y su punto de restauración ya no está disponible.</span><span class="sxs-lookup"><span data-stu-id="a4e98-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="a4e98-135">Costos de restauración</span><span class="sxs-lookup"><span data-stu-id="a4e98-135">Restore costs</span></span>
<span data-ttu-id="a4e98-136">Los cargos de almacenamiento por el almacenamiento de datos restaurado se facturan con la tarifa de Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="a4e98-136">The storage charge for the restored data warehouse is billed at the Azure Premium Storage rate.</span></span> 

<span data-ttu-id="a4e98-137">Si se pausa un almacenamiento de datos restaurado, se le cobrará por el almacenamiento según la tarifa de Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="a4e98-137">If you pause a restored data warehouse, you are charged for storage at the Azure Premium Storage rate.</span></span> <span data-ttu-id="a4e98-138">La ventaja de pausar es que no se cobra por los recursos de computación de DWU.</span><span class="sxs-lookup"><span data-stu-id="a4e98-138">The advantage of pausing is you are not charged for the DWU computing resources.</span></span>

<span data-ttu-id="a4e98-139">Para más información sobre los precios de SQL Data Warehouse, consulte [Precios de SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="a4e98-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="a4e98-140">Usos de la restauración</span><span class="sxs-lookup"><span data-stu-id="a4e98-140">Uses for restore</span></span>
<span data-ttu-id="a4e98-141">El uso principal de la restauración del almacenamiento de datos es recuperar información tras las pérdidas de datos o daños accidentales.</span><span class="sxs-lookup"><span data-stu-id="a4e98-141">The primary use for data warehouse restore is to recover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="a4e98-142">También puede utilizar la restauración del almacenamiento de datos para conservar una copia de seguridad durante más de siete días.</span><span class="sxs-lookup"><span data-stu-id="a4e98-142">You can also use data warehouse restore to retain a backup for longer than seven days.</span></span> <span data-ttu-id="a4e98-143">Una vez restaurada la copia de seguridad, tiene el almacenamiento de datos en línea y puede pausarlo indefinidamente para ahorrar costos de computación.</span><span class="sxs-lookup"><span data-stu-id="a4e98-143">Once the backup is restored, you have the data warehouse online and can pause it indefinitely to save compute costs.</span></span> <span data-ttu-id="a4e98-144">La base de datos en pausa genera gastos de almacenamiento según la tarifa de Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="a4e98-144">The paused database incurs storage charges at the Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="a4e98-145">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="a4e98-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="a4e98-146">Escenarios</span><span class="sxs-lookup"><span data-stu-id="a4e98-146">Scenarios</span></span>
* <span data-ttu-id="a4e98-147">Para ver una introducción a la continuidad empresarial, consulte [Información general sobre la continuidad empresarial](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="a4e98-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="a4e98-148">Para realizar una restauración del almacenamiento de datos, efectúa esta última mediante los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="a4e98-148">To perform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="a4e98-149">Azure Portal; consulte [Restaurar un almacenamiento de datos mediante Azure Portal](sql-data-warehouse-restore-database-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4e98-149">Azure portal, see [Restore a data warehouse using the Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="a4e98-150">Cmdlets de PowerShell; consulte [Restaurar un almacenamiento de datos mediante cmdlets de PowerShell](sql-data-warehouse-restore-database-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a4e98-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="a4e98-151">Las API de REST; consulte [Restaurar un almacenamiento de datos mediante las API de REST](sql-data-warehouse-restore-database-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="a4e98-151">REST APIs, see [Restore a data warehouse using the REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

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
