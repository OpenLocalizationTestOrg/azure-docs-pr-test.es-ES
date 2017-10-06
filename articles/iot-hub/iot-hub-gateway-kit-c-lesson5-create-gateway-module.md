---
title: "aaaCreate el primer módulo de puerta de enlace de IoT de Azure | Documentos de Microsoft"
description: "Cree un módulo y agregar comportamientos de módulo de tooa ejemplo aplicación toocustomize."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Lección 5: Creación del primer módulo de puerta de enlace de IoT de Azure
Mientras que el borde de IoT de Azure permite módulos toobuild escritos en Java, .NET o Node.js, este tutorial le guiará por los pasos de hello para la creación de un módulo en C.

## <a name="what-you-will-do"></a>Lo que hará

- Compile y ejecute la aplicación de ejemplo de Hola hello_world en NUC de Intel.
- Cree un módulo y compílelo en Intel NUC.
- Agregar aplicación de hello nuevo módulo toohello hello_world ejemplo y, a continuación, ejecutar el ejemplo hello en NUC de Intel. nuevo módulo de Hello imprime mensajes de "hello_world" con una marca de tiempo.

## <a name="what-you-will-learn"></a>Lo qué aprenderá

- ¿Cómo toocompile y ejecutar una aplicación de ejemplo en NUC de Intel.
- ¿Cómo toocreate un módulo.
- ¿Cómo tooadd módulo tooa aplicación de ejemplo.

## <a name="what-you-need"></a>Lo que necesita

Azure IoT Edge que se ha instalado en el equipo host.

## <a name="folder-structure"></a>Estructura de carpetas

En la subcarpeta Hola lección 5 de código de ejemplo de Hola que se clonó en la lección 1, hay un `module` carpeta y un `sample` carpeta.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- Hola `module/my_module` carpeta contiene Hola código y los scripts toobuild Hola módulo de origen.
- Hola `sample` carpeta contiene Hola origen código y los scripts toobuild Hola aplicación de ejemplo.

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>Compile y ejecute la aplicación de ejemplo de Hola hello_world en NUC de Intel

Hola `hello_world` ejemplo crea una puerta de enlace en función de hello `hello_world.json` archivo que especifica Hola dos predefinidos módulos asociados con la aplicación hello. puerta de enlace de Hello registra un archivo de tooa de mensaje "¡hello world" cada 5 segundos. En esta sección, se compila y ejecuta hello `hello_world` aplicación con su módulo de manera predeterminada.

Hola toocompile y ejecute `hello_world` aplicación, siga estos pasos en el equipo host:

1. Inicializar archivos de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Actualizar el archivo de configuración de puerta de enlace de hello con hello dirección MAC de NUC de Intel. Omita este paso si ha realizado a través de la lección Hola demasiado[configurar y ejecutar una aplicación de ejemplo Bilitar][config_ble].

   1. Abra el archivo de configuración de puerta de enlace de hello ejecutando Hola siguiente comando:

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. La dirección MAC de actualización Hola la puerta de enlace cuando se [configurar Intel NUC como una puerta de enlace de IoT][setup_nuc]y, a continuación, guarde el archivo hello.

1. Compilar código fuente de ejemplo de Hola ejecutando Hola siguiente comando:

   ```bash
   gulp compile
   ```

   transfiere tooIntel de código de origen de ejemplo de Hola NUC Hello comando y se ejecuta `build.sh` toocompile lo.

1. Ejecute hello `hello_world` aplicación en Intel NUC ejecutando el siguiente comando de hello:

   ```bash
   gulp run
   ```

   Hola la ejecución del comando `../Tools/run-hello-world.js` que se especifica en `config.json` toostart aplicación de ejemplo de Hola en NUC de Intel.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Creación de un módulo y compilarlo en Intel NUC

estos pasos Hola guiarán para crear un nuevo módulo y compilan en NUC de Intel. módulo de Hello imprime los mensajes con una marca de tiempo tras su recepción. En esta sección va a crear el primer módulo de puerta de enlace personalizado.

