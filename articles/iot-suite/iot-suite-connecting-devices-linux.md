---
title: aaaConnect un dispositivo mediante C en Linux | Documentos de Microsoft
description: "Describe cómo tooconnect una toohello dispositivo Azure IoT conjunto preconfigurado solución de supervisión remota con una aplicación escrita en C que se ejecutan en Linux."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="7971a-103">Conectar su toohello de dispositivo remoto de supervisión de solución preconfigurada (Linux)</span><span class="sxs-lookup"><span data-stu-id="7971a-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="7971a-104">Compilación y ejecución de una aplicación cliente de C de ejemplo (Linux)</span><span class="sxs-lookup"><span data-stu-id="7971a-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="7971a-105">Hola pasos muestra cómo una aplicación cliente que se comunica con la supervisión remota de hello toocreate había preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="7971a-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="7971a-106">Esta aplicación se escribe en C y se compila y ejecuta en Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="7971a-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="7971a-107">toocomplete estos pasos, necesita un dispositivo que ejecuta Ubuntu versión 15.04 o 15.10.</span><span class="sxs-lookup"><span data-stu-id="7971a-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="7971a-108">Antes de continuar, instalar paquetes de requisitos previos de hello en el dispositivo de Ubuntu mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7971a-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="7971a-109">Instalar bibliotecas de cliente de hello en el dispositivo</span><span class="sxs-lookup"><span data-stu-id="7971a-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="7971a-110">Hello las bibliotecas de cliente de centro de IoT de Azure están disponibles como un paquete que se puede instalar en el dispositivo de Ubuntu mediante hello **apt get** comando.</span><span class="sxs-lookup"><span data-stu-id="7971a-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="7971a-111">Hola completa siguiendo los pasos tooinstall Hola paquete que contiene Hola biblioteca de cliente de centro de IoT y archivos de encabezado en el equipo de Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="7971a-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="7971a-112">En un shell, agregar equipo de hello AzureIoT repositorio tooyour:</span><span class="sxs-lookup"><span data-stu-id="7971a-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="7971a-113">Instalar el paquete de azure-iot-sdk-c-dev Hola</span><span class="sxs-lookup"><span data-stu-id="7971a-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="7971a-114">Instalar Hola analizador Parson JSON</span><span class="sxs-lookup"><span data-stu-id="7971a-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="7971a-115">usan bibliotecas de cliente de centro de IoT Hola Hola cargas de mensajes JSON Parson analizador tooparse.</span><span class="sxs-lookup"><span data-stu-id="7971a-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="7971a-116">En una carpeta adecuada en el equipo, clonar el repositorio de GitHub Parson de hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7971a-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="7971a-117">Preparación del proyecto</span><span class="sxs-lookup"><span data-stu-id="7971a-117">Prepare your project</span></span>
<span data-ttu-id="7971a-118">En la máquina Ubuntu, cree una carpeta denominada **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="7971a-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="7971a-119">Hola **remoto\_supervisión** carpeta:</span><span class="sxs-lookup"><span data-stu-id="7971a-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="7971a-120">Cree cuatro archivos de hello **main.c**, **remoto\_monitoring.c**, **remoto\_monitoring.h**, y **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="7971a-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="7971a-121">Cree la carpeta denominada **parson**.</span><span class="sxs-lookup"><span data-stu-id="7971a-121">Create folder called **parson**.</span></span>

<span data-ttu-id="7971a-122">Copiar archivos de hello **parson.c** y **parson.h** desde una copia local del repositorio de Parson hello en hello **remoto\_supervisión/parson** carpeta.</span><span class="sxs-lookup"><span data-stu-id="7971a-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="7971a-123">En un editor de texto, abra hello **remoto\_monitoring.c** archivo.</span><span class="sxs-lookup"><span data-stu-id="7971a-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="7971a-124">Agregue los siguiente hello `#include` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="7971a-124">Add hello following `#include` statements:</span></span>
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="7971a-125">Llamar a Hola remoto\_supervisión\_ejecutar (función)</span><span class="sxs-lookup"><span data-stu-id="7971a-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="7971a-126">En un editor de texto, abra hello **remote_monitoring.h** archivo.</span><span class="sxs-lookup"><span data-stu-id="7971a-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="7971a-127">Agregue Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="7971a-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="7971a-128">En un editor de texto, abra hello **main.c** archivo.</span><span class="sxs-lookup"><span data-stu-id="7971a-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="7971a-129">Agregue Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="7971a-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="7971a-130">Compilar y ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="7971a-130">Build and run hello application</span></span>
<span data-ttu-id="7971a-131">Hello pasos siguientes describen cómo toouse *CMake* toobuild la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="7971a-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="7971a-132">En un editor de texto, abra hello **CMakeLists.txt** archivo Hola **remote_monitoring** carpeta.</span><span class="sxs-lookup"><span data-stu-id="7971a-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="7971a-133">Agregar Hola siguiendo las instrucciones toodefine cómo toobuild la aplicación cliente:</span><span class="sxs-lookup"><span data-stu-id="7971a-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. <span data-ttu-id="7971a-134">Hola **remote_monitoring** carpeta, cree un hello toostore de carpeta *realizar* archivos que CMake genera y, a continuación, ejecute hello **cmake** y **realizar** comandos como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="7971a-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="7971a-135">Ejecutar la aplicación de cliente de hello y enviar telemetría tooIoT concentrador:</span><span class="sxs-lookup"><span data-stu-id="7971a-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

