---
title: "telemetría dinámica aaaUse | Documentos de Microsoft"
description: "Siga este tutorial toolearn cómo toouse telemetría dinámica con la supervisión remota de hello Azure IoT conjunto preconfigurado solución."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="b14c9-103">Use la telemetría dinámica con hello solución preconfigurada de supervisión remota</span><span class="sxs-lookup"><span data-stu-id="b14c9-103">Use dynamic telemetry with hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="b14c9-104">Telemetría dinámica permite toovisualize cualquier toohello de telemetría enviado solución preconfigurada de supervisión remoto.</span><span class="sxs-lookup"><span data-stu-id="b14c9-104">Dynamic telemetry enables you toovisualize any telemetry sent toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="b14c9-105">dispositivos de Hello simulada que se implementan con la solución de hello preconfigurado envían telemetría de temperatura y humedad, que puede visualizar en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14c9-105">hello simulated devices that deploy with hello preconfigured solution send temperature and humidity telemetry, which you can visualize on hello dashboard.</span></span> <span data-ttu-id="b14c9-106">Si personaliza los dispositivos simulados existentes, crear nuevos dispositivos simulados o conectarse a dispositivos físicos toohello preconfigurado solución puede enviar otros valores de telemetría como una temperatura externo hello, RPM o velocidad del viento.</span><span class="sxs-lookup"><span data-stu-id="b14c9-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices toohello preconfigured solution you can send other telemetry values such as hello external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="b14c9-107">A continuación, puede visualizar esta telemetría adicional en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14c9-107">You can then visualize this additional telemetry on hello dashboard.</span></span>

<span data-ttu-id="b14c9-108">Este tutorial usa un simple dispositivo simulado de Node.js que puede modificar fácilmente tooexperiment con la telemetría dinámica.</span><span class="sxs-lookup"><span data-stu-id="b14c9-108">This tutorial uses a simple Node.js simulated device that you can easily modify tooexperiment with dynamic telemetry.</span></span>

<span data-ttu-id="b14c9-109">toocomplete este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="b14c9-109">toocomplete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="b14c9-110">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b14c9-110">An active Azure subscription.</span></span> <span data-ttu-id="b14c9-111">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b14c9-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b14c9-112">Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="b14c9-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="b14c9-113">[Node.js][lnk-node] versión 0.12.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="b14c9-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="b14c9-114">Puede completar este tutorial en cualquier sistema operativo, como Windows o Linux, donde pueda instalar Node.js.</span><span class="sxs-lookup"><span data-stu-id="b14c9-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="b14c9-115">Adición de un tipo de datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="b14c9-115">Add a telemetry type</span></span>

<span data-ttu-id="b14c9-116">Hola siguiente paso es telemetría de hello tooreplace generado por dispositivo simulado de hello Node.js con un nuevo conjunto de valores:</span><span class="sxs-lookup"><span data-stu-id="b14c9-116">hello next step is tooreplace hello telemetry generated by hello Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="b14c9-117">Detener hello Node.js dispositivo simulado escribiendo **Ctrl + C** en el símbolo del sistema o el shell.</span><span class="sxs-lookup"><span data-stu-id="b14c9-117">Stop hello Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="b14c9-118">En el archivo de remote_monitoring.js hello, puede ver valores de base de datos de Hola para temperatura existente hello, humedad y telemetría de temperatura externo.</span><span class="sxs-lookup"><span data-stu-id="b14c9-118">In hello remote_monitoring.js file, you can see hello base data values for hello existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="b14c9-119">Agregue un valor de la base de datos para **rpm** como sigue:</span><span class="sxs-lookup"><span data-stu-id="b14c9-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="b14c9-120">dispositivo simulado de Hello Node.js usa hello **generateRandomIncrement** funcionando en hello remote_monitoring.js archivo tooadd un incremento aleatorio toohello valores de base de datos.</span><span class="sxs-lookup"><span data-stu-id="b14c9-120">hello Node.js simulated device uses hello **generateRandomIncrement** function in hello remote_monitoring.js file tooadd a random increment toohello base data values.</span></span> <span data-ttu-id="b14c9-121">Aleatorizar hello **rpm** valor agregando una línea de código después de aleatorizaciones existente de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="b14c9-121">Randomize hello **rpm** value by adding a line of code after hello existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="b14c9-122">Agregue Hola nueva rpm valor toohello JSON carga Hola dispositivo envía tooIoT concentrador:</span><span class="sxs-lookup"><span data-stu-id="b14c9-122">Add hello new rpm value toohello JSON payload hello device sends tooIoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="b14c9-123">Ejecute dispositivo simulado de hello Node.js con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b14c9-123">Run hello Node.js simulated device using hello following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="b14c9-124">Tenga en cuenta Hola nuevo RPM telemetría tipo que se muestra en el gráfico de hello en el panel de hello:</span><span class="sxs-lookup"><span data-stu-id="b14c9-124">Observe hello new RPM telemetry type that displays on hello chart in hello dashboard:</span></span>

