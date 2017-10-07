---
title: aaaGet a trabajar con el borde de IoT de Azure (Windows) | Documentos de Microsoft
description: "¿Cómo toobuild una puerta de enlace de borde de IoT de Azure en una ventana de la máquina y obtener información sobre los conceptos clave de borde de IoT de Azure como módulos y archivos de configuración de JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5dd13cbfc02eeb55d9f2dbffca5021f2624acf14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a>Explorar la arquitectura de Azure IoT Edge en Windows

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>¿Cómo toorun Hola ejemplo

Hola **build.cmd** script genera su resultado en hello **generar** carpeta de la copia local de hello **iot borde** repositorio. Esta salida incluye dos módulos de borde IoT Hola utilizados en este ejemplo.

Hola lugares de la secuencia de comandos de compilación **logger.dll** en hello **generar\\módulos\\registrador\\depurar** carpeta y **hello\_world.dll**  en hello **generar\\módulos\\hello_world\\depurar** carpeta. Usar estas rutas de acceso para hello **ruta de acceso del módulo** valores tal y como se muestra en el siguiente archivo de configuración de JSON de Hola.

Hola Hola\_world\_proceso de ejemplo toma el archivo de configuración de hello ruta de acceso tooa JSON como un argumento de línea de comandos. siguiente archivo JSON de ejemplo Hola se proporciona una en el repositorio SDK de hello en **ejemplos\\hello\_world\\src\\hello\_world\_win.json**. Este archivo de configuración funciona tal cual a menos que modifique Hola compilar hello de la secuencia de comandos tooplace IoT borde módulos o archivos ejecutables en ubicaciones no predeterminadas de ejemplo.

> [!NOTE]
> las rutas de acceso del módulo de Hello son toohello relativa directorio donde hello hello\_world\_sample.exe se encuentra. ejemplo de Hola a JSON configuración archivo los valores predeterminados toowriting 'log.txt' en el directorio de trabajo actual.

```json
{
  "modules": [
    {
      "name": "logger",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
        }
      },
      "args": { "filename": "log.txt" }
    },
    {
      "name": "hello_world",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
        }
      },
      "args": null
      }
  ],
  "links": [
    {
      "source": "hello_world",
      "sink": "logger"
    }
  ]
}
```

1. Navegue toohello **generar** carpeta del directorio raíz de Hola de su copia local de hello **iot borde** repositorio.

1. Ejecute el siguiente comando de hello:

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
