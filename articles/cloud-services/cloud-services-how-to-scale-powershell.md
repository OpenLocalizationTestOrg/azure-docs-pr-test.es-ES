---
title: aaaScale un servicio de nube de Azure en Windows PowerShell | Documentos de Microsoft
description: "(clásico) Obtenga información acerca de cómo toouse PowerShell tooscale un rol web o el rol de trabajo o alejar en Azure."
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
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a><span data-ttu-id="cfa64-103">¿Cómo tooscale una nube de servicio en PowerShell</span><span class="sxs-lookup"><span data-stu-id="cfa64-103">How tooscale a cloud service in PowerShell</span></span>

<span data-ttu-id="cfa64-104">Puede usar Windows PowerShell tooscale un rol web o el rol de trabajo o agregando o quitando instancias.</span><span class="sxs-lookup"><span data-stu-id="cfa64-104">You can use Windows PowerShell tooscale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-tooazure"></a><span data-ttu-id="cfa64-105">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="cfa64-105">Log in tooAzure</span></span>

<span data-ttu-id="cfa64-106">Para poder realizar cualquier operación en su suscripción a través de PowerShell, debe iniciar sesión:</span><span class="sxs-lookup"><span data-stu-id="cfa64-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="cfa64-107">Si tiene varias suscripciones asociadas a su cuenta, deberá suscripción actual de hello toochange según donde reside el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="cfa64-107">If you have multiple subscriptions associated with your account, you may need toochange hello current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="cfa64-108">toocheck Hola suscripción actual, ejecute:</span><span class="sxs-lookup"><span data-stu-id="cfa64-108">toocheck hello current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="cfa64-109">Si necesita la suscripción actual de hello toochange, ejecute:</span><span class="sxs-lookup"><span data-stu-id="cfa64-109">If you need toochange hello current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a><span data-ttu-id="cfa64-110">Compruebe el número de instancias actual de hello para el rol</span><span class="sxs-lookup"><span data-stu-id="cfa64-110">Check hello current instance count for your role</span></span>

<span data-ttu-id="cfa64-111">estado actual de hello toocheck de su rol, ejecute:</span><span class="sxs-lookup"><span data-stu-id="cfa64-111">toocheck hello current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="cfa64-112">Obtendrá información sobre el rol de hello, incluidos su número de versión e instancia de SO actual.</span><span class="sxs-lookup"><span data-stu-id="cfa64-112">You should get back information about hello role, including its current OS version and instance count.</span></span> <span data-ttu-id="cfa64-113">En este caso, el rol de hello tiene una sola instancia.</span><span class="sxs-lookup"><span data-stu-id="cfa64-113">In this case, hello role has a single instance.</span></span>

![Obtener información sobre el rol de Hola](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a><span data-ttu-id="cfa64-115">Escalar horizontalmente el rol de hello mediante la adición de más instancias</span><span class="sxs-lookup"><span data-stu-id="cfa64-115">Scale out hello role by adding more instances</span></span>

<span data-ttu-id="cfa64-116">tooscale horizontal de su rol, pase Hola número deseado de instancias como hello **recuento** parámetro toohello **Set-AzureRole** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cfa64-116">tooscale out your role, pass hello desired number of instances as hello **Count** parameter toohello **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="cfa64-117">bloques de cmdlet Hola momentáneamente al nuevas instancias de Hola se aprovisionan y se inicia.</span><span class="sxs-lookup"><span data-stu-id="cfa64-117">hello cmdlet blocks momentarily while hello new instances are provisioned and started.</span></span> <span data-ttu-id="cfa64-118">Durante este tiempo, si abre una nueva ventana de PowerShell y llamada **Get-AzureRole** tal y como se muestra anteriormente, verá recuento de instancias de destino nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="cfa64-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see hello new target instance count.</span></span> <span data-ttu-id="cfa64-119">Y si examina el estado del rol de hello en el portal de hello, debería ver instancia nueva de hello iniciar:</span><span class="sxs-lookup"><span data-stu-id="cfa64-119">And if you inspect hello role status in hello portal, you should see hello new instance starting up:</span></span>

![Instancia de máquina virtual iniciándose en el portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="cfa64-121">Una vez que se hayan iniciado las instancias nuevas de hello, Hola cmdlet devolverá correctamente:</span><span class="sxs-lookup"><span data-stu-id="cfa64-121">Once hello new instances have started, hello cmdlet will return successfully:</span></span>

![Éxito del aumento de instancias de rol](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a><span data-ttu-id="cfa64-123">Escalar en función de hello mediante la eliminación de instancias</span><span class="sxs-lookup"><span data-stu-id="cfa64-123">Scale in hello role by removing instances</span></span>

<span data-ttu-id="cfa64-124">Puede escalar en un rol mediante la eliminación de instancias en hello igual.</span><span class="sxs-lookup"><span data-stu-id="cfa64-124">You can scale in a role by removing instances in hello same way.</span></span> <span data-ttu-id="cfa64-125">Conjunto hello **recuento** parámetro en **Set-AzureRole** toohello número de instancias que desee toohave una vez completada la escala de hello en la operación.</span><span class="sxs-lookup"><span data-stu-id="cfa64-125">Set hello **Count** parameter on **Set-AzureRole** toohello number of instances you want toohave after hello scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfa64-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cfa64-126">Next steps</span></span>

<span data-ttu-id="cfa64-127">No es posible tooconfigure Autoescala para servicios en la nube de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cfa64-127">It is not possible tooconfigure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="cfa64-128">toodo que vea [cómo tooauto escalar un servicio de nube](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cfa64-128">toodo that, see [How tooauto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
