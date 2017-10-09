---
title: Actualizaciones de aaaInstall en StorSimple Virtual Array | Documentos de Microsoft
description: "Describe cómo toouse actualizaciones de tooapply de la interfaz de usuario de hello StorSimple Virtual Array web mediante hello Azure portal y la revisión (método)"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/07/2017
ms.author: alkohli
ms.openlocfilehash: 6165b305fb0d404b404cf3a11dd0ade2f2f13b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a><span data-ttu-id="a56ef-103">Instalación de Update 0.4 en StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="a56ef-103">Install Update 0.4 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="a56ef-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a56ef-104">Overview</span></span>

<span data-ttu-id="a56ef-105">Este artículo describe Hola pasos necesarios tooinstall actualización 0,4 en la matriz Virtual de StorSimple a través de la interfaz de usuario de web local de Hola y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a56ef-105">This article describes hello steps required tooinstall Update 0.4 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="a56ef-106">Debe tookeep de revisiones o actualizaciones de software de tooapply la matriz Virtual de StorSimple actualizado.</span><span class="sxs-lookup"><span data-stu-id="a56ef-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="a56ef-107">Tenga en cuenta que al instalar una actualización o revisión, se reiniciará el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a56ef-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="a56ef-108">Dado que hello StorSimple Virtual Array es un dispositivo de nodo único, se interrumpe cualquier E/S en curso y el dispositivo produce un tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="a56ef-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="a56ef-109">Antes de aplicar una actualización, se recomienda que permitirán que los volúmenes de Hola o recursos compartidos sin conexión en hello hospedan en primer lugar y, a continuación, Hola dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a56ef-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="a56ef-110">Esto minimizará la posibilidad de daños en los datos.</span><span class="sxs-lookup"><span data-stu-id="a56ef-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a56ef-111">Si está ejecutando Update 0,1 o versiones de software de disponibilidad general, debe usar el método de revisión de hello a través de la interfaz de usuario tooinstall update 0.3 de hello web local.</span><span class="sxs-lookup"><span data-stu-id="a56ef-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="a56ef-112">Si está ejecutando Update 0,2 o una versión posterior, se recomienda que instala actualizaciones de Hola a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a56ef-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span>
 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="a56ef-113">Usar la interfaz de usuario de web local Hola</span><span class="sxs-lookup"><span data-stu-id="a56ef-113">Use hello local web UI</span></span>

<span data-ttu-id="a56ef-114">Cuando se usa la interfaz de usuario de web local de hello, hay dos pasos:</span><span class="sxs-lookup"><span data-stu-id="a56ef-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="a56ef-115">Descargar la actualización de Hola o una revisión de Hola</span><span class="sxs-lookup"><span data-stu-id="a56ef-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="a56ef-116">Instalar la actualización de Hola o revisión de Hola</span><span class="sxs-lookup"><span data-stu-id="a56ef-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="a56ef-117">Descargar la actualización de Hola o una revisión de Hola</span><span class="sxs-lookup"><span data-stu-id="a56ef-117">Download hello update or hello hotfix</span></span>

<span data-ttu-id="a56ef-118">Realizar Hola tras la actualización de software de pasos toodownload Hola de Hola catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="a56ef-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="a56ef-119">revisión de actualización u Hola Hola toodownload</span><span class="sxs-lookup"><span data-stu-id="a56ef-119">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="a56ef-120">Inicie Internet Explorer y vaya demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a56ef-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="a56ef-121">Si se trata de la primera vez mediante Hola catálogo de Microsoft Update en este equipo, haga clic en **instalar** cuando tooinstall solicitada Hola complemento del catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="a56ef-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="a56ef-122">En el cuadro de búsqueda de Hola de hello catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de Hola de revisión de hello desea toodownload.</span><span class="sxs-lookup"><span data-stu-id="a56ef-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="a56ef-123">Escriba **3216577** para Update 0.4 y, luego, haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-123">Enter **3216577** for Update 0.4, and then click **Search**.</span></span>
   
    <span data-ttu-id="a56ef-124">Hello revisión aparece listado, por ejemplo, **StorSimple Virtual Array Update 0,4**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.4**.</span></span>
   
    ![Búsqueda de catálogo](./media/storsimple-virtual-array-install-update-04/download1.png)

4. <span data-ttu-id="a56ef-126">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-126">Click **Add**.</span></span> <span data-ttu-id="a56ef-127">actualización de Hola se agrega toohello cesta.</span><span class="sxs-lookup"><span data-stu-id="a56ef-127">hello update is added toohello basket.</span></span>

5. <span data-ttu-id="a56ef-128">Haga clic en **Ver cesta**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="a56ef-129">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-129">Click **Download**.</span></span> <span data-ttu-id="a56ef-130">Especifique o **examinar** tooa ubicación local donde desee Hola descarga tooappear.</span><span class="sxs-lookup"><span data-stu-id="a56ef-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="a56ef-131">Hello las actualizaciones se descargan toohello ubicación especificada y se coloca en una subcarpeta con el mismo nombre como actualización de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="a56ef-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="a56ef-132">carpeta de Hello también puede ser copiado tooa recurso compartido de red que sea accesible desde el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a56ef-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

7. <span data-ttu-id="a56ef-133">Abra Hola copiado la carpeta, debería ver un archivo de paquete independiente de Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="a56ef-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="a56ef-134">Este archivo es utilizado tooinstall Hola actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="a56ef-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="a56ef-135">Instalar la actualización de Hola o revisión de Hola</span><span class="sxs-lookup"><span data-stu-id="a56ef-135">Install hello update or hello hotfix</span></span>

