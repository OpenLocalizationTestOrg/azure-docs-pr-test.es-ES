---
title: "información general sobre el mantenimiento de recursos aaaAzure | Documentos de Microsoft"
description: "Estado de los recursos de Azure. Información general"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="ed019-103">Información general sobre Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="ed019-103">Azure resource health overview</span></span>
 
<span data-ttu-id="ed019-104">Resource Health le ayuda a diagnosticar y obtener soporte técnico cuando un problema de Azure afecta a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="ed019-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="ed019-105">Le informa sobre el estado de hello actuales y pasadas de los recursos y le ayuda a mitigar los problemas.</span><span class="sxs-lookup"><span data-stu-id="ed019-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="ed019-106">Resource Health le proporciona soporte técnico si necesita ayuda con los problemas de los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed019-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="ed019-107">Mientras que [estado de Azure](https://status.azure.com) le informa sobre los problemas de servicio que afectan a un amplio conjunto de los clientes de Azure, el estado de los recursos, obtendrá un panel personalizado de mantenimiento de Hola de los recursos.</span><span class="sxs-lookup"><span data-stu-id="ed019-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="ed019-108">Estado de los recursos muestra todos los tiempos de hello los recursos no estaban disponibles en hello vencido tooAzure problemas del servicio.</span><span class="sxs-lookup"><span data-stu-id="ed019-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="ed019-109">Esto facilita para toounderstand si se infringe un SLA.</span><span class="sxs-lookup"><span data-stu-id="ed019-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="ed019-110">¿Qué se considera que es un recurso y cómo Resource Health decide si el estado de un recurso es correcto?</span><span class="sxs-lookup"><span data-stu-id="ed019-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="ed019-111">Un recurso es una instancia de un tipo de recurso que un servicio de Azure ofrece a través de Azure Resource Manager, por ejemplo: una máquina virtual, una aplicación web o una base de datos de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ed019-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="ed019-112">Estado de los recursos se basa en señales emitidas por hello distintos servicios de Azure tooassess si un recurso es correcto o no.</span><span class="sxs-lookup"><span data-stu-id="ed019-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="ed019-113">Si un recurso está en mal estado, estado de los recursos analiza información adicional toodetermine Hola origen Hola problema.</span><span class="sxs-lookup"><span data-stu-id="ed019-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="ed019-114">También se identifican las acciones que Microsoft está llevando a cabo toofix problema de Hola o qué acciones puede llevar a cabo tooaddress Hola causa de problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed019-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="ed019-115">Comprueba la lista completa de Hola de revisión de los tipos de recursos y el estado de [estado de los recursos de Azure](resource-health-checks-resource-types.md) para obtener más detalles sobre cómo se evalúa el estado.</span><span class="sxs-lookup"><span data-stu-id="ed019-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="ed019-116">Estado de mantenimiento proporcionado por Resource Health</span><span class="sxs-lookup"><span data-stu-id="ed019-116">Health status provided by resource health</span></span>
<span data-ttu-id="ed019-117">estado de Hola de un recurso es uno de hello siguientes estados:</span><span class="sxs-lookup"><span data-stu-id="ed019-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="ed019-118">Disponible</span><span class="sxs-lookup"><span data-stu-id="ed019-118">Available</span></span>
<span data-ttu-id="ed019-119">servicio de Hello no ha detectado los eventos que tienen efecto sobre el estado de Hola de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed019-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="ed019-120">En casos donde los recursos de Hola se ha recuperado de tiempo de inactividad imprevisto durante Hola última Hola 24 horas aparecerá **se recuperó recientemente** notificación.</span><span class="sxs-lookup"><span data-stu-id="ed019-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![Máquina virtual disponible en Resource Health](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="ed019-122">No disponible</span><span class="sxs-lookup"><span data-stu-id="ed019-122">Unavailable</span></span>
<span data-ttu-id="ed019-123">Hola servicio ha detectado un evento de plataforma no afectar el estado de Hola de recurso de Hola o de plataforma en curso.</span><span class="sxs-lookup"><span data-stu-id="ed019-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="ed019-124">Eventos de plataforma</span><span class="sxs-lookup"><span data-stu-id="ed019-124">Platform events</span></span>
<span data-ttu-id="ed019-125">Estos eventos se desencadenan en varios componentes de infraestructura de Azure hello e incluyen tanto acciones programadas como mantenimiento planeado e incidentes inesperados como un reinicio del host no planeada.</span><span class="sxs-lookup"><span data-stu-id="ed019-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="ed019-126">Mantenimiento de recursos proporciona detalles adicionales sobre el evento de hello, proceso de recuperación de Hola y habilita la compatibilidad con de toocontact incluso si no tienes un Microsoft active contrato de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="ed019-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Máquina virtual recursos mantenimiento no está disponible debido a eventos tooplatform](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="ed019-128">Eventos no de plataforma</span><span class="sxs-lookup"><span data-stu-id="ed019-128">Non-Platform events</span></span>
<span data-ttu-id="ed019-129">Estos eventos se activan mediante acciones realizadas por los usuarios, por ejemplo, detener una máquina virtual o alcance Hola número máximo de conexiones tooa caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="ed019-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Máquina virtual recursos mantenimiento no está disponible debido a eventos de plataforma toonon](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="ed019-131">Desconocido</span><span class="sxs-lookup"><span data-stu-id="ed019-131">Unknown</span></span>
<span data-ttu-id="ed019-132">Este estado de mantenimiento indica que Resource Health no ha recibido información sobre este recurso durante más de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="ed019-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="ed019-133">Aunque este estado no es una indicación definitiva del estado de Hola de recursos de hello, es un punto de datos importantes en el proceso de solución de problemas de hello:</span><span class="sxs-lookup"><span data-stu-id="ed019-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="ed019-134">Si está ejecutando recursos hello como estado de hello esperado del recurso de hello actualizará tooAvailable después de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ed019-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="ed019-135">Si experimenta problemas con el recurso de hello, hello estado desconocido puede sugerir recursos Hola se ve afectado por un evento de plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed019-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![Máquina virtual Desconocida de Resource Health](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="ed019-137">Informe de un estado incorrecto</span><span class="sxs-lookup"><span data-stu-id="ed019-137">Report an incorrect status</span></span>
<span data-ttu-id="ed019-138">Si en cualquier momento considera estado actual de hello es incorrecta, puede hacernos saber haciendo clic en **informan del estado de mantenimiento incorrecto**.</span><span class="sxs-lookup"><span data-stu-id="ed019-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="ed019-139">En casos donde se ven afectados por un problema de Azure, le recomendamos que toocontact de soporte técnico de hoja de mantenimiento de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed019-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![Informe de estado incorrecto en Resource Health](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="ed019-141">Información histórica</span><span class="sxs-lookup"><span data-stu-id="ed019-141">Historical Information</span></span>
<span data-ttu-id="ed019-142">Puede tener acceso a los días de too14 de datos de historial de mantenimiento, haga clic en **ver el historial de** en la hoja de estado de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed019-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![Historial de informes en Resource Health](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="ed019-144">Introducción</span><span class="sxs-lookup"><span data-stu-id="ed019-144">Getting started</span></span>
<span data-ttu-id="ed019-145">tooopen estado de recursos para un recurso</span><span class="sxs-lookup"><span data-stu-id="ed019-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="ed019-146">Inicie sesión en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed019-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="ed019-147">Navegar tooyour recurso.</span><span class="sxs-lookup"><span data-stu-id="ed019-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="ed019-148">En el menú de recursos de hello ubicado en el lado izquierdo de hello, haga clic en **estado de los recursos**.</span><span class="sxs-lookup"><span data-stu-id="ed019-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![Apertura de Resource Health desde la hoja Recurso](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="ed019-150">También puede tener acceso a mantenimiento de recursos, haga clic en **más servicios**y escribiendo **estado de los recursos** Hola de tooopen de cuadro de texto de filtro **ayuda y soporte técnico** hoja.</span><span class="sxs-lookup"><span data-stu-id="ed019-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="ed019-151">Por último, haga clic en [**Resource Health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="ed019-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Apertura de Resource Health desde Más servicios](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="ed019-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed019-153">Next steps</span></span>

<span data-ttu-id="ed019-154">Consulte estos toolearn recursos más información acerca del estado de los recursos:</span><span class="sxs-lookup"><span data-stu-id="ed019-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="ed019-155">Tipos de recurso y comprobaciones de estado en Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="ed019-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="ed019-156">Preguntas más frecuentes de Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="ed019-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




