---
title: aaaConnect un dispositivo mediante C en mbed | Documentos de Microsoft
description: "Describe cómo tooconnect una toohello dispositivo Azure IoT conjunto preconfigurado solución de supervisión remota con una aplicación escrita en C utilizando un dispositivo de mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>Conectar su toohello de dispositivo remoto de supervisión de solución preconfigurada (mbed)

## <a name="scenario-overview"></a>Información general de escenario
En este escenario, se crea un dispositivo que envía Hola después de supervisión remota de telemetría toohello [preconfigurado solución][lnk-what-are-preconfig-solutions]:

* Temperatura exterior
* Temperatura interior
* Humedad

Para simplificar, valores de ejemplo genera el código de hello en dispositivo hello, pero recomendamos ejemplo Hola tooextend: conectar dispositivo tooyour de sensores real y enviar telemetría real.

dispositivo de Hello también es toomethods toorespond puede invocar desde el panel de la solución de Hola y desea valores de propiedad establecidos en el panel de la solución de Hola.

toocomplete este tutorial, necesita una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].

## <a name="before-you-start"></a>Antes de comenzar
Antes de escribir ningún código para el dispositivo, debe aprovisionar la solución preconfigurada de supervisión remota y aprovisionar un nuevo dispositivo personalizado en esa solución.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Aprovisionar su solución preconfigurada de supervisión remota
dispositivo de Hola que creará en este tutorial envía la instancia de datos de tooan de hello [supervisión remota] [ lnk-remote-monitoring] preconfigurado solución. Si aún no aprovisionada Hola supervisión solución preconfigurada en su cuenta de Azure remota, use Hola pasos:

1. En hello <https://www.azureiotsuite.com/> página, haga clic en  **+**  toocreate una solución.
2. Haga clic en **seleccione** en hello **supervisión remota** panel toocreate la solución.
3. En hello **crear remoto solución de supervisión** página, escriba un **nombre de la solución** de su elección, seleccione hello **región** desee toodeploy a y seleccione hello Azure suscripción toowant toouse. Haga clic en **Crear solución**.
4. Espere hasta que se complete el proceso de aprovisionamiento de Hola.

> [!WARNING]
> las soluciones de Hello preconfigurado usan los servicios de Azure facturables. Asegúrese de tooremove Hola solución preconfigurada de la suscripción cuando haya terminado con él tooavoid los cargos innecesarios. Puede quitar completamente una solución preconfigurada de su suscripción visitando hello <https://www.azureiotsuite.com/> página.
> 
> 

Cuando finalice el proceso para hello remoto de solución de supervisión de aprovisionamiento de hello, haga clic en **iniciar** tooopen panel de solución de hello en el explorador.

