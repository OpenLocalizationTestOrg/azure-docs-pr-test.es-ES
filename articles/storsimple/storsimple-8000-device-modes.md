---
title: modo de dispositivo de StorSimple aaaChange | Documentos de Microsoft
description: "Describe los modos de dispositivo de StorSimple de Hola y explica cómo toouse Windows PowerShell para StorSimple toochange Hola modo del dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="ddae1-103">Cambiar el modo de dispositivo de hello en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="ddae1-103">Change hello device mode on your StorSimple device</span></span>

<span data-ttu-id="ddae1-104">En este artículo se proporciona una breve descripción del programa Hola a distintos modos en los que puede operar el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ddae1-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="ddae1-105">El dispositivo StorSimple puede funcionar en tres modos: normal, de mantenimiento y de recuperación.</span><span class="sxs-lookup"><span data-stu-id="ddae1-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="ddae1-106">Después de leer este artículo, sabrá acerca de:</span><span class="sxs-lookup"><span data-stu-id="ddae1-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="ddae1-107">¿Cuáles son los modos de dispositivo de StorSimple de Hola</span><span class="sxs-lookup"><span data-stu-id="ddae1-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="ddae1-108">¿Cómo toofigure qué modo Hola dispositivo StorSimple está en</span><span class="sxs-lookup"><span data-stu-id="ddae1-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="ddae1-109">¿Cómo toochange del modo de toomaintenance normal y *viceversa*</span><span class="sxs-lookup"><span data-stu-id="ddae1-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="ddae1-110">Hola por encima de las tareas de administración solo puede realizarse a través de la interfaz de Windows PowerShell de hello de dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ddae1-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="ddae1-111">Acerca de los modos del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ddae1-111">About StorSimple device modes</span></span>

<span data-ttu-id="ddae1-112">El dispositivo StorSimple puede funcionar en modo normal, de mantenimiento o de recuperación.</span><span class="sxs-lookup"><span data-stu-id="ddae1-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="ddae1-113">A continuación se describe brevemente cada uno de estos modos.</span><span class="sxs-lookup"><span data-stu-id="ddae1-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="ddae1-114">Modo Normal</span><span class="sxs-lookup"><span data-stu-id="ddae1-114">Normal mode</span></span>

<span data-ttu-id="ddae1-115">Esto se define como modo de funcionamiento normal de Hola para un dispositivo de StorSimple totalmente configurado.</span><span class="sxs-lookup"><span data-stu-id="ddae1-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="ddae1-116">De manera predeterminada, su dispositivo debería estar en modo normal.</span><span class="sxs-lookup"><span data-stu-id="ddae1-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="ddae1-117">Modo Mantenimiento</span><span class="sxs-lookup"><span data-stu-id="ddae1-117">Maintenance mode</span></span>

<span data-ttu-id="ddae1-118">A veces hello dispositivo StorSimple que necesite toobe pone en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="ddae1-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="ddae1-119">Este modo permite el mantenimiento de tooperform en dispositivo de Hola e instalar actualizaciones potencialmente perjudiciales, como las relacionadas con firmware toodisk.</span><span class="sxs-lookup"><span data-stu-id="ddae1-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="ddae1-120">Puede colocar sistema hello en modo de mantenimiento sólo a través de hello Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ddae1-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="ddae1-121">En este modo, todas las solicitudes de E/S se interrumpen.</span><span class="sxs-lookup"><span data-stu-id="ddae1-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="ddae1-122">También se detienen los servicios como la memoria de acceso aleatorio no volátil (NVRAM) o servicio de Cluster Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddae1-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="ddae1-123">Ambos controladores Hola se reinician cuando entra o sale de este modo.</span><span class="sxs-lookup"><span data-stu-id="ddae1-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="ddae1-124">Al salir del modo de mantenimiento de hello, todos los servicios de hello continuará y deben estar en buen Estados.</span><span class="sxs-lookup"><span data-stu-id="ddae1-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="ddae1-125">Esta operación puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ddae1-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="ddae1-126">**El modo Mantenimiento solo se admite en un dispositivo que funcione correctamente. No se admite en un dispositivo en el que uno o ambos de controladores de hello no funcionan.**</span><span class="sxs-lookup"><span data-stu-id="ddae1-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="ddae1-127">Modo Recuperación</span><span class="sxs-lookup"><span data-stu-id="ddae1-127">Recovery mode</span></span>

<span data-ttu-id="ddae1-128">El modo Recuperación puede describirse como el "Modo seguro de Windows con compatibilidad de red".</span><span class="sxs-lookup"><span data-stu-id="ddae1-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="ddae1-129">Modo de recuperación pone el equipo de Microsoft Support hello y les permite tooperform diagnósticos en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddae1-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="ddae1-130">Hola principal objetivo del modo de recuperación es registros del sistema tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="ddae1-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="ddae1-131">Si el sistema entra en modo de recuperación, debe ponerse en contacto con el soporte técnico de Microsoft para obtener asistencia.</span><span class="sxs-lookup"><span data-stu-id="ddae1-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="ddae1-132">Para obtener más información, consulte demasiado[póngase en contacto con soporte técnico de Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="ddae1-132">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ddae1-133">**No se puede colocar el dispositivo de hello en modo de recuperación. Si el dispositivo de hello está en mal estado, modo de recuperación intenta tooget dispositivo de hello en un estado en el que el personal de Microsoft Support pueda examinarlo.**</span><span class="sxs-lookup"><span data-stu-id="ddae1-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="ddae1-134">Determinar el modo de dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="ddae1-134">Determine StorSimple device mode</span></span>

