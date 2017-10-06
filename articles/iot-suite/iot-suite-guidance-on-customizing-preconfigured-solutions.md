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
# <a name="customize-a-preconfigured-solution"></a>Personalizar una solución preconfigurada

soluciones de Hello preconfigurado proporcionadas con hello Azure IoT Suite muestran los servicios de hello en hello suite trabajar juntos toodeliver una solución end-to-end. Desde este punto de partida, hay varios lugares en los que puede ampliar y personalizar soluciones de Hola para escenarios concretos. Hola siguientes secciones describe estos puntos de personalización comunes.

## <a name="find-hello-source-code"></a>Buscar código fuente de Hola

código fuente de Hola para soluciones de hello preconfigurado está disponible en GitHub en hello después repositorios:

* Supervisión remota: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* Mantenimiento predictivo: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* Fábrica conectada: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

código fuente de Hola para soluciones de hello preconfigurado es proporciona recomendaciones y los patrones de hello toodemonstrate utilizan funcionalidad de tooimplement Hola-to-end de una solución de IoT con conjunto de IoT de Azure. Puede encontrar más información sobre cómo toobuild e implementar soluciones de hello en repositorios de GitHub Hola.

## <a name="change-hello-preconfigured-rules"></a>Cambiar las reglas de hello preconfigurado

Hello solución de supervisión remota incluye tres [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) trabajos toohandle información del dispositivo, telemetría y lógica de reglas en soluciones de Hola.

Hello tres transmitir trabajos de análisis y su sintaxis se describen con más detalle en hello [supervisión remota preconfigurado tutorial de la solución](iot-suite-remote-monitoring-sample-walkthrough.md). 

Puede editar estos trabajos directamente tooalter Hola lógica o agregar lógica específica tooyour escenario. Puede encontrar Hola trabajos de análisis de transmisiones como sigue:

