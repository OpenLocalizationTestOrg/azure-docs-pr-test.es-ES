---
title: "Administración de la interfaz de usuario web de la matriz virtual de StorSimple | Microsoft Docs"
description: "Describe cómo realizar tareas de administración básicas en los dispositivos mediante la interfaz de usuario web de la matriz virtual de StorSimple."
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
ms.openlocfilehash: 989e7b697f9b527df549fb32be18edd1d3c8d224
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-web-ui-to-administer-your-storsimple-virtual-array"></a><span data-ttu-id="7610e-103">Usar la interfaz de usuario web para administrar la matriz virtual de StorSimple</span><span class="sxs-lookup"><span data-stu-id="7610e-103">Use the Web UI to administer your StorSimple Virtual Array</span></span>
![flujo del proceso de instalación](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="7610e-105">Información general</span><span class="sxs-lookup"><span data-stu-id="7610e-105">Overview</span></span>
<span data-ttu-id="7610e-106">Los tutoriales de este artículo se aplican a la matriz virtual de Microsoft Azure StorSimple (también conocida como dispositivo virtual local de StorSimple) que se ejecuta en la versión de disponibilidad general de marzo de 2016.</span><span class="sxs-lookup"><span data-stu-id="7610e-106">The tutorials in this article apply to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="7610e-107">En este artículo se describen algunos de los flujos de trabajo complejos y tareas de administración que se pueden realizar en la matriz virtual de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7610e-107">This article describes some of the complex workflows and management tasks that can be performed on the StorSimple Virtual Array.</span></span> <span data-ttu-id="7610e-108">Puede administrar la matriz virtual de StorSimple mediante la interfaz de usuario del servicio StorSimple Manager (denominada portal de interfaz de usuario) y la interfaz de usuario web local del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7610e-108">You can manage the StorSimple Virtual Array using the StorSimple Manager service UI (referred to as the portal UI) and the local web UI for the device.</span></span> <span data-ttu-id="7610e-109">En este artículo nos centraremos en las tareas que puede realizar mediante la interfaz de usuario web.</span><span class="sxs-lookup"><span data-stu-id="7610e-109">This article focuses on the tasks that you can perform using the web UI.</span></span>

<span data-ttu-id="7610e-110">Este artículo incluye los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="7610e-110">This article includes the following tutorials:</span></span>

* <span data-ttu-id="7610e-111">Obtener la clave de cifrado de los datos del servicio</span><span class="sxs-lookup"><span data-stu-id="7610e-111">Get the service data encryption key</span></span>
* <span data-ttu-id="7610e-112">Solucionar los problemas de instalación de la interfaz de usuario web</span><span class="sxs-lookup"><span data-stu-id="7610e-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="7610e-113">Crear un paquete de registro</span><span class="sxs-lookup"><span data-stu-id="7610e-113">Generate a log package</span></span>
* <span data-ttu-id="7610e-114">Apagar o reiniciar el dispositivo</span><span class="sxs-lookup"><span data-stu-id="7610e-114">Shut down or restart your device</span></span>

## <a name="get-the-service-data-encryption-key"></a><span data-ttu-id="7610e-115">Obtener la clave de cifrado de los datos del servicio</span><span class="sxs-lookup"><span data-stu-id="7610e-115">Get the service data encryption key</span></span>
<span data-ttu-id="7610e-116">Una clave de cifrado de los datos del servicio se genera cuando se registra el primer dispositivo mediante el servicio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="7610e-116">A service data encryption key is generated when you register your first device with the StorSimple Manager service.</span></span> <span data-ttu-id="7610e-117">Esta clave y la clave de registro del servicio son necesarias para registrar dispositivos adicionales en el servicio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="7610e-117">This key is then required with the service registration key to register additional devices with the StorSimple Manager service.</span></span>

<span data-ttu-id="7610e-118">Si ha perdido su clave de cifrado de los datos del servicio y necesita recuperarla, siga los siguientes pasos en la interfaz de usuario web local del dispositivo que haya registrado con el servicio.</span><span class="sxs-lookup"><span data-stu-id="7610e-118">If you have misplaced your service data encryption key and need to retrieve it, perform the following steps in the local web UI of the device registered with your service.</span></span>

#### <a name="to-get-the-service-data-encryption-key"></a><span data-ttu-id="7610e-119">Cómo obtener la clave de cifrado de los datos del servicio</span><span class="sxs-lookup"><span data-stu-id="7610e-119">To get the service data encryption key</span></span>
1. <span data-ttu-id="7610e-120">Conéctese a la interfaz de usuario web local</span><span class="sxs-lookup"><span data-stu-id="7610e-120">Connect to the local web UI.</span></span> <span data-ttu-id="7610e-121">Vaya a **Configuración** > **Configuración de la nube**.</span><span class="sxs-lookup"><span data-stu-id="7610e-121">Go to **Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="7610e-122">En la parte inferior de la página, haga clic en **Obtener clave de cifrado de datos del servicio**.</span><span class="sxs-lookup"><span data-stu-id="7610e-122">At the bottom of the page, click **Get service data encryption key**.</span></span> <span data-ttu-id="7610e-123">Aparecerá una clave.</span><span class="sxs-lookup"><span data-stu-id="7610e-123">A key will appear.</span></span> <span data-ttu-id="7610e-124">Cópiela y guárdela.</span><span class="sxs-lookup"><span data-stu-id="7610e-124">Copy and save this key.</span></span>
   
    ![obtener la clave de cifrado de los datos del servicio 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="7610e-126">Solucionar los problemas de instalación de la interfaz de usuario web</span><span class="sxs-lookup"><span data-stu-id="7610e-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="7610e-127">Es posible que vea algún error cuando configure el dispositivo a través de la interfaz de usuario web local.</span><span class="sxs-lookup"><span data-stu-id="7610e-127">In some instances when you configure the device through the local web UI, you might run into errors.</span></span> <span data-ttu-id="7610e-128">Para diagnosticar y solucionar estos errores, puede ejecutar las pruebas de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7610e-128">To diagnose and troubleshoot such errors, you can run the diagnostics tests.</span></span>

#### <a name="to-run-the-diagnostic-tests"></a><span data-ttu-id="7610e-129">Ejecutar las pruebas de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="7610e-129">To run the diagnostic tests</span></span>
1. <span data-ttu-id="7610e-130">En la interfaz de usuario web local, vaya a **Solución de problemas** > **Pruebas de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="7610e-130">In the local web UI, go to **Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![ejecutar diagnósticos 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="7610e-132">En la parte inferior de la página, haga clic en **Ejecutar pruebas de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="7610e-132">At the bottom of the page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="7610e-133">Con esto, iniciará las pruebas para diagnosticar los posibles problemas con la red, el dispositivo, el proxy web, la hora o la configuración de la nube.</span><span class="sxs-lookup"><span data-stu-id="7610e-133">This will initiate tests to diagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="7610e-134">Verá una notificación que le indica que el dispositivo está ejecutando algunas pruebas.</span><span class="sxs-lookup"><span data-stu-id="7610e-134">You will be notified that the device is running tests.</span></span>
3. <span data-ttu-id="7610e-135">Cuando hayan terminado estas pruebas, podrá ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="7610e-135">After the tests have completed, the results will be displayed.</span></span> <span data-ttu-id="7610e-136">En el siguiente ejemplo se muestra el resultado de las pruebas de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7610e-136">The following example shows the results of diagnostic tests.</span></span> <span data-ttu-id="7610e-137">Tenga en cuenta que la configuración del proxy web no se ha realizado en este dispositivo y que, por lo tanto, no se ejecutó la prueba del proxy web.</span><span class="sxs-lookup"><span data-stu-id="7610e-137">Note that the web proxy settings were not configured on this device, and therefore, the web proxy test was not run.</span></span> <span data-ttu-id="7610e-138">El resto de las pruebas de la configuración de red, el servidor DNS y la hora se realizaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="7610e-138">All the other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![ejecutar diagnósticos 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="7610e-140">Crear un paquete de registro</span><span class="sxs-lookup"><span data-stu-id="7610e-140">Generate a log package</span></span>
<span data-ttu-id="7610e-141">Un paquete de registro contiene todos los registros relevantes que pueden ayudar al equipo de soporte técnico de Microsoft a solucionar los problemas del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7610e-141">A log package is comprised of all the relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="7610e-142">En esta versión, se puede generar un paquete de registro a través de la interfaz de usuario web local.</span><span class="sxs-lookup"><span data-stu-id="7610e-142">In this release, a log package can be generated via the local web UI.</span></span>

#### <a name="to-generate-the-log-package"></a><span data-ttu-id="7610e-143">Generar el paquete de registro</span><span class="sxs-lookup"><span data-stu-id="7610e-143">To generate the log package</span></span>
1. <span data-ttu-id="7610e-144">En la interfaz de usuario web local, vaya a **Solución de problemas** > **Registros del sistema**.</span><span class="sxs-lookup"><span data-stu-id="7610e-144">In the local web UI, go to **Troubleshooting** > **System logs**.</span></span>
   
    ![crear un paquete de registro 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="7610e-146">En la parte inferior de la página, haga clic en **Crear paquete de registro**.</span><span class="sxs-lookup"><span data-stu-id="7610e-146">At the bottom of the page, click **Create log package**.</span></span> <span data-ttu-id="7610e-147">Se creará un paquete de los registros del sistema.</span><span class="sxs-lookup"><span data-stu-id="7610e-147">A package of the system logs will be created.</span></span> <span data-ttu-id="7610e-148">Este proceso tardará unos minutos.</span><span class="sxs-lookup"><span data-stu-id="7610e-148">This will take a couple of minutes.</span></span>
   
    ![crear un paquete de registro 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="7610e-150">Verá una notificación una vez el paquete se cree correctamente y la página se actualizará para indicar la hora y la fecha durante las cuales se creó el mismo.</span><span class="sxs-lookup"><span data-stu-id="7610e-150">You will be notified after the package is successfully created, and the page will be updated to indicate the time and date when the package was created.</span></span>
   
    ![crear un paquete de registro 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="7610e-152">Haga clic en **Descargar paquete de registro**.</span><span class="sxs-lookup"><span data-stu-id="7610e-152">Click **Download log package**.</span></span> <span data-ttu-id="7610e-153">Se descargará un paquete comprimido en su sistema.</span><span class="sxs-lookup"><span data-stu-id="7610e-153">A zipped package will be downloaded on your system.</span></span>
   
    ![crear un paquete de registro 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="7610e-155">Puede descomprimir el paquete de registro que haya descargado y ver los archivos de registro del sistema.</span><span class="sxs-lookup"><span data-stu-id="7610e-155">You can unzip the downloaded log package and view the system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="7610e-156">Apagar y reiniciar el dispositivo</span><span class="sxs-lookup"><span data-stu-id="7610e-156">Shut down and restart your device</span></span>
<span data-ttu-id="7610e-157">Puede apagar o reiniciar el dispositivo virtual mediante la interfaz de usuario web local.</span><span class="sxs-lookup"><span data-stu-id="7610e-157">You can shut down or restart your virtual device using the local web UI.</span></span> <span data-ttu-id="7610e-158">Se recomienda que antes de reiniciar, desconecte los volúmenes o recursos compartidos en el host y, luego, el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7610e-158">We recommend that before you restart, take the volumes or shares offline on the host and then the device.</span></span> <span data-ttu-id="7610e-159">Esto minimizará la posibilidad de daños en los datos.</span><span class="sxs-lookup"><span data-stu-id="7610e-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="to-shut-down-your-virtual-device"></a><span data-ttu-id="7610e-160">Apagar el dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="7610e-160">To shut down your virtual device</span></span>
1. <span data-ttu-id="7610e-161">En la interfaz de usuario web local, vaya a **Mantenimiento** > **Configuración de energía**.</span><span class="sxs-lookup"><span data-stu-id="7610e-161">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="7610e-162">En la parte inferior de la página, haga clic en **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="7610e-162">At the bottom of the page, click **Shutdown**.</span></span>
   
    ![apagar el dispositivo 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="7610e-164">Aparecerá una advertencia que le indicará que si apaga el dispositivo se interrumpirá cualquier operación de E/S que estuviera en curso, lo que producirá un tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="7610e-164">A warning will appear stating that a shutdown of the device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="7610e-165">Haga clic en el icono de marca de verificación </span><span class="sxs-lookup"><span data-stu-id="7610e-165">Click the check icon</span></span> ![icono de marca de verificación](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="7610e-167">.</span><span class="sxs-lookup"><span data-stu-id="7610e-167">.</span></span>
   
    ![advertencia de apagado del dispositivo](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="7610e-169">Cuando se haya iniciado el apagado verá una notificación.</span><span class="sxs-lookup"><span data-stu-id="7610e-169">You will be notified that the shutdown has been initiated.</span></span>
   
    ![proceso de apagado del dispositivo iniciado](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="7610e-171">El dispositivo se apagará.</span><span class="sxs-lookup"><span data-stu-id="7610e-171">The device will now shut down.</span></span> <span data-ttu-id="7610e-172">Si quiere iniciar el dispositivo, debe hacerlo a través del Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7610e-172">If you want to start your device, you will need to do that through the Hyper-V Manager.</span></span>

#### <a name="to-restart-your-virtual-device"></a><span data-ttu-id="7610e-173">Reiniciar el dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="7610e-173">To restart your virtual device</span></span>
1. <span data-ttu-id="7610e-174">En la interfaz de usuario web local, vaya a **Mantenimiento** > **Configuración de energía**.</span><span class="sxs-lookup"><span data-stu-id="7610e-174">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="7610e-175">En la parte inferior de la página, haga clic en **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="7610e-175">At the bottom of the page, click **Restart**.</span></span>
   
    ![proceso de reinicio del dispositivo](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="7610e-177">Aparecerá una advertencia que le indicará que si reinicia el dispositivo se interrumpirá cualquier operación de E/S que estuviera en curso, lo que resultará en un tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="7610e-177">A warning will appear stating that restarting the device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="7610e-178">Haga clic en el icono de marca de verificación </span><span class="sxs-lookup"><span data-stu-id="7610e-178">Click the check icon</span></span> ![icono de marca de verificación](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="7610e-180">.</span><span class="sxs-lookup"><span data-stu-id="7610e-180">.</span></span>
   
    ![advertencia de reinicio](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="7610e-182">Verá una notificación cuando comience el reinicio.</span><span class="sxs-lookup"><span data-stu-id="7610e-182">You will be notified that the restart has been initiated.</span></span>
   
    ![proceso de reinicio comenzado](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="7610e-184">Mientras el proceso de reinicio esté en curso, perderá la conexión a la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="7610e-184">While the restart is in progress, you will lose the connection to the UI.</span></span> <span data-ttu-id="7610e-185">De todos modos, puede supervisar el proceso de reinicio si actualiza la interfaz de usuario de forma regular.</span><span class="sxs-lookup"><span data-stu-id="7610e-185">You can monitor the restart by refreshing the UI periodically.</span></span> <span data-ttu-id="7610e-186">Como alternativa, puede supervisar el estado del proceso de reinicio del dispositivo a través del Administrador de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7610e-186">Alternatively, you can monitor the device restart status through the Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7610e-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7610e-187">Next steps</span></span>
<span data-ttu-id="7610e-188">Obtenga más información sobre cómo [usar el servicio StorSimple Manager para administrar su dispositivo](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7610e-188">Learn how to [use the StorSimple Manager service to manage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