![Panel de soluciones][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Aprovisionar el dispositivo en hello remoto de solución de supervisión
> [!NOTE]
> Si ya ha aprovisionado un dispositivo en la solución, puede omitir este paso. Necesita credenciales de dispositivo de hello tooknow cuando se crea la aplicación de cliente de Hola.
> 
> 

Para una solución de toohello preconfigurado tooconnect de dispositivo, debe identificarse tooIoT concentrador con credenciales válidas. Puede recuperar las credenciales del dispositivo Hola de panel de la solución de Hola. Incluye las credenciales del dispositivo hello en la aplicación de cliente más adelante en este tutorial.

tooadd una solución de supervisión remota de tooyour de dispositivo, Hola completa siguiendo los pasos en el panel de la solución de hello:

1. En hello esquina izquierda inferior del panel de hello, haga clic en **agregar un dispositivo**.
   
   ![Agregar un dispositivo][1]
2. Hola **dispositivo personalizado** del panel, haga clic en **agregar nueva**.
   
   ![Agregar un dispositivo personalizado][2]
3. Elija **Permitirme definir mi propio id. de dispositivo**. Escriba un Id. de dispositivo como **mydevice**, haga clic en **Check ID** tooverify ese nombre no está en uso y, a continuación, haga clic en **crear** dispositivo de tooprovision Hola.
   
   ![Agregar id. de dispositivo][3]
4. Hacer que un dispositivo de hello tenga en cuenta las credenciales (Id. de dispositivo, el nombre de host de IoT Hub y clave de dispositivo). La aplicación cliente necesita estos toohello de tooconnect valores remoto de solución de supervisión. A continuación, haga clic en **Hecho**.
   
    ![Ver las credenciales del dispositivo][4]
5. Seleccione el dispositivo en la lista de dispositivos de hello en el panel de la solución de Hola. A continuación, en hello **detalles del dispositivo** del panel, haga clic en **Habilitar dispositivo**. Hola estado del dispositivo es ahora **ejecutando**. solución de supervisión remoto Hello ahora puede reciba datos de telemetría del dispositivo e invocar métodos de dispositivo de Hola.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>Compilar y ejecutar la solución de ejemplo de Hola C

Hello las instrucciones siguientes describen los pasos de Hola para conectar un [habilitado mbed Freescale FRDM-K64F] [ lnk-mbed-home] toohello de dispositivo remoto de solución de supervisión.

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>Conectar el dispositivo de la red de tooyour hello mbed y máquina de escritorio

1. Conectar red del dispositivo tooyour de hello mbed mediante un cable Ethernet. Este paso es necesario porque la aplicación de ejemplo de Hola requiere acceso a internet.

1. Vea [Getting Started with mbed] [ lnk-mbed-getstarted] tooconnect mbed dispositivo tooyour escritorio PC.

1. Si su PC de escritorio se ejecuta Windows, vea [configuración de PC] [ lnk-mbed-pcconnect] tooyour mbed dispositivo de tooconfigure puerto serie acceso.

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>Crear un proyecto mbed e importar el código de ejemplo de Hola

Siga estos pasos tooadd algún proyecto de mbed de tooan de código de ejemplo. Importar el proyecto de inicio de supervisión remota de Hola y cambie hello toouse de proyecto Hola protocolo MQTT en lugar de hello protocolo AMQP. Actualmente, debe toouse hello MQTT protocolo toouse Hola dispositivo características de administración de centro de IoT.

1. En el explorador web, vaya toohello mbed.org [sitio para desarrolladores de](https://developer.mbed.org/). Si no se haya registrado, verá un toocreate opción una cuenta (no disponible). De lo contrario, inicie sesión con las credenciales de su cuenta. A continuación, haga clic en **compilador** en hello superior derecha de la página de Hola. Esta acción pone toohello *área de trabajo* interfaz.

1. Asegúrese de que la plataforma de hardware de hello usa aparece en hello la esquina superior derecha de la ventana hello, o haga clic en icono de hello en hello esquina derecha tooselect su plataforma de hardware.

1. Haga clic en **importación** en el menú principal de Hola. A continuación, haga clic en **haga clic aquí tooimport de dirección URL**.
   
    ![Iniciar el área de trabajo de importación toombed][6]

1. En la ventana emergente de hello, especifique el vínculo de Hola Hola ejemplo código https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, a continuación, haga clic en **importación**.
   
    ![Importar el área de trabajo de toombed de código de ejemplo][7]

1. Puede ver en la ventana de compilador de hello mbed que importar este proyecto, también importa varias bibliotecas. Algunas son proporcionados y mantenidos por el equipo de Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), mientras que otros están disponibles en el catálogo de hello mbed bibliotecas de bibliotecas de otros fabricantes.
   
    ![Visualización del proyecto de mbed][8]

1. Hola **área de trabajo de programa**, contextual hello **el centro de IOT\_amqp\_transporte** biblioteca, haga clic en **eliminar**y, a continuación, haga clic en **Aceptar** tooconfirm.

1. Hola **área de trabajo de programa**, contextual hello **azure\_amqp\_c** biblioteca, haga clic en **eliminar**y, a continuación, haga clic en **Aceptar**  tooconfirm.

1. Menú contextual hello **remote_monitoring** proyecto Hola **área de trabajo de programa**, seleccione **biblioteca de importación**, a continuación, seleccione **From URL**.
   
    ![Iniciar el área de trabajo de biblioteca importación toombed][6]

1. En la ventana emergente de hello, especifique el vínculo de Hola Hola MQTT transporte biblioteca https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_de transporte y, a continuación, haga clic en **importación**.
   
    ![Importar el área de trabajo de biblioteca toombed][12]

1. Hola repetición anterior paso tooadd hello MQTT biblioteca de https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. El área de trabajo ahora Hola siguiente aspecto:

    ![Visualización de área de trabajo de mbed][13]

1. Abra Hola remoto\_monitoring\remote_monitoring.c archivo y reemplazar Hola existente `#include` instrucciones con hello siguiente código:

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. Eliminar Hola todas las restantes código de hello remoto\_monitoring\remote\_monitoring.c archivo.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Compilar y ejecutar el ejemplo hello

Agregar Hola de código tooinvoke **remoto\_supervisión\_ejecutar** función y, a continuación, compilar y ejecutar la aplicación de dispositivo de hello.

1. Agregar un **principal** función con el código siguiente al final de Hola de hello remoto\_Hola de monitoring.c archivo tooinvoke **remoto\_supervisión\_ejecutar** función:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Haga clic en **compilar** programa Hola de toobuild. Sin ningún riesgo puede pasar por alto las advertencias, pero si la compilación de hello genera errores, corríjalos antes de continuar.

1. Si Hola compilación es correcta, sitio Web de hello mbed compilador genera un archivo .bin con nombre hello del proyecto y lo descarga en la máquina local tooyour. Dispositivo de copia Hola .bin archivo toohello. Guardar Hola .bin archivo toohello dispositivo hace Hola dispositivo toorestart y ejecuta programa Hola contenido en el archivo .bin Hola. Programa hello, puede reiniciar manualmente en cualquier momento presionando el botón de restablecimiento de hello en dispositivo de mbed Hola.

1. Conecte el dispositivo toohello con una aplicación de cliente SSH como PuTTY. Puede determinar el puerto serie hello que usa el dispositivo mediante la comprobación de administrador de dispositivos de Windows.
   
    ![][11]

1. En PuTTY, haga clic en hello **serie** tipo de conexión. dispositivo de Hello normalmente se conecta a 9600 baudios, por lo que escriba 9600 en hello **velocidad** cuadro. A continuación, haga clic en **Abrir**.

1. programa Hello empieza a ejecutarse. Puede tener placa de hello tooreset (presione CTRL+pausa o botón de restablecimiento del panel presione hello) si programa hello no se inicia automáticamente cuando se conecta.
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
