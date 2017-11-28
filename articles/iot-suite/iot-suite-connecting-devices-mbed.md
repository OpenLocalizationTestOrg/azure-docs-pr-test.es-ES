---
title: Conectar un dispositivo con C en mbed | Microsoft Docs
description: "Se describe cómo conectar un dispositivo a la solución de supervisión remota preconfigurada del Conjunto de IoT de Azure mediante una aplicación creada en C que se ejecuta en un dispositivo de mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="ac5f0-103">Conectar el dispositivo a la solución preconfigurada de supervisión remota (mbed)</span><span class="sxs-lookup"><span data-stu-id="ac5f0-103">Connect your device to the remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="ac5f0-104">Información general de escenario</span><span class="sxs-lookup"><span data-stu-id="ac5f0-104">Scenario overview</span></span>
<span data-ttu-id="ac5f0-105">En este escenario, creará un dispositivo que envía la siguiente telemetría a la [solución preconfigurada][lnk-what-are-preconfig-solutions] de supervisión remota:</span><span class="sxs-lookup"><span data-stu-id="ac5f0-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="ac5f0-106">Temperatura exterior</span><span class="sxs-lookup"><span data-stu-id="ac5f0-106">External temperature</span></span>
* <span data-ttu-id="ac5f0-107">Temperatura interior</span><span class="sxs-lookup"><span data-stu-id="ac5f0-107">Internal temperature</span></span>
* <span data-ttu-id="ac5f0-108">Humedad</span><span class="sxs-lookup"><span data-stu-id="ac5f0-108">Humidity</span></span>

<span data-ttu-id="ac5f0-109">Para simplificar, el código del dispositivo genera valores de ejemplo, pero le recomendamos que amplíe el ejemplo conectando sensores reales a su dispositivo y enviando telemetría real.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="ac5f0-110">El dispositivo también puede responder a los métodos que se invocan desde el panel de la solución y los valores de propiedades deseadas establecidos en el panel de la solución.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="ac5f0-111">Para completar este tutorial, deberá tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="ac5f0-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ac5f0-113">Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="ac5f0-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ac5f0-114">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="ac5f0-114">Before you start</span></span>
<span data-ttu-id="ac5f0-115">Antes de escribir ningún código para el dispositivo, debe aprovisionar la solución preconfigurada de supervisión remota y aprovisionar un nuevo dispositivo personalizado en esa solución.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ac5f0-116">Aprovisionar su solución preconfigurada de supervisión remota</span><span class="sxs-lookup"><span data-stu-id="ac5f0-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="ac5f0-117">El dispositivo que cree en este tutorial enviará datos a una instancia de la solución preconfigurada de [supervisión remota][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="ac5f0-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="ac5f0-118">Si todavía no aprovisionó la solución preconfigurada de supervisión remota en su cuenta de Azure, use estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ac5f0-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="ac5f0-119">En la página <https://www.azureiotsuite.com/>, haga clic en **+** para crear una solución.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="ac5f0-120">Haga clic en **Seleccionar** en el panel de **supervisión remota** para crear la solución.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="ac5f0-121">En la página **Create Remote monitoring solution** (Crear solución de supervisión remota), escriba el **nombre de solución** que prefiera, seleccione la **región** en la que desea realizar la implementación y seleccione la suscripción de Azure que desea usar.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="ac5f0-122">Haga clic en **Crear solución**.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="ac5f0-123">Espere a que finalice el proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="ac5f0-124">Las soluciones preconfiguradas utilizan servicios de Azure facturables.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="ac5f0-125">Para evitar gastos innecesarios, asegúrese de quitar la solución preconfigurada de la suscripción cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="ac5f0-126">Para quitar completamente una solución preconfigurada de su suscripción, diríjase a la página <https://www.azureiotsuite.com/>.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="ac5f0-127">Cuando finalice el proceso de aprovisionamiento para la solución de supervisión remota, haga clic en **Iniciar** para abrir el panel de la solución en el explorador.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Panel de soluciones][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="ac5f0-129">Aprovisionar el dispositivo en la solución de supervisión remota</span><span class="sxs-lookup"><span data-stu-id="ac5f0-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="ac5f0-130">Si ya ha aprovisionado un dispositivo en la solución, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="ac5f0-131">Debe conocer las credenciales del dispositivo cuando cree la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="ac5f0-132">Para que un dispositivo se conecte a la solución preconfigurada, debe identificarse en el Centro de IoT con credenciales válidas.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="ac5f0-133">Puede recuperar las credenciales del dispositivo desde el panel de la solución.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="ac5f0-134">Incluirá las credenciales del dispositivo en la aplicación de cliente más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="ac5f0-135">Para agregar un dispositivo a su solución de supervisión remota, complete los pasos siguientes en el panel de la solución:</span><span class="sxs-lookup"><span data-stu-id="ac5f0-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="ac5f0-136">En la esquina inferior izquierda del panel, haga clic en **Agregar un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Agregar un dispositivo][1]
2. <span data-ttu-id="ac5f0-138">En el panel **Dispositivo personalizado**, haga clic en **Agregar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Agregar un dispositivo personalizado][2]
3. <span data-ttu-id="ac5f0-140">Elija **Permitirme definir mi propio id. de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="ac5f0-141">Especifique un id. de dispositivo, como **mydevice**, haga clic en **Comprobar id.** para comprobar que el nombre todavía no está en uso y, luego, haga clic en **Crear** para aprovisionar el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Agregar id. de dispositivo][3]
4. <span data-ttu-id="ac5f0-143">Anote las credenciales de dispositivo (id. de dispositivo, nombre de host de IoT Hub y clave de dispositivo).</span><span class="sxs-lookup"><span data-stu-id="ac5f0-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="ac5f0-144">La aplicación cliente necesita estos valores para conectarse con la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="ac5f0-145">A continuación, haga clic en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-145">Then click **Done**.</span></span>
   
    ![Ver las credenciales del dispositivo][4]