Cualquier módulo de Azure IoT borde debe implementar Hola siguientes interfaces:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

Puede implementar opcionalmente Hola siguiendo la interfaz:

   ```C
   pfModule_Start Module_Start
   ```

Hello siguiente diagrama muestra las rutas de acceso de hello estado importantes de un módulo. rectángulos cuadrados Hola representan métodos implementan operaciones tooperform cuando el módulo de Hola se mueve entre Estados. óvalos Hola son Hola módulo puede estar en los Estados principales.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Ahora vamos a crear un módulo en función de plantilla de hello:

1. Abra la carpeta de plantillas de hello ejecutando el siguiente comando de hello:

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`actúa como una plantilla que facilita la creación de hello de un módulo. plantilla de Hello declara interfaces Hola. Todo lo que necesita toodo es tooadd lógica toohello `MyModule_Receive` función.
   - `build.sh`es el módulo hello toocompile de script de compilación de hello en NUC de Intel.
1. Abra hello `src/my_module.c` archivo e incluir los dos archivos de encabezado:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Agregar Hola después código toohello `MyModule_Receive` función:

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. Hola de actualización `config.json` Hola de archivo toospecify `workspace` carpeta en la ruta de implementación de hello y equipo de host en NUC de Intel. Durante la compilación, Hola archivos Hola `workspace` carpeta será la ruta de acceso de implementación de toohello transferidos.

   1. Abra hello `config.json` archivo ejecutando Hola siguiente comando:

      ```bash
      code config.json
      ```

   1. Actualización `config.json` con hello siguiente configuración:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Compile el módulo de hello ejecutando Hola siguiente comando:

   ```bash
   gulp compile
   ```

   transfiere Hola origen código tooIntel NUC Hello comando y se ejecuta `build.sh` módulo de hello toocompile.

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>Agregar aplicación de ejemplo de Hola módulo toohello hello_world y ejecutar la aplicación hello en NUC de Intel

tooperform esta tarea, siga estos pasos:

1. Lista de todos los binarios de módulo disponible hello (archivos. SO) en Intel NUC si ejecuta Hola siguiente comando:

   ```bash
   gulp modules --list
   ```

   ruta de acceso binaria Hola de `my_module` que ha compilado debe aparecer a la siguiente:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Si cambia el nombre de usuario de inicio de sesión de hello predeterminado en `config-gateway.json`, ruta de acceso binaria Hola se iniciará con `home/<your username>` en lugar de `root`.

1. Agregar `my_module` toohello `hello_world` aplicación de ejemplo:

   1. Abra hello `hello_world.json` archivo ejecutando Hola siguiente comando:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Agregar Hola después código toohello `modules` sección:

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      Hola valo `module.path` debe ser `/root/gateway_sample/module/my_module/build/libmy_module.so`. código de Hello declara `my_module` toobe asociado con puerta de enlace de hello, así como la ubicación de hello del archivo binario de módulo de hello especificado en `module.path`.
   1. Agregar Hola después código toohello `links` sección:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Este código especifica que se transfieren los mensajes de Hola `hello_world` módulo demasiado`my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Ejecute hello `hello_world` aplicación de ejemplo mediante la ejecución de hello siguiente comando:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   Hola `--config` parámetro fuerza hello `run-hello-world.js` toorun un script mediante el uso de hello `hello_world.json` archivo.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

¡Enhorabuena! Ahora puede ver el comportamiento de Hola de este nuevo módulo, simplemente imprime mensajes de "hello world" con una marca de tiempo, un resultado diferente de un módulo Hola original "hello_world".

## <a name="next-steps"></a>Pasos siguientes

Ha creado un nuevo módulo, agrega toohello hello_world ejemplo y aplicación de ejemplo de get hello toorun con el nuevo módulo de hello en la puerta de enlace. Si desea más información acerca de los módulos de puerta de enlace de IoT de Azure toolearn, puede encontrar más ejemplos de módulo aquí: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
