---
title: "aaaSet seguridad Hola origen y de destino para tooAzure de replicación de VMware con Azure Site Recovery | Documentos de Microsoft"
description: "Resume Hola pasos tooset la configuración de origen y de destino para la replicación de almacenamiento de máquinas virtuales VMware tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="e0c24-103">Paso 8: Configurar origen de Hola y de destino para tooAzure de replicación de VMware</span><span class="sxs-lookup"><span data-stu-id="e0c24-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="e0c24-104">Este artículo describe cómo tooconfigure de configuración de origen y de destino cuando se replican de manera local tooAzure de máquinas virtuales de VMware, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c24-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="e0c24-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e0c24-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="e0c24-106">Configurar el entorno de origen Hola</span><span class="sxs-lookup"><span data-stu-id="e0c24-106">Set up hello source environment</span></span>

<span data-ttu-id="e0c24-107">Configurar el servidor de configuración de hello, registrar en el almacén de Hola y detectar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e0c24-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="e0c24-108">Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="e0c24-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="e0c24-109">Si no tiene un servidor de configuración, haga clic en **+Servidor de configuración**.</span><span class="sxs-lookup"><span data-stu-id="e0c24-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="e0c24-110">En **Agregar servidor**, compruebe que aparezca **Servidor de configuración** en **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="e0c24-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="e0c24-111">Descargue el archivo de instalación de configuración de Site Recovery unificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0c24-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="e0c24-112">Descargue la clave de registro del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0c24-112">Download hello vault registration key.</span></span> <span data-ttu-id="e0c24-113">Se le solicitará cuando ejecute la instalación unificada.</span><span class="sxs-lookup"><span data-stu-id="e0c24-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="e0c24-114">clave de Hello es válida durante cinco días después de generarlo.</span><span class="sxs-lookup"><span data-stu-id="e0c24-114">hello key is valid for five days after you generate it.</span></span>

   ![Configurar origen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="e0c24-116">Registrar el servidor de configuración de hello en el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="e0c24-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="e0c24-117">Realice la siguiente Hola antes de iniciar después ejecutar el programa de instalación unificada tooinstall servidor de configuración de hello, servidor de procesos de Hola y servidor de destino maestro Hola.</span><span class="sxs-lookup"><span data-stu-id="e0c24-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="e0c24-118">Vea un vídeo introductorio rápido</span><span class="sxs-lookup"><span data-stu-id="e0c24-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="e0c24-119">En la máquina virtual del servidor de configuración de hello, asegúrese de que el reloj del sistema de Hola se sincroniza con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="e0c24-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="e0c24-120">Deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="e0c24-120">It should match.</span></span> <span data-ttu-id="e0c24-121">Si hay una diferencia de 15 minutos, antes o después, se podría producir un error en la instalación.</span><span class="sxs-lookup"><span data-stu-id="e0c24-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="e0c24-122">Ejecute el programa de instalación como administrador Local en la máquina virtual del servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0c24-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="e0c24-123">Asegúrese de que TLS 1.0 está habilitado en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e0c24-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="e0c24-124">También se puede instalar el servidor de configuración de Hello [desde la línea de comandos de hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="e0c24-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="e0c24-125">Conectar servidores tooVMware</span><span class="sxs-lookup"><span data-stu-id="e0c24-125">Connect tooVMware servers</span></span>

<span data-ttu-id="e0c24-126">tooallow Azure Site Recovery toodiscover máquinas virtuales que ejecutan en su entorno local, debe tooconnect el servidor VMware vCenter o hosts de ESXi vSphere con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e0c24-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="e0c24-127">Tenga en cuenta los siguiente Hola antes de empezar:</span><span class="sxs-lookup"><span data-stu-id="e0c24-127">Note hello following before you start:</span></span>

- <span data-ttu-id="e0c24-128">Si Agregar servidor de vCenter Hola o vSphere hosts tooSite recuperación con una cuenta sin privilegios de administrador en el servidor de hello, cuenta de hello necesita estos privilegios habilitados:</span><span class="sxs-lookup"><span data-stu-id="e0c24-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="e0c24-129">Centro de datos, Almacén de datos, Carpeta, Host, Red, Recurso, Máquina virtual, vSphere Distributed Switch.</span><span class="sxs-lookup"><span data-stu-id="e0c24-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="e0c24-130">servidor de vCenter Hola necesita permisos de vistas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0c24-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="e0c24-131">Al agregar servidores de VMware tooSite recuperación, se pueden tardar 15 minutos o más para ellos tooappear en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0c24-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="e0c24-132">Agregar cuenta de hello para la detección automática</span><span class="sxs-lookup"><span data-stu-id="e0c24-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="e0c24-133">Configuración de una conexión</span><span class="sxs-lookup"><span data-stu-id="e0c24-133">Set up a connection</span></span>

<span data-ttu-id="e0c24-134">Conectar tooservers como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="e0c24-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="e0c24-135">Seleccione **+ vCenter** toostart conectar un servidor VMware vCenter o un host de VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="e0c24-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="e0c24-136">En **agregar vCenter**, especifique un nombre descriptivo para el servidor de vCenter o host de vSphere de hello y, a continuación, especifique la dirección IP de Hola o FQDN del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0c24-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="e0c24-137">Deje el puerto de hello como 443 a menos que los servidores de VMware son toolisten configurado para las solicitudes en un puerto diferente.</span><span class="sxs-lookup"><span data-stu-id="e0c24-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="e0c24-138">Seleccionar cuenta de hello tooconnect toohello servidor de VMware vCenter o vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="e0c24-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="e0c24-139">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e0c24-139">Click **OK**.</span></span>
4. <span data-ttu-id="e0c24-140">Recuperación del sitio conecta a servidores de tooVMware mediante Hola especifica la configuración y detecta las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e0c24-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="e0c24-141">Si va a agregar un servidor o un host con una cuenta que no tiene privilegios de administrador en el servidor de vCenter o host de hello, asegúrese de que la cuenta de hello tiene estos privilegios habilitados: Centro de datos, almacén de datos, carpeta, Host, red, recurso, Máquina Virtual, y vSphere conmutador distribuida.</span><span class="sxs-lookup"><span data-stu-id="e0c24-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="e0c24-142">Además, servidor hello VMware vCenter necesita vistas de almacenamiento de hello habilitar privilegio.</span><span class="sxs-lookup"><span data-stu-id="e0c24-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="e0c24-143">Configurar el entorno de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="e0c24-143">Set up hello target environment</span></span>

<span data-ttu-id="e0c24-144">Antes de configurar el entorno de destino de hello, asegúrese de que tiene una cuenta de almacenamiento de Azure y la configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="e0c24-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="e0c24-145">Haga clic en **preparar infraestructura** > **destino**, y seleccione Hola desea toouse de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c24-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="e0c24-146">Especifique si el modelo de implementación de destino está basado en Resource Manager o si es el clásico.</span><span class="sxs-lookup"><span data-stu-id="e0c24-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="e0c24-147">Site Recovery comprueba que tiene una o más cuentas de almacenamiento y redes compatibles.</span><span class="sxs-lookup"><span data-stu-id="e0c24-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destino](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="e0c24-149">Si no ha creado una cuenta de almacenamiento o red, haga clic en **+ cuenta de almacenamiento** o **+ red**, toocreate un administrador de recursos cuenta o red en línea.</span><span class="sxs-lookup"><span data-stu-id="e0c24-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0c24-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0c24-150">Next steps</span></span>

<span data-ttu-id="e0c24-151">Vaya demasiado[paso 9: configurar una directiva de replicación](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="e0c24-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
