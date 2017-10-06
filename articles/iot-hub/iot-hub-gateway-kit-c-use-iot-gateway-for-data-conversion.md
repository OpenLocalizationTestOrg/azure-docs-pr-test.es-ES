---
title: "conversión de aaaData en puerta de enlace de IoT con borde de IoT de Azure | Documentos de Microsoft"
description: "Usar formato de Hola de tooconvert de puerta de enlace de IoT de datos de sensor a través de un módulo personalizado de borde de IoT de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conversión de datos de puerta de enlace de iot, transformación de datos de puerta de enlace de iot"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>Uso de la puerta de enlace de IoT para la transformación de datos de sensor con Azure IoT Edge

> [!NOTE]
> Antes de empezar este tutorial, asegúrese de que se haya completado Hola siguientes lecciones en secuencia:
> * [Configuración de Intel NUC como una puerta de enlace de IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [Usar IoT puerta de enlace tooconnect cosas toohello cloud - SensorTag tooAzure centro de IoT](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

Un objetivo de una puerta de enlace de Iot es tooprocess recopilan datos antes de enviarlo toohello en la nube. Borde de IoT de Azure incorpora módulos que pueden ser el flujo de trabajo de procesamiento de datos de tooform creado y montado Hola. Un módulo recibe un mensaje, realiza alguna acción en él y, a continuación, moverlo para otros tooprocess módulos.

## <a name="what-you-learn"></a>Conocimientos que adquirirá

Obtenga información acerca cómo toocreate una tooconvert módulo mensajes de Hola SensorTag en un formato diferente.

## <a name="what-you-do"></a>Qué debe hacer

* Crear un módulo tooconvert un mensaje recibido en formato de .json Hola.
* Compile el módulo de Hola.
* Agregar aplicación de ejemplo de Hola módulo toohello Bilitar del borde de IoT de Azure.
* Ejecutar la aplicación de ejemplo de Hola.

## <a name="what-you-need"></a>Lo que necesita

* Hola tutoriales completada en orden:
  * [Configuración de Intel NUC como una puerta de enlace de IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [Usar IoT puerta de enlace tooconnect cosas toohello cloud - SensorTag tooAzure centro de IoT](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* Un cliente de SSH que se ejecute en el equipo host. En Windows se recomienda PuTTY. Linux y macOS ya vienen con un cliente de SSH.
* dirección IP de Hola y Hola username y password tooaccess Hola puerta de enlace de cliente de SSH Hola.
* Una conexión a Internet.

## <a name="create-a-module"></a>Creación de un módulo

1. En el equipo de host de hello, ejecutar el cliente de SSH de Hola y conectar la puerta de enlace de IoT toohello.
1. Clonar archivos de código fuente de hello del módulo de conversión de Hola desde GitHub toohello directorio particular de puerta de enlace de IoT Hola ejecutando Hola siguientes comandos:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   Se trata de un módulo nativo de Azure borde escrito en lenguaje de programación de C de Hola. módulo de Hello convierte formato Hola de mensajes recibidos en hello sigue uno:

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Compile el módulo de Hola

módulo de hello toocompile, ejecute hello siguientes comandos:

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

Obtendrá un `libmy_module.so` archivo una vez completada la compilación de Hola. Tome nota de la ruta de acceso absoluta de Hola de este archivo.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Agregar aplicación de ejemplo de Hola módulo toohello BLE

1. Carpeta de ejemplos de toohello vaya ejecutando Hola siguiente comando:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Abra el archivo de configuración de hello ejecutando Hola siguiente comando:

   ```bash
   vi ble_gateway.json
   ```

1. Agregar un módulo mediante la inserción de hello después toohello código `modules` sección.

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. Reemplace `[Your libmy_module.so path]` en el código de hello con ruta de acceso absoluta de Hola de hello libmy_module.so' archivo.
1. Reemplace el código de hello en hello `links` sección con hello sigue uno:

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. Presione `ESC`y, a continuación, escriba `:wq` archivo de hello toosave.

## <a name="run-hello-sample-application"></a>Ejecutar la aplicación de ejemplo de Hola

1. Encendido hello SensorTag.
1. Establecer variable de entorno de hello SSL_CERT_FILE ejecutando Hola siguiente comando:

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Ejecutar la aplicación de ejemplo de Hola con el módulo agregado Hola ejecutando Hola siguiente comando:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Pasos siguientes

Se haya correctamente uso Hola IoT puerta de enlace tooconvert mensaje de saludo de SensorTag en formato de .json Hola.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
