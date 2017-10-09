---
title: registros de control de acceso de aaaManage en StorSimple | Documentos de Microsoft
description: "Describe cómo el control de acceso toouse registros toodetermine (ACR) qué hosts pueden conectarse tooa volumen en el dispositivo StorSimple Hola."
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
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="7b065-103">Usar registros de control de acceso de hello StorSimple Manager servicio toomanage</span><span class="sxs-lookup"><span data-stu-id="7b065-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="7b065-104">Información general</span><span class="sxs-lookup"><span data-stu-id="7b065-104">Overview</span></span>
<span data-ttu-id="7b065-105">Registros de control de acceso (ACR) le permiten toospecify qué hosts pueden conectarse tooa volumen en el dispositivo StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="7b065-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="7b065-106">Acr se establecen volumen específico tooa y contener Hola iSCSI (iqn) de nombres completos de los hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b065-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="7b065-107">Cuando un host intenta tooconnect tooa volumen, la comprobación de dispositivo de Hola Hola que ACR asociado a ese volumen para el nombre IQN de Hola y si se encuentra una coincidencia, hello se establezca la conexión.</span><span class="sxs-lookup"><span data-stu-id="7b065-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="7b065-108">Hola registros de control de acceso en hello **configuración** sección de la hoja de servicio del Administrador de dispositivos de StorSimple mostrar todos los registros de control de acceso de hello con hello correspondiente IQN de los hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b065-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="7b065-109">Este tutorial le explica Hola siguientes tareas comunes relacionadas con el ACR:</span><span class="sxs-lookup"><span data-stu-id="7b065-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="7b065-110">Agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="7b065-110">Add an access control record</span></span>
* <span data-ttu-id="7b065-111">Editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="7b065-111">Edit an access control record</span></span>
* <span data-ttu-id="7b065-112">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="7b065-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7b065-113">Al asignar un volumen de tooa ACR, tenga cuidado que volumen hello no es simultáneamente tenga acceso más de un host no agrupado porque esto podría dañar el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b065-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="7b065-114">Al eliminar un ACR de un volumen, asegúrese de que ese host correspondiente hello no se tiene acceso a volumen Hola porque Hola eliminación podría dar lugar a una interrupción de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="7b065-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="7b065-115">Obtener Hola IQN</span><span class="sxs-lookup"><span data-stu-id="7b065-115">Get hello IQN</span></span>

<span data-ttu-id="7b065-116">Realizar Hola siguiendo los pasos tooget Hola IQN de un host de Windows que ejecuta Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="7b065-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="7b065-117">Agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="7b065-117">Add an access control record</span></span>
<span data-ttu-id="7b065-118">Usar hello **configuración** sección en hello Administrador de dispositivos de StorSimple servicio hoja tooadd ACR.</span><span class="sxs-lookup"><span data-stu-id="7b065-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="7b065-119">Normalmente, se asociará un ACR a un volumen.</span><span class="sxs-lookup"><span data-stu-id="7b065-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="7b065-120">Realizar Hola siguiendo los pasos tooadd un ACR.</span><span class="sxs-lookup"><span data-stu-id="7b065-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="7b065-121">tooadd un ACR</span><span class="sxs-lookup"><span data-stu-id="7b065-121">tooadd an ACR</span></span>

