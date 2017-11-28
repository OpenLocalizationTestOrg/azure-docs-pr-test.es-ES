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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="76ee6-103">Lección 5: Creación del primer módulo de puerta de enlace de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="76ee6-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="76ee6-104">Mientras que el borde de IoT de Azure permite módulos toobuild escritos en Java, .NET o Node.js, este tutorial le guiará por los pasos de hello para la creación de un módulo en C.</span><span class="sxs-lookup"><span data-stu-id="76ee6-104">While Azure IoT Edge allows you toobuild modules written in Java, .NET, or Node.js, this tutorial walks you through hello steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="76ee6-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="76ee6-105">What you will do</span></span>

- <span data-ttu-id="76ee6-106">Compile y ejecute la aplicación de ejemplo de Hola hello_world en NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="76ee6-106">Compile and run hello hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="76ee6-107">Cree un módulo y compílelo en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="76ee6-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="76ee6-108">Agregar aplicación de hello nuevo módulo toohello hello_world ejemplo y, a continuación, ejecutar el ejemplo hello en NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="76ee6-108">Add hello new module toohello hello_world sample app and then run hello sample on Intel NUC.</span></span> <span data-ttu-id="76ee6-109">nuevo módulo de Hello imprime mensajes de "hello_world" con una marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="76ee6-109">hello new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="76ee6-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="76ee6-110">What you will learn</span></span>

- <span data-ttu-id="76ee6-111">¿Cómo toocompile y ejecutar una aplicación de ejemplo en NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="76ee6-111">How toocompile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="76ee6-112">¿Cómo toocreate un módulo.</span><span class="sxs-lookup"><span data-stu-id="76ee6-112">How toocreate a module.</span></span>
- <span data-ttu-id="76ee6-113">¿Cómo tooadd módulo tooa aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="76ee6-113">How tooadd module tooa sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="76ee6-114">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="76ee6-114">What you need</span></span>

<span data-ttu-id="76ee6-115">Azure IoT Edge que se ha instalado en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="76ee6-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="76ee6-116">Estructura de carpetas</span><span class="sxs-lookup"><span data-stu-id="76ee6-116">Folder structure</span></span>

<span data-ttu-id="76ee6-117">En la subcarpeta Hola lección 5 de código de ejemplo de Hola que se clonó en la lección 1, hay un `module` carpeta y un `sample` carpeta.</span><span class="sxs-lookup"><span data-stu-id="76ee6-117">In hello Lesson 5 subfolder of hello sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="76ee6-119">Hola `module/my_module` carpeta contiene Hola código y los scripts toobuild Hola módulo de origen.</span><span class="sxs-lookup"><span data-stu-id="76ee6-119">hello `module/my_module` folder contains hello source code and script toobuild hello module.</span></span>
- <span data-ttu-id="76ee6-120">Hola `sample` carpeta contiene Hola origen código y los scripts toobuild Hola aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="76ee6-120">hello `sample` folder contains hello source code and script toobuild hello sample app.</span></span>

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="76ee6-121">Compile y ejecute la aplicación de ejemplo de Hola hello_world en NUC de Intel</span><span class="sxs-lookup"><span data-stu-id="76ee6-121">Compile and run hello hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="76ee6-122">Hola `hello_world` ejemplo crea una puerta de enlace en función de hello `hello_world.json` archivo que especifica Hola dos predefinidos módulos asociados con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="76ee6-122">hello `hello_world` sample creates a gateway based on hello `hello_world.json` file which specifies hello two predefined modules associated with hello app.</span></span> <span data-ttu-id="76ee6-123">puerta de enlace de Hello registra un archivo de tooa de mensaje "¡hello world" cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="76ee6-123">hello gateway logs a "hello world" message tooa file every 5 seconds.</span></span> <span data-ttu-id="76ee6-124">En esta sección, se compila y ejecuta hello `hello_world` aplicación con su módulo de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="76ee6-124">In this section, you compile and run hello `hello_world` app with its default module.</span></span>

