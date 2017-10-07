---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 1: Configuración de Intel NUC | Microsoft Docs"
description: "Intel NUC toowork configurado como una puerta de enlace de IoT entre un sensor y la información del sensor toocollect centro de IoT de Azure y enviar tooIoT concentrador."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: puerta de enlace de iot, intel nuc, equipo nuc, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Configuración de Intel NUC como puerta de enlace de IoT
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>Lo que hará

- Configure Intel NUC como puerta de enlace de IoT.
- Instalar paquete de hello borde de IoT de Azure en hello NUC de Intel.
- Ejecutar una aplicación de ejemplo "hello_world" en la funcionalidad de puerta de enlace de Intel NUC tooverify Hola Hola.

  > Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá

En esta lección, aprenderá lo siguiente:

- ¿Cómo tooconnect Intel NUC con dispositivos periféricos.
- ¿Cómo tooinstall y actualizar paquetes de hello necesario sobre el uso de Intel NUC Hola inteligente Administrador de paquetes.
- Cómo hello toorun "hello_world" ejemplo de funcionalidad de puerta de enlace de aplicaciones tooverify Hola.

## <a name="what-you-need"></a>Lo que necesita

- Un Intel NUC Kit DE3815TYKE con hello Suite de Software de puerta de enlace de IoT de Intel (viento demarcación Linux * 7.0.0.13) preinstalado. [Haga clic aquí toopurchase Kit comercial de puerta de enlace de arboleda IoT](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).
- Un cable Ethernet.
- Un teclado.
- Un cable HDMI o VGA.
- Un monitor con un puerto HDMI o VGA.
- Opcional: [SensorTag de Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)

![Kit de puerta de enlace](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Conectar Intel NUC con dispositivos periféricos de Hola

imagen de Hello siguiente es un ejemplo de NUC de Intel que está conectado a periféricos distintos:

1. Teclado tooa conectado.
2. Conectado tooa monitor con un cable VGA o HDMI.
3. Red con un cable Ethernet cableada mediante tooa conectado.
4. Fuente de alimentación de tooa conectado con un cable de alimentación.

![Intel NUC conectado tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Toohello Intel NUC sistema conectado a la del equipo host a través de Shell seguro (SSH)

Necesitará un teclado y una dirección IP de monitor tooget Hola del dispositivo NUC de Intel. Si ya sabe Hola IP dirección, puede omitir anticipada toostep 3 en esta sección.

1. Activar Hola Intel NUC presionando el botón de encendido de hello y, a continuación, inicie sesión.

   nombre de usuario predeterminado de Hola y la contraseña son ambos `root`.

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. Obtener la dirección IP de Hola de hello Intel NUC ejecutando hello `ifconfig` comando en el dispositivo de Intel NUC Hola.

   Este es un ejemplo de salida del comando Hola.

   ![Salida de ifconfig que muestra la dirección IP de Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   En este ejemplo, Hola valor siguiente `inet addr:` es dirección IP de Hola que necesite conectarse cuando toohello Intel NUC desde un equipo host.

3. Utilice uno de hello siguiendo a los clientes SSH de su tooIntel de tooconnect del equipo host NUC.

    - [PuTTY](http://www.putty.org/) para Windows.
    - cliente SSH integrado de Hello en Ubuntu o macOS.

   Es más eficaz y productiva toooperate un NUC Intel desde un equipo host. Será necesario Hola dirección IP de Intel NUC, tooit tooconnect a través de un cliente de SSH del nombre y la contraseña del usuario. Este es un ejemplo que utiliza un cliente de SSH en Mac OS.
   ![Cliente de SSH que se ejecuta en macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Instalar el paquete de hello borde de IoT de Azure

paquete de Hello borde de IoT de Azure contiene archivos binarios precompilados de Hola de borde de IoT y sus dependencias. Estos archivos binarios forman borde de IoT de Azure, Hola IoT de Azure SDK y herramientas correspondientes de Hola. Hello paquete también contiene una "hello_world" aplicación de ejemplo es una funcionalidad de puerta de enlace de hello toovalidate usado. Borde de IoT es parte del núcleo de Hola de puerta de enlace de Hola. 

Siga estos paquetes de saludo de tooinstall de pasos.

1. Agregue Hola repositorio IoT nube ejecutando Hola siga los comandos en una ventana de terminal:

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > Escriba 'y', cuando se le pida too'Include este canal?'
   
   Si recibe un `import read failed(-1)` error, Hola de uso después de emitir de hello tooresolve de comandos:
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   Hola `rpm` comando importaciones Hola clave rpm. Hola `smart channel` comando agrega rpm Hola canal toohello inteligente Administrador de paquetes. Antes de ejecutar hello `smart update` comando, verá una salida como a continuación.

   ![salida de los comandos rpm y de canal inteligente](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. Ejecutar el comando de actualización inteligente de hello:

   ```bash
   smart update
   ```

3. Instalar el paquete de puerta de enlace de IoT de Azure de hello ejecutando Hola siguiente comando:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`es el nombre de Hola de paquetes de saludo. Hola `smart install` comando es paquete de hello tooinstall usado.

    > Siguiente ejecución Hola comando si ve este error: "clave pública no está disponible"

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > Reiniciar Hola Intel NUC si ve este error: 'no hay ningún paquete proporciona util-linux-dev'

   Después de instalar el paquete de hello, Intel NUC es listo toofunction como una puerta de enlace.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Ejecutar aplicación de ejemplo de "hello_world" hello borde de IoT de Azure

Hola tras la aplicación de ejemplo crea una puerta de enlace de un `hello_world.json` de archivos y utiliza componentes fundamentales de Hola de borde de IoT de Azure arquitectura toolog un archivo de tooa de mensaje hello world (log.txt) cada 5 segundos.

Puede ejecutar el ejemplo de Hola a todos de hello ejecutando Hola siguientes comandos:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Permiten la aplicación hello World Hola ejecutar durante unos minutos y, a continuación, presionar Hola ENTRAR clave toostop se.
![resultado de la aplicación](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> Puede omitir los errores sobre control de argumento no válido (NULL) que aparecen tras pulsar Entrar.

Puede comprobar esa puerta de enlace de Hola se ejecutó correctamente, abra el archivo log.txt hello que se encuentra ahora en la carpeta hello_world ![log.txt vista del directorio](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

Abra log.txt mediante Hola siguiente comando:

```bash
vim log.txt
```

A continuación, verá contenido Hola de log.txt, que será una salida JSON con formato de mensajes de registro de hello escritos por el módulo de Hello World de puerta de enlace de hello cada 5 segundos.
![vista de directorio de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Resumen

¡Enhorabuena! Ha terminado de configurar Intel NUC como puerta de enlace. Ahora está listo toomove en toohello siguiente lección tooset el equipo host, se crea un centro de IoT de Azure y registrar el dispositivo lógico de centro de IoT de Azure.

## <a name="next-steps"></a>Pasos siguientes
[Usar un tooconnect de puerta de enlace de IoT un centro de IoT tooAzure de dispositivo](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

