---
title: "Cambio de la contraseña del administrador de dispositivos de StorSimple Virtual Array | Microsoft Docs"
description: "Describe cómo usar Azure Portal o la interfaz de usuario web de StorSimple Virtual Array para cambiar la contraseña del administrador de dispositivos."
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
ms.openlocfilehash: 260a23003d705e6598da8c51bb5a96f2539a0014
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="cb459-103">Cambio de la contraseña del administrador de dispositivos de la matriz virtual de StorSimple mediante StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="cb459-103">Change the StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="cb459-104">Información general</span><span class="sxs-lookup"><span data-stu-id="cb459-104">Overview</span></span>

<span data-ttu-id="cb459-105">Cuando use la interfaz de Windows PowerShell para acceder a StorSimple Virtual Array, se le pedirá que escriba una contraseña de administrador de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cb459-105">When you use the Windows PowerShell interface to access the StorSimple Virtual Array, you are required to enter a device administrator password.</span></span> <span data-ttu-id="cb459-106">Cuando el dispositivo StorSimple se aprovisione e inicie por primera vez, la contraseña predeterminada es *Password1*.</span><span class="sxs-lookup"><span data-stu-id="cb459-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span></span> <span data-ttu-id="cb459-107">Para la seguridad de los datos, la contraseña predeterminada caduca la primera vez que inicia sesión y deberá cambiar esta contraseña.</span><span class="sxs-lookup"><span data-stu-id="cb459-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span></span>

