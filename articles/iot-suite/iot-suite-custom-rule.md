---
title: aaaCreate una regla personalizada en el conjunto de IoT de Azure | Documentos de Microsoft
description: "¿Cómo toocreate una regla personalizada en un conjunto de IoT había preconfigurado solución."
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
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>Crear una regla personalizada en hello solución preconfigurada de supervisión remota

## <a name="introduction"></a>Introducción

En las soluciones de hello preconfigurado, puede configurar [las reglas que activan cuando una telemetría valor para un dispositivo alcanza un umbral específico][lnk-builtin-rule]. [Use la telemetría dinámica con hello solución preconfigurada de supervisión remota] [ lnk-dynamic-telemetry] describe cómo puede agregar valores de telemetría personalizada, como *ExternalTemperature* tooyour solución. Este artículo muestra cómo toocreate regla personalizada para telemetría dinámica de los tipos de la solución.

Este tutorial usa un simple Node.js dispositivo simulado toogenerate telemetría dinámica toosend toohello solución preconfigurada back-end. A continuación, agregará reglas personalizadas en hello **RemoteMonitoring** solución de Visual Studio e implementar este tooyour de back-end personalizada suscripción de Azure.

toocomplete este tutorial, necesita:

* Una suscripción de Azure activa. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].
* [Node.js] [ lnk-node] versión 0.12.x o posterior toocreate un dispositivo simulado.
* Visual Studio 2015 o Visual Studio de 2017 toomodify Hola preconfigurado solución volver terminar con las nuevas reglas.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

Tome nota del nombre de la solución de Hola que eligió para su implementación. Necesitará el nombre de esta solución más adelante en el tutorial.

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

Puede detener la aplicación de consola de hello Node.js cuando haya comprobado que está enviando **ExternalTemperature** toohello de telemetría preconfigurado solución. Mantenga la ventana de la consola de hello abierta porque esta aplicación de consola Node.js vuelva a ejecutar después de Agregar solución toohello de hello regla personalizada.

## <a name="rule-storage-locations"></a>Ubicaciones de almacenamiento de las reglas

La información sobre las reglas se mantiene en dos ubicaciones:

* **DeviceRulesNormalizedTable** : esta tabla almacena un normalizado hacen referencia a las reglas de toohello definidas por el portal de solución de Hola. Cuando el portal de solución de hello muestra reglas de dispositivos, consulta esta tabla para las definiciones de reglas de Hola.
* **DeviceRules** blob – este blob almacena todas las reglas de hello definidas para todos los dispositivos registrados y se define como un trabajos de análisis de transmisiones de Azure toohello entrada de referencia.
 
Al actualizar una regla existente o definir una nueva regla en el portal de solución de hello, tabla hello y blob son cambios de hello tooreflect actualizada. regla Hola definición se muestra en el portal de hello procede del almacén de tablas de Hola y regla Hola definición hace referencia a trabajos de análisis de transmisiones de hello procede de blob de Hola. 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>Actualizar soluciones de Visual Studio de RemoteMonitoring Hola

Hello pasos siguientes muestran cómo toomodify Hola tooinclude de solución de Visual Studio de RemoteMonitoring una nueva regla que utilice hello **ExternalTemperature** telemetría enviado desde dispositivo simulado de hello:

1. Si se ha no lo ha hecho, Hola clon **-iot-remoto-supervisión de azure** ubicación adecuada del repositorio tooa en el equipo local mediante el siguiente comando de Git de hello:

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. En Visual Studio, abra el archivo de RemoteMonitoring.sln de Hola desde su copia local de hello **-iot-remoto-supervisión de azure** repositorio.

