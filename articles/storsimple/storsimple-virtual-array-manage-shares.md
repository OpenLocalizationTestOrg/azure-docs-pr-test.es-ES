---
title: recursos compartidos de StorSimple Virtual Array aaaManage | Documentos de Microsoft
description: "Hola, Administrador de dispositivos de StorSimple se describe y se explica cómo toouse se toomanage los recursos compartidos de la matriz Virtual de StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="b176c-103">Usar recursos compartidos toomanage de servicio de administrador de dispositivos de StorSimple de hello en hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="b176c-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="b176c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b176c-104">Overview</span></span>

<span data-ttu-id="b176c-105">Este tutorial le explica cómo toouse Hola toocreate de servicio de administrador de dispositivos de StorSimple y administrar recursos compartidos en la matriz Virtual de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b176c-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="b176c-106">Hola servicio Administrador de dispositivos de StorSimple es una extensión en hello portal de Azure que le permite administrar la solución de StorSimple de una única interfaz web.</span><span class="sxs-lookup"><span data-stu-id="b176c-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="b176c-107">En volúmenes y recursos compartidos de toomanaging de suma, puede usar tooview de servicio del Administrador de dispositivos de StorSimple de Hola y administrar dispositivos, ver las alertas, administrar directivas de copia de seguridad y administrar el catálogo de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="b176c-108">Tipos de recursos compartidos</span><span class="sxs-lookup"><span data-stu-id="b176c-108">Share Types</span></span>

<span data-ttu-id="b176c-109">Los recursos compartidos de StorSimple pueden ser de uno de los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="b176c-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="b176c-110">**Anclado localmente**: datos de estos recursos compartidos permanece en la matriz de hello en todo momento y no volcarse toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="b176c-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="b176c-111">**En niveles**: datos de estos recursos compartidos pueden retrasar toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="b176c-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="b176c-112">Cuando se crea un recurso compartido en capas, aproximadamente el 10% del espacio de Hola se aprovisionó en nivel local hello y 90% del espacio de Hola se aprovisiona en nube Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="b176c-113">Por ejemplo, si ha aprovisionado a un recurso compartido de 1 TB, 100 GB residiría en el espacio local hello y 900 GB se utilizaría en nube Hola Hola cuando capas de datos.</span><span class="sxs-lookup"><span data-stu-id="b176c-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="b176c-114">A su vez, esto implica que si se ejecuta fuera de todo el espacio local en hello en dispositivo hello, no se puede aprovisionar un recurso compartido en capas (porque Hola 10% necesarios en hello local nivel no estará disponible).</span><span class="sxs-lookup"><span data-stu-id="b176c-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="b176c-115">Capacidad aprovisionada</span><span class="sxs-lookup"><span data-stu-id="b176c-115">Provisioned capacity</span></span>

<span data-ttu-id="b176c-116">Consulte toohello máxima capacidad aprovisionada para cada tipo de recurso compartido en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="b176c-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="b176c-117">**Identificador de límites**</span><span class="sxs-lookup"><span data-stu-id="b176c-117">**Limit identifier**</span></span> | <span data-ttu-id="b176c-118">**Límite**</span><span class="sxs-lookup"><span data-stu-id="b176c-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="b176c-119">Tamaño mínimo de un recurso compartido en capas</span><span class="sxs-lookup"><span data-stu-id="b176c-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="b176c-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="b176c-120">500 GB</span></span> |
| <span data-ttu-id="b176c-121">Tamaño máximo de un recurso compartido en capas</span><span class="sxs-lookup"><span data-stu-id="b176c-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="b176c-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="b176c-122">20 TB</span></span> |
| <span data-ttu-id="b176c-123">Tamaño mínimo de un recurso compartido anclado localmente</span><span class="sxs-lookup"><span data-stu-id="b176c-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="b176c-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="b176c-124">50 GB</span></span> |
| <span data-ttu-id="b176c-125">Tamaño máximo del recurso compartido anclado localmente</span><span class="sxs-lookup"><span data-stu-id="b176c-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="b176c-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="b176c-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="b176c-127">hoja de recursos compartidos de Hola</span><span class="sxs-lookup"><span data-stu-id="b176c-127">hello Shares blade</span></span>

