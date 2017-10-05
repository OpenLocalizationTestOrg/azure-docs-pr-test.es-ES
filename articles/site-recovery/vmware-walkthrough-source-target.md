---
title: "Configuración del origen y el destino de la replicación de VMware en Azure con Azure Site Recovery | Microsoft Docs"
description: "Se resumen los pasos para configurar los valores de origen y de destino para la replicación de máquinas virtuales VMware en Azure Storage con Azure Site Recovery"
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
ms.openlocfilehash: 94b629a62c3a54eee69ee397b2f27e3f20b753d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-vmware-replication-to-azure"></a><span data-ttu-id="6809b-103">Paso 8: Configuración del origen y el destino de la replicación de VMware en Azure</span><span class="sxs-lookup"><span data-stu-id="6809b-103">Step 8: Set up the source and target for VMware replication to Azure</span></span>

<span data-ttu-id="6809b-104">En este artículo se describe cómo configurar opciones de origen y destino al replicar máquinas virtuales de VMware locales en Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6809b-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="6809b-105">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6809b-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="6809b-106">Configuración del entorno de origen</span><span class="sxs-lookup"><span data-stu-id="6809b-106">Set up the source environment</span></span>

<span data-ttu-id="6809b-107">Configure el servidor de configuración, regístrelo en el almacén y detecte máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6809b-107">Set up the configuration server, register it in the vault, and discover VMs.</span></span>

