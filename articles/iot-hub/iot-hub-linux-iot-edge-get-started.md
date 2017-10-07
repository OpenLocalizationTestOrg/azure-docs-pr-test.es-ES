---
title: aaaGet a trabajar con el borde de IoT de Azure (Linux) | Documentos de Microsoft
description: "¿Cómo toobuild una puerta de enlace en un Linux automático y obtener información sobre los conceptos clave de borde de IoT de Azure como módulos y archivos de configuración de JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a>Explorar la arquitectura de Azure IoT Edge en Linux

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>¿Cómo toorun Hola ejemplo

Hola **build.sh** script genera su resultado en hello **generar** carpeta de la copia local de hello **iot borde** repositorio. Esta salida incluye dos módulos de borde IoT Hola utilizados en este ejemplo.

Hola lugares de la secuencia de comandos de compilación **liblogger.so** en hello **compilación/módulos/registrador/** carpeta y **libhello\_world.so** en hello **compilar / módulos/hello_world/** carpeta. Usar estas rutas de acceso para hello **ruta de acceso del módulo** valores tal y como se muestra en el siguiente archivo de configuración de JSON de ejemplo de Hola.

Hola Hola\_world\_proceso de ejemplo toma el archivo de configuración de JSON de hello ruta de acceso tooa un argumento de línea de comandos. siguiente archivo JSON de ejemplo Hola se proporciona una en el repositorio SDK de hello en **ejemplos/hello\_world/src/hello\_world\_lin.json**. Este archivo de configuración funciona tal cual a menos que modifique Hola compilar hello de la secuencia de comandos tooplace IoT borde módulos o archivos ejecutables en ubicaciones no predeterminadas de ejemplo.

> [!NOTE]
> las rutas de acceso del módulo hello son toohello relativa de directorio de trabajo actual, desde donde Hola Hola\_world\_ejecutable de ejemplo se inicia, no Hola directorio donde se encuentra ejecutable hello. ejemplo de Hola a JSON configuración archivo los valores predeterminados toowriting 'log.txt' en el directorio de trabajo actual.

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. Navegue toohello **generar** carpeta del directorio raíz de Hola de su copia local de hello **iot borde** repositorio.

1. Ejecute el siguiente comando de hello:

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

