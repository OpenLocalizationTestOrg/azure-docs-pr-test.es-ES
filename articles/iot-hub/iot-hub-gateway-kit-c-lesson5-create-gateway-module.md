---
title: "Creación del primer módulo de puerta de enlace de IoT de Azure | Microsoft Docs"
description: "Cree un módulo y agréguelo a una aplicación de ejemplo para personalizar los comportamientos del módulo."
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
ms.openlocfilehash: 5e28422158684c3aaf0ac3fdf5b19c80fbccfb02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="102e1-103">Lección 5: Creación del primer módulo de puerta de enlace de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="102e1-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="102e1-104">Aunque Azure IoT Edge permite compilar módulos escritos en Java, .NET o Node.js, este tutorial le guía por los pasos para compilar un módulo en C.</span><span class="sxs-lookup"><span data-stu-id="102e1-104">While Azure IoT Edge allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="102e1-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="102e1-105">What you will do</span></span>

- <span data-ttu-id="102e1-106">Compile y ejecute la aplicación de ejemplo hello_world en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="102e1-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="102e1-107">Cree un módulo y compílelo en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="102e1-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="102e1-108">Agregue el nuevo módulo a la aplicación de ejemplo hello_world y, después, ejecute el ejemplo en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="102e1-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="102e1-109">El nuevo módulo imprime mensajes de "hello_world" con una marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="102e1-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="102e1-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="102e1-110">What you will learn</span></span>

- <span data-ttu-id="102e1-111">Cómo compilar y ejecutar la aplicación de ejemplo hello_world en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="102e1-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="102e1-112">Cómo crear un módulo.</span><span class="sxs-lookup"><span data-stu-id="102e1-112">How to create a module.</span></span>
- <span data-ttu-id="102e1-113">Cómo agregar un módulo a una aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="102e1-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="102e1-114">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="102e1-114">What you need</span></span>

<span data-ttu-id="102e1-115">Azure IoT Edge que se ha instalado en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="102e1-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="102e1-116">Estructura de carpetas</span><span class="sxs-lookup"><span data-stu-id="102e1-116">Folder structure</span></span>

