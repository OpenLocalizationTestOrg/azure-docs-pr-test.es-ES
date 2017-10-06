---
title: aaaGet a trabajar con soluciones preconfiguradas | Documentos de Microsoft
description: "Siga este tutorial toolearn cómo toodeploy un conjunto de IoT de Azure configurado previamente la solución."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="d8df8-103">Empezar a trabajar con soluciones de hello preconfigurado</span><span class="sxs-lookup"><span data-stu-id="d8df8-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="d8df8-104">Conjunto de Azure IoT [soluciones preconfiguradas] [ lnk-preconfigured-solutions] combinar varias IoT de Azure servicios toodeliver-to-end soluciones que implementan escenarios empresariales IoT.</span><span class="sxs-lookup"><span data-stu-id="d8df8-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="d8df8-105">Hola *supervisión remota* solución preconfigurada conecta tooand supervisa los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="d8df8-106">Puede utilizar Hola solución tooanalyze Hola flujo de datos de los dispositivos y los resultados del negocio tooimprove realizando procesos responder automáticamente toothat flujo de datos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="d8df8-107">Este tutorial muestra cómo la supervisión remota de tooprovision Hola había preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="d8df8-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="d8df8-108">También le guía a través de características básicas de Hola de solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="d8df8-109">Puede tener acceso a muchas de estas características de solución de hello *panel* que implementa como parte de la solución de hello preconfigurado:</span><span class="sxs-lookup"><span data-stu-id="d8df8-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Panel de la solución preconfigurada de supervisión remota][img-dashboard]

<span data-ttu-id="d8df8-111">toocomplete este tutorial, necesita una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8df8-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d8df8-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d8df8-113">Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="d8df8-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="d8df8-114">Información general de escenario</span><span class="sxs-lookup"><span data-stu-id="d8df8-114">Scenario overview</span></span>

<span data-ttu-id="d8df8-115">Al implementar Hola solución preconfigurada de supervisión remoto, se rellena previamente con recursos que permiten toostep a través de un escenario común de supervisión remoto.</span><span class="sxs-lookup"><span data-stu-id="d8df8-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="d8df8-116">En este escenario, varios dispositivos conectados toohello solución dependen de los valores de temperatura inesperado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="d8df8-117">Hello las secciones siguientes muestran cómo para:</span><span class="sxs-lookup"><span data-stu-id="d8df8-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="d8df8-118">Identificar los dispositivos de hello enviar valores de temperatura inesperado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="d8df8-119">Configurar estos dispositivos toosend más detallados telemetría.</span><span class="sxs-lookup"><span data-stu-id="d8df8-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="d8df8-120">Corregir el problema de hello mediante la actualización de firmware de hello en estos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="d8df8-121">Compruebe que la acción ha resuelto el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="d8df8-122">Una característica clave de este escenario es que puede realizar todas estas acciones de forma remota desde el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="d8df8-123">No es necesario dispositivos toohello de acceso físico.</span><span class="sxs-lookup"><span data-stu-id="d8df8-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="d8df8-124">Panel de vista Hola solución</span><span class="sxs-lookup"><span data-stu-id="d8df8-124">View hello solution dashboard</span></span>

<span data-ttu-id="d8df8-125">panel de la solución de Hello permite toomanage solución de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="d8df8-126">Por ejemplo, puede ver la telemetría, agregar dispositivos y configurar las reglas.</span><span class="sxs-lookup"><span data-stu-id="d8df8-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="d8df8-127">Cuando el aprovisionamiento de hello está completado e indica el icono de Hola para su solución preconfigurada **listo**, elija **iniciar** tooopen su portal de solución de supervisión remoto en una nueva pestaña.</span><span class="sxs-lookup"><span data-stu-id="d8df8-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Iniciar solución de hello preconfigurado][img-launch-solution]

1. <span data-ttu-id="d8df8-129">De forma predeterminada, el portal de solución de hello muestra hello *panel*.</span><span class="sxs-lookup"><span data-stu-id="d8df8-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="d8df8-130">Puede navegar por las áreas de tooother del portal de solución de hello con menú de hello en el lado izquierdo de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Panel de la solución preconfigurada de supervisión remota][img-menu]

