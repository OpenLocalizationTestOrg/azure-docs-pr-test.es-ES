---
title: "Telemetría dinámica | Microsoft Docs"
description: "Siga este tutorial para aprender a usar la telemetría dinámica con la solución de supervisión remota preconfigurada del Conjunto de aplicaciones de IoT de Azure."
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
ms.openlocfilehash: 0114f27f9b8ae76e1170d04ddf66e2c4bf20686a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-dynamic-telemetry-with-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="54d09-103">Uso de telemetría dinámica con la solución de supervisión remota preconfigurada</span><span class="sxs-lookup"><span data-stu-id="54d09-103">Use dynamic telemetry with the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="54d09-104">La telemetría dinámica le permite visualizar los datos de telemetría enviados a la solución preconfigurada de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="54d09-104">Dynamic telemetry enables you to visualize any telemetry sent to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="54d09-105">Los dispositivos simulados que se implementan con la solución preconfigurada envían datos de temperatura y humedad de telemetría que puede visualizar en el panel.</span><span class="sxs-lookup"><span data-stu-id="54d09-105">The simulated devices that deploy with the preconfigured solution send temperature and humidity telemetry, which you can visualize on the dashboard.</span></span> <span data-ttu-id="54d09-106">Si personaliza los dispositivos simulados existentes, crea nuevos dispositivos simulados o conecta dispositivos físicos a la solución preconfigurada, podrá enviar otros valores de telemetría, como la temperatura exterior, RPM o la velocidad del viento.</span><span class="sxs-lookup"><span data-stu-id="54d09-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices to the preconfigured solution you can send other telemetry values such as the external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="54d09-107">A continuación podrá visualizar en el panel estos datos de telemetría adicionales.</span><span class="sxs-lookup"><span data-stu-id="54d09-107">You can then visualize this additional telemetry on the dashboard.</span></span>

<span data-ttu-id="54d09-108">Este tutorial usa un dispositivo simulado Node.js simple que puede modificar fácilmente para experimentar con la telemetría dinámica.</span><span class="sxs-lookup"><span data-stu-id="54d09-108">This tutorial uses a simple Node.js simulated device that you can easily modify to experiment with dynamic telemetry.</span></span>

<span data-ttu-id="54d09-109">Para completar este tutorial necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="54d09-109">To complete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="54d09-110">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="54d09-110">An active Azure subscription.</span></span> <span data-ttu-id="54d09-111">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="54d09-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="54d09-112">Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="54d09-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="54d09-113">[Node.js][lnk-node] versión 0.12.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="54d09-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="54d09-114">Puede completar este tutorial en cualquier sistema operativo, como Windows o Linux, donde pueda instalar Node.js.</span><span class="sxs-lookup"><span data-stu-id="54d09-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="54d09-115">Adición de un tipo de datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="54d09-115">Add a telemetry type</span></span>

<span data-ttu-id="54d09-116">El siguiente paso es reemplazar los datos de telemetría generados por el dispositivo simulado de Node.js con un nuevo conjunto de valores:</span><span class="sxs-lookup"><span data-stu-id="54d09-116">The next step is to replace the telemetry generated by the Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="54d09-117">Presione **Ctrl + C** en el símbolo del sistema o el shell para detener el dispositivo simulado de Node.js.</span><span class="sxs-lookup"><span data-stu-id="54d09-117">Stop the Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="54d09-118">En el archivo remote_monitoring.js, verá los valores de la base de datos de telemetría para la temperatura, la humedad y la temperatura exterior existentes.</span><span class="sxs-lookup"><span data-stu-id="54d09-118">In the remote_monitoring.js file, you can see the base data values for the existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="54d09-119">Agregue un valor de la base de datos para **rpm** como sigue:</span><span class="sxs-lookup"><span data-stu-id="54d09-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="54d09-120">El dispositivo simulado de Node.js usa la función **generateRandomIncrement** del archivo remote_monitoring.js para agregar un incremento aleatorio a los valores de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="54d09-120">The Node.js simulated device uses the **generateRandomIncrement** function in the remote_monitoring.js file to add a random increment to the base data values.</span></span> <span data-ttu-id="54d09-121">Aleatorice el valor de **rpm** agregando una línea de código después de la aleatorizaciones existentes como sigue:</span><span class="sxs-lookup"><span data-stu-id="54d09-121">Randomize the **rpm** value by adding a line of code after the existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="54d09-122">Agregue el nuevo valor de rpm para la carga útil de JSON, que el dispositivo envía al Centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="54d09-122">Add the new rpm value to the JSON payload the device sends to IoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="54d09-123">Ejecute el dispositivo simulado de Node.js con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="54d09-123">Run the Node.js simulated device using the following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="54d09-124">Observe el nuevo tipo de datos de telemetría RPM que se muestra en el gráfico en el panel:</span><span class="sxs-lookup"><span data-stu-id="54d09-124">Observe the new RPM telemetry type that displays on the chart in the dashboard:</span></span>

