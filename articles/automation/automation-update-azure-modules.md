---
title: "Actualización de módulos de Azure en Azure Automation | Microsoft Docs"
description: "En este artículo se describe cómo puede actualizar ahora módulos comunes de Azure PowerShell proporcionados de forma predeterminada en Azure Automation."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: ed8c97b642d406a05817ec6c67f31a1b4bce93b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="da2b2-103">Actualización de módulos de Azure PowerShell en Azure Automation</span><span class="sxs-lookup"><span data-stu-id="da2b2-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="da2b2-104">Los módulos de Azure PowerShell más comunes se proporcionan de forma predeterminada en cada cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="da2b2-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="da2b2-105">El equipo de Azure actualiza los módulos de Azure con regularidad, por lo que en la cuenta de Automation se proporciona una manera de actualizar los módulos de la cuenta cuando hay nuevas versiones disponibles en el portal.</span><span class="sxs-lookup"><span data-stu-id="da2b2-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available from the portal.</span></span>  

<span data-ttu-id="da2b2-106">Dado que el grupo del producto actualiza los módulos con regularidad, pueden producirse cambios con los cmdlets incluidos, lo que puede afectar negativamente a los runbooks según el tipo de cambio, por ejemplo, al cambiar el nombre de un parámetro o al dejar de usar un cmdlet por completo.</span><span class="sxs-lookup"><span data-stu-id="da2b2-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="da2b2-107">Para evitar afectar a los runbooks y a los procesos que automatizan, se recomienda encarecidamente probarlos y validarlos antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="da2b2-107">To avoid impacting your runbooks and the processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="da2b2-108">Si no tiene una cuenta de Automation dedicada destinada para este propósito, considere la posibilidad de crear una para poder probar muchos escenarios y permutaciones diferentes durante el desarrollo de los runbooks, además de los cambios iterativos, como la actualización de los módulos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da2b2-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span>  <span data-ttu-id="da2b2-109">Una vez validados los resultados y aplicados los cambios necesarios, continúe con la coordinación de la migración de los runbooks que requieran modificación y realice la actualización tal y como se describe a continuación en un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="da2b2-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="da2b2-110">Actualización de módulos de Azure</span><span class="sxs-lookup"><span data-stu-id="da2b2-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="da2b2-111">En la hoja Módulos de la cuenta de Automation existe una opción denominada **Update Azure Modules** (Actualizar módulos de Azure).</span><span class="sxs-lookup"><span data-stu-id="da2b2-111">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="da2b2-112">Siempre está habilitada.</span><span class="sxs-lookup"><span data-stu-id="da2b2-112">It is always enabled.</span></span><br><br> <span data-ttu-id="da2b2-113">![Opción Update Azure Modules (Actualizar módulos de Azure) en la hoja Módulos](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="da2b2-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="da2b2-114">Haga clic en **Update Azure Modules** (Actualizar módulos de Azure) y aparecerá una notificación de confirmación que le preguntará si desea continuar.</span><span class="sxs-lookup"><span data-stu-id="da2b2-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="da2b2-115">![Notificación de Update Azure Modules (Actualizar módulos de Azure)](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="da2b2-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="da2b2-116">Haga clic en **Sí** y comenzará el proceso de actualización de módulos.</span><span class="sxs-lookup"><span data-stu-id="da2b2-116">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="da2b2-117">El proceso de actualización tarda aproximadamente 15-20 minutos en actualizar los siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="da2b2-117">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="da2b2-118">Las tablas de Azure</span><span class="sxs-lookup"><span data-stu-id="da2b2-118">Azure</span></span>
  * <span data-ttu-id="da2b2-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="da2b2-119">Azure.Storage</span></span>
  * <span data-ttu-id="da2b2-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="da2b2-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="da2b2-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="da2b2-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="da2b2-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="da2b2-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="da2b2-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="da2b2-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="da2b2-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="da2b2-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="da2b2-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="da2b2-125">AzureRm.Storage</span></span>

    <span data-ttu-id="da2b2-126">Si los módulos ya están actualizados, el proceso se completará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="da2b2-126">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="da2b2-127">Cuando el proceso de actualización se complete, recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="da2b2-127">When the update process completes you will be notified.</span></span><br><br> ![Estado de actualización de Update Azure Modules (Actualizar módulos de Azure)](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="da2b2-129">Azure Automation utilizará los módulos más recientes en su cuenta de Automation cuando se ejecuta un nuevo trabajo programado.</span><span class="sxs-lookup"><span data-stu-id="da2b2-129">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="da2b2-130">Si usa cmdlets de estos módulos de Azure PowerShell en sus runbooks para administrar recursos de Azure, le interesará realizar este proceso de actualización cada mes, por ejemplo, para asegurarse de que dispone de los módulos más recientes.</span><span class="sxs-lookup"><span data-stu-id="da2b2-130">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da2b2-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="da2b2-131">Next steps</span></span>

* <span data-ttu-id="da2b2-132">Para más información sobre los módulos de integración y cómo crear módulos personalizados para integrar Automation con otros sistemas, servicios o soluciones, consulte [Módulos de integración](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="da2b2-132">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="da2b2-133">Considere la integración del control de origen con [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) o [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) para controlar las versiones de la cartera de configuración y el runbook de Automation y administrarlas de forma centralizada.</span><span class="sxs-lookup"><span data-stu-id="da2b2-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  