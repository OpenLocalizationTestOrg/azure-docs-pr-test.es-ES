---
title: "Personalizar una solución preconfigurada | Microsoft Docs"
description: "Proporciona directrices sobre la personalización de ñas soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure."
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
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="402b9-103">Personalizar una solución preconfigurada</span><span class="sxs-lookup"><span data-stu-id="402b9-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="402b9-104">Las soluciones preconfiguradas proporcionadas con el conjunto de aplicaciones de IoT de Azure muestran los servicios del conjunto de aplicaciones que funcionan juntos para proporcionar una solución completa.</span><span class="sxs-lookup"><span data-stu-id="402b9-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="402b9-105">Desde este punto de partida, existen varios lugares donde puede ampliar y personalizar la solución para cada situación específica.</span><span class="sxs-lookup"><span data-stu-id="402b9-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="402b9-106">Las secciones siguientes describen estos puntos de personalización comunes.</span><span class="sxs-lookup"><span data-stu-id="402b9-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="402b9-107">Ubicación del código fuente</span><span class="sxs-lookup"><span data-stu-id="402b9-107">Find the source code</span></span>

<span data-ttu-id="402b9-108">El código fuente de su solución preconfigurada está disponible en Github en los repositorios siguientes:</span><span class="sxs-lookup"><span data-stu-id="402b9-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="402b9-109">Supervisión remota: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="402b9-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="402b9-110">Mantenimiento predictivo: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="402b9-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="402b9-111">Fábrica conectada: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="402b9-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="402b9-112">El código fuente de las soluciones preconfiguradas se proporciona para demostrar los patrones y los procedimientos que se usan para implementar la funcionalidad de extremo a extremo de una solución de IoT mediante el conjunto de aplicaciones de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="402b9-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="402b9-113">Puede encontrar más información sobre cómo crear e implementar las soluciones en los repositorios de GitHub.</span><span class="sxs-lookup"><span data-stu-id="402b9-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="402b9-114">Cambio de las reglas previamente configuradas</span><span class="sxs-lookup"><span data-stu-id="402b9-114">Change the preconfigured rules</span></span>