<span data-ttu-id="76ee6-125">Hola toocompile y ejecute `hello_world` aplicación, siga estos pasos en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="76ee6-125">toocompile and run hello `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="76ee6-126">Inicializar archivos de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="76ee6-126">Initialize hello configuration files by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="76ee6-127">Actualizar el archivo de configuración de puerta de enlace de hello con hello dirección MAC de NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="76ee6-127">Update hello gateway configuration file with hello MAC address of Intel NUC.</span></span> <span data-ttu-id="76ee6-128">Omita este paso si ha realizado a través de la lección Hola demasiado[configurar y ejecutar una aplicación de ejemplo Bilitar][config_ble].</span><span class="sxs-lookup"><span data-stu-id="76ee6-128">Skip this step if you have gone through hello lesson too[configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="76ee6-129">Abra el archivo de configuración de puerta de enlace de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76ee6-129">Open hello gateway configuration file by running hello following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="76ee6-130">La dirección MAC de actualización Hola la puerta de enlace cuando se [configurar Intel NUC como una puerta de enlace de IoT][setup_nuc]y, a continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="76ee6-130">Update hello gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save hello file.</span></span>

1. <span data-ttu-id="76ee6-131">Compilar código fuente de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76ee6-131">Compile hello sample source code by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="76ee6-132">transfiere tooIntel de código de origen de ejemplo de Hola NUC Hello comando y se ejecuta `build.sh` toocompile lo.</span><span class="sxs-lookup"><span data-stu-id="76ee6-132">hello command transfers hello sample source code tooIntel NUC and runs `build.sh` toocompile it.</span></span>

1. <span data-ttu-id="76ee6-133">Ejecute hello `hello_world` aplicación en Intel NUC ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="76ee6-133">Run hello `hello_world` app on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="76ee6-134">Hola la ejecución del comando `../Tools/run-hello-world.js` que se especifica en `config.json` toostart aplicación de ejemplo de Hola en NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="76ee6-134">hello command runs `../Tools/run-hello-world.js` that is specified in `config.json` toostart hello sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="76ee6-136">Creación de un módulo y compilarlo en Intel NUC</span><span class="sxs-lookup"><span data-stu-id="76ee6-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="76ee6-137">estos pasos Hola guiarán para crear un nuevo módulo y compilan en NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="76ee6-137">hello steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="76ee6-138">módulo de Hello imprime los mensajes con una marca de tiempo tras su recepción.</span><span class="sxs-lookup"><span data-stu-id="76ee6-138">hello module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="76ee6-139">En esta sección va a crear el primer módulo de puerta de enlace personalizado.</span><span class="sxs-lookup"><span data-stu-id="76ee6-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="76ee6-140">Cualquier módulo de Azure IoT borde debe implementar Hola siguientes interfaces:</span><span class="sxs-lookup"><span data-stu-id="76ee6-140">Any Azure IoT Edge module must implement hello following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="76ee6-141">Puede implementar opcionalmente Hola siguiendo la interfaz:</span><span class="sxs-lookup"><span data-stu-id="76ee6-141">You can optionally implement hello following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="76ee6-142">Hello siguiente diagrama muestra las rutas de acceso de hello estado importantes de un módulo.</span><span class="sxs-lookup"><span data-stu-id="76ee6-142">hello following diagram shows hello important state paths of a module.</span></span> <span data-ttu-id="76ee6-143">rectángulos cuadrados Hola representan métodos implementan operaciones tooperform cuando el módulo de Hola se mueve entre Estados.</span><span class="sxs-lookup"><span data-stu-id="76ee6-143">hello square rectangles represent methods you implement tooperform operations when hello module moves between states.</span></span> <span data-ttu-id="76ee6-144">óvalos Hola son Hola módulo puede estar en los Estados principales.</span><span class="sxs-lookup"><span data-stu-id="76ee6-144">hello ovals are major states hello module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="76ee6-146">Ahora vamos a crear un módulo en función de plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="76ee6-146">Now let’s create a module based on hello template:</span></span>

1. <span data-ttu-id="76ee6-147">Abra la carpeta de plantillas de hello ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="76ee6-147">Open hello template folder by running hello following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="76ee6-149">`src/my_module.c`actúa como una plantilla que facilita la creación de hello de un módulo.</span><span class="sxs-lookup"><span data-stu-id="76ee6-149">`src/my_module.c` serves as a template that facilitates hello creation of a module.</span></span> <span data-ttu-id="76ee6-150">plantilla de Hello declara interfaces Hola.</span><span class="sxs-lookup"><span data-stu-id="76ee6-150">hello template declares hello interfaces.</span></span> <span data-ttu-id="76ee6-151">Todo lo que necesita toodo es tooadd lógica toohello `MyModule_Receive` función.</span><span class="sxs-lookup"><span data-stu-id="76ee6-151">All you need toodo is tooadd logic toohello `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="76ee6-152">`build.sh`es el módulo hello toocompile de script de compilación de hello en NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="76ee6-152">`build.sh` is hello build script toocompile hello module on Intel NUC.</span></span>
1. <span data-ttu-id="76ee6-153">Abra hello `src/my_module.c` archivo e incluir los dos archivos de encabezado:</span><span class="sxs-lookup"><span data-stu-id="76ee6-153">Open hello `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="76ee6-154">Agregar Hola después código toohello `MyModule_Receive` función:</span><span class="sxs-lookup"><span data-stu-id="76ee6-154">Add hello following code toohello `MyModule_Receive` function:</span></span>

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

1. <span data-ttu-id="76ee6-155">Hola de actualización `config.json` Hola de archivo toospecify `workspace` carpeta en la ruta de implementación de hello y equipo de host en NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="76ee6-155">Update hello `config.json` file toospecify hello `workspace` folder on your host computer and hello deployment path on Intel NUC.</span></span> <span data-ttu-id="76ee6-156">Durante la compilación, Hola archivos Hola `workspace` carpeta será la ruta de acceso de implementación de toohello transferidos.</span><span class="sxs-lookup"><span data-stu-id="76ee6-156">During compiling, hello files in hello `workspace` folder will be transferred toohello deployment path.</span></span>

   1. <span data-ttu-id="76ee6-157">Abra hello `config.json` archivo ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76ee6-157">Open hello `config.json` file by running hello following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="76ee6-158">Actualización `config.json` con hello siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="76ee6-158">Update `config.json` with hello following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="76ee6-160">Compile el módulo de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76ee6-160">Compile hello module by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="76ee6-161">transfiere Hola origen código tooIntel NUC Hello comando y se ejecuta `build.sh` módulo de hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="76ee6-161">hello command transfers hello source code tooIntel NUC and runs `build.sh` toocompile hello module.</span></span>

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a><span data-ttu-id="76ee6-162">Agregar aplicación de ejemplo de Hola módulo toohello hello_world y ejecutar la aplicación hello en NUC de Intel</span><span class="sxs-lookup"><span data-stu-id="76ee6-162">Add hello module toohello hello_world sample app and run hello app on Intel NUC</span></span>

<span data-ttu-id="76ee6-163">tooperform esta tarea, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="76ee6-163">tooperform this task, follow these steps:</span></span>

1. <span data-ttu-id="76ee6-164">Lista de todos los binarios de módulo disponible hello (archivos. SO) en Intel NUC si ejecuta Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76ee6-164">List all hello available module binaries (.so files) on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="76ee6-165">ruta de acceso binaria Hola de `my_module` que ha compilado debe aparecer a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="76ee6-165">hello binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="76ee6-166">Si cambia el nombre de usuario de inicio de sesión de hello predeterminado en `config-gateway.json`, ruta de acceso binaria Hola se iniciará con `home/<your username>` en lugar de `root`.</span><span class="sxs-lookup"><span data-stu-id="76ee6-166">If you change hello default login username in `config-gateway.json`, hello binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="76ee6-167">Agregar `my_module` toohello `hello_world` aplicación de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="76ee6-167">Add `my_module` toohello `hello_world` sample app:</span></span>

   1. <span data-ttu-id="76ee6-168">Abra hello `hello_world.json` archivo ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76ee6-168">Open hello `hello_world.json` file by running hello following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="76ee6-169">Agregar Hola después código toohello `modules` sección:</span><span class="sxs-lookup"><span data-stu-id="76ee6-169">Add hello following code toohello `modules` section:</span></span>

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

      <span data-ttu-id="76ee6-170">Hola valo `module.path` debe ser `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="76ee6-170">hello value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="76ee6-171">código de Hello declara `my_module` toobe asociado con puerta de enlace de hello, así como la ubicación de hello del archivo binario de módulo de hello especificado en `module.path`.</span><span class="sxs-lookup"><span data-stu-id="76ee6-171">hello code declares `my_module` toobe associated with hello gateway as well as hello location of hello module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="76ee6-172">Agregar Hola después código toohello `links` sección:</span><span class="sxs-lookup"><span data-stu-id="76ee6-172">Add hello following code toohello `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="76ee6-173">Este código especifica que se transfieren los mensajes de Hola `hello_world` módulo demasiado`my_module`.</span><span class="sxs-lookup"><span data-stu-id="76ee6-173">This code specifies that messages are transferred from hello `hello_world` module too`my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="76ee6-175">Ejecute hello `hello_world` aplicación de ejemplo mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76ee6-175">Run hello `hello_world` sample app by running hello following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="76ee6-176">Hola `--config` parámetro fuerza hello `run-hello-world.js` toorun un script mediante el uso de hello `hello_world.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="76ee6-176">hello `--config` parameter forces hello `run-hello-world.js` script toorun by using hello `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="76ee6-178">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="76ee6-178">Congratulations.</span></span> <span data-ttu-id="76ee6-179">Ahora puede ver el comportamiento de Hola de este nuevo módulo, simplemente imprime mensajes de "hello world" con una marca de tiempo, un resultado diferente de un módulo Hola original "hello_world".</span><span class="sxs-lookup"><span data-stu-id="76ee6-179">You can now see hello behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from hello original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76ee6-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76ee6-180">Next Steps</span></span>

<span data-ttu-id="76ee6-181">Ha creado un nuevo módulo, agrega toohello hello_world ejemplo y aplicación de ejemplo de get hello toorun con el nuevo módulo de hello en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="76ee6-181">You’ve created a new module, added it toohello hello_world sample, and get hello sample app toorun with hello new module on your gateway.</span></span> <span data-ttu-id="76ee6-182">Si desea más información acerca de los módulos de puerta de enlace de IoT de Azure toolearn, puede encontrar más ejemplos de módulo aquí: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="76ee6-182">If you want toolearn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
