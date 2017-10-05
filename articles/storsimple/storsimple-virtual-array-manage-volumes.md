---
title: "Administración de volúmenes en StorSimple Virtual Array | Microsoft Docs"
description: "Describe el servicio StorSimple Device Manager y explica cómo usarlo para administrar volúmenes en StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: a507bf1866952cb79fa6334fed80c88cd207cd0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-service-to-manage-volumes-on-the-storsimple-virtual-array"></a><span data-ttu-id="5654e-103">Uso del servicio StorSimple Device Manager para administrar volúmenes en StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="5654e-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="5654e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="5654e-104">Overview</span></span>

<span data-ttu-id="5654e-105">Este tutorial explica cómo usar el servicio StorSimple Device Manager para crear y administrar volúmenes en StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="5654e-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="5654e-106">El servicio StorSimple Device Manager es una extensión de Azure Portal que permite administrar la solución StorSimple desde una única interfaz web.</span><span class="sxs-lookup"><span data-stu-id="5654e-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="5654e-107">Además de administrar volúmenes y recursos compartidos, puede usar el servicio de StorSimple Device Manager para ver y administrar dispositivos, ver alertas, y ver y administrar directivas de copia de seguridad y el catálogo de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5654e-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="5654e-108">Tipos de volúmenes</span><span class="sxs-lookup"><span data-stu-id="5654e-108">Volume Types</span></span>

<span data-ttu-id="5654e-109">Los volúmenes de StorSimple pueden ser:</span><span class="sxs-lookup"><span data-stu-id="5654e-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="5654e-110">**Anclado localmente**: los datos de estos volúmenes se mantienen en la matriz en todo momento y no se vuelcan en la nube.</span><span class="sxs-lookup"><span data-stu-id="5654e-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="5654e-111">**En capas**: los datos de estos volúmenes pueden volcarse en la nube.</span><span class="sxs-lookup"><span data-stu-id="5654e-111">**Tiered**: Data in these volumes can spill to the cloud.</span></span> <span data-ttu-id="5654e-112">Cuando se crea un volumen en capas, aproximadamente el 10 % del espacio se aprovisiona en la capa local y el 90 % restante en la nube.</span><span class="sxs-lookup"><span data-stu-id="5654e-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="5654e-113">Por ejemplo, si se aprovisiona un volumen de 1 TB, 100 GB residirían en el espacio local y 900 GB se utilizarían en la nube cuando se apilen los datos.</span><span class="sxs-lookup"><span data-stu-id="5654e-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="5654e-114">A su vez, esto hace que, si agota todo el espacio local en el dispositivo, no se podrá aprovisionar un volumen en capas (porque el 10 % necesario de la capa local no estará disponible).</span><span class="sxs-lookup"><span data-stu-id="5654e-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="5654e-115">Capacidad aprovisionada</span><span class="sxs-lookup"><span data-stu-id="5654e-115">Provisioned capacity</span></span>
<span data-ttu-id="5654e-116">Para conocer la capacidad máxima aprovisionada de cada tipo de volumen, consulte la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="5654e-116">Refer to the following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="5654e-117">**Identificador de límites**</span><span class="sxs-lookup"><span data-stu-id="5654e-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="5654e-118">**Límite**</span><span class="sxs-lookup"><span data-stu-id="5654e-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="5654e-119">Tamaño mínimo de un volumen en capas</span><span class="sxs-lookup"><span data-stu-id="5654e-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="5654e-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="5654e-120">500 GB</span></span>        |
| <span data-ttu-id="5654e-121">Tamaño máximo de un volumen en capas</span><span class="sxs-lookup"><span data-stu-id="5654e-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="5654e-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="5654e-122">5 TB</span></span>          |
| <span data-ttu-id="5654e-123">Tamaño mínimo de un volumen anclado localmente</span><span class="sxs-lookup"><span data-stu-id="5654e-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="5654e-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="5654e-124">50 GB</span></span>         |
| <span data-ttu-id="5654e-125">Tamaño máximo de un volumen anclado localmente</span><span class="sxs-lookup"><span data-stu-id="5654e-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="5654e-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="5654e-126">500 GB</span></span>        |

## <a name="the-volumes-blade"></a><span data-ttu-id="5654e-127">La hoja Volúmenes</span><span class="sxs-lookup"><span data-stu-id="5654e-127">The Volumes blade</span></span>
<span data-ttu-id="5654e-128">El menú **Volúmenes** de la hoja de resumen del servicio StorSimple muestra la lista de volúmenes de almacenamiento en una matriz dada de StorSimple y permite administrarlos.</span><span class="sxs-lookup"><span data-stu-id="5654e-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span></span>