<span data-ttu-id="d8df8-132">panel de Hello muestra hello siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d8df8-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="d8df8-133">Un mapa que muestra la ubicación de Hola de cada dispositivo conectado toohello solución.</span><span class="sxs-lookup"><span data-stu-id="d8df8-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="d8df8-134">Cuando ejecuta por primera vez solución hello, hay 25 dispositivos simulados.</span><span class="sxs-lookup"><span data-stu-id="d8df8-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="d8df8-135">dispositivos simulados Hello se implementan una como trabajos Web de Azure y solución de hello usa información de tooplot de API de Bing Maps de hello en el mapa de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="d8df8-136">Vea hello [preguntas más frecuentes sobre] [ lnk-faq] toolearn cómo toomake Hola dinámicos de mapa.</span><span class="sxs-lookup"><span data-stu-id="d8df8-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="d8df8-137">Un panel **Historial de telemetría** que traza los datos de telemetría de temperatura y humedad de un dispositivo seleccionado prácticamente en tiempo real y muestra los datos agregados, como la humedad máxima, mínima y media.</span><span class="sxs-lookup"><span data-stu-id="d8df8-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="d8df8-138">Un panel **Historial de alarmas** que muestra los últimos eventos de alarma cuando un valor de telemetría ha superado un umbral.</span><span class="sxs-lookup"><span data-stu-id="d8df8-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="d8df8-139">Puede definir sus propios alarmas en ejemplos de adición toohello creados por la solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="d8df8-140">Un panel **Trabajos** que muestra información acerca de los trabajos programados.</span><span class="sxs-lookup"><span data-stu-id="d8df8-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="d8df8-141">En la página **Trabajos de administración** puede programar sus propios trabajos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="d8df8-142">Vista de alarmas</span><span class="sxs-lookup"><span data-stu-id="d8df8-142">View alarms</span></span>

<span data-ttu-id="d8df8-143">panel de historial de alarma de Hello muestra cinco dispositivos informas mayor que los valores de telemetría esperado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Historial de alarma de la lista de tareas en el panel de la solución de Hola][img-alarms]

> [!NOTE]
> <span data-ttu-id="d8df8-145">Estas alarmas se generan por una regla que se incluye en la solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="d8df8-146">Esta regla genera una alerta cuando el valor de temperatura de hello enviada por un dispositivo supera los 60.</span><span class="sxs-lookup"><span data-stu-id="d8df8-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="d8df8-147">Puede definir sus propias reglas y acciones eligiendo [reglas](#add-a-rule) y [acciones](#add-an-action) en el menú izquierdo Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="d8df8-148">Vista de dispositivos</span><span class="sxs-lookup"><span data-stu-id="d8df8-148">View devices</span></span>

<span data-ttu-id="d8df8-149">Hola *dispositivos* lista muestra todos los dispositivos de hello registrado en soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="d8df8-150">Desde la lista de dispositivos de hello, puede ver y editar los metadatos del dispositivo, agregar o quitar dispositivos e invocar métodos en los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="d8df8-151">Puede filtrar y ordenar lista de Hola de dispositivos en la lista de dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="d8df8-152">También puede personalizar las columnas de Hola que se muestra en la lista de dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="d8df8-153">Elija **dispositivos** tooshow lista de dispositivos de Hola para esta solución.</span><span class="sxs-lookup"><span data-stu-id="d8df8-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Lista de dispositivos de Hola de vista en el portal de solución de Hola][img-devicelist]

1. <span data-ttu-id="d8df8-155">lista de dispositivos de Hello inicialmente muestra 25 dispositivos simulados creados por el proceso de aprovisionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="d8df8-156">Puede agregar más dispositivos simulados y físicos toohello solución.</span><span class="sxs-lookup"><span data-stu-id="d8df8-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="d8df8-157">detalles de hello tooview de un dispositivo, elija un dispositivo en la lista de dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Ver detalles del dispositivo hello en el portal de solución de Hola][img-devicedetails]

