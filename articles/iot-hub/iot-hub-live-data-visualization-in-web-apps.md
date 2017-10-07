---
title: "Visualización de los datos de sensor desde el centro de IoT de Azure: aplicaciones Web aaaReal tiempo | Documentos de Microsoft"
description: "Usar la característica de las aplicaciones Web de Hola de servicio de aplicaciones de Microsoft Azure toovisualize temperatura y humedad datos que se recopila del sensor de Hola y envía el centro de Iot tooyour."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualización de datos en tiempo real, visualización de datos en directo, visualización de datos de sensor"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>Visualizar datos de sensor en tiempo real desde su centro de IoT de Azure mediante la característica de las aplicaciones Web de Hola de servicio de aplicaciones de Azure

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Conocimientos que adquirirá

En este tutorial, aprenderá cómo toovisualize datos de sensor en tiempo real que recibe de su centro de IoT mediante la ejecución de una aplicación web que se hospedan en una aplicación web. Si desea datos de tootry toovisualize hello en el centro de IoT mediante el uso de Power BI, consulte [datos de sensor en tiempo real de toovisualize Use Power BI desde el centro de IoT de Azure](iot-hub-live-data-visualization-in-power-bi.md).

## <a name="what-you-do"></a>Qué debe hacer

- Crear una aplicación web en hello portal de Azure.
- Preparar el IoT Hub para el acceso a datos mediante la adición de un grupo de consumidores.
- Configurar datos de sensor de hello web app tooread desde el centro de IoT.
- Cargar una toobe de aplicación web hospedada por la aplicación web de hello.
- Abrir hello web toosee en tiempo real temperatura y humedad datos de la aplicación desde el centro de IoT.

## <a name="what-you-need"></a>Lo que necesita

- [Configurar el dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md), donde abordan las Hola según los requisitos:
  - Una suscripción de Azure activa.
  - Un IoT Hub en su suscripción.
  - Una aplicación cliente que envía el centro de Iot tooyour de mensajes
- [Descargar Git](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a>Creación de una aplicación web

1. Hola [portal de Azure](https://ms.portal.azure.com/), haga clic en **New** > **Web y móvil** > **aplicación Web**.
2. Escriba un nombre de trabajo único, compruebe la suscripción de hello, especifique un grupo de recursos y una ubicación, seleccione **Pin toodashboard**y, a continuación, haga clic en **crear**.

   Le recomendamos que seleccione Hola misma ubicación que el grupo de recursos. Si lo hace, ayuda con la velocidad de procesamiento y reduce el costo de Hola de transferencia de datos.

   ![Creación de una aplicación web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>Configurar datos de tooread la aplicación hello web desde el centro de IoT

1. Abra la aplicación web de hello que acaba de aprovisionar.
2. Haga clic en **configuración de la aplicación**y, a continuación, en **configuración de la aplicación**, agregar Hola después de pares clave/valor:

   | Clave                                   | Valor                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | Obtenido de iothub-explorer                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | nombre de Hello del grupo de consumidores de Hola que agregue tooyour centro de IoT  |

   ![Agregar la aplicación web de configuración tooyour con pares clave/valor](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. Haga clic en **configuración de la aplicación**, en **configuración General**, Hola de alternancia **Web sockets** opción y, a continuación, haga clic en **guardar**.

   ![Alternar hello Web sockets, opción](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>Cargar una toobe de aplicación web hospedada por la aplicación web de hello

Hemos facilitado el acceso a una aplicación web en GitHub que muestra datos del sensor en tiempo real desde su IoT Hub. Todo lo que necesita toodo es configurar hello web app toowork con un repositorio Git, descargar la aplicación web de hello desde GitHub y, a continuación, cargarlo tooAzure para toohost de aplicación web de Hola.

1. En la aplicación web de hello, haga clic en **opciones de implementación** > **Elegir origen** > **repositorio de Git Local**y, a continuación, haga clic en **Aceptar**.

   ![Configurar el repositorio de Git web app deployment toouse Hola local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. Haga clic en **las credenciales de implementación**, cree un usuario nombre y la contraseña toouse tooconnect toohello repositorio de Git en Azure y, a continuación, haga clic en **guardar**.

3. Haga clic en **Introducción**y anote el valor de Hola de **url de clonación de Git**.

   ![Obtener la dirección URL de clonación de Git de saludo de la aplicación web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. Abra una ventana de comando o de terminal en el equipo local.

5. Descargar la aplicación web de hello desde GitHub y cargarlo tooAzure para toohost de aplicación web de Hola. toodo es así, ejecute hello comandos siguientes:

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<Dirección URL de clonación de GIT\> es Hola URL del repositorio de Git Hola se encuentra en hello **Introducción** página de aplicación web de hello.

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>Abrir hello web toosee en tiempo real temperatura y humedad datos de la aplicación desde el centro de IoT

En hello **Introducción** página de la aplicación web, haga clic en aplicación web de hello URL tooopen Hola.

![Obtener dirección URL de saludo de la aplicación web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

Debería ver datos de humedad y temperatura de hello en tiempo real desde el centro de IoT.

![Página de aplicación web que muestra la temperatura y humedad en tiempo real](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> Asegúrese de que está ejecutando la aplicación de ejemplo de Hola en el dispositivo. Si no es así, obtendrá un gráfico en blanco, puede consultar toohello tutoriales en [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).

## <a name="next-steps"></a>Pasos siguientes
Ha usado correctamente los datos de sensor en tiempo real de toovisualize de aplicación web de su centro de IoT.

Para un forma alternativa toovisualize los datos desde el centro de IoT de Azure, consulte [datos de sensor en tiempo real de toovisualize Use Power BI desde el centro de IoT](iot-hub-live-data-visualization-in-power-bi.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