![RPM agregado al panel][image3]

> [!NOTE]
> <span data-ttu-id="54d09-126">Puede que necesite deshabilitar y habilitar el dispositivo de Node.js en la página **Dispositivos** del panel para ver el cambio inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="54d09-126">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="customize-the-dashboard-display"></a><span data-ttu-id="54d09-127">Personalización de la presentación en el panel</span><span class="sxs-lookup"><span data-stu-id="54d09-127">Customize the dashboard display</span></span>

<span data-ttu-id="54d09-128">El mensaje **Device-Info** puede incluir metadatos sobre la telemetría que el dispositivo envíe al Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="54d09-128">The **Device-Info** message can include metadata about the telemetry the device can send to IoT Hub.</span></span> <span data-ttu-id="54d09-129">Estos metadatos pueden especificar los tipos de datos de telemetría que envía el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="54d09-129">This metadata can specify the telemetry types the device sends.</span></span> <span data-ttu-id="54d09-130">Modifique el valor **deviceMetaData** en el archivo remote_monitoring.js para que incluya una definición de **telemetría** después de la definición de **comandos**.</span><span class="sxs-lookup"><span data-stu-id="54d09-130">Modify the **deviceMetaData** value in the remote_monitoring.js file to include a **Telemetry** definition following the **Commands** definition.</span></span> <span data-ttu-id="54d09-131">El siguiente fragmento de código muestra la definición **Comandos** (asegúrese de agregar un `,` después de la definición **Comandos**):</span><span class="sxs-lookup"><span data-stu-id="54d09-131">The following code snippet shows the **Commands** definition (be sure to add a `,` after the **Commands** definition):</span></span>

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
> <span data-ttu-id="54d09-132">La solución de supervisión remota utiliza a una coincidencia de mayúsculas y minúsculas para comparar la definición de metadatos con los datos del flujo de telemetría.</span><span class="sxs-lookup"><span data-stu-id="54d09-132">The remote monitoring solution uses a case-insensitive match to compare the metadata definition with data in the telemetry stream.</span></span>


<span data-ttu-id="54d09-133">Agregar una definición de **telemetría** como la del fragmento de código anterior no cambia el comportamiento del panel.</span><span class="sxs-lookup"><span data-stu-id="54d09-133">Adding a **Telemetry** definition as shown in the preceding code snippet does not change the behavior of the dashboard.</span></span> <span data-ttu-id="54d09-134">Sin embargo, los metadatos también pueden incluir los un atributo **DisplayName** para personalizar la presentación en el panel.</span><span class="sxs-lookup"><span data-stu-id="54d09-134">However, the metadata can also include a **DisplayName** attribute to customize the display in the dashboard.</span></span> <span data-ttu-id="54d09-135">Actualice la definición de los metadatos de **telemetría** como se muestra en el siguiente fragmento:</span><span class="sxs-lookup"><span data-stu-id="54d09-135">Update the **Telemetry** metadata definition as shown in the following snippet:</span></span>

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

<span data-ttu-id="54d09-136">En la captura de pantalla siguiente se muestra cómo este cambio modifica la leyenda del gráfico en el panel:</span><span class="sxs-lookup"><span data-stu-id="54d09-136">The following screenshot shows how this change modifies the chart legend on the dashboard:</span></span>

