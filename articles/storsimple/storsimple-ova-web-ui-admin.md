---
title: "web de Virtual Array aaaStorSimple administración de la interfaz de usuario | Documentos de Microsoft"
description: "Describe cómo las tareas de administración de dispositivos básicos tooperform a través de la interfaz de usuario de web de StorSimple Virtual Array Hola."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="5dd7d-103">Usar tooadminister de interfaz de usuario Web Hola la matriz Virtual de StorSimple</span><span class="sxs-lookup"><span data-stu-id="5dd7d-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![flujo del proceso de instalación](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="5dd7d-105">Información general</span><span class="sxs-lookup"><span data-stu-id="5dd7d-105">Overview</span></span>
<span data-ttu-id="5dd7d-106">tutoriales de Hello en este artículo aplican versión de disponibilidad general (GA) de marzo de 2016 ejecución de toohello Microsoft Azure StorSimple Virtual Array (también conocido como hello StorSimple en dispositivo virtual local).</span><span class="sxs-lookup"><span data-stu-id="5dd7d-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="5dd7d-107">En este artículo se describe algunos de los flujos de trabajo complejos de Hola y tareas de administración que se pueden realizar en hello StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="5dd7d-108">Puede administrar Hola StorSimple Virtual Array mediante UI (portal de hello tooas que se hace referencia UI) del servicio de administrador de StorSimple de Hola y Hola de interfaz de usuario web local para dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="5dd7d-109">En este artículo se centra en las tareas de Hola que puede realizar mediante la interfaz de usuario web de Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="5dd7d-110">Este artículo incluye Hola tutoriales:</span><span class="sxs-lookup"><span data-stu-id="5dd7d-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="5dd7d-111">Obtener la clave de cifrado de datos del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="5dd7d-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="5dd7d-112">Solucionar los problemas de instalación de la interfaz de usuario web</span><span class="sxs-lookup"><span data-stu-id="5dd7d-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="5dd7d-113">Crear un paquete de registro</span><span class="sxs-lookup"><span data-stu-id="5dd7d-113">Generate a log package</span></span>
* <span data-ttu-id="5dd7d-114">Apagar o reiniciar el dispositivo</span><span class="sxs-lookup"><span data-stu-id="5dd7d-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="5dd7d-115">Obtener la clave de cifrado de datos del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="5dd7d-115">Get hello service data encryption key</span></span>
<span data-ttu-id="5dd7d-116">Se genera una clave de cifrado de datos de servicio al registrar su primer dispositivo con hello el servicio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="5dd7d-117">Esta clave es, a continuación, se requiere con hello servicio Registro tooregister clave dispositivos adicionales con el servicio StorSimple Manager hello.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="5dd7d-118">Si el usuario ha perdido la clave de cifrado de datos de servicio y necesita tooretrieve, realizar Hola siguientes pasos de la interfaz de usuario del dispositivo de Hola de web local Hola registrados con el servicio.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="5dd7d-119">clave de cifrado de datos del servicio de tooget Hola</span><span class="sxs-lookup"><span data-stu-id="5dd7d-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="5dd7d-120">Conectar la interfaz de usuario de web local toohello.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-120">Connect toohello local web UI.</span></span> <span data-ttu-id="5dd7d-121">Vaya demasiado**configuración** > **configuración de nube**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="5dd7d-122">En la parte inferior de Hola de página de hello, haga clic en **clave de cifrado de datos de servicio Get**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="5dd7d-123">Aparecerá una clave.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-123">A key will appear.</span></span> <span data-ttu-id="5dd7d-124">Cópiela y guárdela.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-124">Copy and save this key.</span></span>
   
    ![obtener la clave de cifrado de los datos del servicio 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="5dd7d-126">Solucionar los problemas de instalación de la interfaz de usuario web</span><span class="sxs-lookup"><span data-stu-id="5dd7d-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="5dd7d-127">Al configurar el dispositivo de Hola a través de web local de hello interfaz de usuario, en algunos casos pueden surgir de errores.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="5dd7d-128">toodiagnose y solucionar estos errores, puede ejecutar pruebas de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="5dd7d-129">pruebas de diagnóstico de hello toorun</span><span class="sxs-lookup"><span data-stu-id="5dd7d-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="5dd7d-130">En la interfaz de usuario web local de hello, vaya demasiado**solución de problemas** > **pruebas de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![ejecutar diagnósticos 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="5dd7d-132">En la parte inferior de Hola de página de hello, haga clic en **ejecutar pruebas de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="5dd7d-133">Esto iniciará pruebas toodiagnose los posibles problemas con la red, dispositivos, proxy web, hora o configuración de la nube.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="5dd7d-134">Se le notificará que ese dispositivo Hola está ejecutando pruebas.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="5dd7d-135">Una vez completadas las pruebas de hello, resultados de Hola se mostrarán.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="5dd7d-136">Hello en el ejemplo siguiente se muestra los resultados de Hola de pruebas de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="5dd7d-137">Tenga en cuenta que no se configuraron la configuración del proxy web hello en este dispositivo y, por lo tanto, no se ejecutó la prueba de hello web proxy.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="5dd7d-138">Todos los Hola otras pruebas para la configuración de red, servidor DNS, y configuración de hora obtuvieron resultados satisfactorios.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![ejecutar diagnósticos 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="5dd7d-140">Crear un paquete de registro</span><span class="sxs-lookup"><span data-stu-id="5dd7d-140">Generate a log package</span></span>
<span data-ttu-id="5dd7d-141">Un paquete de registros está formado por todos los registros pertinentes Hola que pueden ayudar a Microsoft Support a solucionar los problemas del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="5dd7d-142">En esta versión, se puede generar un paquete de registros a través de la interfaz de usuario de web local Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="5dd7d-143">paquete de registros de hello toogenerate</span><span class="sxs-lookup"><span data-stu-id="5dd7d-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="5dd7d-144">En la interfaz de usuario web local de hello, vaya demasiado**solución de problemas** > **registros del sistema**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![crear un paquete de registro 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="5dd7d-146">En la parte inferior de Hola de página de hello, haga clic en **crear paquete de registro**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="5dd7d-147">Se creará un paquete de registros de sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="5dd7d-148">Este proceso tardará unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-148">This will take a couple of minutes.</span></span>
   
    ![crear un paquete de registro 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="5dd7d-150">Se le notificará una vez Hola paquete se creó correctamente y se actualizará la página de hello fecha cuando se creó el paquete de Hola y tooindicate Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![crear un paquete de registro 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="5dd7d-152">Haga clic en **Descargar paquete de registro**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-152">Click **Download log package**.</span></span> <span data-ttu-id="5dd7d-153">Se descargará un paquete comprimido en su sistema.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-153">A zipped package will be downloaded on your system.</span></span>
   
    ![crear un paquete de registro 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="5dd7d-155">Puede descomprimir paquete de registro descargado de Hola y ver archivos de registro del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="5dd7d-156">Apagar y reiniciar el dispositivo</span><span class="sxs-lookup"><span data-stu-id="5dd7d-156">Shut down and restart your device</span></span>
<span data-ttu-id="5dd7d-157">Puede apagar o reiniciar el dispositivo virtual mediante la interfaz de usuario de web local Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="5dd7d-158">Se recomienda, antes de reiniciar, desconecte los volúmenes de Hola o recursos compartidos sin conexión en el host de hello y, a continuación, Hola dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="5dd7d-159">Esto minimizará la posibilidad de daños en los datos.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="5dd7d-160">tooshut hacia abajo el dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="5dd7d-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="5dd7d-161">En la interfaz de usuario web local de hello, vaya demasiado**mantenimiento** > **la configuración de energía**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="5dd7d-162">En la parte inferior de Hola de página de hello, haga clic en **apagado**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![apagar el dispositivo 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="5dd7d-164">Aparecerá una advertencia que indica que un apagado de dispositivo de Hola interrumpirá la E/S que se encuentran en curso, lo que produce un tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="5dd7d-165">Haga clic en el icono de verificación de Hola</span><span class="sxs-lookup"><span data-stu-id="5dd7d-165">Click hello check icon</span></span> ![icono de marca de verificación](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="5dd7d-167">.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-167">.</span></span>
   
    ![advertencia de apagado del dispositivo](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="5dd7d-169">Se le notificará que el cierre Hola se ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![proceso de apagado del dispositivo iniciado](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="5dd7d-171">dispositivo de Hola se cerrará ahora.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-171">hello device will now shut down.</span></span> <span data-ttu-id="5dd7d-172">Si desea toostart el dispositivo, necesitará toodo que a través de administrador de Hyper-V de Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="5dd7d-173">toorestart el dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="5dd7d-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="5dd7d-174">En la interfaz de usuario web local de hello, vaya demasiado**mantenimiento** > **la configuración de energía**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="5dd7d-175">En la parte inferior de Hola de página de hello, haga clic en **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![proceso de reinicio del dispositivo](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="5dd7d-177">Aparecerá una advertencia que indica que ese dispositivo Hola reiniciar interrumpirá cualquier IOs que se encuentran en curso, lo que produce un tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="5dd7d-178">Haga clic en el icono de verificación de Hola</span><span class="sxs-lookup"><span data-stu-id="5dd7d-178">Click hello check icon</span></span> ![icono de marca de verificación](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="5dd7d-180">.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-180">.</span></span>
   
    ![advertencia de reinicio](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="5dd7d-182">Se le notificará que el reinicio Hola se ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![proceso de reinicio comenzado](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="5dd7d-184">Mientras Hola reinicio está en curso, perderá Hola conexión toohello interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="5dd7d-185">Puede supervisar Hola reinicio, actualice periódicamente Hola interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="5dd7d-186">Como alternativa, puede supervisar el estado de reinicio del dispositivo de Hola a través de administrador de Hyper-V de Hola.</span><span class="sxs-lookup"><span data-stu-id="5dd7d-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dd7d-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5dd7d-187">Next steps</span></span>
<span data-ttu-id="5dd7d-188">Obtenga información acerca de cómo demasiado[uso Hola toomanage de servicio de StorSimple Manager el dispositivo](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5dd7d-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

