---
title: "Preparación del origen y el destino para la replicación de Hyper-V en un sitio secundario con Azure Site Recovery | Microsoft Docs"
description: "Describe cómo configurar el origen y el destino al replicar máquinas virtuales de Hyper-V en un sitio de VMM secundario con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 07135e9b5e619971a59cc22ec68a0a4e8bcaabe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-set-up-the-replication-source-and-target"></a><span data-ttu-id="3da14-103">Paso 6: Configuración de los valores de origen y de destino de la replicación</span><span class="sxs-lookup"><span data-stu-id="3da14-103">Step 6: Set up the replication source and target</span></span>


<span data-ttu-id="3da14-104">Después de crear un almacén de Recovery Services para la replicación de Hyper-V en un sitio de VMM secundario con [Azure Site Recovery](site-recovery-overview.md), use este artículo para configurar las ubicaciones de replicación de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="3da14-104">After creating a Recovery Services vault for Hyper-V replication to a secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article to set up the source and target replication locations.</span></span> 

<span data-ttu-id="3da14-105">Publique cualquier comentario que tenga en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3da14-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-the-source-environment"></a><span data-ttu-id="3da14-106">Configuración del entorno de origen</span><span class="sxs-lookup"><span data-stu-id="3da14-106">Set up the source environment</span></span>

<span data-ttu-id="3da14-107">Instale el proveedor de Azure Site Recovery en servidores VMM, y detecte y registre servidores en el almacén.</span><span class="sxs-lookup"><span data-stu-id="3da14-107">Install the Azure Site Recovery Provider on VMM servers, and discover and register servers in the vault.</span></span>