![Agregar RPM toohello panel][image3]

> [!NOTE]
> <span data-ttu-id="b14c9-126">Puede necesita toodisable y, a continuación, habilitar el dispositivo de Node.js Hola Hola **dispositivos** página en hello panel toosee Hola de cambios inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="b14c9-126">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="customize-hello-dashboard-display"></a><span data-ttu-id="b14c9-127">Personalizar la visualización del panel de Hola</span><span class="sxs-lookup"><span data-stu-id="b14c9-127">Customize hello dashboard display</span></span>

<span data-ttu-id="b14c9-128">Hola **información del dispositivo** mensaje puede incluir metadatos acerca de telemetría de hello dispositivo Hola puede enviar tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="b14c9-128">hello **Device-Info** message can include metadata about hello telemetry hello device can send tooIoT Hub.</span></span> <span data-ttu-id="b14c9-129">Estos metadatos pueden especificar tipos de telemetría de Hola Hola dispositivo envíe.</span><span class="sxs-lookup"><span data-stu-id="b14c9-129">This metadata can specify hello telemetry types hello device sends.</span></span> <span data-ttu-id="b14c9-130">Modificar hello **deviceMetaData** valor en hello remote_monitoring.js archivo tooinclude una **telemetría** definición después hello **comandos** definición.</span><span class="sxs-lookup"><span data-stu-id="b14c9-130">Modify hello **deviceMetaData** value in hello remote_monitoring.js file tooinclude a **Telemetry** definition following hello **Commands** definition.</span></span> <span data-ttu-id="b14c9-131">Hello fragmento de código siguiente muestra hello **comandos** definición (ser seguro tooadd una `,` después de hello **comandos** definición):</span><span class="sxs-lookup"><span data-stu-id="b14c9-131">hello following code snippet shows hello **Commands** definition (be sure tooadd a `,` after hello **Commands** definition):</span></span>

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> <span data-ttu-id="b14c9-132">solución de supervisión remoto Hello usa una definición de los metadatos de mayúsculas y minúsculas toocompare Hola con datos de flujo de telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14c9-132">hello remote monitoring solution uses a case-insensitive match toocompare hello metadata definition with data in hello telemetry stream.</span></span>


<span data-ttu-id="b14c9-133">Agregar un **telemetría** definición tal como se muestra en hello anterior fragmento de código no cambia el comportamiento de Hola de panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14c9-133">Adding a **Telemetry** definition as shown in hello preceding code snippet does not change hello behavior of hello dashboard.</span></span> <span data-ttu-id="b14c9-134">Sin embargo, también pueden incluir metadatos Hola un **DisplayName** toocustomize Hola mostrar en el panel de Hola de atributo.</span><span class="sxs-lookup"><span data-stu-id="b14c9-134">However, hello metadata can also include a **DisplayName** attribute toocustomize hello display in hello dashboard.</span></span> <span data-ttu-id="b14c9-135">Hola de actualización **telemetría** definición de metadatos, como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="b14c9-135">Update hello **Telemetry** metadata definition as shown in hello following snippet:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

<span data-ttu-id="b14c9-136">Hello captura de pantalla siguiente muestra cómo este cambio modifica la leyenda del gráfico de hello en el panel de hello:</span><span class="sxs-lookup"><span data-stu-id="b14c9-136">hello following screenshot shows how this change modifies hello chart legend on hello dashboard:</span></span>