5. <span data-ttu-id="ac5f0-147">Seleccione el dispositivo en la lista de dispositivos del panel de la solución.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="ac5f0-148">Luego, en el panel **Detalles del dispositivo**, haga clic en **Habilitar dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="ac5f0-149">El estado del dispositivo ahora es **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="ac5f0-150">La solución de supervisión remota ahora puede recibir telemetría desde el dispositivo e invocar métodos en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a><span data-ttu-id="ac5f0-151">Compilación y ejecución de la solución de ejemplo de C</span><span class="sxs-lookup"><span data-stu-id="ac5f0-151">Build and run the C sample solution</span></span>

<span data-ttu-id="ac5f0-152">Las instrucciones siguientes describen los pasos para conectar un dispositivo [Freescale FRDM-K64F habilitado para mbed][lnk-mbed-home] a la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-152">The following instructions describe the steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device to the remote monitoring solution.</span></span>

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a><span data-ttu-id="ac5f0-153">Conexión del dispositivo mbed a la máquina de escritorio y a la red</span><span class="sxs-lookup"><span data-stu-id="ac5f0-153">Connect the mbed device to your network and desktop machine</span></span>

1. <span data-ttu-id="ac5f0-154">Conecte el dispositivo mbed a la red mediante un cable Ethernet.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-154">Connect the mbed device to your network using an Ethernet cable.</span></span> <span data-ttu-id="ac5f0-155">Este paso es necesario porque la aplicación de ejemplo requiere acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-155">This step is necessary because the sample application requires internet access.</span></span>

1. <span data-ttu-id="ac5f0-156">Vea [Introducción a mbed][lnk-mbed-getstarted] para conectar el dispositivo de mbed al equipo de escritorio.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-156">See [Getting Started with mbed][lnk-mbed-getstarted] to connect your mbed device to your desktop PC.</span></span>

1. <span data-ttu-id="ac5f0-157">Si el equipo de escritorio está ejecutando Windows, vea [Configuración del equipo][lnk-mbed-pcconnect] para configurar el acceso al puerto serie para el dispositivo mbed.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] to configure serial port access to your mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-the-sample-code"></a><span data-ttu-id="ac5f0-158">Crear un proyecto de mbed e importar el código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ac5f0-158">Create an mbed project and import the sample code</span></span>

