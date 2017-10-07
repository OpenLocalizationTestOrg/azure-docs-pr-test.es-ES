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
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="0367d-103">Explorar la arquitectura de Azure IoT Edge en Linux</span><span class="sxs-lookup"><span data-stu-id="0367d-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="0367d-104">¿Cómo toorun Hola ejemplo</span><span class="sxs-lookup"><span data-stu-id="0367d-104">How toorun hello sample</span></span>

<span data-ttu-id="0367d-105">Hola **build.sh** script genera su resultado en hello **generar** carpeta de la copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="0367d-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="0367d-106">Esta salida incluye dos módulos de borde IoT Hola utilizados en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0367d-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="0367d-107">Hola lugares de la secuencia de comandos de compilación **liblogger.so** en hello **compilación/módulos/registrador/** carpeta y **libhello\_world.so** en hello **compilar / módulos/hello_world/** carpeta.</span><span class="sxs-lookup"><span data-stu-id="0367d-107">hello build script places **liblogger.so** in hello **build/modules/logger/** folder and **libhello\_world.so** in hello **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="0367d-108">Usar estas rutas de acceso para hello **ruta de acceso del módulo** valores tal y como se muestra en el siguiente archivo de configuración de JSON de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0367d-108">Use these paths for hello **module path** values as shown in hello following example JSON settings file.</span></span>

<span data-ttu-id="0367d-109">Hola Hola\_world\_proceso de ejemplo toma el archivo de configuración de JSON de hello ruta de acceso tooa un argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="0367d-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file a command-line argument.</span></span> <span data-ttu-id="0367d-110">siguiente archivo JSON de ejemplo Hola se proporciona una en el repositorio SDK de hello en **ejemplos/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="0367d-110">hello following example JSON file is provided in hello SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="0367d-111">Este archivo de configuración funciona tal cual a menos que modifique Hola compilar hello de la secuencia de comandos tooplace IoT borde módulos o archivos ejecutables en ubicaciones no predeterminadas de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0367d-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="0367d-112">las rutas de acceso del módulo hello son toohello relativa de directorio de trabajo actual, desde donde Hola Hola\_world\_ejecutable de ejemplo se inicia, no Hola directorio donde se encuentra ejecutable hello.</span><span class="sxs-lookup"><span data-stu-id="0367d-112">hello module paths are relative toohello current working directory from where hello hello\_world\_sample executable is launched, not hello directory where hello executable is located.</span></span> <span data-ttu-id="0367d-113">ejemplo de Hola a JSON configuración archivo los valores predeterminados toowriting 'log.txt' en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="0367d-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="0367d-114">Navegue toohello **generar** carpeta del directorio raíz de Hola de su copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="0367d-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="0367d-115">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="0367d-115">Run hello following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

