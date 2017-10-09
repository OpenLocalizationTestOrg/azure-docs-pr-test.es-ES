---
title: aaaDeploy servicio de administrador de dispositivos de StorSimple | Documentos de Microsoft
description: "Explica cómo toocreate y delete Hola servicio Administrador de dispositivos de StorSimple en hello portal de Azure y se describe cómo toomanage Hola clave de registro del servicio."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="9d52b-103">Implementar el servicio de administrador de dispositivos de StorSimple de Hola para StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9d52b-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="9d52b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9d52b-104">Overview</span></span>

<span data-ttu-id="9d52b-105">Hola servicio Administrador de dispositivos de StorSimple se ejecuta en Microsoft Azure y conecta a los dispositivos de StorSimple toomultiple.</span><span class="sxs-lookup"><span data-stu-id="9d52b-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="9d52b-106">Después de crear el servicio de hello, se pueden usar dispositivos de hello toomanage desde Hola Microsoft Azure portal se ejecuta en un explorador.</span><span class="sxs-lookup"><span data-stu-id="9d52b-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="9d52b-107">Esto le permite toomonitor todos los dispositivos de hello toohello conectado el Administrador de dispositivos de StorSimple el servicio desde una única ubicación central, con lo que se minimiza el trabajo administrativo.</span><span class="sxs-lookup"><span data-stu-id="9d52b-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="9d52b-108">Hola comunes tareas relacionadas tooa servicio de administrador de dispositivos de StorSimple son:</span><span class="sxs-lookup"><span data-stu-id="9d52b-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="9d52b-109">Crear un servicio</span><span class="sxs-lookup"><span data-stu-id="9d52b-109">Create a service</span></span>
* <span data-ttu-id="9d52b-110">Eliminar un servicio</span><span class="sxs-lookup"><span data-stu-id="9d52b-110">Delete a service</span></span>
* <span data-ttu-id="9d52b-111">Obtener clave de registro del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="9d52b-111">Get hello service registration key</span></span>
* <span data-ttu-id="9d52b-112">Regenerar la clave de registro del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="9d52b-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="9d52b-113">Este tutorial describe cómo tooperform de Hola tareas anteriores.</span><span class="sxs-lookup"><span data-stu-id="9d52b-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="9d52b-114">información de Hello contenida en este artículo es aplicable únicamente tooStorSimple Virtual las matrices.</span><span class="sxs-lookup"><span data-stu-id="9d52b-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="9d52b-115">Para obtener más información acerca de la serie StorSimple 8000, vaya demasiado[implementar un servicio de StorSimple Manager](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="9d52b-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="9d52b-116">Crear un servicio</span><span class="sxs-lookup"><span data-stu-id="9d52b-116">Create a service</span></span>

<span data-ttu-id="9d52b-117">toocreate un servicio, necesita toohave:</span><span class="sxs-lookup"><span data-stu-id="9d52b-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="9d52b-118">Una suscripción con un contrato Enterprise</span><span class="sxs-lookup"><span data-stu-id="9d52b-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="9d52b-119">Una cuenta de Almacenamiento de Microsoft Azure activa.</span><span class="sxs-lookup"><span data-stu-id="9d52b-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="9d52b-120">Hola información de facturación que se usa para la administración de acceso</span><span class="sxs-lookup"><span data-stu-id="9d52b-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="9d52b-121">También puede elegir toogenerate en una cuenta de almacenamiento al crear el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d52b-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="9d52b-122">Un único servicio puede administrar varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9d52b-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="9d52b-123">Sin embargo, un dispositivo no puede abarcar varios servicios.</span><span class="sxs-lookup"><span data-stu-id="9d52b-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="9d52b-124">Una gran empresa puede tener varios toowork de instancias de servicio con distintas suscripciones, organizaciones o incluso regiones de implementación.</span><span class="sxs-lookup"><span data-stu-id="9d52b-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="9d52b-125">Necesita instancias independientes de los dispositivos serie 8000 de StorSimple toomanage del servicio de administrador de dispositivos de StorSimple y arreglos de discos virtuales de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d52b-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="9d52b-126">Realizar Hola siguiendo los pasos toocreate un servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="9d52b-127">Eliminar un servicio</span><span class="sxs-lookup"><span data-stu-id="9d52b-127">Delete a service</span></span>

