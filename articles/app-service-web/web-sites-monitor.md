---
title: aaaMonitor aplicaciones de servicio de aplicaciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor aplicaciones de servicio de aplicaciones de Azure mediante el uso de Hola Portal de Azure."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="0dd59-103">Supervisión de Aplicaciones en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0dd59-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="0dd59-104">[Servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714) proporciona funcionalidad de supervisión incorporada en hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0dd59-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="0dd59-105">Esto incluye Hola capacidad tooreview **cuotas** y **métricas** para una aplicación, así como Hola plan de servicio de aplicaciones, configurar **alertas** e incluso **deajustedeescala** automáticamente en función de estas métricas.</span><span class="sxs-lookup"><span data-stu-id="0dd59-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="0dd59-106">Descripción de cuotas y métricas</span><span class="sxs-lookup"><span data-stu-id="0dd59-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="0dd59-107">Cuotas</span><span class="sxs-lookup"><span data-stu-id="0dd59-107">Quotas</span></span>
<span data-ttu-id="0dd59-108">Las aplicaciones hospedadas en el servicio de aplicaciones son sujeto toocertain *límites* en los recursos que pueden utilizar.</span><span class="sxs-lookup"><span data-stu-id="0dd59-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="0dd59-109">Hello define los límites hello **plan de servicio de aplicaciones** asociado a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0dd59-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="0dd59-110">Si la aplicación hello se hospeda en un **libre** o **Shared** previsto, a continuación, define los límites de hello en recursos de hello puede utilizar la aplicación hello **cuotas**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="0dd59-111">Si la aplicación hello se hospeda en un **básica**, **estándar** o **Premium** previsto, a continuación, se establecen límites de hello en los recursos de hello pueden utilizar por hello **tamaño** (Pequeño, mediano y grande) y **el número de instancias** (1, 2, 3,...) de hello **plan de servicio de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="0dd59-112">Las **cuotas** de las aplicaciones **gratis** o **compartidas** son:</span><span class="sxs-lookup"><span data-stu-id="0dd59-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="0dd59-113">**CPU (Short)**</span><span class="sxs-lookup"><span data-stu-id="0dd59-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="0dd59-114">Cantidad de CPU permitida para esta aplicación en un intervalo de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="0dd59-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="0dd59-115">Esta cuota se vuelve a establecer cada cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="0dd59-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="0dd59-116">**CPU (Day)**</span><span class="sxs-lookup"><span data-stu-id="0dd59-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="0dd59-117">Cantidad total de CPU permitida para esta aplicación en un día.</span><span class="sxs-lookup"><span data-stu-id="0dd59-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="0dd59-118">Esta cuota se vuelve a establecer cada 24 horas a medianoche (UTC).</span><span class="sxs-lookup"><span data-stu-id="0dd59-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="0dd59-119">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="0dd59-119">**Memory**</span></span>
  * <span data-ttu-id="0dd59-120">Cantidad total de memoria permitida para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="0dd59-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="0dd59-121">**Ancho de banda**</span><span class="sxs-lookup"><span data-stu-id="0dd59-121">**Bandwidth**</span></span>
  * <span data-ttu-id="0dd59-122">Cantidad total de ancho de banda saliente permitido para esta aplicación en un día.</span><span class="sxs-lookup"><span data-stu-id="0dd59-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="0dd59-123">Esta cuota se vuelve a establecer cada 24 horas a medianoche (UTC).</span><span class="sxs-lookup"><span data-stu-id="0dd59-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="0dd59-124">**Sistema de archivos**</span><span class="sxs-lookup"><span data-stu-id="0dd59-124">**Filesystem**</span></span>
  * <span data-ttu-id="0dd59-125">Cantidad total de almacenamiento permitido.</span><span class="sxs-lookup"><span data-stu-id="0dd59-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="0dd59-126">Hola solo cuota aplicable tooapps hospedadas en **básica**, **estándar** y **Premium** planes es **Filesystem**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="0dd59-127">Obtener más información sobre cuotas específicas de hello, límites y características disponibles para Hola diferentes SKU de servicio de aplicación puede encontrarse aquí: [los límites de servicio de suscripción de Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="0dd59-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="0dd59-128">Aplicación de cuotas</span><span class="sxs-lookup"><span data-stu-id="0dd59-128">Quota Enforcement</span></span>