#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="ddae1-135">modo toodetermine hello de dispositivo actual</span><span class="sxs-lookup"><span data-stu-id="ddae1-135">toodetermine hello current device mode</span></span>

1. <span data-ttu-id="ddae1-136">Inicie sesión en la consola serie del dispositivo toohello siguiendo los pasos de hello en [consola serie del dispositivo Use PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ddae1-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="ddae1-137">Mire el mensaje de pancarta hello en el menú de consola serie de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddae1-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="ddae1-138">Este mensaje indica explícitamente si dispositivo Hola está en modo de mantenimiento o de recuperación.</span><span class="sxs-lookup"><span data-stu-id="ddae1-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="ddae1-139">Si el mensaje de bienvenida no contiene ninguna información específica relativa a modo de sistema de toohello, dispositivo Hola está en modo normal.</span><span class="sxs-lookup"><span data-stu-id="ddae1-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="ddae1-140">Cambiar el modo de dispositivo de StorSimple Hola</span><span class="sxs-lookup"><span data-stu-id="ddae1-140">Change hello StorSimple device mode</span></span>

<span data-ttu-id="ddae1-141">Puede colocar el dispositivo de StorSimple de hello en mantenimiento de tooperform modo (de modo normal) o instalar actualizaciones del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="ddae1-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="ddae1-142">Realizar Hola siguiendo el modo de mantenimiento de tooenter o salir de procedimientos.</span><span class="sxs-lookup"><span data-stu-id="ddae1-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddae1-143">Antes de entrar en modo de mantenimiento, compruebe que ambos controladores de dispositivo están en buenas condiciones accediendo hello **configuración del dispositivo > estado del Hardware** para el dispositivo en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ddae1-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Device settings > Hardware health** for your device in hello Azure portal.</span></span> <span data-ttu-id="ddae1-144">Si uno o ambos controladores hello no sean correcto, póngase en contacto con Microsoft Support para los pasos siguientes Hola.</span><span class="sxs-lookup"><span data-stu-id="ddae1-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="ddae1-145">Para obtener más información, consulte demasiado[póngase en contacto con soporte técnico de Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="ddae1-145">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="ddae1-146">modo de mantenimiento de tooenter</span><span class="sxs-lookup"><span data-stu-id="ddae1-146">tooenter maintenance mode</span></span>

1. <span data-ttu-id="ddae1-147">Inicie sesión en la consola serie del dispositivo toohello siguiendo los pasos de hello en [consola serie del dispositivo Use PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ddae1-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="ddae1-148">En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="ddae1-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="ddae1-149">Cuando se le solicite, proporcione hello **contraseña de administrador de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ddae1-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="ddae1-150">contraseña de Hello predeterminada es: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="ddae1-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="ddae1-151">En hello símbolo del sistema, escriba</span><span class="sxs-lookup"><span data-stu-id="ddae1-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="ddae1-152">Verá un mensaje de advertencia que le indica que el modo de mantenimiento interrumpirá todas las solicitudes de E/S y Hola conexión toohello portal de Azure y se le pedirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="ddae1-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="ddae1-153">Tipo de **Y** tooenter modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="ddae1-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="ddae1-154">Ambos controladores se reiniciarán.</span><span class="sxs-lookup"><span data-stu-id="ddae1-154">Both controllers will restart.</span></span> <span data-ttu-id="ddae1-155">Una vez completado el reinicio de hello, banner de consola serie de hello indicará que ese dispositivo Hola está en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="ddae1-155">When hello restart is complete, hello serial console banner will indicate that hello device is in maintenance mode.</span></span> <span data-ttu-id="ddae1-156">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ddae1-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="ddae1-157">modo de mantenimiento de tooexit</span><span class="sxs-lookup"><span data-stu-id="ddae1-157">tooexit maintenance mode</span></span>

1. <span data-ttu-id="ddae1-158">Inicie sesión en la consola serie del dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="ddae1-158">Log on toohello device serial console.</span></span> <span data-ttu-id="ddae1-159">Compruebe de mensaje de pancarta Hola que el dispositivo está en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="ddae1-159">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="ddae1-160">En hello símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="ddae1-160">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="ddae1-161">Aparecerán un mensaje de advertencia y un mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="ddae1-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="ddae1-162">Tipo de **Y** tooexit modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="ddae1-162">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="ddae1-163">Ambos controladores se reiniciarán.</span><span class="sxs-lookup"><span data-stu-id="ddae1-163">Both controllers will restart.</span></span> <span data-ttu-id="ddae1-164">Una vez completado el reinicio de hello, banner de consola serie de hello indica que ese dispositivo Hola está en modo normal.</span><span class="sxs-lookup"><span data-stu-id="ddae1-164">When hello restart is complete, hello serial console banner indicates that hello device is in normal mode.</span></span> <span data-ttu-id="ddae1-165">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ddae1-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="ddae1-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ddae1-166">Next steps</span></span>

<span data-ttu-id="ddae1-167">Obtenga información acerca de cómo demasiado[aplicar las actualizaciones del modo normal y el mantenimiento](storsimple-update-device.md) en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ddae1-167">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

