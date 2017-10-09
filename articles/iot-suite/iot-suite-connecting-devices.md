---
title: aaaConnect un dispositivo mediante C en Windows | Documentos de Microsoft
description: "Describe cómo tooconnect una toohello dispositivo Azure IoT conjunto preconfigurado solución de supervisión remota con una aplicación escrita en C que se ejecutan en Windows."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="a7981-103">Conectar su toohello de dispositivo remoto de supervisión de solución preconfigurada (Windows)</span><span class="sxs-lookup"><span data-stu-id="a7981-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="a7981-104">Creación de una solución de ejemplo de C en Windows</span><span class="sxs-lookup"><span data-stu-id="a7981-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="a7981-105">Hola pasos muestra cómo una aplicación cliente que se comunica con la supervisión remota de hello toocreate había preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="a7981-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="a7981-106">Esta aplicación se escribe en C y se compila y ejecuta en Windows.</span><span class="sxs-lookup"><span data-stu-id="a7981-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="a7981-107">Cree un proyecto de inicio en Visual Studio 2015 o Visual Studio de 2017 y agregue paquetes de NuGet de hello centro de IoT dispositivo cliente:</span><span class="sxs-lookup"><span data-stu-id="a7981-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="a7981-108">En Visual Studio, cree una aplicación de consola de C con Visual C++ hello **aplicación de consola Win32** plantilla.</span><span class="sxs-lookup"><span data-stu-id="a7981-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="a7981-109">Proyecto de hello Name **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="a7981-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="a7981-110">En hello **configuración de la aplicación** página Hola **Asistente para aplicaciones Win32**, asegúrese de que **aplicación de consola** está seleccionada y desactive la opción **precompilado encabezado** y **comprobaciones del ciclo de vida de desarrollo de seguridad (SDL)**.</span><span class="sxs-lookup"><span data-stu-id="a7981-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="a7981-111">En **el Explorador de soluciones**, eliminar Hola archivos stdafx.h, targetver.h y stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="a7981-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="a7981-112">En **el Explorador de soluciones**, cambie el nombre hello archivo RMDevice.cpp tooRMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="a7981-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="a7981-113">En **el Explorador de soluciones**, haga doble clic en hello **RMDevice** del proyecto y, a continuación, haga clic en **administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a7981-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="a7981-114">Haga clic en **examinar**, a continuación, buscar e instalar Hola siguientes paquetes de NuGet:</span><span class="sxs-lookup"><span data-stu-id="a7981-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="a7981-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="a7981-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="a7981-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="a7981-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="a7981-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="a7981-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="a7981-118">En **el Explorador de soluciones**, haga doble clic en hello **RMDevice** del proyecto y, a continuación, haga clic en **propiedades** del proyecto de tooopen hello **páginas de propiedades**cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7981-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="a7981-119">Para obtener información, consulte [Setting Visual C++ Project Properties][lnk-c-project-properties] (Establecimiento de propiedades de proyectos de Visual C++).</span><span class="sxs-lookup"><span data-stu-id="a7981-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="a7981-120">Haga clic en hello **vinculador** carpeta, a continuación, haga clic en hello **entrada** página de propiedades.</span><span class="sxs-lookup"><span data-stu-id="a7981-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="a7981-121">Agregar **crypt32.lib** toohello **dependencias adicionales** propiedad.</span><span class="sxs-lookup"><span data-stu-id="a7981-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="a7981-122">Haga clic en **Aceptar** y, a continuación, **Aceptar** valores de propiedad toosave Hola proyecto nuevo.</span><span class="sxs-lookup"><span data-stu-id="a7981-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="a7981-123">Agregar hello Parson JSON biblioteca toohello **RMDevice** del proyecto y agregue Hola necesario `#include` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="a7981-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="a7981-124">En una carpeta adecuada en el equipo, clonar el repositorio de GitHub Parson de hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a7981-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="a7981-125">Copie los archivos de parson.h y parson.c de Hola desde la copia local de Hola de hello Parson repositorio tooyour **RMDevice** carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a7981-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="a7981-126">En Visual Studio, haga clic en hello **RMDevice** proyecto de equipo y haga clic en **agregar**y, a continuación, haga clic en **elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="a7981-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="a7981-127">Hola **Agregar elemento existente** cuadro de diálogo, los archivos de parson.h y parson.c de select Hola Hola **RMDevice** carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a7981-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="a7981-128">A continuación, haga clic en **agregar** tooadd estos proyectos de tooyour dos archivos.</span><span class="sxs-lookup"><span data-stu-id="a7981-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="a7981-129">En Visual Studio, abra el archivo de hello RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="a7981-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="a7981-130">Reemplazar existente hello `#include` instrucciones con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="a7981-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > <span data-ttu-id="a7981-131">Ahora puede comprobar que el proyecto tiene dependencias correctas Hola configurar compilarlas.</span><span class="sxs-lookup"><span data-stu-id="a7981-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="a7981-132">Compilar y ejecutar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="a7981-132">Build and run hello sample</span></span>

<span data-ttu-id="a7981-133">Agregar Hola de código tooinvoke **remoto\_supervisión\_ejecutar** función y, a continuación, compilar y ejecutar la aplicación de dispositivo de hello.</span><span class="sxs-lookup"><span data-stu-id="a7981-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="a7981-134">Reemplace hello **principal** función con hello de tooinvoke de código siguiente **remoto\_supervisión\_ejecutar** función:</span><span class="sxs-lookup"><span data-stu-id="a7981-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="a7981-135">Haga clic en **generar** y, a continuación, **generar solución** aplicación de dispositivo de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="a7981-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="a7981-136">En **el Explorador de soluciones**, contextual hello **RMDevice** proyecto de equipo y haga clic en **depurar**y, a continuación, haga clic en **Iniciar nueva instancia** toorun Hola ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a7981-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="a7981-137">consola de Hello muestra mensajes como hello aplicación envía ejemplo telemetría toohello preconfigurado solución, recibe los valores de propiedad establecidos en el panel de la solución de Hola y responde toomethods invocado desde el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7981-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
