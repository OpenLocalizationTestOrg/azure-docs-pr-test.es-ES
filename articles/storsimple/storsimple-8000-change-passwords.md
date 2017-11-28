---
title: "aaaChange las contraseñas de StorSimple | Documentos de Microsoft"
description: "Describe cómo toouse Hola toochange de servicio de administrador de dispositivos de StorSimple las contraseñas de administrador de administrador de instantáneas StorSimple y dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="663f0-103">Usar toochange de servicio del Administrador de dispositivos de StorSimple de hello las contraseñas de StorSimple</span><span class="sxs-lookup"><span data-stu-id="663f0-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="663f0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="663f0-104">Overview</span></span>
<span data-ttu-id="663f0-105">Hola portal de Azure **configuración de dispositivo** opción contiene todos los parámetros de dispositivo de Hola que puede volver a configurar en un dispositivo de StorSimple que se administra mediante un servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="663f0-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="663f0-106">Este tutorial le explica cómo puede usar hello **seguridad** opción **configuración de dispositivo** toochange el Administrador de dispositivos o la contraseña de administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="663f0-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="663f0-107">Cambiar contraseña de administrador de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="663f0-107">Change hello device administrator password</span></span>
<span data-ttu-id="663f0-108">Cuando se usa el dispositivo de StorSimple de Windows PowerShell interfaz tooaccess Hola, son tooenter requiere una contraseña de administrador de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="663f0-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="663f0-109">Cuando el primer dispositivo de StorSimple Hola está registrado con un servicio, contraseña de hello predeterminada para esta interfaz es *Password1*.</span><span class="sxs-lookup"><span data-stu-id="663f0-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="663f0-110">Por seguridad Hola de los datos, es necesario toochange esta contraseña en el final de Hola Hola del proceso de registro.</span><span class="sxs-lookup"><span data-stu-id="663f0-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="663f0-111">No puede salir del proceso de registro de hello sin cambiar esta contraseña.</span><span class="sxs-lookup"><span data-stu-id="663f0-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="663f0-112">Para obtener más información, consulte [paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="663f0-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="663f0-113">contraseña de Hola que primero se establece a través de la interfaz de Windows PowerShell de Hola durante el registro se puede cambiar más adelante a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="663f0-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="663f0-114">Realizar Hola siguiendo la contraseña de administrador de pasos toochange Hola.</span><span class="sxs-lookup"><span data-stu-id="663f0-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="663f0-115">contraseña del Administrador de dispositivos de toochange Hola</span><span class="sxs-lookup"><span data-stu-id="663f0-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="663f0-116">Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="663f0-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="663f0-117">En la lista tabular de Hola de dispositivos, seleccione y haga clic en el dispositivo de hello cuya contraseña desea toochange.</span><span class="sxs-lookup"><span data-stu-id="663f0-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="663f0-118">Hola **configuración** hoja, vaya demasiado**configuración del dispositivo > seguridad**.</span><span class="sxs-lookup"><span data-stu-id="663f0-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="663f0-119">Hola **configuración de seguridad** hoja, haga clic en **contraseña** contraseña de administrador de dispositivos de toochange Hola.</span><span class="sxs-lookup"><span data-stu-id="663f0-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="663f0-120">Hola **contraseña** hoja, proporcione una contraseña de administrador que tenga entre 8 caracteres too15.</span><span class="sxs-lookup"><span data-stu-id="663f0-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="663f0-121">contraseña de Hello debe ser una combinación de 3 o más caracteres en mayúsculas, minúsculas, numéricos y especiales.</span><span class="sxs-lookup"><span data-stu-id="663f0-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="663f0-122">Confirmar contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="663f0-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="663f0-123">Haga clic en **Guardar** y, cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="663f0-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="663f0-124">Esto se actualizará la contraseña del Administrador de dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="663f0-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="663f0-125">Puede usar esta interfaz de Windows PowerShell de contraseña modificada tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="663f0-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="663f0-126">Establecer contraseña de administrador de instantáneas StorSimple Hola</span><span class="sxs-lookup"><span data-stu-id="663f0-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="663f0-127">Software de administrador de instantáneas StorSimple reside en el host de Windows y permite a los administradores toomanage copias de seguridad del dispositivo de StorSimple en forma de Hola de local y en la nube.</span><span class="sxs-lookup"><span data-stu-id="663f0-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="663f0-128">Al configurar un dispositivo en el Administrador de instantáneas de StorSimple, se le pedirá tooprovide Hola tooauthenticate de dirección y la contraseña de la IP de dispositivo, el dispositivo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="663f0-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="663f0-129">Puede establecer o cambiar la contraseña de hello para el Administrador de instantáneas de StorSimple a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="663f0-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="663f0-130">Realizar Hola siguiendo los pasos tooset o cambiar la contraseña de administrador de instantáneas StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="663f0-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="663f0-131">contraseña de administrador de instantáneas StorSimple hello tooset</span><span class="sxs-lookup"><span data-stu-id="663f0-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="663f0-132">Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="663f0-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="663f0-133">En la lista tabular de Hola de dispositivos, seleccione y haga clic en el dispositivo de hello cuya contraseña de administrador de instantáneas StorSimple va tooset o cambiar.</span><span class="sxs-lookup"><span data-stu-id="663f0-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="663f0-134">Hola **configuración** hoja, vaya demasiado**configuración del dispositivo > seguridad**.</span><span class="sxs-lookup"><span data-stu-id="663f0-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="663f0-135">Hola **configuración de seguridad** hoja, haga clic en **contraseña** tooset o cambiar contraseña de administrador de instantáneas StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="663f0-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="663f0-136">Hola **contraseña** hoja, escriba una contraseña de 14 o 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="663f0-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="663f0-137">Asegúrese de que esa contraseña hello contiene una combinación de 3 o más caracteres en mayúsculas, minúsculas, numéricos y especiales.</span><span class="sxs-lookup"><span data-stu-id="663f0-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="663f0-138">Confirmar contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="663f0-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="663f0-139">Haga clic en **Guardar** y, cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="663f0-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="663f0-140">Esto se actualizará la contraseña de administrador de instantáneas StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="663f0-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="663f0-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="663f0-141">Next steps</span></span>
* <span data-ttu-id="663f0-142">Obtenga más información sobre la [seguridad de StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="663f0-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="663f0-143">Obtenga más información sobre la [modificación de la configuración del dispositivo](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="663f0-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="663f0-144">Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="663f0-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

