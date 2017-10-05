---
title: Escalado de un servicio en la nube de Azure en Windows PowerShell | Microsoft Docs
description: "(modelo clásico) Aprenda a usar PowerShell para escalar o reducir horizontalmente un rol web o de trabajo en Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="2bdc4-103">Escalado de un servicio en la nube en PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bdc4-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="2bdc4-104">Puede usar Windows PowerShell para escalar o reducir horizontalmente un rol web o de trabajo mediante la adición o eliminación de instancias.</span><span class="sxs-lookup"><span data-stu-id="2bdc4-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="2bdc4-105">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="2bdc4-105">Log in to Azure</span></span>

<span data-ttu-id="2bdc4-106">Para poder realizar cualquier operación en su suscripción a través de PowerShell, debe iniciar sesión:</span><span class="sxs-lookup"><span data-stu-id="2bdc4-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="2bdc4-107">Si tiene varias suscripciones asociadas a su cuenta, puede que deba cambiar la suscripción actual (según donde resida el servicio en la nube).</span><span class="sxs-lookup"><span data-stu-id="2bdc4-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="2bdc4-108">Para comprobar la suscripción actual, ejecute:</span><span class="sxs-lookup"><span data-stu-id="2bdc4-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="2bdc4-109">Si necesita cambiar la suscripción actual, ejecute:</span><span class="sxs-lookup"><span data-stu-id="2bdc4-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="2bdc4-110">Comprobación del número actual de instancias para el rol</span><span class="sxs-lookup"><span data-stu-id="2bdc4-110">Check the current instance count for your role</span></span>

<span data-ttu-id="2bdc4-111">Para comprobar el estado actual de su rol, ejecute:</span><span class="sxs-lookup"><span data-stu-id="2bdc4-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="2bdc4-112">Obtendrá información sobre el rol, como su versión actual de SO y el número de instancias.</span><span class="sxs-lookup"><span data-stu-id="2bdc4-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="2bdc4-113">En este caso, el rol tiene una sola instancia.</span><span class="sxs-lookup"><span data-stu-id="2bdc4-113">In this case, the role has a single instance.</span></span>

![Información sobre el rol](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="2bdc4-115">Escalado horizontal del rol mediante la adición de más instancias</span><span class="sxs-lookup"><span data-stu-id="2bdc4-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="2bdc4-116">Para escalar horizontalmente su rol, pase el número deseado de instancias como el parámetro **Count** al cmdlet **Set-AzureRole**:</span><span class="sxs-lookup"><span data-stu-id="2bdc4-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="2bdc4-117">El cmdlet se bloquea momentáneamente mientras las nuevas instancias se aprovisionan e inician.</span><span class="sxs-lookup"><span data-stu-id="2bdc4-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="2bdc4-118">Durante este tiempo, si abre una nueva ventana de PowerShell y llama a **Get-AzureRole** como se mostró anteriormente, verá el nuevo recuento de instancias de destino.</span><span class="sxs-lookup"><span data-stu-id="2bdc4-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="2bdc4-119">Y si examina el estado del rol en el portal, verá que se inicia la nueva instancia:</span><span class="sxs-lookup"><span data-stu-id="2bdc4-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![Instancia de máquina virtual iniciándose en el portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="2bdc4-121">Cuando se hayan iniciado las nuevas instancias, el cmdlet devolverá resultados correctamente:</span><span class="sxs-lookup"><span data-stu-id="2bdc4-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![Éxito del aumento de instancias de rol](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="2bdc4-123">Reducción horizontal del rol mediante la eliminación de instancias</span><span class="sxs-lookup"><span data-stu-id="2bdc4-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="2bdc4-124">Puede reducir un rol horizontalmente quitando instancias de la misma manera.</span><span class="sxs-lookup"><span data-stu-id="2bdc4-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="2bdc4-125">Establezca el parámetro **Count** de **Set-AzureRole** en el número de instancias que quiere tener después de que finalice la operación de reducción horizontal.</span><span class="sxs-lookup"><span data-stu-id="2bdc4-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bdc4-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2bdc4-126">Next steps</span></span>

<span data-ttu-id="2bdc4-127">No es posible configurar el escalado automático para los servicios en la nube de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bdc4-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="2bdc4-128">Para ello, consulte [Cómo escalar automáticamente un servicio en la nube](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2bdc4-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
