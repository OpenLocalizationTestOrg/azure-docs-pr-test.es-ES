---
title: soluciones preconfiguradas de aaaCustomizing | Documentos de Microsoft
description: "Proporciona instrucciones sobre cómo toocustomize hello Azure IoT conjunto había preconfigurado soluciones."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="decf6-103">Personalizar una solución preconfigurada</span><span class="sxs-lookup"><span data-stu-id="decf6-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="decf6-104">soluciones de Hello preconfigurado proporcionadas con hello Azure IoT Suite muestran los servicios de hello en hello suite trabajar juntos toodeliver una solución end-to-end.</span><span class="sxs-lookup"><span data-stu-id="decf6-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="decf6-105">Desde este punto de partida, hay varios lugares en los que puede ampliar y personalizar soluciones de Hola para escenarios concretos.</span><span class="sxs-lookup"><span data-stu-id="decf6-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="decf6-106">Hola siguientes secciones describe estos puntos de personalización comunes.</span><span class="sxs-lookup"><span data-stu-id="decf6-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="decf6-107">Buscar código fuente de Hola</span><span class="sxs-lookup"><span data-stu-id="decf6-107">Find hello source code</span></span>

<span data-ttu-id="decf6-108">código fuente de Hola para soluciones de hello preconfigurado está disponible en GitHub en hello después repositorios:</span><span class="sxs-lookup"><span data-stu-id="decf6-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="decf6-109">Supervisión remota: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="decf6-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="decf6-110">Mantenimiento predictivo: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="decf6-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="decf6-111">Fábrica conectada: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="decf6-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="decf6-112">código fuente de Hola para soluciones de hello preconfigurado es proporciona recomendaciones y los patrones de hello toodemonstrate utilizan funcionalidad de tooimplement Hola-to-end de una solución de IoT con conjunto de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="decf6-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="decf6-113">Puede encontrar más información sobre cómo toobuild e implementar soluciones de hello en repositorios de GitHub Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="decf6-114">Cambiar las reglas de hello preconfigurado</span><span class="sxs-lookup"><span data-stu-id="decf6-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="decf6-115">Hello solución de supervisión remota incluye tres [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) trabajos toohandle información del dispositivo, telemetría y lógica de reglas en soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="decf6-116">Hello tres transmitir trabajos de análisis y su sintaxis se describen con más detalle en hello [supervisión remota preconfigurado tutorial de la solución](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="decf6-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="decf6-117">Puede editar estos trabajos directamente tooalter Hola lógica o agregar lógica específica tooyour escenario.</span><span class="sxs-lookup"><span data-stu-id="decf6-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="decf6-118">Puede encontrar Hola trabajos de análisis de transmisiones como sigue:</span><span class="sxs-lookup"><span data-stu-id="decf6-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="decf6-119">Vaya demasiado[portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="decf6-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="decf6-120">Navegar por grupo de recursos de toohello con el mismo nombre que la solución de IoT de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="decf6-121">Seleccione el trabajo de análisis de transmisiones de Azure de hello le gustaría toomodify.</span><span class="sxs-lookup"><span data-stu-id="decf6-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="decf6-122">Detención del trabajo de hello seleccionando **detener** en conjunto Hola de comandos.</span><span class="sxs-lookup"><span data-stu-id="decf6-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="decf6-123">Editar salidas, consultas y las entradas de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="decf6-124">Una modificación sencilla es consultar toochange Hola Hola **reglas** trabajo toouse una **"<"** en lugar de un **">"**.</span><span class="sxs-lookup"><span data-stu-id="decf6-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="decf6-125">portal de solución de Hello sigue mostrando **">"** al editar una regla, pero tenga en cuenta cómo se voltea el comportamiento de hello debido a cambios toohello Hola subyacente de trabajo.</span><span class="sxs-lookup"><span data-stu-id="decf6-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="decf6-126">Iniciar el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="decf6-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="decf6-127">panel de supervisión remoto Hello depende de datos específicos, modificar trabajos Hola puede causar Hola panel toofail.</span><span class="sxs-lookup"><span data-stu-id="decf6-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="decf6-128">Adición de reglas propias</span><span class="sxs-lookup"><span data-stu-id="decf6-128">Add your own rules</span></span>

<span data-ttu-id="decf6-129">Además toochanging Hola había preconfigurado trabajos de análisis de transmisiones de Azure, puede usar los nuevos trabajos de hello tooadd portal Azure o agregar nuevos trabajos de tooexisting de las consultas.</span><span class="sxs-lookup"><span data-stu-id="decf6-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="decf6-130">Personalización de dispositivos</span><span class="sxs-lookup"><span data-stu-id="decf6-130">Customize devices</span></span>

<span data-ttu-id="decf6-131">Una de las actividades de extensión más comunes de Hola está trabajando con el escenario de tooyour específicos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="decf6-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="decf6-132">Existen varios métodos para trabajar con dispositivos.</span><span class="sxs-lookup"><span data-stu-id="decf6-132">There are several methods for working with devices.</span></span> <span data-ttu-id="decf6-133">Estos métodos incluyen modificar un toomatch dispositivo simulado su escenario, o mediante hello [SDK de dispositivos de IoT] [ IoT Device SDK] tooconnect la solución de toohello de dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="decf6-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="decf6-134">Para un dispositivo de tooadding guía paso a paso, vea hello [Iot Suite conectar dispositivos](iot-suite-connecting-devices.md) hello y artículo [ejemplo de SDK de C de supervisión remota](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="decf6-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="decf6-135">Este ejemplo es toowork diseñada con hello solución preconfigurada de supervisión remoto.</span><span class="sxs-lookup"><span data-stu-id="decf6-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="decf6-136">Creación de dispositivo simulado propio</span><span class="sxs-lookup"><span data-stu-id="decf6-136">Create your own simulated device</span></span>

<span data-ttu-id="decf6-137">Incluido en hello [código fuente de solución de supervisión remota](https://github.com/Azure/azure-iot-remote-monitoring), es un simulador. NET.</span><span class="sxs-lookup"><span data-stu-id="decf6-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="decf6-138">Este simulador es hello uno aprovisionado como parte de la solución de Hola y se puede modificar toosend distintos metadatos, telemetría y responder métodos y comandos de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="decf6-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="decf6-139">simulador preconfigurada de Hola Hola solución preconfigurada de supervisión remota simula un dispositivo de refrigeración que emite la telemetría de temperatura y humedad.</span><span class="sxs-lookup"><span data-stu-id="decf6-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="decf6-140">Puede modificar simulador Hola Hola [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) proyecto cuando se ha bifurcado repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="decf6-141">Ubicaciones disponibles para dispositivos simulados</span><span class="sxs-lookup"><span data-stu-id="decf6-141">Available locations for simulated devices</span></span>

<span data-ttu-id="decf6-142">conjunto de ubicaciones de Hello predeterminado es en Seattle y Redmond, Washington, Estados Unidos de América.</span><span class="sxs-lookup"><span data-stu-id="decf6-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="decf6-143">Puede cambiar estas ubicaciones en [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="decf6-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="decf6-144">Agregar un simulador de toohello del controlador de actualización de propiedad deseada</span><span class="sxs-lookup"><span data-stu-id="decf6-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="decf6-145">Puede establecer un valor para una propiedad deseada para un dispositivo en el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="decf6-146">Es responsabilidad de Hola de solicitud de cambio de propiedad de Hola Hola dispositivo toohandle al dispositivo de hello recupera el valor de la propiedad de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="decf6-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="decf6-147">compatibilidad con tooadd un cambio de valor de propiedad a través de una propiedad deseada, deberá tooadd un simulador de toohello de controlador.</span><span class="sxs-lookup"><span data-stu-id="decf6-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="decf6-148">simulador de Hello contiene controladores para hello **SetPointTemp** y **TelemetryInterval** deseado de propiedades que se pueden actualizar estableciendo valores en el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="decf6-149">Hello en el ejemplo siguiente se muestra controlador Hola Hola **SetPointTemp** deseado propiedad Hola **CoolerDevice** clase:</span><span class="sxs-lookup"><span data-stu-id="decf6-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="decf6-150">Este método actualiza el punto de telemetría Hola informes hello temperatura y, a continuación, cambian atrás tooIoT concentrador estableciendo una propiedad notificada.</span><span class="sxs-lookup"><span data-stu-id="decf6-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="decf6-151">Puede agregar sus propios controladores para sus propias propiedades mediante el siguiente patrón de hello en el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="decf6-152">Debe enlazar también el controlador de hello propiedad deseada toohello tal y como se muestra en el siguiente ejemplo de Hola de hello **CoolerDevice** constructor:</span><span class="sxs-lookup"><span data-stu-id="decf6-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="decf6-153">Tenga en cuenta que **SetPointTempPropertyName** es una constante definida como "Config.SetPointTemp".</span><span class="sxs-lookup"><span data-stu-id="decf6-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="decf6-154">Agregar compatibilidad con un simulador de toohello método nuevo</span><span class="sxs-lookup"><span data-stu-id="decf6-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="decf6-155">Puede personalizar Hola simulador tooadd compatibilidad con un nuevo [método (directo)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="decf6-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="decf6-156">Se necesitan dos pasos principales:</span><span class="sxs-lookup"><span data-stu-id="decf6-156">There are two key steps required:</span></span>

- <span data-ttu-id="decf6-157">simulador Hola debe notificar al centro de IoT de hello en soluciones de hello preconfigurado con los detalles del método hello.</span><span class="sxs-lookup"><span data-stu-id="decf6-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="decf6-158">simulador de Hello debe incluir la llamada al método de código toohandle Hola al invocarlo desde hello **detalles del dispositivo** panel en el Explorador de soluciones de Hola o a través de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="decf6-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="decf6-159">Hello supervisión remota preconfigurado solución usa *notificado propiedades* toosend detalles del concentrador de tooIoT métodos admitidos.</span><span class="sxs-lookup"><span data-stu-id="decf6-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="decf6-160">back-end de soluciones de Hello mantiene una lista de todos los métodos de hello admitidos por cada dispositivo junto con un historial de las invocaciones de método.</span><span class="sxs-lookup"><span data-stu-id="decf6-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="decf6-161">Puede ver esta información acerca de los dispositivos e invocar métodos en el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="decf6-162">Centro de IoT de toonotify Hola que un dispositivo es compatible con un método, dispositivo Hola debe agregar detalles de hello método toohello **SupportedMethods** nodo Hola notificado propiedades:</span><span class="sxs-lookup"><span data-stu-id="decf6-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="decf6-163">firma del método Hello tiene Hola siguiendo el formato: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="decf6-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="decf6-164">Por ejemplo, toospecify hello **InitiateFirmwareUpdate** método espera un parámetro de cadena denominado **FwPackageURI**, usar hello después de la firma del método:</span><span class="sxs-lookup"><span data-stu-id="decf6-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="decf6-165">Para obtener una lista de tipos de parámetro admitidos, vea hello **CommandTypes** clase en el proyecto de infraestructura de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="decf6-166">toodelete un método, establezca la firma del método hello demasiado`null` Hola notificado propiedades.</span><span class="sxs-lookup"><span data-stu-id="decf6-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="decf6-167">Hello back-end de soluciones sólo actualiza la información sobre los métodos admitidos cuando recibe un *información del dispositivo* mensaje de Hola dispositivo.</span><span class="sxs-lookup"><span data-stu-id="decf6-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="decf6-168">Hola siguiente código de ejemplo de Hola **SampleDeviceFactory** clase Hola comunes de proyectos se muestra cómo tooadd una lista de toohello método de **SupportedMethods** Hola notificado propiedad enviada por hello dispositivo:</span><span class="sxs-lookup"><span data-stu-id="decf6-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="decf6-169">Este fragmento de código agrega detalles de hello **InitiateFirmwareUpdate** método incluidos toodisplay de texto en el portal de solución de Hola y los detalles del programa Hola a los parámetros de método necesarios.</span><span class="sxs-lookup"><span data-stu-id="decf6-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="decf6-170">simulador de Hello envía propiedades notificados, incluida la lista de Hola de métodos admitidos, tooIoT concentrador cuando se inicia el simulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="decf6-171">Agregar un código de controlador toohello simulador para cada método que admite.</span><span class="sxs-lookup"><span data-stu-id="decf6-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="decf6-172">Puede ver los controladores existentes Hola Hola **CoolerDevice** clase hello Simulator.WebJob proyecto.</span><span class="sxs-lookup"><span data-stu-id="decf6-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="decf6-173">Hello en el ejemplo siguiente se muestra el controlador de hello para **InitiateFirmwareUpdate** método:</span><span class="sxs-lookup"><span data-stu-id="decf6-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="decf6-174">Los nombres de controlador de método deben empezar por `On` seguido Hola nombre del método hello.</span><span class="sxs-lookup"><span data-stu-id="decf6-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="decf6-175">Hola **methodRequest** parámetro contiene cualquier parámetro pasado con la invocación del método hello de hello solución back-end.</span><span class="sxs-lookup"><span data-stu-id="decf6-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="decf6-176">valor devuelto Hello debe ser una de tipo **tarea&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="decf6-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="decf6-177">Hola **BuildMethodResponse** método de utilidad le ayudará a crear el valor devuelto de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="decf6-178">Dentro de hello método controlador, se puede realizar:</span><span class="sxs-lookup"><span data-stu-id="decf6-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="decf6-179">Iniciar una tarea asincrónica.</span><span class="sxs-lookup"><span data-stu-id="decf6-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="decf6-180">Recuperar propiedades deseadas de hello *gemelas dispositivo* en Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="decf6-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="decf6-181">Actualizar una única propiedad incluida con hello **SetReportedPropertyAsync** método Hola **CoolerDevice** clase.</span><span class="sxs-lookup"><span data-stu-id="decf6-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="decf6-182">Actualizar varias propiedades notificados mediante la creación de un **TwinCollection** hello que realiza la llamada y la instancia **Transport.UpdateReportedPropertiesAsync** método.</span><span class="sxs-lookup"><span data-stu-id="decf6-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="decf6-183">Hello ejemplo de actualización de firmware anterior realiza Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="decf6-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="decf6-184">Comprobaciones de hello dispositivo es solicitud de actualización de firmware de tooaccept capaz de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="decf6-185">Inicia la operación de actualización de firmware de Hola de forma asincrónica y restablece la telemetría de hello cuando se completa la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="decf6-186">Inmediatamente devuelve Hola "FirmwareUpdate aceptado" se aceptó la solicitud de Hola de tooindicate de mensaje por dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="decf6-187">Creación y uso de dispositivos propios (físicos)</span><span class="sxs-lookup"><span data-stu-id="decf6-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="decf6-188">Hola [SDK de Azure IoT](https://github.com/Azure/azure-iot-sdks) proporcionan bibliotecas para conectar numerosos tipos de dispositivo (idiomas y sistemas operativos) en soluciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="decf6-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="decf6-189">Modificación de los límites de panel</span><span class="sxs-lookup"><span data-stu-id="decf6-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="decf6-190">Número de dispositivos que se muestran en la lista desplegable del panel</span><span class="sxs-lookup"><span data-stu-id="decf6-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="decf6-191">Hola predeterminado es 200.</span><span class="sxs-lookup"><span data-stu-id="decf6-191">hello default is 200.</span></span> <span data-ttu-id="decf6-192">Puede cambiar este número en [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="decf6-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="decf6-193">Número de PIN toodisplay en control de mapa de Bing</span><span class="sxs-lookup"><span data-stu-id="decf6-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="decf6-194">Hola predeterminado es 200.</span><span class="sxs-lookup"><span data-stu-id="decf6-194">hello default is 200.</span></span> <span data-ttu-id="decf6-195">Puede cambiar este número en [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="decf6-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="decf6-196">Periodo del gráfico de telemetría</span><span class="sxs-lookup"><span data-stu-id="decf6-196">Time period of telemetry graph</span></span>

<span data-ttu-id="decf6-197">valor predeterminado de Hello es 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="decf6-197">hello default is 10 minutes.</span></span> <span data-ttu-id="decf6-198">Puede cambiar este valor en [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="decf6-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="decf6-199">Configuración manual de los roles de aplicación</span><span class="sxs-lookup"><span data-stu-id="decf6-199">Manually set up application roles</span></span>

<span data-ttu-id="decf6-200">Hello siguiente procedimiento describe cómo tooadd **administración** y **ReadOnly** tooa de roles de aplicación configurado previamente la solución.</span><span class="sxs-lookup"><span data-stu-id="decf6-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="decf6-201">Tenga en cuenta que las soluciones preconfiguradas aprovisionadas desde sitios de hello azureiotsuite.com ya incluyen hello **administración** y **ReadOnly** roles.</span><span class="sxs-lookup"><span data-stu-id="decf6-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="decf6-202">Los miembros de hello **ReadOnly** rol puede ver la lista de dispositivos de Hola y el panel de hello, pero no se permiten dispositivos tooadd, atributos de dispositivo de cambio o comandos de envío.</span><span class="sxs-lookup"><span data-stu-id="decf6-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="decf6-203">Los miembros de hello **administración** rol tiene funcionalidad de acceso completo tooall hello en solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="decf6-204">Vaya toohello [portal de Azure clásico][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="decf6-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="decf6-205">Seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="decf6-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="decf6-206">Haga clic en nombre de hello del inquilino de AAD de Hola que usó al aprovisionar la solución.</span><span class="sxs-lookup"><span data-stu-id="decf6-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="decf6-207">Haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="decf6-207">Click **Applications**.</span></span>
5. <span data-ttu-id="decf6-208">Haga clic en el nombre de Hola de aplicación Hola que coincida con el nombre de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="decf6-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="decf6-209">Si no ve la aplicación en la lista de hello, seleccione **aplicaciones tiene mi compañía** en hello **mostrar** lista desplegable y haga clic en Hola marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="decf6-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="decf6-210">En la parte inferior de Hola de página de hello, haga clic en **administrar manifiesto** y, a continuación, **descargar manifiesto**.</span><span class="sxs-lookup"><span data-stu-id="decf6-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="decf6-211">Este procedimiento descarga un equipo local de .json archivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="decf6-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="decf6-212">Abra este archivo para editarlo en el editor de texto que quiera.</span><span class="sxs-lookup"><span data-stu-id="decf6-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="decf6-213">En hello tercera línea del archivo .json de hello, puede ver:</span><span class="sxs-lookup"><span data-stu-id="decf6-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="decf6-214">Reemplace esta línea con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="decf6-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="decf6-215">Guarde el archivo de .json actualizada de hello (puede sobrescribir archivos existentes de hello).</span><span class="sxs-lookup"><span data-stu-id="decf6-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="decf6-216">Hola portal de Azure clásico, en parte inferior de Hola de página de hello, seleccione **administrar manifiesto** , a continuación, **cargar manifiesto** archivo .json tooupload Hola que guardó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="decf6-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="decf6-217">Ya has agregado hello **administración** y **ReadOnly** aplicación tooyour de roles.</span><span class="sxs-lookup"><span data-stu-id="decf6-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="decf6-218">tooassign uno de estos usuarios tooa de roles en el directorio, consulte [permisos en el sitio de hello azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="decf6-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="decf6-219">Comentarios</span><span class="sxs-lookup"><span data-stu-id="decf6-219">Feedback</span></span>

<span data-ttu-id="decf6-220">¿Tiene una personalización que le gustaría toosee cubierta por este documento?</span><span class="sxs-lookup"><span data-stu-id="decf6-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="decf6-221">Agregar sugerencias sobre características demasiado[User Voice](https://feedback.azure.com/forums/321918-azure-iot), o un comentario en este artículo.</span><span class="sxs-lookup"><span data-stu-id="decf6-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="decf6-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="decf6-222">Next steps</span></span>

<span data-ttu-id="decf6-223">toolearn más información acerca de opciones de Hola para personalizar soluciones de hello preconfigurado, consulte:</span><span class="sxs-lookup"><span data-stu-id="decf6-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="decf6-224">[Solución de Azure de supervisión remota de conjunto de IoT preconfigurado tooyour de aplicación lógica de conexión][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="decf6-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="decf6-225">[Use la telemetría dinámica con hello solución preconfigurada de supervisión remota][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="decf6-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="decf6-226">[Metadatos de información de dispositivo en hello solución preconfigurada de supervisión remota][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="decf6-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="decf6-227">[Personalizar cómo Hola conectado generador solución muestra los datos de los servidores de OPC UA][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="decf6-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md