<span data-ttu-id="ac5f0-159">Siga estos pasos para agregar algún código de ejemplo a un proyecto de mbed.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-159">Follow these steps to add some sample code to an mbed project.</span></span> <span data-ttu-id="ac5f0-160">Importará el proyecto de inicio de supervisión remota y luego cambiará el proyecto para usar el protocolo MQTT en lugar del protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-160">You import the remote monitoring starter project and then change the project to use the MQTT protocol instead of the AMQP protocol.</span></span> <span data-ttu-id="ac5f0-161">Actualmente, debe emplear el protocolo MQTT para usar las características de administración de dispositivos de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-161">Currently, you need to use the MQTT protocol to use the device management features of IoT Hub.</span></span>

1. <span data-ttu-id="ac5f0-162">En el explorador web, vaya al [sitio para desarrolladores](https://developer.mbed.org/)mbed.org.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-162">In your web browser, go to the mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="ac5f0-163">Si aún no se ha registrado, verá una opción para crear una cuenta (es gratuita).</span><span class="sxs-lookup"><span data-stu-id="ac5f0-163">If you haven't signed up, you see an option to create an account (it's free).</span></span> <span data-ttu-id="ac5f0-164">De lo contrario, inicie sesión con las credenciales de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="ac5f0-165">Luego haga clic en **Compilador** en la esquina superior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-165">Then click **Compiler** in the upper right-hand corner of the page.</span></span> <span data-ttu-id="ac5f0-166">Al realizar esta acción, se mostrará la interfaz *Área de trabajo*.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-166">This action brings you to the *Workspace* interface.</span></span>

1. <span data-ttu-id="ac5f0-167">Asegúrese de que la plataforma de hardware que está usando aparezca en la esquina superior derecha de la ventana, o bien haga clic en el icono de la esquina derecha para seleccionar la plataforma de hardware.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-167">Make sure the hardware platform you're using appears in the upper right-hand corner of the window, or click the icon in the right-hand corner to select your hardware platform.</span></span>

1. <span data-ttu-id="ac5f0-168">Haga clic en **Importar** en el menú principal.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-168">Click **Import** on the main menu.</span></span> <span data-ttu-id="ac5f0-169">A continuación, haga clic en **Click here to import from URL** (Haga clic aquí para importar desde la dirección URL).</span><span class="sxs-lookup"><span data-stu-id="ac5f0-169">Then click **Click here to import from URL**.</span></span>
   
    ![Inicio de la importación al área de trabajo de mbed][6]

1. <span data-ttu-id="ac5f0-171">En la ventana emergente, escriba el vínculo al código de ejemplo https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ y, después, haga clic en **Importar**.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-171">In the pop-up window, enter the link for the sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importación del código de ejemplo al área de trabajo de mbed][7]

1. <span data-ttu-id="ac5f0-173">Puede ver en la ventana del compilador de mbed que se importaron varias bibliotecas durante la importación de este proyecto.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-173">You can see in the mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="ac5f0-174">El equipo de IoT de Azure ofrece y mantiene algunas bibliotecas ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), mientras que otras son bibliotecas de terceros que están disponibles en el catálogo de bibliotecas de mbed.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-174">Some are provided and maintained by the Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in the mbed libraries catalog.</span></span>
   
    ![Visualización del proyecto de mbed][8]

1. <span data-ttu-id="ac5f0-176">En el **área de trabajo de programa**, haga clic con el botón derecho en la biblioteca **iothub\_amqp\_transport**, haga clic en **Delete** (Eliminar) y luego en **OK** (Aceptar) para confirmar.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-176">In the **Program Workspace**, right-click the **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="ac5f0-177">En el **área de trabajo de programa**, haga clic con el botón derecho en la biblioteca **azure\_amqp\_c**, haga clic en **Delete** (Eliminar) y luego en **OK** (Aceptar) para confirmar.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-177">In the **Program Workspace**, right-click the **azure\_amqp\_c** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="ac5f0-178">Haga clic con el botón derecho en el proyecto **remote_monitoring** en el **área de trabajo de programa**, seleccione **Import Library** (Importar biblioteca) y luego seleccione **From URL** (Desde dirección URL).</span><span class="sxs-lookup"><span data-stu-id="ac5f0-178">Right-click the **remote_monitoring** project in the **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Inicio de la importación de la biblioteca al área de trabajo de mbed][6]

