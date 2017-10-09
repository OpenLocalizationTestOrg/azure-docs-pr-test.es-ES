---
title: aaaIoT DevKit toocloud - conectar IoT DevKit AZ3166 tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conéctese de plataforma de nube de Azure de toosend datos toohello IoT DevKit AZ3166 tooAzure centro de IoT para él en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>Conectar IoT DevKit AZ3166 tooAzure centro de IoT en nube Hola

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Hola [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) pueden ser usado toodevelop y prototipo soluciones de Internet de las cosas (IoT) aprovechan los servicios de Microsoft Azure. Incluye una placa compatible con Arduino con periféricos y sensores enriquecidos, un paquete de panel de código abierto y un [catálogo proyectos](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) en aumento.

## <a name="what-you-do"></a>Qué debe hacer
Conectar [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan centro de IoT de Azure que cree, Hola recopilar los datos de temperatura y humedad de sensores y enviar tooIoT concentrador de Hola de datos.

¿Aún no tiene un DevKit? Obtenga uno nuevo [aquí](https://aka.ms/iot-devkit-purchase).

## <a name="what-you-learn"></a>Conocimientos que adquirirá

* ¿Cómo tooconnect IoT DevKit tooWireless acceso elija y preparar el entorno de desarrollo.
* ¿Cómo toocreate un centro de IoT y registrar un dispositivo para MXChip IoT DevKit.
* ¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en MXChip IoT DevKit.
* ¿Cómo toosend Hola centro de IoT de tooyour de datos de sensor.

## <a name="what-you-need"></a>Lo que necesita

* Una placa MXChip IoT DevKit con un cable microUSB. [Obténgalo ahora](https://aka.ms/iot-devkit-purchase)
* Un equipo con Windows 10 o macOS 10.10+
* Una suscripción de Azure activa.
  * Active una [cuenta de Microsoft Azure de prueba de 30 días gratis](https://azureinfo.microsoft.com/us-freetrial.html)

## <a name="prepare-your-hardware"></a>Preparar el hardware

Enlazar equipo tooyour de hello hardware.

### <a name="hardware-you-need"></a>Hardware que necesita

* Placa DevKit
* Cable microUSB

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>Conectar el equipo de tooyour DevKit

1. Conectar USB final tooyour PC
2. Conectar Micro USB final toohello DevKit
3. Hola verde LED siguiente toopower confirma la conexión

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>Configuración de la red WiFi

Los proyectos de IoT se basan en la conectividad a Internet. Usar hello siguiendo las instrucciones tooconfigure hello DevKit tooconnect tooWiFi.

### <a name="enter-ap-mode"></a>Entrada al modo AP

Mantenga presionado el botón B, a continuación, insertar y suelte el botón de restablecimiento de hello y, a continuación, versión botón B. Su DevKit pasará al modo de punto de acceso para la configuración de Wi-Fi. pantalla de bienvenida mostrará Hola servicio establecer Identifier(SSID) de hello DevKit, así como la dirección IP del portal de configuración de hello:

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>Conectar tooDevKit PA

Ahora, use otro Wi-Fi habilitado dispositivos (PC o un teléfono móvil) tooconnect toohello SSID DevKit (resaltado en la captura de pantalla de hello anterior), deje Hola contraseña vacía.

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>Configuración de la red WiFi para DevKit

Dirección IP de hello abierta se muestra en la pantalla de bienvenida DevKit en su PC o el Explorador de teléfono móvil, seleccione red Wi-Fi de hello desea hello DevKit tooconnect para, a continuación, escriba Hola contraseña. Haga clic en **conectar** toocomplete:

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Cuando se complete correctamente la conexión de hello, hello DevKit se reiniciará en unos segundos. Si se realizó correctamente, verá Hola Wi-Fi nombre y dirección IP en la pantalla de bienvenida:

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
dirección IP de Hello muestra de foto de hello no puede coincidir con hello real IP asigna y se muestran en la pantalla de bienvenida DevKit. Esto es normal que utilizan Wi-Fi toodynamically DHCP asignar direcciones IP.

Después de configura la red Wi-Fi, sus credenciales se conservarán en el dispositivo de Hola para esa conexión, incluso si desconectado. Por ejemplo, si configurado hello DevKit para Wi-Fi en su hogar y, a continuación, tardó office de hello DevKit toohello, necesitará tooreconfigure PA modo (comenzando por el paso **especificar el modo de Asia Pacífico**) hello tooconnect DevKit tooyour office Wi-Fi. 

## <a name="start-using-devkit"></a>Uso inicial del DevKit

aplicación predeterminada de Hello con DevKit se compruebe Hola versión más reciente del firmware de Hola y mostrar algunos datos de diagnóstico de sensor para usted.

### <a name="upgrade-toohello-latest-firmware"></a>Actualizar el firmware más reciente de toohello

Se le pedirá en pantalla de bienvenida que ambos Hola versión de firmware más reciente y actual si no hay una actualización necesitada. Siga [actualizar firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guía tooupgrade.

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
Se trata de un esfuerzo por única vez, una vez que comience el desarrollo en hello DevKit y cargar la aplicación, tendrá que firmware más reciente de hello vienen con la aplicación.

### <a name="test-various-sensors"></a>Prueba de varios sensores

Presione sensores de tootest botón B, continúe presionando y liberar toocycle de botón Hola B a través de cada sensor.

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Preparación del entorno de desarrollo

Ahora es tiempo tooset el entorno de desarrollo de hello: herramientas y paquetes para toobuild increíbles aplicaciones de IoT. Puede elegir la versión de Windows o macOS según el sistema operativo de tooyour.


### <a name="windows"></a>Windows

Le recomendamos toouse Hola instalación paquete tooprepare Hola entorno de desarrollo. Si tiene algún problema, puede seguir hello [requieren pasos manuales](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget hacerlo.

#### <a name="download-latest-package"></a>Descarga del paquete más reciente

Hola `.zip` descarga de archivos contiene todos los paquetes necesarios para el desarrollo de DevKit y herramientas que necesitan.

> [!div class="button"]
[Descargar](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> Hola `.zip` archivo contiene siguiente Hola herramientas y paquetes. Si ya tiene algunos componentes instalados, el script de Hola detectará y omitirlos.
> * Node.js y Yarn: tiempo de ejecución para el script de instalación de Hola y las tareas automatizadas
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -multiplataforma experiencia de línea de comandos para administrar recursos de Azure, Hola MSI contiene dependientes Python y pip.
> * [Visual Studio Code](https://code.visualstudio.com/): editor de código ligero para el desarrollo de DevKit
> * [Extensión de Visual Studio Code para Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): habilita el desarrollo de Arduino en Visual Studio Code
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): extensión de Hola para Arduino se basa en esta herramienta
> * Paquete de placa de DevKit: Herramienta cadenas, las bibliotecas y proyectos para hello DevKit
> * Utilidad ST-Link: controladores y utilidades esenciales

#### <a name="run-installation-script"></a>Ejecución del script de instalación

En el Explorador de archivos de Windows, busque hello `.zip` y extraerlo, busque `install.cmd`, pulse el botón derecho y seleccione **"Ejecutar como administrador"** toostart.

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Durante la instalación, verá el progreso Hola de cada herramienta o un paquete.

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>Confirmar tooinstall controladores

Hola frente a código de extensión Arduino se basa en hello Arduino IDE. Si es Hola primera vez que se va a instalar hello Arduino IDE, es posible que los controladores relevantes tooinstall solicitadas:

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Tiempo debe durar la instalación de toofinish de aproximadamente 10 minutos según la velocidad de Internet. Una vez completada la instalación de hello, debería ver el código de Visual Studio y Arduino IDE los métodos abreviados en el escritorio.

> [!NOTE] 
En ocasiones, al iniciar VS Code, aparece un error que indica que no se encuentra el IDE de Arduino o un paquete de la placa. toosolve lo, cerrar VS Code, inicie Arduino IDE una vez y el código de VS deben buscar ruta de acceso Arduino IDE correctamente.


### <a name="macos-preview"></a>macOS (versión preliminar)

Siga estos entorno de desarrollo de pasos tooprepare macOS.

#### <a name="install-azure-cli-20"></a>Instalación de la CLI de Azure 2.0

Siga hello [guía oficial](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall 2.0 de CLI de Azure:

Instale la CLI de Azure 2.0 con un comando `curl`:

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

Y reiniciar el shell de comandos para cambios tootake efecto:

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Instalación del IDE de Arduino

Hola extensión Arduino de código de Visual Studio se basa en hello Arduino IDE. Descargue e instale hello [Arduino IDE para macOS](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Instalación de Visual Studio Code

Descargue e instale [Visual Studio Code para macOS](https://code.visualstudio.com/). Se trata de hello principal herramienta de desarrollo para crear aplicaciones de DevKit IoT.

####  <a name="download-latest-package"></a>Descarga del paquete más reciente

1. Instale Node.js. Puede usar el Administrador de paquetes populares macOS [Homebrew](https://brew.sh/) o [pregeneradas instalador](https://nodejs.org/en/download/) tooinstall lo.

2. Descargue el archivo `.zip` con los scripts de tarea necesarios para el desarrollo del DevKit en VS Code.

   > [!div class="button"]
   [Descargar](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Busque hello `.zip` y extráigalo. A continuación, inicie **Terminal** hello ejecución sigue tooconfigure de comandos y aplicación:

   Mover la carpeta de usuario de la carpeta extraída tooyour macOS:
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Instale los paquetes `npm`:
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>Instalación de la extensión de VS Code para Arduino

Código de Visual Studio permite extensiones de Marketplace de tooinstall directamente en la herramienta de hello, simplemente haga clic en el icono de extensiones de hello en el panel del menú izquierdo hello y, a continuación, buscar `Arduino` tooinstall:

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>Instalación del paquete de la placa DevKit

Necesitará placa de DevKit de hello tooadd utilizando Hola Administrador de panel en el código de Visual Studio.

1. Use `Cmd+Shift+P` tooinvoke comando paleta y escriba **Arduino** , a continuación, busque y seleccione **Arduino: Administrador de panel**.

2. Haga clic en **'Las direcciones URL adicionales'** en la parte inferior de hello derecha.
   ![instalación-url-adicionales](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. Hola `settings.json` , agregue una línea en la parte inferior de Hola de `USER SETTINGS` panel y guardar.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Ahora Hola panel administrador buscar 'az3166' e instalar la versión más reciente de Hola.
   ![instalación-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

Ahora dispone de todas las herramientas que necesitan hello y paquetes instalados para macOS.


## <a name="open-project-folder"></a>Apertura de la carpeta del proyecto

### <a name="launch-vs-code"></a>Ejecutar VS Code

Asegúrese de que el DevKit no está conectado. Ejecutar código de VS en primer lugar y conectar hello DevKit tooyour equipo. VS Code lo encontrará automáticamente y abrirá una página de introducción emergente:

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
En ocasiones, al iniciar VS Code, aparece un error que indica que no se encuentra el IDE de Arduino o un paquete de la placa. toosolve lo, cerrar VS Code, vuelva a iniciar el Arduino IDE una vez y el código de VS deben buscar ruta de acceso Arduino IDE correctamente.

### <a name="open-arduino-examples-folder"></a>Apertura de la carpeta de ejemplos de Arduino

Cambiar demasiado**'Arduino ejemplos'** ficha, navegue demasiado`Examples for MXCHIP AZ3166 > AzureIoT` y haga clic en `GetStarted`.

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

Si se encontrara tooclose panel de hello, tooreload lo, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) paleta y el tipo de comando tooinvoke **Arduino** toofind y seleccione **Arduino: ejemplos**.

## <a name="provision-azure-services"></a>Aprovisionamiento de los servicios de Azure

En la ventana de la solución de hello, ejecute la tarea a través de `Ctrl+P` (macOS: `Cmd+P`) escribiendo 'en la nube el aprovisionamiento de tarea':

Hola VS Code terminal, que una línea de comandos interactiva le guiará Hola aprovisionamiento requiere servicios de Azure:

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Creación y carga del boceto de Arduino

### <a name="install-required-library"></a>Instalación de la biblioteca necesaria

1. Presione `F1` o `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) paleta y el tipo de comando tooinvoke **Arduino** , a continuación, busque y seleccione **Arduino: Administrador de bibliotecas de**.

2. Busque la biblioteca `ArduinoJson` y haga clic en **Install** (Instalar)

### <a name="build-and-upload-hello-device-code"></a>Crear y cargar el código de dispositivo de Hola

Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'dispositivo de tarea de carga'. Hola terminal le pedirá tooenter el modo de configuración. toodo por lo tanto, mantenga presionado el botón A, a continuación, botón de restablecimiento de Hola de inserción y de lanzamiento. pantalla de bienvenida mostrará "Configuración". Se trata de una cadena de conexión de hello tooset que recupera del paso 'aprovisionamiento en la nube de tarea'.

A continuación, se iniciará comprobando y cargando boceto de Hola Arduino:

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

Hola DevKit se reinicie e iniciar la ejecución de código de hello.

## <a name="test-hello-project"></a>Proyecto de prueba de Hola

En VS Code, haga clic en el icono de plug de energía de hello en barra tooopen Hola serie Monitor de estado de Hola.

aplicación de ejemplo de Hola se esté ejecutando correctamente cuando vea Hola siguientes resultados:

* Hello muestra Monitor serie Hola misma información como contenido Hola Hola captura de pantalla siguiente.
* Hola LED en MXChip IoT DevKit parpadea.

![Salida final en VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Problemas y comentarios

Puede encontrar [preguntas más frecuentes](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) si tiene problemas o llegar toous de los canales de Hola a continuación.

## <a name="next-steps"></a>Pasos siguientes

Se ha conectado correctamente un tooyour MXChip IoT DevKit centro de IoT y enviado Hola captura centro de IoT de tooyour de datos de sensor.

toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:

- [Administración de la mensajería de dispositivos en la nube con iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [Guardar mensajes de centro de IoT tooAzure el almacenamiento de datos](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Utilizar datos de detección en tiempo real de Power BI toovisualize desde el centro de IoT de Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Utilizar datos de detección en tiempo real de aplicaciones Web de Azure toovisualize desde el centro de IoT de Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [Boletín meteorológico utilizando los datos de sensor de Hola desde el centro de IoT en aprendizaje automático de Azure](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [Administración de dispositivos con iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Supervisión remota y notificaciones con Logic Apps](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)