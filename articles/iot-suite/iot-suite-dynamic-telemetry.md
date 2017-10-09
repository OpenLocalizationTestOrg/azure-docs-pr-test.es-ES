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
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>Use la telemetría dinámica con hello solución preconfigurada de supervisión remota

Telemetría dinámica permite toovisualize cualquier toohello de telemetría enviado solución preconfigurada de supervisión remoto. dispositivos de Hello simulada que se implementan con la solución de hello preconfigurado envían telemetría de temperatura y humedad, que puede visualizar en el panel de Hola. Si personaliza los dispositivos simulados existentes, crear nuevos dispositivos simulados o conectarse a dispositivos físicos toohello preconfigurado solución puede enviar otros valores de telemetría como una temperatura externo hello, RPM o velocidad del viento. A continuación, puede visualizar esta telemetría adicional en el panel de Hola.

Este tutorial usa un simple dispositivo simulado de Node.js que puede modificar fácilmente tooexperiment con la telemetría dinámica.

toocomplete este tutorial, necesitará:

* Una suscripción de Azure activa. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].
* [Node.js][lnk-node] versión 0.12.x, o posteriores.

Puede completar este tutorial en cualquier sistema operativo, como Windows o Linux, donde pueda instalar Node.js.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>Adición de un tipo de datos de telemetría

Hola siguiente paso es telemetría de hello tooreplace generado por dispositivo simulado de hello Node.js con un nuevo conjunto de valores:

1. Detener hello Node.js dispositivo simulado escribiendo **Ctrl + C** en el símbolo del sistema o el shell.
2. En el archivo de remote_monitoring.js hello, puede ver valores de base de datos de Hola para temperatura existente hello, humedad y telemetría de temperatura externo. Agregue un valor de la base de datos para **rpm** como sigue:

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. dispositivo simulado de Hello Node.js usa hello **generateRandomIncrement** funcionando en hello remote_monitoring.js archivo tooadd un incremento aleatorio toohello valores de base de datos. Aleatorizar hello **rpm** valor agregando una línea de código después de aleatorizaciones existente de hello como sigue:

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Agregue Hola nueva rpm valor toohello JSON carga Hola dispositivo envía tooIoT concentrador:

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. Ejecute dispositivo simulado de hello Node.js con hello siguiente comando:

    `node remote_monitoring.js`

6. Tenga en cuenta Hola nuevo RPM telemetría tipo que se muestra en el gráfico de hello en el panel de hello:

![Agregar RPM toohello panel][image3]

> [!NOTE]
> Puede necesita toodisable y, a continuación, habilitar el dispositivo de Node.js Hola Hola **dispositivos** página en hello panel toosee Hola de cambios inmediatamente.

## <a name="customize-hello-dashboard-display"></a>Personalizar la visualización del panel de Hola

Hola **información del dispositivo** mensaje puede incluir metadatos acerca de telemetría de hello dispositivo Hola puede enviar tooIoT concentrador. Estos metadatos pueden especificar tipos de telemetría de Hola Hola dispositivo envíe. Modificar hello **deviceMetaData** valor en hello remote_monitoring.js archivo tooinclude una **telemetría** definición después hello **comandos** definición. Hello fragmento de código siguiente muestra hello **comandos** definición (ser seguro tooadd una `,` después de hello **comandos** definición):

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
> solución de supervisión remoto Hello usa una definición de los metadatos de mayúsculas y minúsculas toocompare Hola con datos de flujo de telemetría de Hola.


Agregar un **telemetría** definición tal como se muestra en hello anterior fragmento de código no cambia el comportamiento de Hola de panel de Hola. Sin embargo, también pueden incluir metadatos Hola un **DisplayName** toocustomize Hola mostrar en el panel de Hola de atributo. Hola de actualización **telemetría** definición de metadatos, como se muestra en el siguiente fragmento de código de hello:

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

Hello captura de pantalla siguiente muestra cómo este cambio modifica la leyenda del gráfico de hello en el panel de hello:

![Personalizar la leyenda del gráfico Hola][image4]

> [!NOTE]
> Puede necesita toodisable y, a continuación, habilitar el dispositivo de Node.js Hola Hola **dispositivos** página en hello panel toosee Hola de cambios inmediatamente.

## <a name="filter-hello-telemetry-types"></a>Filtrar los tipos de telemetría de Hola

De forma predeterminada, el gráfico de hello en el panel de hello muestra cada serie de datos en secuencia de telemetría de Hola. Puede usar hello **información del dispositivo** metadatos toosuppress Hola visualización de tipos de telemetría específica en el gráfico de Hola. 

gráfico de hello toomake mostrar solo telemetría temperatura y humedad, omitir **ExternalTemperature** de hello **información del dispositivo** **telemetría** metadatos como se indica a continuación:

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

Hola **temperatura exteriores** deja de aparecer en el gráfico de hello:

![Filtro de telemetría de hello en el panel de Hola][image5]

Este cambio solo afecta a la presentación del gráfico Hola. Hola **ExternalTemperature** valores de datos aún se almacenan y están disponibles para ningún procesamiento back-end.

> [!NOTE]
> Puede necesita toodisable y, a continuación, habilitar el dispositivo de Node.js Hola Hola **dispositivos** página en hello panel toosee Hola de cambios inmediatamente.

## <a name="handle-errors"></a>errores

Para una toodisplay de flujo de datos en el gráfico de hello, su **tipo** en hello **información del dispositivo** metadatos deben coincidir con el tipo de datos de Hola de valores de telemetría de Hola. Por ejemplo, si hello metadatos especifican ese hello **tipo** humedad de datos son **int** y un **doble** se encuentra en la secuencia de telemetría de hello telemetría de humedad de hello no no se muestran en el gráfico de Hola. Sin embargo, Hola **humedad** valores todavía se almacenan y están disponibles para cualquier procesamiento back-end.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha visto cómo toouse telemetría dinámico, puede obtener más información sobre soluciones preconfiguradas de Hola de cómo usar información del dispositivo: [metadatos de información de dispositivo de supervisión remota de hello preconfigurado solución] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
