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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a>Conectar su toohello de dispositivo remoto de supervisión de solución preconfigurada (Linux)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a>Compilación y ejecución de una aplicación cliente de C de ejemplo (Linux)
Hola pasos muestra cómo una aplicación cliente que se comunica con la supervisión remota de hello toocreate había preconfigurado solución. Esta aplicación se escribe en C y se compila y ejecuta en Ubuntu Linux.

toocomplete estos pasos, necesita un dispositivo que ejecuta Ubuntu versión 15.04 o 15.10. Antes de continuar, instalar paquetes de requisitos previos de hello en el dispositivo de Ubuntu mediante Hola siguiente comando:

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a>Instalar bibliotecas de cliente de hello en el dispositivo
Hello las bibliotecas de cliente de centro de IoT de Azure están disponibles como un paquete que se puede instalar en el dispositivo de Ubuntu mediante hello **apt get** comando. Hola completa siguiendo los pasos tooinstall Hola paquete que contiene Hola biblioteca de cliente de centro de IoT y archivos de encabezado en el equipo de Ubuntu:

1. En un shell, agregar equipo de hello AzureIoT repositorio tooyour:
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. Instalar el paquete de azure-iot-sdk-c-dev Hola
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a>Instalar Hola analizador Parson JSON
usan bibliotecas de cliente de centro de IoT Hola Hola cargas de mensajes JSON Parson analizador tooparse. En una carpeta adecuada en el equipo, clonar el repositorio de GitHub Parson de hello mediante Hola siguiente comando:

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a>Preparación del proyecto
En la máquina Ubuntu, cree una carpeta denominada **remote\_monitoring**. Hola **remoto\_supervisión** carpeta:

- Cree cuatro archivos de hello **main.c**, **remoto\_monitoring.c**, **remoto\_monitoring.h**, y **CMakeLists.txt**.
- Cree la carpeta denominada **parson**.

Copiar archivos de hello **parson.c** y **parson.h** desde una copia local del repositorio de Parson hello en hello **remoto\_supervisión/parson** carpeta.

En un editor de texto, abra hello **remoto\_monitoring.c** archivo. Agregue los siguiente hello `#include` instrucciones:
   
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

## <a name="call-hello-remotemonitoringrun-function"></a>Llamar a Hola remoto\_supervisión\_ejecutar (función)
En un editor de texto, abra hello **remote_monitoring.h** archivo. Agregue Hola siguiente código:

```
void remote_monitoring_run(void);
```

En un editor de texto, abra hello **main.c** archivo. Agregue Hola siguiente código:

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a>Compilar y ejecutar la aplicación hello
Hello pasos siguientes describen cómo toouse *CMake* toobuild la aplicación cliente.

1. En un editor de texto, abra hello **CMakeLists.txt** archivo Hola **remote_monitoring** carpeta.

1. Agregar Hola siguiendo las instrucciones toodefine cómo toobuild la aplicación cliente:
   
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
1. Hola **remote_monitoring** carpeta, cree un hello toostore de carpeta *realizar* archivos que CMake genera y, a continuación, ejecute hello **cmake** y **realizar** comandos como se indica a continuación:
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. Ejecutar la aplicación de cliente de hello y enviar telemetría tooIoT concentrador:
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