1. <span data-ttu-id="3da14-108">Haga clic en **Paso 1: Preparar la infraestructura** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="3da14-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Configurar origen](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="3da14-110">En **Preparar origen**, haga clic en **+ VMM** para agregar un servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="3da14-110">In **Prepare source**, click **+ VMM** to add a VMM server.</span></span>

    ![Configurar origen](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="3da14-112">En **Agregar servidor**, compruebe que aparezca el **servidor VMM de System Center** en **Tipo de servidor** y que dicho servidor cumpla los [requisitos previos](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="3da14-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that the VMM server meets the [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="3da14-113">Descargue el archivo de instalación del proveedor de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3da14-113">Download the Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="3da14-114">Descargue la clave de registro.</span><span class="sxs-lookup"><span data-stu-id="3da14-114">Download the registration key.</span></span> <span data-ttu-id="3da14-115">Se le solicitará cuando ejecute el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="3da14-115">You need this when you run setup.</span></span> <span data-ttu-id="3da14-116">La clave será válida durante cinco días a partir del momento en que se genera.</span><span class="sxs-lookup"><span data-stu-id="3da14-116">The key is valid for five days after you generate it.</span></span>

    ![Configurar origen](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="3da14-118">Instale el proveedor de Azure Site Recovery en el servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="3da14-118">Install the Azure Site Recovery Provider on the VMM server.</span></span> <span data-ttu-id="3da14-119">No es necesario instalar explícitamente nada en los servidores host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="3da14-119">You don't need to explicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-the-azure-site-recovery-provider"></a><span data-ttu-id="3da14-120">Instalación del proveedor de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="3da14-120">Install the Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="3da14-121">Ejecute el archivo de instalación del proveedor en cada servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="3da14-121">Run the Provider setup file on each VMM server.</span></span> <span data-ttu-id="3da14-122">Si VMM está implementado en un clúster, siga este procedimiento la primera vez que instale:</span><span class="sxs-lookup"><span data-stu-id="3da14-122">If VMM is deployed in a cluster, do the following the first time you install:</span></span>
    -  <span data-ttu-id="3da14-123">Instale el proveedor en un nodo activo y finalice la instalación para registrar el servidor VMM en el almacén.</span><span class="sxs-lookup"><span data-stu-id="3da14-123">Install the provider on an active node, and finish the installation to register the VMM server in the vault.</span></span>
    - <span data-ttu-id="3da14-124">A continuación, instale el proveedor en los demás nodos.</span><span class="sxs-lookup"><span data-stu-id="3da14-124">Then, install the Provider on the other nodes.</span></span> <span data-ttu-id="3da14-125">Los nodos del clúster deben ejecutar la misma versión del proveedor.</span><span class="sxs-lookup"><span data-stu-id="3da14-125">Cluster nodes should all run the same version of the Provider.</span></span>
2. <span data-ttu-id="3da14-126">El programa de instalación ejecuta algunas comprobaciones de requisitos previos y solicita permiso para detener el servicio VMM.</span><span class="sxs-lookup"><span data-stu-id="3da14-126">Setup runs a few prerequisite checks, and requests permission to stop the VMM service.</span></span> <span data-ttu-id="3da14-127">El servicio VMM se reiniciará automáticamente cuando finalice la instalación.</span><span class="sxs-lookup"><span data-stu-id="3da14-127">The VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="3da14-128">Si lo instala en un clúster VMM, se le pide que detenga el rol de clúster.</span><span class="sxs-lookup"><span data-stu-id="3da14-128">If you install on a VMM cluster, you're prompted to stop the Cluster role.</span></span>
3. <span data-ttu-id="3da14-129">En **Microsoft Update**, puede participar para especificar que las actualizaciones del proveedor se instalen según las directivas de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="3da14-129">In **Microsoft Update**, you can opt in to specify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="3da14-130">En **Instalación**, acepte o modifique la ubicación predeterminada de instalación y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="3da14-130">In **Installation**, accept or modify the default installation location, and click **Install**.</span></span>

    ![Ubicación de instalación](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="3da14-132">Cuando finalice la instalación, haga clic en **Registrar** para registrar el servidor en el almacén.</span><span class="sxs-lookup"><span data-stu-id="3da14-132">After installation is complete, click **Register** to register the server in the vault.</span></span>

    ![Ubicación de instalación](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="3da14-134">En **Nombre del almacén**, compruebe el nombre del almacén en el que se registrará el servidor.</span><span class="sxs-lookup"><span data-stu-id="3da14-134">In **Vault name**, verify the name of the vault in which the server will be registered.</span></span> <span data-ttu-id="3da14-135">Haga clic en *Siguiente*.</span><span class="sxs-lookup"><span data-stu-id="3da14-135">Click *Next*.</span></span>

    ![Registro de servidor](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="3da14-137">En **Conexión a Internet**, especifique cómo se conecta a Azure el proveedor que se ejecuta en el servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="3da14-137">In **Internet Connection**, specify how the provider running on the VMM server connects to Azure.</span></span>

    ![Configuración de Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="3da14-139">Puede especificar que el proveedor debe conectarse a Internet directamente o a través de un proxy.</span><span class="sxs-lookup"><span data-stu-id="3da14-139">You can specify that the provider should connect directly to the internet, or via a proxy.</span></span>
   - <span data-ttu-id="3da14-140">Especifique la configuración de proxy si es necesario.</span><span class="sxs-lookup"><span data-stu-id="3da14-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="3da14-141">Si utiliza un proxy, se crea automáticamente una cuenta de ejecución de VMM (DRAProxyAccount) que usa las credenciales de proxy especificadas.</span><span class="sxs-lookup"><span data-stu-id="3da14-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using the specified proxy credentials.</span></span> <span data-ttu-id="3da14-142">Configure el servidor proxy para que esta cuenta pueda autenticarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="3da14-142">Configure the proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="3da14-143">Se puede modificar la configuración de la cuenta de ejecución en la consola VMM > **Configuración** > **Seguridad** > **Cuentas de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="3da14-143">The RunAs account settings can be modified in the VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="3da14-144">Reinicie el servicio VMM para actualizar los cambios.</span><span class="sxs-lookup"><span data-stu-id="3da14-144">Restart the VMM service to update changes.</span></span>
8. <span data-ttu-id="3da14-145">En **Clave de registro**, seleccione la clave que ha descargado de Azure Site Recovery y copiado en el servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="3da14-145">In **Registration Key**, select the key that you downloaded from Azure Site Recovery and copied to the VMM server.</span></span>
9. <span data-ttu-id="3da14-146">La configuración de cifrado solo se usa cuando se está replicando VM de Hyper-V en nubes de VMM en Azure.</span><span class="sxs-lookup"><span data-stu-id="3da14-146">The encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds to Azure.</span></span> <span data-ttu-id="3da14-147">Si se está replicando en un sitio secundario, no se usa.</span><span class="sxs-lookup"><span data-stu-id="3da14-147">If you're replicating to a secondary site it's not used.</span></span>
10. <span data-ttu-id="3da14-148">En **Nombre del servidor**, especifique un nombre descriptivo para identificar el servidor VMM en el almacén.</span><span class="sxs-lookup"><span data-stu-id="3da14-148">In **Server name**, specify a friendly name to identify the VMM server in the vault.</span></span> <span data-ttu-id="3da14-149">En una configuración de clúster, especifique el nombre del rol de clúster VMM.</span><span class="sxs-lookup"><span data-stu-id="3da14-149">In a cluster configuration specify the VMM cluster role name.</span></span>
11. <span data-ttu-id="3da14-150">En **Sincronizar metadatos en la nube** seleccione si quiere sincronizar los metadatos de todas las nubes del servidor VMM con el almacén.</span><span class="sxs-lookup"><span data-stu-id="3da14-150">In **Synchronize cloud metadata**, select whether you want to synchronize metadata for all clouds on the VMM server with the vault.</span></span> <span data-ttu-id="3da14-151">Esta acción solo se debe ejecutar una vez en cada servidor.</span><span class="sxs-lookup"><span data-stu-id="3da14-151">This action only needs to happen once on each server.</span></span> <span data-ttu-id="3da14-152">Si no desea sincronizar todas las nubes, puede dejar este parámetro sin marcar y sincronizar cada nube individualmente en las propiedades de la nube de la consola de VMM.</span><span class="sxs-lookup"><span data-stu-id="3da14-152">If you don't want to synchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in the cloud properties in the VMM console.</span></span>
12. <span data-ttu-id="3da14-153">Haga clic en **Next** para finalizar el proceso.</span><span class="sxs-lookup"><span data-stu-id="3da14-153">Click **Next** to complete the process.</span></span> <span data-ttu-id="3da14-154">Después del registro, la Recuperación del sitio de Azure recupera los metadatos del servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="3da14-154">After registration, metadata from the VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="3da14-155">El servidor se muestra en la pestaña **Servidores VMM** de la página **Servidores** del almacén.</span><span class="sxs-lookup"><span data-stu-id="3da14-155">The server is displayed on the **VMM Servers** tab on the **Servers** page in the vault.</span></span>

    ![Server](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="3da14-157">Después de que el servidor esté disponible en la consola de Site Recovery, en **Origen** > **Preparar origen** , seleccione el servidor VMM y la nube en la que se encuentra el host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="3da14-157">After the server is available in the Site Recovery console, in **Source** > **Prepare source** select the VMM server, and select the cloud in which the Hyper-V host is located.</span></span> <span data-ttu-id="3da14-158">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3da14-158">Then click **OK**.</span></span>

<span data-ttu-id="3da14-159">También puede instalar el proveedor desde la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="3da14-159">You can also install the provider from the command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-the-target-environment"></a><span data-ttu-id="3da14-160">Configuración del entorno de destino</span><span class="sxs-lookup"><span data-stu-id="3da14-160">Set up the target environment</span></span>

<span data-ttu-id="3da14-161">Seleccione el servidor VMM y la nube de destino:</span><span class="sxs-lookup"><span data-stu-id="3da14-161">Select the target VMM server and cloud:</span></span>

1. <span data-ttu-id="3da14-162">Haga clic en **Preparar infraestructura** > **Destino** y seleccione el servidor VMM de destino que quiere usar.</span><span class="sxs-lookup"><span data-stu-id="3da14-162">Click **Prepare infrastructure** > **Target**, and select the target VMM server you want to use.</span></span>
2. <span data-ttu-id="3da14-163">Se mostrarán las nubes en el servidor que están sincronizadas con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3da14-163">Clouds on the server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="3da14-164">Seleccione la nube de destino.</span><span class="sxs-lookup"><span data-stu-id="3da14-164">Select the target cloud.</span></span>

   ![Destino](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="3da14-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3da14-166">Next steps</span></span>

<span data-ttu-id="3da14-167">Vaya al [Paso 7: Configuración de la asignación de red](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="3da14-167">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