3. Abra el archivo hello Infrastructure\Models\DeviceRuleBlobEntity.cs y agregue un **ExternalTemperature** propiedad tal como se indica a continuación:

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. En el mismo archivo de Hola, agregar un **ExternalTemperatureRuleOutput** propiedad tal como se indica a continuación:

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. Abra el archivo hello Infrastructure\Models\DeviceRuleDataFields.cs y agregue Hola siguiente **ExternalTemperature** propiedad después de hello existente **humedad** propiedad:

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. Hola mismo archivo en la consulta, actualizar hello **_availableDataFields** método tooinclude **ExternalTemperature** como se indica a continuación:

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. Abra el archivo hello Infrastructure\Repository\DeviceRulesRepository.cs y modificar hello **BuildBlobEntityListFromTableRows** método tal como se indica a continuación:

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a>Volver a generar e implementar soluciones de Hola.

Ahora puede implementar Hola Actualizar solución tooyour suscripción de Azure.

1. Abra un símbolo del sistema con privilegios elevados y vaya toohello raíz de una copia local del repositorio de hello-iot-remoto-supervisión de azure.

2. toodeploy la solución actualizada, ejecute hello después de sustituir el comando **{nombre de la implementación}** con nombre de saludo de la implementación de soluciones preconfiguradas que se ha indicado anteriormente:

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>Actualizar el trabajo de análisis de transmisiones de Hola

Una vez completada la implementación de hello, puede actualizar Hola análisis de transmisiones toouse Hola nueva regla definiciones de trabajos.

1. Hola portal de Azure, navegue toohello grupo de recursos que contiene los recursos de la solución preconfigurada. Este grupo de recursos tiene Hola mismo nombre que especificó para Hola solución durante la implementación de Hola.

2. Navegue toohello {nombre de la implementación}-trabajo de análisis de transmisiones de reglas. 

3. Haga clic en **detener** trabajo de análisis de transmisiones de hello toostop de ejecución. (Se debe esperar a hello toostop de trabajo de streaming antes de poder editar consulta hello).

4. Haga clic en **Consulta**. Editar Hola de hello consulta tooinclude **seleccione** instrucción para **ExternalTemperature**. Hello en el ejemplo siguiente se muestra completo de la consulta Hola con hello nueva **seleccione** instrucción:

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
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. Haga clic en **guardar** toochange Hola actualiza la consulta de la regla.

6. Haga clic en **iniciar** trabajo de análisis de transmisiones de hello toostart ejecutar de nuevo.

## <a name="add-your-new-rule-in-hello-dashboard"></a>Agregar la nueva regla en el panel de Hola

Ahora puede agregar hello **ExternalTemperature** dispositivo de tooa de regla en el panel de la solución de Hola.

1. Navegue toohello portal de solución.

2. Navegue toohello **dispositivos** panel.

3. Busque Hola dispositivo personalizado que crea que envía **ExternalTemperature** telemetría y en hello **detalles del dispositivo** del panel, haga clic en **Agregar regla**.

4. Seleccione **ExternalTemperature** en **Campo de datos**.

5. Establecer **umbral** too56. Luego, haga clic en **Guardar y ver reglas**.

6. Devuelve el historial de alarma de toohello panel tooview Hola.

7. En ventana de consola de Hola dejan abiertos, empezar a enviar de toobegin de aplicación de hello Node.js consola **ExternalTemperature** los datos de telemetría.

8. Tenga en cuenta que hello **historial de alarma** tabla muestran alarmas nueva cuando se desencadene Hola nueva regla.
 
## <a name="additional-information"></a>Información adicional

Cambiar operador hello  **>**  es más compleja y va más allá de los pasos de hello descritos en este tutorial. Aunque es posible cambiar toouse de trabajo de análisis de transmisiones de hello cualquier operador le gusta, reflejar ese operador en el portal de solución de hello es una tarea más compleja. 

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha visto cómo toocreate reglas personalizadas, puede obtener más información acerca de las soluciones de hello preconfigurado:

- [Solución de Azure de supervisión remota de conjunto de IoT preconfigurado tooyour de aplicación lógica de conexión][lnk-logic-app]
- [Metadatos de información de dispositivo de supervisión remota de hello preconfigurado solución][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md