<span data-ttu-id="cb459-108">También puede utilizar la interfaz de usuario web local o Azure Portal para cambiar la contraseña del administrador de dispositivos en cualquier momento después de que el dispositivo se implemente en un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cb459-108">You can also use either the local web UI or the Azure portal to change the device administrator password at any time after the device is deployed in your production environment.</span></span> <span data-ttu-id="cb459-109">En este artículo se describe cada uno de estos procedimientos.</span><span class="sxs-lookup"><span data-stu-id="cb459-109">Each of these procedures is described in this article.</span></span>

 ![hoja de dispositivos](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-the-azure-portal-to-change-the-password"></a><span data-ttu-id="cb459-111">Uso de Azure Portal para cambiar la contraseña</span><span class="sxs-lookup"><span data-stu-id="cb459-111">Use the Azure portal to change the password</span></span>

<span data-ttu-id="cb459-112">Realice los pasos siguientes para cambiar la contraseña del administrador de dispositivos a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cb459-112">Perform the following steps to change the device administrator password through the Azure portal.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-azure-portal"></a><span data-ttu-id="cb459-113">Para cambiar la contraseña del administrador de dispositivos a través de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cb459-113">To change the device administrator password via the Azure portal</span></span>

1. <span data-ttu-id="cb459-114">En la página de aterrizaje del servicio, seleccione el servicio, haga doble clic en su nombre y, en la sección **Administración**, haga clic en **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="cb459-114">On the service landing page, select your service, double-click the service name, and then within the **Management** section, click **Devices**.</span></span> <span data-ttu-id="cb459-115">Se abrirá la hoja **Dispositivos**, que enumera todos los dispositivos de StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="cb459-115">This opens the **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="cb459-116">En la hoja **Dispositivos**, haga doble clic en el dispositivo que requiere un cambio de contraseña.</span><span class="sxs-lookup"><span data-stu-id="cb459-116">In the **Devices** blade, double-click the device that requires a change of password.</span></span>

3. <span data-ttu-id="cb459-117">En la hoja **Configuración** del dispositivo, haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="cb459-117">In the **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="cb459-118">En la hoja **Configuración de seguridad**, realice las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="cb459-118">In the **Security Settings** blade, do the following:</span></span>
   
   1. <span data-ttu-id="cb459-119">Desplácese hacia abajo a la sección **Contraseña de administrador de dispositivos** .</span><span class="sxs-lookup"><span data-stu-id="cb459-119">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="cb459-120">Proporcione una contraseña de administrador que tenga entre 8 y 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="cb459-120">Provide an administrator password that contains from 8 to 15 characters.</span></span>
   2. <span data-ttu-id="cb459-121">Confirme la contraseña.</span><span class="sxs-lookup"><span data-stu-id="cb459-121">Confirm the password.</span></span>
   3. <span data-ttu-id="cb459-122">Haga clic en **Guardar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="cb459-122">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="cb459-123">La contraseña del administrador de dispositivos ya está actualizada.</span><span class="sxs-lookup"><span data-stu-id="cb459-123">The device administrator password is now updated.</span></span> <span data-ttu-id="cb459-124">Puede usar esta contraseña modificada para tener acceso al dispositivo de forma local.</span><span class="sxs-lookup"><span data-stu-id="cb459-124">You can use this modified password to access the device locally.</span></span>

![Hoja Configuración de seguridad](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-the-local-web-ui-to-change-the-password"></a><span data-ttu-id="cb459-126">Uso de la interfaz de usuario web local para cambiar la contraseña</span><span class="sxs-lookup"><span data-stu-id="cb459-126">Use the local web UI to change the password</span></span>

<span data-ttu-id="cb459-127">Realice los pasos siguientes para cambiar la contraseña del administrador de dispositivos a través de la interfaz de usuario web local.</span><span class="sxs-lookup"><span data-stu-id="cb459-127">Perform the following steps to change the device administrator password through the local web UI.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a><span data-ttu-id="cb459-128">Para cambiar la contraseña del administrador de dispositivos a través de la interfaz de usuario web local</span><span class="sxs-lookup"><span data-stu-id="cb459-128">To change the device administrator password via the local web UI</span></span>

1. <span data-ttu-id="cb459-129">En la interfaz de usuario web local, haga clic en **Mantenimiento**  >  **Cambio de contraseña** para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cb459-129">In the local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![cambiar password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="cb459-131">Escriba la **Contraseña actual**.</span><span class="sxs-lookup"><span data-stu-id="cb459-131">Enter the **Current password**.</span></span>
3. <span data-ttu-id="cb459-132">Introduzca una **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cb459-132">Provide a **New Password**.</span></span> <span data-ttu-id="cb459-133">La contraseña debe tener al menos 8 caracteres.</span><span class="sxs-lookup"><span data-stu-id="cb459-133">The password must be at least 8 characters long.</span></span> <span data-ttu-id="cb459-134">Debe contener 3 de 4 de los siguientes requisitos: caracteres en mayúsculas, minúsculas, números y caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="cb459-134">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="cb459-135">Tenga en cuenta que la contraseña no puede ser la misma que ninguna de las 24 últimas contraseñas.</span><span class="sxs-lookup"><span data-stu-id="cb459-135">Note that your password cannot be the same as the last 24 passwords.</span></span>
4. <span data-ttu-id="cb459-136">Vuelva a escribir la contraseña para confirmarla.</span><span class="sxs-lookup"><span data-stu-id="cb459-136">Reenter the password to confirm it.</span></span>
   
    ![cambiar password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="cb459-138">En la parte inferior de la página, haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="cb459-138">At the bottom of the page, click **Apply**.</span></span> <span data-ttu-id="cb459-139">Se aplica la nueva contraseña.</span><span class="sxs-lookup"><span data-stu-id="cb459-139">The new password is now applied.</span></span> <span data-ttu-id="cb459-140">Si el cambio de contraseña no se realiza correctamente, aparece el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="cb459-140">If the password change is not successful, you see the following error:</span></span>
   
    ![error de contraseña](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="cb459-142">Después de que la contraseña se haya actualizado correctamente, se le notifica.</span><span class="sxs-lookup"><span data-stu-id="cb459-142">After the password is successfully updated, you are notified.</span></span> <span data-ttu-id="cb459-143">A continuación, puede usar esta contraseña modificada para tener acceso al dispositivo de forma local.</span><span class="sxs-lookup"><span data-stu-id="cb459-143">You can then use this modified password to access the device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cb459-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb459-144">Next steps</span></span>
<span data-ttu-id="cb459-145">Obtenga más información para [administrar la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="cb459-145">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

