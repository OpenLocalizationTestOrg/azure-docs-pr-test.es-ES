---
title: "Implementación del servicio StorSimple Device Manager | Microsoft Docs"
description: "Aquí encontrará información acerca de cómo crear y eliminar el servicio StorSimple Device Manager en Azure Portal, así como una descripción acerca de cómo administrar la clave de registro del servicio."
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
ms.openlocfilehash: 1881a0625b107ae1a90e5b772f5296a4d728973d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="edb44-103">Implementación del servicio StorSimple Device Manager en una instancia de StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="edb44-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="edb44-104">Información general</span><span class="sxs-lookup"><span data-stu-id="edb44-104">Overview</span></span>

<span data-ttu-id="edb44-105">El servicio StorSimple Device Manager se ejecuta en Microsoft Azure y se conecta a varios dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="edb44-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="edb44-106">Después de crear el servicio, puede usarlo para administrar los dispositivos desde el Portal de Microsoft Azure, ejecutándolo en un explorador.</span><span class="sxs-lookup"><span data-stu-id="edb44-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="edb44-107">Esto permite supervisar todos los dispositivos que están conectados al servicio StorSimple Device Manager desde una única ubicación central, reduciendo la carga administrativa.</span><span class="sxs-lookup"><span data-stu-id="edb44-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="edb44-108">Las tareas comunes relacionadas con un servicio StorSimple Device Manager son:</span><span class="sxs-lookup"><span data-stu-id="edb44-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="edb44-109">Crear un servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-109">Create a service</span></span>
* <span data-ttu-id="edb44-110">Eliminar un servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-110">Delete a service</span></span>
* <span data-ttu-id="edb44-111">Obtener la clave de registro del servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-111">Get the service registration key</span></span>
* <span data-ttu-id="edb44-112">Volver a generar la clave de registro de servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-112">Regenerate the service registration key</span></span>

