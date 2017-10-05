---
title: "Administración de la potencia de proceso en Azure SQL Data Warehouse (Azure Portal) | Microsoft Docs"
description: Tareas del Portal de Azure para administrar la potencia de proceso. Escalado de los recursos de proceso ajustando DWU. Pausar y reanudar recursos de proceso para ahorrar costos.
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
ms.openlocfilehash: 63888d5dd103b585cf18e4787d3e779810163e3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="da7ef-105">Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (Portal de Azure)</span><span class="sxs-lookup"><span data-stu-id="da7ef-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da7ef-106">Información general</span><span class="sxs-lookup"><span data-stu-id="da7ef-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="da7ef-107">Portal</span><span class="sxs-lookup"><span data-stu-id="da7ef-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="da7ef-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da7ef-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="da7ef-109">REST</span><span class="sxs-lookup"><span data-stu-id="da7ef-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="da7ef-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="da7ef-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="da7ef-111">Escalado de la potencia de proceso</span><span class="sxs-lookup"><span data-stu-id="da7ef-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="da7ef-112">Para cambiar los recursos de proceso:</span><span class="sxs-lookup"><span data-stu-id="da7ef-112">To change compute resources:</span></span>

1. <span data-ttu-id="da7ef-113">Abra [Azure Portal][Azure portal], abra la base de datos y haga clic en **Escalar**.</span><span class="sxs-lookup"><span data-stu-id="da7ef-113">Open the [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Haga clic en Escala][1]
2. <span data-ttu-id="da7ef-115">En la hoja Escalar, mueva el control deslizante izquierdo o derecho para cambiar el valor de DWU.</span><span class="sxs-lookup"><span data-stu-id="da7ef-115">In the Scale blade, move the slider left or right to change the DWU setting.</span></span>

    ![Mueva el control deslizante][2]
3. <span data-ttu-id="da7ef-117">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="da7ef-117">Click **Save**.</span></span> <span data-ttu-id="da7ef-118">Aparece un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="da7ef-118">A confirmation message appears.</span></span> <span data-ttu-id="da7ef-119">Haga clic en **Sí** para confirmar o **No** para cancelar.</span><span class="sxs-lookup"><span data-stu-id="da7ef-119">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Haga clic en Guardar][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="da7ef-121">Pausa del proceso</span><span class="sxs-lookup"><span data-stu-id="da7ef-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="da7ef-122">Para pausar una base de datos:</span><span class="sxs-lookup"><span data-stu-id="da7ef-122">To pause a database:</span></span>

1. <span data-ttu-id="da7ef-123">Abra [Azure Portal][Azure portal] y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="da7ef-123">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="da7ef-124">Tenga en cuenta que el estado sea **En línea**.</span><span class="sxs-lookup"><span data-stu-id="da7ef-124">Notice that the Status is **Online**.</span></span>

    ![Estado En línea][6]
2. <span data-ttu-id="da7ef-126">Para suspender los recursos de proceso y memoria, haga clic en **Pausar**. Aparece un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="da7ef-126">To suspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="da7ef-127">Haga clic en **Sí** para confirmar o **No** para cancelar.</span><span class="sxs-lookup"><span data-stu-id="da7ef-127">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Confirme la pausa][7]
3. <span data-ttu-id="da7ef-129">Mientras Almacenamiento de datos SQL está iniciando la base de datos, el estado será **En pausa**.</span><span class="sxs-lookup"><span data-stu-id="da7ef-129">While SQL Data Warehouse is starting the database, the status is **Pausing**.</span></span>
4. <span data-ttu-id="da7ef-130">Cuando el estado sea **En pausa**, se realizará la operación de pausa y ya no se le cobrará por DWU.</span><span class="sxs-lookup"><span data-stu-id="da7ef-130">When the status is **Paused**, the pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Estado de pausa][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="da7ef-132">Reanudación del proceso</span><span class="sxs-lookup"><span data-stu-id="da7ef-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="da7ef-133">Para reanudar una base de datos:</span><span class="sxs-lookup"><span data-stu-id="da7ef-133">To resume a database:</span></span>

1. <span data-ttu-id="da7ef-134">Abra [Azure Portal][Azure portal] y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="da7ef-134">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="da7ef-135">Tenga en cuenta que el estado sea **En pausa**.</span><span class="sxs-lookup"><span data-stu-id="da7ef-135">Notice that the Status is **Paused**.</span></span>

    ![Base de datos de pausa][4]
2. <span data-ttu-id="da7ef-137">Para reanudar la base de datos, haga clic en **Iniciar**. Aparece un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="da7ef-137">To resume the database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="da7ef-138">Haga clic en **Sí** para confirmar o **No** para cancelar.</span><span class="sxs-lookup"><span data-stu-id="da7ef-138">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Confirme la reanudación][5]
3. <span data-ttu-id="da7ef-140">Mientras Almacenamiento de datos SQL está iniciando la base de datos, el estado será "Reanudando".</span><span class="sxs-lookup"><span data-stu-id="da7ef-140">While SQL Data Warehouse is starting the database, the status is "Resuming".</span></span>
4. <span data-ttu-id="da7ef-141">Cuando el estado sea **En línea**, la base de datos estará lista.</span><span class="sxs-lookup"><span data-stu-id="da7ef-141">When the status is **online**, the database is ready.</span></span>

    ![Estado En línea][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="da7ef-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="da7ef-143">Next steps</span></span>
<span data-ttu-id="da7ef-144">Para más información, consulte [Introducción a la administración][Management overview].</span><span class="sxs-lookup"><span data-stu-id="da7ef-144">For more information, see [Management overview][Management overview].</span></span>

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
