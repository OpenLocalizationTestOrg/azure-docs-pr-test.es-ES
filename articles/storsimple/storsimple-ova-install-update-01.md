---
title: "Instalación de actualizaciones en la matriz virtual de StorSimple | Microsoft Docs"
description: "Se describe cómo usar la interfaz de usuario web de la matriz virtual de StorSimple para aplicar actualizaciones mediante el portal y el método de revisiones."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: bccb0d49c1959a690d513961c32d946763385a87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="dc791-103">Instalación de actualizaciones en la matriz virtual de StorSimple</span><span class="sxs-lookup"><span data-stu-id="dc791-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="dc791-104">Información general</span><span class="sxs-lookup"><span data-stu-id="dc791-104">Overview</span></span>
<span data-ttu-id="dc791-105">En este artículo se describen los pasos necesarios para instalar actualizaciones en la matriz virtual de StorSimple mediante la interfaz de usuario web local y el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="dc791-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure classic portal.</span></span> <span data-ttu-id="dc791-106">Deberá aplicar alguna actualización o revisión de software para mantener actualizada la matriz virtual de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dc791-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="dc791-107">Tenga en cuenta que al instalar una actualización o revisión, se reiniciará el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dc791-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="dc791-108">Dado que la matriz virtual de StorSimple es un dispositivo de nodo único, se interrumpirá cualquier operación de E/S que esté en curso y el dispositivo permanecerá un rato inactivo.</span><span class="sxs-lookup"><span data-stu-id="dc791-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="dc791-109">Antes de aplicar una actualización, se recomienda que desconecte primero los volúmenes o recursos compartidos en el host y, luego, el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dc791-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="dc791-110">Esto minimizará la posibilidad de daños en los datos.</span><span class="sxs-lookup"><span data-stu-id="dc791-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc791-111">Si está ejecutando Update 0.1 o versiones de software de GA, debe utilizar el método de revisión a través de la interfaz de usuario web local para instalar Update 0.3.</span><span class="sxs-lookup"><span data-stu-id="dc791-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="dc791-112">Si ejecuta Update 0.2, recomendamos que instale las actualizaciones a través del Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="dc791-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
> 
> 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="dc791-113">Uso de la interfaz de usuario web local</span><span class="sxs-lookup"><span data-stu-id="dc791-113">Use the local web UI</span></span>
<span data-ttu-id="dc791-114">Se pueden seguir dos pasos con la interfaz de usuario web local:</span><span class="sxs-lookup"><span data-stu-id="dc791-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="dc791-115">Descargar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="dc791-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="dc791-116">Instalar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="dc791-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="dc791-117">Descargar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="dc791-117">Download the update or the hotfix</span></span>
<span data-ttu-id="dc791-118">Realice los pasos siguientes para descargar la actualización de software desde el catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="dc791-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="dc791-119">Para descargar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="dc791-119">To download the update or the hotfix</span></span>
1. <span data-ttu-id="dc791-120">Inicie Internet Explorer y vaya a [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="dc791-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="dc791-121">Si esta es la primera vez que utiliza el Catálogo de Microsoft Update en este equipo, haga clic en **Instalar** cuando se le solicite que instale el complemento del Catálogo de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="dc791-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="dc791-122">En el cuadro de búsqueda del Catálogo de Microsoft Update, escriba el número de Knowledge Base correspondiente a la revisión que quiera descargar.</span><span class="sxs-lookup"><span data-stu-id="dc791-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="dc791-123">Escriba **3182061** para Update 0.3 y luego haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="dc791-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="dc791-124">Aparece la lista de revisiones, por ejemplo, **StorSimple Virtual Array Update 0.3**.</span><span class="sxs-lookup"><span data-stu-id="dc791-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Búsqueda de catálogo](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="dc791-126">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dc791-126">Click **Add**.</span></span> <span data-ttu-id="dc791-127">La actualización se agrega a la cesta.</span><span class="sxs-lookup"><span data-stu-id="dc791-127">The update is added to the basket.</span></span>
5. <span data-ttu-id="dc791-128">Haga clic en **Ver cesta**.</span><span class="sxs-lookup"><span data-stu-id="dc791-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="dc791-129">Haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="dc791-129">Click **Download**.</span></span> <span data-ttu-id="dc791-130">Especifique o **busque** una ubicación local en la que quiera que aparezcan las descargas.</span><span class="sxs-lookup"><span data-stu-id="dc791-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="dc791-131">Las actualizaciones se descargan en la ubicación especificada y se colocan en una subcarpeta con el mismo nombre que la actualización.</span><span class="sxs-lookup"><span data-stu-id="dc791-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="dc791-132">La carpeta también se puede copiar en un recurso compartido de red que sea accesible desde el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dc791-132">The folder can also be copied to a network share that is reachable from the device.</span></span>
7. <span data-ttu-id="dc791-133">Abra la carpeta copiada, debería ver un archivo de paquete independiente de Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="dc791-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="dc791-134">Este archivo se utiliza para instalar la actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="dc791-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="dc791-135">Instalar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="dc791-135">Install the update or the hotfix</span></span>
<span data-ttu-id="dc791-136">Antes de instalar la actualización o la revisión, asegúrese de que tiene la actualización o la revisión descargada de forma local en el host o que puede acceder a ella a través de un recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="dc791-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="dc791-137">Utilice este método para instalar actualizaciones en un dispositivo que ejecute las versiones de software Update 0.1 o GA.</span><span class="sxs-lookup"><span data-stu-id="dc791-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="dc791-138">Este procedimiento tarda menos de 2 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="dc791-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="dc791-139">Realice los pasos siguientes para instalar la actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="dc791-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="dc791-140">Instalar la actualización o la revisión</span><span class="sxs-lookup"><span data-stu-id="dc791-140">To install the update or the hotfix</span></span>
1. <span data-ttu-id="dc791-141">En la interfaz de usuario web local, vaya a **Mantenimiento** > **Actualización de software**.</span><span class="sxs-lookup"><span data-stu-id="dc791-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="dc791-143">En **Update file path**(Ruta de acceso del archivo de actualización), escriba el nombre del archivo de actualización o de revisión.</span><span class="sxs-lookup"><span data-stu-id="dc791-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="dc791-144">Asimismo, también puede acceder al archivo de instalación de la actualización o de la revisión si está en un recurso compartido de red.</span><span class="sxs-lookup"><span data-stu-id="dc791-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="dc791-145">Haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="dc791-145">Click **Apply**.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="dc791-147">Se mostrará una advertencia.</span><span class="sxs-lookup"><span data-stu-id="dc791-147">A warning is displayed.</span></span> <span data-ttu-id="dc791-148">Dado que se trata de un dispositivo de nodo único, una vez aplicada la actualización, se reiniciará el dispositivo y habrá un tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="dc791-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="dc791-149">Haga clic en el icono de marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="dc791-149">Click the check icon.</span></span>
   
   ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="dc791-151">Se inicia la actualización.</span><span class="sxs-lookup"><span data-stu-id="dc791-151">The update starts.</span></span> <span data-ttu-id="dc791-152">Una vez que el dispositivo se actualice correctamente, este se reiniciará.</span><span class="sxs-lookup"><span data-stu-id="dc791-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="dc791-153">La interfaz de usuario local no será accesible durante este tiempo.</span><span class="sxs-lookup"><span data-stu-id="dc791-153">The local UI is not accessible in this duration.</span></span>
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="dc791-155">Una vez completado el reinicio, se le llevará a la página de **inicio de sesión** .</span><span class="sxs-lookup"><span data-stu-id="dc791-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="dc791-156">Para comprobar que el software del dispositivo se ha actualizado, en la interfaz de usuario de web local, vaya a **Mantenimiento** > **Actualización de software**.</span><span class="sxs-lookup"><span data-stu-id="dc791-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="dc791-157">La versión de software mostrada debe ser **10.0.0.0.0.10288.0** para Update 0.3.</span><span class="sxs-lookup"><span data-stu-id="dc791-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dc791-158">Las versiones de software se muestran de forma ligeramente distinta en la interfaz de usuario web local y el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="dc791-158">We report the software versions in a slightly different way in the local web UI and the Azure classic portal.</span></span> <span data-ttu-id="dc791-159">Por ejemplo, la misma versión aparece como **10.0.0.0.0.10288** en la interfaz de usuario web local y como **10.0.10288.0** en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="dc791-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure classic portal reports **10.0.10288.0** for the same version.</span></span> 
   > 
   > 
   
    ![actualizar dispositivo](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="dc791-161">Uso del Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="dc791-161">Use the Azure classic portal</span></span>
<span data-ttu-id="dc791-162">Si se ejecuta Update 0.2, recomendamos que instale las actualizaciones a través del Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="dc791-162">If running Update 0.2, we recommend that you install updates through the Azure classic portal.</span></span> <span data-ttu-id="dc791-163">El procedimiento del Portal requiere que el usuario examine, descargue e instale las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="dc791-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="dc791-164">Este procedimiento tarda aproximadamente 7 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="dc791-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="dc791-165">Realice los pasos siguientes para instalar la actualización o revisión.</span><span class="sxs-lookup"><span data-stu-id="dc791-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="dc791-166">Una vez que la instalación esté completa (podrá comprobarlo cuando el estado del trabajo esté al 100 %), vaya a **Dispositivos > Mantenimiento > Actualizaciones de software**.</span><span class="sxs-lookup"><span data-stu-id="dc791-166">After the installation is complete (as indicated by job status at 100 %), go to **Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="dc791-167">La versión de software que aparece debe ser 10.0.10288.0.</span><span class="sxs-lookup"><span data-stu-id="dc791-167">The displayed software version should be 10.0.10288.0.</span></span>

![actualizar dispositivo](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="dc791-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc791-169">Next steps</span></span>
<span data-ttu-id="dc791-170">Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="dc791-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

