---
title: Conectar un dispositivo con C en mbed | Microsoft Docs
description: "Se describe cómo conectar un dispositivo a la solución de supervisión remota preconfigurada del Conjunto de IoT de Azure mediante una aplicación creada en C que se ejecuta en un dispositivo de mbed."
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
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a>Conectar el dispositivo a la solución preconfigurada de supervisión remota (mbed)

## <a name="scenario-overview"></a>Información general de escenario
En este escenario, creará un dispositivo que envía la siguiente telemetría a la [solución preconfigurada][lnk-what-are-preconfig-solutions] de supervisión remota:

* Temperatura exterior
* Temperatura interior
* Humedad

Para simplificar, el código del dispositivo genera valores de ejemplo, pero le recomendamos que amplíe el ejemplo conectando sensores reales a su dispositivo y enviando telemetría real.

El dispositivo también puede responder a los métodos que se invocan desde el panel de la solución y los valores de propiedades deseadas establecidos en el panel de la solución.

Para completar este tutorial, deberá tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].

## <a name="before-you-start"></a>Antes de comenzar
Antes de escribir ningún código para el dispositivo, debe aprovisionar la solución preconfigurada de supervisión remota y aprovisionar un nuevo dispositivo personalizado en esa solución.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Aprovisionar su solución preconfigurada de supervisión remota
El dispositivo que cree en este tutorial enviará datos a una instancia de la solución preconfigurada de [supervisión remota][lnk-remote-monitoring]. Si todavía no aprovisionó la solución preconfigurada de supervisión remota en su cuenta de Azure, use estos pasos:

1. En la página <https://www.azureiotsuite.com/>, haga clic en **+** para crear una solución.
2. Haga clic en **Seleccionar** en el panel de **supervisión remota** para crear la solución.
3. En la página **Create Remote monitoring solution** (Crear solución de supervisión remota), escriba el **nombre de solución** que prefiera, seleccione la **región** en la que desea realizar la implementación y seleccione la suscripción de Azure que desea usar. Haga clic en **Crear solución**.
4. Espere a que finalice el proceso de aprovisionamiento.

> [!WARNING]
> Las soluciones preconfiguradas utilizan servicios de Azure facturables. Para evitar gastos innecesarios, asegúrese de quitar la solución preconfigurada de la suscripción cuando haya terminado. Para quitar completamente una solución preconfigurada de su suscripción, diríjase a la página <https://www.azureiotsuite.com/>.
> 
> 

Cuando finalice el proceso de aprovisionamiento para la solución de supervisión remota, haga clic en **Iniciar** para abrir el panel de la solución en el explorador.

