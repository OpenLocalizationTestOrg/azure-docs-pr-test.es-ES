---
title: "Instalación de Update 0.6 en StorSimple Virtual Array | Microsoft Docs"
description: "Describe cómo usar la IU web de StorSimple Virtual Array para aplicar actualizaciones mediante Azure Portal y el método de revisiones"
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
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 111976cd684561f5bc63b92f09a20470fe3036d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a><span data-ttu-id="f3a20-103">Instalación de Update 0.6 en StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="f3a20-103">Install Update 0.6 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="f3a20-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f3a20-104">Overview</span></span>

<span data-ttu-id="f3a20-105">En este artículo se describen los pasos requeridos para instalar Update 0.6 en StorSimple Virtual Array a través tanto de la interfaz de usuario web local como de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f3a20-105">This article describes the steps required to install Update 0.6 on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="f3a20-106">Se aplican las actualizaciones o revisiones de software para mantener actualizada la matriz virtual de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f3a20-106">You apply the software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="f3a20-107">Antes de aplicar una actualización, se recomienda que desconecte primero los volúmenes o recursos compartidos en el host y, luego, el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3a20-107">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="f3a20-108">Esto minimizará la posibilidad de daños en los datos.</span><span class="sxs-lookup"><span data-stu-id="f3a20-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="f3a20-109">Cuando los volúmenes o recursos compartidos están sin conexión, también debe realizar una copia de seguridad manual del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3a20-109">After the volumes or shares are offline, you should also take a manual backup of the device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="f3a20-110">Update 0.6 se corresponde a la versión de software **10.0.10293.0** del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3a20-110">Update 0.6 corresponds to **10.0.10293.0** software version on your device.</span></span> <span data-ttu-id="f3a20-111">Para obtener más información sobre cuáles son las novedades de esta actualización, vaya a las [Notas de la versión de Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="f3a20-111">For information on what is new in this update, go to [Release notes for Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span></span>
>
> - <span data-ttu-id="f3a20-112">Si ejecuta Update 0.2, o cualquier versión posterior, se recomienda instalar las actualizaciones a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f3a20-112">If you are running Update 0.2 or later, we recommend that you install the updates via the Azure portal.</span></span> <span data-ttu-id="f3a20-113">Si está ejecutando Update 0.1 o versiones de software de GA, debe utilizar el método de revisión mediante la interfaz de usuario web local para instalar Update 0.6.</span><span class="sxs-lookup"><span data-stu-id="f3a20-113">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install Update 0.6.</span></span>
>
> - <span data-ttu-id="f3a20-114">Tenga en cuenta que al instalar una actualización o revisión, se reiniciará el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3a20-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="f3a20-115">Dado que la matriz virtual de StorSimple es un dispositivo de nodo único, se interrumpirá cualquier operación de E/S que esté en curso y el dispositivo permanecerá un rato inactivo.</span><span class="sxs-lookup"><span data-stu-id="f3a20-115">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="f3a20-116">Uso del Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f3a20-116">Use the Azure portal</span></span>

<span data-ttu-id="f3a20-117">Si se ejecuta Update 0.2, o cualquier versión posterior, se recomienda instalar las actualizaciones mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f3a20-117">If running Update 0.2 and later, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="f3a20-118">El procedimiento del Portal requiere que el usuario examine, descargue e instale las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="f3a20-118">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="f3a20-119">Este procedimiento tarda aproximadamente 7 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="f3a20-119">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="f3a20-120">Realice los pasos siguientes para instalar la actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="f3a20-120">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="f3a20-121">Una vez que la instalación esté completa, vaya a su servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="f3a20-121">After the installation is complete, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="f3a20-122">Seleccione **Dispositivos** y, a continuación, seleccione y haga clic en el dispositivo que acaba de actualizar.</span><span class="sxs-lookup"><span data-stu-id="f3a20-122">Select **Devices** and then select and click the device you just updated.</span></span> <span data-ttu-id="f3a20-123">Vaya a **Configuración > Administrar > Actualizaciones del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="f3a20-123">Go to **Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="f3a20-124">La versión de software que aparece debe ser **10.0.10293.0**.</span><span class="sxs-lookup"><span data-stu-id="f3a20-124">The displayed software version should be **10.0.10293.0**.</span></span>

## <a name="use-the-local-web-ui"></a><span data-ttu-id="f3a20-125">Uso de la interfaz de usuario web local</span><span class="sxs-lookup"><span data-stu-id="f3a20-125">Use the local web UI</span></span>

<span data-ttu-id="f3a20-126">Se pueden seguir dos pasos con la interfaz de usuario web local:</span><span class="sxs-lookup"><span data-stu-id="f3a20-126">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="f3a20-127">Descargar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="f3a20-127">Download the update or the hotfix</span></span>
* <span data-ttu-id="f3a20-128">Instalar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="f3a20-128">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="f3a20-129">Descargar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="f3a20-129">Download the update or the hotfix</span></span>

<span data-ttu-id="f3a20-130">Realice los pasos siguientes para descargar la actualización de software desde el catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="f3a20-130">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="f3a20-131">Para descargar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="f3a20-131">To download the update or the hotfix</span></span>

1. <span data-ttu-id="f3a20-132">Inicie Internet Explorer y vaya a [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f3a20-132">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="f3a20-133">Si esta es la primera vez que utiliza el Catálogo de Microsoft Update en este equipo, haga clic en **Instalar** cuando se le solicite que instale el complemento del Catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="f3a20-133">If you are using the Microsoft Update Catalog for the first time on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="f3a20-134">En el cuadro de búsqueda del Catálogo de Microsoft Update, escriba el número de Knowledge Base correspondiente a la revisión que quiera descargar.</span><span class="sxs-lookup"><span data-stu-id="f3a20-134">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="f3a20-135">Escriba **4023268** para Update 0.6 y, luego, haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="f3a20-135">Enter **4023268** for Update 0.6, and then click **Search**.</span></span>
   
    <span data-ttu-id="f3a20-136">Aparece la lista de revisiones, por ejemplo, **StorSimple Virtual Array Update 0.6**.</span><span class="sxs-lookup"><span data-stu-id="f3a20-136">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.6**.</span></span>
   
    ![Búsqueda de catálogo](./media/storsimple-virtual-array-install-update-06/download1.png)

4. <span data-ttu-id="f3a20-138">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="f3a20-138">Click **Download**.</span></span>

5. <span data-ttu-id="f3a20-139">Debería ver cinco archivos para descargar.</span><span class="sxs-lookup"><span data-stu-id="f3a20-139">You should see five files to download.</span></span> <span data-ttu-id="f3a20-140">Descargue cada uno de esos archivos en una carpeta.</span><span class="sxs-lookup"><span data-stu-id="f3a20-140">Download each of those files to a folder.</span></span> <span data-ttu-id="f3a20-141">La carpeta también se puede copiar en un recurso compartido de red que sea accesible desde el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3a20-141">The folder can also be copied to a network share that is reachable from the device.</span></span>

6. <span data-ttu-id="f3a20-142">Abra la carpeta donde se encuentran los archivos.</span><span class="sxs-lookup"><span data-stu-id="f3a20-142">Open the folder where the files are located.</span></span>
    <span data-ttu-id="f3a20-143">![Archivos del paquete](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span><span class="sxs-lookup"><span data-stu-id="f3a20-143">![Files in the package](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span></span>

    <span data-ttu-id="f3a20-144">Se ve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3a20-144">You see:</span></span>
    -  <span data-ttu-id="f3a20-145">Un archivo de paquete independiente de Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="f3a20-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="f3a20-146">Este archivo se utiliza para actualizar el software del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3a20-146">This file is used to update the device software.</span></span>
    - <span data-ttu-id="f3a20-147">Un archivo de paquete del agente de supervisión de Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="f3a20-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="f3a20-148">Este archivo se utiliza para actualizar el agente del servicio de supervisión y diagnóstico (MDS).</span><span class="sxs-lookup"><span data-stu-id="f3a20-148">This file is used to update the Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="f3a20-149">Haga doble clic en el archivo cab.</span><span class="sxs-lookup"><span data-stu-id="f3a20-149">Double-click the cab file.</span></span> <span data-ttu-id="f3a20-150">Aparece un archivo _.msi_.</span><span class="sxs-lookup"><span data-stu-id="f3a20-150">A _.msi_ is displayed.</span></span> <span data-ttu-id="f3a20-151">Seleccione el archivo, haga clic con el botón derecho sobre él y, a continuación, **extraiga** el archivo.</span><span class="sxs-lookup"><span data-stu-id="f3a20-151">Select the file, right-click, and then **Extract** the file.</span></span> <span data-ttu-id="f3a20-152">Se usa el archivo _.msi_ para actualizar el agente.</span><span class="sxs-lookup"><span data-stu-id="f3a20-152">You use the _.msi_ file to update the agent.</span></span>

        ![Extracción del archivo de actualización del agente de MDS](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > <span data-ttu-id="f3a20-154">No es necesario actualizar al agente MDS si está ejecutando StorSimple Update 0.5 (0.0.10293.0).</span><span class="sxs-lookup"><span data-stu-id="f3a20-154">You do not need to update the MDS agent if you are running StorSimple Update 0.5 (0.0.10293.0).</span></span>

    - <span data-ttu-id="f3a20-155">Tres archivos que contienen actualizaciones críticas de seguridad de Windows: `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64` y `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="f3a20-155">Three files that contain critical Windows security updates, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span>


### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="f3a20-156">Instalar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="f3a20-156">Install the update or the hotfix</span></span>

<span data-ttu-id="f3a20-157">Antes de instalar la actualización o la revisión, asegúrese de que tiene la actualización o la revisión descargada de forma local en el host o que puede acceder a ella a través de un recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="f3a20-157">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="f3a20-158">Utilice este método para instalar actualizaciones en un dispositivo que ejecute las versiones de software Update 0.1 o GA.</span><span class="sxs-lookup"><span data-stu-id="f3a20-158">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="f3a20-159">Este procedimiento tarda aproximadamente doce minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="f3a20-159">This procedure takes approximately 12 minutes to complete.</span></span> <span data-ttu-id="f3a20-160">Realice los pasos siguientes para instalar la actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="f3a20-160">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="f3a20-161">Instalar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="f3a20-161">To install the update or the hotfix</span></span>

1. <span data-ttu-id="f3a20-162">En la interfaz de usuario web local, vaya a **Mantenimiento** > **Actualización de software**.</span><span class="sxs-lookup"><span data-stu-id="f3a20-162">In the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="f3a20-163">Tome nota de la versión de software que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="f3a20-163">Make a note of the software version that you are running.</span></span> <span data-ttu-id="f3a20-164">Si está ejecutando **10.0.10290.0**, no es necesario actualizar el agente MDS en el paso 6.</span><span class="sxs-lookup"><span data-stu-id="f3a20-164">If you are running **10.0.10290.0**, you do not need to update the MDS agent in step 6.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="f3a20-166">En **Update file path**(Ruta de acceso del archivo de actualización), escriba el nombre del archivo de actualización o de revisión.</span><span class="sxs-lookup"><span data-stu-id="f3a20-166">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="f3a20-167">Asimismo, también puede acceder al archivo de instalación de la actualización o de la revisión si está en un recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="f3a20-167">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="f3a20-168">Haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="f3a20-168">Click **Apply**.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="f3a20-170">Se mostrará una advertencia.</span><span class="sxs-lookup"><span data-stu-id="f3a20-170">A warning is displayed.</span></span> <span data-ttu-id="f3a20-171">Dado que la matriz virtual es un dispositivo de nodo único, una vez aplicada la actualización, se reiniciará el dispositivo y habrá un tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="f3a20-171">Given the virtual array is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="f3a20-172">Haga clic en el icono de marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="f3a20-172">Click the check icon.</span></span>
   
   ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="f3a20-174">Se inicia la actualización.</span><span class="sxs-lookup"><span data-stu-id="f3a20-174">The update starts.</span></span> <span data-ttu-id="f3a20-175">Una vez que el dispositivo se actualice correctamente, este se reiniciará.</span><span class="sxs-lookup"><span data-stu-id="f3a20-175">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="f3a20-176">La interfaz de usuario local no será accesible durante este tiempo.</span><span class="sxs-lookup"><span data-stu-id="f3a20-176">The local UI is not accessible in this duration.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="f3a20-178">Una vez completado el reinicio, se le llevará a la página de **inicio de sesión** .</span><span class="sxs-lookup"><span data-stu-id="f3a20-178">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="f3a20-179">Para comprobar que el software del dispositivo se ha actualizado, en la interfaz de usuario de web local, vaya a **Mantenimiento** > **Actualización de software**.</span><span class="sxs-lookup"><span data-stu-id="f3a20-179">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="f3a20-180">La versión de software que aparece debe ser **10.0.0.0.0.10293** para Update 0.6.</span><span class="sxs-lookup"><span data-stu-id="f3a20-180">The displayed software version should be **10.0.0.0.0.10293** for Update 0.6.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f3a20-181">Las versiones de software se muestran de forma ligeramente distinta en la interfaz de usuario web local y Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f3a20-181">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="f3a20-182">Por ejemplo, la misma versión aparece como **10.0.0.0.0.10293** en la interfaz de usuario web local y como **10.0.10293.0** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f3a20-182">For example, the local web UI reports **10.0.0.0.0.10293** and the Azure portal reports **10.0.10293.0** for the same version.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. <span data-ttu-id="f3a20-184">Omita este paso si se estaba ejecutando StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) antes de aplicar esta actualización.</span><span class="sxs-lookup"><span data-stu-id="f3a20-184">Skip this step if you were running StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) before you applied this update.</span></span> <span data-ttu-id="f3a20-185">Tomó nota de la versión de software en el paso 1 antes de iniciar la actualización.</span><span class="sxs-lookup"><span data-stu-id="f3a20-185">You made a note of the software version in step 1 before you began to update.</span></span> <span data-ttu-id="f3a20-186">Si estaba ejecutando Update 0.5, el agente MDS ya está actualizado.</span><span class="sxs-lookup"><span data-stu-id="f3a20-186">If you were running Update 0.5, your MDS agent is already up-to-date .</span></span>

    <span data-ttu-id="f3a20-187">Si está ejecutando una versión de software anterior a Update 0.5, lo siguiente que debe hacer es actualizar el agente MDS.</span><span class="sxs-lookup"><span data-stu-id="f3a20-187">If you are running a software version prior to Update 0.5, the next step for you is to update the MDS agent.</span></span> <span data-ttu-id="f3a20-188">En la página **Actualización de software**, vaya a **Actualizar ruta de acceso al archivo** y vaya al archivo `GenevaMonitoringAgentPackageInstaller.msi`.</span><span class="sxs-lookup"><span data-stu-id="f3a20-188">In the **Software Update** page, go to the **Update file path** and browse to the `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="f3a20-189">Repita los pasos del 2 al 4.</span><span class="sxs-lookup"><span data-stu-id="f3a20-189">Repeat steps 2-4.</span></span> <span data-ttu-id="f3a20-190">Después de que se reinicie la matriz virtual, inicie sesión en la interfaz de usuario web local.</span><span class="sxs-lookup"><span data-stu-id="f3a20-190">After the virtual array restarts, sign into the local web UI.</span></span>

7. <span data-ttu-id="f3a20-191">Repita los pasos del 2 al 4 para instalar las correcciones de seguridad de Windows con los archivos `windows8.1-kb4012213-x64`, `windows8.1-kb3205400-x64` y `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="f3a20-191">Repeat step 2-4 to install the Windows security fixes using files `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span> <span data-ttu-id="f3a20-192">La matriz virtual se reinicia después de cada instalación y debe iniciar sesión en la interfaz de usuario web local.</span><span class="sxs-lookup"><span data-stu-id="f3a20-192">The virtual array restarts after each install and you need to sign into the local web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3a20-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3a20-193">Next steps</span></span>

<span data-ttu-id="f3a20-194">Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="f3a20-194">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

