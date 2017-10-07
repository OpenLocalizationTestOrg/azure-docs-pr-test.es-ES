---
title: "contraseña de administrador de dispositivos de StorSimple Virtual Array aaaChange | Documentos de Microsoft"
description: "Describe cómo toouse Hola o portal de Azure o la contraseña de administrador dispositivo Hola de toochange de la interfaz de usuario de web de StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="50c13-103">Cambiar contraseña del Administrador de dispositivos de StorSimple Virtual Array de Hola a través del Administrador de dispositivos de StorSimple</span><span class="sxs-lookup"><span data-stu-id="50c13-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="50c13-104">Información general</span><span class="sxs-lookup"><span data-stu-id="50c13-104">Overview</span></span>

<span data-ttu-id="50c13-105">Cuando usas tooaccess de interfaz de Windows PowerShell de Hola Hola StorSimple Virtual Array, estás tooenter requiere una contraseña de administrador de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="50c13-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="50c13-106">Cuando el dispositivo de StorSimple de hello en primer lugar se aprovisionan y se inicia, contraseña predeterminada de hello es *Password1*.</span><span class="sxs-lookup"><span data-stu-id="50c13-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="50c13-107">Para la seguridad de Hola de los datos, contraseña predeterminada de hello expira hello primera vez que inicie una sesión y es necesario toochange esta contraseña.</span><span class="sxs-lookup"><span data-stu-id="50c13-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="50c13-108">También puede usar cualquier hello web local interfaz de usuario o hello toochange portal Azure Hola contraseña de administrador en cualquier momento después de que el dispositivo de Hola se implementa en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="50c13-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="50c13-109">En este artículo se describe cada uno de estos procedimientos.</span><span class="sxs-lookup"><span data-stu-id="50c13-109">Each of these procedures is described in this article.</span></span>

 ![hoja de dispositivos](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="50c13-111">Usar hello toochange portal Azure Hola contraseña</span><span class="sxs-lookup"><span data-stu-id="50c13-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="50c13-112">Realizar Hola siguiendo los pasos toochange Hola contraseña de administrador a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="50c13-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="50c13-113">contraseña de administrador de dispositivos de toochange Hola a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="50c13-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="50c13-114">En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic Hola nombre del servicio y, a continuación, en hello **administración** sección, haga clic en **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="50c13-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="50c13-115">Se abrirá hello **dispositivos** hoja que enumera todos los dispositivos de StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="50c13-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="50c13-116">Hola **dispositivos** hoja, haga doble clic en el dispositivo de Hola que requiere un cambio de contraseña.</span><span class="sxs-lookup"><span data-stu-id="50c13-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="50c13-117">Hola **configuración** hoja para el dispositivo, haga clic en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="50c13-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="50c13-118">Hola **configuración de seguridad** hoja, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="50c13-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="50c13-119">Desplácese hacia abajo toohello **contraseña de administrador de dispositivos** sección.</span><span class="sxs-lookup"><span data-stu-id="50c13-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="50c13-120">Proporcione una contraseña de administrador que tenga entre 8 caracteres too15.</span><span class="sxs-lookup"><span data-stu-id="50c13-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="50c13-121">Confirmar contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="50c13-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="50c13-122">Haga clic en **guardar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="50c13-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="50c13-123">contraseña de administrador de dispositivos de Hola se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="50c13-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="50c13-124">Puede usar este dispositivo de contraseña modificada tooaccess Hola localmente.</span><span class="sxs-lookup"><span data-stu-id="50c13-124">You can use this modified password tooaccess hello device locally.</span></span>

![Hoja Configuración de seguridad](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="50c13-126">Usar hello web local UI toochange Hola contraseña</span><span class="sxs-lookup"><span data-stu-id="50c13-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="50c13-127">Realizar Hola siguiendo los pasos toochange Hola contraseña de administrador a través de la interfaz de usuario de web local Hola.</span><span class="sxs-lookup"><span data-stu-id="50c13-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="50c13-128">contraseña del Administrador de dispositivos de toochange Hola a través de la interfaz de usuario de web local Hola</span><span class="sxs-lookup"><span data-stu-id="50c13-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="50c13-129">En la interfaz de usuario web local de hello, haga clic en **mantenimiento** > **cambio de contraseña** para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="50c13-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![cambiar password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="50c13-131">Escriba hello **contraseña actual**.</span><span class="sxs-lookup"><span data-stu-id="50c13-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="50c13-132">Introduzca una **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="50c13-132">Provide a **New Password**.</span></span> <span data-ttu-id="50c13-133">contraseña de Hello debe ser al menos 8 caracteres.</span><span class="sxs-lookup"><span data-stu-id="50c13-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="50c13-134">Debe contener 3 de 4 siguiente hello: caracteres en mayúsculas, minúsculas, numéricos y especiales.</span><span class="sxs-lookup"><span data-stu-id="50c13-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="50c13-135">Tenga en cuenta que la contraseña no puede ser igual que Hola últimas 24 contraseñas Hola.</span><span class="sxs-lookup"><span data-stu-id="50c13-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="50c13-136">Vuelva a escribir Hola contraseña tooconfirm lo.</span><span class="sxs-lookup"><span data-stu-id="50c13-136">Reenter hello password tooconfirm it.</span></span>
   
    ![cambiar password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="50c13-138">En la parte inferior de Hola de página de hello, haga clic en **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="50c13-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="50c13-139">Ahora se aplica la nueva contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="50c13-139">hello new password is now applied.</span></span> <span data-ttu-id="50c13-140">Si el cambio de contraseña hello no se realiza correctamente, verá Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="50c13-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![error de contraseña](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="50c13-142">Una vez que se actualizó correctamente la contraseña de hello, se le notificará.</span><span class="sxs-lookup"><span data-stu-id="50c13-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="50c13-143">A continuación, puede usar este dispositivo de contraseña modificada tooaccess Hola localmente.</span><span class="sxs-lookup"><span data-stu-id="50c13-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="50c13-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50c13-144">Next steps</span></span>
<span data-ttu-id="50c13-145">Obtenga información acerca de cómo demasiado[administrar la matriz Virtual de StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="50c13-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

