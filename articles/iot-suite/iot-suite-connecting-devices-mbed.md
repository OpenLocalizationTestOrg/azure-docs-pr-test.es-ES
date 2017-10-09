---
title: aaaConnect un dispositivo mediante C en mbed | Documentos de Microsoft
description: "Describe cómo tooconnect una toohello dispositivo Azure IoT conjunto preconfigurado solución de supervisión remota con una aplicación escrita en C utilizando un dispositivo de mbed."
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
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="1a2e5-103">Conectar su toohello de dispositivo remoto de supervisión de solución preconfigurada (mbed)</span><span class="sxs-lookup"><span data-stu-id="1a2e5-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="1a2e5-104">Información general de escenario</span><span class="sxs-lookup"><span data-stu-id="1a2e5-104">Scenario overview</span></span>
<span data-ttu-id="1a2e5-105">En este escenario, se crea un dispositivo que envía Hola después de supervisión remota de telemetría toohello [preconfigurado solución][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="1a2e5-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="1a2e5-106">Temperatura exterior</span><span class="sxs-lookup"><span data-stu-id="1a2e5-106">External temperature</span></span>
* <span data-ttu-id="1a2e5-107">Temperatura interior</span><span class="sxs-lookup"><span data-stu-id="1a2e5-107">Internal temperature</span></span>
* <span data-ttu-id="1a2e5-108">Humedad</span><span class="sxs-lookup"><span data-stu-id="1a2e5-108">Humidity</span></span>

<span data-ttu-id="1a2e5-109">Para simplificar, valores de ejemplo genera el código de hello en dispositivo hello, pero recomendamos ejemplo Hola tooextend: conectar dispositivo tooyour de sensores real y enviar telemetría real.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="1a2e5-110">dispositivo de Hello también es toomethods toorespond puede invocar desde el panel de la solución de Hola y desea valores de propiedad establecidos en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="1a2e5-111">toocomplete este tutorial, necesita una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="1a2e5-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1a2e5-113">Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="1a2e5-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1a2e5-114">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="1a2e5-114">Before you start</span></span>
<span data-ttu-id="1a2e5-115">Antes de escribir ningún código para el dispositivo, debe aprovisionar la solución preconfigurada de supervisión remota y aprovisionar un nuevo dispositivo personalizado en esa solución.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="1a2e5-116">Aprovisionar su solución preconfigurada de supervisión remota</span><span class="sxs-lookup"><span data-stu-id="1a2e5-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="1a2e5-117">dispositivo de Hola que creará en este tutorial envía la instancia de datos de tooan de hello [supervisión remota] [ lnk-remote-monitoring] preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="1a2e5-118">Si aún no aprovisionada Hola supervisión solución preconfigurada en su cuenta de Azure remota, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1a2e5-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="1a2e5-119">En hello <https://www.azureiotsuite.com/> página, haga clic en  **+**  toocreate una solución.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="1a2e5-120">Haga clic en **seleccione** en hello **supervisión remota** panel toocreate la solución.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="1a2e5-121">En hello **crear remoto solución de supervisión** página, escriba un **nombre de la solución** de su elección, seleccione hello **región** desee toodeploy a y seleccione hello Azure suscripción toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="1a2e5-122">Haga clic en **Crear solución**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="1a2e5-123">Espere hasta que se complete el proceso de aprovisionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="1a2e5-124">las soluciones de Hello preconfigurado usan los servicios de Azure facturables.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="1a2e5-125">Asegúrese de tooremove Hola solución preconfigurada de la suscripción cuando haya terminado con él tooavoid los cargos innecesarios.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="1a2e5-126">Puede quitar completamente una solución preconfigurada de su suscripción visitando hello <https://www.azureiotsuite.com/> página.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="1a2e5-127">Cuando finalice el proceso para hello remoto de solución de supervisión de aprovisionamiento de hello, haga clic en **iniciar** tooopen panel de solución de hello en el explorador.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Panel de soluciones][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="1a2e5-129">Aprovisionar el dispositivo en hello remoto de solución de supervisión</span><span class="sxs-lookup"><span data-stu-id="1a2e5-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="1a2e5-130">Si ya ha aprovisionado un dispositivo en la solución, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="1a2e5-131">Necesita credenciales de dispositivo de hello tooknow cuando se crea la aplicación de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="1a2e5-132">Para una solución de toohello preconfigurado tooconnect de dispositivo, debe identificarse tooIoT concentrador con credenciales válidas.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="1a2e5-133">Puede recuperar las credenciales del dispositivo Hola de panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="1a2e5-134">Incluye las credenciales del dispositivo hello en la aplicación de cliente más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="1a2e5-135">tooadd una solución de supervisión remota de tooyour de dispositivo, Hola completa siguiendo los pasos en el panel de la solución de hello:</span><span class="sxs-lookup"><span data-stu-id="1a2e5-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="1a2e5-136">En hello esquina izquierda inferior del panel de hello, haga clic en **agregar un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Agregar un dispositivo][1]
2. <span data-ttu-id="1a2e5-138">Hola **dispositivo personalizado** del panel, haga clic en **agregar nueva**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Agregar un dispositivo personalizado][2]
3. <span data-ttu-id="1a2e5-140">Elija **Permitirme definir mi propio id. de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="1a2e5-141">Escriba un Id. de dispositivo como **mydevice**, haga clic en **Check ID** tooverify ese nombre no está en uso y, a continuación, haga clic en **crear** dispositivo de tooprovision Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Agregar id. de dispositivo][3]
4. <span data-ttu-id="1a2e5-143">Hacer que un dispositivo de hello tenga en cuenta las credenciales (Id. de dispositivo, el nombre de host de IoT Hub y clave de dispositivo).</span><span class="sxs-lookup"><span data-stu-id="1a2e5-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="1a2e5-144">La aplicación cliente necesita estos toohello de tooconnect valores remoto de solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="1a2e5-145">A continuación, haga clic en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-145">Then click **Done**.</span></span>
   
    ![Ver las credenciales del dispositivo][4]
