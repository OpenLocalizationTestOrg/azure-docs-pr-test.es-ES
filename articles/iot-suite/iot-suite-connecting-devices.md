---
title: aaaConnect un dispositivo mediante C en Windows | Documentos de Microsoft
description: "Describe cómo tooconnect una toohello dispositivo Azure IoT conjunto preconfigurado solución de supervisión remota con una aplicación escrita en C que se ejecutan en Windows."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>Conectar su toohello de dispositivo remoto de supervisión de solución preconfigurada (Windows)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>Creación de una solución de ejemplo de C en Windows
Hola pasos muestra cómo una aplicación cliente que se comunica con la supervisión remota de hello toocreate había preconfigurado solución. Esta aplicación se escribe en C y se compila y ejecuta en Windows.

Cree un proyecto de inicio en Visual Studio 2015 o Visual Studio de 2017 y agregue paquetes de NuGet de hello centro de IoT dispositivo cliente:

1. En Visual Studio, cree una aplicación de consola de C con Visual C++ hello **aplicación de consola Win32** plantilla. Proyecto de hello Name **RMDevice**.
2. En hello **configuración de la aplicación** página Hola **Asistente para aplicaciones Win32**, asegúrese de que **aplicación de consola** está seleccionada y desactive la opción **precompilado encabezado** y **comprobaciones del ciclo de vida de desarrollo de seguridad (SDL)**.
3. En **el Explorador de soluciones**, eliminar Hola archivos stdafx.h, targetver.h y stdafx.cpp.
4. En **el Explorador de soluciones**, cambie el nombre hello archivo RMDevice.cpp tooRMDevice.c.
5. En **el Explorador de soluciones**, haga doble clic en hello **RMDevice** del proyecto y, a continuación, haga clic en **administrar paquetes NuGet**. Haga clic en **examinar**, a continuación, buscar e instalar Hola siguientes paquetes de NuGet:
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport
6. En **el Explorador de soluciones**, haga doble clic en hello **RMDevice** del proyecto y, a continuación, haga clic en **propiedades** del proyecto de tooopen hello **páginas de propiedades**cuadro de diálogo. Para obtener información, consulte [Setting Visual C++ Project Properties][lnk-c-project-properties] (Establecimiento de propiedades de proyectos de Visual C++). 
7. Haga clic en hello **vinculador** carpeta, a continuación, haga clic en hello **entrada** página de propiedades.
8. Agregar **crypt32.lib** toohello **dependencias adicionales** propiedad. Haga clic en **Aceptar** y, a continuación, **Aceptar** valores de propiedad toosave Hola proyecto nuevo.

Agregar hello Parson JSON biblioteca toohello **RMDevice** del proyecto y agregue Hola necesario `#include` instrucciones:

1. En una carpeta adecuada en el equipo, clonar el repositorio de GitHub Parson de hello mediante Hola siguiente comando:

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Copie los archivos de parson.h y parson.c de Hola desde la copia local de Hola de hello Parson repositorio tooyour **RMDevice** carpeta del proyecto.

1. En Visual Studio, haga clic en hello **RMDevice** proyecto de equipo y haga clic en **agregar**y, a continuación, haga clic en **elemento existente**.

1. Hola **Agregar elemento existente** cuadro de diálogo, los archivos de parson.h y parson.c de select Hola Hola **RMDevice** carpeta del proyecto. A continuación, haga clic en **agregar** tooadd estos proyectos de tooyour dos archivos.

1. En Visual Studio, abra el archivo de hello RMDevice.c. Reemplazar existente hello `#include` instrucciones con hello siguiente código:
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > Ahora puede comprobar que el proyecto tiene dependencias correctas Hola configurar compilarlas.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Compilar y ejecutar el ejemplo hello

Agregar Hola de código tooinvoke **remoto\_supervisión\_ejecutar** función y, a continuación, compilar y ejecutar la aplicación de dispositivo de hello.

1. Reemplace hello **principal** función con hello de tooinvoke de código siguiente **remoto\_supervisión\_ejecutar** función:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Haga clic en **generar** y, a continuación, **generar solución** aplicación de dispositivo de hello toobuild.

1. En **el Explorador de soluciones**, contextual hello **RMDevice** proyecto de equipo y haga clic en **depurar**y, a continuación, haga clic en **Iniciar nueva instancia** toorun Hola ejemplo. consola de Hello muestra mensajes como hello aplicación envía ejemplo telemetría toohello preconfigurado solución, recibe los valores de propiedad establecidos en el panel de la solución de Hola y responde toomethods invocado desde el panel de la solución de Hola.

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
