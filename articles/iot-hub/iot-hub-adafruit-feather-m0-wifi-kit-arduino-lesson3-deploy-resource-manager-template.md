---
title: "Connect Arduino (C) tooAzure IoT - lección 3: implementación de plantilla | Documentos de Microsoft"
description: "aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: almacenar datos en la nube de hello, los datos almacenados en la nube, el servicio de nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6a84a6d3c5263a85c8997cf69fe446d73ab7a5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Creación de una instancia de Azure Function App y una cuenta de Azure Storage
[Las funciones de Azure](../../articles/azure-functions/functions-overview.md) es una solución para ejecutar fácilmente *funciones* (pequeños fragmentos de código) en la nube de Hola. Una aplicación de Azure función hospeda ejecución Hola de las funciones de Azure.

## <a name="what-will-you-do"></a>Qué hará
Utilice un toocreate de plantilla de Azure Resource Manager una aplicación de Azure de función y una cuenta de almacenamiento de Azure. aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla.

Si tiene problemas, buscar soluciones en hello [solución de problemas de la página de su placa Adafruit compacto M0 Wi-Fi Arduino](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-will-you-learn"></a>Qué aprenderá
En este artículo, aprenderá lo siguiente:
* Cómo toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure recursos.
* ¿Cómo toouse un Azure función tooprocess aplicación mensajes del centro de IoT y escribirlos tooa tabla en el almacenamiento de tabla de Azure.

## <a name="what-do-you-need"></a>Qué necesita
Debe haber completado correctamente los siguientes tutoriales:
- [Get started with your Arduino board][get-started] (Introducción a la placa de Arduino)
- [Creación de una instancia de Azure IoT Hub][create-iot-hub]

## <a name="open-hello-sample-app"></a>Aplicación de ejemplo de Hola abierto
Abra el proyecto de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:

```bash
cd Lesson3
code .
```

![Estructura del repositorio][repo-structure]

* Hola `app.ino` archivo Hola `app` subcarpeta es el archivo de origen de la clave de Hola. Este archivo de origen contiene código de hello toosend un mensaje 20 veces tooyour IoT hub- and blink Hola LED para cada mensaje que envía.
* Hola `config.json` contiene valores de configuración necesarios.
* Hola `arm-template.json` archivo es hello Azure Resource Manager plantilla que contiene una aplicación de Azure de función y una cuenta de almacenamiento de Azure.
* Hola `arm-template-param.json` archivo es el archivo de configuración de hello utilizado por la plantilla de hello Azure Resource Manager.
* Hola `ReceiveDeviceMessages` subcarpeta contiene código de Node.js de Hola para hello Azure función.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure
Hola de actualización `arm-template-param.json` archivo de código de Visual Studio.

![Parámetros de plantilla de Azure Resource Manager][arm-template-params]

* Sustituya **[su nombre de IoT Hub]** por el valor **{mi nombre de centro}** que especificó cuando [creó el IoT Hub y registró la placa de Arduino][created-iot-hub-and-registered-arduino-board].
* Reemplace **[prefix string for new resources]** por el prefijo que desee. prefijo de Hola garantiza que el nombre de recurso hello es globalmente único tooavoid conflicto. No use un guión o un número inicial de prefijo de Hola.

Después de actualizar hello `arm-template-param.json` de archivos, implementar Hola recursos tooAzure ejecutando Hola siguiente comando:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Tarda aproximadamente cinco minutos toocreate estos recursos. Mientras la creación de recursos de hello está en curso, puede mover en el artículo siguiente de toohello.

## <a name="summary"></a>Resumen
Ha creado su tooprocess de aplicación de Azure función mensajes de centro de IoT y el almacenamiento de Azure cuenta toostore estos mensajes. Ahora puede implementar y ejecutar mensajes de dispositivo a la nube de toosend de ejemplo de Hola en el panel de Arduino.

## <a name="next-steps"></a>Pasos siguientes
[Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube en el panel de Arduino][send-device-to-cloud-messages]

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md