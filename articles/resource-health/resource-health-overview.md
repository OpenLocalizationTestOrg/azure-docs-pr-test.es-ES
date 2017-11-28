---
title: "Información general sobre Estado de los recursos de Azure | Microsoft Docs"
description: "Estado de los recursos de Azure. Información general"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: d54979995ca97a70ba92c64915b919da09f548ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="a0378-103">Información general sobre Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="a0378-103">Azure resource health overview</span></span>
 
<span data-ttu-id="a0378-104">Resource Health le ayuda a diagnosticar y obtener soporte técnico cuando un problema de Azure afecta a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="a0378-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="a0378-105">Le informa acerca del mantenimiento actual y pasado de los recursos y le ayuda a mitigar los problemas.</span><span class="sxs-lookup"><span data-stu-id="a0378-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="a0378-106">Resource Health le proporciona soporte técnico si necesita ayuda con los problemas de los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="a0378-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="a0378-107">Mientras que [Estado de Azure](https://status.azure.com) le informa sobre problemas de servicio que afectan a un amplio conjunto de clientes de Azure, Resource Health le proporciona un panel personalizado del estado de los recursos.</span><span class="sxs-lookup"><span data-stu-id="a0378-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span></span> <span data-ttu-id="a0378-108">Resource Health muestra todas las veces que los recursos no estuvieron disponibles en el pasado debido a problemas de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="a0378-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span></span> <span data-ttu-id="a0378-109">Esto facilita comprender si se infringió un Acuerdo de Nivel de Servicio.</span><span class="sxs-lookup"><span data-stu-id="a0378-109">This makes it simple for you to understand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="a0378-110">¿Qué se considera que es un recurso y cómo Resource Health decide si el estado de un recurso es correcto?</span><span class="sxs-lookup"><span data-stu-id="a0378-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="a0378-111">Un recurso es una instancia de un tipo de recurso que un servicio de Azure ofrece a través de Azure Resource Manager, por ejemplo: una máquina virtual, una aplicación web o una base de datos de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a0378-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="a0378-112">Resource Health se basa en las señales que emiten los distintos servicios de Azure para evaluar si el estado de un recurso es correcto o no.</span><span class="sxs-lookup"><span data-stu-id="a0378-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span></span> <span data-ttu-id="a0378-113">Si el estado de un recurso no es correcto, Resource Health analiza información adicional para determinar el origen del problema.</span><span class="sxs-lookup"><span data-stu-id="a0378-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span></span> <span data-ttu-id="a0378-114">También identifica las acciones que lleva a cabo Microsoft para corregir el problema o las acciones que usted puede realizar para solucionar la causa del problema.</span><span class="sxs-lookup"><span data-stu-id="a0378-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span></span> 

<span data-ttu-id="a0378-115">Revise la lista completa de tipos de recurso y comprobaciones de estado en [Azure Resource Health](resource-health-checks-resource-types.md) para detalles adicionales sobre cómo se evalúa el estado de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="a0378-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="a0378-116">Estado de mantenimiento proporcionado por Resource Health</span><span class="sxs-lookup"><span data-stu-id="a0378-116">Health status provided by resource health</span></span>
<span data-ttu-id="a0378-117">Un recurso tiene uno de los siguientes estados:</span><span class="sxs-lookup"><span data-stu-id="a0378-117">The health of a resource is one of the following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="a0378-118">Disponible</span><span class="sxs-lookup"><span data-stu-id="a0378-118">Available</span></span>
<span data-ttu-id="a0378-119">El servicio no ha detectado ningún evento que afecte el estado del recurso.</span><span class="sxs-lookup"><span data-stu-id="a0378-119">The service has not detected any events impacting the health of the resource.</span></span> <span data-ttu-id="a0378-120">En los casos en que el recurso se recuperó de un tiempo de inactividad no planeado durante las últimas 24 horas, verá la notificación de que se **recuperó recientemente**.</span><span class="sxs-lookup"><span data-stu-id="a0378-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span></span>

