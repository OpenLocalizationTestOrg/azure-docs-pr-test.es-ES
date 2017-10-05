---
title: "Administración de los registros de control de acceso en StorSimple | Microsoft Docs"
description: "Describe cómo utilizar los registros de control de acceso (ACR) para determinar qué hosts pueden conectarse a un volumen en el dispositivo StorSimple."
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
ms.openlocfilehash: 9173e34f889ce1c082b20bb382cb6ca9a03dd797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="0f235-103">Usar el servicio de Administrador de StorSimple para administrar registros de control de acceso</span><span class="sxs-lookup"><span data-stu-id="0f235-103">Use the StorSimple Manager service to manage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="0f235-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0f235-104">Overview</span></span>
<span data-ttu-id="0f235-105">Los registros de control de acceso (ACR) le permiten especificar qué hosts pueden conectarse a un volumen del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0f235-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="0f235-106">Los ACR se establecen en un volumen específico y contienen los nombres calificados iSCSI (IQNs) de los hosts.</span><span class="sxs-lookup"><span data-stu-id="0f235-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="0f235-107">Cuando un host intenta conectarse a un volumen, el dispositivo comprueba el ACR asociado a ese volumen para el nombre IQN y, a continuación, si hay una coincidencia, se establece la conexión.</span><span class="sxs-lookup"><span data-stu-id="0f235-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="0f235-108">Los registros de control de acceso de la sección **Configuración** de la hoja del servicio StorSimple Device Manager muestra todos los registros de control de acceso con los IQN correspondientes de los hosts.</span><span class="sxs-lookup"><span data-stu-id="0f235-108">The access control records in the **Configuration** section of your StorSimple Device Manager service blade display all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="0f235-109">Este tutorial explica las siguientes tareas comunes relacionadas con los ACR comunes:</span><span class="sxs-lookup"><span data-stu-id="0f235-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="0f235-110">Agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="0f235-110">Add an access control record</span></span>
* <span data-ttu-id="0f235-111">Editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="0f235-111">Edit an access control record</span></span>
* <span data-ttu-id="0f235-112">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="0f235-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="0f235-113">Al asignar un ACR a un volumen, tenga cuidado de que no accedan al mismo tiempo al volumen más de un host no agrupado porque esto podría dañar el volumen.</span><span class="sxs-lookup"><span data-stu-id="0f235-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="0f235-114">Al eliminar un ACR de un volumen, asegúrese de que el host correspondiente no tiene acceso al volumen porque la eliminación podría dar lugar a una interrupción de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="0f235-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>

## <a name="get-the-iqn"></a><span data-ttu-id="0f235-115">Obtención del IQN</span><span class="sxs-lookup"><span data-stu-id="0f235-115">Get the IQN</span></span>

<span data-ttu-id="0f235-116">Siga estos pasos para obtener el nombre completo del IQN de un host de Windows que ejecute Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="0f235-116">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="0f235-117">Agregar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="0f235-117">Add an access control record</span></span>
<span data-ttu-id="0f235-118">Use la sección **Configuración** en la hoja del servicio StorSimple Device Manager para agregar los registros de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="0f235-118">You use the **Configuration** section in the StorSimple Device Manager service blade to add ACRs.</span></span> <span data-ttu-id="0f235-119">Normalmente, se asociará un ACR a un volumen.</span><span class="sxs-lookup"><span data-stu-id="0f235-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="0f235-120">Realice los pasos siguientes para agregar un ACR.</span><span class="sxs-lookup"><span data-stu-id="0f235-120">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="0f235-121">Para agregar un ACR</span><span class="sxs-lookup"><span data-stu-id="0f235-121">To add an ACR</span></span>

