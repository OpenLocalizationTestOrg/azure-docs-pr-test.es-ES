---
title: registros de control de acceso de aaaManage para StorSimple Virtual Array | Documentos de Microsoft
description: "Describe cómo el control de acceso toomanage registros toodetermine (ACR) qué hosts pueden conectarse tooa volumen hello StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="a2e3a-103">Use el Administrador de dispositivos de StorSimple toomanage registros de control de acceso para StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="a2e3a-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="a2e3a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a2e3a-104">Overview</span></span>

<span data-ttu-id="a2e3a-105">Registros de control de acceso (ACR) le permiten toospecify qué hosts pueden conectarse tooa volumen hello StorSimple Virtual Array (también conocido como hello StorSimple en dispositivo virtual local).</span><span class="sxs-lookup"><span data-stu-id="a2e3a-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="a2e3a-106">Acr se establecen volumen específico tooa y contener Hola iSCSI (iqn) de nombres completos de los hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="a2e3a-107">Cuando un host intenta tooconnect tooa volumen, dispositivo Hola comprueba Hola ACR asociado a ese volumen para el nombre IQN de hello y, si hay una coincidencia, se establece conexión Hola.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="a2e3a-108">Hola **registros de control de acceso** hoja dentro de hello **configuración** sección de su servicio de administrador de dispositivos muestra todos los registros de control de acceso de hello con hello correspondiente IQN de los hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![Administrar registros de control de acceso](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="a2e3a-110">Este tutorial le explica Hola siguientes tareas comunes relacionadas con el ACR:</span><span class="sxs-lookup"><span data-stu-id="a2e3a-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="a2e3a-111">Obtener Hola IQN</span><span class="sxs-lookup"><span data-stu-id="a2e3a-111">Get hello IQN</span></span>
* <span data-ttu-id="a2e3a-112">Agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="a2e3a-112">Add an access control record</span></span>
* <span data-ttu-id="a2e3a-113">Editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="a2e3a-113">Edit an access control record</span></span>
* <span data-ttu-id="a2e3a-114">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="a2e3a-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="a2e3a-115">Al asignar un volumen de tooa ACR, tenga cuidado que volumen hello no es simultáneamente tenga acceso más de un host no agrupado porque esto podría dañar el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="a2e3a-116">Al eliminar un ACR de un volumen, asegúrese de que ese host correspondiente hello no se tiene acceso a volumen Hola porque Hola eliminación podría dar lugar a una interrupción de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="a2e3a-117">Obtener Hola IQN</span><span class="sxs-lookup"><span data-stu-id="a2e3a-117">Get hello IQN</span></span>

<span data-ttu-id="a2e3a-118">Realizar Hola siguiendo los pasos tooget Hola IQN de un host de Windows que ejecuta Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="a2e3a-119">Adición de ACR</span><span class="sxs-lookup"><span data-stu-id="a2e3a-119">Add an ACR</span></span>