![Máquina virtual disponible en Resource Health](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="a0378-122">No disponible</span><span class="sxs-lookup"><span data-stu-id="a0378-122">Unavailable</span></span>
<span data-ttu-id="a0378-123">El servicio detectó un evento de plataforma o no de plataforma en curso que afecta el estado del recurso.</span><span class="sxs-lookup"><span data-stu-id="a0378-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="a0378-124">Eventos de plataforma</span><span class="sxs-lookup"><span data-stu-id="a0378-124">Platform events</span></span>
<span data-ttu-id="a0378-125">Estos eventos los desencadenan varios componentes de la infraestructura de Azure e incluyen tanto acciones programadas como mantenimiento planeado o incidentes inesperados, como un reinicio no planeado del host.</span><span class="sxs-lookup"><span data-stu-id="a0378-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="a0378-126">Resource Health proporciona detalles adicionales sobre el evento y el proceso de recuperación y le permite ponerse en contacto con el soporte técnico incluso si no tiene ningún contrato de Soporte técnico de Microsoft activo.</span><span class="sxs-lookup"><span data-stu-id="a0378-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span></span>

![Máquina virtual no disponible en Resource Health debido a un evento de plataforma](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="a0378-128">Eventos no de plataforma</span><span class="sxs-lookup"><span data-stu-id="a0378-128">Non-Platform events</span></span>
<span data-ttu-id="a0378-129">Estos eventos los desencadenan las acciones que realizan los usuarios; por ejemplo, detener una máquina virtual o llegar a la cantidad máxima de conexiones a Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="a0378-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span></span>

![Máquina virtual no disponible en Resource Health debido a un evento no de plataforma](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="a0378-131">Desconocido</span><span class="sxs-lookup"><span data-stu-id="a0378-131">Unknown</span></span>
<span data-ttu-id="a0378-132">Este estado de mantenimiento indica que Resource Health no ha recibido información sobre este recurso durante más de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="a0378-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="a0378-133">Si bien este estado no es una indicación definitiva del estado del recurso, es un punto de datos importante en el proceso de solución de problemas:</span><span class="sxs-lookup"><span data-stu-id="a0378-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span></span>
* <span data-ttu-id="a0378-134">Si el recurso se ejecuta según lo esperado, el estado del recurso cambiará a Disponible después de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="a0378-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span></span>
* <span data-ttu-id="a0378-135">Si tiene problemas con el recurso, el estado de mantenimiento Desconocido podría sugerir que un evento de la plataforma afecta al recurso.</span><span class="sxs-lookup"><span data-stu-id="a0378-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span></span>

![Máquina virtual Desconocida de Resource Health](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="a0378-137">Informe de un estado incorrecto</span><span class="sxs-lookup"><span data-stu-id="a0378-137">Report an incorrect status</span></span>
<span data-ttu-id="a0378-138">Si en algún momento cree que el estado de mantenimiento actual es incorrecto, puede hacérnoslo saber si hace clic en **Informe de estado de mantenimiento incorrecto**.</span><span class="sxs-lookup"><span data-stu-id="a0378-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="a0378-139">En los casos en que lo afecta un problema de Azure, se recomienda que se ponga en contacto con el soporte técnico desde la hoja Resource Health.</span><span class="sxs-lookup"><span data-stu-id="a0378-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span></span> 

![Informe de estado incorrecto en Resource Health](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="a0378-141">Información histórica</span><span class="sxs-lookup"><span data-stu-id="a0378-141">Historical Information</span></span>
<span data-ttu-id="a0378-142">Puede tener acceso a los datos históricos de mantenimiento de hasta 14 días; para ello, haga clic en **Ver el historial** en la hoja Resource Health.</span><span class="sxs-lookup"><span data-stu-id="a0378-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span></span> 

![Historial de informes en Resource Health](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="a0378-144">Introducción</span><span class="sxs-lookup"><span data-stu-id="a0378-144">Getting started</span></span>
<span data-ttu-id="a0378-145">Para abrir Resource Health para un recurso</span><span class="sxs-lookup"><span data-stu-id="a0378-145">To open Resource health for one resource</span></span>
1.  <span data-ttu-id="a0378-146">Inicie sesión en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a0378-146">Sign in into the Azure portal.</span></span>
2.  <span data-ttu-id="a0378-147">Vaya al recurso.</span><span class="sxs-lookup"><span data-stu-id="a0378-147">Navigate to your resource.</span></span>
3.  <span data-ttu-id="a0378-148">En el menú de recursos que se encuentra en el lado izquierdo, haga clic en **Resource Health**.</span><span class="sxs-lookup"><span data-stu-id="a0378-148">In the resource menu located in the left-hand side, click **Resource health**.</span></span>

![Apertura de Resource Health desde la hoja Recurso](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="a0378-150">También puede tener acceso a Resource Health con un clic en **Más servicios** y escribiendo **Resource Health** en el cuadro de texto de filtro para abrir la hoja **Ayuda y soporte técnico**.</span><span class="sxs-lookup"><span data-stu-id="a0378-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span></span> <span data-ttu-id="a0378-151">Por último, haga clic en [**Resource Health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="a0378-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Apertura de Resource Health desde Más servicios](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="a0378-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a0378-153">Next steps</span></span>

<span data-ttu-id="a0378-154">Revise estos recursos para más información sobre Resource Health:</span><span class="sxs-lookup"><span data-stu-id="a0378-154">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="a0378-155">Tipos de recurso y comprobaciones de estado en Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="a0378-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="a0378-156">Preguntas más frecuentes de Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="a0378-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