<span data-ttu-id="0dd59-129">Si una aplicación en su uso supera hello **CPU (corto)**, **CPU (día)**, o **ancho de banda** aplicación de cuota, a continuación, Hola se detendrá hasta que vuelve a establece la cuota de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dd59-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="0dd59-130">Durante este tiempo, todas las solicitudes entrantes provocarán un error **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="0dd59-131">Si Hola aplicación **memoria** se supera la cuota, a continuación, aplicación hello se reiniciará.</span><span class="sxs-lookup"><span data-stu-id="0dd59-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="0dd59-132">Si hello **Filesystem** se supera la cuota, a continuación, cualquier escritura que se producirá un error en la operación, se incluye la escritura toologs.</span><span class="sxs-lookup"><span data-stu-id="0dd59-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="0dd59-133">Las cuotas se pueden incrementar o quitar de la aplicación actualizando el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="0dd59-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="0dd59-134">Métricas</span><span class="sxs-lookup"><span data-stu-id="0dd59-134">Metrics</span></span>
<span data-ttu-id="0dd59-135">**Las métricas** proporcionan información sobre la aplicación hello y comportamiento del plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0dd59-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="0dd59-136">Para una **aplicación**, métricas de hello disponibles son:</span><span class="sxs-lookup"><span data-stu-id="0dd59-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="0dd59-137">**Tiempo de respuesta promedio**</span><span class="sxs-lookup"><span data-stu-id="0dd59-137">**Average Response Time**</span></span>
  * <span data-ttu-id="0dd59-138">tiempo promedio de Hello necesario para las solicitudes de hello aplicación tooserve en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="0dd59-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="0dd59-139">**Espacio de trabajo de memoria promedio**</span><span class="sxs-lookup"><span data-stu-id="0dd59-139">**Average memory working set**</span></span>
  * <span data-ttu-id="0dd59-140">promedio de Hola de memoria en MIB utilizados por la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0dd59-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="0dd59-141">**Tiempo de CPU**</span><span class="sxs-lookup"><span data-stu-id="0dd59-141">**CPU Time**</span></span>
  * <span data-ttu-id="0dd59-142">cantidad de Hola de CPU en segundos consumidos por la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0dd59-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="0dd59-143">Para más información acerca de esta métrica, consulte [Tiempo de CPU y porcentaje de CPU](#cpu-time-vs-cpu-percentage).</span><span class="sxs-lookup"><span data-stu-id="0dd59-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="0dd59-144">**Entrada de datos**</span><span class="sxs-lookup"><span data-stu-id="0dd59-144">**Data In**</span></span>
  * <span data-ttu-id="0dd59-145">cantidad de Hola de ancho de banda entrante consumida por la aplicación hello en MIB.</span><span class="sxs-lookup"><span data-stu-id="0dd59-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="0dd59-146">**Salida de datos**</span><span class="sxs-lookup"><span data-stu-id="0dd59-146">**Data Out**</span></span>
  * <span data-ttu-id="0dd59-147">cantidad de Hola de ancho de banda saliente utilizado por la aplicación hello en MIB.</span><span class="sxs-lookup"><span data-stu-id="0dd59-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="0dd59-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="0dd59-148">**Http 2xx**</span></span>
  * <span data-ttu-id="0dd59-149">Cantidad total de solicitudes que devuelven un código de estado HTTP superior a 200 e inferior a 300.</span><span class="sxs-lookup"><span data-stu-id="0dd59-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="0dd59-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="0dd59-150">**Http 3xx**</span></span>
  * <span data-ttu-id="0dd59-151">Cantidad total de solicitudes que devuelven un código de estado HTTP superior a 300 e inferior a 400.</span><span class="sxs-lookup"><span data-stu-id="0dd59-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="0dd59-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="0dd59-152">**Http 401**</span></span>
  * <span data-ttu-id="0dd59-153">Cantidad total de solicitudes que devuelven el código de estado HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="0dd59-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="0dd59-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="0dd59-154">**Http 403**</span></span>
  * <span data-ttu-id="0dd59-155">Cantidad total de solicitudes que devuelven el código de estado HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="0dd59-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="0dd59-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="0dd59-156">**Http 404**</span></span>
  * <span data-ttu-id="0dd59-157">Cantidad total de solicitudes que devuelven el código de estado HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="0dd59-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="0dd59-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="0dd59-158">**Http 406**</span></span>
  * <span data-ttu-id="0dd59-159">Cantidad total de solicitudes que devuelven el código de estado HTTP 406.</span><span class="sxs-lookup"><span data-stu-id="0dd59-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="0dd59-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="0dd59-160">**Http 4xx**</span></span>
  * <span data-ttu-id="0dd59-161">Cantidad total de solicitudes que devuelven un código de estado HTTP superior a 400 e inferior a 500.</span><span class="sxs-lookup"><span data-stu-id="0dd59-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="0dd59-162">**Errores de servidor HTTP**</span><span class="sxs-lookup"><span data-stu-id="0dd59-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="0dd59-163">Cantidad total de solicitudes que devuelven un código de estado HTTP superior a 500 e inferior a 600.</span><span class="sxs-lookup"><span data-stu-id="0dd59-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="0dd59-164">**Espacio de trabajo de memoria**</span><span class="sxs-lookup"><span data-stu-id="0dd59-164">**Memory working set**</span></span>
  * <span data-ttu-id="0dd59-165">Cantidad actual de memoria utilizada por la aplicación hello en MIB.</span><span class="sxs-lookup"><span data-stu-id="0dd59-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="0dd59-166">**Solicitudes**</span><span class="sxs-lookup"><span data-stu-id="0dd59-166">**Requests**</span></span>
  * <span data-ttu-id="0dd59-167">Número total de solicitudes, independientemente de su código de estado HTTP resultante.</span><span class="sxs-lookup"><span data-stu-id="0dd59-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="0dd59-168">Para una **plan de servicio de aplicaciones**, métricas de hello disponibles son:</span><span class="sxs-lookup"><span data-stu-id="0dd59-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="0dd59-169">Las métricas de plan de App Service solo están disponibles para planes de SKU **básico**, **estándar** o **premium**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="0dd59-170">**Porcentaje de CPU**</span><span class="sxs-lookup"><span data-stu-id="0dd59-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="0dd59-171">Hola promedio de CPU utilizado por todas las instancias del plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dd59-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="0dd59-172">**Porcentaje de memoria**</span><span class="sxs-lookup"><span data-stu-id="0dd59-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="0dd59-173">Hola promedio de memoria usado en todas las instancias del plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dd59-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="0dd59-174">**Entrada de datos**</span><span class="sxs-lookup"><span data-stu-id="0dd59-174">**Data In**</span></span>
  * <span data-ttu-id="0dd59-175">Hola promedio entrantes ancho de banda utilizado por todas las instancias del plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dd59-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="0dd59-176">**Salida de datos**</span><span class="sxs-lookup"><span data-stu-id="0dd59-176">**Data Out**</span></span>
  * <span data-ttu-id="0dd59-177">promedio de Hello ancho de banda utilizado por todas las instancias del plan de Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="0dd59-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="0dd59-178">**Longitud de la cola de disco**</span><span class="sxs-lookup"><span data-stu-id="0dd59-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="0dd59-179">promedio de Hola de tanto lectura y escritura de las solicitudes que se pusieron en cola en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0dd59-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="0dd59-180">Una longitud de cola de disco alta es una indicación de una aplicación que se podría ralentizar debido tooexcessive de E/S de disco.</span><span class="sxs-lookup"><span data-stu-id="0dd59-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="0dd59-181">**Longitud de la cola HTTP**</span><span class="sxs-lookup"><span data-stu-id="0dd59-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="0dd59-182">promedio de Hola de solicitudes HTTP que tenía toosit en cola Hola antes de que se cumplen.</span><span class="sxs-lookup"><span data-stu-id="0dd59-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="0dd59-183">Una longitud de la cola HTTP elevada o creciente indica que un plan está sobrecargado.</span><span class="sxs-lookup"><span data-stu-id="0dd59-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="0dd59-184">Tiempo de CPU y porcentaje de CPU</span><span class="sxs-lookup"><span data-stu-id="0dd59-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="0dd59-185">Hay 2 métricas que reflejan el uso de CPU.</span><span class="sxs-lookup"><span data-stu-id="0dd59-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="0dd59-186">**Tiempo de CPU** y **Porcentaje de CPU**</span><span class="sxs-lookup"><span data-stu-id="0dd59-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="0dd59-187">**Tiempo de CPU** es útil para las aplicaciones hospedadas en **libre** o **Shared** planes como uno de sus cuotas se define en minutos de CPU utilizados por la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0dd59-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="0dd59-188">**Porcentaje de CPU** en hello otro lado es útil para las aplicaciones hospedadas en **básica**, **estándar** y **premium** planes desde que se pueden escalar horizontalmente y esta métrica es una buena indicación de hello el uso general en todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="0dd59-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="0dd59-189">Directiva de retención y granularidad de métricas</span><span class="sxs-lookup"><span data-stu-id="0dd59-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="0dd59-190">Las métricas para un plan de servicio de aplicación y la aplicación se registran y agregadas por el servicio de hello con hello siguientes granularidades y las directivas de retención:</span><span class="sxs-lookup"><span data-stu-id="0dd59-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="0dd59-191">Las métricas de granularidad de **minuto** se conservan durante **48 horas**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="0dd59-192">Las métricas de granularidad de **hora** se conservan durante **30 días**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="0dd59-193">Las métricas de granularidad de **día** se conservan durante **90 días**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="0dd59-194">Supervisión de las cuotas y las métricas en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0dd59-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="0dd59-195">Puede revisar el estado de Hola de hello diferentes **cuotas** y **métricas** que afectan a una aplicación Hola [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0dd59-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="0dd59-196">![][quotas]
Las **cuotas** se encuentran en Configuración &gt;**Cuotas**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="0dd59-197">Hola UX permite revisar: nombre de las cuotas de hello (1), (2) su intervalo de restablecimiento, (3) el límite actual y el valor (4) actual.</span><span class="sxs-lookup"><span data-stu-id="0dd59-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="0dd59-198">![][metrics]
**Las métricas** es posible acceder a directamente desde la hoja de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dd59-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="0dd59-199">También puede personalizar el gráfico de Hola por: (1) **haga clic en** en la base de datos y seleccione (2) **Editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="0dd59-200">Desde aquí puede cambiar hello (3) **el intervalo de tiempo**, (4) **tipo de gráfico**y (5) **métricas** toodisplay.</span><span class="sxs-lookup"><span data-stu-id="0dd59-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="0dd59-201">Para más información acerca de las métricas, consulte [Supervisión de las métricas del servicio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="0dd59-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="0dd59-202">Alertas y autoescala</span><span class="sxs-lookup"><span data-stu-id="0dd59-202">Alerts and Autoscale</span></span>
<span data-ttu-id="0dd59-203">Las métricas para un plan de aplicación o servicio de aplicaciones puede enlazarse tooalerts, toolearn más detalles al respecto, consulte [recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="0dd59-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="0dd59-204">Las aplicaciones de App Service hospedadas en planes de App Service básicos, estándar o premium admiten la **autoescala**.</span><span class="sxs-lookup"><span data-stu-id="0dd59-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="0dd59-205">Esto permite tooconfigure reglas que supervisan las métricas del plan de servicio de aplicaciones y pueden aumentar o reducir el número de instancias de hello proporciona recursos adicionales según sea necesario o guardando dinero cuando aplicación hello es aprovisionar excesivo.</span><span class="sxs-lookup"><span data-stu-id="0dd59-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="0dd59-206">Puede aprender más acerca de la escala automática aquí: [cómo tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) y aquí [las prácticas recomendadas para el ajuste automático del Monitor de Azure](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="0dd59-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="0dd59-207">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0dd59-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0dd59-208">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="0dd59-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="0dd59-209">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="0dd59-209">What's changed</span></span>
* <span data-ttu-id="0dd59-210">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="0dd59-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