![Personalizar la leyenda del gráfico Hola][image4]

> [!NOTE]
> <span data-ttu-id="b14c9-138">Puede necesita toodisable y, a continuación, habilitar el dispositivo de Node.js Hola Hola **dispositivos** página en hello panel toosee Hola de cambios inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="b14c9-138">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="filter-hello-telemetry-types"></a><span data-ttu-id="b14c9-139">Filtrar los tipos de telemetría de Hola</span><span class="sxs-lookup"><span data-stu-id="b14c9-139">Filter hello telemetry types</span></span>

<span data-ttu-id="b14c9-140">De forma predeterminada, el gráfico de hello en el panel de hello muestra cada serie de datos en secuencia de telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14c9-140">By default, hello chart on hello dashboard shows every data series in hello telemetry stream.</span></span> <span data-ttu-id="b14c9-141">Puede usar hello **información del dispositivo** metadatos toosuppress Hola visualización de tipos de telemetría específica en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14c9-141">You can use hello **Device-Info** metadata toosuppress hello display of specific telemetry types on hello chart.</span></span> 

<span data-ttu-id="b14c9-142">gráfico de hello toomake mostrar solo telemetría temperatura y humedad, omitir **ExternalTemperature** de hello **información del dispositivo** **telemetría** metadatos como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b14c9-142">toomake hello chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from hello **Device-Info** **Telemetry** metadata as follows:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

<span data-ttu-id="b14c9-143">Hola **temperatura exteriores** deja de aparecer en el gráfico de hello:</span><span class="sxs-lookup"><span data-stu-id="b14c9-143">hello **Outdoor Temperature** no longer displays on hello chart:</span></span>

![Filtro de telemetría de hello en el panel de Hola][image5]

<span data-ttu-id="b14c9-145">Este cambio solo afecta a la presentación del gráfico Hola.</span><span class="sxs-lookup"><span data-stu-id="b14c9-145">This change only affects hello chart display.</span></span> <span data-ttu-id="b14c9-146">Hola **ExternalTemperature** valores de datos aún se almacenan y están disponibles para ningún procesamiento back-end.</span><span class="sxs-lookup"><span data-stu-id="b14c9-146">hello **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="b14c9-147">Puede necesita toodisable y, a continuación, habilitar el dispositivo de Node.js Hola Hola **dispositivos** página en hello panel toosee Hola de cambios inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="b14c9-147">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="b14c9-148">errores</span><span class="sxs-lookup"><span data-stu-id="b14c9-148">Handle errors</span></span>

<span data-ttu-id="b14c9-149">Para una toodisplay de flujo de datos en el gráfico de hello, su **tipo** en hello **información del dispositivo** metadatos deben coincidir con el tipo de datos de Hola de valores de telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14c9-149">For a data stream toodisplay on hello chart, its **Type** in hello **Device-Info** metadata must match hello data type of hello telemetry values.</span></span> <span data-ttu-id="b14c9-150">Por ejemplo, si hello metadatos especifican ese hello **tipo** humedad de datos son **int** y un **doble** se encuentra en la secuencia de telemetría de hello telemetría de humedad de hello no no se muestran en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14c9-150">For example, if hello metadata specifies that hello **Type** of humidity data is **int** and a **double** is found in hello telemetry stream then hello humidity telemetry does not display on hello chart.</span></span> <span data-ttu-id="b14c9-151">Sin embargo, Hola **humedad** valores todavía se almacenan y están disponibles para cualquier procesamiento back-end.</span><span class="sxs-lookup"><span data-stu-id="b14c9-151">However, hello **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b14c9-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b14c9-152">Next steps</span></span>

<span data-ttu-id="b14c9-153">Ahora que ha visto cómo toouse telemetría dinámico, puede obtener más información sobre soluciones preconfiguradas de Hola de cómo usar información del dispositivo: [metadatos de información de dispositivo de supervisión remota de hello preconfigurado solución] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="b14c9-153">Now that you've seen how toouse dynamic telemetry, you can learn more about how hello preconfigured solutions use device information: [Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
