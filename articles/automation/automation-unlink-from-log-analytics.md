---
title: "cuenta de automatización de Azure de análisis de registros aaaUnlink | Documentos de Microsoft"
description: "Este artículo proporciona información general sobre cómo toounlink la automatización de Azure de la cuenta de un área de trabajo OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="52899-103">¿Cómo toounlink la automatización de la cuenta de un área de trabajo de análisis de registros</span><span class="sxs-lookup"><span data-stu-id="52899-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="52899-104">Automatización de Azure se integra con análisis de registros toonot solo compatibilidad con la supervisión proactiva de los trabajos de runbook a través de todas las cuentas de automatización, pero también es necesario cuando se importa Hola siguiendo las soluciones que dependan de análisis de registros:</span><span class="sxs-lookup"><span data-stu-id="52899-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="52899-105">Administración de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="52899-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="52899-106">Seguimiento de cambios</span><span class="sxs-lookup"><span data-stu-id="52899-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="52899-107">Inicio y detención de máquinas virtuales durante las horas de trabajo</span><span class="sxs-lookup"><span data-stu-id="52899-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="52899-108">Si decide que ya no desea toointegrate su cuenta de automatización con análisis de registros, puede desvincular la cuenta directamente desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="52899-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="52899-109">Antes de continuar, primero deberá soluciones de hello tooremove que se ha mencionado anteriormente, en caso contrario, este proceso se impedirá continuar.</span><span class="sxs-lookup"><span data-stu-id="52899-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="52899-110">Tema de Hola de revisión para solución concreta Hola ha importado pasos de hello toounderstand necesarios tooremove lo.</span><span class="sxs-lookup"><span data-stu-id="52899-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="52899-111">Después de quitar estas soluciones pueden realizar Hola siguiendo los pasos toounlink su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="52899-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="52899-112">Unlink workspace (Desvincular área de trabajo)</span><span class="sxs-lookup"><span data-stu-id="52899-112">Unlink workspace</span></span>

1. <span data-ttu-id="52899-113">En hello portal de Azure, abra su cuenta de automatización y, en la hoja de cuenta de automatización de hello, en la hoja de la cuenta de hello, seleccione **desvincular el área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="52899-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="52899-114">![Opción para desvincular el área de trabajo](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="52899-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="52899-115">En la hoja de hello desvincular área de trabajo, haga clic en **desvincular el área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="52899-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="52899-116">![Hoja Unlink workspace (Desvincular área de trabajo)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="52899-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="52899-117">Recibirá un aviso de comprobar que se va tooproceed.</span><span class="sxs-lookup"><span data-stu-id="52899-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="52899-118">Mientras la automatización de Azure intenta toounlink cuenta de hello en el área de trabajo de análisis de registros, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="52899-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="52899-119">Si ha usado la solución de administración de actualizaciones de hello, opcionalmente, puede que desee hello tooremove siguientes elementos que ya no son necesarios después de quitar la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="52899-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="52899-120">Actualice las programaciones.</span><span class="sxs-lookup"><span data-stu-id="52899-120">Update schedules.</span></span>  <span data-ttu-id="52899-121">Cada uno tendrá nombres que coinciden con las implementaciones de actualizaciones de hello creaste)</span><span class="sxs-lookup"><span data-stu-id="52899-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="52899-122">Grupos de trabajo híbrido creados para la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="52899-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="52899-123">Cada uno de ellos se denominarán del mismo modo demasiado machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="52899-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="52899-124">Si usa máquinas virtuales de inicio/detención de Hola durante la solución de fuera del horario comercial, opcionalmente, puede que desee hello tooremove siguientes elementos que ya no son necesarios después de quitar la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="52899-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="52899-125">Programaciones de runbook de inicio y detención de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="52899-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="52899-126">Runbooks de inicio y detención de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="52899-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="52899-127">Variables</span><span class="sxs-lookup"><span data-stu-id="52899-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="52899-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52899-128">Next steps</span></span>

<span data-ttu-id="52899-129">tooreconfigure su toointegrate de cuenta de automatización con análisis de registros de OMS, consulte [reenviar el estado del trabajo y flujos de trabajo de automatización tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="52899-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 
