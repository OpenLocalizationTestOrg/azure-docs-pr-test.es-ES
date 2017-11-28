---
title: "aaaSet seguridad Hola origen y de destino para tooAzure de replicación de Hyper-V (sin System Center VMM) con Azure Site Recovery | Documentos de Microsoft"
description: "Resume Hola pasos tooset la configuración de origen y de destino para la replicación de almacenamiento de máquinas virtuales de Hyper-V tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="ad84f-103">Paso 8: Configurar origen de Hola y de destino para tooAzure de replicación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ad84f-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="ad84f-104">Este artículo describe cómo tooconfigure de configuración de origen y de destino cuando se replican de manera local tooAzure de máquinas virtuales (sin System Center VMM) de Hyper-V, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad84f-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="ad84f-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ad84f-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="ad84f-106">Configurar el entorno de origen Hola</span><span class="sxs-lookup"><span data-stu-id="ad84f-106">Set up hello source environment</span></span>

<span data-ttu-id="ad84f-107">Configurar el sitio de Hyper-V de hello, instalar Hola proveedor de Azure Site Recovery y el agente de servicios de recuperación de Azure de hello en hosts de Hyper-V y registrar sitio hello en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad84f-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="ad84f-108">En **Preparar infraestructura**, haga clic en **Origen**.</span><span class="sxs-lookup"><span data-stu-id="ad84f-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="ad84f-109">Haga clic en un nuevo sitio de Hyper-V como un contenedor para los hosts de Hyper-V o clústeres, tooadd **+ sitio de Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="ad84f-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Configurar origen](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="ad84f-111">En **sitio Hyper-V crear**, especifique un nombre para el sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad84f-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="ad84f-112">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ad84f-112">Then click **OK**.</span></span> <span data-ttu-id="ad84f-113">Ahora, seleccione el sitio de Hola que creó y, después, haga clic en **+ servidor Hyper-V** tooadd un sitio de toohello de servidor.</span><span class="sxs-lookup"><span data-stu-id="ad84f-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![Configurar origen](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="ad84f-115">En **Agregar servidor** > **Tipo de servidor**, compruebe que se muestra **Hyper-V Server**.</span><span class="sxs-lookup"><span data-stu-id="ad84f-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="ad84f-116">Asegúrese de que ese servidor hello Hyper-V que desee tooadd cumple con hello [requisitos previos](#on-premises-prerequisites), y es capaz de tooaccess Hola direcciones URL especificadas.</span><span class="sxs-lookup"><span data-stu-id="ad84f-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="ad84f-117">Descargar archivo de instalación del proveedor de Azure Site Recovery de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad84f-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="ad84f-118">Ejecute este hello de tooinstall archivo proveedor y Hola agente de servicios de recuperación en cada host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ad84f-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![Configurar origen](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="ad84f-120">Instalar Hola proveedor y agente</span><span class="sxs-lookup"><span data-stu-id="ad84f-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="ad84f-121">Ejecutar el archivo de instalación de proveedor de hello en cada host agregado toohello Hyper-V sitio.</span><span class="sxs-lookup"><span data-stu-id="ad84f-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="ad84f-122">Si va a realizar la instalación en un clúster de Hyper-V, ejecute el programa de instalación en cada nodo de clúster.</span><span class="sxs-lookup"><span data-stu-id="ad84f-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="ad84f-123">Instalar y registrar los nodos de cada clúster de Hyper-V garantiza que las máquinas virtuales permanezcan protegidas incluso si se migran entre nodos.</span><span class="sxs-lookup"><span data-stu-id="ad84f-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="ad84f-124">En **Microsoft Update** puede optar por recibir actualizaciones para que las actualizaciones del proveedor se realicen según las directivas de Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="ad84f-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="ad84f-125">En **instalación**, acepte o modifique la ubicación de instalación de proveedor de hello predeterminada y haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="ad84f-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="ad84f-126">En **configuración del almacén**, haga clic en **examinar** tooselect Hola almacén archivo de clave que ha descargado.</span><span class="sxs-lookup"><span data-stu-id="ad84f-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="ad84f-127">Especifique la suscripción de Azure Site Recovery Hola, nombre del almacén de hello, y pertenece Hola Hyper-V sitio toowhich Hola Hyper-V server.</span><span class="sxs-lookup"><span data-stu-id="ad84f-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![Registro de servidor](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="ad84f-129">En **configuración de Proxy**, especifique cómo Hola Hola que se ejecutan en hosts de Hyper-V conectará tooAzure Site Recovery por proveedor a internet.</span><span class="sxs-lookup"><span data-stu-id="ad84f-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="ad84f-130">Si desea que Hola proveedor tooconnect directamente seleccione **conectarse directamente tooAzure Site Recovery sin un proxy**.</span><span class="sxs-lookup"><span data-stu-id="ad84f-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="ad84f-131">Si el proxy existente requiere autenticación, o si desea toouse un proxy personalizado para la conexión del proveedor de hello, seleccione **conectar tooAzure Site Recovery con un servidor proxy**.</span><span class="sxs-lookup"><span data-stu-id="ad84f-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="ad84f-132">Si utiliza un proxy:</span><span class="sxs-lookup"><span data-stu-id="ad84f-132">If you use a proxy:</span></span>
        - <span data-ttu-id="ad84f-133">Especifique las credenciales, el puerto y la dirección de Hola</span><span class="sxs-lookup"><span data-stu-id="ad84f-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="ad84f-134">Hace que direcciones URL de hello descritas en hello [requisitos previos](#prerequisites) se permiten a través de proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad84f-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="ad84f-136">Una vez finalizada la instalación, haga clic en **registrar** tooregister servidor de hello en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad84f-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![Ubicación de instalación](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="ad84f-138">Después de que finalice el registro, Azure Site Recovery recupera metadatos del servidor de Hyper-V de Hola y Hola servidor se muestra en **infraestructura del sitio de recuperación** > **Hosts de Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="ad84f-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="ad84f-139">Configurar el entorno de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="ad84f-139">Set up hello target environment</span></span>

<span data-ttu-id="ad84f-140">Especifique la cuenta de almacenamiento de Azure de hello para la replicación y hello toowhich de red de Azure máquinas virtuales de Azure se conectará tras la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ad84f-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="ad84f-141">Haga clic en **Preparar infraestructura** > **Destino**.</span><span class="sxs-lookup"><span data-stu-id="ad84f-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="ad84f-142">Seleccione la suscripción de Hola y el grupo de recursos de hello en el que desea toocreate Hola máquinas virtuales de Azure después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ad84f-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="ad84f-143">Elija Hola implementación modelo que quiere toouse en Azure (classic o recursos administración) de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ad84f-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="ad84f-144">Site Recovery comprueba que tiene una o más redes y cuentas de Azure Storage compatibles.</span><span class="sxs-lookup"><span data-stu-id="ad84f-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="ad84f-145">Si no tienes una cuenta de almacenamiento, haga clic en **+ almacenamiento** toocreate un insertado cuenta basada en el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="ad84f-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="ad84f-146">Si no tiene una red de Azure, haga clic en **+ red** toocreate un insertado de red basada en el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="ad84f-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="ad84f-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad84f-147">Next steps</span></span>

<span data-ttu-id="ad84f-148">Vaya demasiado[paso 9: configurar una directiva de replicación](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ad84f-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
