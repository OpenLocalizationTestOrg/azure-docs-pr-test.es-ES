---
title: "Migración de una cuenta de Automation y sus recursos | Microsoft Docs"
description: "En este artículo se describe cómo mover una cuenta de Automatización en Automatización de Azure y sus recursos relacionados correspondientes de una suscripción a otra."
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
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="f58d3-103">Migrar una cuenta de Automatización y sus recursos</span><span class="sxs-lookup"><span data-stu-id="f58d3-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="f58d3-104">Para las cuentas de Automation y los recursos asociados (es decir, recuros, runbooks, módulos, etc.) que ha creado en Azure Portal y que desea migrar de un grupo de recursos a otro o de una suscripción a otra, puede hacerlo fácilmente con la característica de [mover recursos](../azure-resource-manager/resource-group-move-resources.md), disponible en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f58d3-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="f58d3-105">Pero, antes de llevar esto a cabo, conviene revisar la siguiente [lista de comprobación antes de mover recursos](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) y, además, la siguiente lista específica de Automation.</span><span class="sxs-lookup"><span data-stu-id="f58d3-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="f58d3-106">El grupo de recursos/suscripción de destino debe estar en la misma región que el origen.</span><span class="sxs-lookup"><span data-stu-id="f58d3-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="f58d3-107">Es decir, no se pueden mover cuentas de Automatización de una región a otra.</span><span class="sxs-lookup"><span data-stu-id="f58d3-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="f58d3-108">Al mover recursos (por ejemplo, Runbooks, trabajos, etc.), el grupo de origen y el grupo de destino se bloquean durante la operación.</span><span class="sxs-lookup"><span data-stu-id="f58d3-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="f58d3-109">Las operaciones de escritura y eliminación están bloqueadas en los grupos hasta que se completa el movimiento.</span><span class="sxs-lookup"><span data-stu-id="f58d3-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="f58d3-110">Los Runbooks o variables que hacen referencia a un identificador de suscripción o recurso de la suscripción existente deben actualizarse después de completar la migración.</span><span class="sxs-lookup"><span data-stu-id="f58d3-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="f58d3-111">Con esta característica no se pueden mover recursos de Automatización clásicos.</span><span class="sxs-lookup"><span data-stu-id="f58d3-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="f58d3-112">Para mover la cuenta de Automatización a través del Portal</span><span class="sxs-lookup"><span data-stu-id="f58d3-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="f58d3-113">En la cuenta de Automation, haga clic en **Mover** en la parte superior de la hoja. </span><span class="sxs-lookup"><span data-stu-id="f58d3-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="f58d3-114">![Opción Mover](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="f58d3-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="f58d3-115">En la hoja **Mover recursos** , vea que se muestran recursos relacionados tanto con la cuenta de Automatización como con los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="f58d3-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="f58d3-116">Seleccione la **suscripción** y el **grupo de recursos** en las listas desplegables, o seleccione la opción **Crear un nuevo grupo de recursos** y escriba el nombre del nuevo grupo de recursos en el campo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="f58d3-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="f58d3-117">Revise y active la casilla *Entiendo que las herramientas y los scripts necesitarán actualizarse para usar los nuevos identificadores de recursos después de que los recursos se hayan movido*. Tras ello, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f58d3-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="f58d3-118">![Hoja Mover recursos](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="f58d3-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="f58d3-119">Este paso puede tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="f58d3-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="f58d3-120">En **Notificaciones**, aparecerá el estado de cada acción que haya tenido lugar: validación, migración y, por último, cuando el proceso finalice.</span><span class="sxs-lookup"><span data-stu-id="f58d3-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="f58d3-121">Para mover la cuenta de Automatización con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f58d3-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="f58d3-122">Para mover los recursos de Automation existentes a otro grupo de recursos o suscripción, use el cmdlet **Get-AzureRmResource** para obtener la cuenta de Automation específica y, después, el **Move-AzureRmResource** para realizar el movimiento.</span><span class="sxs-lookup"><span data-stu-id="f58d3-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="f58d3-123">El primer ejemplo muestra cómo mover una cuenta de Automatización a un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f58d3-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="f58d3-124">Después de ejecutar el ejemplo de código anterior, se le pedirá que confirme que quiere realizar esta acción.</span><span class="sxs-lookup"><span data-stu-id="f58d3-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="f58d3-125">Cuando haga clic en **Sí** y deje que el script continúe, no recibirá ninguna notificación mientras la migración se realiza.</span><span class="sxs-lookup"><span data-stu-id="f58d3-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="f58d3-126">Para moverlos a una nueva suscripción, especifique un valor para el parámetro *DestinationSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="f58d3-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="f58d3-127">Al igual que en el ejemplo anterior, se le pedirá que confirme el movimiento.</span><span class="sxs-lookup"><span data-stu-id="f58d3-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f58d3-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f58d3-128">Next steps</span></span>
* <span data-ttu-id="f58d3-129">Para más información sobre cómo mover recursos a un nuevo grupo de recursos o a una nueva suscripción, consulte [Traslado de los recursos a un nuevo grupo de recursos o a una nueva suscripción](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="f58d3-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="f58d3-130">Para más información acerca del control de acceso basado en rol de Automatización de Azure, consulte [Control de acceso basado en rol en Automatización de Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="f58d3-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="f58d3-131">Para más información sobre los cmdlets de PowerShell que permiten administrar su suscripción, vea [Uso de Azure PowerShell con Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="f58d3-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="f58d3-132">Para conocer las características del Portal que permiten administrar la suscripción, vea [Uso del Portal de Azure para implementar y administrar los recursos de Azure](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f58d3-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
