---
title: "aaaUpdate Azure módulos de automatización de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="08662-103">¿Cómo tooupdate módulos de PowerShell de Azure en automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="08662-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="08662-104">módulos de PowerShell de Azure más comunes de Hola se proporcionan de forma predeterminada en cada cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="08662-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="08662-105">las actualizaciones del equipo de Azure de Hola Hola módulos de Azure con regularidad, por lo que en hello cuenta de automatización se proporcionan una manera para tooupdate módulos de hello en la cuenta de hello cuando estén disponibles desde el portal de hello las nuevas versiones.</span><span class="sxs-lookup"><span data-stu-id="08662-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="08662-106">Debido a los módulos se actualizan periódicamente por grupo de producto de hello, pueden producirse cambios con los cmdlets de hello incluida, lo que puede afectar negativamente sus runbooks según tipo hello de cambo, como cambiar el nombre de un parámetro o dejando un cmdlet completamente.</span><span class="sxs-lookup"><span data-stu-id="08662-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="08662-107">tooavoid que afectan a los runbooks y Hola procesos automatizan, se recomienda encarecidamente que probar y validar antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="08662-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="08662-108">Si no tiene una cuenta de automatización dedicada diseñada para este propósito, considere la posibilidad de crear uno para que pueda probar muchos escenarios diferentes y permutaciones durante el desarrollo de Hola de sus runbooks, cambios de tooiterative de suma, como la actualización Hola Módulos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08662-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="08662-109">Después de que se validan los resultados de Hola y se les aplique los cambios necesarios, continuar con la migración Hola de los runbooks que requieren la modificación de coordinar y realizar la actualización de hello tal y como se describe a continuación en producción.</span><span class="sxs-lookup"><span data-stu-id="08662-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="08662-110">Actualización de módulos de Azure</span><span class="sxs-lookup"><span data-stu-id="08662-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="08662-111">En los módulos de hello hoja de la cuenta de automatización no existe es una opción denominada **módulos de Azure Update**.</span><span class="sxs-lookup"><span data-stu-id="08662-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="08662-112">Siempre está habilitada.</span><span class="sxs-lookup"><span data-stu-id="08662-112">It is always enabled.</span></span><br><br> <span data-ttu-id="08662-113">![Opción Update Azure Modules (Actualizar módulos de Azure) en la hoja Módulos](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="08662-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="08662-114">Haga clic en **módulos de Azure Update** y aparecerá una notificación de confirmación que le pregunta si desea toocontinue.</span><span class="sxs-lookup"><span data-stu-id="08662-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="08662-115">![Notificación de Update Azure Modules (Actualizar módulos de Azure)](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="08662-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="08662-116">Haga clic en **Sí** y se iniciará el proceso de actualización del módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08662-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="08662-117">proceso de actualización de Hello tarda aproximadamente Hola de tooupdate 15-20 minutos siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="08662-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="08662-118">Azure</span><span class="sxs-lookup"><span data-stu-id="08662-118">Azure</span></span>
  * <span data-ttu-id="08662-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="08662-119">Azure.Storage</span></span>
  * <span data-ttu-id="08662-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="08662-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="08662-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="08662-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="08662-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="08662-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="08662-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="08662-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="08662-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="08662-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="08662-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="08662-125">AzureRm.Storage</span></span>

    <span data-ttu-id="08662-126">Si los módulos de hello ya están en marcha toodate, proceso de Hola se completará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="08662-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="08662-127">Cuando se completa el proceso de actualización de Hola se le notificará.</span><span class="sxs-lookup"><span data-stu-id="08662-127">When hello update process completes you will be notified.</span></span><br><br> ![Estado de actualización de Update Azure Modules (Actualizar módulos de Azure)](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="08662-129">Automatización de Azure utilizará módulos más recientes de hello en su cuenta de automatización cuando se ejecuta un nuevo trabajo programado.</span><span class="sxs-lookup"><span data-stu-id="08662-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="08662-130">Si usa cmdlets de estos módulos de PowerShell de Azure en su toomanage runbooks Azure recursos, es recomendable tooperform este proceso de actualización de cada mes o por lo que tooassure que tienes bienvenida módulos más recientes.</span><span class="sxs-lookup"><span data-stu-id="08662-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08662-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="08662-131">Next steps</span></span>

* <span data-ttu-id="08662-132">toolearn más información acerca de los módulos de integración y cómo integrar toocreate módulos personalizados toofurther la automatización con otros sistemas, servicios o soluciones, consulte [módulos de integración](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="08662-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="08662-133">Considere el uso de la integración de control de origen [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) o [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally administrar y controlar las versiones de la cartera de runbook y la configuración de automatización.</span><span class="sxs-lookup"><span data-stu-id="08662-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
