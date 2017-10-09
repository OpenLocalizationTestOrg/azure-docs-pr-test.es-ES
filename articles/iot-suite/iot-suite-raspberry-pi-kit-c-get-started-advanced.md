---
title: aaaConnect un tooAzure frambuesa Pi Suite IoT mediante C toosupport firmware actualiza | Documentos de Microsoft
description: "Utilice hello IoT Starter Kit de Microsoft Azure para hello frambuesa Pi 3 y conjunto de IoT de Azure. Usar C tooconnect la solución de supervisión remota toohello de frambuesa Pi, enviar telemetría desde sensores toohello en la nube y realizar una actualización de firmware remoto."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a>Conectar la solución de supervisión remota toohello de frambuesa Pi 3 y habilitar las actualizaciones de firmware remotas mediante C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Este tutorial muestra cómo toouse Hola IoT Starter Kit de Microsoft Azure para frambuesa Pi 3 para:

* Desarrollar un lector de temperatura y humedad que puede comunicarse con la nube de Hola.
* Habilitar y realice una aplicación de cliente remoto firmware update tooupdate Hola Hola frambuesa Pi.

tutorial de Hello usa:

* Raspbian OS, lenguaje de programación de C de Hola y Hola IoT de Microsoft Azure SDK para C tooimplement un dispositivo de ejemplo.
* supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.

## <a name="overview"></a>Información general

En este tutorial, se realizará Hola pasos:

* Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure. Este paso implementa y configura varios servicios de Azure automáticamente.
* Configurar el dispositivo y sensores toocommunicate con el equipo y Hola remoto de solución de supervisión.
* Actualizar Hola ejemplo dispositivo código tooconnect toohello solución de supervisión y enviar telemetría que se puede ver en el panel de la solución de Hola.
* Usar dispositivos de ejemplo Hola código tooupdate Hola cliente aplicación.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure. implementación de Hello refleja una arquitectura empresarial real. tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él. Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente. Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Descargar y configurar el ejemplo hello

Ahora puede descargar y configurar la aplicación de cliente de supervisión remota de hello en el instalador de plataforma de frambuesa.

### <a name="clone-hello-repositories"></a>Clonar repositorios de Hola

Si aún no lo ha hecho lo ha hecho, Hola clon necesario repositorios ejecutando Hola siga los comandos en el instalador de plataforma:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Actualizar la cadena de conexión de dispositivo de Hola

Archivo de configuración de ejemplo de Hola abierto en hello **nano** editor mediante Hola siguiente comando:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Reemplazar los valores de marcador de posición de Hola por hello Id. y centro de IoT información del dispositivo ha creado y guardado en el inicio de Hola de este tutorial.

Cuando haya terminado, contenido de hello del archivo de deviceinfo hello debería ser similar Hola siguiente ejemplo:

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

Guarde los cambios (**O Ctrl**, **ENTRAR**) y salga del editor hello (**Ctrl-X**).

## <a name="build-hello-sample"></a>Compilar el ejemplo hello

Si no lo ha hecho ya, instale los paquetes de requisitos previos de Hola para hello SDK de dispositivos de IoT de Azure de Microsoft para C con hello siguiente comandos en un terminal de hello frambuesa Pi:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Ahora puede compilar la solución de ejemplo de Hola en hello frambuesa Pi:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

Ahora puede ejecutar el programa de ejemplo de Hola en hello frambuesa Pi. Escriba el comando de hello:

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

Hello resultados del ejemplo siguiente es un ejemplo de salida de hello, vea en línea de comandos de hello en hello frambuesa Pi:

![Salida de la aplicación Raspberry Pi][img-raspberry-output]

Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. En el panel de la solución de hello, haga clic en **dispositivos** toovisit hello **dispositivos** página. Seleccione el instalador de plataforma de frambuesa Hola **lista de dispositivos**. A continuación, elija **Métodos**:

    ![Lista de dispositivos en el panel][img-list-devices]

1. En hello **invocar método** página, elija **InitiateFirmwareUpdate** en hello **método** lista desplegable.

1. Hola **FWPackageURI** , escriba **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**. Este archivo contiene la implementación de hello de la versión 2.0 del firmware de Hola.

1. Elija **Invocar método**. aplicación de Hello en hello frambuesa Pi envía un panel de solución de toohello espera de confirmación. A continuación, inicia el proceso de actualización de firmware de hello descargando la nueva versión del firmware de Hola de hello:

    ![Mostrar el historial de métodos][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Observar el proceso de actualización de firmware de Hola

Puede observar el proceso de actualización de firmware de hello mientras se ejecuta en el dispositivo de Hola y viendo Hola notificado propiedades en el panel de la solución de hello:

1. Puede ver el progreso de hello en del proceso de actualización de hello en hello frambuesa Pi:

    ![Mostrar el progreso de la actualización][img-update-progress]

    > [!NOTE]
    > aplicación de supervisión remoto Hello en modo silencioso reinicia cuando se completa la actualización de Hola. Use el comando de hello `ps -ef` tooverify se está ejecutando. Si desea que el proceso de hello tooterminate, use hello `kill` comando con Id. de proceso de Hola.

1. Puede ver estado de Hola de actualización de firmware de hello, indicados por dispositivo de hello, en el portal de solución de Hola. Hello captura de pantalla siguiente muestra el estado de Hola y la duración de cada fase del proceso de actualización de hello y la nueva versión de firmware de hello:

    ![Mostrar estado del trabajo][img-job-status]

    Si navega toohello back-panel, puede comprobar dispositivo Hola todavía esté enviando telemetría después de la actualización de firmware de Hola.

> [!WARNING]
> Si deja Hola supervisión de solución que se ejecuta en su cuenta de Azure remota, se le facturará por vez Hola que se ejecuta. Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config]. Eliminar soluciones Hola preconfigurado de su cuenta de Azure cuando termine de usarlo.

## <a name="next-steps"></a>Pasos siguientes

Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md