<span data-ttu-id="9d52b-128">Antes de eliminar un servicio, asegúrese de que no lo esté utilizando ningún dispositivo conectado.</span><span class="sxs-lookup"><span data-stu-id="9d52b-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="9d52b-129">Si el servicio de hello está en uso, desactive los dispositivos de hello conectado.</span><span class="sxs-lookup"><span data-stu-id="9d52b-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="9d52b-130">Hola desactivar la operación se Hola conexión entre el dispositivo de Hola y el servicio de hello, pero conserva los datos del dispositivo hello en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d52b-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d52b-131">Después de elimina un servicio, no se puede revertir la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d52b-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="9d52b-132">Cualquier dispositivo que estaba utilizando el servicio de hello deberá toobe antes de que se puede utilizar con otro servicio de restablecimiento de fábrica.</span><span class="sxs-lookup"><span data-stu-id="9d52b-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="9d52b-133">En este escenario, los datos locales de hello en dispositivo hello, así como la configuración de hello, se perderán.</span><span class="sxs-lookup"><span data-stu-id="9d52b-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="9d52b-134">Realizar Hola siguiendo los pasos toodelete un servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="9d52b-135">toodelete un servicio</span><span class="sxs-lookup"><span data-stu-id="9d52b-135">toodelete a service</span></span>

