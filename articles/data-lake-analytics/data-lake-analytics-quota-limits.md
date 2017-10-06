---
title: "Límites de cuota de Data Lake análisis aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se limita tooadjust y aumento de cuota en las cuentas de Azure datos Lake Analytics (ADLA)."
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
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="1269b-104">Límites de cuota de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1269b-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="1269b-105">Obtenga información acerca de cómo se limita tooadjust y aumento de cuota en las cuentas de Azure datos Lake Analytics (ADLA).</span><span class="sxs-lookup"><span data-stu-id="1269b-105">Learn how tooadjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="1269b-106">Conocer estos límites puede ayudarle a comprender su comportamiento de trabajos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1269b-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="1269b-107">Todos los límites de cuota son suaves, por lo que puede aumentar los límites máximos Hola llegando toous.</span><span class="sxs-lookup"><span data-stu-id="1269b-107">All quota limits are soft, so you can increase hello maximum limits by reaching out toous.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="1269b-108">Límites de las suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="1269b-108">Azure subscriptions limits</span></span>

<span data-ttu-id="1269b-109">**Número máximo de cuentas de ADLA por suscripción:** 5</span><span class="sxs-lookup"><span data-stu-id="1269b-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="1269b-110">Se trata de hello número máximo de cuentas ADLA que puede crear por suscripción.</span><span class="sxs-lookup"><span data-stu-id="1269b-110">This is hello maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="1269b-111">Si trata de cuenta ADLA toocreate un sexto, obtendrá un error "Se ha alcanzado Hola número máximo de cuentas de análisis de Data Lake permitidas (5) en la región con nombre de la suscripción".</span><span class="sxs-lookup"><span data-stu-id="1269b-111">If you try toocreate a sixth ADLA account, you will get an error "You have reached hello maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="1269b-112">En este caso, elimine las cuentas de ADLA sin usar, o llegar toous por [abrir una incidencia de soporte técnico](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="1269b-112">In this case, either delete any unused ADLA accounts, or reach out toous by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="1269b-113">Límites de la cuenta de ADLA</span><span class="sxs-lookup"><span data-stu-id="1269b-113">ADLA account limits</span></span>

<span data-ttu-id="1269b-114">**Número máximo de unidades de análisis por cuenta:** 250</span><span class="sxs-lookup"><span data-stu-id="1269b-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="1269b-115">Se trata de número máximo de Hola de AUs que pueden ejecutarse simultáneamente en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1269b-115">This is hello maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="1269b-116">Si el total de unidades de análisis entre todos los trabajos supera este límite, los trabajos nuevos se ponen en cola automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1269b-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="1269b-117">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1269b-117">For example:</span></span>

* <span data-ttu-id="1269b-118">Si tiene sólo un trabajo ejecuta con 250 AUs, cuando se envía un segundo trabajo espera en cola de trabajos de hello hasta que se complete el primer trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1269b-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in hello job queue until hello first job completes.</span></span>
* <span data-ttu-id="1269b-119">Si ya tiene cinco trabajos en ejecución y cada uno está usando 50 AUs, cuando se envía un trabajo sexto que necesita 20 AUs espera en cola de trabajos de hello hasta que hay 20 AUs disponibles.</span><span class="sxs-lookup"><span data-stu-id="1269b-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in hello job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="1269b-120">**Número máximo de trabajos de U-SQL simultáneos por cuenta:** 20</span><span class="sxs-lookup"><span data-stu-id="1269b-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="1269b-121">Se trata de hello número máximo de trabajos que pueden ejecutarse simultáneamente en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1269b-121">This is hello maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="1269b-122">Por encima de este valor, los últimos trabajos permanecen en la cola automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1269b-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="1269b-123">Ajuste de los límites de cuota de ADLA por cuenta</span><span class="sxs-lookup"><span data-stu-id="1269b-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="1269b-124">Inicio de sesión toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1269b-124">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1269b-125">Elija una cuenta de ADLA existente.</span><span class="sxs-lookup"><span data-stu-id="1269b-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="1269b-126">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="1269b-126">Click **Properties**.</span></span>
4. <span data-ttu-id="1269b-127">Ajustar **paralelismo** y **trabajos simultáneos** toosuit sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="1269b-127">Adjust **Parallelism** and **Concurrent Jobs** toosuit your needs.</span></span>

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="1269b-129">Aumento de los límites de cuota máximos</span><span class="sxs-lookup"><span data-stu-id="1269b-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="1269b-130">Cree una petición de soporte técnico en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1269b-130">Open a support request in Azure Portal.</span></span>

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="1269b-133">Seleccione el tipo de problema de hello **cuota**.</span><span class="sxs-lookup"><span data-stu-id="1269b-133">Select hello issue type **Quota**.</span></span>
3. <span data-ttu-id="1269b-134">Seleccione su **Suscripción** (asegúrese de que no sea una suscripción de "prueba").</span><span class="sxs-lookup"><span data-stu-id="1269b-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="1269b-135">Seleccione el tipo de cuota **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="1269b-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="1269b-137">En la hoja de problema de hello, explique el límite de incremento solicitado con **detalles** de por qué necesita esta capacidad adicional.</span><span class="sxs-lookup"><span data-stu-id="1269b-137">In hello problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="1269b-139">Compruebe la información de contacto y crear solicitud de soporte técnico de Hola.</span><span class="sxs-lookup"><span data-stu-id="1269b-139">Verify your contact information and create hello support request.</span></span>

<span data-ttu-id="1269b-140">Microsoft revisa la solicitud e intenta tooaccommodate necesidades de su empresa tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="1269b-140">Microsoft reviews your request and tries tooaccommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1269b-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1269b-141">Next steps</span></span>

* [<span data-ttu-id="1269b-142">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1269b-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="1269b-143">Administración de Análisis de Azure Data Lake mediante Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="1269b-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="1269b-144">Supervisión y solución de problemas de trabajos de Azure Data Lake Analytics con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1269b-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