<span data-ttu-id="a56ef-136">Instalación de actualización o revisión de toohello anteriores, asegúrese de que tiene Hola actualización o revisión Hola descargado localmente en el host o accesible a través de un recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="a56ef-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="a56ef-137">Usar este método tooinstall actualiza en un dispositivo que ejecuta GA o actualizar 0.1 versiones de software.</span><span class="sxs-lookup"><span data-stu-id="a56ef-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="a56ef-138">Este procedimiento toma inferior toocomplete de 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="a56ef-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="a56ef-139">Realizar Hola siguientes pasos tooinstall Hola actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="a56ef-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="a56ef-140">revisión de actualización u Hola Hola tooinstall</span><span class="sxs-lookup"><span data-stu-id="a56ef-140">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="a56ef-141">En la interfaz de usuario web local de hello, vaya demasiado**mantenimiento** > **actualización de Software**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="a56ef-143">En **ruta de acceso de archivo de actualización**, escriba el nombre de archivo de hello para la actualización de Hola u Hola revisión.</span><span class="sxs-lookup"><span data-stu-id="a56ef-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="a56ef-144">También puede examinar los archivos de instalación de actualización o revisión de toohello si se coloca en un recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="a56ef-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="a56ef-145">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-145">Click **Apply**.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="a56ef-147">Se mostrará una advertencia.</span><span class="sxs-lookup"><span data-stu-id="a56ef-147">A warning is displayed.</span></span> <span data-ttu-id="a56ef-148">Debido a esto es un dispositivo de nodo único, después de que se aplica la actualización de hello, Hola dispositivo se reinicia y no hay tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="a56ef-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="a56ef-149">Haga clic en el icono de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a56ef-149">Click hello check icon.</span></span>
   
   ![actualizar dispositivo](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="a56ef-151">inicia la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="a56ef-151">hello update starts.</span></span> <span data-ttu-id="a56ef-152">Después de que el dispositivo de Hola se actualizó correctamente, éste se reinicia.</span><span class="sxs-lookup"><span data-stu-id="a56ef-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="a56ef-153">Hello interfaz de usuario local no es accesible durante este proceso.</span><span class="sxs-lookup"><span data-stu-id="a56ef-153">hello local UI is not accessible in this duration.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="a56ef-155">Una vez completado el reinicio de hello, se toman toohello **iniciar sesión en** página.</span><span class="sxs-lookup"><span data-stu-id="a56ef-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="a56ef-156">tooverify que ha actualizado el software de dispositivo de hello, en web local de hello interfaz de usuario, vaya demasiado**mantenimiento** > **actualización de Software**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="a56ef-157">Hello muestra la versión de software debe tener **10.0.0.0.0.10289.0** para actualización 0.4.</span><span class="sxs-lookup"><span data-stu-id="a56ef-157">hello displayed software version should be **10.0.0.0.0.10289.0** for Update 0.4.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a56ef-158">Se informan de versiones de software de Hola de forma ligeramente diferente en la interfaz de usuario de web local de Hola y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a56ef-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="a56ef-159">Por ejemplo, Hola informes de interfaz de usuario web local **10.0.0.0.0.10289** y Hola informes del portal Azure **10.0.10289.0** para hello misma versión.</span><span class="sxs-lookup"><span data-stu-id="a56ef-159">For example, hello local web UI reports **10.0.0.0.0.10289** and hello Azure portal reports **10.0.10289.0** for hello same version.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a><span data-ttu-id="a56ef-161">Usar hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a56ef-161">Use hello Azure portal</span></span>

<span data-ttu-id="a56ef-162">Si ejecuta Update 0.2 y versiones posteriores, se recomienda que instale las actualizaciones a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a56ef-162">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="a56ef-163">procedimiento portal Hola requiere Hola usuario tooscan, descargue e instale las actualizaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a56ef-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="a56ef-164">Este procedimiento toma toocomplete unos 7 minutos.</span><span class="sxs-lookup"><span data-stu-id="a56ef-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="a56ef-165">Realizar Hola siguientes pasos tooinstall Hola actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="a56ef-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="a56ef-166">Después de hello instalación es tooyour vaya completa (según se indica por el estado del trabajo al 100%), el servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a56ef-166">After hello installation is complete (as indicated by job status at 100 %), go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="a56ef-167">Seleccione **dispositivos** y, a continuación, seleccione y haga clic en dispositivo de Hola que desee tooupdate de lista de Hola de dispositivos conectados toothis servicio.</span><span class="sxs-lookup"><span data-stu-id="a56ef-167">Select **Devices** and then select and click hello device you want tooupdate from hello list of devices connected toothis service.</span></span> <span data-ttu-id="a56ef-168">Hola **configuración** hoja, vaya demasiado**administrar** sección y seleccione **actualizaciones del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-168">In hello **Settings** blade, go too**Manage** section and select **Device updates**.</span></span> <span data-ttu-id="a56ef-169">Hello muestra la versión de software debe tener **10.0.10289.0**.</span><span class="sxs-lookup"><span data-stu-id="a56ef-169">hello displayed software version should be **10.0.10289.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a56ef-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a56ef-170">Next steps</span></span>

<span data-ttu-id="a56ef-171">Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a56ef-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