<span data-ttu-id="a2e3a-120">Usa **registros de control de acceso** hoja dentro de hello **configuración** sección de su tooadd de servicio de administrador de dispositivos de StorSimple ACR.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="a2e3a-121">Normalmente, se asociará un ACR a un volumen.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="a2e3a-122">Para obtener información sobre cómo asociar un ACR a un volumen, consulte demasiado[agregar un volumen](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="a2e3a-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2e3a-123">Al asignar un volumen de tooa ACR, tenga cuidado que volumen hello no es simultáneamente tenga acceso más de un host no agrupado porque esto podría dañar el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="a2e3a-124">Realizar Hola siguiendo los pasos tooadd un ACR.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="a2e3a-125">tooadd un ACR</span><span class="sxs-lookup"><span data-stu-id="a2e3a-125">tooadd an ACR</span></span>

1. <span data-ttu-id="a2e3a-126">En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, haga clic en **registros de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="a2e3a-127">Hola **registros de control de acceso** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="a2e3a-128">Hola **agregar ACR** hoja, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a2e3a-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="a2e3a-129">Proporcione un **Nombre** para el ACR.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="a2e3a-130">En **nombre del iniciador iSCSI**, proporcione el nombre IQN de Hola de su host de Windows.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="a2e3a-131">Hola tooget IQN del host Windows Server, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a2e3a-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="a2e3a-132">Inicie el iniciador iSCSI de Microsoft de hello en el host de Windows.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="a2e3a-133">En la ventana de propiedades del iniciador de iSCSI de hello en hello **configuración** ficha, seleccione y copie cadena Hola de hello **nombre del iniciador** campo.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="a2e3a-134">Pegue esta cadena en hello **IQN** campo hello **agregar ACR** hoja.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="a2e3a-135">Haga clic en **agregar** tooadd Hola ACR.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![Incorporación de registros de control de acceso](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="a2e3a-137">Hola lista tabular es tooreflect actualizado esta adición.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="a2e3a-138">Edición de un ACR</span><span class="sxs-lookup"><span data-stu-id="a2e3a-138">Edit an ACR</span></span>

<span data-ttu-id="a2e3a-139">Usar hello **registros de control de acceso** hoja dentro de hello **configuración** sección de su servicio de administrador de dispositivos en hello ACR tooedit de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="a2e3a-140">No debe modificar un ACR que esté en uso.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="a2e3a-141">tooedit que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="a2e3a-142">Realizar Hola siguiendo los pasos tooedit un ACR.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="a2e3a-143">tooedit un ACR</span><span class="sxs-lookup"><span data-stu-id="a2e3a-143">tooedit an ACR</span></span>

1. <span data-ttu-id="a2e3a-144">En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, **registros de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="a2e3a-145">Hola **registros de control de acceso** hoja, de la lista tabular de Hola de registros de control de acceso de hello, haga doble clic en hello ACR que desea toomodify.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="a2e3a-146">Hola **registros de control de acceso de edición** hoja, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a2e3a-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="a2e3a-147">Fuente de alimentación hello IQN de hello ACR.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="a2e3a-148">Haga clic en **guardar** en parte superior de Hola de hello hoja toosave Hola modificado el ACR.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="a2e3a-149">Vea Hola siguiente mensaje de confirmación:</span><span class="sxs-lookup"><span data-stu-id="a2e3a-149">You see hello following confirmation message:</span></span>
   
        ![Edición de registros de control de acceso](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="a2e3a-151">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="a2e3a-151">Delete an access control record</span></span>

<span data-ttu-id="a2e3a-152">Usar hello **configuración** página Hola ACR toodelete de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="a2e3a-153">No debe eliminar un ACR que esté en uso.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="a2e3a-154">toodelete que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="a2e3a-155">Al eliminar un ACR de un volumen, asegúrese de que ese host correspondiente hello no se tiene acceso a volumen Hola porque Hola eliminación podría dar lugar a una interrupción de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="a2e3a-156">Realizar Hola siguiendo los pasos toodelete un registro de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="a2e3a-157">toodelete un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="a2e3a-157">toodelete an access control record</span></span>

1. <span data-ttu-id="a2e3a-158">En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, **registros de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="a2e3a-159">Hola **registros de control de acceso** hoja, de la lista tabular de Hola de registros de control de acceso de hello, haga doble clic en hello ACR que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="a2e3a-160">En la hoja de registros de control de acceso de hello editar, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![Eliminación de ACR](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="a2e3a-162">Cuando se le solicite confirmación, haga clic en **eliminar** toocontinue con eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="a2e3a-163">lista tabular de Hello es tooreflect actualizada Hola eliminación.</span><span class="sxs-lookup"><span data-stu-id="a2e3a-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![Mensaje de advertencia](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="a2e3a-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2e3a-165">Next steps</span></span>

* <span data-ttu-id="a2e3a-166">Obtenga más información sobre la [adición de volúmenes y la configuración de ACR](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="a2e3a-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

