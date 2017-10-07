---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 4: Guardado de mensajes | Microsoft Docs"
description: "Guardar mensajes Intel NUC tooyour centro de IoT, escribirlos tooAzure el almacenamiento de tabla y, a continuación, leerlos desde la nube de Hola."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: almacenar datos en la nube de hello, los datos almacenados en la nube, el servicio de nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 230f2708b62b89c6eed2e238efefc1c4da86e373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Creación de una cuenta de Azure Storage y una aplicación de Azure Function

Las funciones de Azure es una solución para ejecutar fácilmente _funciones_ (pequeños fragmentos de código) en la nube de Hola. Una aplicación de Azure función hospeda ejecución Hola de las funciones de Azure. 

## <a name="what-you-will-do"></a>Lo que hará

- Utilice un toocreate de plantilla de Azure Resource Manager una aplicación de Azure de función y una cuenta de almacenamiento de Azure. aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla.

Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).


## <a name="what-you-will-learn"></a>Lo qué aprenderá

En esta lección, aprenderá lo siguiente:

- Cómo toouse toodeploy de administrador de recursos de Azure recursos de Azure.
- ¿Cómo toouse un Azure función tooprocess aplicación mensajes del centro de IoT y escribirlos tooa tabla en el almacenamiento de tabla de Azure.

## <a name="what-you-need"></a>Lo que necesita

Debe haber completado correctamente lecciones anteriores de hello:

- [Lección 1: Configuración de Intel NUC como puerta de enlace de IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [Lección 2: Preparación del equipo host y de IoT Hub de Azure](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [Lección 3: Recibir mensajes de dispositivo simulado de Hola y leer los mensajes de su centro de IoT](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a>Apertura de una aplicación de ejemplo

Vaya tooyour `iot-hub-c-intel-nuc-gateway-getting-started` carpeta repo, archivos de configuración de inicializar hello y proyecto de ejemplo de Hola, a continuación, abrir en Visual Studio Code ejecutando el siguiente comando de hello:

```bash
cd Lesson4
npm install
gulp init
code .
```

![estructura del repositorio](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- Hola `arm-template.json` archivo es hello Azure Resource Manager plantilla que contiene una aplicación de Azure de función y una cuenta de almacenamiento de Azure.
- Hola `arm-template-param.json` archivo es el archivo de configuración de hello utilizado por la plantilla de hello Azure Resource Manager.
- Hola `ReceiveDeviceMessages` subcarpeta contiene código de Node.js de Hola para hello Azure función.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure

Hola de actualización `arm-template-param.json` archivo de código de Visual Studio.

![arm template json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Sustituya `[your IoT Hub name]` por el valor `{my hub name}` que especificó en la lección 2.

Después de actualizar hello `arm-template-param.json` de archivos, implementar Hola recursos tooAzure ejecutando Hola siguiente comando:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Use `iot-gateway` como valor de Hola de `{resource group name}` si no cambia el valor de hello en la lección 2.

## <a name="summary"></a>Resumen

Ha creado su tooprocess de aplicación de Azure función mensajes de centro de IoT y el almacenamiento de Azure cuenta toostore estos mensajes. Ahora puede leer los mensajes enviados por el centro de IoT tooyour de puerta de enlace.

## <a name="next-steps"></a>Pasos siguientes
[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md) (Lectura de los mensajes que se conservan en Azure Storage).