1. <span data-ttu-id="ac5f0-180">En la ventana emergente, especifique el vínculo de la biblioteca de transporte de MQTT https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ y luego haga clic en **Import** (Importar).</span><span class="sxs-lookup"><span data-stu-id="ac5f0-180">In the pop-up window, enter the link for the MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importación de la biblioteca al área de trabajo de mbed][12]

1. <span data-ttu-id="ac5f0-182">Repita el paso anterior para agregar la biblioteca MQTT desde https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-182">Repeat the previous step to add the MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="ac5f0-183">El área de trabajo se parece ahora a esta:</span><span class="sxs-lookup"><span data-stu-id="ac5f0-183">Your workspace now looks like the following:</span></span>

    ![Visualización de área de trabajo de mbed][13]

1. <span data-ttu-id="ac5f0-185">Abra el archivo remote\_monitoring\remote_monitoring.c y sustituya las instrucciones `#include` existentes por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac5f0-185">Open the remote\_monitoring\remote_monitoring.c file and replace the existing `#include` statements with the following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="ac5f0-186">Elimine el resto de código del archivo remote\_monitoring\remote\_monitoring.c.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-186">Delete all the remaining code in the remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="ac5f0-187">Compilación y ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="ac5f0-187">Build and run the sample</span></span>

<span data-ttu-id="ac5f0-188">Agregue código para invocar la función **remote\_monitoring\_run** y luego compile y ejecute la aplicación del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-188">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="ac5f0-189">Agregue una función **main** con el código siguiente al final del archivo remote\_monitoring.c para invocar la función **remote\_monitoring\_run**:</span><span class="sxs-lookup"><span data-stu-id="ac5f0-189">Add a **main** function with following code at the end of the remote\_monitoring.c file to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="ac5f0-190">Haga clic en **Compilar** para compilar el programa.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-190">Click **Compile** to build the program.</span></span> <span data-ttu-id="ac5f0-191">Puede omitir con seguridad las advertencias, pero si la compilación genera errores, corríjalos antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-191">You can safely ignore any warnings, but if the build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="ac5f0-192">Si la compilación es correcta, el sitio web del compilador de mbed genera un archivo .bin con el nombre del proyecto y lo descarga en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-192">If the build is successful, the mbed compiler website generates a .bin file with the name of your project and downloads it to your local machine.</span></span> <span data-ttu-id="ac5f0-193">Copie el archivo .bin en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-193">Copy the .bin file to the device.</span></span> <span data-ttu-id="ac5f0-194">Si guarda el archivo .bin en el dispositivo, este último se reiniciará y ejecutará el programa incluido en el archivo .bin.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-194">Saving the .bin file to the device causes the device to restart and run the program contained in the .bin file.</span></span> <span data-ttu-id="ac5f0-195">Puede reiniciar manualmente el programa en cualquier momento presionando el botón Restablecer en el dispositivo mbed.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-195">You can manually restart the program at any time by pressing the reset button on the mbed device.</span></span>

1. <span data-ttu-id="ac5f0-196">Conecte con el dispositivo mediante una aplicación cliente de SSH, como PuTTY.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-196">Connect to the device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="ac5f0-197">Puede determinar el puerto serie que usa el dispositivo comprobando el Administrador de dispositivos de Windows.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-197">You can determine the serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="ac5f0-198">En PuTTY, haga clic en el tipo de conexión **serie** .</span><span class="sxs-lookup"><span data-stu-id="ac5f0-198">In PuTTY, click the **Serial** connection type.</span></span> <span data-ttu-id="ac5f0-199">Como el dispositivo normalmente se conecta a 9600 baudios, especifique 9600 en el cuadro **Velocidad** .</span><span class="sxs-lookup"><span data-stu-id="ac5f0-199">The device typically connects at 9600 baud, so enter 9600 in the **Speed** box.</span></span> <span data-ttu-id="ac5f0-200">A continuación, haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-200">Then click **Open**.</span></span>

1. <span data-ttu-id="ac5f0-201">El programa comienza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-201">The program starts executing.</span></span> <span data-ttu-id="ac5f0-202">Si el programa no se inicia automáticamente al conectarse, puede que tenga que restablecer la placa (presione CTRL+Pausa o pulse el botón de reinicio de la placa).</span><span class="sxs-lookup"><span data-stu-id="ac5f0-202">You may have to reset the board (press CTRL+Break or press the board's reset button) if the program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
