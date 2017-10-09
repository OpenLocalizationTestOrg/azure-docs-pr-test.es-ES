---
title: "aaaSet seguridad Hola origen y de destino para el sitio secundario tooa de Hyper-V replicación con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo tooset una copia de seguridad origen Hola y de destino cuando la replicación de máquinas virtuales de Hyper-V toosecondary VMM del sitio con Azure Site Recovery."
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
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="9fcc9-103">Paso 6: Configurar origen de replicación de Hola y de destino</span><span class="sxs-lookup"><span data-stu-id="9fcc9-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="9fcc9-104">Después de crear servicios de recuperación de un almacén para Hyper-V replicación tooa sitio VMM secundario con [Azure Site Recovery](site-recovery-overview.md), use este artículo tooset el origen de Hola y ubicaciones de replicación de destino.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="9fcc9-105">Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="9fcc9-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="9fcc9-106">Configurar el entorno de origen Hola</span><span class="sxs-lookup"><span data-stu-id="9fcc9-106">Set up hello source environment</span></span>

<span data-ttu-id="9fcc9-107">Instale hello Azure Site Recovery Provider en servidores VMM y detectar y registrar los servidores en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="9fcc9-108">Haga clic en **Paso 1: Preparar la infraestructura** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Configurar origen](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="9fcc9-110">En **preparar origen**, haga clic en **+ VMM** tooadd un servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Configurar origen](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="9fcc9-112">En **Agregar servidor**, compruebe que **servidor de System Center VMM** aparece en **tipo de servidor** y ese servidor VMM Hola cumple hello [requisitos previos](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="9fcc9-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="9fcc9-113">Descargar archivo de instalación del proveedor de Azure Site Recovery de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="9fcc9-114">Descargue la clave de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-114">Download hello registration key.</span></span> <span data-ttu-id="9fcc9-115">Se le solicitará cuando ejecute el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-115">You need this when you run setup.</span></span> <span data-ttu-id="9fcc9-116">clave de Hello es válida durante cinco días después de generarlo.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-116">hello key is valid for five days after you generate it.</span></span>

    ![Configurar origen](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="9fcc9-118">Instale hello Azure Site Recovery Provider en servidor VMM de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="9fcc9-119">No es necesario tooexplicitly ninguna instalación adicional en los servidores de host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="9fcc9-120">Instalar hello Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="9fcc9-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="9fcc9-121">Ejecute el archivo de configuración de proveedor de hello en cada servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="9fcc9-122">Si VMM está implementado en un clúster, siguiente Hola Hola primera vez que instale:</span><span class="sxs-lookup"><span data-stu-id="9fcc9-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="9fcc9-123">Instalar el proveedor de hello en un nodo activo y finalizar Hola instalación tooregister Hola servidor VMM en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="9fcc9-124">A continuación, instale Hola proveedor en hello otros nodos.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="9fcc9-125">Los nodos del clúster deben ejecutarse todos Hola misma versión de Hola proveedor.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="9fcc9-126">El programa de instalación ejecuta algunas comprobaciones de requisitos previos y las solicitudes de servicio VMM de permiso toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="9fcc9-127">Hola servicio VMM se reiniciará automáticamente cuando finaliza el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="9fcc9-128">Si instala en un clúster VMM, está el rol de clúster de hello toostop solicitadas.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="9fcc9-129">En **Microsoft Update**, puede participar en toospecify que están instaladas las actualizaciones del proveedor con arreglo a la directiva de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="9fcc9-130">En **instalación**, acepte o modifique la ubicación de instalación predeterminada de Hola y haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![Ubicación de instalación](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="9fcc9-132">Una vez completada la instalación, haga clic en **registrar** tooregister servidor de hello en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![Ubicación de instalación](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="9fcc9-134">En **nombre del almacén**, compruebe el nombre de Hola de almacén de hello en qué Hola se registrará el servidor.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="9fcc9-135">Haga clic en *Siguiente*.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-135">Click *Next*.</span></span>

    ![Registro de servidor](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="9fcc9-137">En **conexión a Internet**, especifique cómo se proveedor Hola que se ejecuta en el servidor VMM Hola conecta tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![Configuración de Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="9fcc9-139">Puede especificar ese proveedor Hola debe conectarse directamente toohello internet, o a través de un servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="9fcc9-140">Especifique la configuración de proxy si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="9fcc9-141">Si usa un proxy, una cuenta de ejecución de VMM (DRAProxyAccount) se crea automáticamente con hello especificada las credenciales del proxy.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="9fcc9-142">Configurar servidor proxy de Hola para que esta cuenta se pueda autenticar correctamente.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="9fcc9-143">Hello configuración de la cuenta de ejecución puede modificarse en la consola VMM hello > **configuración** > **seguridad** > **cuentas de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="9fcc9-144">Reinicie los cambios de tooupdate de servicio VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="9fcc9-145">En **clave de registro**, seleccione clave de Hola que descargó desde Azure Site Recovery y copió toohello servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="9fcc9-146">configuración de cifrado de Hello sólo se utiliza al replicar las máquinas virtuales de Hyper-V en tooAzure de nubes VMM.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="9fcc9-147">Si replica tooa de sitio secundario no se utiliza.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="9fcc9-148">En **nombre del servidor**, especifique un servidor VMM Nombre_descriptivo tooidentify hello en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="9fcc9-149">En una configuración de clúster especificar nombre de rol de clúster VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="9fcc9-150">En **sincronizar metadatos de nube**, seleccione si desea toosynchronize metadatos para todas las nubes en el servidor VMM de hello con almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="9fcc9-151">Esta acción solo debe toohappen una vez en cada servidor.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="9fcc9-152">Si no desea toosynchronize todas las nubes, puede dejar esta configuración desactivada y sincronizar cada nube individualmente en las propiedades de la nube de hello en la consola VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="9fcc9-153">Haga clic en **siguiente** toocomplete proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="9fcc9-154">Después del registro, Azure Site Recovery recupera metadatos desde un servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="9fcc9-155">servidor Hola se muestra en hello **servidores VMM** ficha en hello **servidores** página en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![Server](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="9fcc9-157">Después de hello servidor está disponible en la consola de Site Recovery hello, en **origen** > **preparar origen** seleccione servidor VMM de Hola y en qué Hola Hyper-V host se encuentra en la nube Hola select.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="9fcc9-158">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-158">Then click **OK**.</span></span>

<span data-ttu-id="9fcc9-159">También puede instalar el proveedor de Hola desde línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="9fcc9-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="9fcc9-160">Configurar el entorno de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="9fcc9-160">Set up hello target environment</span></span>

<span data-ttu-id="9fcc9-161">Seleccione en la nube y el servidor VMM de destino de hello:</span><span class="sxs-lookup"><span data-stu-id="9fcc9-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="9fcc9-162">Haga clic en **preparar infraestructura** > **destino**y el servidor VMM de destino Hola seleccione desea toouse.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="9fcc9-163">Se mostrarán las nubes en el servidor de Hola que se sincronizan con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="9fcc9-164">Seleccione la nube de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fcc9-164">Select hello target cloud.</span></span>

   ![Destino](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="9fcc9-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9fcc9-166">Next steps</span></span>

<span data-ttu-id="9fcc9-167">Vaya demasiado[paso 7: configurar la asignación de red](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="9fcc9-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
