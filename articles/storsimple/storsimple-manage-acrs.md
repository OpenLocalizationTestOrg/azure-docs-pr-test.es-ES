---
title: registros de control de acceso de aaaManage en StorSimple | Documentos de Microsoft
description: "Describe cómo el control de acceso toouse registros toodetermine (ACR) qué hosts pueden conectarse tooa volumen en el dispositivo StorSimple Hola."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="47298-103">Usar registros de control de acceso de hello StorSimple Manager servicio toomanage</span><span class="sxs-lookup"><span data-stu-id="47298-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="47298-104">Información general</span><span class="sxs-lookup"><span data-stu-id="47298-104">Overview</span></span>
<span data-ttu-id="47298-105">Registros de control de acceso (ACR) le permiten toospecify qué hosts pueden conectarse tooa volumen en el dispositivo StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="47298-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="47298-106">Acr se establecen volumen específico tooa y contener Hola iSCSI (iqn) de nombres completos de los hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="47298-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="47298-107">Cuando un host intenta tooconnect tooa volumen, la comprobación de dispositivo de Hola Hola que ACR asociado a ese volumen para el nombre IQN de Hola y si se encuentra una coincidencia, hello se establezca la conexión.</span><span class="sxs-lookup"><span data-stu-id="47298-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="47298-108">registros de control de acceso de Hello sección en hello **configurar** página muestra todos los registros de control de acceso de hello con hello correspondiente IQN de los hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="47298-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="47298-109">Este tutorial le explica Hola siguientes tareas comunes relacionadas con el ACR:</span><span class="sxs-lookup"><span data-stu-id="47298-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="47298-110">Agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="47298-110">Add an access control record</span></span> 
* <span data-ttu-id="47298-111">Editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="47298-111">Edit an access control record</span></span> 
* <span data-ttu-id="47298-112">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="47298-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="47298-113">Al asignar un volumen de tooa ACR, tenga cuidado que volumen hello no es simultáneamente tenga acceso más de un host no agrupado porque esto podría dañar el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="47298-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="47298-114">Al eliminar un ACR de un volumen, asegúrese de que ese host correspondiente hello no se tiene acceso a volumen Hola porque Hola eliminación podría dar lugar a una interrupción de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="47298-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="47298-115">Agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="47298-115">Add an access control record</span></span>
<span data-ttu-id="47298-116">Usar el servicio StorSimple Manager hello **configurar** página tooadd ACR.</span><span class="sxs-lookup"><span data-stu-id="47298-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="47298-117">Normalmente, se asociará un ACR a un volumen.</span><span class="sxs-lookup"><span data-stu-id="47298-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="47298-118">Realizar Hola siguiendo los pasos tooadd un ACR.</span><span class="sxs-lookup"><span data-stu-id="47298-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="47298-119">tooadd un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="47298-119">tooadd an access control record</span></span>
1. <span data-ttu-id="47298-120">En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic en el nombre del servicio de hello y, a continuación, haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="47298-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="47298-121">Hola tabular listado en **registros de control de acceso**, proporcione un **nombre** para el ACR.</span><span class="sxs-lookup"><span data-stu-id="47298-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="47298-122">Proporcione el nombre IQN de Hola de su host de Windows en **nombre del iniciador iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="47298-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="47298-123">Hola tooget IQN del host Windows Server, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="47298-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="47298-124">Inicie el iniciador iSCSI de Microsoft de hello en el host de Windows.</span><span class="sxs-lookup"><span data-stu-id="47298-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="47298-125">Hola **propiedades del iniciador iSCSI** ventana hello **configuración** ficha, seleccione y copie cadena Hola de hello **nombre del iniciador** campo.</span><span class="sxs-lookup"><span data-stu-id="47298-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="47298-126">Pegue esta cadena en hello **nombre del iniciador iSCSI** campo en la tabla de ACR Hola Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="47298-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="47298-127">Haga clic en **guardar** hello toosave recién creado ACR.</span><span class="sxs-lookup"><span data-stu-id="47298-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="47298-128">Hola tabular enumerar will ser tooreflect actualizado esta adición.</span><span class="sxs-lookup"><span data-stu-id="47298-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="47298-129">Editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="47298-129">Edit an access control record</span></span>
<span data-ttu-id="47298-130">Usar hello **configurar** página Hola ACR Azure tooedit portal clásico.</span><span class="sxs-lookup"><span data-stu-id="47298-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="47298-131">Puede modificar solo esos ACR que no están actualmente en uso.</span><span class="sxs-lookup"><span data-stu-id="47298-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="47298-132">tooedit que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.</span><span class="sxs-lookup"><span data-stu-id="47298-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="47298-133">Realizar Hola siguiendo los pasos tooedit un ACR.</span><span class="sxs-lookup"><span data-stu-id="47298-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="47298-134">tooedit un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="47298-134">tooedit an access control record</span></span>
1. <span data-ttu-id="47298-135">En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic en el nombre del servicio de hello y, a continuación, haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="47298-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="47298-136">En la lista tabular de Hola de registros de control de acceso de hello, mantenga el mouse sobre Hola ACR que desea toomodify.</span><span class="sxs-lookup"><span data-stu-id="47298-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="47298-137">Proporcione un nombre nuevo o el IQN de hello ACR.</span><span class="sxs-lookup"><span data-stu-id="47298-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="47298-138">Haga clic en **guardar** toosave Hola modificado el ACR.</span><span class="sxs-lookup"><span data-stu-id="47298-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="47298-139">Hola tabular enumerar will ser tooreflect actualizado este cambio.</span><span class="sxs-lookup"><span data-stu-id="47298-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="47298-140">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="47298-140">Delete an access control record</span></span>
<span data-ttu-id="47298-141">Usar hello **configurar** página Hola ACR Azure toodelete portal clásico.</span><span class="sxs-lookup"><span data-stu-id="47298-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="47298-142">Solo puede eliminar esos ACR que no están actualmente en uso.</span><span class="sxs-lookup"><span data-stu-id="47298-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="47298-143">toodelete que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.</span><span class="sxs-lookup"><span data-stu-id="47298-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="47298-144">Realizar Hola siguiendo los pasos toodelete un registro de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="47298-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="47298-145">toodelete un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="47298-145">toodelete an access control record</span></span>
1. <span data-ttu-id="47298-146">En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic en el nombre del servicio de hello y, a continuación, haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="47298-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="47298-147">En la lista tabular de Hola de registros de control de acceso (ACR) de hello, mantenga el mouse sobre Hola ACR que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="47298-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="47298-148">Un icono de eliminación (**x**) aparecerá en hello la columna extrema derecha para hello ACR que seleccione.</span><span class="sxs-lookup"><span data-stu-id="47298-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="47298-149">Haga clic en hello **x** Hola de icono toodelete ACR.</span><span class="sxs-lookup"><span data-stu-id="47298-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="47298-150">Cuando se le solicite confirmación, haga clic en **Sí** toocontinue con eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="47298-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="47298-151">lista tabular de Hello estará actualizada tooreflect Hola eliminación.</span><span class="sxs-lookup"><span data-stu-id="47298-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47298-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="47298-152">Next steps</span></span>
* <span data-ttu-id="47298-153">Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="47298-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="47298-154">Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="47298-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

