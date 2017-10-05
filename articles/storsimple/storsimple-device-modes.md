---
title: Cambiar el modo del dispositivo StorSimple | Microsoft Docs
description: "Describe los modos de dispositivo StorSimple y explica cómo usar Windows PowerShell para StorSimple para cambiar el modo del dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 33c65bf2eecff3914f3227c76f7d638a4507e1f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="b6b96-103">Cambiar el modo del dispositivo en su dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="b6b96-103">Change the device mode on your StorSimple device</span></span>
<span data-ttu-id="b6b96-104">En este artículo se proporciona una breve descripción de los distintos modos en que puede funcionar el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b6b96-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="b6b96-105">El dispositivo StorSimple puede funcionar en tres modos: normal, de mantenimiento y de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b6b96-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="b6b96-106">Después de leer este artículo, sabrá acerca de:</span><span class="sxs-lookup"><span data-stu-id="b6b96-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="b6b96-107">¿Qué son los modos del dispositivo StorSimple?</span><span class="sxs-lookup"><span data-stu-id="b6b96-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="b6b96-108">Cómo determinar el modo en que está establecido el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b6b96-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="b6b96-109">Cómo cambiar del modo normal al modo de mantenimiento y *viceversa*</span><span class="sxs-lookup"><span data-stu-id="b6b96-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="b6b96-110">Las tareas de administración mencionadas solo pueden realizarse a través de la interfaz de Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b6b96-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="b6b96-111">Acerca de los modos del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b6b96-111">About StorSimple device modes</span></span>
<span data-ttu-id="b6b96-112">El dispositivo StorSimple puede funcionar en modo normal, de mantenimiento o de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b6b96-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="b6b96-113">A continuación se describe brevemente cada uno de estos modos.</span><span class="sxs-lookup"><span data-stu-id="b6b96-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="b6b96-114">Modo Normal</span><span class="sxs-lookup"><span data-stu-id="b6b96-114">Normal mode</span></span>
<span data-ttu-id="b6b96-115">Está definido como modo de funcionamiento normal de un dispositivo StorSimple totalmente configurado.</span><span class="sxs-lookup"><span data-stu-id="b6b96-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="b6b96-116">De manera predeterminada, su dispositivo debería estar en modo normal.</span><span class="sxs-lookup"><span data-stu-id="b6b96-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="b6b96-117">Modo Mantenimiento</span><span class="sxs-lookup"><span data-stu-id="b6b96-117">Maintenance mode</span></span>
<span data-ttu-id="b6b96-118">A veces puede ser necesario colocar el dispositivo StorSimple en el modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b6b96-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="b6b96-119">Este modo le permite realizar tareas de mantenimiento en el dispositivo e instalar actualizaciones potencialmente problemáticas, como las relacionadas con el firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="b6b96-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="b6b96-120">Solo puede poner el sistema en modo de mantenimiento por medio de Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b6b96-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b6b96-121">En este modo, todas las solicitudes de E/S se interrumpen.</span><span class="sxs-lookup"><span data-stu-id="b6b96-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="b6b96-122">También se detienen servicios como la memoria de acceso aleatorio no volátil (NVRAM) o el servicio de Cluster Server.</span><span class="sxs-lookup"><span data-stu-id="b6b96-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="b6b96-123">Ambos controladores se reinician al entrar o salir de este modo.</span><span class="sxs-lookup"><span data-stu-id="b6b96-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="b6b96-124">Al salir del modo de mantenimiento, todos los servicios se reanudan y deben funcionar correctamente.</span><span class="sxs-lookup"><span data-stu-id="b6b96-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="b6b96-125">Esta operación puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b6b96-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="b6b96-126">**El modo Mantenimiento solo se admite en un dispositivo que funcione correctamente. No se admite en un dispositivo en el que uno o ambos controladores no funcionan.**
> </span><span class="sxs-lookup"><span data-stu-id="b6b96-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="b6b96-127">Modo Recuperación</span><span class="sxs-lookup"><span data-stu-id="b6b96-127">Recovery mode</span></span>
<span data-ttu-id="b6b96-128">El modo Recuperación puede describirse como el "Modo seguro de Windows con compatibilidad de red".</span><span class="sxs-lookup"><span data-stu-id="b6b96-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="b6b96-129">El modo Recuperación avisa al equipo de soporte técnico de Microsoft y le permite realizar diagnósticos en el sistema.</span><span class="sxs-lookup"><span data-stu-id="b6b96-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="b6b96-130">El objetivo principal del modo de recuperación es recuperar los registros del sistema.</span><span class="sxs-lookup"><span data-stu-id="b6b96-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="b6b96-131">Si el sistema entra en modo de recuperación, debe ponerse en contacto con el soporte técnico de Microsoft para obtener asistencia.</span><span class="sxs-lookup"><span data-stu-id="b6b96-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="b6b96-132">Para obtener más información, vaya a [Contactar al soporte técnico de Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b6b96-132">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b6b96-133">**No puede poner el dispositivo en modo de recuperación. Si el dispositivo está en mal estado, el modo de recuperación intenta llevar al dispositivo a un estado en el que el personal de soporte técnico de Microsoft pueda examinarlo.**</span><span class="sxs-lookup"><span data-stu-id="b6b96-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="b6b96-134">Determinar el modo de dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="b6b96-134">Determine StorSimple device mode</span></span>
#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="b6b96-135">Para determinar el modo del dispositivo actual</span><span class="sxs-lookup"><span data-stu-id="b6b96-135">To determine the current device mode</span></span>
1. <span data-ttu-id="b6b96-136">Inicie sesión en la consola serie del dispositivo siguiendo los pasos detallados en [Uso de PuTTY para conectarse a la consola serie del dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b6b96-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="b6b96-137">Mire el mensaje de pancarta del menú de la consola serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b6b96-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="b6b96-138">Este mensaje indica de forma explícita si el dispositivo está en modo de mantenimiento o de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b6b96-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="b6b96-139">Si el mensaje no contiene información específica relativa al modo del sistema, el dispositivo está en modo normal.</span><span class="sxs-lookup"><span data-stu-id="b6b96-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="b6b96-140">Cambiar el modo del dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="b6b96-140">Change the StorSimple device mode</span></span>
<span data-ttu-id="b6b96-141">Puede colocar el dispositivo StorSimple en modo de mantenimiento (desde el modo normal) para realizar tareas de mantenimiento o instalar las actualizaciones del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b6b96-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="b6b96-142">Lleve a cabo los siguientes procedimientos para entrar o salir del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b6b96-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6b96-143">Antes de entrar en modo de mantenimiento, verifique que ambos controladores del dispositivo funcionen correctamente. Para ello, vaya a **Estado de hardware** en la página **Mantenimiento** del Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="b6b96-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="b6b96-144">Si uno o ambos controladores no tienen un estado correcto, póngase en contacto con el servicio de soporte técnico de Microsoft para conocer los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="b6b96-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="b6b96-145">Para obtener más información, vaya a [Contactar al soporte técnico de Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b6b96-145">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="b6b96-146">Para acceder al modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="b6b96-146">To enter maintenance mode</span></span>
1. <span data-ttu-id="b6b96-147">Inicie sesión en la consola serie del dispositivo siguiendo los pasos detallados en [Uso de PuTTY para conectarse a la consola serie del dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b6b96-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="b6b96-148">En el menú de la consola serie, seleccione la opción 1, **Iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="b6b96-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="b6b96-149">Cuando se le solicite, proporcione la **contraseña de administrador de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="b6b96-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="b6b96-150">La contraseña predeterminada es: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="b6b96-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="b6b96-151">En el símbolo del sistema, escriba</span><span class="sxs-lookup"><span data-stu-id="b6b96-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="b6b96-152">Verá un mensaje de advertencia que indica que el modo de mantenimiento interrumpe todas las solicitudes de E/S y detiene la conexión al Portal de Azure clásico. También se le solicitará la confirmación.</span><span class="sxs-lookup"><span data-stu-id="b6b96-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="b6b96-153">Escriba **Y** para acceder al modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b6b96-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="b6b96-154">Ambos controladores se reiniciarán.</span><span class="sxs-lookup"><span data-stu-id="b6b96-154">Both controllers will restart.</span></span> <span data-ttu-id="b6b96-155">Una vez completado el reinicio, aparecerá otro mensaje que indica que el dispositivo está en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b6b96-155">When the restart is complete, another message will appear indicating that the device is in maintenance mode.</span></span>

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="b6b96-156">Para salir del modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="b6b96-156">To exit maintenance mode</span></span>
1. <span data-ttu-id="b6b96-157">Inicie sesión en la consola serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b6b96-157">Log on to the device serial console.</span></span> <span data-ttu-id="b6b96-158">En el mensaje de pancarta, verifique que el dispositivo esté en el modo Mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b6b96-158">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="b6b96-159">En el símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="b6b96-159">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="b6b96-160">Aparecerán un mensaje de advertencia y un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="b6b96-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="b6b96-161">Escriba **Y** para salir del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b6b96-161">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="b6b96-162">Ambos controladores se reiniciarán.</span><span class="sxs-lookup"><span data-stu-id="b6b96-162">Both controllers will restart.</span></span> <span data-ttu-id="b6b96-163">Una vez completado el reinicio, aparecerá otro mensaje que indica que el dispositivo está en modo normal.</span><span class="sxs-lookup"><span data-stu-id="b6b96-163">When the restart is complete, another message will appear indicating that the device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6b96-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6b96-164">Next steps</span></span>
<span data-ttu-id="b6b96-165">Aprenda a [aplicar las actualizaciones del modo normal y del de mantenimiento](storsimple-update-device.md) en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b6b96-165">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

