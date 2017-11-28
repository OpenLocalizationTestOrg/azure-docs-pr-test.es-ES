---
title: "aaaAzure modelos de datos de telemetría de visión de aplicación, contexto de telemetría | Documentos de Microsoft"
description: "Modelo de datos de contexto de telemetría de Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="4b90a-103">Contexto de telemetría: modelo de datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="4b90a-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="4b90a-104">Cada elemento de telemetría puede tener campos de contexto fuertemente tipados.</span><span class="sxs-lookup"><span data-stu-id="4b90a-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="4b90a-105">Cada campo permite un escenario de supervisión específico.</span><span class="sxs-lookup"><span data-stu-id="4b90a-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="4b90a-106">Utilice Hola propiedades personalizadas colección toostore personalizados o específicos de la aplicación información contextual.</span><span class="sxs-lookup"><span data-stu-id="4b90a-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="4b90a-107">Versión de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4b90a-107">Application version</span></span>

<span data-ttu-id="4b90a-108">La información en los campos de contexto de aplicación Hola está siempre acerca de la aplicación hello que está enviando la telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b90a-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="4b90a-109">Versión de la aplicación es usado tooanalyze tendencia cambios de comportamiento de la aplicación hello y sus implementaciones de toohello de correlación.</span><span class="sxs-lookup"><span data-stu-id="4b90a-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="4b90a-110">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="4b90a-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="4b90a-111">Dirección IP de cliente</span><span class="sxs-lookup"><span data-stu-id="4b90a-111">Client IP address</span></span>

<span data-ttu-id="4b90a-112">dirección IP de Hello hello de dispositivo de cliente.</span><span class="sxs-lookup"><span data-stu-id="4b90a-112">hello IP address of hello client device.</span></span> <span data-ttu-id="4b90a-113">Se admiten IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="4b90a-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="4b90a-114">Cuando telemetría se envía desde un servicio, contexto de ubicación de hello es acerca del usuario de Hola que inició la operación de hello en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b90a-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="4b90a-115">Application Insights extraen información de ubicación geográfica de Hola de dirección IP del cliente de hello y, a continuación, truncan.</span><span class="sxs-lookup"><span data-stu-id="4b90a-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="4b90a-116">La IP del cliente no puede usarse por sí misma a modo de información de identificación del usuario final.</span><span class="sxs-lookup"><span data-stu-id="4b90a-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="4b90a-117">Longitud máxima: 46</span><span class="sxs-lookup"><span data-stu-id="4b90a-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="4b90a-118">Tipo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="4b90a-118">Device type</span></span>

<span data-ttu-id="4b90a-119">Este campo se utilizaba originalmente tooindicate Hola tipo de dispositivo de usuario final Hola Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4b90a-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="4b90a-120">Hoy en día utiliza principalmente toodistinguish JavaScript telemetría con hello tipo de dispositivo 'Browser' de telemetría de servidor con el tipo de dispositivo de hello 'Equipo'.</span><span class="sxs-lookup"><span data-stu-id="4b90a-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="4b90a-121">Longitud máxima: 64</span><span class="sxs-lookup"><span data-stu-id="4b90a-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="4b90a-122">Identificador de operación</span><span class="sxs-lookup"><span data-stu-id="4b90a-122">Operation id</span></span>

<span data-ttu-id="4b90a-123">Un identificador único de la operación de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b90a-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="4b90a-124">Este identificador permite toogroup telemetría a través de varios componentes.</span><span class="sxs-lookup"><span data-stu-id="4b90a-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="4b90a-125">Consulte [Correlación de telemetría](application-insights-correlation.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4b90a-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="4b90a-126">Id. de operación de Hola se crea mediante una solicitud o una vista de página.</span><span class="sxs-lookup"><span data-stu-id="4b90a-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="4b90a-127">Todos los demás telemetría establece este valor de toohello de campo de Hola que contiene la vista de página o de solicitud.</span><span class="sxs-lookup"><span data-stu-id="4b90a-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="4b90a-128">Longitud máxima: 128</span><span class="sxs-lookup"><span data-stu-id="4b90a-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="4b90a-129">Identificador de la operación principal</span><span class="sxs-lookup"><span data-stu-id="4b90a-129">Parent operation ID</span></span>