<span data-ttu-id="d8df8-159">Hola **detalles del dispositivo** panel contiene seis secciones:</span><span class="sxs-lookup"><span data-stu-id="d8df8-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="d8df8-160">Una colección de vínculos que permiten toocustomize Hola icono de dispositivo, deshabilitar dispositivos hello, agregar una regla, invocan un método o envían un comando.</span><span class="sxs-lookup"><span data-stu-id="d8df8-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="d8df8-161">Para ver una comparación de comandos (mensajes de dispositivo a la nube) y métodos (métodos directos), consulte [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="d8df8-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="d8df8-162">Hola **dispositivo gemelas - etiquetas** sección le permite tooedit valores de etiqueta para el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="d8df8-163">Puede mostrar valores de etiqueta en la lista de dispositivos de Hola y usar la lista de dispositivos de etiqueta valores toofilter Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="d8df8-164">Hola **dispositivo gemelas - propiedades deseado** sección le permite tooset propiedad valores toobe enviado toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8df8-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="d8df8-165">Hola **dispositivo gemelas - propiedades notificado** sección muestra valores de propiedad enviados desde dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="d8df8-166">Hola **propiedades del dispositivo** sección muestra información del registro de la identidad de hello como dispositivo de hello claves id y la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d8df8-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="d8df8-167">Hola **trabajos recientes** sección muestra información sobre todos los trabajos que tienen recientemente destinados a este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8df8-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="d8df8-168">Filtrar la lista de dispositivos de Hola</span><span class="sxs-lookup"><span data-stu-id="d8df8-168">Filter hello device list</span></span>

<span data-ttu-id="d8df8-169">Puede usar un filtro toodisplay solo aquellos dispositivos que va a enviar valores de temperatura inesperado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="d8df8-170">Hola remoto solución preconfigurada de supervisión incluye hello **dispositivos en mal estado** filtrar los dispositivos tooshow con un valor de temperatura media superior a 60.</span><span class="sxs-lookup"><span data-stu-id="d8df8-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="d8df8-171">También puede [crear sus propios filtros](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="d8df8-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="d8df8-172">Elija **Abrir filtro guardado** toodisplay una lista de los filtros disponibles.</span><span class="sxs-lookup"><span data-stu-id="d8df8-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="d8df8-173">A continuación, elija **dispositivos en mal estado** filtro de Hola tooapply:</span><span class="sxs-lookup"><span data-stu-id="d8df8-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![Mostrar la lista de Hola de filtros][img-unhealthy-filter]

1. <span data-ttu-id="d8df8-175">lista de dispositivos de Hello ahora muestra solo los dispositivos con un valor de la temperatura media superior a 60.</span><span class="sxs-lookup"><span data-stu-id="d8df8-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Lista de dispositivos filtrado de Hola de vista que muestra los dispositivos en mal estado][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="d8df8-177">Actualizar las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="d8df8-177">Update desired properties</span></span>

<span data-ttu-id="d8df8-178">Ha identificado un conjunto de dispositivos que pueden necesitar corrección.</span><span class="sxs-lookup"><span data-stu-id="d8df8-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="d8df8-179">Sin embargo, decide que no es suficiente para un diagnóstico más detallado claro del problema de Hola frecuencia de datos de Hola de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="d8df8-180">Cambiar Hola telemetría frecuencia toofive segundos tooprovide con toobetter de puntos de datos más diagnosticar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="d8df8-181">Puede insertar esta configuración cambio tooyour los dispositivos remotos desde el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="d8df8-182">Puede realizar el cambio de hello una vez, evaluar el impacto de hello y, a continuación, actuar en los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="d8df8-183">Siga estos toorun pasos un trabajo que cambia hello **TelemetryInterval** deseado de propiedad para los dispositivos de hello afectado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="d8df8-184">Cuando los dispositivos de hello reciben Hola nueva **TelemetryInterval** valor de propiedad, cambian su telemetría de toosend configuración cada cinco segundos en lugar de cada 15 segundos:</span><span class="sxs-lookup"><span data-stu-id="d8df8-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="d8df8-185">Mientras se visualizan lista Hola de dispositivos incorrecto en la lista de dispositivos de hello, elija **programador de trabajos**, a continuación, **Editar dispositivo gemelas**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="d8df8-186">Llamar al trabajo de hello **intervalo de cambio de telemetría**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="d8df8-187">Cambiar valor Hola de hello **propiedad deseada** nombre **deseado. Config.TelemetryInterval** toofive segundos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="d8df8-188">Seleccione **Programación**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-188">Choose **Schedule**.</span></span>

    ![Cambiar hello TelemetryInterval propiedad toofive segundos][img-change-interval]

1. <span data-ttu-id="d8df8-190">Puede supervisar el progreso de hello del trabajo de hello en hello **trabajos de administración** página del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d8df8-191">Si desea toochange un valor de propiedad para un dispositivo individual, utilice hello **propiedades deseadas** sección Hola **detalles del dispositivo** panel en lugar de ejecutar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="d8df8-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="d8df8-192">Esta tarea establece el valor de Hola de hello **TelemetryInterval** deseado propiedad gemelas de dispositivo de Hola para todos los dispositivos seleccionados por el filtro de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="d8df8-193">dispositivos de Hello recuperar este valor del doble de dispositivo de Hola y actualización su comportamiento.</span><span class="sxs-lookup"><span data-stu-id="d8df8-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="d8df8-194">Cuando un dispositivo recupera y procesa una propiedad deseada de un doble de dispositivo, Establece Hola correspondiente notificado value (propiedad).</span><span class="sxs-lookup"><span data-stu-id="d8df8-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="d8df8-195">Invocación de métodos</span><span class="sxs-lookup"><span data-stu-id="d8df8-195">Invoke methods</span></span>

<span data-ttu-id="d8df8-196">Mientras se ejecuta el trabajo de hello, observará en lista de Hola de dispositivos incorrecto que todos estos dispositivos tienen firmware antiguo (menor que la versión 1.6) versiones.</span><span class="sxs-lookup"><span data-stu-id="d8df8-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Hola de vista notifica la versión de firmware para dispositivos en mal estado Hola][img-old-firmware]

<span data-ttu-id="d8df8-198">Esta versión de firmware puede ser la causa de raíz de Hola de hello inesperado porque sabe que otros dispositivos correcto eran actualizado recientemente tooversion 2.0 de los valores de temperatura.</span><span class="sxs-lookup"><span data-stu-id="d8df8-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="d8df8-199">También puede usar integrada de hello **dispositivos de firmware anterior** filtrar tooidentify los dispositivos con las versiones de firmware anteriores.</span><span class="sxs-lookup"><span data-stu-id="d8df8-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="d8df8-200">Desde el portal de hello, a continuación, se pueden actualizar remotamente todos los dispositivos de hello sigan ejecutando versiones de firmware anterior:</span><span class="sxs-lookup"><span data-stu-id="d8df8-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="d8df8-201">Elija **Abrir filtro guardado** toodisplay una lista de los filtros disponibles.</span><span class="sxs-lookup"><span data-stu-id="d8df8-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="d8df8-202">A continuación, elija **dispositivos de firmware anterior** filtro de Hola tooapply:</span><span class="sxs-lookup"><span data-stu-id="d8df8-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![Mostrar la lista de Hola de filtros][img-old-filter]

1. <span data-ttu-id="d8df8-204">lista de dispositivos de Hello ahora muestra solo los dispositivos con las versiones de firmware anteriores.</span><span class="sxs-lookup"><span data-stu-id="d8df8-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="d8df8-205">Esta lista incluye cinco dispositivos de hello identificados por hello **dispositivos en mal estado** filtro y tres dispositivos adicionales:</span><span class="sxs-lookup"><span data-stu-id="d8df8-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![Lista de dispositivos filtrado de Hola de vista mostrará dispositivos antiguos][img-filtered-old-list]

1. <span data-ttu-id="d8df8-207">Elija **Programador de trabajos** y a continuación, **Invocar método**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="d8df8-208">Establecer **nombre del trabajo** demasiado**tooversion de actualización de Firmware 2.0**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="d8df8-209">Elija **InitiateFirmwareUpdate** como hello **método**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="d8df8-210">Conjunto hello **FwPackageUri** parámetro demasiado**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="d8df8-211">Seleccione **Programación**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-211">Choose **Schedule**.</span></span> <span data-ttu-id="d8df8-212">valor predeterminado de Hello es Hola trabajo toorun ahora.</span><span class="sxs-lookup"><span data-stu-id="d8df8-212">hello default is for hello job toorun now.</span></span>

    ![Crear el firmware de Hola de tooupdate de trabajo de los dispositivos de hello seleccionado][img-method-update]

> [!NOTE]
> <span data-ttu-id="d8df8-214">Elija si desea que un método en un dispositivo individual tooinvoke, **métodos** en hello **detalles del dispositivo** panel en lugar de ejecutar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="d8df8-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="d8df8-215">Este trabajo invoca hello **InitiateFirmwareUpdate** método directo en todos los dispositivos de Hola Hola filtro seleccionados.</span><span class="sxs-lookup"><span data-stu-id="d8df8-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="d8df8-216">Dispositivos responderán inmediatamente tooIoT concentrador y, a continuación, inician el proceso de actualización de firmware de Hola de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="d8df8-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="d8df8-217">los dispositivos de Hello proporcionan información de estado sobre el proceso de actualización de firmware de Hola a través de los valores de propiedad notificado, como se muestra en las siguientes capturas de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="d8df8-218">Elija hello **actualizar** información de Hola de icono tooupdate en las listas de dispositivo y el trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="d8df8-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="d8df8-219">![Lista de trabajos que muestra la ejecución de lista de actualización de firmware de hello][img-update-1]
![lista de dispositivos que muestra el estado de actualización de firmware][img-update-2]
![trabajo mostrando Hola firmware actualización lista completa][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="d8df8-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="d8df8-220">En un entorno de producción, puede programar trabajos toorun durante una ventana de mantenimiento designado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="d8df8-221">Revisión del escenario</span><span class="sxs-lookup"><span data-stu-id="d8df8-221">Scenario review</span></span>

<span data-ttu-id="d8df8-222">En este escenario, ha identificado un problema potencial con algunos de los dispositivos remotos mediante el historial de alarma de hello en el panel de Hola y un filtro.</span><span class="sxs-lookup"><span data-stu-id="d8df8-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="d8df8-223">Que, a continuación, filtro Hola usado y un trabajo tooremotely configuran Hola dispositivos tooprovide más toohelp información diagnosticar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="d8df8-224">Por último, se utilizan un filtro y un mantenimiento de tooschedule de trabajo en los dispositivos de hello afectado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="d8df8-225">Si devuelve toohello panel, puede comprobar que ya no son las alarmas procedentes de dispositivos de la solución.</span><span class="sxs-lookup"><span data-stu-id="d8df8-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="d8df8-226">Puede utilizar un filtro tooverify que Hola firmware está actualizado en todos los dispositivos de hello en la solución y que no son dispositivos no hay más incorrecto:</span><span class="sxs-lookup"><span data-stu-id="d8df8-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![Filtro que muestra que todos los dispositivos tienen firmware actualizado][img-updated]

![Filtro que muestra que todos los dispositivos tiene un estado correcto][img-healthy]

## <a name="other-features"></a><span data-ttu-id="d8df8-229">Otras características</span><span class="sxs-lookup"><span data-stu-id="d8df8-229">Other features</span></span>

<span data-ttu-id="d8df8-230">Hello las secciones siguientes describen algunas características adicionales de hello solución preconfigurada de supervisión remota que no se describen como parte del escenario anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="d8df8-231">Personalización de columnas</span><span class="sxs-lookup"><span data-stu-id="d8df8-231">Customize columns</span></span>

<span data-ttu-id="d8df8-232">Puede personalizar la información de Hola se muestra en la lista de dispositivos de hello eligiendo **editor columna**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="d8df8-233">Puede agregar y quitar las columnas que muestran los valores de propiedad y etiqueta notificados.</span><span class="sxs-lookup"><span data-stu-id="d8df8-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="d8df8-234">Las columnas también se pueden reordenar y cambiar de nombre:</span><span class="sxs-lookup"><span data-stu-id="d8df8-234">You can also reorder and rename columns:</span></span>

   ![Lista de dispositivos de columna editor ion Hola][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="d8df8-236">Personalizar el icono de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="d8df8-236">Customize hello device icon</span></span>

<span data-ttu-id="d8df8-237">Puede personalizar el icono de dispositivo de hello aparece en la lista de dispositivos de Hola de hello **detalles del dispositivo** panel como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d8df8-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="d8df8-238">Elija Hola Hola de tooopen de icono de lápiz **Editar imagen** panel para un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="d8df8-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![Abrir el editor de imágenes del dispositivo][img-startimageedit]

1. <span data-ttu-id="d8df8-240">Cargar una nueva imagen o utilizar una de las imágenes existentes hello y, a continuación, elija **guardar**:</span><span class="sxs-lookup"><span data-stu-id="d8df8-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![Modificar editor de imágenes del dispositivo][img-imageedit]

1. <span data-ttu-id="d8df8-242">Hello imagen que ha seleccionado ahora muestra de Hola **icono** columna para dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="d8df8-243">image de Hola se almacena en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="d8df8-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="d8df8-244">Una etiqueta en gemelas de dispositivo de hello contiene una imagen de toohello de vínculo en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="d8df8-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="d8df8-245">Agregar un dispositivo</span><span class="sxs-lookup"><span data-stu-id="d8df8-245">Add a device</span></span>

<span data-ttu-id="d8df8-246">Al implementar soluciones de hello preconfigurado, aprovisionar automáticamente 25 dispositivos de ejemplo que puede ver en la lista de dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="d8df8-247">Estos dispositivos son *dispositivos simulados* que se ejecutan en un WebJob de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8df8-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="d8df8-248">Dispositivos simulados facilitan automáticamente tooexperiment con la solución de hello preconfigurado sin Hola necesidad toodeploy real físico dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="d8df8-249">Si desea tooconnect una solución de toohello dispositivo real, vea hello [conectar su toohello de dispositivo remoto solución preconfigurada de supervisión] [ lnk-connect-rm] tutorial.</span><span class="sxs-lookup"><span data-stu-id="d8df8-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="d8df8-250">Hello pasos siguientes muestran cómo tooadd una solución de toohello dispositivo simulado:</span><span class="sxs-lookup"><span data-stu-id="d8df8-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="d8df8-251">Navegue toohello back-lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="d8df8-252">elegir un dispositivo, tooadd **+ agregar un dispositivo** en la esquina izquierda inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![Agregar una solución de toohello preconfigurado de dispositivo][img-adddevice]

1. <span data-ttu-id="d8df8-254">Elija **Agregar nuevo** en hello **dispositivo simulado** icono.</span><span class="sxs-lookup"><span data-stu-id="d8df8-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![Establecer nuevos detalles de los dispositivos en el panel][img-addnew]

   <span data-ttu-id="d8df8-256">En toocreating de agregar un nuevo dispositivo simulado, también puede agregar un dispositivo físico si elige toocreate una **dispositivo personalizado**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="d8df8-257">toolearn más información acerca de la conexión de dispositivos físicos toohello solución, consulte [conectar su toohello dispositivo IoT Suite solución preconfigurada de supervisión remota][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="d8df8-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="d8df8-258">Seleccione **Let me define my own Device ID** (Permitirme definir mi propio identificador de dispositivo) y escriba un nombre de identificador de dispositivo único como **mydevice_01**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="d8df8-259">Seleccione **Create**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-259">Choose **Create**.</span></span>

   ![Guardar un dispositivo nuevo][img-definedevice]

1. <span data-ttu-id="d8df8-261">En el paso 3 de **agregar un dispositivo simulado**, elija **realiza** lista de dispositivos de tooreturn toohello.</span><span class="sxs-lookup"><span data-stu-id="d8df8-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="d8df8-262">Puede ver el dispositivo **ejecutando** en la lista de dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-262">You can view your device **Running** in hello device list.</span></span>

    ![Ver un dispositivo nuevo en la lista de dispositivos][img-runningnew]

1. <span data-ttu-id="d8df8-264">También puede ver Hola simulados telemetría desde el nuevo dispositivo en el panel de hello:</span><span class="sxs-lookup"><span data-stu-id="d8df8-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![Ver telemetría desde el nuevo dispositivo][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="d8df8-266">Deshabilitar y eliminar un dispositivo</span><span class="sxs-lookup"><span data-stu-id="d8df8-266">Disable and delete a device</span></span>

<span data-ttu-id="d8df8-267">Puede deshabilitar un dispositivo y, después, quitarlo:</span><span class="sxs-lookup"><span data-stu-id="d8df8-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Deshabilitar y quitar un dispositivo][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="d8df8-269">Agregar una regla</span><span class="sxs-lookup"><span data-stu-id="d8df8-269">Add a rule</span></span>

<span data-ttu-id="d8df8-270">No hay reglas para el nuevo dispositivo de Hola que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="d8df8-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="d8df8-271">En esta sección, agregará una regla que desencadena una alarma cuando temperatura Hola Hola nuevo dispositivo supera grados 47.</span><span class="sxs-lookup"><span data-stu-id="d8df8-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="d8df8-272">Antes de empezar, observe que historial de telemetría de Hola de nuevo dispositivo de hello en el panel de hello muestra la temperatura del dispositivo Hola nunca supere el 45 grados.</span><span class="sxs-lookup"><span data-stu-id="d8df8-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="d8df8-273">Navegue toohello back-lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="d8df8-274">tooadd una regla para dispositivos de hello, seleccione el nuevo dispositivo de hello **lista de dispositivos**y, a continuación, elija **Agregar regla**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="d8df8-275">Crear una regla que usa **temperatura** como campo de datos de Hola y utiliza **AlarmTemp** como salida de hello cuando temperatura Hola supera 47 grados:</span><span class="sxs-lookup"><span data-stu-id="d8df8-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![Agregar una regla de dispositivo][img-adddevicerule]

1. <span data-ttu-id="d8df8-277">los cambios, elija a toosave **guardar y ver las reglas**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="d8df8-278">Elija **comandos** en panel de detalles de dispositivo de hello en dispositivo nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![Agregar una regla de dispositivo][img-adddevicerule2]

1. <span data-ttu-id="d8df8-280">Seleccione **ChangeSetPointTemp** desde la lista de comandos de Hola y establezca **SetPointTemp** too45.</span><span class="sxs-lookup"><span data-stu-id="d8df8-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="d8df8-281">A continuación, elija **Enviar comando**:</span><span class="sxs-lookup"><span data-stu-id="d8df8-281">Then choose **Send Command**:</span></span>

    ![Agregar una regla de dispositivo][img-adddevicerule3]

1. <span data-ttu-id="d8df8-283">Navegue panel toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="d8df8-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="d8df8-284">Después de unos minutos, verá una nueva entrada en hello **historial de alarma** panel cuando temperatura Hola notificados por el nuevo dispositivo supera el umbral de 47 grados de hello:</span><span class="sxs-lookup"><span data-stu-id="d8df8-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![Agregar una regla de dispositivo][img-adddevicerule4]

1. <span data-ttu-id="d8df8-286">Puede revisar y editar todas las reglas en hello **reglas** página del panel de hello:</span><span class="sxs-lookup"><span data-stu-id="d8df8-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![Enumerar reglas de dispositivo][img-rules]

1. <span data-ttu-id="d8df8-288">Puede revisar y editar todas las acciones de Hola que pueden realizarse en la regla de tooa de respuesta en hello **acciones** página del panel de hello:</span><span class="sxs-lookup"><span data-stu-id="d8df8-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![Enumerar acciones de dispositivo][img-actions]

> [!NOTE]
> <span data-ttu-id="d8df8-290">Es toodefine posibles acciones que pueden enviar un mensaje de correo electrónico o SMS en respuesta tooa regla o integrar con un sistema de línea de negocio a través de un [aplicación lógica][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="d8df8-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="d8df8-291">Para obtener más información, vea hello [tooyour de conectar la aplicación de lógica en la supervisión remota de Azure IoT conjunto preconfigurado solución][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="d8df8-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="d8df8-292">Administración de filtros</span><span class="sxs-lookup"><span data-stu-id="d8df8-292">Manage filters</span></span>

<span data-ttu-id="d8df8-293">En la lista de dispositivos de hello, puede crear, guardar y volver a cargar filtros toodisplay una lista personalizada de concentrador de dispositivos conectados tooyour.</span><span class="sxs-lookup"><span data-stu-id="d8df8-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="d8df8-294">toocreate un filtro:</span><span class="sxs-lookup"><span data-stu-id="d8df8-294">toocreate a filter:</span></span>

1. <span data-ttu-id="d8df8-295">Elija el icono de filtro de edición de Hola por encima de la lista de Hola de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="d8df8-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![Editor de filtros de hello abierto][img-editfiltericon]

1. <span data-ttu-id="d8df8-297">Hola **editor de filtros**, agregar campos de hello, operadores y lista de dispositivos de valores toofilter Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="d8df8-298">Puede agregar varios toorefine cláusulas el filtro.</span><span class="sxs-lookup"><span data-stu-id="d8df8-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="d8df8-299">Elija **filtro** filtro de Hola tooapply:</span><span class="sxs-lookup"><span data-stu-id="d8df8-299">Choose **Filter** tooapply hello filter:</span></span>

    ![Crear un filtro][img-filtereditor]

1. <span data-ttu-id="d8df8-301">En este ejemplo, la lista de Hola se filtra por fabricante y número de modelo:</span><span class="sxs-lookup"><span data-stu-id="d8df8-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![Lista filtrada][img-filterelist]

1. <span data-ttu-id="d8df8-303">toosave el filtro con un nombre personalizado, elija hello **Guardar como** icono:</span><span class="sxs-lookup"><span data-stu-id="d8df8-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![Agregar un filtro][img-savefilter]

1. <span data-ttu-id="d8df8-305">tooreapply un filtro guardado previamente, elija hello **Abrir filtro guardado** icono:</span><span class="sxs-lookup"><span data-stu-id="d8df8-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![Abrir un filtro][img-openfilter]

<span data-ttu-id="d8df8-307">Se pueden crear filtros basados en el Id. de dispositivo, estado del dispositivo, propiedades deseadas, propiedades notificadas y etiquetas.</span><span class="sxs-lookup"><span data-stu-id="d8df8-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="d8df8-308">Agregar su propio dispositivo tooa de etiquetas personalizadas en hello **etiquetas** sección de hello **detalles del dispositivo** panel o ejecutar un trabajo tooupdate etiquetas en varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="d8df8-309">Hola **editor de filtros**, puede usar hello **vista avanzada** tooedit Hola texto de la consulta directamente.</span><span class="sxs-lookup"><span data-stu-id="d8df8-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="d8df8-310">Comandos:</span><span class="sxs-lookup"><span data-stu-id="d8df8-310">Commands</span></span>

<span data-ttu-id="d8df8-311">De hello **detalles del dispositivo** panel, puede enviar el dispositivo de toohello de comandos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="d8df8-312">Cuando se inicia por primera vez un dispositivo, envía información sobre Hola comandos admite toohello solución.</span><span class="sxs-lookup"><span data-stu-id="d8df8-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="d8df8-313">Para obtener una explicación de las diferencias de hello entre los comandos y métodos, consulte [opciones de centro de IoT de Azure en la nube al dispositivo][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="d8df8-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="d8df8-314">Elija **comandos** en hello **detalles del dispositivo** panel del dispositivo seleccionado hello:</span><span class="sxs-lookup"><span data-stu-id="d8df8-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![Comandos de los dispositivos en el panel][img-devicecommands]

1. <span data-ttu-id="d8df8-316">Seleccione **PingDevice** desde la lista de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="d8df8-317">Elija **Enviar comando**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="d8df8-318">Puede ver estado de saludo del comando de Hola Hola historial de comandos.</span><span class="sxs-lookup"><span data-stu-id="d8df8-318">You can see hello status of hello command in hello command history.</span></span>

   ![Estado de los comandos en el panel][img-pingcommand]

<span data-ttu-id="d8df8-320">solución de Hello realiza un seguimiento de estado Hola de cada comando que envía.</span><span class="sxs-lookup"><span data-stu-id="d8df8-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="d8df8-321">Inicialmente es el resultado de hello **pendiente**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="d8df8-322">Cuando el dispositivo de hello informa de que se ha ejecutado el comando hello, del conjunto de resultados de hello es demasiado**correcto**.</span><span class="sxs-lookup"><span data-stu-id="d8df8-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="d8df8-323">Entre bastidores de Hola</span><span class="sxs-lookup"><span data-stu-id="d8df8-323">Behind hello scenes</span></span>

<span data-ttu-id="d8df8-324">Al implementar una solución preconfigurada, el proceso de implementación de hello crea varios recursos en hello Azure suscripción que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="d8df8-325">Puede ver estos recursos en hello Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="d8df8-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="d8df8-326">proceso de implementación de Hello crea un **grupo de recursos** con un nombre basado en el nombre de Hola que elija para su solución preconfigurada:</span><span class="sxs-lookup"><span data-stu-id="d8df8-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Solución preconfigurada en hello portal de Azure][img-portal]

<span data-ttu-id="d8df8-328">Puede ver configuración de Hola de cada recurso mediante su selección en la lista de Hola de recursos de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="d8df8-329">También puede ver el código fuente de hello para la solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="d8df8-330">Hola código fuente de solución preconfigurada de supervisión remota está en hello [-iot-remoto-supervisión de azure] [ lnk-rmgithub] repositorio de GitHub:</span><span class="sxs-lookup"><span data-stu-id="d8df8-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="d8df8-331">Hola **DeviceAdministration** carpeta contiene el código de origen de hello para el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="d8df8-332">Hola **simulador** carpeta contiene código de fuente de hello de dispositivo simulado Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="d8df8-333">Hola **EventProcessor** carpeta contiene el código de origen de Hola para procesos de back-end de Hola que controla la telemetría de Hola entrantes.</span><span class="sxs-lookup"><span data-stu-id="d8df8-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="d8df8-334">Cuando haya terminado, puede eliminar solución Hola preconfigurado de su suscripción de Azure en hello [azureiotsuite.com] [ lnk-azureiotsuite] sitio.</span><span class="sxs-lookup"><span data-stu-id="d8df8-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="d8df8-335">Este sitio le permite eliminar tooeasily que todos Hola recursos que estaban aprovisionados al crear soluciones de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="d8df8-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="d8df8-336">tooensure eliminar todos los elementos relacionados con la solución toohello preconfigurado, eliminarlo de hello [azureiotsuite.com] [ lnk-azureiotsuite] de sitio y no se elimine el grupo de recursos de hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8df8-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8df8-337">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8df8-337">Next Steps</span></span>

<span data-ttu-id="d8df8-338">Ahora que ha implementado una solución de trabajo configurado preconfigurada, puede seguir introducción con Suite IoT leyendo Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="d8df8-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="d8df8-339">[Tutorial de la solución preconfigurada de supervisión remota][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="d8df8-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="d8df8-340">[Conectar su toohello de dispositivo remoto solución preconfigurada de supervisión][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="d8df8-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="d8df8-341">[Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="d8df8-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md