---
title: "Tutorial de solución de supervisión preconfigurado aaaRemote | Documentos de Microsoft"
description: "Una descripción de hello Azure IoT preconfigurado supervisión remota de solución y su arquitectura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="7e30d-103">Tutorial de la solución preconfigurada de supervisión remota</span><span class="sxs-lookup"><span data-stu-id="7e30d-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="7e30d-104">Hola supervisión remota de IoT Suite [preconfigurado solución] [ lnk-preconfigured-solutions] es una implementación de un extremo a extremo de supervisión soluciones para varias máquinas que se ejecutan en ubicaciones remotas.</span><span class="sxs-lookup"><span data-stu-id="7e30d-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="7e30d-105">solución de Hello combina servicios de Azure clave tooprovide una implementación genérica de escenario empresarial de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="7e30d-106">Puede usar soluciones de hello como punto de partida para su propia implementación y [personalizar] [ lnk-customize] toomeet sus propios requisitos empresariales específicos.</span><span class="sxs-lookup"><span data-stu-id="7e30d-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="7e30d-107">Este artículo le guiará a través de algunos de los elementos clave de Hola de tooenable de solución de supervisión remota de hello toounderstand su funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="7e30d-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="7e30d-108">Esta información le ayuda a:</span><span class="sxs-lookup"><span data-stu-id="7e30d-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="7e30d-109">Solucionar problemas de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="7e30d-110">Planear cómo toocustomize toohello solución toomeet sus propios requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="7e30d-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="7e30d-111">Diseñar una solución de IoT propia que utilice servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e30d-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="7e30d-112">Arquitectura lógica</span><span class="sxs-lookup"><span data-stu-id="7e30d-112">Logical architecture</span></span>

<span data-ttu-id="7e30d-113">Hola siguiente diagrama describe los componentes lógicos de Hola de solución de hello preconfigurado:</span><span class="sxs-lookup"><span data-stu-id="7e30d-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Arquitectura lógica](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="7e30d-115">Dispositivos simulados</span><span class="sxs-lookup"><span data-stu-id="7e30d-115">Simulated devices</span></span>

<span data-ttu-id="7e30d-116">En la solución Hola preconfigurado, dispositivo simulado de Hola representa un dispositivo de enfriamiento (como un acondicionador de aire de creación o la unidad de control de utilidad aire).</span><span class="sxs-lookup"><span data-stu-id="7e30d-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="7e30d-117">Al implementar soluciones de hello preconfigurado, aprovisionar automáticamente cuatro dispositivos simulados que se ejecutan en un [WebJob de Azure][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="7e30d-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="7e30d-118">dispositivos de Hello simulado facilitan tooexplore Hola comportamiento de hello solución sin Hola necesidad toodeploy los dispositivos físicos.</span><span class="sxs-lookup"><span data-stu-id="7e30d-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="7e30d-119">toodeploy un dispositivo físico real, vea hello [conectar su toohello de dispositivo remoto solución preconfigurada de supervisión] [ lnk-connect-rm] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7e30d-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="7e30d-120">Mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="7e30d-120">Device-to-cloud messages</span></span>

<span data-ttu-id="7e30d-121">Cada dispositivo simulado puede enviar Hola después tooIoT de tipos de mensaje concentrador:</span><span class="sxs-lookup"><span data-stu-id="7e30d-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="7e30d-122">Message</span><span class="sxs-lookup"><span data-stu-id="7e30d-122">Message</span></span> | <span data-ttu-id="7e30d-123">Description</span><span class="sxs-lookup"><span data-stu-id="7e30d-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e30d-124">Inicio</span><span class="sxs-lookup"><span data-stu-id="7e30d-124">Startup</span></span> |<span data-ttu-id="7e30d-125">Cuando se inicia el dispositivo de hello, envía una **información del dispositivo** mensaje que contiene información sobre ella misma toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="7e30d-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="7e30d-126">Estos datos incluyen el Id. de dispositivo de hello y una lista de comandos de Hola y métodos Hola admite el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="7e30d-127">Presencia</span><span class="sxs-lookup"><span data-stu-id="7e30d-127">Presence</span></span> |<span data-ttu-id="7e30d-128">Un dispositivo envía periódicamente un **presencia** tooreport de mensajes si el dispositivo Hola puede detectar la presencia de Hola de un sensor.</span><span class="sxs-lookup"><span data-stu-id="7e30d-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="7e30d-129">Telemetría</span><span class="sxs-lookup"><span data-stu-id="7e30d-129">Telemetry</span></span> |<span data-ttu-id="7e30d-130">Un dispositivo envía periódicamente un **telemetría** mensaje que notifica simulados valores de temperatura de Hola y humedad procedentes de dispositivos de Hola de simular sensores.</span><span class="sxs-lookup"><span data-stu-id="7e30d-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="7e30d-131">solución de Hello almacena la lista de Hola de comandos admitidos por dispositivo de hello en una base de datos de la base de datos de Cosmos y no en gemelas de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="7e30d-132">Propiedades y dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="7e30d-132">Properties and device twins</span></span>

