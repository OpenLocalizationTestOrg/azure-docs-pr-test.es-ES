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
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="b4567-103">Restauración de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b4567-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b4567-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="b4567-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b4567-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="b4567-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="b4567-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="b4567-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="b4567-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="b4567-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="b4567-108">SQL Data Warehouse ofrece restauraciones locales y geográficas como parte de sus funcionalidades de recuperación ante desastres de almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="b4567-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="b4567-109">Utilice toorestore de copias de seguridad de almacenamiento de datos la restauración de tooa de almacenamiento de datos de punto en la región principal de hello, o usar región geográfica diferente de tooa de toorestore copias de seguridad con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="b4567-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="b4567-110">Este artículo explica detalles Hola de restauración de un almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="b4567-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="b4567-111">¿Qué es una restauración de almacenamiento de datos?</span><span class="sxs-lookup"><span data-stu-id="b4567-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="b4567-112">Una restauración de almacenamiento de datos es un nuevo almacenamiento de datos que se crea a partir de una copia de seguridad de un almacenamiento de datos existente o eliminado.</span><span class="sxs-lookup"><span data-stu-id="b4567-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="b4567-113">almacenamiento de datos restaurada de Hello vuelve a crea el almacenamiento de datos de copia de seguridad de hello en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="b4567-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="b4567-114">Como SQL Data Warehouse es un sistema distribuido, una restauración de almacenamiento de datos se crea a partir de muchos archivos de copia de seguridad que se almacenan en blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4567-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="b4567-115">La restauración de las bases de datos es una parte esencial de cualquier estrategia de recuperación ante desastres y continuidad empresarial, ya que vuelve a crear los datos tras daños o eliminaciones accidentales.</span><span class="sxs-lookup"><span data-stu-id="b4567-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="b4567-116">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="b4567-116">For more information, see:</span></span>

* [<span data-ttu-id="b4567-117">Copias de seguridad de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b4567-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="b4567-118">Información general acerca de la continuidad empresarial</span><span class="sxs-lookup"><span data-stu-id="b4567-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="b4567-119">Puntos de restauración de almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="b4567-119">Data warehouse restore points</span></span>
<span data-ttu-id="b4567-120">Como una ventaja del uso de almacenamiento Premium de Azure, almacenamiento de datos de SQL utiliza almacenamiento de datos principal de Hola de toobackup de instantáneas de Blob de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4567-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="b4567-121">Cada instantánea tiene un punto de restauración que representa el tiempo de hello instantánea Hola iniciado.</span><span class="sxs-lookup"><span data-stu-id="b4567-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="b4567-122">toorestore un almacenamiento de datos, puede seleccionar un punto de restauración y emite un comando de restauración.</span><span class="sxs-lookup"><span data-stu-id="b4567-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="b4567-123">Almacenamiento de datos de SQL siempre restaura nuevo almacenamiento de datos de hello tooa copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b4567-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="b4567-124">Puede mantener el almacenamiento de datos restaurada de Hola y Hola actual o eliminar uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="b4567-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="b4567-125">Si desea que tooreplace Hola actual almacenamiento de datos con hello restaura el almacén de datos, puede cambiar el nombre.</span><span class="sxs-lookup"><span data-stu-id="b4567-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="b4567-126">Si necesita toorestore un almacenamiento de datos eliminada o en pausa, puede [crear una incidencia de soporte técnico](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="b4567-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="b4567-127">Restauración con redundancia geográfica</span><span class="sxs-lookup"><span data-stu-id="b4567-127">Geo-redundant restore</span></span>
<span data-ttu-id="b4567-128">Puede restaurar la región de tooany de almacenamiento de datos admite el almacenamiento de datos de SQL Azure en el nivel de rendimiento elegido.</span><span class="sxs-lookup"><span data-stu-id="b4567-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="b4567-129">Tenga en cuenta que 9000 y 18000 DWU no se admiten en todas las regiones durante la vista previa de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4567-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="b4567-130">restauración de tooperform un con redundancia geográfica que debe no optó por esta característica.</span><span class="sxs-lookup"><span data-stu-id="b4567-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="b4567-131">Escala de tiempo de restauración</span><span class="sxs-lookup"><span data-stu-id="b4567-131">Restore timeline</span></span>
<span data-ttu-id="b4567-132">Puede restaurar un punto de restauración disponible de base de datos tooany de hello últimos siete días.</span><span class="sxs-lookup"><span data-stu-id="b4567-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="b4567-133">Las instantáneas iniciar cada cuatro horas tooeight y están disponibles durante siete días.</span><span class="sxs-lookup"><span data-stu-id="b4567-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="b4567-134">Cuando una instantánea tiene una antigüedad superior a siete días, caduca y su punto de restauración ya no está disponible.</span><span class="sxs-lookup"><span data-stu-id="b4567-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="b4567-135">Costos de restauración</span><span class="sxs-lookup"><span data-stu-id="b4567-135">Restore costs</span></span>
<span data-ttu-id="b4567-136">cargo de almacenamiento de Hello para el almacén de datos restaurados Hola se factura a velocidad de hello almacenamiento Premium de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4567-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="b4567-137">Si hace una pausa un almacenamiento de datos restaurada, se le cobra por almacenamiento a velocidad de hello almacenamiento Premium de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4567-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="b4567-138">ventaja de Hello de la pausa no es que se le cobrará para recursos informáticos de hello DWU.</span><span class="sxs-lookup"><span data-stu-id="b4567-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="b4567-139">Para más información sobre los precios de SQL Data Warehouse, consulte [Precios de SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="b4567-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="b4567-140">Usos de la restauración</span><span class="sxs-lookup"><span data-stu-id="b4567-140">Uses for restore</span></span>
<span data-ttu-id="b4567-141">uso principal de Hola de restauración del almacén de datos es toorecover datos después de la pérdida accidental de datos o daños.</span><span class="sxs-lookup"><span data-stu-id="b4567-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="b4567-142">También puede utilizar tooretain de restauración del almacén de datos una copia de seguridad durante más de siete días.</span><span class="sxs-lookup"><span data-stu-id="b4567-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="b4567-143">Una vez restaurada la copia de seguridad de hello, tiene almacenamiento de datos de hello en línea y puede pausarla indefinidamente toosave gastos de proceso.</span><span class="sxs-lookup"><span data-stu-id="b4567-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="b4567-144">base de datos pausado Hola incurre en gastos de almacenamiento a velocidad de almacenamiento de Azure Premium Hola.</span><span class="sxs-lookup"><span data-stu-id="b4567-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="b4567-145">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="b4567-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="b4567-146">Escenarios</span><span class="sxs-lookup"><span data-stu-id="b4567-146">Scenarios</span></span>
* <span data-ttu-id="b4567-147">Para ver una introducción a la continuidad empresarial, consulte [Información general sobre la continuidad empresarial](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="b4567-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="b4567-148">tooperform un almacenamiento de datos de restauración, restaurar con:</span><span class="sxs-lookup"><span data-stu-id="b4567-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="b4567-149">Azure portal, vea [restaurar un almacenamiento de datos con hello portal de Azure](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b4567-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="b4567-150">Cmdlets de PowerShell; consulte [Restaurar un almacenamiento de datos mediante cmdlets de PowerShell](sql-data-warehouse-restore-database-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b4567-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="b4567-151">Las API de REST, vea [restaurar un almacén de datos mediante las API de REST de Hola](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="b4567-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

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
