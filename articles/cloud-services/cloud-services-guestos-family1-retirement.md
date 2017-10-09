---
title: familia de SO aaaGuest 1 retirada Observe | Documentos de Microsoft
description: "Proporciona información acerca de cuándo se produjeron retirada Hola familia 1 del SO de invitado de Azure y cómo toodetermine si se ve afectado"
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
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="c93bc-103">Aviso de retirada de la familia 1 del SO invitado</span><span class="sxs-lookup"><span data-stu-id="c93bc-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="c93bc-104">retirada de Hola de familia 1 del SO se presentó por primera vez en el 1 de junio de 2013.</span><span class="sxs-lookup"><span data-stu-id="c93bc-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="c93bc-105">**2 de septiembre de 2014** hello Azure sistema operativo (SO invitado) familia 1.x, que se basa en el sistema operativo de Windows Server 2008 hello, se retira oficialmente.</span><span class="sxs-lookup"><span data-stu-id="c93bc-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="c93bc-106">Todos los intentos de toodeploy nuevos servicios o actualizar servicios existentes con la familia 1 se producirá un error con un mensaje de error que informa que Hola que se ha retirado la familia 1 del SO invitado.</span><span class="sxs-lookup"><span data-stu-id="c93bc-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="c93bc-107">**3 de noviembre de 2014** El soporte extendido para la familia 1 del SO invitado finaliza y se retira completamente.</span><span class="sxs-lookup"><span data-stu-id="c93bc-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="c93bc-108">Todos los servicios todavía en la familia 1 se verá afectados.</span><span class="sxs-lookup"><span data-stu-id="c93bc-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="c93bc-109">Podemos detener dichos servicios en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="c93bc-109">We may stop those services at any time.</span></span> <span data-ttu-id="c93bc-110">No hay ninguna garantía de que los servicios continúen toorun a menos que los actualice manualmente.</span><span class="sxs-lookup"><span data-stu-id="c93bc-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="c93bc-111">Si tiene preguntas adicionales, visite hello [foros de servicios de nube](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) o [póngase en contacto con soporte técnico de Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="c93bc-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="c93bc-112">Cómo saber si se ve afectado</span><span class="sxs-lookup"><span data-stu-id="c93bc-112">Are you affected?</span></span>
<span data-ttu-id="c93bc-113">Servicios en la nube se ven afectados si se aplica cualquiera de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="c93bc-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="c93bc-114">Tiene un valor de "osFamily ="1"especifica explícitamente en el archivo ServiceConfiguration.cscfg de hello para el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="c93bc-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="c93bc-115">No tiene un valor para osFamily especifica explícitamente en el archivo ServiceConfiguration.cscfg de hello para el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="c93bc-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="c93bc-116">Actualmente, sistema de Hola usa Hola predeterminado valor de "1" en este caso.</span><span class="sxs-lookup"><span data-stu-id="c93bc-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="c93bc-117">Hola portal de Azure indica el valor de familia de sistema operativo invitado como "Windows Server 2008".</span><span class="sxs-lookup"><span data-stu-id="c93bc-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="c93bc-118">toofind qué de servicios en la nube qué familia del SO se están ejecutando, puede ejecutar Hola siguiente secuencia de comandos de PowerShell de Azure, aunque primero debe [configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) primero.</span><span class="sxs-lookup"><span data-stu-id="c93bc-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="c93bc-119">Para obtener más información sobre el script de Hola, consulte [Azure invitado SO familia 1 final del ciclo de vida: junio de 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="c93bc-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="c93bc-120">Servicios en la nube se verá afectados por la familia 1 del SO retirada si la columna de osFamily hello en la salida del script de Hola está vacío o contiene un "1".</span><span class="sxs-lookup"><span data-stu-id="c93bc-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="c93bc-121">Recomendaciones en caso de verse afectado</span><span class="sxs-lookup"><span data-stu-id="c93bc-121">Recommendations if you are affected</span></span>
<span data-ttu-id="c93bc-122">Se recomienda que migre su tooone de roles de servicio en la nube de familias del SO invitado Hola admitida:</span><span class="sxs-lookup"><span data-stu-id="c93bc-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="c93bc-123">**Familia 4.x del SO invitado** : Windows Server 2012 R2 *(recomendado)*</span><span class="sxs-lookup"><span data-stu-id="c93bc-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="c93bc-124">Asegúrese de que la aplicación use el SDK 2.1 o posterior con .NET Framework 4.0, 4.5 o 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="c93bc-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="c93bc-125">Establecer archivo ServiceConfiguration.cscfg de hello osFamily atributo hello en demasiado "4" y volver a implementar su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="c93bc-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="c93bc-126">**Familia 3.x del SO invitado** : Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c93bc-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="c93bc-127">Asegúrese de que la aplicación use el SDK 1.8 o posterior con .NET Framework 4.0 o 4.5.</span><span class="sxs-lookup"><span data-stu-id="c93bc-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="c93bc-128">Establecer archivo ServiceConfiguration.cscfg de hello osFamily atributo hello en demasiado "3" y volver a implementar su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="c93bc-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="c93bc-129">**Familia 2.x del SO invitado** : Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c93bc-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="c93bc-130">Asegúrese de que la aplicación use el SDK 1.3 o posterior con .NET Framework 3.5 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="c93bc-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="c93bc-131">Establecer archivo ServiceConfiguration.cscfg de hello osFamily atributo hello en demasiado "2" y vuelva a implementar el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="c93bc-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="c93bc-132">El soporte extendido para la familia 1 del SO invitado finalizó el 3 de noviembre de 2014.</span><span class="sxs-lookup"><span data-stu-id="c93bc-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="c93bc-133">Los servicios en la nube de la familia 1 del SO invitado ya no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="c93bc-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="c93bc-134">Migre la familia 1 tan pronto como tooavoid posibles interrupciones de servicio.</span><span class="sxs-lookup"><span data-stu-id="c93bc-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c93bc-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c93bc-135">Next steps</span></span>
<span data-ttu-id="c93bc-136">Hola de revisión más reciente [versiones del SO invitado](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="c93bc-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