![Personalización de la leyenda del gráfico][image4]

> [!NOTE]
> <span data-ttu-id="54d09-138">Puede que necesite deshabilitar y habilitar el dispositivo de Node.js en la página **Dispositivos** del panel para ver el cambio inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="54d09-138">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="filter-the-telemetry-types"></a><span data-ttu-id="54d09-139">Filtrado de los tipos de datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="54d09-139">Filter the telemetry types</span></span>

<span data-ttu-id="54d09-140">De forma predeterminada, el gráfico del panel muestra las series de datos en el flujo de telemetría.</span><span class="sxs-lookup"><span data-stu-id="54d09-140">By default, the chart on the dashboard shows every data series in the telemetry stream.</span></span> <span data-ttu-id="54d09-141">Puede usar los metadatos de **Device-Info** para suprimir la presentación de determinados tipos de datos de telemetría en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="54d09-141">You can use the **Device-Info** metadata to suppress the display of specific telemetry types on the chart.</span></span> 

<span data-ttu-id="54d09-142">Para que en el gráfico se muestren solo los datos de telemetría relativos a la temperatura y la humedad, omita el dato de **ExternalTemperature** de los metadatos de **telemetría** de **Device-Info** como sigue:</span><span class="sxs-lookup"><span data-stu-id="54d09-142">To make the chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from the **Device-Info** **Telemetry** metadata as follows:</span></span>

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

<span data-ttu-id="54d09-143">La **temperatura exterior** ya no aparece en el gráfico:</span><span class="sxs-lookup"><span data-stu-id="54d09-143">The **Outdoor Temperature** no longer displays on the chart:</span></span>

![Datos de telemetría filtrados en el panel][image5]

<span data-ttu-id="54d09-145">Este cambio solo afecta a la visualización del gráfico.</span><span class="sxs-lookup"><span data-stu-id="54d09-145">This change only affects the chart display.</span></span> <span data-ttu-id="54d09-146">Los valores de datos de **ExternalTemperature** siguen almacenados y están disponibles para cualquier procesamiento de back-end.</span><span class="sxs-lookup"><span data-stu-id="54d09-146">The **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="54d09-147">Puede que necesite deshabilitar y habilitar el dispositivo de Node.js en la página **Dispositivos** del panel para ver el cambio inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="54d09-147">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="54d09-148">errores</span><span class="sxs-lookup"><span data-stu-id="54d09-148">Handle errors</span></span>

<span data-ttu-id="54d09-149">Para que el gráfico muestre el flujo de datos, su **Type** en los metadatos de **Device-Info** debe coincidir con el tipo de datos de los valores de telemetría.</span><span class="sxs-lookup"><span data-stu-id="54d09-149">For a data stream to display on the chart, its **Type** in the **Device-Info** metadata must match the data type of the telemetry values.</span></span> <span data-ttu-id="54d09-150">Por ejemplo, si los metadatos que especifican que el **tipo** de datos de humedad es **int** y se encuentra **double** en el flujo de telemetría, los datos de telemetría relativos a la humedad no se muestran en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="54d09-150">For example, if the metadata specifies that the **Type** of humidity data is **int** and a **double** is found in the telemetry stream then the humidity telemetry does not display on the chart.</span></span> <span data-ttu-id="54d09-151">Sin embargo, los valores de **Humidity** (Humedad) siguen almacenados y están disponibles para cualquier procesamiento de back-end.</span><span class="sxs-lookup"><span data-stu-id="54d09-151">However, the **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54d09-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="54d09-152">Next steps</span></span>

<span data-ttu-id="54d09-153">Ahora que ya sabe cómo utilizar la telemetría dinámico, puede obtener más información sobre cómo las soluciones preconfiguradas emplean la información de los dispositivos: [Metadatos de información de dispositivo en la solución preconfigurada de supervisión remota][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="54d09-153">Now that you've seen how to use dynamic telemetry, you can learn more about how the preconfigured solutions use device information: [Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