<span data-ttu-id="102e1-117">En la subcarpeta de la lección 5 del código de ejemplo que se clonó en la lección 1, hay una carpeta `module` y una carpeta `sample`.</span><span class="sxs-lookup"><span data-stu-id="102e1-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="102e1-119">La carpeta `module/my_module` contiene el código fuente y el script para crear el módulo.</span><span class="sxs-lookup"><span data-stu-id="102e1-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="102e1-120">La carpeta `sample` contiene el código fuente y el script para crear la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="102e1-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="102e1-121">Compilación y ejecución de la aplicación de ejemplo hello_world en Intel NUC</span><span class="sxs-lookup"><span data-stu-id="102e1-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="102e1-122">El ejemplo `hello_world` crea una puerta de enlace basada en el archivo `hello_world.json` que especifica los dos módulos predefinidos asociados a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="102e1-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="102e1-123">La puerta de enlace registra un mensaje "hello world" en un archivo cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="102e1-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="102e1-124">En esta sección, se compila y ejecuta la aplicación `hello_world` con su módulo predeterminado.</span><span class="sxs-lookup"><span data-stu-id="102e1-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="102e1-125">Para compilar y ejecutar la aplicación `hello_world`, siga estos pasos en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="102e1-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="102e1-126">Inicialice el archivo de configuración mediante la ejecución de los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="102e1-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="102e1-127">Actualice el archivo de configuración de puerta de enlace con la dirección MAC de Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="102e1-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="102e1-128">Omita este paso si ha leído la lección [Configuración y ejecución de la aplicación de ejemplo BLE][config_ble].</span><span class="sxs-lookup"><span data-stu-id="102e1-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="102e1-129">Genere el archivo de configuración de puerta de enlace mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="102e1-130">Actualice las direcciones MAC de la puerta de enlace cuando [configure Intel NUC como una puerta de enlace de IoT][setup_nuc] y, después, guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="102e1-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="102e1-131">Compile el código fuente de ejemplo mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="102e1-132">El comando transfiere el código fuente de ejemplo a Intel NUC y ejecuta `build.sh` para compilarlo.</span><span class="sxs-lookup"><span data-stu-id="102e1-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="102e1-133">Ejecute la aplicación `hello_world` en Intel NUC mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="102e1-134">El comando ejecuta `../Tools/run-hello-world.js`, que en `config.json` está especificado para iniciar la aplicación de ejemplo en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="102e1-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="102e1-136">Creación de un módulo y compilarlo en Intel NUC</span><span class="sxs-lookup"><span data-stu-id="102e1-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="102e1-137">Los pasos siguientes lo guían para crear un módulo y compilarlo en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="102e1-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="102e1-138">El módulo imprime los mensajes con una marca de tiempo tras su recepción.</span><span class="sxs-lookup"><span data-stu-id="102e1-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="102e1-139">En esta sección va a crear el primer módulo de puerta de enlace personalizado.</span><span class="sxs-lookup"><span data-stu-id="102e1-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="102e1-140">Cualquier módulo de Azure IoT Edge debe implementar las siguientes interfaces:</span><span class="sxs-lookup"><span data-stu-id="102e1-140">Any Azure IoT Edge module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="102e1-141">También puede implementar la interfaz siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="102e1-142">El diagrama siguiente muestra las rutas de acceso de estado importantes de un módulo.</span><span class="sxs-lookup"><span data-stu-id="102e1-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="102e1-143">Los rectángulos cuadrados representan métodos que se implementan para llevar a cabo operaciones cuando el módulo se mueve entre estados.</span><span class="sxs-lookup"><span data-stu-id="102e1-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="102e1-144">Las formas ovaladas representan los estados más importantes que un módulo puede tener.</span><span class="sxs-lookup"><span data-stu-id="102e1-144">The ovals are major states the module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="102e1-146">Ahora se va a crear un módulo basado en la plantilla:</span><span class="sxs-lookup"><span data-stu-id="102e1-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="102e1-147">Abra la carpeta de la plantilla mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="102e1-149">`src/my_module.c` actúa como una plantilla que facilita la creación de un módulo.</span><span class="sxs-lookup"><span data-stu-id="102e1-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="102e1-150">La plantilla declara las interfaces.</span><span class="sxs-lookup"><span data-stu-id="102e1-150">The template declares the interfaces.</span></span> <span data-ttu-id="102e1-151">Lo único que necesita es agregar lógica a la función `MyModule_Receive`.</span><span class="sxs-lookup"><span data-stu-id="102e1-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="102e1-152">`build.sh` es el script para compilar el módulo en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="102e1-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="102e1-153">Abra el archivo `src/my_module.c` e incluya dos archivos de encabezado:</span><span class="sxs-lookup"><span data-stu-id="102e1-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="102e1-154">Agregue el siguiente código a la función `MyModule_Receive`:</span><span class="sxs-lookup"><span data-stu-id="102e1-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
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
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="102e1-155">Actualice el archivo `config.json` para especificar la carpeta `workspace` en el equipo host y la ruta de acceso de la implementación en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="102e1-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="102e1-156">Durante la compilación, los archivos de la carpeta `workspace` se transferirán a la ruta de acceso de la implementación.</span><span class="sxs-lookup"><span data-stu-id="102e1-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="102e1-157">Abra el archivo `config.json` mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="102e1-158">Actualice `config.json` con la configuración siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="102e1-160">Compile el módulo mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="102e1-161">El comando transfiere el código fuente a Intel NUC y ejecuta `build.sh` para compilar el módulo.</span><span class="sxs-lookup"><span data-stu-id="102e1-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="102e1-162">Agregar el módulo a la aplicación de ejemplo hello_world y ejecutar la aplicación en Intel NUC</span><span class="sxs-lookup"><span data-stu-id="102e1-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="102e1-163">Para realizar esta tarea, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="102e1-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="102e1-164">Enumere todos los archivos binarios disponibles en el módulo (archivos .so) en Intel NUC mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="102e1-165">La ruta de acceso binaria de `my_module` que ha compilado debe aparecer como sigue:</span><span class="sxs-lookup"><span data-stu-id="102e1-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="102e1-166">Si cambia el nombre de usuario de inicio de sesión predeterminado en `config-gateway.json`, la ruta de acceso binaria se iniciará con `home/<your username>` en lugar de con `root`.</span><span class="sxs-lookup"><span data-stu-id="102e1-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="102e1-167">Agregue `my_module` a la aplicación de ejemplo `hello_world`:</span><span class="sxs-lookup"><span data-stu-id="102e1-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="102e1-168">Abra el archivo `hello_world.json` mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="102e1-169">Agregue el siguiente código a la sección `modules`:</span><span class="sxs-lookup"><span data-stu-id="102e1-169">Add the following code to the `modules` section:</span></span>

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

      <span data-ttu-id="102e1-170">El valor de `module.path` debe ser `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="102e1-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="102e1-171">El código declara que `my_module` se asocie con la puerta de enlace y la ubicación del archivo binario del módulo especificado en `module.path`.</span><span class="sxs-lookup"><span data-stu-id="102e1-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="102e1-172">Agregue el siguiente código a la sección `links`:</span><span class="sxs-lookup"><span data-stu-id="102e1-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="102e1-173">Este código especifica que los mensajes se transfieran del módulo `hello_world` a `my_module`.</span><span class="sxs-lookup"><span data-stu-id="102e1-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="102e1-175">Ejecute la aplicación de ejemplo `hello_world` mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="102e1-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="102e1-176">El parámetro `--config` fuerza la ejecución del script `run-hello-world.js` con la utilización del archivo `hello_world.json`.</span><span class="sxs-lookup"><span data-stu-id="102e1-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="102e1-178">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="102e1-178">Congratulations.</span></span> <span data-ttu-id="102e1-179">Ahora puede ver el comportamiento de este nuevo módulo; simplemente imprime mensajes de "hello world" con una marca de tiempo, un resultado diferente del módulo original de "hello_world".</span><span class="sxs-lookup"><span data-stu-id="102e1-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="102e1-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="102e1-180">Next Steps</span></span>

<span data-ttu-id="102e1-181">Ha creado un módulo, lo ha agregado al ejemplo hello_world y ha hecho que la aplicación de ejemplo se ejecute con el nuevo módulo en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="102e1-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="102e1-182">Si desea obtener más información sobre los módulos de puerta de enlace de IoT de Azure, puede encontrar más ejemplos de módulo aquí: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="102e1-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md