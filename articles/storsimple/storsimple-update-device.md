---
title: aaaUpdate el dispositivo StorSimple | Documentos de Microsoft
description: "Explica cómo toouse hello StorSimple actualizar tooinstall característica regular y actualizaciones del modo de mantenimiento y las revisiones."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="82709-103">Actualización del dispositivo de la serie StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="82709-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="82709-104">Información general</span><span class="sxs-lookup"><span data-stu-id="82709-104">Overview</span></span>
<span data-ttu-id="82709-105">Hello StorSimple actualizaciones características le permiten tooeasily mantener actualizado el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="82709-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="82709-106">Según el tipo de actualización de hello, puede aplicar el dispositivo de toohello de las actualizaciones a través del portal de Azure clásico de Hola o a través de la interfaz de Windows PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="82709-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="82709-107">Este tutorial describen los tipos de actualización de Hola y cómo tooinstall de ellos.</span><span class="sxs-lookup"><span data-stu-id="82709-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="82709-108">Puede aplicar dos tipos de actualizaciones de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="82709-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="82709-109">Actualizaciones normales (o en modo normal)</span><span class="sxs-lookup"><span data-stu-id="82709-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="82709-110">Actualizaciones en modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="82709-110">Maintenance mode updates</span></span>

<span data-ttu-id="82709-111">Puede instalar actualizaciones periódicas a través de hello portal de Azure clásico o Windows PowerShell; Sin embargo, debe usar las actualizaciones del modo de mantenimiento de Windows PowerShell tooinstall.</span><span class="sxs-lookup"><span data-stu-id="82709-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="82709-112">A continuación se describe cada tipo de actualización.</span><span class="sxs-lookup"><span data-stu-id="82709-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="82709-113">Actualizaciones normales</span><span class="sxs-lookup"><span data-stu-id="82709-113">Regular updates</span></span>
<span data-ttu-id="82709-114">Las actualizaciones normales son las actualizaciones no causan interrupción y que se pueden instalar cuando el dispositivo de hello está en modo Normal.</span><span class="sxs-lookup"><span data-stu-id="82709-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="82709-115">Estas actualizaciones se aplican a través de controlador de dispositivo de tooeach de sitio Web de Microsoft Update de Hola.</span><span class="sxs-lookup"><span data-stu-id="82709-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="82709-116">Un controlador de conmutación por error puede producirse durante el proceso de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="82709-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="82709-117">Sin embargo, esto no afectará a la disponibilidad ni al funcionamiento del sistema.</span><span class="sxs-lookup"><span data-stu-id="82709-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="82709-118">Para obtener detalles sobre cómo tooinstall actualizaciones frecuentes a través de hello portal de Azure clásico, consulte [instale actualizaciones periódicas a través del portal de Azure clásico hello](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="82709-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="82709-119">También puede instalar actualizaciones normales a través de Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="82709-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="82709-120">Para obtener más información, consulte [Instalación de actualizaciones normales a través de Windows PowerShell para StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="82709-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="82709-121">Actualizaciones en modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="82709-121">Maintenance mode updates</span></span>
<span data-ttu-id="82709-122">Se trata de actualizaciones con interrupciones, como las actualizaciones de firmware de disco.</span><span class="sxs-lookup"><span data-stu-id="82709-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="82709-123">Estas actualizaciones requieren Hola dispositivo toobe poner en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="82709-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="82709-124">Para obtener más información, consulte [Paso 2: Acceso al modo de mantenimiento](#step2).</span><span class="sxs-lookup"><span data-stu-id="82709-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="82709-125">No se puede usar actualizaciones del modo de mantenimiento de hello Azure tooinstall portal clásico.</span><span class="sxs-lookup"><span data-stu-id="82709-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="82709-126">En su lugar, debe usar Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="82709-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="82709-127">Para obtener detalles sobre cómo actualiza el modo de mantenimiento de tooinstall, consulte [actualizaciones del modo de mantenimiento de la instalación a través de Windows PowerShell para StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="82709-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82709-128">Modo de mantenimiento de actualizaciones deben aplicarse por separado tooeach controlador.</span><span class="sxs-lookup"><span data-stu-id="82709-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="82709-129">Instale actualizaciones periódicas a través de hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="82709-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="82709-130">Puede usar el dispositivo de StorSimple de tooyour de las actualizaciones de hello Azure tooapply portal clásico.</span><span class="sxs-lookup"><span data-stu-id="82709-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="82709-131">Instalación de actualizaciones normales a través de Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="82709-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="82709-132">Como alternativa, puede usar Windows PowerShell para las actualizaciones de StorSimple tooapply normal (modo Normal).</span><span class="sxs-lookup"><span data-stu-id="82709-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82709-133">Aunque puede instalar las actualizaciones normales mediante Windows PowerShell para StorSimple, recomendamos encarecidamente que instale actualizaciones periódicas a través de hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="82709-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="82709-134">A partir de Update 1, comprobaciones previas será tooinstalling anteriores realizan actualizaciones desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="82709-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="82709-135">Estas comprobaciones previas previenen los errores y garantizan una experiencia con menos complicaciones.</span><span class="sxs-lookup"><span data-stu-id="82709-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="82709-136">Instalación de actualizaciones en modo de mantenimiento a través de Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="82709-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="82709-137">Usar Windows PowerShell para StorSimple tooapply mantenimiento modo actualizaciones tooyour el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="82709-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="82709-138">En este modo, todas las solicitudes de E/S se interrumpen.</span><span class="sxs-lookup"><span data-stu-id="82709-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="82709-139">También se detienen los servicios como la memoria de acceso aleatorio no volátil (NVRAM) o servicio de Cluster Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="82709-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="82709-140">Al entrar o salir de este modo, se reinician ambos controladores.</span><span class="sxs-lookup"><span data-stu-id="82709-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="82709-141">Al salir de este modo, todos los servicios de hello continuará y deben estar en buen Estados.</span><span class="sxs-lookup"><span data-stu-id="82709-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="82709-142">Esto puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="82709-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="82709-143">Si necesita actualizaciones del modo de mantenimiento tooapply, recibirá una alerta a través del portal de Azure clásico de Hola que tiene actualizaciones que se deben instalar.</span><span class="sxs-lookup"><span data-stu-id="82709-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="82709-144">Esta alerta incluirá instrucciones para usar Windows PowerShell para las actualizaciones de StorSimple tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="82709-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="82709-145">Después de actualizar el dispositivo, use Hola mismo modo de procedimiento toochange Hola dispositivo tooRegular.</span><span class="sxs-lookup"><span data-stu-id="82709-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="82709-146">Para obtener instrucciones detalladas, consulte [Paso 4: Salir del modo de mantenimiento](#step4).</span><span class="sxs-lookup"><span data-stu-id="82709-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="82709-147">Antes de entrar en modo de mantenimiento, compruebe que ambos controladores de dispositivo están en buenas condiciones comprobando hello **estado del Hardware** en hello **mantenimiento** página Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="82709-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="82709-148">Si el controlador de hello no es correcto, póngase en contacto con Microsoft Support para los pasos siguientes Hola.</span><span class="sxs-lookup"><span data-stu-id="82709-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="82709-149">Para obtener más información, visite tooContact Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="82709-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="82709-150">Cuando esté en modo de mantenimiento, necesita tooapply Hola actualización primero en un controlador y, a continuación, en Hola otro controlador.</span><span class="sxs-lookup"><span data-stu-id="82709-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="82709-151">Paso 1: Conectar la consola serie toohello<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="82709-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="82709-152">En primer lugar, utilice una aplicación como PuTTY tooaccess Hola consola serie.</span><span class="sxs-lookup"><span data-stu-id="82709-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="82709-153">Hello siguiente procedimiento se explica cómo toouse tooconnect PuTTY toohello consola en serie.</span><span class="sxs-lookup"><span data-stu-id="82709-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="82709-154">Paso 2: Acceso al modo de mantenimiento <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="82709-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="82709-155">Después de conectar la consola de toohello, determinar si existen actualizaciones tooinstall y escriba tooinstall de modo de mantenimiento ellos.</span><span class="sxs-lookup"><span data-stu-id="82709-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="82709-156">Paso 3: Instalación de las actualizaciones <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="82709-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="82709-157">A continuación, instale las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="82709-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="82709-158">Paso 4: Salir del modo de mantenimiento <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="82709-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="82709-159">Por último, salga del modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="82709-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="82709-160">Instale las reparaciones mediante Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="82709-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="82709-161">A diferencia de las actualizaciones para Microsoft Azure StorSimple, las revisiones se instalan desde una carpeta compartida.</span><span class="sxs-lookup"><span data-stu-id="82709-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="82709-162">Al igual que en el caso de las actualizaciones, hay dos tipos de revisiones:</span><span class="sxs-lookup"><span data-stu-id="82709-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="82709-163">Revisiones normales</span><span class="sxs-lookup"><span data-stu-id="82709-163">Regular hotfixes</span></span> 
* <span data-ttu-id="82709-164">Revisiones en modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="82709-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="82709-165">Hello procedimientos siguientes explican cómo toouse Windows PowerShell para StorSimple tooinstall regular y las revisiones de modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="82709-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="82709-166">¿Qué ocurre restablecer tooupdates si lleva a cabo una fábrica del dispositivo de hello?</span><span class="sxs-lookup"><span data-stu-id="82709-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="82709-167">Si un dispositivo es restablecer toofactory configuración, todas las actualizaciones de Hola se pierden.</span><span class="sxs-lookup"><span data-stu-id="82709-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="82709-168">Después de hello restablecimiento de fábrica está registrado y configurado, necesitará toomanually instalar las actualizaciones a través de hello portal de Azure clásico o Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="82709-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="82709-169">Para obtener más información sobre el restablecimiento de fábrica, consulte [restablecer la configuración predeterminada de hello dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="82709-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82709-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82709-170">Next steps</span></span>
* <span data-ttu-id="82709-171">Obtenga más información sobre [mediante Windows PowerShell para StorSimple tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="82709-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="82709-172">Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="82709-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

