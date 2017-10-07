---
title: "capacidad de almacenamiento de datos de SQL Azure (portal de Azure) de cálculo aaaManage | Documentos de Microsoft"
description: Capacidad de proceso de tareas del portal Azure toomanage. Escalado de los recursos de proceso ajustando DWU. O bien, puede pausar y reanudar los costos de toosave de recursos de proceso.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="f4e35-105">Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (Portal de Azure)</span><span class="sxs-lookup"><span data-stu-id="f4e35-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4e35-106">Información general</span><span class="sxs-lookup"><span data-stu-id="f4e35-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="f4e35-107">Portal</span><span class="sxs-lookup"><span data-stu-id="f4e35-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="f4e35-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4e35-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="f4e35-109">REST</span><span class="sxs-lookup"><span data-stu-id="f4e35-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="f4e35-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="f4e35-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="f4e35-111">Escalado de la potencia de proceso</span><span class="sxs-lookup"><span data-stu-id="f4e35-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="f4e35-112">recursos de proceso de toochange:</span><span class="sxs-lookup"><span data-stu-id="f4e35-112">toochange compute resources:</span></span>

1. <span data-ttu-id="f4e35-113">Abra hello [portal de Azure][Azure portal], abra la base de datos y haga clic en **escala**.</span><span class="sxs-lookup"><span data-stu-id="f4e35-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Haga clic en Escala][1]
2. <span data-ttu-id="f4e35-115">En la hoja de la escala de hello, mover regulador Hola a la izquierda o hacia la derecha toochange configuración de la unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4e35-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![Mueva el control deslizante][2]
3. <span data-ttu-id="f4e35-117">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4e35-117">Click **Save**.</span></span> <span data-ttu-id="f4e35-118">Aparece un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="f4e35-118">A confirmation message appears.</span></span> <span data-ttu-id="f4e35-119">Haga clic en **Sí** tooconfirm o **no** toocancel.</span><span class="sxs-lookup"><span data-stu-id="f4e35-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Haga clic en Guardar][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="f4e35-121">Pausa del proceso</span><span class="sxs-lookup"><span data-stu-id="f4e35-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="f4e35-122">toopause una base de datos:</span><span class="sxs-lookup"><span data-stu-id="f4e35-122">toopause a database:</span></span>

1. <span data-ttu-id="f4e35-123">Abra hello [portal de Azure] [ Azure portal] y abra la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f4e35-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="f4e35-124">Tenga en cuenta que Hola estado es **Online**.</span><span class="sxs-lookup"><span data-stu-id="f4e35-124">Notice that hello Status is **Online**.</span></span>

    ![Estado En línea][6]
2. <span data-ttu-id="f4e35-126">Haga clic en recursos de proceso y memoria de toosuspend, **pausa**, y, a continuación, aparece un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="f4e35-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="f4e35-127">Haga clic en **Sí** tooconfirm o **no** toocancel.</span><span class="sxs-lookup"><span data-stu-id="f4e35-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Confirme la pausa][7]
3. <span data-ttu-id="f4e35-129">Durante el almacenamiento de datos SQL es inicio de base de datos de hello, estado de hello es **pausar**.</span><span class="sxs-lookup"><span data-stu-id="f4e35-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="f4e35-130">Cuando el estado de hello es **en pausa**, se realiza la operación de pausa de Hola y se ya no se le cobrará por a Dwu.</span><span class="sxs-lookup"><span data-stu-id="f4e35-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Estado de pausa][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="f4e35-132">Reanudación del proceso</span><span class="sxs-lookup"><span data-stu-id="f4e35-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="f4e35-133">tooresume una base de datos:</span><span class="sxs-lookup"><span data-stu-id="f4e35-133">tooresume a database:</span></span>

1. <span data-ttu-id="f4e35-134">Abra hello [portal de Azure] [ Azure portal] y abra la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f4e35-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="f4e35-135">Tenga en cuenta que Hola estado es **en pausa**.</span><span class="sxs-lookup"><span data-stu-id="f4e35-135">Notice that hello Status is **Paused**.</span></span>

    ![Base de datos de pausa][4]
2. <span data-ttu-id="f4e35-137">Haga clic en el base de datos de hello tooresume **iniciar**, y, a continuación, aparece un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="f4e35-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="f4e35-138">Haga clic en **Sí** tooconfirm o **no** toocancel.</span><span class="sxs-lookup"><span data-stu-id="f4e35-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Confirme la reanudación][5]
3. <span data-ttu-id="f4e35-140">Durante el almacenamiento de datos SQL es inicio de base de datos de hello, el estado de hello es "Reanudar".</span><span class="sxs-lookup"><span data-stu-id="f4e35-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="f4e35-141">Cuando el estado de hello es **en línea**, base de datos de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="f4e35-141">When hello status is **online**, hello database is ready.</span></span>

    ![Estado En línea][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="f4e35-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4e35-143">Next steps</span></span>
<span data-ttu-id="f4e35-144">Para más información, consulte [Introducción a la administración][Management overview].</span><span class="sxs-lookup"><span data-stu-id="f4e35-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
