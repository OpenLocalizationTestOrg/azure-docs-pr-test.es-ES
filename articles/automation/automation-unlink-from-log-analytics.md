---
title: "Desvinculación de la cuenta de Azure Automation de Log Analytics | Microsoft Docs"
description: "Este artículo proporciona información general sobre cómo desvincular la cuenta de Azure Automation desde un área de trabajo de OMS."
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
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="6c75f-103">Procedimiento para desvincular su cuenta de Automation de un área de trabajo de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6c75f-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="6c75f-104">Azure Automation se integra con Log Analytics para admitir no solo la supervisión proactiva de los trabajos de runbook a través de todas las cuentas de Azure Automation, pero también es necesario cuando se importan las siguientes soluciones que dependan de Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="6c75f-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="6c75f-105">Administración de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="6c75f-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="6c75f-106">Seguimiento de cambios</span><span class="sxs-lookup"><span data-stu-id="6c75f-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="6c75f-107">Inicio y detención de máquinas virtuales durante las horas de trabajo</span><span class="sxs-lookup"><span data-stu-id="6c75f-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="6c75f-108">Si decide que ya no desea integrar su cuenta de Automation con Log Analytics, puede desvincular la cuenta directamente desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6c75f-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="6c75f-109">Antes de continuar, primero deberá quitar las soluciones mencionados anteriormente, en caso contrario, este proceso le impedirá continuar.</span><span class="sxs-lookup"><span data-stu-id="6c75f-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="6c75f-110">Revise el tema de la solución concreto que ha importado para conocer los pasos necesarios para quitarla.</span><span class="sxs-lookup"><span data-stu-id="6c75f-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="6c75f-111">Después de quitar estas soluciones, puede realizar los pasos siguientes para desvincular la cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="6c75f-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="6c75f-112">Unlink workspace (Desvincular área de trabajo)</span><span class="sxs-lookup"><span data-stu-id="6c75f-112">Unlink workspace</span></span>

1. <span data-ttu-id="6c75f-113">En Azure Portal, abra su cuenta de Automation y, en la hoja de la cuenta de Automation, y en la hoja de la cuenta, seleccione **Unlink workspace** (Desvincular área de trabajo).</span><span class="sxs-lookup"><span data-stu-id="6c75f-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="6c75f-114">![Opción para desvincular el área de trabajo](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="6c75f-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="6c75f-115">En la hoja Unlink workspace (Desvincular área de trabajo), haga clic en **Unlink workspace** (Desvincular área de trabajo).</span><span class="sxs-lookup"><span data-stu-id="6c75f-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="6c75f-116">![Hoja Unlink workspace (Desvincular área de trabajo)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="6c75f-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="6c75f-117">Recibirá un aviso para comprobar que desea continuar.</span><span class="sxs-lookup"><span data-stu-id="6c75f-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="6c75f-118">Aunque Azure Automation trate de desvincular la cuenta del área de trabajo de Log Analytics, puede seguir el progreso en **Notificaciones** en el menú.</span><span class="sxs-lookup"><span data-stu-id="6c75f-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="6c75f-119">Si ha usado la solución de administración de actualizaciones, también puede quitar los siguientes elementos que ya no necesite después de quitar la solución.</span><span class="sxs-lookup"><span data-stu-id="6c75f-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="6c75f-120">Actualice las programaciones.</span><span class="sxs-lookup"><span data-stu-id="6c75f-120">Update schedules.</span></span>  <span data-ttu-id="6c75f-121">Cada uno tendrá nombres que coinciden con las implementaciones de actualizaciones que se ha creado.</span><span class="sxs-lookup"><span data-stu-id="6c75f-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="6c75f-122">Se crean grupos de trabajo híbridos para la solución.</span><span class="sxs-lookup"><span data-stu-id="6c75f-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="6c75f-123">Cada uno de ellos se llamará de forma similar a machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="6c75f-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="6c75f-124">Si ha usado la solución de inicio y detención de máquinas virtuales durante las horas de trabajo, también puede quitar los siguientes elementos que ya no necesite después de quitar la solución.</span><span class="sxs-lookup"><span data-stu-id="6c75f-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="6c75f-125">Programaciones de runbook de inicio y detención de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6c75f-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="6c75f-126">Runbooks de inicio y detención de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6c75f-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="6c75f-127">Variables</span><span class="sxs-lookup"><span data-stu-id="6c75f-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="6c75f-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c75f-128">Next steps</span></span>

<span data-ttu-id="6c75f-129">Para volver a configurar la cuenta de Automation para integrarla con Log Analytics de OMS, consulte [Reenvío del estado de un trabajo y de transmisiones de trabajos desde Automation a Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="6c75f-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 