<span data-ttu-id="edb44-113">Este tutorial describe cómo realizar cada una de las tareas anteriores.</span><span class="sxs-lookup"><span data-stu-id="edb44-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="edb44-114">La información contenida en este artículo se aplica solo a las matrices virtuales de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="edb44-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="edb44-115">Para más información acerca de la serie 8000 de StorSimple, vaya a [Implementar el servicio StorSimple Manager](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="edb44-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="edb44-116">Crear un servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-116">Create a service</span></span>

<span data-ttu-id="edb44-117">Para crear un servicio, debe tener:</span><span class="sxs-lookup"><span data-stu-id="edb44-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="edb44-118">Una suscripción con un contrato Enterprise</span><span class="sxs-lookup"><span data-stu-id="edb44-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="edb44-119">Una cuenta de Almacenamiento de Microsoft Azure activa.</span><span class="sxs-lookup"><span data-stu-id="edb44-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="edb44-120">La información de facturación que se usa para la administración de acceso</span><span class="sxs-lookup"><span data-stu-id="edb44-120">The billing information that is used for access management</span></span>

<span data-ttu-id="edb44-121">También puede generar una cuenta de almacenamiento al crear el servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="edb44-122">Un único servicio puede administrar varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="edb44-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="edb44-123">Sin embargo, un dispositivo no puede abarcar varios servicios.</span><span class="sxs-lookup"><span data-stu-id="edb44-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="edb44-124">Una gran empresa puede tener varias instancias de servicio para trabajar con distintas suscripciones, organizaciones o incluso las ubicaciones de implementación.</span><span class="sxs-lookup"><span data-stu-id="edb44-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="edb44-125">Necesita instancias separadas del servicio StorSimple Device Manager para administrar instancias de StorSimple Virtual Array y dispositivos de StorSimple de la serie 8000.</span><span class="sxs-lookup"><span data-stu-id="edb44-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="edb44-126">Realice los siguientes pasos para crear un servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="edb44-127">Eliminar un servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-127">Delete a service</span></span>

<span data-ttu-id="edb44-128">Antes de eliminar un servicio, asegúrese de que no lo esté utilizando ningún dispositivo conectado.</span><span class="sxs-lookup"><span data-stu-id="edb44-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="edb44-129">Si se está utilizando el servicio, desactive los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="edb44-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="edb44-130">La operación de desactivación eliminará la conexión entre el dispositivo y el servicio, pero conservará los datos del dispositivo en la nube.</span><span class="sxs-lookup"><span data-stu-id="edb44-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="edb44-131">Después de eliminar un servicio, no se puede revertir la operación.</span><span class="sxs-lookup"><span data-stu-id="edb44-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="edb44-132">Cualquier dispositivo que estaba utilizando el servicio deberá restablecerse a los valores de fábrica para que pueda ser usado con otro servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="edb44-133">En este escenario, se perderán los datos locales del dispositivo, así como la configuración.</span><span class="sxs-lookup"><span data-stu-id="edb44-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="edb44-134">Realice los siguientes pasos para eliminar un servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="edb44-135">Para eliminar un servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-135">To delete a service</span></span>

1. <span data-ttu-id="edb44-136">Vaya a **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="edb44-136">Go to **All resources**.</span></span> <span data-ttu-id="edb44-137">Busque el servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="edb44-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="edb44-138">Seleccione el servicio que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="edb44-138">Select the service that you wish to delete.</span></span>
   
    ![Selección del servicio que se eliminará](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="edb44-140">Vaya al panel de servicio para asegurarse de que no hay ningún dispositivo conectado al servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="edb44-141">Si no hay ningún dispositivo registrado en este servicio, también verá un mensaje en un banner que lo indica.</span><span class="sxs-lookup"><span data-stu-id="edb44-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="edb44-142">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="edb44-142">Click **Delete**.</span></span>
   
    ![Eliminar servicio](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="edb44-144">Cuando se le solicite confirmación, haga clic en **Sí** en la notificación de confirmación.</span><span class="sxs-lookup"><span data-stu-id="edb44-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![Confirmación de la eliminación del servicio](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="edb44-146">Es posible que el servicio tarde unos minutos en eliminarse.</span><span class="sxs-lookup"><span data-stu-id="edb44-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="edb44-147">Recibirá una notificación apropiada cuando el servicio se elimine correctamente.</span><span class="sxs-lookup"><span data-stu-id="edb44-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![Eliminación del servicio correcta](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="edb44-149">Se actualizará la lista de servicios.</span><span class="sxs-lookup"><span data-stu-id="edb44-149">The list of services will be refreshed.</span></span>

 ![Lista de servicios actualizada](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="edb44-151">Obtener la clave de registro del servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-151">Get the service registration key</span></span>
<span data-ttu-id="edb44-152">Después de haber creado correctamente un servicio, deberá registrar el dispositivo StorSimple con el servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="edb44-153">Para registrar el primer dispositivo StorSimple, necesitará la clave de registro del servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="edb44-154">Para registrar dispositivos adicionales con un servicio existente StorSimple, necesitará la clave de registro y la clave de cifrado de datos de servicio (que se genera en el primer dispositivo durante el registro).</span><span class="sxs-lookup"><span data-stu-id="edb44-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="edb44-155">Para obtener más información acerca de la clave de cifrado de datos de servicio, consulte [Seguridad de StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="edb44-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="edb44-156">Para obtener la clave de registro, acceda a la hoja **Claves** para el servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="edb44-157">Realice los pasos siguientes para obtener la clave de registro del servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="edb44-158">Para obtener la clave de registro del servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-158">To get the service registration key</span></span>
1. <span data-ttu-id="edb44-159">En la hoja **StorSimple Device Manager**, vaya a **Administración &gt;** **Claves**.</span><span class="sxs-lookup"><span data-stu-id="edb44-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Hoja de claves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="edb44-161">En la hoja **Claves** se muestra una clave de registro del servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="edb44-162">Copie la clave de registro mediante el icono de copia.</span><span class="sxs-lookup"><span data-stu-id="edb44-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="edb44-163">Mantenga la clave de registro del servicio en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="edb44-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="edb44-164">Necesitará esta clave, así como la clave de cifrado de datos de servicio para registrar dispositivos adicionales con este servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="edb44-165">Después de obtener la clave de registro del servicio, deberá configurar el dispositivo a través de la interfaz de Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="edb44-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="edb44-166">Volver a generar la clave de registro de servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-166">Regenerate the service registration key</span></span>
<span data-ttu-id="edb44-167">Será necesario volver a generar una clave de registro del servicio si es necesario para realizar la rotación de claves o si ha cambiado la lista de administradores de servicios.</span><span class="sxs-lookup"><span data-stu-id="edb44-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="edb44-168">Cuando se regenera la clave, la nueva clave se utiliza solo para registrar dispositivos posteriores.</span><span class="sxs-lookup"><span data-stu-id="edb44-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="edb44-169">Los dispositivos que ya se han registrado no se ven afectados por este proceso.</span><span class="sxs-lookup"><span data-stu-id="edb44-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="edb44-170">Realice los pasos siguientes para volver a generar una clave de registro de servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="edb44-171">Para volver a generar la clave de registro de servicio</span><span class="sxs-lookup"><span data-stu-id="edb44-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="edb44-172">En la hoja **StorSimple Device Manager**, vaya a **Administración &gt;** **Claves**.</span><span class="sxs-lookup"><span data-stu-id="edb44-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Hoja de claves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="edb44-174">En la hoja **Claves**, haga clic en **Regenerar**.</span><span class="sxs-lookup"><span data-stu-id="edb44-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![Haga clic en Regenerar](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="edb44-176">En la hoja **Regenerar clave de registro del servicio**, revise la acción necesaria cuando se regeneren las claves.</span><span class="sxs-lookup"><span data-stu-id="edb44-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="edb44-177">Todos los dispositivos posteriores que están registrados en este servicio usará la nueva clave del registro.</span><span class="sxs-lookup"><span data-stu-id="edb44-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="edb44-178">Haga clic en **Regenerar** para confirmarlo.</span><span class="sxs-lookup"><span data-stu-id="edb44-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="edb44-179">Se le notificará una vez completado el registro.</span><span class="sxs-lookup"><span data-stu-id="edb44-179">You will be notified after the registration is complete.</span></span>
   
   ![Confirmación de la clave regenerada](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="edb44-181">Aparecerá una nueva clave de registro de servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-181">A new service registration key will appear.</span></span>
   
    ![Confirmación de la clave regenerada](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="edb44-183">Copie esta clave y guárdela para registrar los dispositivos nuevos con este servicio.</span><span class="sxs-lookup"><span data-stu-id="edb44-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edb44-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="edb44-184">Next steps</span></span>
* <span data-ttu-id="edb44-185">Lea una [introducción](storsimple-virtual-array-deploy1-portal-prep.md) a StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="edb44-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="edb44-186">Obtenga información sobre cómo [administrar el dispositivo StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="edb44-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