1. <span data-ttu-id="9d52b-136">Vaya demasiado**todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="9d52b-136">Go too**All resources**.</span></span> <span data-ttu-id="9d52b-137">Busque el servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="9d52b-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="9d52b-138">Seleccione servicio de Hola que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="9d52b-138">Select hello service that you wish toodelete.</span></span>
   
    ![Seleccione toodelete de servicio](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="9d52b-140">Vaya tooyour servicio panel tooensure no hay ningún dispositivo conectado toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="9d52b-141">Si no hay ningún dispositivo registrado con este servicio, también verá un efecto de toohello de mensaje de pancarta.</span><span class="sxs-lookup"><span data-stu-id="9d52b-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="9d52b-142">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9d52b-142">Click **Delete**.</span></span>
   
    ![Eliminar servicio](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="9d52b-144">Cuando se le solicite confirmación, haga clic en **Sí** en la notificación de confirmación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d52b-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![Confirmación de la eliminación del servicio](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="9d52b-146">Puede tardar unos minutos para hello servicio toobe eliminado.</span><span class="sxs-lookup"><span data-stu-id="9d52b-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="9d52b-147">Después de hello servicio se elimina correctamente, se le notificará.</span><span class="sxs-lookup"><span data-stu-id="9d52b-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![Eliminación del servicio correcta](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="9d52b-149">se actualizará la lista de Hello de servicios.</span><span class="sxs-lookup"><span data-stu-id="9d52b-149">hello list of services will be refreshed.</span></span>

 ![Lista de servicios actualizada](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="9d52b-151">Obtener clave de registro del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="9d52b-151">Get hello service registration key</span></span>
<span data-ttu-id="9d52b-152">Después de haber creado correctamente un servicio, deberá tooregister el dispositivo StorSimple con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d52b-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="9d52b-153">tooregister el primer dispositivo de StorSimple, se necesita Hola clave de registro del servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="9d52b-154">tooregister dispositivos adicionales con un servicio existente de StorSimple, necesitará la clave de registro de hello y clave de cifrado de datos de servicio de hello (que se genera en el primer dispositivo de Hola durante el registro).</span><span class="sxs-lookup"><span data-stu-id="9d52b-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="9d52b-155">Para obtener más información acerca de la clave de cifrado de datos del servicio de hello, consulte [seguridad de StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="9d52b-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="9d52b-156">Puede obtener clave de registro de hello accediendo hello **claves** hoja para el servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="9d52b-157">Realizar Hola después de la clave de registro del servicio de pasos tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="9d52b-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="9d52b-158">clave de registro del servicio de tooget Hola</span><span class="sxs-lookup"><span data-stu-id="9d52b-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="9d52b-159">Hola **el Administrador de dispositivos de StorSimple** hoja, vaya demasiado**administración &gt;**  **claves**.</span><span class="sxs-lookup"><span data-stu-id="9d52b-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Hoja de claves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="9d52b-161">Hola **claves** blade, se muestra una clave de registro del servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="9d52b-162">Copie la clave de registro de hello mediante el icono de copiar Hola.</span><span class="sxs-lookup"><span data-stu-id="9d52b-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="9d52b-163">Mantenga la clave de registro del servicio de hello en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="9d52b-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="9d52b-164">Necesitará esta clave, así como clave de cifrado de datos del servicio de hello, tooregister dispositivos adicionales con este servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="9d52b-165">Después de obtener la clave de registro del servicio de hello, necesitará tooconfigure el dispositivo a través de hello Windows PowerShell para StorSimple interfaz.</span><span class="sxs-lookup"><span data-stu-id="9d52b-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="9d52b-166">Regenerar la clave de registro del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="9d52b-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="9d52b-167">Necesitará una clave de registro del servicio de tooregenerate si es necesario tooperform rotación de claves o si ha cambiado la lista de Hola de administradores de servicios.</span><span class="sxs-lookup"><span data-stu-id="9d52b-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="9d52b-168">Cuando vuelva a generar clave de hello, nueva clave de Hola se usa solo para registrar dispositivos subsiguientes.</span><span class="sxs-lookup"><span data-stu-id="9d52b-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="9d52b-169">dispositivos de Hola que ya estaban registrados no se ven afectados por este proceso.</span><span class="sxs-lookup"><span data-stu-id="9d52b-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="9d52b-170">Realizar Hola siguiendo los pasos tooregenerate una clave de registro del servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="9d52b-171">clave de registro del servicio de tooregenerate Hola</span><span class="sxs-lookup"><span data-stu-id="9d52b-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="9d52b-172">Hola **el Administrador de dispositivos de StorSimple** hoja, vaya demasiado**administración &gt;**  **claves**.</span><span class="sxs-lookup"><span data-stu-id="9d52b-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Hoja de claves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="9d52b-174">Hola **claves** hoja, haga clic en **regenerar**.</span><span class="sxs-lookup"><span data-stu-id="9d52b-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![Haga clic en Regenerar](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="9d52b-176">Hola **Regenerar clave de registro** hoja, revisión Hola requiere una acción cuando hello se vuelven a generar las claves.</span><span class="sxs-lookup"><span data-stu-id="9d52b-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="9d52b-177">Todos los dispositivos subsiguientes Hola que están registrados con este servicio usará la nueva clave de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9d52b-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="9d52b-178">Haga clic en **regenerar** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="9d52b-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="9d52b-179">Se le notificará una vez completado el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9d52b-179">You will be notified after hello registration is complete.</span></span>
   
   ![Confirmación de la clave regenerada](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="9d52b-181">Aparecerá una nueva clave de registro de servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-181">A new service registration key will appear.</span></span>
   
    ![Confirmación de la clave regenerada](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="9d52b-183">Copie esta clave y guárdela para registrar los dispositivos nuevos con este servicio.</span><span class="sxs-lookup"><span data-stu-id="9d52b-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d52b-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d52b-184">Next steps</span></span>
* <span data-ttu-id="9d52b-185">Obtenga información acerca de cómo demasiado[Introducción](storsimple-virtual-array-deploy1-portal-prep.md) con una matriz Virtual de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d52b-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="9d52b-186">Obtenga información acerca de cómo demasiado[administrar el dispositivo StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="9d52b-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

