---
title: "Conexión de Raspberry Pi (Node) a Azure IoT: Lección 3: Implementación de plantillas | Microsoft Docs"
description: La instancia de Azure Function App escucha los eventos de Azure IoT Hub, procesa los mensajes entrantes y los escribe en Azure Table Storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: almacenar datos en la nube, datos almacenados en la nube, servicio en la nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Creación de una instancia de Azure Function App y una cuenta de Azure Storage
[Azure Functions](../azure-functions/functions-overview.md) es una solución que permite ejecutar *funciones* (pequeños fragmentos de código) en la nube fácilmente. Una aplicación de Azure Function hospeda la ejecución de sus funciones en Azure.

## <a name="what-you-will-do"></a>Lo que hará
Va a utilizar una plantilla de Azure Resource Manager para crear una instancia de Azure Function App y una cuenta de Azure Storage. La instancia de Azure Function App escucha los eventos de Azure IoT Hub, procesa los mensajes entrantes y los escribe en Azure Table Storage. Si tiene problemas, puede encontrar soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* Cómo utilizar [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) para implementar recursos de Azure.
* Cómo utilizar una instancia de Azure Function App para procesar mensajes de IoT Hub y escribirlos en una tabla de Azure Table Storage.

## <a name="what-you-need"></a>Lo que necesita
Debe haber completado correctamente los siguientes tutoriales:
* [Get started with Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md) (Introducción a Raspberry Pi 3)
* [Create your Azure IoT hub](iot-hub-raspberry-pi-kit-node-get-started.md) (Creación de un centro de IoT de Azure)

## <a name="open-the-sample-app"></a>Apertura de la aplicación de ejemplo
Abra el proyecto de ejemplo en Visual Studio Code ejecutando los comandos siguientes:

```bash
cd Lesson3
code .
```

![Estructura del repositorio](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* El archivo `app.js` de la subcarpeta `app` es el archivo de origen de la clave. Este archivo de origen contiene el código para enviar un mensaje 20 veces en su instancia de IoT Hub y hacer parpadear el LED para cada mensaje que envía.
* El archivo `arm-template.json` es una plantilla de Azure Resource Manager que contiene una instancia de Azure Function App y una cuenta de Azure Storage.
* El archivo `arm-template-param.json` es el archivo de configuración que utiliza la plantilla de Azure Resource Manager.
* La subcarpeta `ReceiveDeviceMessages` contiene el código de Node.js para la función de Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure
Actualice el archivo `arm-template-param.json` en Visual Studio Code.

![Parámetros de plantilla de Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* Sustituya **[su nombre de centro IoT]** por **{mi nombre de centro}** que especificó cuando [creó el centro de IoT y registró Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).
* Reemplace **[prefix string for new resources]** por el prefijo que desee. El prefijo garantiza que el nombre del recurso sea globalmente único para evitar conflictos. No utilice guiones ni números al comienzo del prefijo.

Después de actualizar el archivo `arm-template-param.json`, implemente los recursos en Azure ejecutando el comando siguiente:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Este proceso tarda aproximadamente cinco minutos en crear estos recursos. Mientras espera a que se ejecute la creación de recursos, puede pasar al siguiente artículo.

## <a name="summary"></a>Resumen
Ha creado una instancia de Azure Function App para procesar mensajes de IoT Hub, así como una cuenta de Azure Storage para almacenar estos mensajes. Ahora puede implementar y ejecutar el ejemplo para enviar mensajes del dispositivo a la nube en Pi.

## <a name="next-steps"></a>Pasos siguientes
[Run a sample application to send device-to-cloud messages on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md) (Ejecución de una aplicación de ejemplo para enviar mensajes de dispositivo a nube en Raspberry Pi 3)