<span data-ttu-id="402b9-115">La solución de supervisión remota incluye tres trabajos de [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) para controlar la información del dispositivo, la telemetría y la lógica de reglas de la solución.</span><span class="sxs-lookup"><span data-stu-id="402b9-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="402b9-116">Los tres trabajos de Stream Analytics y su sintaxis se describen detalladamente en el [Tutorial de la solución preconfigurada de supervisión remota](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="402b9-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="402b9-117">Puede editar directamente estos trabajos y modificar la lógica, o agregar lógica específica a su escenario.</span><span class="sxs-lookup"><span data-stu-id="402b9-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="402b9-118">Para encontrar los trabajos de Análisis de transmisiones, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="402b9-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="402b9-119">Vaya al [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="402b9-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="402b9-120">Vaya al grupo de recursos con el mismo nombre que la solución de IoT.</span><span class="sxs-lookup"><span data-stu-id="402b9-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="402b9-121">Seleccione el trabajo de Análisis de transmisiones de Azure que desea modificar.</span><span class="sxs-lookup"><span data-stu-id="402b9-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="402b9-122">Detenga el trabajo seleccionando **Detener** en el conjunto de comandos.</span><span class="sxs-lookup"><span data-stu-id="402b9-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="402b9-123">Edite las entradas, la consulta y las salidas.</span><span class="sxs-lookup"><span data-stu-id="402b9-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="402b9-124">Una modificación sencilla consiste en cambiar la consulta para que el trabajo **Reglas** use **"<"** en lugar de **">"**.</span><span class="sxs-lookup"><span data-stu-id="402b9-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="402b9-125">El portal de la solución sigue mostrando **">"** al editar una regla, pero observe cómo varía el comportamiento debido al cambio en el trabajo subyacente.</span><span class="sxs-lookup"><span data-stu-id="402b9-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="402b9-126">Inicio del trabajo</span><span class="sxs-lookup"><span data-stu-id="402b9-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="402b9-127">El panel de supervisión remota depende de datos específicos, así que la modificación de los trabajos puede provocar errores del panel.</span><span class="sxs-lookup"><span data-stu-id="402b9-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="402b9-128">Adición de reglas propias</span><span class="sxs-lookup"><span data-stu-id="402b9-128">Add your own rules</span></span>

<span data-ttu-id="402b9-129">Además de cambiar los trabajos de Análisis de transmisiones de Azure preconfigurados, puede usar el Portal de Azure para agregar nuevos trabajos o nuevas consultas a los trabajos existentes.</span><span class="sxs-lookup"><span data-stu-id="402b9-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="402b9-130">Personalización de dispositivos</span><span class="sxs-lookup"><span data-stu-id="402b9-130">Customize devices</span></span>

<span data-ttu-id="402b9-131">Una de las actividades de extensión más comunes es trabajar con dispositivos específicos de su escenario.</span><span class="sxs-lookup"><span data-stu-id="402b9-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="402b9-132">Existen varios métodos para trabajar con dispositivos.</span><span class="sxs-lookup"><span data-stu-id="402b9-132">There are several methods for working with devices.</span></span> <span data-ttu-id="402b9-133">Entre estos se incluye la modificación de un dispositivo simulado para adaptarlo a su situación, o bien el uso del [SDK de dispositivo de IoT][IoT Device SDK] para conectar el dispositivo físico a la solución.</span><span class="sxs-lookup"><span data-stu-id="402b9-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="402b9-134">Para obtener una guía paso a paso sobre cómo agregar dispositivos, consulte el artículo [Dispositivos de conexión del conjunto de aplicaciones de IoT](iot-suite-connecting-devices.md) y el [ejemplo del SDK de C de supervisión remota](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="402b9-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="402b9-135">Este ejemplo está diseñado para funcionar con la solución de supervisión remota preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="402b9-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="402b9-136">Creación de dispositivo simulado propio</span><span class="sxs-lookup"><span data-stu-id="402b9-136">Create your own simulated device</span></span>

<span data-ttu-id="402b9-137">El [código fuente de la solución de supervisión remota](https://github.com/Azure/azure-iot-remote-monitoring) incluye un simulador. NET.</span><span class="sxs-lookup"><span data-stu-id="402b9-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="402b9-138">Este simulador es el que se aprovisiona como parte de la solución y puede modificarlo para enviar distintos metadatos, telemetría y responder a distintos comandos y métodos.</span><span class="sxs-lookup"><span data-stu-id="402b9-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="402b9-139">El simulador preconfigurado en la solución preconfigurada de supervisión remota imita un dispositivo de refrigeración que emite la telemetría de temperatura y humedad.</span><span class="sxs-lookup"><span data-stu-id="402b9-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="402b9-140">Puede modificar el simulador en el proyecto [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) cuando haya bifurcado el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="402b9-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="402b9-141">Ubicaciones disponibles para dispositivos simulados</span><span class="sxs-lookup"><span data-stu-id="402b9-141">Available locations for simulated devices</span></span>

<span data-ttu-id="402b9-142">El conjunto predeterminado de ubicaciones es Seattle/Redmond, Washington (Estados Unidos de América).</span><span class="sxs-lookup"><span data-stu-id="402b9-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="402b9-143">Puede cambiar estas ubicaciones en [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="402b9-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="402b9-144">Adición de un controlador de actualización de propiedad deseada al simulador</span><span class="sxs-lookup"><span data-stu-id="402b9-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="402b9-145">Puede establecer un valor para una propiedad deseada de un dispositivo en el portal de la solución.</span><span class="sxs-lookup"><span data-stu-id="402b9-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="402b9-146">Es responsabilidad del dispositivo controlar la solicitud de cambio de la propiedad cuando el dispositivo recupera el valor de la propiedad deseada.</span><span class="sxs-lookup"><span data-stu-id="402b9-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="402b9-147">Para agregar compatibilidad para un cambio del valor de propiedad mediante una propiedad deseada, debe agregar un controlador al simulador.</span><span class="sxs-lookup"><span data-stu-id="402b9-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="402b9-148">El simulador contiene controladores para las propiedades **SetPointTemp** y **TelemetryInterval** que puede actualizar mediante el establecimiento de los valores deseados en el portal de soluciones.</span><span class="sxs-lookup"><span data-stu-id="402b9-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="402b9-149">En el ejemplo siguiente se muestra el controlador para la propiedad deseada **SetPointTemp** de la clase **CoolerDevice**:</span><span class="sxs-lookup"><span data-stu-id="402b9-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="402b9-150">Este método permite actualizar la temperatura de telemetría y, a continuación, informa del cambio a IoT Hub estableciendo una propiedad notificada.</span><span class="sxs-lookup"><span data-stu-id="402b9-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="402b9-151">Puede agregar sus propios controladores a sus propias propiedades siguiendo el patrón del ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="402b9-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="402b9-152">También debe enlazar la propiedad deseada al controlador tal y como se muestra en el siguiente ejemplo del constructor **CoolerDevice**:</span><span class="sxs-lookup"><span data-stu-id="402b9-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="402b9-153">Tenga en cuenta que **SetPointTempPropertyName** es una constante definida como "Config.SetPointTemp".</span><span class="sxs-lookup"><span data-stu-id="402b9-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="402b9-154">Adición de compatibilidad con un nuevo método al simulador</span><span class="sxs-lookup"><span data-stu-id="402b9-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="402b9-155">Puede personalizar el simulador para agregar compatibilidad con un nuevo [método (método directo)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="402b9-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="402b9-156">Se necesitan dos pasos principales:</span><span class="sxs-lookup"><span data-stu-id="402b9-156">There are two key steps required:</span></span>

- <span data-ttu-id="402b9-157">El simulador debe notificar a la instancia de IoT Hub de la solución preconfigurada los detalles del método.</span><span class="sxs-lookup"><span data-stu-id="402b9-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="402b9-158">El simulador debe incluir código para controlar la llamada al método cuando se invoca desde el panel **Detalles del dispositivo** en el Explorador de soluciones o a través de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="402b9-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="402b9-159">La solución preconfigurada de supervisión remota usa *propiedades notificadas* para enviar los detalles sobre los métodos admitidos a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="402b9-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="402b9-160">El back-end de soluciones mantiene una lista de todos los métodos admitidos por cada dispositivo junto con un historial de las invocaciones de cada método.</span><span class="sxs-lookup"><span data-stu-id="402b9-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="402b9-161">Puede ver esta información acerca de los dispositivos e invocar métodos en el portal de la solución.</span><span class="sxs-lookup"><span data-stu-id="402b9-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="402b9-162">Para notificar a IoT Hub que un dispositivo es compatible con un método, el dispositivo debe agregar los detalles del método al nodo **SupportedMethods** en las propiedades notificadas:</span><span class="sxs-lookup"><span data-stu-id="402b9-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="402b9-163">La firma del método tiene el formato siguiente: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="402b9-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="402b9-164">Por ejemplo, para especificar que el método **InitiateFirmwareUpdate** espera un parámetro de cadena denominado **FwPackageURI**, use la siguiente firma de método:</span><span class="sxs-lookup"><span data-stu-id="402b9-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="402b9-165">Para obtener una lista de los tipos de parámetro admitidos, consulte la clase **CommandTypes** del proyecto Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="402b9-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="402b9-166">Para eliminar un método, establezca la firma del método en `null` en las propiedades notificadas.</span><span class="sxs-lookup"><span data-stu-id="402b9-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="402b9-167">El back-end de soluciones solo actualiza información acerca de los métodos compatibles cuando recibe un mensaje de *información del dispositivo* desde este.</span><span class="sxs-lookup"><span data-stu-id="402b9-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="402b9-168">El siguiente ejemplo de código de la clase **SampleDeviceFactory** del proyecto Common muestra cómo agregar un método a la lista de **SupportedMethods** en las propiedades notificadas enviadas por el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="402b9-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="402b9-169">Este fragmento de código permite agregar los detalles del método **InitiateFirmwareUpdate**, incluido el texto para mostrar en el portal de solución, y los detalles sobre los parámetros de método necesarios.</span><span class="sxs-lookup"><span data-stu-id="402b9-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="402b9-170">Al iniciarse, el simulador envía propiedades notificadas, incluida la lista de métodos admitidos, a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="402b9-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="402b9-171">Agregue un controlador al código del simulador de cada método que admite.</span><span class="sxs-lookup"><span data-stu-id="402b9-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="402b9-172">Puede ver los controladores existentes en la clase **CoolerDevice** del proyecto Simulator.WebJob.</span><span class="sxs-lookup"><span data-stu-id="402b9-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="402b9-173">En el ejemplo siguiente se muestra el controlador del método **InitiateFirmwareUpdate**:</span><span class="sxs-lookup"><span data-stu-id="402b9-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="402b9-174">Los nombres de controlador de método deben empezar por `On` seguido del nombre del método.</span><span class="sxs-lookup"><span data-stu-id="402b9-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="402b9-175">El parámetro **methodRequest** contiene todos los parámetros pasados con la invocación del método desde el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="402b9-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="402b9-176">El valor devuelto debe ser del tipo **Task&lt;RespuestaDelMétodo&gt;**.</span><span class="sxs-lookup"><span data-stu-id="402b9-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="402b9-177">El método de la utilidad **BuildMethodResponse** le ayudará a crear el valor devuelto.</span><span class="sxs-lookup"><span data-stu-id="402b9-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="402b9-178">Dentro del controlador de método, puede:</span><span class="sxs-lookup"><span data-stu-id="402b9-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="402b9-179">Iniciar una tarea asincrónica.</span><span class="sxs-lookup"><span data-stu-id="402b9-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="402b9-180">Recuperar las propiedades deseadas desde el *dispositivo gemelo* de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="402b9-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="402b9-181">Actualizar una única propiedad notificada mediante el método **SetReportedPropertyAsync** de la clase **CoolerDevice**.</span><span class="sxs-lookup"><span data-stu-id="402b9-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="402b9-182">Actualizar varias propiedades notificadas mediante la creación de una instancia de **TwinCollection** y la llamada al método **Transport.UpdateReportedPropertiesAsync**.</span><span class="sxs-lookup"><span data-stu-id="402b9-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="402b9-183">El ejemplo de actualización de firmware anterior realiza los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="402b9-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="402b9-184">Comprueba que el dispositivo puede aceptar la solicitud de actualización de firmware.</span><span class="sxs-lookup"><span data-stu-id="402b9-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="402b9-185">Inicia la operación de actualización de firmware de forma asincrónica y restablece la telemetría cuando se completa la operación.</span><span class="sxs-lookup"><span data-stu-id="402b9-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="402b9-186">Devuelve inmediatamente el mensaje "FirmwareUpdate aceptado" para indicar que el dispositivo aceptó la solicitud.</span><span class="sxs-lookup"><span data-stu-id="402b9-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="402b9-187">Creación y uso de dispositivos propios (físicos)</span><span class="sxs-lookup"><span data-stu-id="402b9-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="402b9-188">Los [SDK de IoT de Azure](https://github.com/Azure/azure-iot-sdks) proporcionan bibliotecas que permiten conectar distintos tipos de dispositivos (lenguajes y sistemas operativos) a soluciones IoT.</span><span class="sxs-lookup"><span data-stu-id="402b9-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="402b9-189">Modificación de los límites de panel</span><span class="sxs-lookup"><span data-stu-id="402b9-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="402b9-190">Número de dispositivos que se muestran en la lista desplegable del panel</span><span class="sxs-lookup"><span data-stu-id="402b9-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="402b9-191">El valor predeterminado es 200.</span><span class="sxs-lookup"><span data-stu-id="402b9-191">The default is 200.</span></span> <span data-ttu-id="402b9-192">Puede cambiar este número en [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="402b9-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="402b9-193">Número de chinchetas que se muestran en el control de Bing Maps</span><span class="sxs-lookup"><span data-stu-id="402b9-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="402b9-194">El valor predeterminado es 200.</span><span class="sxs-lookup"><span data-stu-id="402b9-194">The default is 200.</span></span> <span data-ttu-id="402b9-195">Puede cambiar este número en [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="402b9-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="402b9-196">Periodo del gráfico de telemetría</span><span class="sxs-lookup"><span data-stu-id="402b9-196">Time period of telemetry graph</span></span>

<span data-ttu-id="402b9-197">El valor predeterminado es 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="402b9-197">The default is 10 minutes.</span></span> <span data-ttu-id="402b9-198">Puede cambiar este valor en [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="402b9-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="402b9-199">Configuración manual de los roles de aplicación</span><span class="sxs-lookup"><span data-stu-id="402b9-199">Manually set up application roles</span></span>

<span data-ttu-id="402b9-200">El siguiente procedimiento describe cómo agregar los roles de aplicación **Admin** y **ReadOnly** a una solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="402b9-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="402b9-201">Tenga en cuenta que las soluciones preconfiguradas aprovisionadas desde el sitio azureiotsuite.com ya incluyen los roles **Admin** y **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="402b9-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="402b9-202">Los miembros del rol **ReadOnly** pueden ver el panel y la lista de dispositivos, pero no tienen permiso para agregar dispositivos, cambiar atributos de dispositivo ni enviar comandos.</span><span class="sxs-lookup"><span data-stu-id="402b9-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="402b9-203">Los miembros del rol **Admin** tienen acceso total a todas las funciones de la solución.</span><span class="sxs-lookup"><span data-stu-id="402b9-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="402b9-204">Vaya al [Portal de Azure clásico][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="402b9-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="402b9-205">Seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="402b9-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="402b9-206">Haga clic en el nombre del inquilino de AAD que usó al aprovisionar la solución.</span><span class="sxs-lookup"><span data-stu-id="402b9-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="402b9-207">Haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="402b9-207">Click **Applications**.</span></span>
5. <span data-ttu-id="402b9-208">Haga clic en el nombre de la aplicación que coincida con el nombre de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="402b9-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="402b9-209">Si no ve la aplicación en la lista, seleccione **Aplicaciones que tiene mi compañía** en la lista desplegable **Mostrar** y haga clic en la marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="402b9-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="402b9-210">En la parte inferior de la página, haga clic en **Administrar manifiesto** y, luego, en **Descargar manifiesto**.</span><span class="sxs-lookup"><span data-stu-id="402b9-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="402b9-211">Este procedimiento permite descargar un archivo .json en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="402b9-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="402b9-212">Abra este archivo para editarlo en el editor de texto que quiera.</span><span class="sxs-lookup"><span data-stu-id="402b9-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="402b9-213">En la tercera línea del archivo .json, verá:</span><span class="sxs-lookup"><span data-stu-id="402b9-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="402b9-214">Reemplace esta línea por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="402b9-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="402b9-215">Guarde el archivo .json actualizado (puede sobrescribir el archivo existente).</span><span class="sxs-lookup"><span data-stu-id="402b9-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="402b9-216">En el Portal de Azure clásico, en la parte inferior de la página, seleccione **Administrar manifiesto** y, después, **Cargar manifiesto** para cargar el archivo .json que guardó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="402b9-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="402b9-217">Ahora, los roles **Admin** y **ReadOnly** ya están agregados a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="402b9-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="402b9-218">Para asignar uno de estos roles a un usuario del directorio, consulte [Permisos en el sitio azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="402b9-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="402b9-219">Comentarios</span><span class="sxs-lookup"><span data-stu-id="402b9-219">Feedback</span></span>

<span data-ttu-id="402b9-220">¿Tiene una personalización que le gustaría que se tratara en este documento?</span><span class="sxs-lookup"><span data-stu-id="402b9-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="402b9-221">Agregue las sugerencias de características a [User Voice](https://feedback.azure.com/forums/321918-azure-iot) o comente este artículo.</span><span class="sxs-lookup"><span data-stu-id="402b9-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="402b9-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="402b9-222">Next steps</span></span>

<span data-ttu-id="402b9-223">Para obtener más información sobre las opciones para personalizar las soluciones preconfiguradas, consulte estos artículos:</span><span class="sxs-lookup"><span data-stu-id="402b9-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="402b9-224">[Tutorial: Conexión de una aplicación lógica a la solución preconfigurada de supervisión remota del Conjunto de aplicaciones de IoT de Azure][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="402b9-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="402b9-225">[Uso de telemetría dinámica con la solución de supervisión remota preconfigurada][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="402b9-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="402b9-226">[Metadatos de información de dispositivo en la solución preconfigurada de supervisión remota][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="402b9-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="402b9-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize] (Personalización de cómo muestra la solución de fábrica conectada los datos de los servidores de OPC UA)</span><span class="sxs-lookup"><span data-stu-id="402b9-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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