![Hoja Volúmenes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="5654e-130">Un volumen se compone de una serie de atributos:</span><span class="sxs-lookup"><span data-stu-id="5654e-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="5654e-131">**Nombre** : nombre descriptivo que debe ser único y que ayuda a identificar el volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span>
* <span data-ttu-id="5654e-132">**Estado** : puede estar conectado o desconectado.</span><span class="sxs-lookup"><span data-stu-id="5654e-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="5654e-133">Si un volumen está desconectado, no es visible para los iniciadores (servidores) que tienen permitido el acceso para usar el volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="5654e-134">**Tipo**: indica si el tipo del volumen es **En capas** (predeterminado) o **Anclado localmente**.</span><span class="sxs-lookup"><span data-stu-id="5654e-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="5654e-135">**Capacidad**: especifica la cantidad de datos utilizados en comparación con la cantidad total de datos que puede almacenar el iniciador (servidor).</span><span class="sxs-lookup"><span data-stu-id="5654e-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span></span>
* <span data-ttu-id="5654e-136">**Copia de seguridad**: en el caso de StorSimple Virtual Array, se habilitan automáticamente todos los volúmenes para la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5654e-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="5654e-137">**Hosts conectados**: especifica los iniciadores (servidores) que pueden tener acceso a este volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span></span>

![Detalles de volúmenes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="5654e-139">Siga las instrucciones de este tutorial para realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="5654e-139">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="5654e-140">Agregar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-140">Add a volume</span></span>
* <span data-ttu-id="5654e-141">Modificar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-141">Modify a volume</span></span>
* <span data-ttu-id="5654e-142">Desconectar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-142">Take a volume offline</span></span>
* <span data-ttu-id="5654e-143">Eliminar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="5654e-144">Agregar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-144">Add a volume</span></span>

1. <span data-ttu-id="5654e-145">En la hoja de resumen del servicio StorSimple, haga clic en **+ Agregar volumen** desde la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="5654e-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="5654e-146">Con ello, se abrirá la hoja **Agregar volumen**.</span><span class="sxs-lookup"><span data-stu-id="5654e-146">This opens up the **Add volume** blade.</span></span>
   
    ![Agregar volumen](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="5654e-148">En la hoja **Agregar volumen**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5654e-148">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="5654e-149">En el campo **Nombre del volumen**, escriba un nombre único para el volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-149">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="5654e-150">El nombre debe ser una cadena que contenga entre 3 y 127 caracteres.</span><span class="sxs-lookup"><span data-stu-id="5654e-150">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="5654e-151">En la lista desplegable **Tipo**, especifique si desea crear un volumen **en capas** o **anclado localmente**.</span><span class="sxs-lookup"><span data-stu-id="5654e-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="5654e-152">Para las cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione **Volumen anclado localmente**.</span><span class="sxs-lookup"><span data-stu-id="5654e-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="5654e-153">Para todos los demás datos, seleccione volumen **en capas**.</span><span class="sxs-lookup"><span data-stu-id="5654e-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="5654e-154">En el campo **Capacidad**, especifique el tamaño del volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-154">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="5654e-155">Un volumen en capas debe tener entre 500 GB y 5 TB, mientras que un volumen anclado localmente debe oscilar entre 50 GB y 500 GB.</span><span class="sxs-lookup"><span data-stu-id="5654e-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="5654e-156">Haga clic en **Hosts conectados**, seleccione un registro de control de acceso (ACR) correspondiente al iniciador iSCSI que desea conectar a este volumen y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="5654e-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span>
3. <span data-ttu-id="5654e-157">Para agregar un nuevo host conectado, haga clic en **Agregar nuevo**, escriba un nombre para el host y su nombre calificado iSCSI (IQN) y, a continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5654e-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Agregar volumen](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="5654e-159">Cuando haya terminado de configurar el volumen, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5654e-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="5654e-160">Se creará un volumen con la configuración especificada y verá una notificación al finalizar correctamente la creación de este.</span><span class="sxs-lookup"><span data-stu-id="5654e-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span></span> <span data-ttu-id="5654e-161">De forma predeterminada, se habilitará la copia de seguridad para el volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-161">By default backup will be enabled for the volume.</span></span>
5. <span data-ttu-id="5654e-162">Para confirmar que el volumen se creó correctamente, vaya a la hoja **Volúmenes**.</span><span class="sxs-lookup"><span data-stu-id="5654e-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="5654e-163">Debería ver el volumen mostrado.</span><span class="sxs-lookup"><span data-stu-id="5654e-163">You should see the volume listed.</span></span>
   
    ![Creación de volumen correcta](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="5654e-165">Modificar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-165">Modify a volume</span></span>

<span data-ttu-id="5654e-166">Modifique un volumen cuando necesite cambiar los hosts que tienen acceso al volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-166">Modify a volume when you need to change the hosts that access the volume.</span></span> <span data-ttu-id="5654e-167">No se podrán modificar los demás atributos de un volumen una vez que se haya creado este.</span><span class="sxs-lookup"><span data-stu-id="5654e-167">The other attributes of a volume cannot be modified once the volume has been created.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="5654e-168">Para modificar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-168">To modify a volume</span></span>

1. <span data-ttu-id="5654e-169">Desde el valor **Volúmenes** de la hoja de resumen del servicio StorSimple, seleccione la matriz virtual en la que reside el volumen que se desea modificar.</span><span class="sxs-lookup"><span data-stu-id="5654e-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span></span>
2. <span data-ttu-id="5654e-170">**Seleccione** el volumen y haga clic en **Hosts conectados** para ver el host conectado actualmente y modifíquelo en un servidor diferente.</span><span class="sxs-lookup"><span data-stu-id="5654e-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span></span>
   
    ![Modificación del volumen](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="5654e-172">Guarde los cambios haciendo clic en **Guardar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="5654e-172">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="5654e-173">Se aplicará la configuración especificada y verá una notificación.</span><span class="sxs-lookup"><span data-stu-id="5654e-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="5654e-174">Desconectar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-174">Take a volume offline</span></span>

<span data-ttu-id="5654e-175">Puede que necesite desconectar un volumen si tiene previsto modificarlo o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="5654e-175">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="5654e-176">Cuando un volumen está desconectado, no está disponible para el acceso de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="5654e-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="5654e-177">Deberá desconectar el volumen en el host, así como en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5654e-177">You will need to take the volume offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="5654e-178">Para desconectar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-178">To take a volume offline</span></span>

1. <span data-ttu-id="5654e-179">Asegúrese de que el volumen en cuestión no está en uso antes de desconectarlo.</span><span class="sxs-lookup"><span data-stu-id="5654e-179">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="5654e-180">Desconecte el volumen primero en el host.</span><span class="sxs-lookup"><span data-stu-id="5654e-180">Take the volume offline on the host first.</span></span> <span data-ttu-id="5654e-181">Esto elimina cualquier riesgo potencial de dañar los datos del volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-181">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="5654e-182">Para conocer los pasos específicos, consulte las instrucciones del sistema operativo del host.</span><span class="sxs-lookup"><span data-stu-id="5654e-182">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="5654e-183">Una vez desconectado el volumen del host, desconecte el volumen de la matriz siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5654e-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span></span>
   
   * <span data-ttu-id="5654e-184">Desde el valor **Volúmenes** de la hoja de resumen del servicio StorSimple, seleccione la matriz virtual en la que reside el volumen que desea desconectar.</span><span class="sxs-lookup"><span data-stu-id="5654e-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span></span>
   * <span data-ttu-id="5654e-185">**Seleccione** el volumen y haga clic en **...** (o bien haga clic derecho en esta fila) y en el menú contextual, seleccione **Desconectar**.</span><span class="sxs-lookup"><span data-stu-id="5654e-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Volumen desconectado](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="5654e-187">Revise la información de la hoja **Desconectar** y confirme la aceptación de la operación.</span><span class="sxs-lookup"><span data-stu-id="5654e-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="5654e-188">Haga clic en **Desconectar** para desconectar el volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-188">Click **Take offline** to take the volume offline.</span></span> <span data-ttu-id="5654e-189">Verá una notificación que le indica que la operación está en curso.</span><span class="sxs-lookup"><span data-stu-id="5654e-189">You will see a notification of the operation in progress.</span></span>
   * <span data-ttu-id="5654e-190">Para confirmar que el volumen se desconectó correctamente, vaya a la hoja **Volúmenes**.</span><span class="sxs-lookup"><span data-stu-id="5654e-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span></span> <span data-ttu-id="5654e-191">El volumen debe aparecer como desconectado.</span><span class="sxs-lookup"><span data-stu-id="5654e-191">You should see the status of the volume as offline.</span></span>
     
       ![Confirmación de volumen desconectado](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="5654e-193">Eliminar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5654e-194">Puede eliminar un volumen solo si está desconectado.</span><span class="sxs-lookup"><span data-stu-id="5654e-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="5654e-195">Siga estos pasos para eliminar un volumen.</span><span class="sxs-lookup"><span data-stu-id="5654e-195">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="5654e-196">Para eliminar un volumen</span><span class="sxs-lookup"><span data-stu-id="5654e-196">To delete a volume</span></span>

1. <span data-ttu-id="5654e-197">Desde el valor **Volúmenes** de la hoja de resumen del servicio StorSimple, seleccione la matriz virtual en la que reside el volumen que se desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="5654e-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span></span>
2. <span data-ttu-id="5654e-198">**Seleccione** el volumen y haga clic en **...** (o bien haga clic derecho en esta fila) y en el menú contextual, seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="5654e-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Eliminar volumen](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="5654e-200">Compruebe el estado del volumen que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="5654e-200">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="5654e-201">Si el volumen que desea eliminar no está desconectado, desconéctelo primero siguiendo los pasos indicados en [Desconectar un volumen](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="5654e-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="5654e-202">Cuando se le pida confirmación en la hoja **Eliminar**, acepte la confirmación y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="5654e-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="5654e-203">El volumen se eliminará y la hoja **Volúmenes** mostrará la lista actualizada de volúmenes dentro de la matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="5654e-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5654e-204">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5654e-204">Next steps</span></span>

<span data-ttu-id="5654e-205">Aprenda cómo [clonar un volumen de StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="5654e-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

