---
title: "Administración de los registros de control de acceso en StorSimple | Microsoft Docs"
description: "Describe cómo utilizar los registros de control de acceso (ACR) para determinar qué hosts pueden conectarse a un volumen en el dispositivo StorSimple."
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
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="4913f-103">Usar el servicio de Administrador de StorSimple para administrar registros de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="4913f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4913f-104">Overview</span></span>
<span data-ttu-id="4913f-105">Los registros de control de acceso (ACR) le permiten especificar qué hosts pueden conectarse a un volumen del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4913f-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="4913f-106">Los ACR se establecen en un volumen específico y contienen los nombres calificados iSCSI (IQNs) de los hosts.</span><span class="sxs-lookup"><span data-stu-id="4913f-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="4913f-107">Cuando un host intenta conectarse a un volumen, el dispositivo comprueba el ACR asociado a ese volumen para el nombre IQN y, a continuación, si hay una coincidencia, se establece la conexión.</span><span class="sxs-lookup"><span data-stu-id="4913f-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="4913f-108">La sección de registros de control de acceso de la página **Configurar** muestra todos los registros de control de acceso con los IQN correspondientes de los hosts.</span><span class="sxs-lookup"><span data-stu-id="4913f-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="4913f-109">Este tutorial explica las siguientes tareas comunes relacionadas con los ACR comunes:</span><span class="sxs-lookup"><span data-stu-id="4913f-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="4913f-110">Agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-110">Add an access control record</span></span> 
* <span data-ttu-id="4913f-111">Editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-111">Edit an access control record</span></span> 
* <span data-ttu-id="4913f-112">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="4913f-113">Al asignar un ACR a un volumen, tenga cuidado de que no accedan al mismo tiempo al volumen más de un host no agrupado porque esto podría dañar el volumen.</span><span class="sxs-lookup"><span data-stu-id="4913f-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="4913f-114">Al eliminar un ACR de un volumen, asegúrese de que el host correspondiente no tiene acceso al volumen porque la eliminación podría dar lugar a una interrupción de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="4913f-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="4913f-115">Agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-115">Add an access control record</span></span>
<span data-ttu-id="4913f-116">Use la página **Configurar** del servicio Administrador de StorSimple para agregar ACR.</span><span class="sxs-lookup"><span data-stu-id="4913f-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="4913f-117">Normalmente, se asociará un ACR a un volumen.</span><span class="sxs-lookup"><span data-stu-id="4913f-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="4913f-118">Realice los pasos siguientes para agregar un ACR.</span><span class="sxs-lookup"><span data-stu-id="4913f-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="4913f-119">Para agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-119">To add an access control record</span></span>
1. <span data-ttu-id="4913f-120">En la página de aterrizaje del servicio, seleccione el servicio, haga doble clic en el nombre del servicio y, a continuación, haga clic en la pestaña **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="4913f-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="4913f-121">En la lista tabular de **Registros de control de acceso**, escriba un **Nombre** para el ACR.</span><span class="sxs-lookup"><span data-stu-id="4913f-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="4913f-122">Proporcione el nombre IQN del host de Windows en **Nombre del iniciador iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="4913f-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="4913f-123">Para obtener el IQN del host de Windows Server, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4913f-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="4913f-124">Inicie el iniciador iSCSI de Microsoft en el host de Windows.</span><span class="sxs-lookup"><span data-stu-id="4913f-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="4913f-125">En la ventana **Propiedades del iniciador iSCSI**, en la pestaña **Configuración**, seleccione y copie la cadena desde el campo **Nombre de iniciador**.</span><span class="sxs-lookup"><span data-stu-id="4913f-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="4913f-126">Pegue esta cadena en el campo **Nombre del iniciador iSCSI** de la tabla de ACR en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="4913f-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="4913f-127">Haga clic en **Guardar** para guardar el ACR recién creado.</span><span class="sxs-lookup"><span data-stu-id="4913f-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="4913f-128">La lista tabular se actualizará para reflejar esta adición.</span><span class="sxs-lookup"><span data-stu-id="4913f-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="4913f-129">Editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-129">Edit an access control record</span></span>
<span data-ttu-id="4913f-130">Use la página **Configurar** del Portal de Azure clásico para editar ACR.</span><span class="sxs-lookup"><span data-stu-id="4913f-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="4913f-131">Puede modificar solo esos ACR que no están actualmente en uso.</span><span class="sxs-lookup"><span data-stu-id="4913f-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="4913f-132">Para editar un ACR asociado a un volumen que está actualmente en uso, primero debe establecer el volumen como sin conexión.</span><span class="sxs-lookup"><span data-stu-id="4913f-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="4913f-133">Realice los pasos siguientes para editar un ACR.</span><span class="sxs-lookup"><span data-stu-id="4913f-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="4913f-134">Para editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-134">To edit an access control record</span></span>
1. <span data-ttu-id="4913f-135">En la página de aterrizaje del servicio, seleccione el servicio, haga doble clic en el nombre del servicio y, a continuación, haga clic en la pestaña **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="4913f-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="4913f-136">En la lista tabular de los registros de control de acceso, pase el ratón sobre el ACR que desea modificar.</span><span class="sxs-lookup"><span data-stu-id="4913f-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="4913f-137">Proporcione un nombre nuevo y/o el IQN del ACR.</span><span class="sxs-lookup"><span data-stu-id="4913f-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="4913f-138">Haga clic en **Guardar** para guardar el ACR modificado.</span><span class="sxs-lookup"><span data-stu-id="4913f-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="4913f-139">La lista tabular se actualizará para reflejar este cambio.</span><span class="sxs-lookup"><span data-stu-id="4913f-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="4913f-140">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-140">Delete an access control record</span></span>
<span data-ttu-id="4913f-141">Use la página **Configurar** del Portal de Azure clásico para eliminar ACR.</span><span class="sxs-lookup"><span data-stu-id="4913f-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="4913f-142">Solo puede eliminar esos ACR que no están actualmente en uso.</span><span class="sxs-lookup"><span data-stu-id="4913f-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="4913f-143">Para eliminar un ACR asociado a un volumen que está actualmente en uso, primero debe establecer el volumen como sin conexión.</span><span class="sxs-lookup"><span data-stu-id="4913f-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="4913f-144">Realice los pasos siguientes para eliminar un registro de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="4913f-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="4913f-145">Para eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="4913f-145">To delete an access control record</span></span>
1. <span data-ttu-id="4913f-146">En la página de aterrizaje del servicio, seleccione el servicio, haga doble clic en el nombre del servicio y, a continuación, haga clic en la pestaña **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="4913f-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="4913f-147">En la lista tabular de los registros de control de acceso (ACR), pase el ratón sobre el ACR que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="4913f-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="4913f-148">Aparecerá un icono de eliminación (**x**) en la columna en el extremo derecho para el ACR que seleccione.</span><span class="sxs-lookup"><span data-stu-id="4913f-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="4913f-149">Haga clic en el icono **x** para eliminar el ACR.</span><span class="sxs-lookup"><span data-stu-id="4913f-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="4913f-150">Cuando se le pida confirmación, haga clic en **SÍ** para continuar con la eliminación.</span><span class="sxs-lookup"><span data-stu-id="4913f-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="4913f-151">La lista tabular se actualizará para reflejar la eliminación.</span><span class="sxs-lookup"><span data-stu-id="4913f-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4913f-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4913f-152">Next steps</span></span>
* <span data-ttu-id="4913f-153">Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="4913f-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="4913f-154">Obtenga más información sobre el [uso del servicio StorSimple Manager para administrar su dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4913f-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