1. <span data-ttu-id="0f235-122">Vaya al servicio StorSimple Device Manager, haga doble clic en el nombre del servicio y, en la sección **Configuración**, haga clic en **Registros de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="0f235-122">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="0f235-123">En la hoja **Registros de control de acceso**, haga clic en **Agregar ACR**.</span><span class="sxs-lookup"><span data-stu-id="0f235-123">In the **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Hacer clic en Agregar ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="0f235-125">En la hoja **Agregar ACR**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0f235-125">In the **Add ACR** blade, do the following steps:</span></span>

    1. <span data-ttu-id="0f235-126">Proporcione un Nombre para el ACR.</span><span class="sxs-lookup"><span data-stu-id="0f235-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="0f235-127">Proporcione el nombre IQN del host de Windows Server en **Nombre del iniciador iSCSI (IQN)**.</span><span class="sxs-lookup"><span data-stu-id="0f235-127">Provide the IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="0f235-128">Haga clic en **Agregar** para crear el ACR.</span><span class="sxs-lookup"><span data-stu-id="0f235-128">Click **Add** to create the ACR.</span></span>

        ![Hacer clic en Agregar ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="0f235-130">El ACR recién agregado aparecerá en la lista tabular de ACR.</span><span class="sxs-lookup"><span data-stu-id="0f235-130">The newly added ACR will display in the tabular listing of ACRs.</span></span>

    ![Hacer clic en Agregar ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="0f235-132">Editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="0f235-132">Edit an access control record</span></span>
<span data-ttu-id="0f235-133">Use la sección **Configuración** en la hoja del servicio StorSimple Device Manager para editar los registros de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="0f235-133">You use the **Configuration** section in the StorSimple Device Manager service blade to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="0f235-134">Es recomendable que modifique solo los ACR que no están actualmente en uso.</span><span class="sxs-lookup"><span data-stu-id="0f235-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="0f235-135">Para editar un ACR asociado a un volumen que está actualmente en uso, primero debe establecer el volumen como sin conexión.</span><span class="sxs-lookup"><span data-stu-id="0f235-135">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="0f235-136">Realice los pasos siguientes para editar un ACR.</span><span class="sxs-lookup"><span data-stu-id="0f235-136">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="0f235-137">Para editar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="0f235-137">To edit an access control record</span></span>
1.  <span data-ttu-id="0f235-138">Vaya al servicio StorSimple Device Manager, haga doble clic en el nombre del servicio y, en la sección **Configuración**, haga clic en **Registros de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="0f235-138">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Ir a los registros de control de acceso](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="0f235-140">En la lista tabular de los registros de control de acceso, haga clic y seleccione el ACR que desea modificar.</span><span class="sxs-lookup"><span data-stu-id="0f235-140">In the tabular listing of the access control records, click and select the ACR that you wish to modify.</span></span>

    ![Edición de registros de control de acceso](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="0f235-142">En la hoja **Editar registro de control de acceso**, proporcione un IQN diferente correspondiente a otro host.</span><span class="sxs-lookup"><span data-stu-id="0f235-142">In the **Edit access control record** blade, provide a different IQN corresponding to another host.</span></span>

    ![Edición de registros de control de acceso](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="0f235-144">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0f235-144">Click **Save**.</span></span> <span data-ttu-id="0f235-145">Cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="0f235-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Edición de registros de control de acceso](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="0f235-147">Se le notificará cuando se actualice el ACR.</span><span class="sxs-lookup"><span data-stu-id="0f235-147">You are notified when the ACR is updated.</span></span> <span data-ttu-id="0f235-148">La lista tabular se actualizará también para reflejar los cambios.</span><span class="sxs-lookup"><span data-stu-id="0f235-148">The tabular listing also updates to reflect the change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="0f235-149">Eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="0f235-149">Delete an access control record</span></span>
<span data-ttu-id="0f235-150">Use la sección **Configuración** en la hoja del servicio StorSimple Device Manager para eliminar los registros de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="0f235-150">You use the **Configuration** section in the StorSimple Device Manager service blade to delete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="0f235-151">Solo puede eliminar esos ACR que no están actualmente en uso.</span><span class="sxs-lookup"><span data-stu-id="0f235-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="0f235-152">Para eliminar un ACR asociado a un volumen que está actualmente en uso, primero debe establecer el volumen como sin conexión.</span><span class="sxs-lookup"><span data-stu-id="0f235-152">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="0f235-153">Realice los pasos siguientes para eliminar un registro de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="0f235-153">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="0f235-154">Para eliminar un registro de control de acceso</span><span class="sxs-lookup"><span data-stu-id="0f235-154">To delete an access control record</span></span>
1.  <span data-ttu-id="0f235-155">Vaya al servicio StorSimple Device Manager, haga doble clic en el nombre del servicio y, en la sección **Configuración**, haga clic en **Registros de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="0f235-155">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Ir a los registros de control de acceso](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="0f235-157">En la lista tabular de los registros de control de acceso, haga clic y seleccione el ACR que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="0f235-157">In the tabular listing of the access control records, click and select the ACR that you wish to delete.</span></span>

    ![Ir a los registros de control de acceso](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="0f235-159">Haga clic con el botón derecho para invocar el menú contextual y seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0f235-159">Right-click to invoke the context menu and select **Delete**.</span></span>

    ![Ir a los registros de control de acceso](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="0f235-161">Cuando se le pida confirmación, revise la información y, a continuación, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0f235-161">When prompted for confirmation, review the information and then click **Delete**.</span></span>

    ![Ir a los registros de control de acceso](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="0f235-163">Se le notificará cuando se complete la eliminación.</span><span class="sxs-lookup"><span data-stu-id="0f235-163">You are notified when the deletion completes.</span></span> <span data-ttu-id="0f235-164">La lista tabular se actualizará para reflejar la eliminación.</span><span class="sxs-lookup"><span data-stu-id="0f235-164">The tabular listing is updated to reflect the deletion.</span></span>

    ![Ir a los registros de control de acceso](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="0f235-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f235-166">Next steps</span></span>
* <span data-ttu-id="0f235-167">Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="0f235-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="0f235-168">Obtenga más información sobre el [uso del servicio StorSimple Manager para administrar su dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0f235-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