1. <span data-ttu-id="6809b-108">Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="6809b-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="6809b-109">Si no tiene un servidor de configuración, haga clic en **+Servidor de configuración**.</span><span class="sxs-lookup"><span data-stu-id="6809b-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="6809b-110">En **Agregar servidor**, compruebe que aparezca **Servidor de configuración** en **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="6809b-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="6809b-111">Descargue el archivo de instalación unificada de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6809b-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="6809b-112">Descargue la clave de registro del almacén.</span><span class="sxs-lookup"><span data-stu-id="6809b-112">Download the vault registration key.</span></span> <span data-ttu-id="6809b-113">Se le solicitará cuando ejecute la instalación unificada.</span><span class="sxs-lookup"><span data-stu-id="6809b-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="6809b-114">La clave será válida durante cinco días a partir del momento en que se genera.</span><span class="sxs-lookup"><span data-stu-id="6809b-114">The key is valid for five days after you generate it.</span></span>

   ![Configurar origen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="6809b-116">Registro del servidor de configuración en el almacén</span><span class="sxs-lookup"><span data-stu-id="6809b-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="6809b-117">Haga lo siguiente antes de empezar y, después, ejecute la instalación unificada para instalar el servidor de configuración, el servidor de procesos y el servidor de destino maestro.</span><span class="sxs-lookup"><span data-stu-id="6809b-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span>
    - <span data-ttu-id="6809b-118">Vea un vídeo introductorio rápido</span><span class="sxs-lookup"><span data-stu-id="6809b-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="6809b-119">En la máquina virtual del servidor de configuración, asegúrese de que el reloj del sistema está sincronizado con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="6809b-119">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="6809b-120">Deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="6809b-120">It should match.</span></span> <span data-ttu-id="6809b-121">Si hay una diferencia de 15 minutos, antes o después, se podría producir un error en la instalación.</span><span class="sxs-lookup"><span data-stu-id="6809b-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="6809b-122">Ejecute la instalación como administrador Local en la máquina virtual del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="6809b-122">Run setup as a Local Administrator on the configuration server VM.</span></span>
    - <span data-ttu-id="6809b-123">Asegúrese de que TLS 1.0 está habilitada en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6809b-123">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="6809b-124">El servidor de configuración también se puede instalar [desde la línea de comandos](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="6809b-124">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-to-vmware-servers"></a><span data-ttu-id="6809b-125">Conexión a servidores de VMware</span><span class="sxs-lookup"><span data-stu-id="6809b-125">Connect to VMware servers</span></span>

<span data-ttu-id="6809b-126">Para permitir que Azure Site Recovery detecte las máquinas virtuales que se ejecutan en el entorno local, debe conectar los hosts ESXi de vSphere o servidor vCenter de VMware con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6809b-126">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="6809b-127">Antes de empezar, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6809b-127">Note the following before you start:</span></span>

- <span data-ttu-id="6809b-128">Si agrega el servidor vCenter o los hosts de vSphere a Site Recovery con una cuenta sin privilegios de administrador en el servidor, la cuenta necesita que se habiliten estos privilegios:</span><span class="sxs-lookup"><span data-stu-id="6809b-128">If you add the vCenter server or vSphere hosts to Site Recovery with an account without administrator privileges on the server, the account needs these privileges enabled:</span></span>
    - <span data-ttu-id="6809b-129">Centro de datos, Almacén de datos, Carpeta, Host, Red, Recurso, Máquina virtual, vSphere Distributed Switch.</span><span class="sxs-lookup"><span data-stu-id="6809b-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="6809b-130">El servidor vCenter necesita el permiso Vistas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6809b-130">The vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="6809b-131">Cuando se agregan servidores VMware a Site Recovery, pueden tardar 15 minutos o más en aparecer en el portal.</span><span class="sxs-lookup"><span data-stu-id="6809b-131">When you add VMware servers to Site Recovery, it can take 15 minutes or longer for them to appear in the portal.</span></span>

### <a name="add-the-account-for-automatic-discovery"></a><span data-ttu-id="6809b-132">Incorporación de la cuenta para detección automática</span><span class="sxs-lookup"><span data-stu-id="6809b-132">Add the account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="6809b-133">Configuración de una conexión</span><span class="sxs-lookup"><span data-stu-id="6809b-133">Set up a connection</span></span>

<span data-ttu-id="6809b-134">Conéctese a los servidores de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="6809b-134">Connect to servers as follows:</span></span>

1. <span data-ttu-id="6809b-135">Seleccione **+vCenter** para comenzar a conectar un servidor vCenter de VMware o un host ESXi de vSphere de VMware.</span><span class="sxs-lookup"><span data-stu-id="6809b-135">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="6809b-136">En **Add vCenter** (Agregar vCenter), especifique un nombre descriptivo para el host de vSphere o el servidor vCenter y especifique la dirección IP o el FQDN del servidor.</span><span class="sxs-lookup"><span data-stu-id="6809b-136">In **Add vCenter**, specify a friendly name for the vSphere host or vCenter server, and then specify the IP address or FQDN of the server.</span></span>
3. <span data-ttu-id="6809b-137">Deje el puerto 443 a menos que los servidores de VMware estén configurados para escuchar las solicitudes en un puerto diferente.</span><span class="sxs-lookup"><span data-stu-id="6809b-137">Leave the port as 443 unless your VMware servers are configured to listen for requests on a different port.</span></span> <span data-ttu-id="6809b-138">Seleccione la cuenta que va a conectar al servidor de VMware vCenter o vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="6809b-138">Select the account that is to connect to the VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="6809b-139">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6809b-139">Click **OK**.</span></span>
4. <span data-ttu-id="6809b-140">Site Recovery se conecta a los servidores de VMware con la configuración especificada y detecta máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6809b-140">Site Recovery connects to VMware servers using the specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="6809b-141">Si agrega un servidor o host con una cuenta que no tiene privilegios de administrador en el servidor vCenter o el servidor host, asegúrese de que la cuenta tiene habilitados los siguientes privilegios: Centro de datos, Almacén de datos, Carpeta, Host, Red, Recurso, Máquina virtual y Conmutador distribuido de vSphere.</span><span class="sxs-lookup"><span data-stu-id="6809b-141">If you're adding a server or host with an account that doesn't have administrator privileges on the vCenter or host server, make sure that the account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="6809b-142">Además, el servidor VMware vCenter necesita el privilegio Vistas de almacenamiento habilitado.</span><span class="sxs-lookup"><span data-stu-id="6809b-142">In addition, the VMware vCenter server needs the Storage Views privilege enabled.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="6809b-143">Configuración del entorno de destino</span><span class="sxs-lookup"><span data-stu-id="6809b-143">Set up the target environment</span></span>

<span data-ttu-id="6809b-144">Antes de configurar el entorno de destino, asegúrese de tener una cuenta de Azure Storage y una red virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="6809b-144">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="6809b-145">Haga clic en **Preparar infraestructura** > **Destino** y seleccione la suscripción de Azure que quiere usar.</span><span class="sxs-lookup"><span data-stu-id="6809b-145">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="6809b-146">Especifique si el modelo de implementación de destino está basado en Resource Manager o si es el clásico.</span><span class="sxs-lookup"><span data-stu-id="6809b-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="6809b-147">Site Recovery comprueba que tiene una o más cuentas de almacenamiento y redes compatibles.</span><span class="sxs-lookup"><span data-stu-id="6809b-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destino](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="6809b-149">Si no ha creado una cuenta de almacenamiento ni una red, haga clic en **+Cuenta de almacenamiento** o **+Red** para crear una cuenta o red de Resource Manager en línea.</span><span class="sxs-lookup"><span data-stu-id="6809b-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6809b-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6809b-150">Next steps</span></span>

<span data-ttu-id="6809b-151">Vaya al [paso 9: configuración de una directiva de replicación](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6809b-151">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
