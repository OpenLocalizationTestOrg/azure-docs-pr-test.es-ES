---
title: "Límites de cuota de Azure Data Lake Analytics | Microsoft Docs"
description: "Obtenga información sobre cómo ajustar y aumentar los límites de cuota en cuentas de Azure Data Lake Analytics (ADLA)."
services: data-lake-analytics
keywords: "Análisis con Azure Data Lake"
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="b46e5-104">Límites de cuota de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b46e5-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="b46e5-105">Obtenga información sobre cómo ajustar y aumentar los límites de cuota en cuentas de Azure Data Lake Analytics (ADLA).</span><span class="sxs-lookup"><span data-stu-id="b46e5-105">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="b46e5-106">Conocer estos límites puede ayudarle a comprender su comportamiento de trabajos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b46e5-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="b46e5-107">Todos los límites de cuota son flexibles, y siempre se puede poner en contacto con nosotros para aumentar los límites máximos.</span><span class="sxs-lookup"><span data-stu-id="b46e5-107">All quota limits are soft, so you can increase the maximum limits by reaching out to us.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="b46e5-108">Límites de las suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="b46e5-108">Azure subscriptions limits</span></span>

<span data-ttu-id="b46e5-109">**Número máximo de cuentas de ADLA por suscripción:** 5</span><span class="sxs-lookup"><span data-stu-id="b46e5-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="b46e5-110">Este es el número máximo de cuentas de ADLA que puede crear por suscripción.</span><span class="sxs-lookup"><span data-stu-id="b46e5-110">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="b46e5-111">Al intentar crear la sexta cuenta de ADLA, se muestra el error "Ha alcanzado el número máximo de cuentas de Data Lake Analytics permitido (5) en {región} con la suscripción {nombre}".</span><span class="sxs-lookup"><span data-stu-id="b46e5-111">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="b46e5-112">En este caso, elimine las cuentas de ADLA sin usar, o póngase en contacto con nosotros mediante la [apertura de un vale de soporte](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="b46e5-112">In this case, either delete any unused ADLA accounts, or reach out to us by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="b46e5-113">Límites de la cuenta de ADLA</span><span class="sxs-lookup"><span data-stu-id="b46e5-113">ADLA account limits</span></span>

<span data-ttu-id="b46e5-114">**Número máximo de unidades de análisis por cuenta:** 250</span><span class="sxs-lookup"><span data-stu-id="b46e5-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="b46e5-115">Es el número máximo de unidades de análisis que se pueden ejecutar de forma simultánea en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="b46e5-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="b46e5-116">Si el total de unidades de análisis entre todos los trabajos supera este límite, los trabajos nuevos se ponen en cola automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b46e5-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="b46e5-117">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b46e5-117">For example:</span></span>

* <span data-ttu-id="b46e5-118">Si solo tiene un trabajo en ejecución con doscientas cincuenta unidades de análisis, cuando envíe un segundo trabajo, este permanecerá en la cola de trabajos hasta que el primero se complete.</span><span class="sxs-lookup"><span data-stu-id="b46e5-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="b46e5-119">Si ya tiene cinco trabajos en ejecución y cada uno usa cincuenta unidades de análisis, al enviar un sexto trabajo que necesita veinte unidades de análisis, este permanecerá en la cola de trabajos hasta que haya veinte unidades de análisis disponibles.</span><span class="sxs-lookup"><span data-stu-id="b46e5-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in the job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="b46e5-120">**Número máximo de trabajos de U-SQL simultáneos por cuenta:** 20</span><span class="sxs-lookup"><span data-stu-id="b46e5-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="b46e5-121">Es el número máximo de trabajos que se pueden ejecutar de forma simultánea en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="b46e5-121">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="b46e5-122">Por encima de este valor, los últimos trabajos permanecen en la cola automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b46e5-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="b46e5-123">Ajuste de los límites de cuota de ADLA por cuenta</span><span class="sxs-lookup"><span data-stu-id="b46e5-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="b46e5-124">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b46e5-124">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b46e5-125">Elija una cuenta de ADLA existente.</span><span class="sxs-lookup"><span data-stu-id="b46e5-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="b46e5-126">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="b46e5-126">Click **Properties**.</span></span>
4. <span data-ttu-id="b46e5-127">Ajuste los valores de **Paralelismo** y **Trabajos simultáneos** según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="b46e5-127">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="b46e5-129">Aumento de los límites de cuota máximos</span><span class="sxs-lookup"><span data-stu-id="b46e5-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="b46e5-130">Cree una petición de soporte técnico en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b46e5-130">Open a support request in Azure Portal.</span></span>

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="b46e5-133">Seleccione el tipo de problema **Cuota**.</span><span class="sxs-lookup"><span data-stu-id="b46e5-133">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="b46e5-134">Seleccione su **Suscripción** (asegúrese de que no sea una suscripción de "prueba").</span><span class="sxs-lookup"><span data-stu-id="b46e5-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="b46e5-135">Seleccione el tipo de cuota **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="b46e5-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="b46e5-137">En la hoja del problema, explique el límite de aumento que quiere pedir y los **detalles** sobre por qué necesita esta capacidad adicional.</span><span class="sxs-lookup"><span data-stu-id="b46e5-137">In the problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="b46e5-139">Verifique su información de contacto y cree la petición de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="b46e5-139">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="b46e5-140">Microsoft revisa la solicitud y se intenta dar cabida a sus necesidades empresariales tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="b46e5-140">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b46e5-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b46e5-141">Next steps</span></span>

* [<span data-ttu-id="b46e5-142">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b46e5-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="b46e5-143">Administración de Análisis de Azure Data Lake mediante Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="b46e5-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="b46e5-144">Supervisión y solución de problemas de trabajos de Azure Data Lake Analytics con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b46e5-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
