---
title: aaaAzure IoT Suite y Logic Apps | Documentos de Microsoft
description: "Ver un tutorial sobre cómo toohook seguridad Logic Apps tooAzure IoT conjunto para el proceso empresarial."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>Tutorial: Conectar la solución de aplicación lógica tooyour Azure de supervisión remota de conjunto de IoT preconfigurado
Hola [Microsoft Azure IoT Suite] [ lnk-internetofthings] solución preconfigurada de supervisión remota es una excelente manera tooget a trabajar rápidamente con un conjunto de características de-to-end que ejemplifica una solución de IoT. Este tutorial le guía a través de la supervisión remota de tooadd aplicación lógica tooyour Microsoft Azure IoT Suite había preconfigurado solución. Estos pasos muestran cómo puede aprovechar aún más la solución de IoT conectándola tooa proceso de negocio.

*Si está pensando para ver un tutorial sobre cómo tooprovision una supervisión remota preconfigurado solución, consulte [Tutorial: Introducción a soluciones de IoT preconfigurado hello][lnk-getstarted].*

Antes de comenzar este tutorial, debe:

* Hola de aprovisionar solución preconfigurada en su suscripción de Azure de supervisión remoto.
* Crear un tooenable de cuenta de SendGrid toosend un correo electrónico que desencadena el proceso empresarial. Puede registrarse para obtener una cuenta de evaluación gratuita en [SendGrid](https://sendgrid.com/) haciendo clic en **Try for Free**(Probar gratis). Después de haber registrado para su cuenta de evaluación gratuita, debe toocreate una [clave de API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) en SendGrid que concede permisos toosend correo. Se necesita esta clave API más adelante en el tutorial de Hola.

toocomplete este tutorial, necesita Visual Studio 2015 o Visual Studio de 2017 acciones de hello toomodify en hello solución preconfigurada back-end.

Suponiendo que ya se ha aprovisionado la supervisión remota preconfigurado solución, vaya toohello el grupo de recursos para esa solución Hola [portal de Azure][lnk-azureportal]. grupo de recursos de Hello tiene Hola mismo nombre como hello solución el nombre eligió al aprovisionar la solución de supervisión remota. En el grupo de recursos de hello, puede ver aprovisionado de hello todos los recursos de Azure para su solución excepto Hola aplicación de Azure Active Directory que se puede encontrar en hello Portal clásico de Azure. Hello captura de pantalla siguiente muestra un ejemplo **grupo de recursos** hoja para una supervisión remota preconfigurado soluciones:

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, configurar toouse de aplicación lógica de hello con hello preconfigurado solución.

## <a name="set-up-hello-logic-app"></a>Configurar la aplicación lógica de Hola
1. Haga clic en **agregar** en parte superior de saludo de la hoja de grupo de recursos en hello portal de Azure.
2. Busque la **aplicación lógica**, selecciónela y, después, haga clic en **Crear**.
3. Rellene hello **nombre** y use Hola mismo **suscripción** y **grupo de recursos** que usó al aprovisionar la solución de supervisión remota. Haga clic en **Crear**.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. Cuando se completa la implementación, puede ver Hola que lógica de aplicación se muestra como un recurso en el grupo de recursos.
5. Haga clic en la hoja de aplicación lógica de toohello de toonavigate de aplicación lógica de hello, seleccione hello **en blanco de lógica de aplicación** Hola de plantilla tooopen **el Diseñador de aplicaciones de la lógica de**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. Seleccione **Solicitud**. Esta acción especifica que una solicitud HTTP entrante con una carga específica con formato de JSON actúa como desencadenador.
7. Pegue Hola siguiente código en hello esquema de JSON de cuerpo de solicitud:
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > Puede copiar dirección URL de Hola de publicación de hello HTTP después de guardar aplicación lógica de hello, pero primero debe agregar una acción.
   > 
   > 
8. Haga clic en **+ Nuevo paso** en el desencadenador manual. A continuación, haga clic en **Agregar una acción**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. Busque la opción **SendGrid - Send email** (SendGrid: enviar correo electrónico) y haga clic en ella.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. Escriba un nombre para la conexión de hello, como **SendGridConnection**, escriba Hola **clave de API de SendGrid** que creó al configurar la cuenta de SendGrid y haga clic en **crear**.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. Agregar direcciones de correo electrónico tooboth propio hello **de** y **a** campos. Agregar **alerta de supervisión remota [DeviceId]** toohello **asunto** campo. Hola **cuerpo del correo electrónico** , a continuación, agregar **ha informado de dispositivo [DeviceId] [measurementName] con el valor [measuredValue].** Puede agregar **[DeviceId]**, **[measurementName]**, y **[measuredValue]** haciendo clic en hello **puede insertar datos de los pasos anteriores**sección.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. Haga clic en **guardar** en el menú superior Hola.
13. Haga clic en hello **solicitar** desencadenador y copia hello **dirección URL de Http Post toothis** valor. Necesitará esta URL más adelante en el tutorial.

> [!NOTE]
> Las aplicaciones lógicas le permiten toorun [muchos tipos diferentes de acción] [ lnk-logic-apps-actions] incluidas acciones en Office 365. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>Configurar hello EventProcessor Web trabajo
En esta sección, se conecta la aplicación lógica que creó toohello de solución preconfigurada. toocomplete esta tarea, agregará hello tootrigger Hola aplicación lógica toohello acción de dirección URL que se desencadena cuando un valor del sensor de dispositivo supera un umbral.

1. Use la git tooclone Hola última versión del cliente de hello [azure iot-remoto-supervisión de repositorio de github][lnk-rmgithub]. Por ejemplo:
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. En Visual Studio, abra hello **RemoteMonitoring.sln** desde la copia local de hello del repositorio de Hola.
3. Abra hello **ActionRepository.cs** archivo Hola **infraestructura\\repositorio** carpeta.
4. Hola de actualización **actionIds** diccionario con hello **dirección URL de Http Post toothis** que anotó desde la aplicación lógica como sigue:
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. Guardar los cambios de hello en la solución y salga de Visual Studio.

## <a name="deploy-from-hello-command-line"></a>Implementar desde la línea de comandos de Hola
En esta sección, se implementa la versión actualizada de hello supervisión solución tooreplace Hola versión remota está ejecutando actualmente en Azure.

1. Después de hello [dev instalación] [ lnk-devsetup] tooset de instrucciones del entorno para la implementación.
2. toodeploy localmente, siga hello [implementación local] [ lnk-localdeploy] instrucciones.
3. toodeploy toohello en la nube y actualizar la implementación de nube existente, siga hello [implementación de nube] [ lnk-clouddeploy] instrucciones. Usar el nombre de saludo de la implementación original como nombre de la implementación de Hola. Por ejemplo, si se llamara a implementación original de hello **demologicapp**, usar hello siguiente comando:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   Cuando Hola compila el script se ejecuta, asegúrese de toouse Hola misma cuenta de Azure, suscripción, región e instancia de Active Directory que usó al aprovisionar solución Hola.

## <a name="see-your-logic-app-in-action"></a>La aplicación lógica en acción
Hola remoto solución preconfigurada de supervisión tiene dos reglas configuradas de forma predeterminada al aprovisionar una solución. Ambas reglas se encuentran en hello **SampleDevice001** dispositivo:

* Temperature > 38.00 (Temperatura > 38,00)
* Humidity > 48.00 (Humedad > 48,00)

regla de temperatura de Hello desencadena hello **generar alarma** hello y acción de regla de humedad desencadena hello **SendMessage** acción. Suponiendo que utilizaran Hola misma dirección URL para ambos hello acciones **ActionRepository** de la clase, los desencadenadores de aplicación lógica para cualquiera de ellas. Ambas reglas usan SendGrid toosend un correo electrónico toohello **a** dirección con detalles de alerta de Hola.

> [!NOTE]
> Hola aplicación lógica continúa tootrigger cada vez que se alcanza el umbral de Hola. tooavoid de los correos electrónicos innecesarios, o bien puede deshabilitar las reglas de hello en su solución portal o deshabilitar Hola aplicación lógica en hello [portal de Azure][lnk-azureportal].
> 
> 

Además tooreceiving de mensajes de correo electrónico, también puede ver cuando Hola lógica de aplicación se ejecuta en el portal de hello:

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha usado un proceso de negocio de tooa de solución de aplicación lógica tooconnect Hola preconfigurado, puede aprender más acerca de las opciones de Hola para personalizar soluciones de hello preconfigurado:

* [Use la telemetría dinámica con hello solución preconfigurada de supervisión remota][lnk-dynamic]
* [Metadatos de información de dispositivo en hello solución preconfigurada de supervisión remota][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
