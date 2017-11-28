---
title: Aviso de retirada de la familia 1 del SO invitado | Microsoft Docs
description: "Proporciona información acerca de cuándo se produjo la retirada de la familia 1 del SO invitado de Azure y cómo determinar si el usuario se ve afectado."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: 3178a09dab1cb972a3460d54dc9908fb95cce68b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="24b90-103">Aviso de retirada de la familia 1 del SO invitado</span><span class="sxs-lookup"><span data-stu-id="24b90-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="24b90-104">La retirada de la familia 1 del SO se anunció por primera vez el 1 de junio de 2013.</span><span class="sxs-lookup"><span data-stu-id="24b90-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="24b90-105">**2 de septiembre de 2014** La familia 1.x del sistema operativo invitado (SO invitado) de Azure, basada en el sistema operativo Windows Server 2008, se retiró oficialmente.</span><span class="sxs-lookup"><span data-stu-id="24b90-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="24b90-106">Todos los intentos para implementar nuevos servicios o actualizar los ya existentes mediante la familia 1 generarán un mensaje de error que informa de que la familia 1 del SO invitado se ha retirado.</span><span class="sxs-lookup"><span data-stu-id="24b90-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="24b90-107">**3 de noviembre de 2014** El soporte extendido para la familia 1 del SO invitado finaliza y se retira completamente.</span><span class="sxs-lookup"><span data-stu-id="24b90-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="24b90-108">Todos los servicios todavía en la familia 1 se verá afectados.</span><span class="sxs-lookup"><span data-stu-id="24b90-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="24b90-109">Podemos detener dichos servicios en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="24b90-109">We may stop those services at any time.</span></span> <span data-ttu-id="24b90-110">No existen garantías de que los servicios continúen ejecutándose a menos que los actualice manualmente.</span><span class="sxs-lookup"><span data-stu-id="24b90-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="24b90-111">Si tiene más preguntas, visite los [foros de Cloud Services](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) o [póngase en contacto con el soporte técnico de Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="24b90-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="24b90-112">Cómo saber si se ve afectado</span><span class="sxs-lookup"><span data-stu-id="24b90-112">Are you affected?</span></span>
<span data-ttu-id="24b90-113">Si se observa cualquiera de las situaciones siguientes,sus servicios en la nube se ven afectados:</span><span class="sxs-lookup"><span data-stu-id="24b90-113">Your Cloud Services are affected if any one of the following applies:</span></span>

1. <span data-ttu-id="24b90-114">Se especifica de manera explícita el valor "osFamily = "1" en el archivo ServiceConfiguration.cscfg del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="24b90-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="24b90-115">No se especifica ningún valor explícitamente para osFamily en el archivo ServiceConfiguration.cscfg del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="24b90-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="24b90-116">Actualmente, el sistema usa el valor predeterminado de "1" en este caso.</span><span class="sxs-lookup"><span data-stu-id="24b90-116">Currently, the system uses the default value of "1" in this case.</span></span>
3. <span data-ttu-id="24b90-117">Azure Portal muestra el valor de la familia del sistema operativo invitado como "Windows Server 2008".</span><span class="sxs-lookup"><span data-stu-id="24b90-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="24b90-118">Para determinar la familia de SO que ejecuta cada servicio en la nube, puede ejecutar el siguiente script en Azure PowerShell, aunque antes debe [configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="24b90-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="24b90-119">Para más información acerca del script, consulte [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx) (Final de la vida de la familia 1 del SO invitado de Azure: junio de 2014).</span><span class="sxs-lookup"><span data-stu-id="24b90-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="24b90-120">Los servicios en la nube se verán afectados por la retirada de la familia 1 del SO si la columna osFamily del resultado del script está vacía o contiene un "1".</span><span class="sxs-lookup"><span data-stu-id="24b90-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="24b90-121">Recomendaciones en caso de verse afectado</span><span class="sxs-lookup"><span data-stu-id="24b90-121">Recommendations if you are affected</span></span>
<span data-ttu-id="24b90-122">Se recomienda migrar los roles de los servicios en la nube a una de las familias del SO invitado compatibles:</span><span class="sxs-lookup"><span data-stu-id="24b90-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span></span>

<span data-ttu-id="24b90-123">**Familia 4.x del SO invitado** : Windows Server 2012 R2 *(recomendado)*</span><span class="sxs-lookup"><span data-stu-id="24b90-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="24b90-124">Asegúrese de que la aplicación use el SDK 2.1 o posterior con .NET Framework 4.0, 4.5 o 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="24b90-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="24b90-125">Establezca el atributo osFamily en “4” en el archivo ServiceConfiguration.cscfg y vuelva a implementar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="24b90-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="24b90-126">**Familia 3.x del SO invitado** : Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="24b90-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="24b90-127">Asegúrese de que la aplicación use el SDK 1.8 o posterior con .NET Framework 4.0 o 4.5.</span><span class="sxs-lookup"><span data-stu-id="24b90-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="24b90-128">Establezca el atributo osFamily en “3” en el archivo ServiceConfiguration.cscfg y vuelva a implementar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="24b90-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="24b90-129">**Familia 2.x del SO invitado** : Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="24b90-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="24b90-130">Asegúrese de que la aplicación use el SDK 1.3 o posterior con .NET Framework 3.5 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="24b90-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="24b90-131">Establezca el atributo osFamily en "2" en el archivo ServiceConfiguration.cscfg y vuelva a implementar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="24b90-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="24b90-132">El soporte extendido para la familia 1 del SO invitado finalizó el 3 de noviembre de 2014.</span><span class="sxs-lookup"><span data-stu-id="24b90-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="24b90-133">Los servicios en la nube de la familia 1 del SO invitado ya no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="24b90-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="24b90-134">Migre la familia 1 lo antes posible para evitar la interrupción del servicio.</span><span class="sxs-lookup"><span data-stu-id="24b90-134">Migrate off family 1 as soon as possible to avoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="24b90-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24b90-135">Next steps</span></span>
<span data-ttu-id="24b90-136">Revise las [versiones del SO invitado](cloud-services-guestos-update-matrix.md)más recientes.</span><span class="sxs-lookup"><span data-stu-id="24b90-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
