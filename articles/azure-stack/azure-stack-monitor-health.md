---
title: aaaMonitor de estado y alertas en la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor mantenimiento y alertas en la pila de Azure."
services: azure-stack
documentationcenter: 
author: chasat-MS
manager: dsavage
editor: 
ms.assetid: 69901c7b-4673-4bd8-acf2-8c6bdd9d1546
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: chasat
ms.openlocfilehash: 11e287c497e154b767c775fe4afcc78ec9e72fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a><span data-ttu-id="6b486-103">Supervisar el estado y las alertas en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6b486-103">Monitor health and alerts in Azure Stack</span></span>

<span data-ttu-id="6b486-104">Pila de Azure incluye infraestructura de supervisión de funciones que permiten a un estado de tooview de operador en la nube y las alertas de una región de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b486-104">Azure Stack includes infrastructure monitoring capabilities that enable a cloud operator tooview health and alerts for an Azure Stack region.</span></span>

<span data-ttu-id="6b486-105">Pila de Azure tiene un conjunto de capacidades de administración de región disponibles en hello **administración región** icono.</span><span class="sxs-lookup"><span data-stu-id="6b486-105">Azure Stack has a set of region management capabilities available in hello **Region management** tile.</span></span> <span data-ttu-id="6b486-106">Este icono, anclado de forma predeterminada en el portal de administración de Hola para hello suscripción a proveedor de forma predeterminada, enumera todas las regiones de hello implementado de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b486-106">This tile, pinned by default in hello administrator portal for hello Default Provider Subscription, lists all hello deployed regions of Azure Stack.</span></span> <span data-ttu-id="6b486-107">También se muestra el recuento de Hola de alertas activas de críticas y de advertencia para cada región.</span><span class="sxs-lookup"><span data-stu-id="6b486-107">It also shows hello count of active critical and warning alerts for each region.</span></span> <span data-ttu-id="6b486-108">Este icono es el punto de entrada de estado de Hola y alerta de funcionalidad de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b486-108">This tile is your entry point into hello health and alert functionality of Azure Stack.</span></span>

 ![icono de administración de la región de Hola](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a><span data-ttu-id="6b486-110">Comprender el estado en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6b486-110">Understand health in Azure Stack</span></span>

 <span data-ttu-id="6b486-111">Mantenimiento y alertas se administran en la pila de Azure por el proveedor de recursos de mantenimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b486-111">Health and alerts are managed in Azure Stack by hello Health resource provider.</span></span> <span data-ttu-id="6b486-112">Componentes de la infraestructura de pila Azure registran con el proveedor de recursos de mantenimiento de Hola durante la configuración e implementación de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b486-112">Azure Stack infrastructure components register with hello Health resource provider during Azure Stack deployment and configuration.</span></span> <span data-ttu-id="6b486-113">Este registro permite mostrar hello de estado y alertas para cada componente.</span><span class="sxs-lookup"><span data-stu-id="6b486-113">This registration enables hello display of health and alerts for each component.</span></span> <span data-ttu-id="6b486-114">El estado en Azure Stack es un concepto simple.</span><span class="sxs-lookup"><span data-stu-id="6b486-114">Health in Azure Stack is a simple concept.</span></span> <span data-ttu-id="6b486-115">Si Hola de alertas para una instancia registrada condiciones de un componente, el estado de dicho componente refleja Hola peor active gravedad de alerta; advertencia o crítico.</span><span class="sxs-lookup"><span data-stu-id="6b486-115">If alerts for a registered instance of a component exist, hello health state of that component reflects hello worst active alert severity; warning, or critical.</span></span>
 
 ## <a name="view-and-manage-component-health-state"></a><span data-ttu-id="6b486-116">Ver y administrar el estado de mantenimiento de un componente</span><span class="sxs-lookup"><span data-stu-id="6b486-116">View and manage component health state</span></span>
 
 <span data-ttu-id="6b486-117">Puede ver el estado de mantenimiento de Hola de componentes en ambos portal del Administrador de pila de Azure de Hola y a través de la API de Rest y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b486-117">You can view hello health state of components in both hello Azure Stack administrator portal and through Rest API and PowerShell.</span></span>
 
<span data-ttu-id="6b486-118">estado de mantenimiento de tooview hello en el portal de hello, haga clic en que desea tooview Hola de región de hello **administración región** icono.</span><span class="sxs-lookup"><span data-stu-id="6b486-118">tooview hello health state in hello portal, click hello region that you want tooview in hello **Region management** tile.</span></span> <span data-ttu-id="6b486-119">Puede ver el estado de mantenimiento de Hola de roles de infraestructura y de proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="6b486-119">You can view hello health state of infrastructure roles and of resource providers.</span></span> <span data-ttu-id="6b486-120">Tenga en cuenta que en esta versión, proveedor de recursos de proceso de hello no notifica el estado.</span><span class="sxs-lookup"><span data-stu-id="6b486-120">Note that in this release, hello Compute resource provider does not report health state.</span></span>

![Lista de roles de infraestructura](media/azure-stack-monitor-health/image2.png)

<span data-ttu-id="6b486-122">Puede hacer clic en un tooview de rol de infraestructura o el proveedor de recursos información más detallada.</span><span class="sxs-lookup"><span data-stu-id="6b486-122">You can click a resource provider or infrastructure role tooview more detailed information.</span></span>

> [!WARNING]
><span data-ttu-id="6b486-123">Si hace clic en un rol de infraestructura y, a continuación, haga clic en la instancia de rol de hello, hay opciones en hello **instancia de rol** tooStart hoja, reinicio o apagado.</span><span class="sxs-lookup"><span data-stu-id="6b486-123">If you click an infrastructure role, and then click hello role instance, there are options in hello **Role instance** blade tooStart, Restart, or Shutdown.</span></span> <span data-ttu-id="6b486-124">**No** utilice estas opciones en un entorno de Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="6b486-124">Do **not** use these options in an Azure Stack Development Kit environment.</span></span> <span data-ttu-id="6b486-125">Estas opciones están diseñadas únicamente para un entorno de varios nodos, donde hay más de una instancia de rol por rol de infraestructura.</span><span class="sxs-lookup"><span data-stu-id="6b486-125">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="6b486-126">Al reiniciar una instancia de rol (especialmente AzS-Xrp01) en el kit de desarrollo de hello provoca inestabilidad del sistema.</span><span class="sxs-lookup"><span data-stu-id="6b486-126">Restarting a role instance (especially AzS-Xrp01) in hello development kit causes system instability.</span></span> <span data-ttu-id="6b486-127">Solución de problemas, publique su problema toohello [foro de Azure pila](https://aka.ms/azurestackforum).</span><span class="sxs-lookup"><span data-stu-id="6b486-127">For troubleshooting assistance, please post your issue toohello [Azure Stack forum](https://aka.ms/azurestackforum).</span></span>
>
 
## <a name="view-alerts"></a><span data-ttu-id="6b486-128">Visualización de alertas</span><span class="sxs-lookup"><span data-stu-id="6b486-128">View alerts</span></span>

<span data-ttu-id="6b486-129">lista de Hola de alertas activas para cada región de la pila de Azure está disponible directamente desde hello **administración región** hoja.</span><span class="sxs-lookup"><span data-stu-id="6b486-129">hello list of active alerts for each Azure Stack region is available directly from hello **Region management** blade.</span></span> <span data-ttu-id="6b486-130">primer mosaico en la configuración predeterminada de hello Hello es hello **alertas** aparezca como mosaico que muestra un resumen de hello crítico y alertas de advertencia para la región de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b486-130">hello first tile in hello default configuration is hello **Alerts** tile, which displays a summary of hello critical and warning alerts for hello region.</span></span> <span data-ttu-id="6b486-131">Puede anclar el icono de alertas de hello, al igual que cualquier otro icono en esta hoja, panel de toohello para un acceso rápido.</span><span class="sxs-lookup"><span data-stu-id="6b486-131">You can pin hello Alerts tile, like any other tile on this blade, toohello dashboard for quick access.</span></span>   

![Ventana Alerts que muestra una advertencia](media/azure-stack-monitor-health/image3.png)

<span data-ttu-id="6b486-133">Mediante la selección en la parte superior del programa Hola Hola **alertas** icono, navegue toohello lista de todas las alertas activas para la región de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b486-133">By selecting hello top portion of hello **Alerts** tile, you navigate toohello list of all active alerts for hello region.</span></span> <span data-ttu-id="6b486-134">Si selecciona cualquier hello **crítico** o **advertencia** artículo de línea en el icono de hello, navegar tooa filtrada la lista de alertas (crítico o advertencia).</span><span class="sxs-lookup"><span data-stu-id="6b486-134">If you select either hello **Critical** or **Warning** line item within hello tile, you navigate tooa filtered list of alerts (Critical or Warning).</span></span> 

![Alertas de advertencia filtradas](media/azure-stack-monitor-health/image4.png)
  
<span data-ttu-id="6b486-136">Hola **alertas** hoja admite Hola capacidad toofilter tanto en gravedad (crítico o advertencia) y el estado (activa o cerrada).</span><span class="sxs-lookup"><span data-stu-id="6b486-136">hello **Alerts** blade supports hello ability toofilter both on status (Active or Closed) and severity (Critical or Warning).</span></span> <span data-ttu-id="6b486-137">vista predeterminada de Hello muestra todas las alertas activas.</span><span class="sxs-lookup"><span data-stu-id="6b486-137">hello default view displays all Active alerts.</span></span> <span data-ttu-id="6b486-138">Todas las alertas cerradas se quitan del sistema de hello después de siete días.</span><span class="sxs-lookup"><span data-stu-id="6b486-138">All closed alerts are removed from hello system after seven days.</span></span>

![Toofilter del panel de filtro por estado crítico o de advertencia](media/azure-stack-monitor-health/image5.png)

<span data-ttu-id="6b486-140">hoja de alertas de Hello también expone hello **API de vista** acción, ver qué hello muestra API de Rest que era usado toogenerate Hola lista.</span><span class="sxs-lookup"><span data-stu-id="6b486-140">hello Alerts blade also exposes hello **View API** action, which displays hello Rest API that was used toogenerate hello list view.</span></span> <span data-ttu-id="6b486-141">Esta acción proporciona un familiarizado con la sintaxis de la API de Rest de Hola que puede usar las alertas de tooquery toobecome de forma rápida.</span><span class="sxs-lookup"><span data-stu-id="6b486-141">This action provides a quick way toobecome familiar with hello Rest API syntax that you can use tooquery alerts.</span></span> <span data-ttu-id="6b486-142">Puede utilizar esta API para automatización o para integración con las soluciones existentes de supervisión, informe y vales del centro de datos.</span><span class="sxs-lookup"><span data-stu-id="6b486-142">You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions.</span></span> 

![Hola opción de API de vista que muestra hello API de Rest](media/azure-stack-monitor-health/image6.png)

<span data-ttu-id="6b486-144">Desde la hoja de alertas de hello, puede seleccionar una alerta toonavigate toohello **detalles de alerta** hoja.</span><span class="sxs-lookup"><span data-stu-id="6b486-144">From hello Alerts blade, you can select an alert toonavigate toohello **Alert details** blade.</span></span> <span data-ttu-id="6b486-145">Esta hoja muestra todos los campos que están asociados a la alerta de Hola y permite una navegación rápida toohello afectadas componente y origen de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b486-145">This blade displays all fields that are associated with hello alert, and enables quick navigation toohello affected component and source of hello alert.</span></span> <span data-ttu-id="6b486-146">Por ejemplo, hello alerta siguiente se produce si una de las instancias de rol de infraestructura de Hola se queda sin conexión o no está accesible.</span><span class="sxs-lookup"><span data-stu-id="6b486-146">For example, hello following alert occurs if one of hello infrastructure role instances goes offline or is not accessible.</span></span>  

![hoja de detalles de la alerta de Hola](media/azure-stack-monitor-health/image7.png)

<span data-ttu-id="6b486-148">Después de instancia de rol de infraestructura de hello es nuevo en línea, esta alerta se cierra automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6b486-148">After hello infrastructure role instance is back online, this alert automatically closes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b486-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6b486-149">Next steps</span></span>

[<span data-ttu-id="6b486-150">Administrar las actualizaciones en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6b486-150">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)

[<span data-ttu-id="6b486-151">Administración de regiones en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6b486-151">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