1. Vaya demasiado[portal de Azure](https://portal.azure.com).
2. Navegar por grupo de recursos de toohello con el mismo nombre que la solución de IoT de Hola. 
3. Seleccione el trabajo de análisis de transmisiones de Azure de hello le gustaría toomodify. 
4. Detención del trabajo de hello seleccionando **detener** en conjunto Hola de comandos. 
5. Editar salidas, consultas y las entradas de Hola.
   
    Una modificación sencilla es consultar toochange Hola Hola **reglas** trabajo toouse una **"<"** en lugar de un **">"**. portal de solución de Hello sigue mostrando **">"** al editar una regla, pero tenga en cuenta cómo se voltea el comportamiento de hello debido a cambios toohello Hola subyacente de trabajo.
6. Iniciar el trabajo de Hola

> [!NOTE]
> panel de supervisión remoto Hello depende de datos específicos, modificar trabajos Hola puede causar Hola panel toofail.

## <a name="add-your-own-rules"></a>Adición de reglas propias

Además toochanging Hola había preconfigurado trabajos de análisis de transmisiones de Azure, puede usar los nuevos trabajos de hello tooadd portal Azure o agregar nuevos trabajos de tooexisting de las consultas.

## <a name="customize-devices"></a>Personalización de dispositivos

Una de las actividades de extensión más comunes de Hola está trabajando con el escenario de tooyour específicos de dispositivos. Existen varios métodos para trabajar con dispositivos. Estos métodos incluyen modificar un toomatch dispositivo simulado su escenario, o mediante hello [SDK de dispositivos de IoT] [ IoT Device SDK] tooconnect la solución de toohello de dispositivo físico.

Para un dispositivo de tooadding guía paso a paso, vea hello [Iot Suite conectar dispositivos](iot-suite-connecting-devices.md) hello y artículo [ejemplo de SDK de C de supervisión remota](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring). Este ejemplo es toowork diseñada con hello solución preconfigurada de supervisión remoto.

### <a name="create-your-own-simulated-device"></a>Creación de dispositivo simulado propio

Incluido en hello [código fuente de solución de supervisión remota](https://github.com/Azure/azure-iot-remote-monitoring), es un simulador. NET. Este simulador es hello uno aprovisionado como parte de la solución de Hola y se puede modificar toosend distintos metadatos, telemetría y responder métodos y comandos de toodifferent.

simulador preconfigurada de Hola Hola solución preconfigurada de supervisión remota simula un dispositivo de refrigeración que emite la telemetría de temperatura y humedad. Puede modificar simulador Hola Hola [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) proyecto cuando se ha bifurcado repositorio de GitHub de Hola.

### <a name="available-locations-for-simulated-devices"></a>Ubicaciones disponibles para dispositivos simulados

conjunto de ubicaciones de Hello predeterminado es en Seattle y Redmond, Washington, Estados Unidos de América. Puede cambiar estas ubicaciones en [SampleDeviceFactory.cs][lnk-sample-device-factory].

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>Agregar un simulador de toohello del controlador de actualización de propiedad deseada

Puede establecer un valor para una propiedad deseada para un dispositivo en el portal de solución de Hola. Es responsabilidad de Hola de solicitud de cambio de propiedad de Hola Hola dispositivo toohandle al dispositivo de hello recupera el valor de la propiedad de hello deseado. compatibilidad con tooadd un cambio de valor de propiedad a través de una propiedad deseada, deberá tooadd un simulador de toohello de controlador.

simulador de Hello contiene controladores para hello **SetPointTemp** y **TelemetryInterval** deseado de propiedades que se pueden actualizar estableciendo valores en el portal de solución de Hola.

Hello en el ejemplo siguiente se muestra controlador Hola Hola **SetPointTemp** deseado propiedad Hola **CoolerDevice** clase:

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

Este método actualiza el punto de telemetría Hola informes hello temperatura y, a continuación, cambian atrás tooIoT concentrador estableciendo una propiedad notificada.

Puede agregar sus propios controladores para sus propias propiedades mediante el siguiente patrón de hello en el anterior ejemplo de Hola.

Debe enlazar también el controlador de hello propiedad deseada toohello tal y como se muestra en el siguiente ejemplo de Hola de hello **CoolerDevice** constructor:

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

Tenga en cuenta que **SetPointTempPropertyName** es una constante definida como "Config.SetPointTemp".

### <a name="add-support-for-a-new-method-toohello-simulator"></a>Agregar compatibilidad con un simulador de toohello método nuevo

Puede personalizar Hola simulador tooadd compatibilidad con un nuevo [método (directo)][lnk-direct-methods]. Se necesitan dos pasos principales:

- simulador Hola debe notificar al centro de IoT de hello en soluciones de hello preconfigurado con los detalles del método hello.
- simulador de Hello debe incluir la llamada al método de código toohandle Hola al invocarlo desde hello **detalles del dispositivo** panel en el Explorador de soluciones de Hola o a través de un trabajo.

Hello supervisión remota preconfigurado solución usa *notificado propiedades* toosend detalles del concentrador de tooIoT métodos admitidos. back-end de soluciones de Hello mantiene una lista de todos los métodos de hello admitidos por cada dispositivo junto con un historial de las invocaciones de método. Puede ver esta información acerca de los dispositivos e invocar métodos en el portal de solución de Hola.

Centro de IoT de toonotify Hola que un dispositivo es compatible con un método, dispositivo Hola debe agregar detalles de hello método toohello **SupportedMethods** nodo Hola notificado propiedades:

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

firma del método Hello tiene Hola siguiendo el formato: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`. Por ejemplo, toospecify hello **InitiateFirmwareUpdate** método espera un parámetro de cadena denominado **FwPackageURI**, usar hello después de la firma del método:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

Para obtener una lista de tipos de parámetro admitidos, vea hello **CommandTypes** clase en el proyecto de infraestructura de Hola.

toodelete un método, establezca la firma del método hello demasiado`null` Hola notificado propiedades.

> [!NOTE]
> Hello back-end de soluciones sólo actualiza la información sobre los métodos admitidos cuando recibe un *información del dispositivo* mensaje de Hola dispositivo.

Hola siguiente código de ejemplo de Hola **SampleDeviceFactory** clase Hola comunes de proyectos se muestra cómo tooadd una lista de toohello método de **SupportedMethods** Hola notificado propiedad enviada por hello dispositivo:

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

Este fragmento de código agrega detalles de hello **InitiateFirmwareUpdate** método incluidos toodisplay de texto en el portal de solución de Hola y los detalles del programa Hola a los parámetros de método necesarios.

simulador de Hello envía propiedades notificados, incluida la lista de Hola de métodos admitidos, tooIoT concentrador cuando se inicia el simulador de Hola.

Agregar un código de controlador toohello simulador para cada método que admite. Puede ver los controladores existentes Hola Hola **CoolerDevice** clase hello Simulator.WebJob proyecto. Hello en el ejemplo siguiente se muestra el controlador de hello para **InitiateFirmwareUpdate** método:

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

Los nombres de controlador de método deben empezar por `On` seguido Hola nombre del método hello. Hola **methodRequest** parámetro contiene cualquier parámetro pasado con la invocación del método hello de hello solución back-end. valor devuelto Hello debe ser una de tipo **tarea&lt;MethodResponse&gt;**. Hola **BuildMethodResponse** método de utilidad le ayudará a crear el valor devuelto de Hola.

Dentro de hello método controlador, se puede realizar:

- Iniciar una tarea asincrónica.
- Recuperar propiedades deseadas de hello *gemelas dispositivo* en Centro de IoT.
- Actualizar una única propiedad incluida con hello **SetReportedPropertyAsync** método Hola **CoolerDevice** clase.
- Actualizar varias propiedades notificados mediante la creación de un **TwinCollection** hello que realiza la llamada y la instancia **Transport.UpdateReportedPropertiesAsync** método.

Hello ejemplo de actualización de firmware anterior realiza Hola pasos:

- Comprobaciones de hello dispositivo es solicitud de actualización de firmware de tooaccept capaz de Hola.
- Inicia la operación de actualización de firmware de Hola de forma asincrónica y restablece la telemetría de hello cuando se completa la operación de Hola.
- Inmediatamente devuelve Hola "FirmwareUpdate aceptado" se aceptó la solicitud de Hola de tooindicate de mensaje por dispositivo de Hola.

### <a name="build-and-use-your-own-physical-device"></a>Creación y uso de dispositivos propios (físicos)

Hola [SDK de Azure IoT](https://github.com/Azure/azure-iot-sdks) proporcionan bibliotecas para conectar numerosos tipos de dispositivo (idiomas y sistemas operativos) en soluciones de IoT.

## <a name="modify-dashboard-limits"></a>Modificación de los límites de panel

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>Número de dispositivos que se muestran en la lista desplegable del panel

Hola predeterminado es 200. Puede cambiar este número en [DashboardController.cs][lnk-dashboard-controller].

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>Número de PIN toodisplay en control de mapa de Bing

Hola predeterminado es 200. Puede cambiar este número en [TelemetryApiController.cs][lnk-telemetry-api-controller-01].

### <a name="time-period-of-telemetry-graph"></a>Periodo del gráfico de telemetría

valor predeterminado de Hello es 10 minutos. Puede cambiar este valor en [TelmetryApiController.cs][lnk-telemetry-api-controller-02].

## <a name="manually-set-up-application-roles"></a>Configuración manual de los roles de aplicación

Hello siguiente procedimiento describe cómo tooadd **administración** y **ReadOnly** tooa de roles de aplicación configurado previamente la solución. Tenga en cuenta que las soluciones preconfiguradas aprovisionadas desde sitios de hello azureiotsuite.com ya incluyen hello **administración** y **ReadOnly** roles.

Los miembros de hello **ReadOnly** rol puede ver la lista de dispositivos de Hola y el panel de hello, pero no se permiten dispositivos tooadd, atributos de dispositivo de cambio o comandos de envío.  Los miembros de hello **administración** rol tiene funcionalidad de acceso completo tooall hello en solución de Hola.

1. Vaya toohello [portal de Azure clásico][lnk-classic-portal].
2. Seleccione **Active Directory**.
3. Haga clic en nombre de hello del inquilino de AAD de Hola que usó al aprovisionar la solución.
4. Haga clic en **Aplicaciones**.
5. Haga clic en el nombre de Hola de aplicación Hola que coincida con el nombre de la solución preconfigurada. Si no ve la aplicación en la lista de hello, seleccione **aplicaciones tiene mi compañía** en hello **mostrar** lista desplegable y haga clic en Hola marca de verificación.
6. En la parte inferior de Hola de página de hello, haga clic en **administrar manifiesto** y, a continuación, **descargar manifiesto**.
7. Este procedimiento descarga un equipo local de .json archivo tooyour. Abra este archivo para editarlo en el editor de texto que quiera.
8. En hello tercera línea del archivo .json de hello, puede ver:

   ```json
   "appRoles" : [],
   ```
   Reemplace esta línea con hello siguiente código:

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

9. Guarde el archivo de .json actualizada de hello (puede sobrescribir archivos existentes de hello).
10. Hola portal de Azure clásico, en parte inferior de Hola de página de hello, seleccione **administrar manifiesto** , a continuación, **cargar manifiesto** archivo .json tooupload Hola que guardó en el paso anterior de Hola.
11. Ya has agregado hello **administración** y **ReadOnly** aplicación tooyour de roles.
12. tooassign uno de estos usuarios tooa de roles en el directorio, consulte [permisos en el sitio de hello azureiotsuite.com][lnk-permissions].

## <a name="feedback"></a>Comentarios

¿Tiene una personalización que le gustaría toosee cubierta por este documento? Agregar sugerencias sobre características demasiado[User Voice](https://feedback.azure.com/forums/321918-azure-iot), o un comentario en este artículo. 

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de opciones de Hola para personalizar soluciones de hello preconfigurado, consulte:

* [Solución de Azure de supervisión remota de conjunto de IoT preconfigurado tooyour de aplicación lógica de conexión][lnk-logicapp]
* [Use la telemetría dinámica con hello solución preconfigurada de supervisión remota][lnk-dynamic]
* [Metadatos de información de dispositivo en hello solución preconfigurada de supervisión remota][lnk-devinfo]
* [Personalizar cómo Hola conectado generador solución muestra los datos de los servidores de OPC UA][lnk-cf-customize]

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