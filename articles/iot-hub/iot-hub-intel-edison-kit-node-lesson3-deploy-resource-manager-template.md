---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 3: crear la aplicación de la función | Documentos de Microsoft"
description: "aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: almacenar datos en la nube de hello, los datos almacenados en la nube, el servicio de nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 37ee5962-95ce-40e8-8162-17e735eaec21
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8ea0a4cdf978158d70e47eaed57e3de378b638d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Creación de una instancia de Azure Function App y una cuenta de Azure Storage
[Las funciones de Azure](../../articles/azure-functions/functions-overview.md) es una solución para ejecutar fácilmente *funciones* (pequeños fragmentos de código) en la nube de Hola. Una aplicación de Azure función hospeda ejecución Hola de las funciones de Azure.

## <a name="what-will-you-do"></a>Qué hará
Utilice un toocreate de plantilla de Azure Resource Manager una aplicación de Azure de función y una cuenta de almacenamiento de Azure. aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla. cuenta de almacenamiento Hello se usa una para su lectura Hola conserva copias de los mensajes de la tabla de Azure. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-will-you-learn"></a>Qué aprenderá
En este artículo, aprenderá lo siguiente:
* Cómo toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure recursos.
* ¿Cómo toouse un Azure función tooprocess aplicación mensajes del centro de IoT y escribirlos tooa tabla en el almacenamiento de tabla de Azure.

## <a name="what-do-you-need"></a>Qué necesita
Debe haber completado correctamente los siguientes tutoriales:
- [Introducción a Intel Edison][get-started-with-your-intel-edison]
- [Create your Azure IoT hub][create-your-azure-iot-hub] (Creación de un Azure IoT Hub)

## <a name="open-hello-sample-app"></a>Aplicación de ejemplo de Hola abierto
Abra el proyecto de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:

```bash
cd Lesson3
code .
```

![Estructura del repositorio][repo-structure]

* archivo de Hello en hello `app` subcarpeta es el archivo de origen de la clave de Hola. Este archivo de origen contiene código de hello toosend un mensaje 20 veces tooyour IoT hub- and blink Hola LED para cada mensaje que envía.
* Hola `arm-template.json` archivo es hello Azure Resource Manager plantilla que contiene una aplicación de Azure de función y una cuenta de almacenamiento de Azure.
* Hola `arm-template-param.json` archivo es el archivo de configuración de hello utilizado por la plantilla de hello Azure Resource Manager.
* Hola `ReceiveDeviceMessages` subcarpeta contiene código de Node.js de Hola para hello Azure función.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure
Hola de actualización `arm-template-param.json` archivo de código de Visual Studio.

![Parámetros de plantilla de Azure Resource Manager][arm-template-parameters]

* Sustituya **[su nombre de centro de IoT Hub]** por **{mi nombre de centro}** que especificó cuando [creó el centro de IoT Hub y registró Intel Edison][created-your-iot-hub-and-registered-intel-edison].
* Reemplace **[prefix string for new resources]** por el prefijo que desee. prefijo de Hola garantiza que el nombre de recurso hello es globalmente único tooavoid conflicto. No use un guión o un número inicial de prefijo de Hola.

Después de actualizar hello `arm-template-param.json` de archivos, implementar Hola recursos tooAzure ejecutando Hola siguiente comando:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Tarda aproximadamente cinco minutos toocreate estos recursos. Mientras la creación de recursos de hello está en curso, puede mover en el artículo siguiente de toohello.

## <a name="summary"></a>Resumen
Ha creado su tooprocess de aplicación de Azure función mensajes de centro de IoT y el almacenamiento de Azure cuenta toostore estos mensajes. Ahora puede implementar y ejecutar mensajes de dispositivo a la nube de toosend de ejemplo de Hola en Edison.

## <a name="next-steps"></a>Pasos siguientes
[Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube en Intel Edison][send-device-to-cloud-messages].
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md