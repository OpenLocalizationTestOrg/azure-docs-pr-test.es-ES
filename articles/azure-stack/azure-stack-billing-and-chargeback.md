---
title: "Facturación y anulación de Azure la pila aaaCustomer | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooretrieve información de uso de recursos de pila de Azure."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: a9afc7b6-43da-437b-a853-aab73ff14113
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: d92caac2874e5364870b29a38515b579ab059991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="usage-and-billing-in-azure-stack"></a><span data-ttu-id="526ae-103">Utilización y facturación en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="526ae-103">Usage and billing in Azure Stack</span></span>

<span data-ttu-id="526ae-104">Uso representa la cantidad de Hola de los recursos utilizados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="526ae-104">Usage represents hello quantity of resources consumed by a user.</span></span> <span data-ttu-id="526ae-105">Pila de Azure recopila información de uso para cada usuario y la usa toobill ellos.</span><span class="sxs-lookup"><span data-stu-id="526ae-105">Azure Stack collects usage information for each user and uses it toobill them.</span></span> <span data-ttu-id="526ae-106">Este artículo describe cómo se facturarán a los usuarios de la pila de Azure para uso de recursos y cómo se tiene acceso a información de facturación de hello para el análisis, anulación, etcetera.</span><span class="sxs-lookup"><span data-stu-id="526ae-106">This article describes how Azure Stack users are billed for resource usage, and how hello billing information is accessed for analytics, chargeback, etc.</span></span>

<span data-ttu-id="526ae-107">Pila de Azure contiene hello toocollect de infraestructura y los datos de uso agregadas para todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="526ae-107">Azure Stack contains hello infrastructure toocollect and aggregate usage data for all resources.</span></span> <span data-ttu-id="526ae-108">Puede tener acceso a estos datos y exportar el sistema de facturación tooa mediante el uso de un adaptador de facturación o exportarlo tooa herramienta de inteligencia empresarial como Microsoft Power BI.</span><span class="sxs-lookup"><span data-stu-id="526ae-108">You can access this data and export it tooa billing system by using a billing adapter, or export it tooa business intelligence tool like Microsoft Power BI.</span></span> <span data-ttu-id="526ae-109">Una vez exportado, esta información de facturación se utiliza para el análisis o transferidas tooa sistema de cargo al usuario.</span><span class="sxs-lookup"><span data-stu-id="526ae-109">After exporting, this billing information is used for analytics or transferred tooa chargeback system.</span></span>