1. <span data-ttu-id="7b065-122">Servicio de administrador de dispositivos de StorSimple tooyour go, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, haga clic en **registros de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="7b065-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="7b065-123">Hola **registros de control de acceso** hoja, haga clic en **+ agregar ACR**.</span><span class="sxs-lookup"><span data-stu-id="7b065-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Hacer clic en Agregar ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="7b065-125">Hola **agregar ACR** hoja, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b065-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="7b065-126">Proporcione un Nombre para el ACR.</span><span class="sxs-lookup"><span data-stu-id="7b065-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="7b065-127">Proporcione el nombre IQN de Hola de su host de Windows Server en **iSCSI nombre de iniciador (IQN)**.</span><span class="sxs-lookup"><span data-stu-id="7b065-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="7b065-128">Haga clic en **agregar** toocreate Hola ACR.</span><span class="sxs-lookup"><span data-stu-id="7b065-128">Click **Add** toocreate hello ACR.</span></span>

        ![Hacer clic en Agregar ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="7b065-130">Hola recién agregado que ACR se mostrará en la lista tabular de Hola de ACR.</span><span class="sxs-lookup"><span data-stu-id="7b065-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![Hacer clic en Agregar ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="7b065-132">Editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="7b065-132">Edit an access control record</span></span>
<span data-ttu-id="7b065-133">Usar hello **configuración** sección en hello Administrador de dispositivos de StorSimple servicio hoja tooedit ACR.</span><span class="sxs-lookup"><span data-stu-id="7b065-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="7b065-134">Es recomendable que modifique solo los ACR que no están actualmente en uso.</span><span class="sxs-lookup"><span data-stu-id="7b065-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="7b065-135">tooedit que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.</span><span class="sxs-lookup"><span data-stu-id="7b065-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="7b065-136">Realizar Hola siguiendo los pasos tooedit un ACR.</span><span class="sxs-lookup"><span data-stu-id="7b065-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="7b065-137">tooedit un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="7b065-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="7b065-138">Servicio de administrador de dispositivos de StorSimple tooyour go, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, haga clic en **registros de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="7b065-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="7b065-140">En la lista tabular de Hola de registros de control de acceso de hello, haga clic en y seleccione Hola ACR que desea toomodify.</span><span class="sxs-lookup"><span data-stu-id="7b065-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![Edición de registros de control de acceso](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="7b065-142">Hola **registro de control de acceso de edición** hoja, proporcionar un host distinto de tooanother IQN correspondiente.</span><span class="sxs-lookup"><span data-stu-id="7b065-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![Edición de registros de control de acceso](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="7b065-144">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7b065-144">Click **Save**.</span></span> <span data-ttu-id="7b065-145">Cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="7b065-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Edición de registros de control de acceso](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="7b065-147">Se le notificará cuando se actualiza Hola ACR.</span><span class="sxs-lookup"><span data-stu-id="7b065-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="7b065-148">lista tabular de Hello también actualiza los cambios de hello tooreflect.</span><span class="sxs-lookup"><span data-stu-id="7b065-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="7b065-149">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="7b065-149">Delete an access control record</span></span>
<span data-ttu-id="7b065-150">Usar hello **configuración** sección en hello Administrador de dispositivos de StorSimple servicio hoja toodelete ACR.</span><span class="sxs-lookup"><span data-stu-id="7b065-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="7b065-151">Solo puede eliminar esos ACR que no están actualmente en uso.</span><span class="sxs-lookup"><span data-stu-id="7b065-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="7b065-152">toodelete que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.</span><span class="sxs-lookup"><span data-stu-id="7b065-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="7b065-153">Realizar Hola siguiendo los pasos toodelete un registro de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="7b065-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="7b065-154">toodelete un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="7b065-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="7b065-155">Servicio de administrador de dispositivos de StorSimple tooyour go, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, haga clic en **registros de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="7b065-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="7b065-157">En la lista tabular de Hola de registros de control de acceso de hello, haga clic en y seleccione Hola ACR que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="7b065-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="7b065-159">Haga clic en el menú contextual de tooinvoke hello y seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="7b065-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="7b065-161">Cuando se le pida confirmación, revise la información de hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="7b065-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="7b065-163">Se le notificará cuando se complete la eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b065-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="7b065-164">lista tabular de Hello es tooreflect actualizada Hola eliminación.</span><span class="sxs-lookup"><span data-stu-id="7b065-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="7b065-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b065-166">Next steps</span></span>
* <span data-ttu-id="7b065-167">Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="7b065-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="7b065-168">Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7b065-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