5. <span data-ttu-id="1a2e5-147">Seleccione el dispositivo en la lista de dispositivos de hello en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="1a2e5-148">A continuación, en hello **detalles del dispositivo** del panel, haga clic en **Habilitar dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="1a2e5-149">Hola estado del dispositivo es ahora **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="1a2e5-150">solución de supervisión remoto Hello ahora puede reciba datos de telemetría del dispositivo e invocar métodos de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="1a2e5-151">Compilar y ejecutar la solución de ejemplo de Hola C</span><span class="sxs-lookup"><span data-stu-id="1a2e5-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="1a2e5-152">Hello las instrucciones siguientes describen los pasos de Hola para conectar un [habilitado mbed Freescale FRDM-K64F] [ lnk-mbed-home] toohello de dispositivo remoto de solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="1a2e5-153">Conectar el dispositivo de la red de tooyour hello mbed y máquina de escritorio</span><span class="sxs-lookup"><span data-stu-id="1a2e5-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="1a2e5-154">Conectar red del dispositivo tooyour de hello mbed mediante un cable Ethernet.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="1a2e5-155">Este paso es necesario porque la aplicación de ejemplo de Hola requiere acceso a internet.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="1a2e5-156">Vea [Getting Started with mbed] [ lnk-mbed-getstarted] tooconnect mbed dispositivo tooyour escritorio PC.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="1a2e5-157">Si su PC de escritorio se ejecuta Windows, vea [configuración de PC] [ lnk-mbed-pcconnect] tooyour mbed dispositivo de tooconfigure puerto serie acceso.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="1a2e5-158">Crear un proyecto mbed e importar el código de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="1a2e5-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="1a2e5-159">Siga estos pasos tooadd algún proyecto de mbed de tooan de código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="1a2e5-160">Importar el proyecto de inicio de supervisión remota de Hola y cambie hello toouse de proyecto Hola protocolo MQTT en lugar de hello protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="1a2e5-161">Actualmente, debe toouse hello MQTT protocolo toouse Hola dispositivo características de administración de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="1a2e5-162">En el explorador web, vaya toohello mbed.org [sitio para desarrolladores de](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="1a2e5-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="1a2e5-163">Si no se haya registrado, verá un toocreate opción una cuenta (no disponible).</span><span class="sxs-lookup"><span data-stu-id="1a2e5-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="1a2e5-164">De lo contrario, inicie sesión con las credenciales de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="1a2e5-165">A continuación, haga clic en **compilador** en hello superior derecha de la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="1a2e5-166">Esta acción pone toohello *área de trabajo* interfaz.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="1a2e5-167">Asegúrese de que la plataforma de hardware de hello usa aparece en hello la esquina superior derecha de la ventana hello, o haga clic en icono de hello en hello esquina derecha tooselect su plataforma de hardware.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="1a2e5-168">Haga clic en **importación** en el menú principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="1a2e5-169">A continuación, haga clic en **haga clic aquí tooimport de dirección URL**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![Iniciar el área de trabajo de importación toombed][6]