<span data-ttu-id="7e30d-133">dispositivos simulados Hello envían Hola después toohello de propiedades de dispositivo [gemelas] [ lnk-device-twins] en el centro de IoT hello como *notificado propiedades*.</span><span class="sxs-lookup"><span data-stu-id="7e30d-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="7e30d-134">dispositivo envía Hello notificado propiedades en el inicio y en respuesta tooa **cambio de estado de dispositivo** comando o un método.</span><span class="sxs-lookup"><span data-stu-id="7e30d-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="7e30d-135">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7e30d-135">Property</span></span> | <span data-ttu-id="7e30d-136">Propósito</span><span class="sxs-lookup"><span data-stu-id="7e30d-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="7e30d-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="7e30d-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="7e30d-138">Dispositivo de Hola de frecuencia (segundos) envía telemetría</span><span class="sxs-lookup"><span data-stu-id="7e30d-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="7e30d-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="7e30d-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="7e30d-140">Especifica el valor medio de Hola para telemetría de temperatura de hello simulada</span><span class="sxs-lookup"><span data-stu-id="7e30d-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="7e30d-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="7e30d-141">Device.DeviceID</span></span> |<span data-ttu-id="7e30d-142">Id. que se proporcionan o se asigna cuando se crea un dispositivo de solución de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="7e30d-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="7e30d-143">Device.DeviceState</span></span> | <span data-ttu-id="7e30d-144">Estado notificado por dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-144">State reported by hello device</span></span> |
| <span data-ttu-id="7e30d-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="7e30d-145">Device.CreatedTime</span></span> |<span data-ttu-id="7e30d-146">Dispositivo de Hola de tiempo se creó en soluciones de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="7e30d-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="7e30d-147">Device.StartupTime</span></span> |<span data-ttu-id="7e30d-148">Se inició el dispositivo de Hola de tiempo</span><span class="sxs-lookup"><span data-stu-id="7e30d-148">Time hello device was started</span></span> |
| <span data-ttu-id="7e30d-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="7e30d-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="7e30d-150">cambiar el número de versión de Hello de la última propiedad deseado de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="7e30d-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="7e30d-151">Device.Location.Latitude</span></span> |<span data-ttu-id="7e30d-152">Ubicación de latitud de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="7e30d-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="7e30d-153">Device.Location.Longitude</span></span> |<span data-ttu-id="7e30d-154">Ubicación de la longitud del dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="7e30d-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="7e30d-155">System.Manufacturer</span></span> |<span data-ttu-id="7e30d-156">Fabricante del dispositivo</span><span class="sxs-lookup"><span data-stu-id="7e30d-156">Device manufacturer</span></span> |
| <span data-ttu-id="7e30d-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="7e30d-157">System.ModelNumber</span></span> |<span data-ttu-id="7e30d-158">Número de modelo de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-158">Model number of hello device</span></span> |
| <span data-ttu-id="7e30d-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="7e30d-159">System.SerialNumber</span></span> |<span data-ttu-id="7e30d-160">Número de serie del dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-160">Serial number of hello device</span></span> |
| <span data-ttu-id="7e30d-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="7e30d-161">System.FirmwareVersion</span></span> |<span data-ttu-id="7e30d-162">Versión actual de firmware de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="7e30d-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="7e30d-163">System.Platform</span></span> |<span data-ttu-id="7e30d-164">Arquitectura de la plataforma de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="7e30d-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="7e30d-165">System.Processor</span></span> |<span data-ttu-id="7e30d-166">Dispositivo en ejecución Hola procesador</span><span class="sxs-lookup"><span data-stu-id="7e30d-166">Processor running hello device</span></span> |
| <span data-ttu-id="7e30d-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="7e30d-167">System.InstalledRAM</span></span> |<span data-ttu-id="7e30d-168">Cantidad de RAM instalada en el dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="7e30d-169">simulador de Hello propaga estas propiedades en los dispositivos simulados con valores de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="7e30d-170">Cada vez simulador Hola Inicializa un dispositivo simulado, el dispositivo de hello notifica Hola metadatos previamente definidos tooIoT concentrador como propiedades notificados.</span><span class="sxs-lookup"><span data-stu-id="7e30d-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="7e30d-171">Propiedades incluidos solo pueden actualizarse por dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="7e30d-172">toochange una propiedad incluida, se establece una propiedad deseada en el portal de solución.</span><span class="sxs-lookup"><span data-stu-id="7e30d-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="7e30d-173">Es responsabilidad de hello de dispositivo de Hola para:</span><span class="sxs-lookup"><span data-stu-id="7e30d-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="7e30d-174">Recuperar de forma periódica propiedades deseadas Hola centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7e30d-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="7e30d-175">Actualice su configuración con el valor de propiedad de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="7e30d-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="7e30d-176">Enviar nuevo centro de atrás toohello valor Hola como una propiedad notificada.</span><span class="sxs-lookup"><span data-stu-id="7e30d-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="7e30d-177">En el panel de la solución de hello, puede usar *deseado propiedades* tooset propiedades en un dispositivo mediante el uso de hello [gemelas dispositivo][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="7e30d-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="7e30d-178">Normalmente, un dispositivo lee un valor de propiedad de hello concentrador tooupdate que cambian su estado interno y Hola de informe como una propiedad notificada.</span><span class="sxs-lookup"><span data-stu-id="7e30d-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="7e30d-179">Hello dispositivo simulado código solo usa hello **Desired.Config.TemperatureMeanValue** y **Desired.Config.TelemetryInterval** hello tooupdate de propiedades que desee notificado propiedades devuelve tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="7e30d-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="7e30d-180">Se omiten todas las demás solicitudes de cambio de la propiedad deseada en el dispositivo simulado de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="7e30d-181">Métodos</span><span class="sxs-lookup"><span data-stu-id="7e30d-181">Methods</span></span>

<span data-ttu-id="7e30d-182">Hello dispositivos simulados pueden controlar Hola siguiendo métodos ([dirigir métodos][lnk-direct-methods]) se invoca desde el portal de solución de Hola a través del centro de IoT de hello:</span><span class="sxs-lookup"><span data-stu-id="7e30d-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="7e30d-183">Método</span><span class="sxs-lookup"><span data-stu-id="7e30d-183">Method</span></span> | <span data-ttu-id="7e30d-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="7e30d-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e30d-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="7e30d-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="7e30d-186">Indica a Hola dispositivo tooperform una actualización de firmware</span><span class="sxs-lookup"><span data-stu-id="7e30d-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="7e30d-187">Reboot</span><span class="sxs-lookup"><span data-stu-id="7e30d-187">Reboot</span></span> |<span data-ttu-id="7e30d-188">Indica a Hola dispositivo tooreboot</span><span class="sxs-lookup"><span data-stu-id="7e30d-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="7e30d-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="7e30d-189">FactoryReset</span></span> |<span data-ttu-id="7e30d-190">Indica a Hola dispositivo tooperform restablecer una fábrica</span><span class="sxs-lookup"><span data-stu-id="7e30d-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="7e30d-191">Algunos métodos usan propiedades notificado tooreport en curso.</span><span class="sxs-lookup"><span data-stu-id="7e30d-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="7e30d-192">Por ejemplo, hello **InitiateFirmwareUpdate** método simula la ejecución actualización Hola asincrónicamente en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="7e30d-193">método Hello devuelve inmediatamente en el dispositivo de hello, mientras continúa la tarea asincrónica Hola volver las actualizaciones de estado de toosend toohello solución panel mediante informó de propiedades.</span><span class="sxs-lookup"><span data-stu-id="7e30d-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="7e30d-194">Comandos:</span><span class="sxs-lookup"><span data-stu-id="7e30d-194">Commands</span></span>

<span data-ttu-id="7e30d-195">dispositivos de Hello simulado pueden administrar Hola después de comandos (en la nube al dispositivo mensajes) enviados desde el portal de solución de Hola a través del centro de IoT de hello:</span><span class="sxs-lookup"><span data-stu-id="7e30d-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="7e30d-196">Comando</span><span class="sxs-lookup"><span data-stu-id="7e30d-196">Command</span></span> | <span data-ttu-id="7e30d-197">Description</span><span class="sxs-lookup"><span data-stu-id="7e30d-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e30d-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="7e30d-198">PingDevice</span></span> |<span data-ttu-id="7e30d-199">Envía una *ping* toohello toocheck de dispositivo está activo</span><span class="sxs-lookup"><span data-stu-id="7e30d-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="7e30d-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="7e30d-200">StartTelemetry</span></span> |<span data-ttu-id="7e30d-201">Dispositivo de hello inicia enviar telemetría</span><span class="sxs-lookup"><span data-stu-id="7e30d-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="7e30d-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="7e30d-202">StopTelemetry</span></span> |<span data-ttu-id="7e30d-203">Dispositivo de Hola se detiene en el envío de telemetría</span><span class="sxs-lookup"><span data-stu-id="7e30d-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="7e30d-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="7e30d-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="7e30d-205">Cambia el valor punto establecido Hola alrededor de qué Hola se generan datos aleatorios</span><span class="sxs-lookup"><span data-stu-id="7e30d-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="7e30d-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="7e30d-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="7e30d-207">Desencadenadores Hola toosend de simulador de dispositivo un valor de telemetría adicionales (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="7e30d-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="7e30d-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="7e30d-208">ChangeDeviceState</span></span> |<span data-ttu-id="7e30d-209">Cambia una propiedad de estado extendido para dispositivo hello y envía el mensaje de información de dispositivo de hello de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e30d-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="7e30d-210">Para ver una comparación de estos comandos (mensajes de la nube al dispositivo) y métodos (métodos directos), consulte [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="7e30d-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="7e30d-211">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7e30d-211">IoT Hub</span></span>

<span data-ttu-id="7e30d-212">Hola [centro de IoT] [ lnk-iothub] introduce los datos enviados desde dispositivos de hello en nube de Hola y hace que los trabajos de análisis de transmisiones de Azure (ASA) toohello disponibles.</span><span class="sxs-lookup"><span data-stu-id="7e30d-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="7e30d-213">Cada trabajo ASA de flujo utiliza una centro de IoT consumidor grupo tooread hello secuencia independiente de los mensajes de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7e30d-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="7e30d-214">Hola centro de IoT de solución de hello también:</span><span class="sxs-lookup"><span data-stu-id="7e30d-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="7e30d-215">Mantiene un registro de la identidad que almacena los identificadores de Hola y claves de autenticación de todos los dispositivos de hello permitidas tooconnect toohello portal.</span><span class="sxs-lookup"><span data-stu-id="7e30d-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="7e30d-216">Puede habilitar y deshabilitar dispositivos a través del registro de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="7e30d-217">Envía comandos tooyour dispositivos en nombre de portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="7e30d-218">Invoca los métodos de los dispositivos en nombre de portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="7e30d-219">Mantiene los dispositivos gemelos para todos los dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="7e30d-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="7e30d-220">Un gemelas dispositivo almacena valores de propiedades de hello notificados por un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="7e30d-221">Un gemelas dispositivo también almacena las propiedades deseadas, establecidas en el portal de solución de hello, para hello dispositivo tooretrieve cuando se conecta a continuación.</span><span class="sxs-lookup"><span data-stu-id="7e30d-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="7e30d-222">Programaciones de trabajos tooset propiedades para varios dispositivos o para invocar métodos en varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7e30d-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="7e30d-223">Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="7e30d-223">Azure Stream Analytics</span></span>

<span data-ttu-id="7e30d-224">Hola remoto de supervisión de solución, [análisis de transmisiones de Azure] [ lnk-asa] (ASA) envía los mensajes de dispositivo recibidos por componentes de hello IoT hub tooother back-end para el procesamiento o de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7e30d-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="7e30d-225">Los distintos trabajos ASA realizan funciones específicas basadas en contenido de Hola de mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="7e30d-226">**Trabajo 1: Información del dispositivo** filtra los mensajes de información de dispositivo de la secuencia de mensajes de Hola entrantes y los envía el punto de conexión de tooan centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="7e30d-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="7e30d-227">Un dispositivo envía mensajes de información de dispositivo en el inicio y de respuesta tooa **SendDeviceInfo** comando.</span><span class="sxs-lookup"><span data-stu-id="7e30d-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="7e30d-228">Este trabajo utiliza Hola después tooidentify de definición de consulta **información del dispositivo** mensajes:</span><span class="sxs-lookup"><span data-stu-id="7e30d-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="7e30d-229">Este trabajo envía su centro de eventos de salida tooan para su posterior procesamiento.</span><span class="sxs-lookup"><span data-stu-id="7e30d-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="7e30d-230">**Trabajo 2: reglas** evalúa los valores de telemetría de temperatura y humedad entrantes según los umbrales por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="7e30d-231">Valores de umbral se establecen en el editor de reglas de hello disponible en el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="7e30d-232">Cada par de valor/dispositivo se almacena en la marca de tiempo de un blob que se lee en Análisis de transmisiones como **datos de referencia**.</span><span class="sxs-lookup"><span data-stu-id="7e30d-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="7e30d-233">trabajo Hola compara cualquier valor no vacío con umbral de conjunto de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="7e30d-234">Si se supera hello ' >' de condición, Hola trabajo devuelva un **alarma** evento que indica que ese umbral Hola se supera y ofrecen dispositivo hello, valor y los valores de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="7e30d-235">Este trabajo utiliza Hola siguientes mensajes de telemetría de tooidentify de definición de consulta que deben desencadenar una alarma:</span><span class="sxs-lookup"><span data-stu-id="7e30d-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="7e30d-236">Hola trabajo envía su centro de eventos de salida tooan para su posterior procesamiento y evita que los detalles de cada alerta tooblob almacenamiento donde portal de solución de hello puede leer la información de alertas de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="7e30d-237">**Tarea 3: Telemetría** funciona en flujo de telemetría de dispositivo entrante de Hola de dos maneras.</span><span class="sxs-lookup"><span data-stu-id="7e30d-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="7e30d-238">Hola envía primero todos los mensajes de telemetría Hola dispositivos toopersistent almacenamiento de blobs para almacenamiento a largo plazo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="7e30d-239">Hola segundo calcula humedad promedio, mínimo y máximo valores a través de una ventana deslizante de cinco minutos y envía este almacenamiento de datos tooblob.</span><span class="sxs-lookup"><span data-stu-id="7e30d-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="7e30d-240">portal de solución de Hello lee los datos de telemetría de Hola de gráficos de Hola de toopopulate de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="7e30d-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="7e30d-241">Este trabajo utiliza Hola después de la definición de la consulta:</span><span class="sxs-lookup"><span data-stu-id="7e30d-241">This job uses hello following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="7e30d-242">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="7e30d-242">Event Hubs</span></span>

<span data-ttu-id="7e30d-243">Hola **información del dispositivo** y **reglas** trabajos ASA muestran su datos tooEvent concentradores tooreliably al día en toohello **procesador de eventos** ejecutando Hola trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="7e30d-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="7e30d-244">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="7e30d-244">Azure storage</span></span>

<span data-ttu-id="7e30d-245">solución de Hello utiliza toopersist de almacenamiento de blobs de Azure todos los datos de telemetría resumido y sin formato de Hola desde dispositivos de hello en soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="7e30d-246">portal de Hello lee los datos de telemetría de Hola de gráficos de Hola de toopopulate de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="7e30d-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="7e30d-247">toodisplay alertas, portal de solución de hello lee Hola datos desde almacenamiento de blobs que registra cuando Hola de telemetría valores superados configura valores de umbral.</span><span class="sxs-lookup"><span data-stu-id="7e30d-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="7e30d-248">solución de Hello también utiliza valores blob almacenamiento toorecord Hola umbral establecido en el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="7e30d-249">Trabajos web</span><span class="sxs-lookup"><span data-stu-id="7e30d-249">WebJobs</span></span>

<span data-ttu-id="7e30d-250">Además simuladores de dispositivos de toohosting hello, Hola trabajos Web de solución de hello también Hola host **procesador de eventos** ejecutando en un trabajo Web de Azure que controla las respuestas de comando.</span><span class="sxs-lookup"><span data-stu-id="7e30d-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="7e30d-251">Usa el comando respuesta mensajes tooupdate Hola dispositivo comando Historial (almacenado en la base de datos de base de datos de Cosmos hello).</span><span class="sxs-lookup"><span data-stu-id="7e30d-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="7e30d-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7e30d-252">Cosmos DB</span></span>

<span data-ttu-id="7e30d-253">solución de Hello utiliza una base de datos de Cosmos base de datos toostore información sobre las Hola dispositivos toohello conectado solución.</span><span class="sxs-lookup"><span data-stu-id="7e30d-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="7e30d-254">Esta información incluye el historial de Hola de comandos enviados toodevices desde el portal de solución de Hola y de los métodos invocados desde el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="7e30d-255">Portal de solución</span><span class="sxs-lookup"><span data-stu-id="7e30d-255">Solution portal</span></span>

<span data-ttu-id="7e30d-256">portal de solución de Hello es una aplicación web que se implementa como parte de la solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="7e30d-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="7e30d-257">páginas de clave de Hello en el portal de solución de hello son lista de dispositivos de Hola y el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="7e30d-258">Panel</span><span class="sxs-lookup"><span data-stu-id="7e30d-258">Dashboard</span></span>

<span data-ttu-id="7e30d-259">Esta página de aplicación web de hello usa controles de javascript de Power BI (consulte [repositorio de PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals)) los datos de telemetría de hello toovisualize desde dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="7e30d-260">solución de Hello utiliza Hola ASA telemetría trabajo toowrite Hola telemetría tooblob almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="7e30d-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="7e30d-261">Lista de dispositivos</span><span class="sxs-lookup"><span data-stu-id="7e30d-261">Device list</span></span>

<span data-ttu-id="7e30d-262">Desde esta página en el portal de solución de hello hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e30d-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="7e30d-263">Aprovisionar un dispositivo nuevo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-263">Provision a new device.</span></span> <span data-ttu-id="7e30d-264">Esta acción establece el Id. de dispositivo único hello y genera la clave de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e30d-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="7e30d-265">Escribe información acerca de Hola Hola de tooboth de dispositivo del registro de identidad de centro de IoT y base de datos de base de datos de Cosmos de hello específica de la solución.</span><span class="sxs-lookup"><span data-stu-id="7e30d-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="7e30d-266">Administrar las propiedades del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-266">Manage device properties.</span></span> <span data-ttu-id="7e30d-267">Esta acción incluye las propiedades de visualización existentes y la actualización con nuevas propiedades.</span><span class="sxs-lookup"><span data-stu-id="7e30d-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="7e30d-268">Enviar dispositivo tooa de comandos.</span><span class="sxs-lookup"><span data-stu-id="7e30d-268">Send commands tooa device.</span></span>
* <span data-ttu-id="7e30d-269">Ver el historial del comando de Hola para un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e30d-269">View hello command history for a device.</span></span>
* <span data-ttu-id="7e30d-270">Habilitar y deshabilitar dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7e30d-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e30d-271">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7e30d-271">Next steps</span></span>

<span data-ttu-id="7e30d-272">Hello entradas de blog de TechNet siguientes proporcionan más detalles sobre Hola remoto solución preconfigurada de supervisión:</span><span class="sxs-lookup"><span data-stu-id="7e30d-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="7e30d-273">Supervisión remota de IoT Suite - bajo el paraguas de Hola:</span><span class="sxs-lookup"><span data-stu-id="7e30d-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="7e30d-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (Conjunto de aplicaciones de IoT, Supervisión remota: Incorporación de dispositivos activos y simulados)</span><span class="sxs-lookup"><span data-stu-id="7e30d-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="7e30d-275">Puede seguir introducción con Suite IoT leyendo Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="7e30d-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="7e30d-276">[Conectar su toohello de dispositivo remoto solución preconfigurada de supervisión][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="7e30d-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="7e30d-277">[Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="7e30d-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
