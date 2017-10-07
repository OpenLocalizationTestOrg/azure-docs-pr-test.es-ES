---
title: "aaaInstall actualización 0,5 en StorSimple Virtual Array | Documentos de Microsoft"
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
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="617d0-103">Instalación de Update 0.5 en StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="617d0-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="617d0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="617d0-104">Overview</span></span>

<span data-ttu-id="617d0-105">Este artículo describe Hola pasos necesarios tooinstall actualización 0,5 en la matriz Virtual de StorSimple a través de la interfaz de usuario de web local de Hola y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="617d0-105">This article describes hello steps required tooinstall Update 0.5 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="617d0-106">Debe tookeep de revisiones o actualizaciones de software de tooapply la matriz Virtual de StorSimple actualizado.</span><span class="sxs-lookup"><span data-stu-id="617d0-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="617d0-107">Antes de aplicar una actualización, se recomienda que permitirán que los volúmenes de Hola o recursos compartidos sin conexión en hello hospedan en primer lugar y, a continuación, Hola dispositivo.</span><span class="sxs-lookup"><span data-stu-id="617d0-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="617d0-108">Esto minimizará la posibilidad de daños en los datos.</span><span class="sxs-lookup"><span data-stu-id="617d0-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="617d0-109">Después de hello volúmenes o recursos compartidos sin conexión, también debe tener manual de un copia de seguridad del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="617d0-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="617d0-110">Actualización 0,5 corresponde demasiado**10.0.10290.0** versión de software en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="617d0-110">Update 0.5 corresponds too**10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="617d0-111">Para obtener información sobre lo que es nuevo en esta actualización, vaya demasiado[notas de la versión de actualización de 0,5](storsimple-virtual-array-update-05-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="617d0-111">For information on what is new in this update, go too[Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="617d0-112">Si está ejecutando Update 0,2 o una versión posterior, se recomienda que instala actualizaciones de Hola a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="617d0-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="617d0-113">Si está ejecutando Update 0,1 o versiones de software de disponibilidad general, debe usar método de revisión de hello mediante tooinstall de interfaz de usuario web local de hello actualización 0,5.</span><span class="sxs-lookup"><span data-stu-id="617d0-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.5.</span></span>
>
> - <span data-ttu-id="617d0-114">Tenga en cuenta que al instalar una actualización o revisión, se reiniciará el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="617d0-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="617d0-115">Dado que hello StorSimple Virtual Array es un dispositivo de nodo único, se interrumpe cualquier E/S en curso y el dispositivo produce un tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="617d0-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="617d0-116">Usar hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="617d0-116">Use hello Azure portal</span></span>

<span data-ttu-id="617d0-117">Si ejecuta Update 0.2 y versiones posteriores, se recomienda que instale las actualizaciones a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="617d0-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="617d0-118">procedimiento portal Hola requiere Hola usuario tooscan, descargue e instale las actualizaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="617d0-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="617d0-119">Este procedimiento toma toocomplete unos 7 minutos.</span><span class="sxs-lookup"><span data-stu-id="617d0-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="617d0-120">Realizar Hola siguientes pasos tooinstall Hola actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="617d0-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="617d0-121">Después de hello instalación está completa, vaya tooyour servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="617d0-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="617d0-122">Seleccione **dispositivos** y, a continuación, seleccione y haga clic en el dispositivo de Hola que acaba de actualizar.</span><span class="sxs-lookup"><span data-stu-id="617d0-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="617d0-123">Vaya demasiado**configuración > Administrar > actualizaciones del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="617d0-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="617d0-124">Hello muestra la versión de software debe tener **10.0.10290.0**.</span><span class="sxs-lookup"><span data-stu-id="617d0-124">hello displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="617d0-125">Usar la interfaz de usuario de web local Hola</span><span class="sxs-lookup"><span data-stu-id="617d0-125">Use hello local web UI</span></span>

<span data-ttu-id="617d0-126">Cuando se usa la interfaz de usuario de web local de hello, hay dos pasos:</span><span class="sxs-lookup"><span data-stu-id="617d0-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="617d0-127">Descargar la actualización de Hola o una revisión de Hola</span><span class="sxs-lookup"><span data-stu-id="617d0-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="617d0-128">Instalar la actualización de Hola o revisión de Hola</span><span class="sxs-lookup"><span data-stu-id="617d0-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="617d0-129">Descargar la actualización de Hola o una revisión de Hola</span><span class="sxs-lookup"><span data-stu-id="617d0-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="617d0-130">Realizar Hola tras la actualización de software de pasos toodownload Hola de Hola catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="617d0-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="617d0-131">revisión de actualización u Hola Hola toodownload</span><span class="sxs-lookup"><span data-stu-id="617d0-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="617d0-132">Inicie Internet Explorer y vaya demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="617d0-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="617d0-133">Si se trata de la primera vez mediante Hola catálogo de Microsoft Update en este equipo, haga clic en **instalar** cuando tooinstall solicitada Hola complemento del catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="617d0-133">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="617d0-134">En el cuadro de búsqueda de Hola de hello catálogo de Microsoft Update, escriba el número de Knowledge Base (KB) de Hola de revisión de hello desea toodownload.</span><span class="sxs-lookup"><span data-stu-id="617d0-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="617d0-135">Escriba **4021576** para Update 0.5 y luego haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="617d0-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="617d0-136">Hello revisión aparece listado, por ejemplo, **StorSimple Virtual Array Update 0,5**.</span><span class="sxs-lookup"><span data-stu-id="617d0-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![Búsqueda de catálogo](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="617d0-138">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="617d0-138">Click **Download**.</span></span> 

5. <span data-ttu-id="617d0-139">Debería ver dos toodownload de archivos, un *.msu* y un *.cab* archivo.</span><span class="sxs-lookup"><span data-stu-id="617d0-139">You should see two files toodownload, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="617d0-140">Descargar cada una de esas carpetas tooa de archivos.</span><span class="sxs-lookup"><span data-stu-id="617d0-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="617d0-141">carpeta de Hello también puede ser copiado tooa recurso compartido de red que sea accesible desde el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="617d0-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="617d0-142">Abra la carpeta de Hola donde se encuentran los archivos de saludo.</span><span class="sxs-lookup"><span data-stu-id="617d0-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="617d0-143">![Archivos de paquete de Hola](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="617d0-143">![Files in hello package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="617d0-144">Se ve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="617d0-144">You see:</span></span>
    -  <span data-ttu-id="617d0-145">Un archivo de paquete independiente de Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="617d0-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="617d0-146">Este archivo es un software de dispositivo de hello tooupdate usado.</span><span class="sxs-lookup"><span data-stu-id="617d0-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="617d0-147">Un archivo de paquete del agente de supervisión de Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="617d0-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="617d0-148">Este archivo es el agente del servicio (MDS) de supervisión y diagnóstico de hello tooupdate usado.</span><span class="sxs-lookup"><span data-stu-id="617d0-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="617d0-149">Haga doble clic en el archivo cab de Hola.</span><span class="sxs-lookup"><span data-stu-id="617d0-149">Double-click hello cab file.</span></span> <span data-ttu-id="617d0-150">Aparece un archivo .msi.</span><span class="sxs-lookup"><span data-stu-id="617d0-150">A .msi is displayed.</span></span> <span data-ttu-id="617d0-151">Archivo de SELECT hello, menú contextual y, a continuación, **extraer** archivo hello.</span><span class="sxs-lookup"><span data-stu-id="617d0-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="617d0-152">Va a usar hello _.msi_ agente de archivos tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="617d0-152">You will use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Extracción del archivo de actualización del agente de MDS](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="617d0-154">Instalar la actualización de Hola o revisión de Hola</span><span class="sxs-lookup"><span data-stu-id="617d0-154">Install hello update or hello hotfix</span></span>

<span data-ttu-id="617d0-155">Instalación de actualización o revisión de toohello anteriores, asegúrese de que tiene Hola actualización o revisión Hola descargado localmente en el host o accesible a través de un recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="617d0-155">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="617d0-156">Usar este método tooinstall actualiza en un dispositivo que ejecuta GA o actualizar 0.1 versiones de software.</span><span class="sxs-lookup"><span data-stu-id="617d0-156">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="617d0-157">Este procedimiento toma inferior toocomplete de 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="617d0-157">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="617d0-158">Realizar Hola siguientes pasos tooinstall Hola actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="617d0-158">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="617d0-159">revisión de actualización u Hola Hola tooinstall</span><span class="sxs-lookup"><span data-stu-id="617d0-159">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="617d0-160">En la interfaz de usuario web local de hello, vaya demasiado**mantenimiento** > **actualización de Software**.</span><span class="sxs-lookup"><span data-stu-id="617d0-160">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="617d0-162">En **ruta de acceso de archivo de actualización**, escriba el nombre de archivo de hello para la actualización de Hola u Hola revisión.</span><span class="sxs-lookup"><span data-stu-id="617d0-162">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="617d0-163">También puede examinar los archivos de instalación de actualización o revisión de toohello si se coloca en un recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="617d0-163">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="617d0-164">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="617d0-164">Click **Apply**.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="617d0-166">Se mostrará una advertencia.</span><span class="sxs-lookup"><span data-stu-id="617d0-166">A warning is displayed.</span></span> <span data-ttu-id="617d0-167">Debido a esto es un dispositivo de nodo único, después de que se aplica la actualización de hello, Hola dispositivo se reinicia y no hay tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="617d0-167">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="617d0-168">Haga clic en el icono de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="617d0-168">Click hello check icon.</span></span>
   
   ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="617d0-170">inicia la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="617d0-170">hello update starts.</span></span> <span data-ttu-id="617d0-171">Después de que el dispositivo de Hola se actualizó correctamente, éste se reinicia.</span><span class="sxs-lookup"><span data-stu-id="617d0-171">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="617d0-172">Hello interfaz de usuario local no es accesible durante este proceso.</span><span class="sxs-lookup"><span data-stu-id="617d0-172">hello local UI is not accessible in this duration.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="617d0-174">Una vez completado el reinicio de hello, se toman toohello **iniciar sesión en** página.</span><span class="sxs-lookup"><span data-stu-id="617d0-174">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="617d0-175">tooverify que ha actualizado el software de dispositivo de hello, en web local de hello interfaz de usuario, vaya demasiado**mantenimiento** > **actualización de Software**.</span><span class="sxs-lookup"><span data-stu-id="617d0-175">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="617d0-176">Hello muestra la versión de software debe tener **10.0.0.0.0.10290.0** de actualización de 0,5.</span><span class="sxs-lookup"><span data-stu-id="617d0-176">hello displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="617d0-177">Se informan de versiones de software de Hola de forma ligeramente diferente en la interfaz de usuario de web local de Hola y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="617d0-177">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="617d0-178">Por ejemplo, Hola informes de interfaz de usuario web local **10.0.0.0.0.10290** y Hola informes del portal Azure **10.0.10290.0** para hello misma versión.</span><span class="sxs-lookup"><span data-stu-id="617d0-178">For example, hello local web UI reports **10.0.0.0.0.10290** and hello Azure portal reports **10.0.10290.0** for hello same version.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="617d0-180">Hola siguiente paso es agente de tooupdate Hola MDS.</span><span class="sxs-lookup"><span data-stu-id="617d0-180">hello next step is tooupdate hello MDS agent.</span></span> <span data-ttu-id="617d0-181">Hola **actualización de Software** página, vaya toohello **ruta de acceso de archivo de actualización** y examinar toohello `GenevaMonitoringAgentPackageInstaller.msi` archivo.</span><span class="sxs-lookup"><span data-stu-id="617d0-181">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="617d0-182">Repita los pasos del 2 al 4.</span><span class="sxs-lookup"><span data-stu-id="617d0-182">Repeat steps 2-4.</span></span> <span data-ttu-id="617d0-183">Una vez reiniciado matriz virtual hello, inicie sesión en la interfaz de usuario de web local de Hola.</span><span class="sxs-lookup"><span data-stu-id="617d0-183">After hello virtual array restarts, sign into hello local web UI.</span></span>

<span data-ttu-id="617d0-184">actualización de Hello está completa.</span><span class="sxs-lookup"><span data-stu-id="617d0-184">hello update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="617d0-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="617d0-185">Next steps</span></span>

<span data-ttu-id="617d0-186">Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="617d0-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

