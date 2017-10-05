---
title: "Introducción a Azure IoT Edge (Linux) | Microsoft Docs"
description: "Cómo crear una puerta de enlace en un equipo Linux y obtener información sobre los conceptos claves de Azure IoT Edge, como los módulos y los archivos de configuración de JSON."
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
ms.openlocfilehash: b02d79fcd9cd2a2ef0041aac4e85528263c8d58a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="b553e-103">Explorar la arquitectura de Azure IoT Edge en Linux</span><span class="sxs-lookup"><span data-stu-id="b553e-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="b553e-104">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="b553e-104">How to run the sample</span></span>

<span data-ttu-id="b553e-105">El script **build.sh** genera su salida en la carpeta **build** de la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="b553e-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="b553e-106">Esta salida incluye los dos módulos de IoT Edge utilizados en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b553e-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="b553e-107">El script de compilación coloca **liblogger.so** en la carpeta **build/modules/logger/** y **lib\_helloworld.so** en la carpeta **build/modules/hello_world/**.</span><span class="sxs-lookup"><span data-stu-id="b553e-107">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="b553e-108">Use estas rutas de acceso en los valores de **module path**, tal y como se muestra en el archivo de configuración JSON siguiente.</span><span class="sxs-lookup"><span data-stu-id="b553e-108">Use these paths for the **module path** values as shown in the following example JSON settings file.</span></span>

<span data-ttu-id="b553e-109">El proceso de hello\_world\_sample acepta la ruta de acceso a un archivo de configuración JSON como argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="b553e-109">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span></span> <span data-ttu-id="b553e-110">El siguiente archivo JSON de ejemplo se encuentra en el repositorio de SDK, en **samples/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="b553e-110">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="b553e-111">Este archivo de configuración funciona tal y como está, a menos que se modifique el script de compilación para colocar los módulos de IoT Edge o los ejecutables de ejemplo en ubicaciones diferentes de las predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="b553e-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="b553e-112">Las rutas de acceso del módulo son relativas al directorio de trabajo actual desde donde se inicia el archivo ejecutable hello\_world\_sample, no el directorio donde se encuentra el archivo ejecutable.</span><span class="sxs-lookup"><span data-stu-id="b553e-112">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span></span> <span data-ttu-id="b553e-113">De manera predeterminada, el archivo de configuración JSON de ejemplo escribe "log.txt" en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="b553e-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="b553e-114">Vaya a la carpeta **build** en la raíz de la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="b553e-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="b553e-115">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b553e-115">Run the following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

