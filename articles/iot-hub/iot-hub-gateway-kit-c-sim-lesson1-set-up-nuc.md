---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 1: Configuración de NUC | Microsoft Docs"
description: "Intel NUC toowork configurado como una puerta de enlace de IoT entre un sensor y la información del sensor toocollect centro de IoT de Azure y enviar tooIoT concentrador."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: puerta de enlace de iot, intel nuc, equipo nuc, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Configuración de Intel NUC como puerta de enlace de IoT

## <a name="what-you-will-do"></a>Lo que hará

- Configure Intel NUC como puerta de enlace de IoT.
- Instalar paquete de hello borde de IoT de Azure en NUC de Intel.
- Ejecutar una aplicación de ejemplo "hello_world" en la funcionalidad de puerta de enlace de Intel NUC tooverify Hola.
Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá

En esta lección, aprenderá lo siguiente:

- ¿Cómo tooconnect Intel NUC con dispositivos periféricos.
- ¿Cómo tooinstall y actualizar paquetes de hello necesario sobre el uso de Intel NUC Hola inteligente Administrador de paquetes.
- Cómo hello toorun "hello_world" ejemplo de funcionalidad de puerta de enlace de aplicaciones tooverify Hola.

## <a name="what-you-need"></a>Lo que necesita

- Un Intel NUC Kit DE3815TYKE con hello Suite de Software de puerta de enlace de IoT de Intel (viento demarcación Linux * 7.0.0.13) preinstalado.
- Un cable Ethernet.
- Un teclado.
- Un cable HDMI o VGA.
- Un monitor con un puerto HDMI o VGA.

![Kit de puerta de enlace](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Conectar Intel NUC con dispositivos periféricos de Hola

imagen de Hello siguiente es un ejemplo de NUC de Intel que está conectado a periféricos distintos:

1. Teclado tooa conectado.
2. Conectado toohello monitor mediante un cable VGA o HDMI.
3. Red cableada mediante tooa conectado mediante un cable Ethernet.
4. Fuente de alimentación de toohello conectado con un cable de alimentación.

![Intel NUC conectado tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Toohello Intel NUC sistema conectado a la del equipo host a través de Shell seguro (SSH)

Aquí necesitará teclado y monitor tooget Hola dirección IP del dispositivo NUC. Si ya sabe Hola IP dirección, puede omitir toostep 3 en esta sección.

1. Activar Intel NUC presionando el botón de encendido de Hola y de registro en el sistema de Hola.

   nombre de usuario predeterminado de Hola y la contraseña son ambos `root`.

2. Obtener dirección IP de Hola de NUC ejecutando hello `ifconfig` comando. Este paso se realiza en el dispositivo NUC Hola.

   Este es un ejemplo de salida del comando Hola.

   ![Salida de ifconfig que muestra la dirección IP de NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   En este ejemplo, Hola valor siguiente `inet addr:` es dirección IP de Hola que necesita, si tiene previsto tooconnect remotamente desde un tooIntel del equipo host NUC.

3. Utilice uno de hello siguiendo a los clientes SSH de su tooIntel tooconnect de máquina de host NUC.

   - [PuTTY](http://www.putty.org/) para Windows.
   - Hola compilación en el cliente de SSH en Ubuntu o macOS.

   Es más eficaz y productiva toooperate en Intel NUC desde un equipo host. Necesita la dirección IP de Hola Hola, nombre de usuario y contraseña tooconnect hello NUC mediante el cliente de SSH. Este es el cliente de SSH de uso de ejemplo de Hola en macOS.
   ![Cliente de SSH que se ejecuta en macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Instalar el paquete de hello borde de IoT de Azure

paquete de Hello borde de IoT de Azure contiene archivos binarios precompilados de Hola de hello SDK y sus dependencias. Estos archivos binarios forman borde de IoT de Azure, Hola IoT de Azure SDK y herramientas correspondientes de Hola. paquete de Hello también contiene una aplicación de ejemplo de "hello_world" es la funcionalidad de puerta de enlace de hello toovalidate usado. Borde de IoT es parte del núcleo de Hola de puerta de enlace de Hola. Hola tooinstall del paquete, siga estos pasos:

1. Agregar repositorio de nube de hello IoT ejecutando Hola siga los comandos en una ventana de terminal:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   Hola `rpm` comando importaciones Hola clave rpm. Hola `smart channel` comando agrega rpm Hola canal toohello inteligente Administrador de paquetes. Antes de ejecutar hello `smart update` comando, verá una salida similar a continuación.

   ![salida de los comandos rpm y de canal inteligente](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Instalar paquete Hola ejecutando Hola siguiente comando:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`es el nombre de Hola de paquetes de saludo. Hola `smart install` comando es paquete de hello tooinstall usado.

   Después de instalar el paquete de hello, Intel NUC es toowork esperado como una puerta de enlace.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Ejecutar aplicación de ejemplo de "hello_world" hello borde de IoT de Azure

Vaya demasiado`azureiotgatewaysdk/samples` y ejecute la aplicación de ejemplo de Hola ejemplo "hello_world". Esta aplicación de ejemplo crea una puerta de enlace de hello `hello_world.json` archivo y usa los componentes fundamentales de Hola de hello borde de IoT de Azure arquitectura toolog un archivo de tooa de hello world mensaje cada 5 segundos.

Puede ejecutar la aplicación de ejemplo de "hello_world" de ejemplo de Hola ejecutando el siguiente comando de hello:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

aplicación de ejemplo de Hola produce siguiente de hello resultado si la funcionalidad de puerta de enlace de hello funciona correctamente:

![resultado de la aplicación](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Resumen

¡Enhorabuena! Ha terminado de configurar Intel NUC como puerta de enlace. Ahora está listo toomove en toohello siguiente lección tooset el equipo host, crear un centro de IoT de Azure y registrar el dispositivo lógico de centro de IoT de Azure.

## <a name="next-steps"></a>Pasos siguientes
[Preparación del equipo host y de IoT Hub de Azure](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