<span data-ttu-id="b176c-128">Hola **recursos compartidos** menú en la hoja de resumen de servicio de StorSimple muestra la lista de Hola de recursos compartidos de almacenamiento en una matriz StorSimple y permitiéndole toomanage ellos.</span><span class="sxs-lookup"><span data-stu-id="b176c-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![Hoja Recursos compartidos](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="b176c-130">Un recurso compartido se compone de una serie de atributos:</span><span class="sxs-lookup"><span data-stu-id="b176c-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="b176c-131">**Nombre del recurso compartido** : un nombre descriptivo que debe ser únicos y ayuda a identificar el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="b176c-132">**Estado** : puede estar conectado o desconectado.</span><span class="sxs-lookup"><span data-stu-id="b176c-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="b176c-133">Si un recurso compartido está desconectado, los usuarios del recurso compartido de hello no estarán tooaccess capaz de él.</span><span class="sxs-lookup"><span data-stu-id="b176c-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="b176c-134">**Tipo de** : indica si el recurso compartido de hello es **"en capas"** (Hola predeterminado) o **anclado localmente**.</span><span class="sxs-lookup"><span data-stu-id="b176c-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="b176c-135">**Capacidad** : especifica la cantidad de Hola de datos que se usan como toohello en comparación con la cantidad total de datos que pueden almacenarse en el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="b176c-136">**Descripción** – una configuración opcional que ayuda a describir el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="b176c-137">**Permisos** -Hola NTFS permisos toohello recurso compartido que se pueden administrar a través del explorador de Windows.</span><span class="sxs-lookup"><span data-stu-id="b176c-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="b176c-138">**Copia de seguridad** : en el caso de hello StorSimple Virtual Array, se habilitan automáticamente todos los recursos compartidos para copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b176c-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Detalles del recurso compartido](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="b176c-140">Use las instrucciones de hello en este hello tooperform tutorial siguiente las tareas:</span><span class="sxs-lookup"><span data-stu-id="b176c-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="b176c-141">Agregar un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-141">Add a share</span></span>
* <span data-ttu-id="b176c-142">Modificación de un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-142">Modify a share</span></span>
* <span data-ttu-id="b176c-143">Desconexión de un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-143">Take a share offline</span></span>
* <span data-ttu-id="b176c-144">Eliminación de un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="b176c-145">Agregar un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-145">Add a share</span></span>

1. <span data-ttu-id="b176c-146">En la hoja de resumen de hello StorSimple servicio, haga clic en **+ recurso compartido de agregar** de barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="b176c-147">Esto abrirá hello **recurso compartido de agregar** hoja.</span><span class="sxs-lookup"><span data-stu-id="b176c-147">This opens up hello **Add share** blade.</span></span>

    ![Incorporación de un recurso compartido](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="b176c-149">Hola **recurso compartido de agregar** hoja, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b176c-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="b176c-150">Hola **nombre de recurso compartido** , escriba un nombre único para el recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="b176c-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="b176c-151">nombre de Hello debe ser una cadena que contiene 3 too127 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b176c-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="b176c-152">Opcional **descripción** para el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="b176c-153">Descripción de Hello le ayudará a identificar los propietarios del recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="b176c-154">Hola **tipo** lista desplegable lista, especifique si toocreate una **"en capas"** o **anclado localmente** compartir.</span><span class="sxs-lookup"><span data-stu-id="b176c-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="b176c-155">Para las cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione **Recurso compartido anclado localmente**.</span><span class="sxs-lookup"><span data-stu-id="b176c-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="b176c-156">Para todos los demás datos, seleccione **Recurso compartido en capas**.</span><span class="sxs-lookup"><span data-stu-id="b176c-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="b176c-157">Hola **capacidad** , especifique el tamaño de Hola de recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="b176c-158">Un recurso compartido en capas debe tener entre 500 GB y 20 TB, y uno anclado localmente debe tener entre 50 GB y 2 TB.</span><span class="sxs-lookup"><span data-stu-id="b176c-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="b176c-159">Hola **establezca predeterminados todos los permisos** , a continuación, asignar Hola permisos toohello, usuario o grupo de Hola que tenga acceso a este recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="b176c-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="b176c-160">Especifique Hola nombre de usuario de Hola o grupo de usuarios de hello en  _john@contoso.com_  formato.</span><span class="sxs-lookup"><span data-stu-id="b176c-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="b176c-161">Se recomienda usar un tooaccess de privilegios de administrador de usuario grupo (en lugar de un solo usuario) tooallow estos recursos compartidos.</span><span class="sxs-lookup"><span data-stu-id="b176c-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="b176c-162">Después de haber asignado permisos de hello aquí, a continuación, puede usar estos permisos toomodify del explorador de archivos.</span><span class="sxs-lookup"><span data-stu-id="b176c-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="b176c-163">Cuando haya terminado de configurar el recurso compartido, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b176c-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="b176c-164">Se creará un recurso compartido con hello especificado configuración y verá una notificación.</span><span class="sxs-lookup"><span data-stu-id="b176c-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="b176c-165">De forma predeterminada, copia de seguridad se habilitará para el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="b176c-166">tooconfirm que Hola recurso compartido estaba se creó correctamente, vaya toohello **recursos compartidos** hoja.</span><span class="sxs-lookup"><span data-stu-id="b176c-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="b176c-167">Debería ver Hola compartir enumeradas.</span><span class="sxs-lookup"><span data-stu-id="b176c-167">You should see hello share listed.</span></span>
   
    ![Creación de un recurso compartido correcta](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="b176c-169">Modificación de un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-169">Modify a share</span></span>

<span data-ttu-id="b176c-170">Modificar un recurso compartido cuando necesite descripción de hello toochange del recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="b176c-171">Ninguna otra propiedad de recurso compartido puede modificarse una vez creado el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="b176c-172">toomodify un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-172">toomodify a share</span></span>

1. <span data-ttu-id="b176c-173">De hello **recursos compartidos** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el recurso compartido que le gustaría toomodify.</span><span class="sxs-lookup"><span data-stu-id="b176c-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="b176c-174">**Seleccione** Hola descripción actual del recurso compartido tooview hello y modificarlo.</span><span class="sxs-lookup"><span data-stu-id="b176c-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="b176c-175">Guarde los cambios haciendo clic en hello **guardar** barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="b176c-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="b176c-176">Se aplicará la configuración especificada y verá una notificación.</span><span class="sxs-lookup"><span data-stu-id="b176c-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="b176c-177">Editar recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="b176c-178">Desconexión de un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-178">Take a share offline</span></span>

<span data-ttu-id="b176c-179">Puede que necesite tootake sin conexión un recurso compartido si tiene previsto toomodify lo o delete.</span><span class="sxs-lookup"><span data-stu-id="b176c-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="b176c-180">Cuando un recurso compartido está desconectado, no está disponible para el acceso de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="b176c-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="b176c-181">Necesitará tootake Hola recursos compartidos sin conexión en el host de hello, así como en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="b176c-182">tootake un recurso compartido sin conexión</span><span class="sxs-lookup"><span data-stu-id="b176c-182">tootake a share offline</span></span>

1. <span data-ttu-id="b176c-183">Asegúrese de que ese recurso compartido de hello en cuestión no está en uso antes de desconectarlo.</span><span class="sxs-lookup"><span data-stu-id="b176c-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="b176c-184">Quitarle participación de hello en la matriz de hello sin conexión mediante la realización de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="b176c-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="b176c-185">De hello **recursos compartidos** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el recurso compartido que le gustaría tootake sin conexión.</span><span class="sxs-lookup"><span data-stu-id="b176c-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="b176c-186">**Seleccione** recurso compartido de Hola y haga clic en **...**  (o bien pulse el botón derecho en esta fila) y en el menú contextual de hello, seleccione **desconectar**.</span><span class="sxs-lookup"><span data-stu-id="b176c-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Recurso compartido sin conexión](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="b176c-188">Revise la información de Hola Hola **desconectar** hoja y confirmar la aceptación de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="b176c-189">Haga clic en **desconectar** compartir de hello tootake sin conexión.</span><span class="sxs-lookup"><span data-stu-id="b176c-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="b176c-190">Verá una notificación de Hola la operación en curso.</span><span class="sxs-lookup"><span data-stu-id="b176c-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="b176c-191">tooconfirm que Hola recurso compartido se realizó correctamente sin conexión, vaya toohello **recursos compartidos** hoja.</span><span class="sxs-lookup"><span data-stu-id="b176c-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="b176c-192">Debería ver estado de saludo del recurso compartido de hello como sin conexión.</span><span class="sxs-lookup"><span data-stu-id="b176c-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="b176c-193">Eliminación de un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b176c-194">Puede eliminar un recurso compartido solo si está desconectado.</span><span class="sxs-lookup"><span data-stu-id="b176c-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="b176c-195">Hola completa siguiendo los pasos toodelete un recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="b176c-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="b176c-196">toodelete un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="b176c-196">toodelete a share</span></span>

1. <span data-ttu-id="b176c-197">De hello **recursos compartidos** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en el recurso compartido de hello desea toodelete reside.</span><span class="sxs-lookup"><span data-stu-id="b176c-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="b176c-198">**Seleccione** recurso compartido de Hola y haga clic en **...**  (o bien pulse el botón derecho en esta fila) y en el menú contextual de hello, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="b176c-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Eliminación del recurso compartido](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="b176c-200">Comprobar el estado de saludo del recurso compartido de Hola que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="b176c-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="b176c-201">Si desea toodelete de recurso compartido de hello no está desconectado, desconéctelo primero.</span><span class="sxs-lookup"><span data-stu-id="b176c-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="b176c-202">Siga los pasos de hello en [poner sin conexión un recurso compartido de](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="b176c-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="b176c-203">Cuando se le pida confirmación en hello **eliminar** hoja, acepte la confirmación de Hola y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="b176c-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="b176c-204">recurso compartido de Hola se eliminará y Hola **recursos compartidos** hoja muestra la lista de hello actualizado de recursos compartidos dentro de la matriz virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="b176c-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b176c-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b176c-205">Next steps</span></span>
<span data-ttu-id="b176c-206">Obtenga información acerca de cómo demasiado[clonar un recurso compartido de StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="b176c-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

