---
title: "Introducción a Azure IoT Edge (Windows) | Documentos de Microsoft"
description: "Cómo crear una puerta de enlace de Azure IoT Edge en un equipo Windows y obtener información sobre los conceptos claves de Azure IoT Edge, como los módulos y los archivos de configuración de JSON."
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
ms.openlocfilehash: 5db39bab8e31a8e7026b34e72b4614b0f6f57772
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="b1d8f-103">Explorar la arquitectura de Azure IoT Edge en Windows</span><span class="sxs-lookup"><span data-stu-id="b1d8f-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="b1d8f-104">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="b1d8f-104">How to run the sample</span></span>

<span data-ttu-id="b1d8f-105">El script **build.cmd** genera su salida en la carpeta **build** de la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="b1d8f-106">Esta salida incluye los dos módulos de IoT Edge utilizados en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="b1d8f-107">El script de compilación coloca **logger.dll** en la carpeta **build\\modules\\logger\\Debug** y **hello\_world.dll** en la carpeta **build\\modules\\hello_world\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-107">The build script places **logger.dll** in the **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in the **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="b1d8f-108">Utilice estas rutas de acceso para los valores de **ruta de acceso del módulo**, tal y como se muestra en el archivo de configuración JSON siguiente.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-108">Use these paths for the **module path** values as shown in the following JSON settings file.</span></span>

<span data-ttu-id="b1d8f-109">El proceso de hello\_world\_sample toma la ruta de acceso a un archivo de configuración JSON como argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-109">The hello\_world\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="b1d8f-110">El siguiente archivo JSON de ejemplo se encuentra en el repositorio de SDK, en **samples\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-110">The following example JSON file is provided in the SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="b1d8f-111">Este archivo de configuración funcionará tal y como está, a menos que se modifique el script de compilación para colocar los módulos de IoT Edge o los ejecutables de ejemplo en ubicaciones que no sean las predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="b1d8f-112">Las rutas de acceso del módulo son relativas al directorio en el que se encuentra hello\_world\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-112">The module paths are relative to the directory where the hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="b1d8f-113">De manera predeterminada, el archivo de configuración JSON de ejemplo escribe "log.txt" en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="b1d8f-114">Vaya a la carpeta **build** en la raíz de la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="b1d8f-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="b1d8f-115">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b1d8f-115">Run the following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