![Panel de soluciones][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a>Aprovisionar el dispositivo en la solución de supervisión remota
> [!NOTE]
> Si ya ha aprovisionado un dispositivo en la solución, puede omitir este paso. Debe conocer las credenciales del dispositivo cuando cree la aplicación cliente.
> 
> 

Para que un dispositivo se conecte a la solución preconfigurada, debe identificarse en el Centro de IoT con credenciales válidas. Puede recuperar las credenciales del dispositivo desde el panel de la solución. Incluirá las credenciales del dispositivo en la aplicación de cliente más adelante en este tutorial.

Para agregar un dispositivo a su solución de supervisión remota, complete los pasos siguientes en el panel de la solución:

1. En la esquina inferior izquierda del panel, haga clic en **Agregar un dispositivo**.
   
   ![Agregar un dispositivo][1]
2. En el panel **Dispositivo personalizado**, haga clic en **Agregar nuevo**.
   
   ![Agregar un dispositivo personalizado][2]
3. Elija **Permitirme definir mi propio id. de dispositivo**. Especifique un id. de dispositivo, como **mydevice**, haga clic en **Comprobar id.** para comprobar que el nombre todavía no está en uso y, luego, haga clic en **Crear** para aprovisionar el dispositivo.
   
   ![Agregar id. de dispositivo][3]
4. Anote las credenciales de dispositivo (id. de dispositivo, nombre de host de IoT Hub y clave de dispositivo). La aplicación cliente necesita estos valores para conectarse con la solución de supervisión remota. A continuación, haga clic en **Hecho**.
   
    ![Ver las credenciales del dispositivo][4]
5. Seleccione el dispositivo en la lista de dispositivos del panel de la solución. Luego, en el panel **Detalles del dispositivo**, haga clic en **Habilitar dispositivo**. El estado del dispositivo ahora es **En ejecución**. La solución de supervisión remota ahora puede recibir telemetría desde el dispositivo e invocar métodos en el dispositivo.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a>Compilación y ejecución de la solución de ejemplo de C

Las instrucciones siguientes describen los pasos para conectar un dispositivo [Freescale FRDM-K64F habilitado para mbed][lnk-mbed-home] a la solución de supervisión remota.

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a>Conexión del dispositivo mbed a la máquina de escritorio y a la red

1. Conecte el dispositivo mbed a la red mediante un cable Ethernet. Este paso es necesario porque la aplicación de ejemplo requiere acceso a Internet.

1. Vea [Introducción a mbed][lnk-mbed-getstarted] para conectar el dispositivo de mbed al equipo de escritorio.

1. Si el equipo de escritorio está ejecutando Windows, vea [Configuración del equipo][lnk-mbed-pcconnect] para configurar el acceso al puerto serie para el dispositivo mbed.

### <a name="create-an-mbed-project-and-import-the-sample-code"></a>Crear un proyecto de mbed e importar el código de ejemplo

Siga estos pasos para agregar algún código de ejemplo a un proyecto de mbed. Importará el proyecto de inicio de supervisión remota y luego cambiará el proyecto para usar el protocolo MQTT en lugar del protocolo AMQP. Actualmente, debe emplear el protocolo MQTT para usar las características de administración de dispositivos de IoT Hub.

1. En el explorador web, vaya al [sitio para desarrolladores](https://developer.mbed.org/)mbed.org. Si aún no se ha registrado, verá una opción para crear una cuenta (es gratuita). De lo contrario, inicie sesión con las credenciales de su cuenta. Luego haga clic en **Compilador** en la esquina superior derecha de la página. Al realizar esta acción, se mostrará la interfaz *Área de trabajo*.

1. Asegúrese de que la plataforma de hardware que está usando aparezca en la esquina superior derecha de la ventana, o bien haga clic en el icono de la esquina derecha para seleccionar la plataforma de hardware.

1. Haga clic en **Importar** en el menú principal. A continuación, haga clic en **Click here to import from URL** (Haga clic aquí para importar desde la dirección URL).
   
    ![Inicio de la importación al área de trabajo de mbed][6]

1. En la ventana emergente, escriba el vínculo al código de ejemplo https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ y, después, haga clic en **Importar**.
   
    ![Importación del código de ejemplo al área de trabajo de mbed][7]

1. Puede ver en la ventana del compilador de mbed que se importaron varias bibliotecas durante la importación de este proyecto. El equipo de IoT de Azure ofrece y mantiene algunas bibliotecas ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), mientras que otras son bibliotecas de terceros que están disponibles en el catálogo de bibliotecas de mbed.
   
    ![Visualización del proyecto de mbed][8]

1. En el **área de trabajo de programa**, haga clic con el botón derecho en la biblioteca **iothub\_amqp\_transport**, haga clic en **Delete** (Eliminar) y luego en **OK** (Aceptar) para confirmar.

1. En el **área de trabajo de programa**, haga clic con el botón derecho en la biblioteca **azure\_amqp\_c**, haga clic en **Delete** (Eliminar) y luego en **OK** (Aceptar) para confirmar.

1. Haga clic con el botón derecho en el proyecto **remote_monitoring** en el **área de trabajo de programa**, seleccione **Import Library** (Importar biblioteca) y luego seleccione **From URL** (Desde dirección URL).
   
    ![Inicio de la importación de la biblioteca al área de trabajo de mbed][6]

1. En la ventana emergente, especifique el vínculo de la biblioteca de transporte de MQTT https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ y luego haga clic en **Import** (Importar).
   
    ![Importación de la biblioteca al área de trabajo de mbed][12]

1. Repita el paso anterior para agregar la biblioteca MQTT desde https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.

1. El área de trabajo se parece ahora a esta:

    ![Visualización de área de trabajo de mbed][13]

1. Abra el archivo remote\_monitoring\remote_monitoring.c y sustituya las instrucciones `#include` existentes por el código siguiente:

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
1. Elimine el resto de código del archivo remote\_monitoring\remote\_monitoring.c.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a>Compilación y ejecución del ejemplo

Agregue código para invocar la función **remote\_monitoring\_run** y luego compile y ejecute la aplicación del dispositivo.

1. Agregue una función **main** con el código siguiente al final del archivo remote\_monitoring.c para invocar la función **remote\_monitoring\_run**:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Haga clic en **Compilar** para compilar el programa. Puede omitir con seguridad las advertencias, pero si la compilación genera errores, corríjalos antes de continuar.

1. Si la compilación es correcta, el sitio web del compilador de mbed genera un archivo .bin con el nombre del proyecto y lo descarga en el equipo local. Copie el archivo .bin en el dispositivo. Si guarda el archivo .bin en el dispositivo, este último se reiniciará y ejecutará el programa incluido en el archivo .bin. Puede reiniciar manualmente el programa en cualquier momento presionando el botón Restablecer en el dispositivo mbed.

1. Conecte con el dispositivo mediante una aplicación cliente de SSH, como PuTTY. Puede determinar el puerto serie que usa el dispositivo comprobando el Administrador de dispositivos de Windows.
   
    ![][11]

1. En PuTTY, haga clic en el tipo de conexión **serie** . Como el dispositivo normalmente se conecta a 9600 baudios, especifique 9600 en el cuadro **Velocidad** . A continuación, haga clic en **Abrir**.

1. El programa comienza a ejecutarse. Si el programa no se inicia automáticamente al conectarse, puede que tenga que restablecer la placa (presione CTRL+Pausa o pulse el botón de reinicio de la placa).
   
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
