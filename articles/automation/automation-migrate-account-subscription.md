---
title: "aaaMigrate cuenta de automatización y los recursos | Documentos de Microsoft"
description: "Este artículo describe cómo toomove una automatización de la cuenta en automatización de Azure y recursos asociados de tooanother de una suscripción."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="193ea-103">Migrar una cuenta de Automatización y sus recursos</span><span class="sxs-lookup"><span data-stu-id="193ea-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="193ea-104">Para las cuentas de automatización y los recursos asociados (es decir, activos, runbooks, módulos, etc.) que ha creado en hello portal de Azure y desea toomigrate desde un recurso de grupo tooanother o de tooanother de una suscripción, puede hacerlo fácilmente con Hola [mover recursos](../azure-resource-manager/resource-group-move-resources.md) característica disponible en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="193ea-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="193ea-105">Sin embargo, antes de continuar con esta acción, primero debe revisar siguiente hello [lista de comprobación antes de mover recursos](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) y además, la lista de hello debajo tooAutomation específico.</span><span class="sxs-lookup"><span data-stu-id="193ea-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="193ea-106">grupo de recursos/suscripción de destino de Hello debe estar en la misma región como origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="193ea-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="193ea-107">Es decir, no se pueden mover cuentas de Automatización de una región a otra.</span><span class="sxs-lookup"><span data-stu-id="193ea-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="193ea-108">Al mover los recursos (por ejemplo, runbooks, trabajos, etc.), los grupos de código fuente de Hola y Hola destino se bloquean durante Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="193ea-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="193ea-109">Escribir y eliminar operaciones están bloqueados en grupos de hello hasta que se completa el movimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="193ea-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="193ea-110">Los runbooks o las variables que hacen referencia a un identificador de recursos o suscripción de la suscripción existente Hola deberá toobe actualiza una vez completada la migración.</span><span class="sxs-lookup"><span data-stu-id="193ea-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="193ea-111">Con esta característica no se pueden mover recursos de Automatización clásicos.</span><span class="sxs-lookup"><span data-stu-id="193ea-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="193ea-112">Cuenta de automatización mediante el portal de Hola Hola a toomove</span><span class="sxs-lookup"><span data-stu-id="193ea-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="193ea-113">En su cuenta de automatización, haga clic en **mover** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="193ea-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="193ea-114">![Opción Mover](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="193ea-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="193ea-115">En hello **mover recursos** hoja, tenga en cuenta que presenta tooboth de recursos relacionados con su cuenta de automatización y los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="193ea-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="193ea-116">Seleccione hello **suscripción** y **grupo de recursos** de listas desplegables de Hola u Hola seleccione opción **crear un nuevo grupo de recursos** y escriba un nuevo nombre de grupo de recursos en campo de Hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="193ea-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="193ea-117">Revise y seleccione Hola casilla tooacknowledge se *comprender will scripts y herramientas necesidad toobe actualiza toouse nuevos identificadores de recursos después de que se han movido recursos* y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="193ea-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="193ea-118">![Hoja Mover recursos](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="193ea-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="193ea-119">Esta acción tendrá varias toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="193ea-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="193ea-120">En **Notificaciones**, aparecerá el estado de cada acción que haya tenido lugar: validación, migración y, por último, cuando el proceso finalice.</span><span class="sxs-lookup"><span data-stu-id="193ea-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="193ea-121">toomove Hola cuenta de automatización mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="193ea-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="193ea-122">toomove existente suscripción, utilice Hola o grupo de recursos de automatización recursos tooanother **Get-AzureRmResource** cuenta de automatización específico de cmdlet tooget hello y, a continuación, **Move-AzureRmResource** Mueva el cmdlet tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="193ea-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="193ea-123">Hola primer ejemplo muestra cómo toomove una automatización cuenta tooa nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="193ea-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="193ea-124">Después de ejecutar Hola ejemplo de código anterior, es posible que tooverify solicitada desea tooperform esta acción.</span><span class="sxs-lookup"><span data-stu-id="193ea-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="193ea-125">Una vez que pulses **Sí** y permitirá Hola tooproceed de script, no recibirá ninguna notificación mientras está realizando la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="193ea-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="193ea-126">toomove tooa nueva suscripción, especifique un valor para hello *DestinationSubscriptionId* parámetro.</span><span class="sxs-lookup"><span data-stu-id="193ea-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="193ea-127">Al igual que con el ejemplo anterior de hello, será tooconfirm solicitadas Hola move.</span><span class="sxs-lookup"><span data-stu-id="193ea-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="193ea-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="193ea-128">Next steps</span></span>
* <span data-ttu-id="193ea-129">Para obtener más información acerca de cómo mover grupo de recursos de toonew de recursos o suscripción, vea [Mover grupo de recursos de toonew de recursos o suscripción](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="193ea-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="193ea-130">Para obtener más información sobre el Control de acceso basado en roles en automatización de Azure, consulte demasiado[control de acceso basado en roles en automatización de Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="193ea-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="193ea-131">toolearn acerca de los cmdlets de PowerShell para administrar su suscripción, vea [mediante PowerShell de Azure con el Administrador de recursos](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="193ea-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="193ea-132">toolearn acerca de características del portal para administrar su suscripción, vea [uso de recursos de hello Azure Portal toomanage](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="193ea-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
