---
title: "volúmenes de aaaManage en StorSimple Virtual Array | Documentos de Microsoft"
description: "Hola, Administrador de dispositivos de StorSimple se describe y se explica cómo toouse se toomanage volúmenes en la matriz Virtual de StorSimple."
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
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a><span data-ttu-id="74cb3-103">Volúmenes de toomanage de servicio de administrador de dispositivos de StorSimple de uso en hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="74cb3-103">Use StorSimple Device Manager service toomanage volumes on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="74cb3-104">Información general</span><span class="sxs-lookup"><span data-stu-id="74cb3-104">Overview</span></span>

<span data-ttu-id="74cb3-105">Este tutorial le explica cómo toouse Hola toocreate de servicio de administrador de dispositivos de StorSimple y administrar los volúmenes en la matriz Virtual de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="74cb3-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="74cb3-106">Hola servicio Administrador de dispositivos de StorSimple es una extensión en hello portal de Azure que le permite administrar la solución de StorSimple de una única interfaz web.</span><span class="sxs-lookup"><span data-stu-id="74cb3-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="74cb3-107">En los volúmenes y recursos compartidos de toomanaging de suma, puede usar tooview de servicio del Administrador de dispositivos de StorSimple de Hola y administrar dispositivos, ver alertas y ver y administrar directivas de copia de seguridad y el catálogo de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="74cb3-108">Tipos de volúmenes</span><span class="sxs-lookup"><span data-stu-id="74cb3-108">Volume Types</span></span>