![Modelo conceptual de un adaptador de facturación conectando Azure pila tooa aplicación de facturación](media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a><span data-ttu-id="526ae-111">¿Qué información de utilización se puede encontrar y cómo?</span><span class="sxs-lookup"><span data-stu-id="526ae-111">What usage information can I find, and how?</span></span>

<span data-ttu-id="526ae-112">Los proveedores de recursos de Azure Stack como, por ejemplo, Compute, Storage y Network, generan datos de utilización a intervalos de horas para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="526ae-112">Azure Stack Resource providers, such as Compute, Storage, and Network, generate usage data at hourly intervals for each subscription.</span></span> <span data-ttu-id="526ae-113">datos de uso Hello contienen información acerca de recursos de hello usa como nombre del recurso, medidor de la cantidad de nombre, identificador de medidor, usados toolearn etc. acerca de los recursos de Id. de hello metros, consulte toohello [uso de preguntas más frecuentes de API](azure-stack-usage-related-faq.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="526ae-113">hello usage data contains information about hello resource used such as resource name, meter name, meter ID, quantity used etc. toolearn about hello meters ID resources, refer toohello [usage API FAQ](azure-stack-usage-related-faq.md) article.</span></span> 

<span data-ttu-id="526ae-114">Después de que se han recopilado datos de uso de hello, resulta [notificado tooAzure](azure-stack-usage-reporting.md) toogenerate una factura, que se puede ver a través de hello Azure portal de facturación.</span><span class="sxs-lookup"><span data-stu-id="526ae-114">After hello usage data has been collected, it is [reported tooAzure](azure-stack-usage-reporting.md) toogenerate a bill, which can be viewed through hello Azure billing portal.</span></span> <span data-ttu-id="526ae-115">Hola portal de facturación de Azure muestra los datos de uso de hello sólo de recursos facturables Hola.</span><span class="sxs-lookup"><span data-stu-id="526ae-115">hello Azure billing portal shows hello usage data only for hello chargeable resources.</span></span> <span data-ttu-id="526ae-116">Además, toohello facturables recursos, pila de Azure captura datos de uso de un conjunto más amplio de recursos, que se pueden tener acceso a su entorno de pila de Azure a través de la API de REST o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="526ae-116">In addition toohello chargeable resources, Azure Stack captures usage data for a broader set of resources, which you can access in your Azure Stack environment through REST APIs or PowerShell.</span></span> <span data-ttu-id="526ae-117">Los administradores de la nube de Azure pila pueden recuperar los datos de uso de Hola para todas las suscripciones de usuario, mientras que un usuario puede obtener solamente los detalles de uso.</span><span class="sxs-lookup"><span data-stu-id="526ae-117">Azure Stack cloud administrators can retrieve hello usage data for all user subscriptions whereas a user can get only their usage details.</span></span>

## <a name="retrieve-usage-information"></a><span data-ttu-id="526ae-118">Recuperar información de utilización</span><span class="sxs-lookup"><span data-stu-id="526ae-118">Retrieve usage information</span></span>

<span data-ttu-id="526ae-119">datos de uso de hello toogenerate, debe tener recursos que se ejecuta y se usa activamente sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="526ae-119">toogenerate hello usage data, you should have resources that are running and actively using hello system.</span></span> <span data-ttu-id="526ae-120">Si no está seguro de si tiene algún recurso que se ejecuta en Azure Marketplace de pila, implementar una máquina virtual (VM) y comprobar Hola VM supervisión hoja toomake seguro de se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="526ae-120">If you’re not sure whether you have any resources running in Azure Stack Marketplace, deploy a virtual machine (VM), and verify hello VM monitoring blade toomake sure it’s running.</span></span> <span data-ttu-id="526ae-121">Usar hello datos de uso de PowerShell cmdlets tooview Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="526ae-121">Use hello following PowerShell cmdlets tooview hello usage data:</span></span>

1. [<span data-ttu-id="526ae-122">Instale PowerShell para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="526ae-122">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)
2. * <span data-ttu-id="526ae-123">[Configurar hello Azure pila usuario](azure-stack-powershell-configure-user.md) o hello [del operador de la pila de Azure](azure-stack-powershell-configure-admin.md) entorno de PowerShell</span><span class="sxs-lookup"><span data-stu-id="526ae-123">[Configure hello Azure Stack user's](azure-stack-powershell-configure-user.md) or hello [Azure Stack operator's](azure-stack-powershell-configure-admin.md) PowerShell environment</span></span> 
3. <span data-ttu-id="526ae-124">datos de uso de hello tooretrieve, usar hello [UsageAggregates Get](/powershell/module/azurerm.usageaggregates/get-usageaggregates) cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="526ae-124">tooretrieve hello usage data, use hello [Get-UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) PowerShell cmdlet:</span></span>
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   <span data-ttu-id="526ae-125">Si hay datos de uso, se devuelve en tal y como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="526ae-125">If usage data is available, it’s returned in as shown in hello following screenshot:</span></span> 
   
   ![Agregados de utilización](media/azure-stack-billing-and-chargeback/image2.png)
   
   <span data-ttu-id="526ae-127">PowerShell devuelve 1000 líneas de utilización por llamada.</span><span class="sxs-lookup"><span data-stu-id="526ae-127">PowerShell returns 1,000 lines of usage per call.</span></span> <span data-ttu-id="526ae-128">Puede usar más de 1.000 líneas Hola continuación parámetro tooretrieve</span><span class="sxs-lookup"><span data-stu-id="526ae-128">You can use hello continuation parameter tooretrieve more than 1,000 lines</span></span>

## <a name="next-steps"></a><span data-ttu-id="526ae-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="526ae-129">Next steps</span></span>

[<span data-ttu-id="526ae-130">Informe tooAzure de datos de uso de la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="526ae-130">Report Azure Stack usage data tooAzure</span></span>](azure-stack-usage-reporting.md)

<span data-ttu-id="526ae-131">[Provider Resource Usage API](azure-stack-provider-resource-api.md) (API de utilización de recursos de proveedor)</span><span class="sxs-lookup"><span data-stu-id="526ae-131">[Provider Resource Usage API](azure-stack-provider-resource-api.md)</span></span>

<span data-ttu-id="526ae-132">[Tenant Resource Usage API](azure-stack-tenant-resource-usage-api.md) (API de utilización de recursos de inquilino)</span><span class="sxs-lookup"><span data-stu-id="526ae-132">[Tenant Resource Usage API](azure-stack-tenant-resource-usage-api.md)</span></span>

<span data-ttu-id="526ae-133">[Usage-related FAQ](azure-stack-usage-related-faq.md) (P+F relacionadas con la utilización)</span><span class="sxs-lookup"><span data-stu-id="526ae-133">[Usage-related FAQ](azure-stack-usage-related-faq.md)</span></span>

