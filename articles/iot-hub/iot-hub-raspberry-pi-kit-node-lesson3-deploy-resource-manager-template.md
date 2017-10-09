---
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 3: implementación de plantilla | Documentos de Microsoft"
description: "aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: almacenar datos en la nube de hello, los datos almacenados en la nube, el servicio de nube de iot
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
ms.openlocfilehash: b6c0a9530cb80e3f78c0e96037f6f3942b602aea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Creación de una instancia de Azure Function App y una cuenta de Azure Storage
[Las funciones de Azure](../azure-functions/functions-overview.md) es una solución para ejecutar fácilmente *funciones* (pequeños fragmentos de código) en la nube de Hola. Una aplicación de Azure función hospeda ejecución Hola de las funciones de Azure.

## <a name="what-you-will-do"></a>Lo que hará
Utilice un toocreate de plantilla de Azure Resource Manager una aplicación de Azure de función y una cuenta de almacenamiento de Azure. aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* Cómo toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure recursos.
* ¿Cómo toouse un Azure función tooprocess aplicación mensajes del centro de IoT y escribirlos tooa tabla en el almacenamiento de tabla de Azure.

## <a name="what-you-need"></a>Lo que necesita
Debe haber completado correctamente los siguientes tutoriales:
* [Get started with Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md) (Introducción a Raspberry Pi 3)
* [Create your Azure IoT hub](iot-hub-raspberry-pi-kit-node-get-started.md) (Creación de un centro de IoT de Azure)

## <a name="open-hello-sample-app"></a>Aplicación de ejemplo de Hola abierto
Abra el proyecto de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:

```bash
cd Lesson3
code .
```

![Estructura del repositorio](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* Hola `app.js` archivo Hola `app` subcarpeta es el archivo de origen de la clave de Hola. Este archivo de origen contiene código de hello toosend un mensaje 20 veces tooyour IoT hub- and blink Hola LED para cada mensaje que envía.
* Hola `arm-template.json` archivo es hello Azure Resource Manager plantilla que contiene una aplicación de Azure de función y una cuenta de almacenamiento de Azure.
* Hola `arm-template-param.json` archivo es el archivo de configuración de hello utilizado por la plantilla de hello Azure Resource Manager.
* Hola `ReceiveDeviceMessages` subcarpeta contiene código de Node.js de Hola para hello Azure función.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure
Hola de actualización `arm-template-param.json` archivo de código de Visual Studio.

![Parámetros de plantilla de Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* Sustituya **[su nombre de centro IoT]** por **{mi nombre de centro}** que especificó cuando [creó el centro de IoT y registró Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).
* Reemplace **[prefix string for new resources]** por el prefijo que desee. prefijo de Hola garantiza que el nombre de recurso hello es globalmente único tooavoid conflicto. No use un guión o un número inicial de prefijo de Hola.

Después de actualizar hello `arm-template-param.json` de archivos, implementar Hola recursos tooAzure ejecutando Hola siguiente comando:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Tarda aproximadamente cinco minutos toocreate estos recursos. Mientras la creación de recursos de hello está en curso, puede mover en el artículo siguiente de toohello.

## <a name="summary"></a>Resumen
Ha creado su tooprocess de aplicación de Azure función mensajes de centro de IoT y el almacenamiento de Azure cuenta toostore estos mensajes. Ahora puede implementar y ejecutar mensajes de dispositivo a la nube de toosend de ejemplo de Hola en Pi.

## <a name="next-steps"></a>Pasos siguientes
[Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube en frambuesa Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