<span data-ttu-id="74cb3-109">Los volúmenes de StorSimple pueden ser:</span><span class="sxs-lookup"><span data-stu-id="74cb3-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="74cb3-110">**Anclado localmente**: datos de estos volúmenes permanece en la matriz de hello en todo momento y no volcarse toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="74cb3-110">**Locally pinned**: Data in these volumes stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="74cb3-111">**En niveles**: datos de estos volúmenes pueden retrasar toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="74cb3-111">**Tiered**: Data in these volumes can spill toohello cloud.</span></span> <span data-ttu-id="74cb3-112">Cuando se crea un volumen en capas, aproximadamente el 10% del espacio de Hola se aprovisionó en nivel local hello y 90% del espacio de Hola se aprovisiona en nube Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-112">When you create a tiered volume, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="74cb3-113">Por ejemplo, si ha aprovisionado un volumen de 1 TB, 100 GB residiría en el espacio local hello y 900 GB se utilizaría en nube Hola Hola cuando capas de datos.</span><span class="sxs-lookup"><span data-stu-id="74cb3-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="74cb3-114">A su vez, esto implica que si se ejecuta fuera de todo el espacio local en hello en dispositivo hello, no se puede aprovisionar un volumen en capas (porque Hola 10% necesarios en hello local nivel no estará disponible).</span><span class="sxs-lookup"><span data-stu-id="74cb3-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered volume (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="74cb3-115">Capacidad aprovisionada</span><span class="sxs-lookup"><span data-stu-id="74cb3-115">Provisioned capacity</span></span>
<span data-ttu-id="74cb3-116">Consulte toohello máxima capacidad aprovisionada para cada tipo de volumen en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="74cb3-116">Refer toohello following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="74cb3-117">**Identificador de límites**</span><span class="sxs-lookup"><span data-stu-id="74cb3-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="74cb3-118">**Límite**</span><span class="sxs-lookup"><span data-stu-id="74cb3-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="74cb3-119">Tamaño mínimo de un volumen en capas</span><span class="sxs-lookup"><span data-stu-id="74cb3-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="74cb3-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="74cb3-120">500 GB</span></span>        |
| <span data-ttu-id="74cb3-121">Tamaño máximo de un volumen en capas</span><span class="sxs-lookup"><span data-stu-id="74cb3-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="74cb3-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="74cb3-122">5 TB</span></span>          |
| <span data-ttu-id="74cb3-123">Tamaño mínimo de un volumen anclado localmente</span><span class="sxs-lookup"><span data-stu-id="74cb3-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="74cb3-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="74cb3-124">50 GB</span></span>         |
| <span data-ttu-id="74cb3-125">Tamaño máximo de un volumen anclado localmente</span><span class="sxs-lookup"><span data-stu-id="74cb3-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="74cb3-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="74cb3-126">500 GB</span></span>        |

## <a name="hello-volumes-blade"></a><span data-ttu-id="74cb3-127">hoja de volúmenes de Hola</span><span class="sxs-lookup"><span data-stu-id="74cb3-127">hello Volumes blade</span></span>
<span data-ttu-id="74cb3-128">Hola **volúmenes** menú en la hoja de resumen de servicio de StorSimple muestra la lista de Hola de volúmenes de almacenamiento en una matriz StorSimple y permitiéndole toomanage ellos.</span><span class="sxs-lookup"><span data-stu-id="74cb3-128">hello **Volumes** menu on your StorSimple service summary blade displays hello list of storage volumes on a given StorSimple array and allows you toomanage them.</span></span>

![Hoja Volúmenes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="74cb3-130">Un volumen se compone de una serie de atributos:</span><span class="sxs-lookup"><span data-stu-id="74cb3-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="74cb3-131">**Nombre del volumen** : un nombre descriptivo que debe ser únicos y ayuda a identificar el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-131">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span>
* <span data-ttu-id="74cb3-132">**Estado** : puede estar conectado o desconectado.</span><span class="sxs-lookup"><span data-stu-id="74cb3-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="74cb3-133">Si un volumen está sin conexión, no es visible tooinitiators (servidores) que se permiten acceso toouse Hola volumen.</span><span class="sxs-lookup"><span data-stu-id="74cb3-133">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="74cb3-134">**Tipo de** : indica si el volumen de hello es **"en capas"** (Hola predeterminado) o **anclado localmente**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-134">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="74cb3-135">**Capacidad** : especifica la cantidad de Hola de datos que se usan como toohello en comparación con la cantidad total de datos que se pueden almacenar por el iniciador de hello (servidor).</span><span class="sxs-lookup"><span data-stu-id="74cb3-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored by hello initiator (server).</span></span>
* <span data-ttu-id="74cb3-136">**Copia de seguridad** : en el caso de hello StorSimple Virtual Array, se habilitan automáticamente todos los volúmenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="74cb3-136">**Backup** – In case of hello StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="74cb3-137">**Hosts conectados** – especifica iniciadores de hello (servidores) que se permiten acceso toothis volumen.</span><span class="sxs-lookup"><span data-stu-id="74cb3-137">**Connected hosts** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span>

![Detalles de volúmenes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="74cb3-139">Use las instrucciones de hello en este hello tooperform tutorial siguiente las tareas:</span><span class="sxs-lookup"><span data-stu-id="74cb3-139">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="74cb3-140">Agregar un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-140">Add a volume</span></span>
* <span data-ttu-id="74cb3-141">Modificar un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-141">Modify a volume</span></span>
* <span data-ttu-id="74cb3-142">Desconectar un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-142">Take a volume offline</span></span>
* <span data-ttu-id="74cb3-143">Eliminar un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="74cb3-144">Agregar un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-144">Add a volume</span></span>

1. <span data-ttu-id="74cb3-145">En la hoja de resumen de hello StorSimple servicio, haga clic en **+ agregar volumen** de barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-145">From hello StorSimple service summary blade, click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="74cb3-146">Esto abrirá hello **agregar volumen** hoja.</span><span class="sxs-lookup"><span data-stu-id="74cb3-146">This opens up hello **Add volume** blade.</span></span>
   
    ![Agregar volumen](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="74cb3-148">Hola **agregar volumen** hoja, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="74cb3-148">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="74cb3-149">Hola **nombre del volumen** , a continuación, escriba un nombre único para su volumen.</span><span class="sxs-lookup"><span data-stu-id="74cb3-149">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="74cb3-150">nombre de Hello debe ser una cadena que contiene 3 too127 caracteres.</span><span class="sxs-lookup"><span data-stu-id="74cb3-150">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="74cb3-151">Hola **tipo** lista desplegable lista, especifique si toocreate una **"en capas"** o **anclado localmente** volumen.</span><span class="sxs-lookup"><span data-stu-id="74cb3-151">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="74cb3-152">Para las cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione **Volumen anclado localmente**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="74cb3-153">Para todos los demás datos, seleccione volumen **en capas**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="74cb3-154">Hola **capacidad** , especifique el tamaño de hello del volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-154">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="74cb3-155">Un volumen en capas debe tener entre 500 GB y 5 TB, mientras que un volumen anclado localmente debe oscilar entre 50 GB y 500 GB.</span><span class="sxs-lookup"><span data-stu-id="74cb3-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="74cb3-156">Haga clic en **hosts conectados**, seleccione un acceso control registro (ACR) correspondiente toohello iniciador iSCSI que desee tooconnect toothis volumen y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-156">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span>
3. <span data-ttu-id="74cb3-157">tooadd un nuevo host conectado, haga clic en **agregar nueva**, escriba un nombre de host de Hola y su iSCSI (IQN) nombre completo y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-157">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Agregar volumen](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="74cb3-159">Cuando haya terminado de configurar el volumen, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="74cb3-160">Se creará un volumen con hello especificado configuración y verá una notificación durante la creación correcta de Hola de Hola igual.</span><span class="sxs-lookup"><span data-stu-id="74cb3-160">A volume will be created with hello specified settings and you will see a notification on hello successful creation of hello same.</span></span> <span data-ttu-id="74cb3-161">De forma predeterminada, copia de seguridad se habilitarán para volumen Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-161">By default backup will be enabled for hello volume.</span></span>
5. <span data-ttu-id="74cb3-162">tooconfirm que Hola volumen estaba se creó correctamente, vaya toohello **volúmenes** hoja.</span><span class="sxs-lookup"><span data-stu-id="74cb3-162">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="74cb3-163">Debería ver los volúmenes de Hola que aparecen.</span><span class="sxs-lookup"><span data-stu-id="74cb3-163">You should see hello volume listed.</span></span>
   
    ![Creación de volumen correcta](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="74cb3-165">Modificar un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-165">Modify a volume</span></span>

<span data-ttu-id="74cb3-166">Modificar un volumen cuando necesita toochange Hola hosts que tienen acceso a los volúmenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-166">Modify a volume when you need toochange hello hosts that access hello volume.</span></span> <span data-ttu-id="74cb3-167">Hello otros atributos de un volumen no se puede modificar una vez que se ha creado el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-167">hello other attributes of a volume cannot be modified once hello volume has been created.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="74cb3-168">toomodify un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-168">toomodify a volume</span></span>

1. <span data-ttu-id="74cb3-169">De hello **volúmenes** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el volumen que le gustaría toomodify.</span><span class="sxs-lookup"><span data-stu-id="74cb3-169">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toomodify resides.</span></span>
2. <span data-ttu-id="74cb3-170">**Seleccione** Hola volumen y haga clic en **hosts conectados** tooview Hola host conectado actualmente y modifíquelo tooa otro servidor.</span><span class="sxs-lookup"><span data-stu-id="74cb3-170">**Select** hello volume and click **Connected hosts** tooview hello currently connected host and modify it tooa different server.</span></span>
   
    ![Modificación del volumen](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="74cb3-172">Guarde los cambios haciendo clic en hello **guardar** barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="74cb3-172">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="74cb3-173">Se aplicará la configuración especificada y verá una notificación.</span><span class="sxs-lookup"><span data-stu-id="74cb3-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="74cb3-174">Desconectar un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-174">Take a volume offline</span></span>

<span data-ttu-id="74cb3-175">Puede que necesite tootake un volumen sin conexión cuando piensa toomodify lo o delete.</span><span class="sxs-lookup"><span data-stu-id="74cb3-175">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="74cb3-176">Cuando un volumen está desconectado, no está disponible para el acceso de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="74cb3-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="74cb3-177">Necesitará tootake Hola volumen sin conexión en el host de hello, así como en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-177">You will need tootake hello volume offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="74cb3-178">tootake un volumen sin conexión</span><span class="sxs-lookup"><span data-stu-id="74cb3-178">tootake a volume offline</span></span>

1. <span data-ttu-id="74cb3-179">Asegúrese de que volumen hello en cuestión no está en uso antes de desconectarlo.</span><span class="sxs-lookup"><span data-stu-id="74cb3-179">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="74cb3-180">Desconecte volumen hello en el host de hello primero.</span><span class="sxs-lookup"><span data-stu-id="74cb3-180">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="74cb3-181">Esto elimina cualquier riesgo potencial de daños en los datos en el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-181">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="74cb3-182">Para obtener pasos específicos, consulte las instrucciones de toohello para el sistema operativo host.</span><span class="sxs-lookup"><span data-stu-id="74cb3-182">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="74cb3-183">Después de volumen de hello en el host de hello está sin conexión, desconecte el volumen de hello en la matriz de hello sin conexión mediante la realización de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="74cb3-183">After hello volume on hello host is offline, take hello volume on hello array  offline by performing hello following steps:</span></span>
   
   * <span data-ttu-id="74cb3-184">De hello **volúmenes** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el volumen que le gustaría tootake sin conexión.</span><span class="sxs-lookup"><span data-stu-id="74cb3-184">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you tootake offline resides.</span></span>
   * <span data-ttu-id="74cb3-185">**Seleccione** Hola volumen y haga clic en **...**  (o bien pulse el botón derecho en esta fila) y en el menú contextual de hello, seleccione **desconectar**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-185">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Volumen desconectado](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="74cb3-187">Revise la información de Hola Hola **desconectar** hoja y confirmar la aceptación de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-187">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="74cb3-188">Haga clic en **desconectar** volumen tootake Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-188">Click **Take offline** tootake hello volume offline.</span></span> <span data-ttu-id="74cb3-189">Verá una notificación de Hola la operación en curso.</span><span class="sxs-lookup"><span data-stu-id="74cb3-189">You will see a notification of hello operation in progress.</span></span>
   * <span data-ttu-id="74cb3-190">tooconfirm que el volumen de hello correctamente se dejó sin conexión, vaya toohello **volúmenes** hoja.</span><span class="sxs-lookup"><span data-stu-id="74cb3-190">tooconfirm that hello volume was successfully taken offline, go toohello **Volumes** blade.</span></span> <span data-ttu-id="74cb3-191">Debería ver estado de saludo del volumen de hello como sin conexión.</span><span class="sxs-lookup"><span data-stu-id="74cb3-191">You should see hello status of hello volume as offline.</span></span>
     
       ![Confirmación de volumen desconectado](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="74cb3-193">Eliminar un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74cb3-194">Puede eliminar un volumen solo si está desconectado.</span><span class="sxs-lookup"><span data-stu-id="74cb3-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="74cb3-195">Completar Hola siguiendo los pasos toodelete un volumen.</span><span class="sxs-lookup"><span data-stu-id="74cb3-195">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="74cb3-196">toodelete un volumen</span><span class="sxs-lookup"><span data-stu-id="74cb3-196">toodelete a volume</span></span>

1. <span data-ttu-id="74cb3-197">De hello **volúmenes** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el volumen que le gustaría toodelete.</span><span class="sxs-lookup"><span data-stu-id="74cb3-197">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toodelete resides.</span></span>
2. <span data-ttu-id="74cb3-198">**Seleccione** Hola volumen y haga clic en **...**  (o bien pulse el botón derecho en esta fila) y en el menú contextual de hello, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-198">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Eliminar volumen](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="74cb3-200">Comprobar el estado de saludo del volumen de Hola que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="74cb3-200">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="74cb3-201">Si desea toodelete de volumen de hello no está desconectado, dejarlo pasos hello en primer lugar, siguiente sin conexión [desconectar un volumen](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="74cb3-201">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="74cb3-202">Cuando se le pida confirmación en hello **eliminar** hoja, acepte la confirmación de Hola y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-202">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="74cb3-203">volumen de Hola se eliminará y Hola **volúmenes** hoja mostrará la lista de hello actualizado de volúmenes dentro de la matriz virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="74cb3-203">hello volume will now be deleted and hello **Volumes** blade will show hello updated list of volumes within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74cb3-204">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="74cb3-204">Next steps</span></span>

<span data-ttu-id="74cb3-205">Obtenga información acerca de cómo demasiado[clonar un volumen de StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="74cb3-205">Learn how too[clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