<span data-ttu-id="4b90a-130">Identificador único del primario inmediato del elemento de hello telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b90a-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="4b90a-131">Consulte [Correlación de telemetría](application-insights-correlation.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4b90a-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="4b90a-132">Longitud máxima: 128</span><span class="sxs-lookup"><span data-stu-id="4b90a-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="4b90a-133">Nombre de la operación</span><span class="sxs-lookup"><span data-stu-id="4b90a-133">Operation name</span></span>

<span data-ttu-id="4b90a-134">nombre de Hello (grupo) de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b90a-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="4b90a-135">nombre de la operación de Hola se crea mediante una solicitud o una vista de página.</span><span class="sxs-lookup"><span data-stu-id="4b90a-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="4b90a-136">Todos los demás elementos de telemetría establecer este valor de toohello de campo para hello que contiene la vista de página o de solicitud.</span><span class="sxs-lookup"><span data-stu-id="4b90a-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="4b90a-137">Nombre de la operación se utiliza para buscar todos los elementos de telemetría de Hola para un grupo de operaciones (por ejemplo ' GET Home/Index').</span><span class="sxs-lookup"><span data-stu-id="4b90a-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="4b90a-138">Esta propiedad de contexto es usado tooanswer preguntas como "¿Cuáles son Hola típico excepciones de esta página."</span><span class="sxs-lookup"><span data-stu-id="4b90a-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="4b90a-139">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="4b90a-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="4b90a-140">Origen sintético de operación de Hola</span><span class="sxs-lookup"><span data-stu-id="4b90a-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="4b90a-141">Nombre del origen sintético.</span><span class="sxs-lookup"><span data-stu-id="4b90a-141">Name of synthetic source.</span></span> <span data-ttu-id="4b90a-142">Algunos telemetría de aplicación hello puede representar tráfico sintético.</span><span class="sxs-lookup"><span data-stu-id="4b90a-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="4b90a-143">Puede ser web rastreador (crawler) indización Hola de sitio web, pruebas de disponibilidad de sitio o seguimientos de bibliotecas de diagnóstico como Application Insights SDK propio.</span><span class="sxs-lookup"><span data-stu-id="4b90a-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="4b90a-144">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="4b90a-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="4b90a-145">Identificador de la sesión</span><span class="sxs-lookup"><span data-stu-id="4b90a-145">Session id</span></span>

<span data-ttu-id="4b90a-146">Id. de sesión - instancia Hola Hola de interacción del usuario con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4b90a-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="4b90a-147">Información de los campos de contexto de sesión de hello siempre es acerca del usuario final de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b90a-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="4b90a-148">Cuando telemetría se envía desde un servicio, contexto de la sesión de hello es acerca del usuario de Hola que inició la operación de hello en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b90a-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="4b90a-149">Longitud máxima: 64</span><span class="sxs-lookup"><span data-stu-id="4b90a-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="4b90a-150">Identificador del usuario anónimo</span><span class="sxs-lookup"><span data-stu-id="4b90a-150">Anonymous user id</span></span>

<span data-ttu-id="4b90a-151">Este es el identificador del usuario anónimo. Representa el usuario final de saludo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4b90a-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="4b90a-152">Cuando se envía la telemetría de un servicio, contexto de usuario de hello es acerca del usuario de Hola que inició la operación de hello en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b90a-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="4b90a-153">[Muestreo](app-insights-sampling.md) es una cantidad de hello técnicas toominimize Hola de telemetría recopilado.</span><span class="sxs-lookup"><span data-stu-id="4b90a-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="4b90a-154">Tooeither de intentos de algoritmo de muestreo ejemplo o alejar Hola todos los ponen en correlación telemetría.</span><span class="sxs-lookup"><span data-stu-id="4b90a-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="4b90a-155">El identificador del usuario anónimo se usa para muestrear la generación de puntuaciones.</span><span class="sxs-lookup"><span data-stu-id="4b90a-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="4b90a-156">Por ello, el identificador del usuario anónimo debería ser un valor suficiente aleatorio.</span><span class="sxs-lookup"><span data-stu-id="4b90a-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="4b90a-157">Con nombre de usuario de toostore de Id. de usuario anónimo es un uso inapropiado del campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b90a-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="4b90a-158">Use el identificador del usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="4b90a-158">Use Authenticated user id.</span></span>

<span data-ttu-id="4b90a-159">Longitud máxima: 128</span><span class="sxs-lookup"><span data-stu-id="4b90a-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="4b90a-160">Identificador del usuario autenticado</span><span class="sxs-lookup"><span data-stu-id="4b90a-160">Authenticated user id</span></span>

<span data-ttu-id="4b90a-161">Id. de usuario autenticado. Hola opuesto del identificador de usuario anónimo, este campo representa el usuario Hola con un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="4b90a-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="4b90a-162">Puesto que se trata de información de identificación personal, la mayoría de SDK no la recopilan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4b90a-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="4b90a-163">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="4b90a-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="4b90a-164">Identificador de la cuenta</span><span class="sxs-lookup"><span data-stu-id="4b90a-164">Account id</span></span>

<span data-ttu-id="4b90a-165">En aplicaciones de varios inquilinos es Id. de cuenta de Hola o nombre, qué usuario Hola está actuando con.</span><span class="sxs-lookup"><span data-stu-id="4b90a-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="4b90a-166">Algunos ejemplos son el identificador de la suscripción de Azure Portal o el nombre del blog de la plataforma de creación de blogs.</span><span class="sxs-lookup"><span data-stu-id="4b90a-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="4b90a-167">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="4b90a-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="4b90a-168">Rol en la nube</span><span class="sxs-lookup"><span data-stu-id="4b90a-168">Cloud role</span></span>

<span data-ttu-id="4b90a-169">Nombre de aplicación Hola de hello rol es una parte de.</span><span class="sxs-lookup"><span data-stu-id="4b90a-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="4b90a-170">Se asigna directamente toohello nombre del rol en azure.</span><span class="sxs-lookup"><span data-stu-id="4b90a-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="4b90a-171">También puede ser usado toodistinguish micro servicios, que son parte de una sola aplicación.</span><span class="sxs-lookup"><span data-stu-id="4b90a-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="4b90a-172">Longitud máxima: 256</span><span class="sxs-lookup"><span data-stu-id="4b90a-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="4b90a-173">Instancia de rol en la nube</span><span class="sxs-lookup"><span data-stu-id="4b90a-173">Cloud role instance</span></span>

<span data-ttu-id="4b90a-174">Nombre de instancia de Hola donde se ejecuta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4b90a-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="4b90a-175">El nombre de equipo del nombre de instancia local para Azure.</span><span class="sxs-lookup"><span data-stu-id="4b90a-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="4b90a-176">Longitud máxima: 256</span><span class="sxs-lookup"><span data-stu-id="4b90a-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="4b90a-177">Interno: versión del SDK</span><span class="sxs-lookup"><span data-stu-id="4b90a-177">Internal: SDK version</span></span>

<span data-ttu-id="4b90a-178">Esta es la versión del SDK.</span><span class="sxs-lookup"><span data-stu-id="4b90a-178">SDK version.</span></span> <span data-ttu-id="4b90a-179">Consulte https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification para obtener información.</span><span class="sxs-lookup"><span data-stu-id="4b90a-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="4b90a-180">Longitud máxima: 64</span><span class="sxs-lookup"><span data-stu-id="4b90a-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="4b90a-181">Interno: nombre del nodo</span><span class="sxs-lookup"><span data-stu-id="4b90a-181">Internal: Node name</span></span>

<span data-ttu-id="4b90a-182">Este campo representa el nombre de nodo Hola usado para la facturación.</span><span class="sxs-lookup"><span data-stu-id="4b90a-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="4b90a-183">Usar detección estándar de hello toooverride de nodos.</span><span class="sxs-lookup"><span data-stu-id="4b90a-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="4b90a-184">Longitud máxima: 256</span><span class="sxs-lookup"><span data-stu-id="4b90a-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="4b90a-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b90a-185">Next steps</span></span>

- <span data-ttu-id="4b90a-186">Obtenga información acerca de cómo demasiado[ampliar y filtrar telemetría](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="4b90a-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="4b90a-187">Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4b90a-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="4b90a-188">Compruebe la [configuración](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) de la recopilación de propiedades estándar de contexto.</span><span class="sxs-lookup"><span data-stu-id="4b90a-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