1. <span data-ttu-id="1a2e5-171">En la ventana emergente de hello, especifique el vínculo de Hola Hola ejemplo código https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, a continuación, haga clic en **importación**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importar el área de trabajo de toombed de código de ejemplo][7]

1. <span data-ttu-id="1a2e5-173">Puede ver en la ventana de compilador de hello mbed que importar este proyecto, también importa varias bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="1a2e5-174">Algunas son proporcionados y mantenidos por el equipo de Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), mientras que otros están disponibles en el catálogo de hello mbed bibliotecas de bibliotecas de otros fabricantes.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![Visualización del proyecto de mbed][8]

1. <span data-ttu-id="1a2e5-176">Hola **área de trabajo de programa**, contextual hello **el centro de IOT\_amqp\_transporte** biblioteca, haga clic en **eliminar**y, a continuación, haga clic en **Aceptar** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="1a2e5-177">Hola **área de trabajo de programa**, contextual hello **azure\_amqp\_c** biblioteca, haga clic en **eliminar**y, a continuación, haga clic en **Aceptar**  tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="1a2e5-178">Menú contextual hello **remote_monitoring** proyecto Hola **área de trabajo de programa**, seleccione **biblioteca de importación**, a continuación, seleccione **From URL**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Iniciar el área de trabajo de biblioteca importación toombed][6]

1. <span data-ttu-id="1a2e5-180">En la ventana emergente de hello, especifique el vínculo de Hola Hola MQTT transporte biblioteca https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_de transporte y, a continuación, haga clic en **importación**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importar el área de trabajo de biblioteca toombed][12]

1. <span data-ttu-id="1a2e5-182">Hola repetición anterior paso tooadd hello MQTT biblioteca de https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="1a2e5-183">El área de trabajo ahora Hola siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="1a2e5-183">Your workspace now looks like hello following:</span></span>

    ![Visualización de área de trabajo de mbed][13]

1. <span data-ttu-id="1a2e5-185">Abra Hola remoto\_monitoring\remote_monitoring.c archivo y reemplazar Hola existente `#include` instrucciones con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="1a2e5-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

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
1. <span data-ttu-id="1a2e5-186">Eliminar Hola todas las restantes código de hello remoto\_monitoring\remote\_monitoring.c archivo.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="1a2e5-187">Compilar y ejecutar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="1a2e5-187">Build and run hello sample</span></span>

<span data-ttu-id="1a2e5-188">Agregar Hola de código tooinvoke **remoto\_supervisión\_ejecutar** función y, a continuación, compilar y ejecutar la aplicación de dispositivo de hello.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="1a2e5-189">Agregar un **principal** función con el código siguiente al final de Hola de hello remoto\_Hola de monitoring.c archivo tooinvoke **remoto\_supervisión\_ejecutar** función:</span><span class="sxs-lookup"><span data-stu-id="1a2e5-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="1a2e5-190">Haga clic en **compilar** programa Hola de toobuild.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="1a2e5-191">Sin ningún riesgo puede pasar por alto las advertencias, pero si la compilación de hello genera errores, corríjalos antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="1a2e5-192">Si Hola compilación es correcta, sitio Web de hello mbed compilador genera un archivo .bin con nombre hello del proyecto y lo descarga en la máquina local tooyour.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="1a2e5-193">Dispositivo de copia Hola .bin archivo toohello.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="1a2e5-194">Guardar Hola .bin archivo toohello dispositivo hace Hola dispositivo toorestart y ejecuta programa Hola contenido en el archivo .bin Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="1a2e5-195">Programa hello, puede reiniciar manualmente en cualquier momento presionando el botón de restablecimiento de hello en dispositivo de mbed Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="1a2e5-196">Conecte el dispositivo toohello con una aplicación de cliente SSH como PuTTY.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="1a2e5-197">Puede determinar el puerto serie hello que usa el dispositivo mediante la comprobación de administrador de dispositivos de Windows.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="1a2e5-198">En PuTTY, haga clic en hello **serie** tipo de conexión.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="1a2e5-199">dispositivo de Hello normalmente se conecta a 9600 baudios, por lo que escriba 9600 en hello **velocidad** cuadro.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="1a2e5-200">A continuación, haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-200">Then click **Open**.</span></span>

1. <span data-ttu-id="1a2e5-201">programa Hello empieza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-201">hello program starts executing.</span></span> <span data-ttu-id="1a2e5-202">Puede tener placa de hello tooreset (presione CTRL+pausa o botón de restablecimiento del panel presione hello) si programa hello no se inicia automáticamente cuando se conecta.</span><span class="sxs-lookup"><span data-stu-id="1a2e5-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
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
