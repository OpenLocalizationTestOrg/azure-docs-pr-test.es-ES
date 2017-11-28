---
title: Almacenamiento Premium de Azure con SQL Server aaaUse | Documentos de Microsoft
description: "En este artículo usa recursos creados con el modelo de implementación clásica de Hola y proporciona una orientación sobre el uso de almacenamiento Premium de Azure con SQL Server que se ejecutan en máquinas virtuales de Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="bf1e9-103">Usar el almacenamiento Premium de Azure con SQL Server en máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="bf1e9-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="bf1e9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="bf1e9-104">Overview</span></span>
<span data-ttu-id="bf1e9-105">[Almacenamiento Premium de Azure](../../../storage/common/storage-premium-storage.md) es Hola siguiente generación de almacenamiento que proporciona baja latencia y alto rendimiento de E/S.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="bf1e9-106">Funciona mejor para cargas de trabajo intensivas clave de E/S, como [máquinas virtuales](https://azure.microsoft.com/services/virtual-machines/)de SQL Server en IaaS.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf1e9-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bf1e9-108">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="bf1e9-109">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="bf1e9-110">Este artículo proporciona orientación para migrar una máquina Virtual con SQL Server toouse almacenamiento Premium y planeación.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="bf1e9-111">Esto incluye pasos relacionados con la infraestructura de Azure (redes, almacenamiento) y la máquina virtual invitada de Windows.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="bf1e9-112">ejemplo de Hola Hola [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) local se muestra una migración de tooend final integrales de cómo mejora toomove mayor ventaja de tootake de las máquinas virtuales de almacenamiento SSD con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="bf1e9-113">Es importante toounderstand Hola-to-end proceso usando almacenamiento Premium de Azure con SQL Server en máquinas virtuales de IAAS.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="bf1e9-114">En ella se incluye:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-114">This includes:</span></span>

* <span data-ttu-id="bf1e9-115">Identificación de los requisitos previos de hello toouse almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="bf1e9-116">Ejemplos de implementación de SQL Server en IaaS tooPremium almacenamiento para nuevas implementaciones.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="bf1e9-117">Ejemplos de migración de implementaciones existentes, tanto servidores independientes como implementaciones mediante grupos de disponibilidad AlwaysOn de SQL.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="bf1e9-118">Enfoques de migración posibles.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-118">Possible migration approaches.</span></span>
* <span data-ttu-id="bf1e9-119">Muestra los pasos de Azure, Windows y SQL Server para la migración de Hola de una implementación existente siempre en el ejemplo de end-to-end.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="bf1e9-120">Para obtener información general sobre SQL Server en máquinas virtuales de Azure, consulte [SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="bf1e9-121">**Autor:** Daniel Sol **Revisores técnicos:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="bf1e9-122">Requisitos previos para el almacenamiento Premium</span><span class="sxs-lookup"><span data-stu-id="bf1e9-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="bf1e9-123">Hay varios requisitos previos para usar el almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="bf1e9-124">Tamaño de la máquina</span><span class="sxs-lookup"><span data-stu-id="bf1e9-124">Machine size</span></span>
<span data-ttu-id="bf1e9-125">Para usar almacenamiento Premium debe toouse DS serie máquinas virtuales (VM).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="bf1e9-126">Si no ha utilizado las máquinas de la serie DS en el servicio de nube antes, debe eliminar Hola existente VM, mantener Hola adjuntada discos y, a continuación, crear un nuevo servicio de nube antes de volver a Hola VM como DS * tamaño de rol.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="bf1e9-127">Para más información sobre los tamaños de las máquinas virtuales, consulte [Tamaños de máquinas virtuales y servicios en la nube de Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="bf1e9-128">Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="bf1e9-128">Cloud services</span></span>
<span data-ttu-id="bf1e9-129">Solo puede usar máquinas virtuales DS* con almacenamiento Premium cuando se crean en un servicio en la nube nuevo.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="bf1e9-130">Si usas SQL Server Always On en Azure, Hola siempre escucha hará referencia dirección toohello Azure interno o externo IP del equilibrador de carga que está asociada a un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="bf1e9-131">En este artículo se centra en cómo toomigrate manteniendo la disponibilidad en este escenario.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1e9-132">Una serie DS * debe ser Hola primera máquina virtual que está implementado toohello nuevo servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="bf1e9-133">Redes virtuales regionales</span><span class="sxs-lookup"><span data-stu-id="bf1e9-133">Regional VNETS</span></span>
<span data-ttu-id="bf1e9-134">Para las máquinas virtuales de DS * debe configurar Hola red Virtual (VNET) hospeda el toobe de las máquinas virtuales regional.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="bf1e9-135">Este Hola "amplía" red virtual es toobe tooallow Hola de máquinas virtuales más grande aprovisionado en otros clústeres y permitir la comunicación entre ellos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="bf1e9-136">En la siguiente captura de pantalla de hello, hello ubicación resaltada muestra redes virtuales regionales, mientras que el primer resultado de hello muestra una red virtual "estrecha".</span><span class="sxs-lookup"><span data-stu-id="bf1e9-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="bf1e9-138">Puede generar un tooa de toomigrate del vale de soporte técnico de Microsoft red virtual regional, Microsoft realizará un cambio, a continuación, toocomplete Hola migración tooregional de redes virtuales, cambie la propiedad hello AffinityGroup configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="bf1e9-139">Primero debe exportar Hola configuración de red en PowerShell y, a continuación, reemplace hello **AffinityGroup** propiedad Hola **VirtualNetworkSite** elemento con un **ubicación** propiedad.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="bf1e9-140">Especifique `Location = XXXX` donde `XXXX` es una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="bf1e9-141">A continuación, importar configuración nueva de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-141">Then import hello new configuration.</span></span>

<span data-ttu-id="bf1e9-142">Por ejemplo, tenga en cuenta Hola siguiente configuración de red virtual:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="bf1e9-143">toomove este tooa red virtual regional en Europa occidental, cambiar hello toohello de configuración siguientes:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="bf1e9-144">Cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bf1e9-144">Storage accounts</span></span>
<span data-ttu-id="bf1e9-145">Deberá toocreate una nueva cuenta de almacenamiento que está configurada para el almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="bf1e9-146">Tenga en cuenta que use Hola de almacenamiento Premium está establecida en la cuenta de almacenamiento de hello, no en discos duros virtuales individuales, sin embargo, cuando se usa una VM de serie DS * puede adjuntar VHD desde cuentas de almacenamiento estándar y Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="bf1e9-147">Puede considerar esta opción si no desea tooplace Hola VHD de SO en toohello cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="bf1e9-148">siguiente Hello **New-AzureStorageAccountPowerShell** comando con hello "Premium_LRS" **tipo** crea una cuenta de almacenamiento Premium:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="bf1e9-149">Configuración de la caché de los VHD</span><span class="sxs-lookup"><span data-stu-id="bf1e9-149">VHDs Cache Settings</span></span>
<span data-ttu-id="bf1e9-150">Hola principal diferencia entre la creación de discos que forman parte de una cuenta de almacenamiento Premium es configuración de caché de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="bf1e9-151">En el caso de discos de volumen de datos de SQL Server, se recomienda usar "**Read Caching**".</span><span class="sxs-lookup"><span data-stu-id="bf1e9-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="bf1e9-152">Para volúmenes de registro de transacciones, configuración de caché de disco de hello debe establecerse demasiado '**ninguno**'.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="bf1e9-153">Esto es diferente de las recomendaciones de hello las cuentas de almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="bf1e9-154">Una vez que se han adjuntado Hola discos duros virtuales, no se puede modificar la configuración de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="bf1e9-155">¿Necesita toodetach y volver a adjuntar Hola VHD con una configuración de memoria caché actualizada.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="bf1e9-156">Espacios de almacenamiento de Windows</span><span class="sxs-lookup"><span data-stu-id="bf1e9-156">Windows storage spaces</span></span>
<span data-ttu-id="bf1e9-157">Puede usar [espacios de almacenamiento de Windows](https://technet.microsoft.com/library/hh831739.aspx) como lo hizo con almacenamiento estándar anterior, esto le permitirá toomigrate una máquina virtual que ya se utiliza espacios de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="bf1e9-158">ejemplo de Hola en [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (paso 9 y siguientes) se muestra hello tooextract de código de Powershell e importar una máquina virtual con varios discos duros virtuales conectados.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="bf1e9-159">Grupos de almacenamiento se usan con un rendimiento tooenhance de cuenta de almacenamiento de Azure estándar y reducen la latencia.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="bf1e9-160">Pueden resultarle útiles las pruebas de los grupos de almacenamiento con el almacenamiento Premium para implementaciones nuevas, pero agregan una complejidad adicional con la configuración del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="bf1e9-161">¿Cómo toofind qué discos virtuales de Azure se asignan grupos de toostorage</span><span class="sxs-lookup"><span data-stu-id="bf1e9-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="bf1e9-162">Tal y como se ofrecen recomendaciones de configuración de caché diferente para VHD adjunto, podría decidir toocopy Hola discos duros virtuales tooa cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="bf1e9-163">Sin embargo, cuando se vuelva a adjuntarlos toohello la serie DS nueva máquina virtual, tendrá que configuración de la caché de tooalter Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="bf1e9-164">Resulta más sencillo Hola tooapply que almacenamiento Premium recomienda configuración de la caché cuando tienes VHD independiente para Hola de datos de SQL archivos y registro archivos (en lugar de un solo disco duro virtual que contiene).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="bf1e9-165">Si tiene archivos de datos y de registro de SQL Server en el mismo volumen, Hola almacenamiento en caché de la opción que elija depende de los patrones de acceso de E/S de Hola para las cargas de trabajo de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="bf1e9-166">Solo las pruebas pueden demostrar qué opción de caché es más adecuada para este escenario.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="bf1e9-167">Sin embargo, si usa espacios de almacenamiento de Windows que se compone de varios discos duros virtuales deberá toolook en su tooidentify scripts original que ha adjuntado discos duros virtuales están en qué grupo específico, por lo que se pueden establecer opciones de caché de hello en consecuencia para cada disco.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="bf1e9-168">Si no tiene original tooshow disponibles de script qué discos duros virtuales se asignan toohello bloque de almacenamiento, puede usar Hola después de asignación de grupo de pasos toodetermine Hola/almacenamiento en disco.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="bf1e9-169">Para cada disco, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="bf1e9-170">Obtención de una lista de discos conectados tooVM con hello **Get-AzureVM** comando:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="bf1e9-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="bf1e9-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="bf1e9-172">Tenga en cuenta Hola Diskname y LUN.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="bf1e9-174">Escritorio remoto en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="bf1e9-175">A continuación, vaya demasiado**administración de equipos** | **el Administrador de dispositivos** | **unidades de disco**.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="bf1e9-176">Examine las propiedades de Hola de cada uno de hello 'Microsoft 'discos virtuales</span><span class="sxs-lookup"><span data-stu-id="bf1e9-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="bf1e9-178">aquí el número de LUN Hello es un número LUN de toohello de referencia que especifique al adjuntar Hola VHD toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="bf1e9-179">Para hello 'Disco Virtual de Microsoft' vaya toohello **detalles** ficha, a continuación, en hello **propiedad** lista, vaya demasiado**clave Driver**.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="bf1e9-180">Hola **valor**, Hola Nota **desplazamiento**, que es 0002 Hola siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="bf1e9-181">Hola 0002 denota hello PhysicalDisk2 que Hola referencias del grupo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="bf1e9-183">Para cada grupo de almacenamiento, volcado out Hola asociados discos:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="bf1e9-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="bf1e9-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="bf1e9-186">Ahora puede usar este tooassociate de información de discos duros virtuales tooPhysical discos en grupos de almacenamiento conectados.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="bf1e9-187">Una vez que ha asignado los discos duros virtuales tooPhysical discos en grupos de almacenamiento, a continuación, puede separar y cópielos en tooa cuenta de almacenamiento Premium, a continuación, deberá asociarlas con configuración de caché correcto Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="bf1e9-188">Vea ejemplo de Hola Hola [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), los pasos del 8 al 12.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="bf1e9-189">Estos pasos muestran cómo tooextract un archivo VHD conectado a la máquina virtual disco configuración tooa CSV, copiar discos duros virtuales de hello, modificar opciones de caché de configuración de disco de Hola y por último, volver a implementar Hola VM como una serie DS VM con hello todos los discos conectados.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="bf1e9-190">Ancho de banda del almacenamiento de la VM y rendimiento del almacenamiento del VHD</span><span class="sxs-lookup"><span data-stu-id="bf1e9-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="bf1e9-191">cantidad de Hola de rendimiento de almacenamiento depende de hello tamaño de VM de DS * especificado y Hola tamaños de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="bf1e9-192">máquinas virtuales de Hello tienen diferentes compensaciones por número de Hola de discos duros virtuales que se pueden adjuntar y Hola ancho de banda máximo, admitirán (MB/s).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="bf1e9-193">Los números de ancho de banda determinado hello, consulte [Máquina Virtual y tamaños de servicio de nube de Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="bf1e9-194">El aumento de IOPS se consigue con tamaños de disco mayores.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="bf1e9-195">Debe tenerlo en cuenta al considerar la ruta de acceso de la migración.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="bf1e9-196">Para obtener más información, [ver tabla de Hola para los tipos de disco y e/s por segundo](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="bf1e9-197">Por último, tenga en cuenta que las máquinas virtuales admiten diferentes anchos de banda de disco máximos para todos los discos conectados.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="bf1e9-198">Bajo una carga alta, podría saturar el ancho de banda máximo en disco de hello disponible para ese tamaño de rol de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="bf1e9-199">Por ejemplo un Standard_DS14 admitirán la too512MB/s; por lo tanto, con tres discos P30 podría saturar el ancho de banda de disco de Hola de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="bf1e9-200">Pero en este ejemplo, se puede superar el límite de rendimiento de hello según la combinación de Hola de lectura y escritura IOs.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="bf1e9-201">Nuevas implementaciones</span><span class="sxs-lookup"><span data-stu-id="bf1e9-201">New deployments</span></span>
<span data-ttu-id="bf1e9-202">Hola dos secciones siguientes muestran cómo se puede implementar tooPremium almacenamiento de VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="bf1e9-203">Como se mencionó antes, no es necesario necesariamente tooplace el disco del sistema operativo de hello en almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="bf1e9-204">Puede elegir toodo de esto si tiene previsto tooplace las cargas de trabajo intensivas de E/S en hello VHD de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="bf1e9-205">Hola primer ejemplo demuestra el uso de imágenes de la Galería de Azure existente.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="bf1e9-206">Hello segundo ejemplo muestra cómo toouse una máquina virtual personalizada de la imagen que tiene en una cuenta de almacenamiento estándar existente.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1e9-207">En estos ejemplos se supone que ya ha creado una red virtual regional.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="bf1e9-208">Crear una nueva máquina virtual con almacenamiento Premium con una imagen de la Galería</span><span class="sxs-lookup"><span data-stu-id="bf1e9-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="bf1e9-209">ejemplo de Hola siguiente muestra cómo tooplace Hola VHD de SO en almacenamiento premium y adjuntar VHD de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="bf1e9-210">Sin embargo, puede ubicar el disco del sistema operativo hello en una cuenta de almacenamiento estándar y, a continuación, adjuntar discos duros virtuales que residen en una cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="bf1e9-211">Se muestran ambos escenarios.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="bf1e9-212">Paso 1: Crear una cuenta de almacenamiento Premium</span><span class="sxs-lookup"><span data-stu-id="bf1e9-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="bf1e9-213">Paso 2: Crear un nuevo servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="bf1e9-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="bf1e9-214">Paso 3: Reservar una VIP de servicio en la nube (opcional)</span><span class="sxs-lookup"><span data-stu-id="bf1e9-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="bf1e9-215">Paso 4: Crear un contenedor de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="bf1e9-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="bf1e9-216">Paso 5: Colocar el VHD del sistema operativo en el almacenamiento estándar o Premium</span><span class="sxs-lookup"><span data-stu-id="bf1e9-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="bf1e9-217">Paso 6: Crear una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bf1e9-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="bf1e9-218">Crear un nuevo toouse VM almacenamiento Premium con una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="bf1e9-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="bf1e9-219">Este escenario muestra dónde tiene imágenes personalizadas que residen en una cuenta de almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="bf1e9-220">Como se mencionó si desea tooplace Hola VHD de sistema operativo en almacenamiento Premium debe toocopy Hola imagen que existe en la cuenta de almacenamiento estándar hello y transferirlas tooa almacenamiento Premium antes de poder utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="bf1e9-221">Si tiene una imagen local, puede usar este método toocopy directamente toohello cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="bf1e9-222">Paso 1: Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bf1e9-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="bf1e9-223">Paso 2: Crear un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="bf1e9-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="bf1e9-224">Paso 3: Usar una imagen existente</span><span class="sxs-lookup"><span data-stu-id="bf1e9-224">Step 3: Use existing image</span></span>
<span data-ttu-id="bf1e9-225">Puede usar una imagen existente.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-225">You can use an existing image.</span></span> <span data-ttu-id="bf1e9-226">También puede [captar la imagen de una máquina existente](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="bf1e9-227">Máquina de hello tenga en cuenta que la imagen no tiene toobe DS * máquina.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="bf1e9-228">Una vez que tenga la imagen de hello, Hola siguientes pasos muestran cómo toocopy se toohello cuenta de almacenamiento Premium con hello **AzureStorageBlobCopy inicio** commandlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="bf1e9-229">Paso 4: Copiar un blob entre cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bf1e9-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="bf1e9-230">Paso 5: Comprobar periódicamente el estado de copia</span><span class="sxs-lookup"><span data-stu-id="bf1e9-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="bf1e9-231">Paso 6: Agregar disco de imagen en tooAzure repositorio de suscripción</span><span class="sxs-lookup"><span data-stu-id="bf1e9-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="bf1e9-232">Es posible que, aunque los informes de estado de hello como correcto, todavía podrían obtener un error de concesión de disco.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="bf1e9-233">En este caso, espere unos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="bf1e9-234">Paso 7: Crear Hola VM</span><span class="sxs-lookup"><span data-stu-id="bf1e9-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="bf1e9-235">Aquí está generando Hola VM de la imagen y asociar dos VHD de almacenamiento Premium:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="bf1e9-236">Implementaciones existentes que no usan grupos de disponibilidad AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="bf1e9-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="bf1e9-237">Para las implementaciones existentes, primero consulte hello [requisitos previos](#prerequisites-for-premium-storage) sección de este tema.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="bf1e9-238">Existen diferentes consideraciones para las implementaciones de SQL Server que no usan grupos de disponibilidad AlwaysOn y para las que los usan.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="bf1e9-239">Si no se usa siempre en y tiene un servidor SQL Server independiente existente, puede actualizar tooPremium almacenamiento mediante una nueva cuenta de servicio y el almacenamiento en nube.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="bf1e9-240">Considere la posibilidad de hello siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-240">Consider hello following options:</span></span>

* <span data-ttu-id="bf1e9-241">**Crear una nueva máquina virtual de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="bf1e9-242">Puede crear una nueva máquina virtual de SQL Server que use una cuenta de almacenamiento Premium, como se documenta en Nuevas implementaciones.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="bf1e9-243">A continuación, haga una copia de seguridad y restaure las bases de datos de usuario y la configuración de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="bf1e9-244">Hello aplicación necesitará toobe actualiza tooreference Hola nuevo SQL Server si se tiene acceso interna o externamente.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="bf1e9-245">Necesitaría toocopy todos los objetos "fuera de la base de datos' como si está realizando una migración de en paralelo (SxS) de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="bf1e9-246">Esto incluye objetos tales como inicios de sesión, certificados y servidores vinculados.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="bf1e9-247">**Migrar una máquina virtual de SQL Server existente**.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="bf1e9-248">Esto requerirá desconectar Hola VM de SQL Server, a continuación, transferir tooa nuevo servicio en la nube, que incluye la copia de todos su toohello de discos duros virtuales conectado cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="bf1e9-249">Cuando Hola VM se pone en línea, aplicación hello hará referencia a nombre de host del servidor hello como antes.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="bf1e9-250">Tenga en cuenta que tamaño Hola de disco existente de hello afectarán a las características de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="bf1e9-251">Por ejemplo, un disco de 400 GB obtiene redondea tooa P20.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="bf1e9-252">Si sabe que no requieren ese rendimiento del disco, a continuación, puede volver a crear Hola máquina virtual como una VM de la serie DS y adjuntar VHD de almacenamiento Premium de especificación de tamaño/rendimiento Hola que necesita.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="bf1e9-253">A continuación, podría separar y adjuntar los archivos de base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1e9-254">Al copiar los discos VHD de hello debe ser consciente del tamaño de hello, según el tamaño de hello en cuenta qué tipo de disco de almacenamiento Premium se dividen en, esto determina la especificación de rendimiento de disco.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="bf1e9-255">Tamaño de Azure será de ida y vuelta de toohello más cercano de disco, por lo que si tiene un disco de GB 400, esto se redondeará hasta tooa P20.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="bf1e9-256">Dependiendo de los requisitos de E/S existentes de hello VHD de sistema operativo, no tendrá que toomigrate esta tooa cuenta de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="bf1e9-257">Si se tiene acceso a SQL Server externamente, VIP de servicio de nube de hello cambiará.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="bf1e9-258">También tendrá dos puntos finales tooupdate, ACL y DNS configuración.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="bf1e9-259">Implementaciones existentes que usan grupos de disponibilidad AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="bf1e9-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="bf1e9-260">Para las implementaciones existentes, primero consulte hello [requisitos previos](#prerequisites-for-premium-storage) sección de este tema.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="bf1e9-261">En esta sección, examinaremos, en primer lugar, la forma en que AlwaysOn interactúa con las redes de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="bf1e9-262">A continuación, se interrumpirá hacia abajo las migraciones en escenarios de tootwo: las migraciones que puede tolerar cierto tiempo de inactividad y migraciones donde debe lograr tiempo de inactividad mínimo.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="bf1e9-263">Los grupos de disponibilidad AlwaysOn de SQL Server locales usan un agente de escucha local que registra un nombre DNS virtual junto con una dirección IP que comparten uno o varios servidores SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="bf1e9-264">Cuando los clientes se conectan que se enrutan a través de hello del agente de escucha IP toohello principal de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="bf1e9-265">Éste es el servidor de Hola que posee el recurso siempre IP hello en ese momento.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="bf1e9-267">En Microsoft Azure puede tener solo una IP dirección asignada tooa NIC en hello VM, en orden tooachieve Hola misma capa de abstracción como locales, Azure emplea la dirección IP de hello asignado equilibradores de carga de toohello internas y externas (ILB/ELB).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="bf1e9-268">recurso de IP de Hola que se comparte entre los servidores de Hola se establece toohello mismo IP como hello ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="bf1e9-269">Esta información se publica en hello DNS y tráfico del cliente se pasa a través de réplica de SQL Server principal de hello ILB/ELB toohello.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="bf1e9-270">Hola ILB/ELB sabe que SQL Server es principal, ya que utiliza recursos de sondeos tooprobe Hola siempre IP.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="bf1e9-271">En el ejemplo anterior de hello, sondea cada nodo que tiene un extremo al que hace referencia Hola ELB/ILB, lo que responde es Hola principal de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1e9-272">Hello ILB y ELB tienen asignado tooa servicio de nube de Azure específica, por lo tanto, cualquier migración a la nube en Azure, significará que más probable es que ese Hola que cambiará IP del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="bf1e9-273">Migración de implementaciones de AlwaysOn que permiten cierto tiempo de inactividad</span><span class="sxs-lookup"><span data-stu-id="bf1e9-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="bf1e9-274">Hay dos estrategias toomigrate siempre en las implementaciones que permiten cierto tiempo de inactividad:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="bf1e9-275">**Agregar más tooan réplicas secundarias existentes siempre en clúster**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="bf1e9-276">**Migrar tooa nuevo siempre en clúster**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="bf1e9-277">1. Agregar más tooan réplicas secundarias existentes siempre en clúster</span><span class="sxs-lookup"><span data-stu-id="bf1e9-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="bf1e9-278">Una estrategia es tooadd más secundarias toohello siempre en el grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="bf1e9-279">Estos elementos en un nuevo servicio de nube es necesario tooadd y actualizar el agente de escucha de hello con hello IP de equilibrador de carga nueva.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="bf1e9-280">Puntos de tiempo de inactividad:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-280">Points of downtime:</span></span>
* <span data-ttu-id="bf1e9-281">Validación de clústeres.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-281">Cluster Validation.</span></span>
* <span data-ttu-id="bf1e9-282">Pruebas de las conmutaciones por error de AlwaysOn en los elementos secundarios nuevos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="bf1e9-283">Si usas grupos de almacenamiento de Windows dentro de hello VM para un mayor rendimiento de E/S, a continuación, estos se desconectará durante una validación de clúster completa.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="bf1e9-284">prueba de validación de Hello es necesaria cuando agregue nodos toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="bf1e9-285">tiempo de Hola que tarda la prueba de hello toorun puede variar, por lo que debe probar esto en su tooget del entorno de prueba representativo un tiempo aproximado de cuánto se tardará.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="bf1e9-286">Debe aprovisionar que puede realizar la conmutación por error manual y chaos pruebas en hello recién agregado funciones de alta disponibilidad de AlwaysOn de nodos tooensure según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="bf1e9-288">Se deben detener todas las instancias de SQL Server que se usan los grupos de almacenamiento de hello antes de hello la validación se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="bf1e9-289">Pasos de alto nivel</span><span class="sxs-lookup"><span data-stu-id="bf1e9-289">High-level steps</span></span>
>

1. <span data-ttu-id="bf1e9-290">Cree dos nuevos servidores SQL Server en el nuevo servicio en la nube con el almacenamiento Premium conectado.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="bf1e9-291">Copie las de copias de seguridad completas y restáurelas con **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="bf1e9-292">Copie los objetos dependientes “fuera de la base de datos de usuario”, como los inicios de sesión, etc.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="bf1e9-293">Cree un equilibrador de carga interno nuevo (ILB) o use un equilibrador de carga externo (ELB) y, a continuación, configure los extremos de carga equilibrada en ambos nodos nuevos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bf1e9-294">Compruebe que todos los nodos tienen la configuración de punto de conexión correcto Hola antes de continuar</span><span class="sxs-lookup"><span data-stu-id="bf1e9-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="bf1e9-295">Detener toohello de acceso de usuario/aplicaciones SQL Server (si utiliza grupos de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="bf1e9-296">Detenga los servicios del motor de SQL Server en todos los nodos (si usa grupos de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="bf1e9-297">Agregar nueva toocluster de nodos y ejecute la validación completa.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="bf1e9-298">Una vez que la validación sea correcta, inicie todos los servicios de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="bf1e9-299">Haga una copia de seguridad de los registros de transacciones y restaure las bases de datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="bf1e9-300">Agregue nuevos nodos en hello siempre en el grupo de disponibilidad y coloque la replicación en **sincrónica**.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="bf1e9-301">Agregar IP de hello el recurso de dirección de hello servicio de nube nuevo ILB/ELB a través de PowerShell para AlwaysOn tomando como ejemplo de varios sitios de Hola Hola [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="bf1e9-302">En los clústeres de Windows, establecer hello **posibles propietarios** de hello **dirección IP** recursos toohello nuevos nodos anteriores.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="bf1e9-303">Consulte la sección 'Agregar recurso de dirección IP en la misma subred' de Hola de hello [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="bf1e9-304">Tooone de conmutación por error de nuevos nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="bf1e9-305">Realizar Hola nuevos nodos asociados de conmutación por error automática y probar las conmutaciones por error.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="bf1e9-306">Quite los nodos originales del grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="bf1e9-307">Ventajas</span><span class="sxs-lookup"><span data-stu-id="bf1e9-307">Advantages</span></span>
* <span data-ttu-id="bf1e9-308">Puede ser nuevos servidores de SQL comprobado (SQL Server y aplicación) antes de que se agregan tooAlways en.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="bf1e9-309">Puede cambiar el tamaño de la máquina virtual de Hola y personalizar requisitos exactos de hello almacenamiento tooyour.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="bf1e9-310">Sin embargo, sería beneficioso tookeep todas las rutas de acceso de archivo SQL Hola Hola igual.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="bf1e9-311">Puede controlar cuando se inicia la transferencia Hola de toohello de las copias de seguridad de base de datos de hello las réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="bf1e9-312">Esto difiere del uso de Azure **AzureStorageBlobCopy inicio** commandlet toocopy discos duros virtuales, ya que es una copia asincrónica.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="bf1e9-313">Desventajas</span><span class="sxs-lookup"><span data-stu-id="bf1e9-313">Disadvantages</span></span>
* <span data-ttu-id="bf1e9-314">Al utilizar grupos de almacenamiento de Windows, hay un tiempo de inactividad de clúster durante Hola validación de clúster completa para los nodos adicionales de hello nueva.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="bf1e9-315">Según Hola versión de SQL Server y número existente de Hola de réplicas secundarias, podría no ser capaz de tooadd varias réplicas secundarias sin quitar réplicas secundarias existentes.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="bf1e9-316">Podría haber mucho tiempo de transferencia de datos SQL al configurar los elementos secundarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="bf1e9-317">Hay costos adicionales durante la migración cuando se tienen máquinas nuevas que se ejecutan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="bf1e9-318">2. Migrar tooa nuevo siempre en clúster</span><span class="sxs-lookup"><span data-stu-id="bf1e9-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="bf1e9-319">Otra estrategia es toocreate un nuevo siempre en clúster con completamente nuevos nodos en el nuevo servicio de nube y, a continuación, toouse de los clientes de Hola de redirección.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="bf1e9-320">Puntos de tiempo de inactividad</span><span class="sxs-lookup"><span data-stu-id="bf1e9-320">Points of downtime</span></span>
<span data-ttu-id="bf1e9-321">No hay tiempo de inactividad cuando la transferencia de aplicaciones y usuarios toohello nuevo siempre en agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="bf1e9-322">tiempo de inactividad de Hello depende de:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-322">hello downtime depends on:</span></span>

* <span data-ttu-id="bf1e9-323">Hola tiempo toodatabases de copias de seguridad de registro de transacciones final toorestore en los nuevos servidores.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="bf1e9-324">Hola tiempo tooupdate aplicaciones toouse nueva siempre en escucha de cliente.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="bf1e9-325">Ventajas</span><span class="sxs-lookup"><span data-stu-id="bf1e9-325">Advantages</span></span>
* <span data-ttu-id="bf1e9-326">Puede probar el entorno de producción real de hello, SQL Server, y cambios de compilación del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="bf1e9-327">Tiene dispositivos de almacenamiento de hello opción toocustomize hello y toopotentially reducir el tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="bf1e9-328">Esto podría reducir los costos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="bf1e9-329">Puede actualizar su compilación o versión de SQL Server durante este proceso.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="bf1e9-330">También puede actualizar Hola sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="bf1e9-331">Hola que anterior siempre clúster puede actuar como un destino de reversión sólido.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="bf1e9-332">Desventajas</span><span class="sxs-lookup"><span data-stu-id="bf1e9-332">Disadvantages</span></span>
* <span data-ttu-id="bf1e9-333">Nombre DNS de hello toochange del agente de escucha de hello necesita si desea que ambos clústeres siempre en ejecución de forma simultánea.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="bf1e9-334">Esto agrega administración sobrecarga durante la migración de hello como las cadenas de la aplicación de cliente deben reflejar el nuevo nombre de agente de escucha Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="bf1e9-335">Debe implementar un mecanismo de sincronización entre Hola dos entornos tookeep como cerrar como requisitos de sincronización final de hello toominimize posibles antes de la migración.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="bf1e9-336">Se agrega costes durante la migración mientras se tiene que ejecutar de nuevo entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="bf1e9-337">Migración de las implementaciones de AlwaysOn para reducir el tiempo de inactividad al mínimo</span><span class="sxs-lookup"><span data-stu-id="bf1e9-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="bf1e9-338">Hay dos estrategias para migrar las implementaciones de AlwaysOn de tal modo que el tiempo de inactividad sea mínimo:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="bf1e9-339">**Usar un elemento secundario existente: sitio único**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="bf1e9-340">**Usar una réplica de un elemento secundario existente: multisitio**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="bf1e9-341">1. Usar un elemento secundario existente: sitio único</span><span class="sxs-lookup"><span data-stu-id="bf1e9-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="bf1e9-342">Una estrategia de tiempo de inactividad mínimo es tootake una existente en la nube secundaria y quítelo del servicio de nube de hello actual.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="bf1e9-343">A continuación, copie hello toohello de discos duros virtuales nueva cuenta de almacenamiento Premium y cree Hola VM Hola nuevo servicio en nube.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="bf1e9-344">A continuación, actualice el agente de escucha de hello en clústeres y la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="bf1e9-345">Puntos de tiempo de inactividad</span><span class="sxs-lookup"><span data-stu-id="bf1e9-345">Points of downtime</span></span>
* <span data-ttu-id="bf1e9-346">No hay tiempo de inactividad cuando se actualiza el nodo final de hello con el extremo de equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="bf1e9-347">La reconexión del cliente podría retrasarse en función de la configuración de cliente/DNS.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="bf1e9-348">No hay tiempo de inactividad adicional si elige tootake Hola siempre clúster grupo sin conexión tooswap las direcciones IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="bf1e9-349">Puede evitar esto mediante el uso de una dependencia OR y propietarios posibles para hello agregó el recurso de dirección IP.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="bf1e9-350">Consulte la sección 'Agregar recurso de dirección IP en la misma subred' de Hola de hello [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="bf1e9-351">Cuando quiera Hola toopartake nodo agregado en como siempre en Failover Partner, deberá tooadd un extremo de Azure con un toohello de referencia de carga equilibrada establece.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="bf1e9-352">Cuando ejecute hello **Add-AzureEndpoint** comando toodo, tooremain actual de conexiones abierta, pero el nuevo agente de escucha de conexiones toohello no será capaz de toobe establecida hasta que haya actualizado el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="bf1e9-353">En las pruebas Esto se toolast encontrada 90-120 segundos, se debe probar.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="bf1e9-354">Ventajas</span><span class="sxs-lookup"><span data-stu-id="bf1e9-354">Advantages</span></span>
* <span data-ttu-id="bf1e9-355">No se incurre en más gastos durante la migración.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="bf1e9-356">Migración uno a uno.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-356">A one-to-one migration.</span></span>
* <span data-ttu-id="bf1e9-357">Menor complejidad.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-357">Reduced complexity.</span></span>
* <span data-ttu-id="bf1e9-358">Admite una mayor IOPS en los SKU de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="bf1e9-359">Cuando Hola discos desasociados de hello VM y copian toohello nuevo servicio en la nube, un 3rd party herramienta puede ser tamaño de disco duro virtual de hello tooincrease usado, que proporciona un mayor rendimiento.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="bf1e9-360">Para aumentar el tamaño del VHD, consulte este [debate de foro](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="bf1e9-361">Desventajas</span><span class="sxs-lookup"><span data-stu-id="bf1e9-361">Disadvantages</span></span>
* <span data-ttu-id="bf1e9-362">Hay una pérdida temporal de alta disponibilidad y recuperación ante desastres durante la migración.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="bf1e9-363">Tal y como se trata de una migración de 1:1, tendrá que toouse es un tamaño mínimo de máquina virtual que vaya a admitir el número de discos duros virtuales, por lo que quizás no pueda toodownsize las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="bf1e9-364">Este escenario utilizaría hello Azure **AzureStorageBlobCopy inicio** commandlet, que es asincrónico.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="bf1e9-365">No hay ningún contrato de nivel de servicio cuando finaliza la copia.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="bf1e9-366">tiempo de Hola de hello copias varía, aunque esto depende de espera en cola que también dependerá de cantidad de Hola de tootransfer de datos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="bf1e9-367">el tiempo de copia de Hello aumenta si transferencia Hola va tooanother centro de datos de Azure que admite el almacenamiento de Premium en otra región.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="bf1e9-368">Si solo tiene 2 nodos, tenga en cuenta una mitigación posibles en caso de que copia Hola tarda más en las pruebas.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="bf1e9-369">Esto podría incluir Hola después ideas.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="bf1e9-370">Agregar un nodo 3rd temporal de SQL Server para alta disponibilidad antes de la migración de hello acordada tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="bf1e9-371">Ejecutar migración Hola fuera de Azure mantenimiento programado.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="bf1e9-372">Asegúrese de que ha configurado correctamente el cuórum de clúster.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="bf1e9-373">Pasos de alto nivel</span><span class="sxs-lookup"><span data-stu-id="bf1e9-373">High-level steps</span></span>
<span data-ttu-id="bf1e9-374">Este documento no muestra un ejemplo de tooend final completa, sin embargo Hola [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) proporciona detalles que pueden ser aprovechado tooperform esto.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="bf1e9-376">Configuración de disco de recopilación y quitar un nodo hello (no elimine VHD conectados).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="bf1e9-377">Cree una cuenta de almacenamiento Premium y copiar discos duros virtuales de hello cuenta de almacenamiento estándar</span><span class="sxs-lookup"><span data-stu-id="bf1e9-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="bf1e9-378">Crear nuevo servicio de nube y volver a implementar Hola SQL2 VM en ese servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="bf1e9-379">Crear hello VM con hello copian los VHD de sistema operativo original y adjuntar Hola copia discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="bf1e9-380">Configure ILB/ELB y agregue extremos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="bf1e9-381">Actualice el agente de escucha de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-381">Update Listener by either:</span></span>
  * <span data-ttu-id="bf1e9-382">Tomar Hola siempre está en el grupo sin conexión y actualización Hola siempre en agente de escucha con ILB nuevo / dirección IP de ELB.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="bf1e9-383">O bien, agregar el recurso de dirección IP de Hola de nuevo en la nube servicio ILB/ELB a través de PowerShell en clústeres de Windows.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="bf1e9-384">A continuación, conjunto Hola posibles propietarios de toohello de recurso de dirección IP de hello migran nodo, SQL2 y establecerla como la dependencia OR Hola nombre de red.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="bf1e9-385">Consulte la sección 'Agregar recurso de dirección IP en la misma subred' de Hola de hello [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="bf1e9-386">Compruebe a los clientes de toohello de configuración/propagación DNS.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="bf1e9-387">Migre la máquina virtual SQL1 y siga los pasos del 2 al 4.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="bf1e9-388">Si usa los pasos 5ii, a continuación, agregue SQL1 como un posible propietario de hello agrega el recurso de dirección IP</span><span class="sxs-lookup"><span data-stu-id="bf1e9-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="bf1e9-389">Pruebe las conmutaciones por error.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="bf1e9-390">2. Usar una réplica de un elemento secundario existente: multisitio</span><span class="sxs-lookup"><span data-stu-id="bf1e9-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="bf1e9-391">Si tienes nodos en más de un centro de datos Azure (DC) o si tiene un entorno híbrido, puede usar una configuración de AlwaysOn en este tiempo de inactividad de toominimize de entorno.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="bf1e9-392">enfoque de Hello es toochange Hola siempre en sincronización tooSynchronous para hello local o controlador de dominio secundario de Azure y, a continuación, conmutación por error sobre toothat SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="bf1e9-393">A continuación, copie Hola discos duros virtuales tooa cuenta de almacenamiento Premium y volver a implementar la máquina de hello en un nuevo servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="bf1e9-394">Actualizar el agente de escucha de hello y, a continuación, realizar conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="bf1e9-395">Puntos de tiempo de inactividad</span><span class="sxs-lookup"><span data-stu-id="bf1e9-395">Points of downtime</span></span>
<span data-ttu-id="bf1e9-396">tiempo de inactividad de Hello está formada por toofailover toohello alternativa DC de hello tiempo y viceversa.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="bf1e9-397">También depende de la configuración de cliente/DNS, y la reconexión del cliente podría retrasarse.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="bf1e9-398">Considere la posibilidad de hello siguiente ejemplo de una configuración híbrida Always On:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="bf1e9-400">Ventajas</span><span class="sxs-lookup"><span data-stu-id="bf1e9-400">Advantages</span></span>
* <span data-ttu-id="bf1e9-401">Puede usar la infraestructura existente.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="bf1e9-402">Tener Hola Hola de actualización de toopre opción almacenamiento de Azure en hello Azure DR DC en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="bf1e9-403">puede volver a configurar Hola almacenamiento de Azure DR DC.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="bf1e9-404">Se produce un mínimo de dos conmutaciones por error durante la migración, excluidas las conmutaciones por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="bf1e9-405">No necesita datos de SQL Server toomove con copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="bf1e9-406">Desventajas</span><span class="sxs-lookup"><span data-stu-id="bf1e9-406">Disadvantages</span></span>
* <span data-ttu-id="bf1e9-407">Según tooSQL de acceso de cliente servidor, puede haber una mayor latencia cuando SQL Server se ejecuta en una aplicación de toohello de controlador de dominio alternativa.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="bf1e9-408">tiempo de copia de Hola de almacenamiento de discos duros virtuales tooPremium podría ser largo.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="bf1e9-409">Esto podría afectar a la decisión sobre si tookeep Hola nodo Hola grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="bf1e9-410">Tenga en cuenta esto cuando la carga se ejecuta durante la migración de Hola de trabajo intensivas de registro es necesario, ya que el nodo principal Hola tendrá tookeep Hola transacciones sin replicar en su registro de transacciones.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="bf1e9-411">En consecuencia, este podría aumentar de forma significativa.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="bf1e9-412">Este escenario utilizaría hello Azure **AzureStorageBlobCopy inicio** commandlet, que es asincrónico.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="bf1e9-413">No hay ningún contrato de nivel de servicio al finalizar.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-413">There is no SLA on completion.</span></span> <span data-ttu-id="bf1e9-414">Hello tiempo de hello copias varía, aunque esto depende de espera en cola, también dependerá de cantidad de Hola de tootransfer de datos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="bf1e9-415">Por lo tanto, sólo tiene un nodo en el centro de datos 2, debe seguir los pasos de mitigación en caso de que copia Hola tarda más en las pruebas.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="bf1e9-416">Esto podría incluir Hola después ideas.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="bf1e9-417">Agregar un nodo SQL 2nd temporal para alta disponibilidad antes de la migración de hello acordada tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="bf1e9-418">Ejecutar migración Hola fuera de Azure mantenimiento programado.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="bf1e9-419">Asegúrese de que ha configurado correctamente el cuórum de clúster.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="bf1e9-420">Este escenario se supone que ha documentado la instalación y saber cómo se asigna almacenamiento hello en toomake ordenar los cambios de configuración de la caché de disco óptimo.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="bf1e9-421">Pasos de alto nivel</span><span class="sxs-lookup"><span data-stu-id="bf1e9-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="bf1e9-423">Asegúrese de Hola local / alternar Hola de controlador de dominio de Azure SQL Server principal y configurarlo como Hola otro asociado de conmutación por error automática (AFP).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="bf1e9-424">Recopilar la información de configuración de disco SQL2 y quitar un nodo hello (no eliminar adjuntos discos duros virtuales).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="bf1e9-425">Cree una cuenta de almacenamiento Premium y copiar discos duros virtuales de hello cuenta de almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="bf1e9-426">Crear un nuevo servicio de nube y cree Hola SQL2 VM con los discos de almacenamiento de bonificaciones adjuntados.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="bf1e9-427">Configure ILB/ELB y agregue extremos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="bf1e9-428">Hola de actualización siempre en agente de escucha con ILB nuevo / ELB IP dirección y prueba failover.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="bf1e9-429">Compruebe la configuración de DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="bf1e9-430">Cambiar hello tooSQL2 AFP y, a continuación, migrar SQL1 y vaya a través de los pasos del 2 al 5.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="bf1e9-431">Pruebe las conmutaciones por error.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-431">Test failovers.</span></span>
* <span data-ttu-id="bf1e9-432">Cambiar tooSQL1 atrás Hola AFP y SQL2</span><span class="sxs-lookup"><span data-stu-id="bf1e9-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="bf1e9-433">Apéndice: Migrar a un almacenamiento de la funcionalidad de multisitio siempre en clúster tooPremium</span><span class="sxs-lookup"><span data-stu-id="bf1e9-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="bf1e9-434">resto de Hola de este tema proporciona un ejemplo detallado de conversión de un almacenamiento tooPremium multisitio siempre en clúster.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="bf1e9-435">También convierte Hola agente de escucha del uso de un equilibrador de carga interno de tooan (ELB) de equilibrador de carga externo (ILB).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="bf1e9-436">Environment</span><span class="sxs-lookup"><span data-stu-id="bf1e9-436">Environment</span></span>
* <span data-ttu-id="bf1e9-437">Windows 2k12 / SQL 2k12</span><span class="sxs-lookup"><span data-stu-id="bf1e9-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="bf1e9-438">1 archivo de base de datos en SP</span><span class="sxs-lookup"><span data-stu-id="bf1e9-438">1 DB Files on SP</span></span>
* <span data-ttu-id="bf1e9-439">2 grupos de almacenamiento por nodo</span><span class="sxs-lookup"><span data-stu-id="bf1e9-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="bf1e9-441">Máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bf1e9-441">VM:</span></span>
<span data-ttu-id="bf1e9-442">En este ejemplo vamos toodemonstrate mover desde un tooILB ELB.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="bf1e9-443">ELB no estaba disponible antes de ILB, por lo que aquí indica cómo Hola a tooswitch toothis durante la migración.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="bf1e9-445">Los pasos anteriores: Conectar tooSubscription</span><span class="sxs-lookup"><span data-stu-id="bf1e9-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="bf1e9-446">Paso 1: Crear una cuenta de almacenamiento y un servicio en la nube nuevos</span><span class="sxs-lookup"><span data-stu-id="bf1e9-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="bf1e9-447">Paso 2: Hola de aumento permitida errores en los recursos<Optional></span><span class="sxs-lookup"><span data-stu-id="bf1e9-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="bf1e9-448">En determinados recursos que pertenecen tooyour grupo de disponibilidad AlwaysOn hay límites en cuántos errores que pueden producirse en un tiempo, donde el servicio de clúster de Hola tratará de grupo de recursos de hello toorestart.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="bf1e9-449">Se recomienda que aumentar este mientras se recorrer a través de este procedimiento, ya que si no lo hace manualmente conmutaciones por error de conmutación por error y se desencadena al apagar máquinas pueden obtener el límite de toothis cerrar.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="bf1e9-450">Podría ser tolerancia de error de hello toodouble prudente, toodo esto en el Administrador de clústeres de conmutación por error, consulte toohello propiedades Hola Always On del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="bf1e9-452">Cambiar hello too6 máximo de errores.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="bf1e9-453">Paso 3: Agregar el recurso de dirección IP para el grupo de clústeres <Optional></span><span class="sxs-lookup"><span data-stu-id="bf1e9-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="bf1e9-454">Si tiene sólo una dirección IP para hello grupo de clúster y se trata de subred de toohello alineado en la nube, tenga cuidado, si accidentalmente realizar sin conexión todos los nodos de clúster en la nube de hello en que red, a continuación, el recurso de clúster IP de Hola y nombre de red de clúster no será capaz de toocome en línea.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="bf1e9-455">Hola eventos de esto impedirá que actualiza tooother los recursos de clúster.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="bf1e9-456">Paso 4: Configuración de DNS</span><span class="sxs-lookup"><span data-stu-id="bf1e9-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="bf1e9-457">tooimplement una transición sin problemas depende de cómo se va DNS utilizan y actualizan.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="bf1e9-458">Cuando se instala siempre en, crea un grupo de recursos de clúster de Windows, si abre el Administrador de clústeres de conmutación por error, verá que como mínimo tendrá tres recursos, Hola dos que Hola documento hace referencia tooare:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="bf1e9-459">Nombre de red virtual (VNN): se trata de hello DNS nombre de ese cliente conectarse toowhen que deseaba un tooconnect tooSQL servidores a través de AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="bf1e9-460">El recurso de dirección IP: se trata de Hola de direcciones IP que asociado hello VNN, puede tener más de uno y en una configuración multisitio tendrá una dirección IP por subred del sitio.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="bf1e9-461">Cuando se recuperar registros DNS de hello asociados con el agente de escucha de Hola y se trata de tooconnect tooeach tooSQL conexión Server, controlador de SQL Server Client Hola siempre en había asociado dirección IP, a continuación se explican algunos de los factores que pueden influir en esto.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="bf1e9-462">Hello número simultáneos de registros de DNS que están asociados con el nombre de agente de escucha de hello depende no solo de número de Hola de direcciones IP asociadas, pero hello ' RegisterAllIpProviders'setting en el clúster de conmutación por error para hello recursos siempre ON VNN.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="bf1e9-463">Cuando se implementa de AlwaysOn en Azure hay pasos diferentes toocreate Hola agente de escucha y las direcciones IP, tiene toomanually configurar hello 'RegisterAllIpProviders' too1, esto es diferente tooan local siempre en la implementación donde ya se ha establecido too1.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="bf1e9-464">Si 'RegisterAllIpProviders' es 0, sólo verá registro DNS en DNS asociado Hola agente de escucha:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="bf1e9-466">Si “RegisterAllIpProviders” es 1:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="bf1e9-468">siguiente de código de Hello se volcar Hola configuración VNN y se establecen automáticamente, por favor, tenga en cuenta que para hello Cambiar efecto tootake necesitará tootake hello VNN sin conexión y en línea volver a activarlo, este tomar Hola agente de escucha sin conexión que producen cliente conectividad interrupción.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="bf1e9-469">En un paso posterior de la migración se necesitarán tooupdate Hola siempre escucha de con una dirección IP actualizada que hará referencia a un equilibrador de carga, esto implica una eliminación de recursos de dirección IP y las sumas.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="bf1e9-470">Después de la actualización IP de hello, deberá tooensure Hola nueva dirección IP se ha actualizado en la zona DNS y que los clientes de Hola son actualizar su caché DNS local.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="bf1e9-471">Si los clientes residen en un segmento de red diferente y hacer referencia a un servidor DNS diferente, deberá tooconsider lo que sucede con transferencia de zona DNS durante la migración de hello, como hello aplicación volver a conectarse se restringirá tiempo por Hola al menos el tiempo de transferencia de zona de las nuevas direcciones IP para el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="bf1e9-472">Si está en la restricción del tiempo, debe analizar y probar forzando una transferencia de zona incremental con los equipos de Windows, y también coloca Hola DNS tooa registros de host reducir tiempo tooLive (TTL), para actualizan los clientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="bf1e9-473">Para más información, consulte las [transferencias de zona incrementales](https://technet.microsoft.com/library/cc958973.aspx) y [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="bf1e9-474">Hola predeterminado TTL de registro DNS que está asociado con hello escucha en Always On en Azure es 1.200 segundos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="bf1e9-475">Es recomendable tooreduce esto si se encuentra en la restricción del tiempo durante la actualización de los clientes de migración tooensure Hola sus DNS con la dirección IP de hello actualiza una dirección para el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="bf1e9-476">Puede ver y modificar configuración de hello mediante el volcado de configuración de Hola Hola VNN:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="bf1e9-477">Tenga en cuenta, Hola Hola inferior 'HostRecordTTL', se producirá una mayor cantidad de tráfico DNS.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="bf1e9-478">Configuración de la aplicación cliente</span><span class="sxs-lookup"><span data-stu-id="bf1e9-478">Client application settings</span></span>
<span data-ttu-id="bf1e9-479">Si la aplicación de cliente SQL es compatible con .NET Framework 4.5 de Hola SQLClient; a continuación, puede usar ' MULTISUBNETFAILOVER = TRUE' palabra clave, se recomienda hacer esto toobe aplicada tal y como permite para tooSQL de conexión más rápido siempre en el grupo de disponibilidad durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="bf1e9-480">Enumera todas las direcciones IP asociadas con hello siempre en agente de escucha en paralelo y realiza una velocidad de reintento de conexión TCP más agresiva durante una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="bf1e9-481">Para obtener más información sobre la configuración de hello anterior, vea [palabra clave MultiSubnetFailover y características asociadas con](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="bf1e9-482">Consulte también [Compatibilidad de SqlClient para la alta disponibilidad y la recuperación ante desastres](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="bf1e9-483">Paso 5: Configuración del cuórum de clúster</span><span class="sxs-lookup"><span data-stu-id="bf1e9-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="bf1e9-484">Como va toobe sacar al menos un servidor de SQL hacia abajo a la vez, debe modificar la configuración de quórum de clúster de hello, si usa el testigo de recurso compartido de archivos (FSW) con 2 nodos, debe establecer la mayoría de nodo de hello quórum tooallow y utilizar el voto dinámico y se trata de tooallow para un pie de tooremain de nodo único.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="bf1e9-485">Para obtener más información sobre la administración y configuración de quórum de clúster de hello, visite [configurar y administrar Hola quórum en un clúster de conmutación por error de Windows Server 2012](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf1e9-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="bf1e9-486">Paso 6: Extraer los extremos y las ACL existentes</span><span class="sxs-lookup"><span data-stu-id="bf1e9-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="bf1e9-487">Guardar estos archivos de texto tooa.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="bf1e9-488">Paso 7: Cambiar los asociados de conmutación por error y los modos de replicación</span><span class="sxs-lookup"><span data-stu-id="bf1e9-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="bf1e9-489">Si tiene más de 2 servidores SQL Server, se debe cambiar la conmutación por error de Hola de otra base de datos secundaria en otro controlador de dominio o local 'too'Synchronous y que sea un asociado de conmutación por error automática (AFP), por lo que mantener la alta disponibilidad al tiempo que se va a realizar cambios.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="bf1e9-490">Puede hacerlo a través de TSQL o modificarlo mediante SSMS:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="bf1e9-492">Paso 8: Quitar la VM secundaria del servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="bf1e9-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="bf1e9-493">Debe prepararse toomigrate un nodo secundario en la nube en primer lugar, si se trata actualmente principal, debe iniciar una conmutación por error manual.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="bf1e9-494">Paso 9: Cambiar la configuración de la caché de disco en el archivo CSV y guardarla</span><span class="sxs-lookup"><span data-stu-id="bf1e9-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="bf1e9-495">Para volúmenes de datos se debe establecer tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="bf1e9-496">Para volúmenes de registro de transacciones se debe establecer tooNONE.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-496">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="bf1e9-498">Paso 10: Copiar los VHD</span><span class="sxs-lookup"><span data-stu-id="bf1e9-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="bf1e9-499">Puede comprobar estado de la copia de Hola de hello discos duros virtuales toohello cuenta de almacenamiento Premium:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

<span data-ttu-id="bf1e9-501">Espere hasta que todos se registren como correctos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="bf1e9-502">Para obtener información sobre blobs individuales:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="bf1e9-503">Paso 11: Registrar el disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="bf1e9-503">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="bf1e9-504">Paso 12: Importar el elemento secundario en el nuevo servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="bf1e9-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="bf1e9-505">código de Hello siguiente también se agregan Hola de usos opción aquí se puede importar la máquina de Hola y utilizar hello conservable VIP.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="bf1e9-506">Paso 13: Crear ILB en SVC en la nube nuevo y agregar extremos de carga equilibrada y ACL</span><span class="sxs-lookup"><span data-stu-id="bf1e9-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="bf1e9-507">Paso 14: Actualizar AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="bf1e9-507">Step 14: Update Always On</span></span>
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="bf1e9-509">Quitar ahora Hola antiguo servicio en la nube dirección IP.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-509">Now remove hello old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="bf1e9-511">Paso 15: Comprobar actualizaciones de DNS</span><span class="sxs-lookup"><span data-stu-id="bf1e9-511">Step 15: DNS update check</span></span>
<span data-ttu-id="bf1e9-512">Ahora debe comprobar los servidores DNS en sus redes de cliente de SQL Server y asegúrese de que la agrupación en clústeres se agregado Hola registro host adicionales para hello agrega dirección IP.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="bf1e9-513">Si no han actualizado los servidores DNS, considere la posibilidad de forzar a una transferencia de zona DNS y asegúrese de que los clientes en la subred ahí hello sean tooresolve pueda tooboth siempre en direcciones IP, por lo que no es necesario toowait para la replicación automática de DNS.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="bf1e9-514">Paso 16: Reconfigurar AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="bf1e9-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="bf1e9-515">En este momento espere Hola secundaria ese nodo que fue migrado toofully volver a sincronizar con el nodo local de Hola y cambie el nodo de replicación toosynchronous y hacerla AFP Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="bf1e9-516">Paso 17: Migrar el nodo secundario</span><span class="sxs-lookup"><span data-stu-id="bf1e9-516">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="bf1e9-517">Paso 18: Cambiar la configuración de la caché de disco en el archivo CSV y guardarla</span><span class="sxs-lookup"><span data-stu-id="bf1e9-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="bf1e9-518">Para volúmenes de datos se debe establecer tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="bf1e9-519">Para volúmenes de registro de transacciones se debe establecer tooNONE.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-519">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="bf1e9-521">Paso 19: Crear una nueva cuenta de almacenamiento independiente para el nodo secundario</span><span class="sxs-lookup"><span data-stu-id="bf1e9-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="bf1e9-522">Paso 20: Copiar los VHD</span><span class="sxs-lookup"><span data-stu-id="bf1e9-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="bf1e9-523">Puede comprobar el estado de copia de disco duro virtual de Hola para todos los discos duros virtuales: ForEach ($disk en $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. EtiquetaDeDisco $diskName = $disk. DiskName</span><span class="sxs-lookup"><span data-stu-id="bf1e9-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="bf1e9-525">Espere hasta que todos se registren como correctos.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="bf1e9-526">Para obtener información sobre blobs individuales:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="bf1e9-527">Paso 21: Registrar el disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="bf1e9-527">Step 21: Register OS disk</span></span>
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="bf1e9-528">Paso 22: Agregar extremos de carga equilibrada y ACL</span><span class="sxs-lookup"><span data-stu-id="bf1e9-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="bf1e9-529">Paso 23: Probar la conmutación por error</span><span class="sxs-lookup"><span data-stu-id="bf1e9-529">Step 23: Test failover</span></span>
<span data-ttu-id="bf1e9-530">Ahora debe permitir que Hola migrados nodo sincronizar con hello local siempre en el nodo, lo coloca en modo de replicación toosynchronous y espere hasta que se sincronicen.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="bf1e9-531">A continuación, migra conmutación por error de local toohello primer nodo que es AFP Hola.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="bf1e9-532">Una vez que ha funcionado, cambio Hola migrado por última vez nodo toohello AFP.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="bf1e9-533">Debe probar las conmutaciones por error entre todos los nodos y se ejecutan aunque pruebas chaos tooensure las conmutaciones por error de trabajo como se esperaba y en un tiempo manor.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="bf1e9-534">Paso 24: Reponer la configuración del cuórum de clúster / TTL de DNS / asociados de conmutación por error / configuración de sincronización</span><span class="sxs-lookup"><span data-stu-id="bf1e9-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="bf1e9-535">Agregar un recurso de dirección IP en la misma subred</span><span class="sxs-lookup"><span data-stu-id="bf1e9-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="bf1e9-536">Si tiene sólo 2 servidores SQL Server y desea toomigrate les tooa nuevo servicio en la nube, pero desea tookeep cambiarlas en Hola misma subred, puede evitar teniendo el agente de escucha de hello toodelete sin conexión Hola siempre original en la dirección IP y agregar Hola nueva dirección IP.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="bf1e9-537">Si va a migrar subred tooanother hello las máquinas virtuales que no necesitará toodo esto como habrá una red de clúster adicionales que hacen referencia a esa subred.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="bf1e9-538">Una vez que haya llevado Hola migra la base de datos secundaria y agrega nuevo recurso de dirección IP hello para el nuevo servicio de nube Hola antes de conmutación por error Hola primario existente, debe completar estos pasos en hello Administrador de clústeres de conmutación por error:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="bf1e9-539">tooadd en dirección IP, vea hello [apéndice](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), paso 14.</span><span class="sxs-lookup"><span data-stu-id="bf1e9-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="bf1e9-540">Para el recurso de dirección IP actual de hello, cambiar propietario posible de hello too'Existing principal de SQL Server ", en el ejemplo de Hola a continuación, 'dansqlams4':</span><span class="sxs-lookup"><span data-stu-id="bf1e9-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="bf1e9-542">Para el recurso de dirección IP nueva hello, cambiar Hola posible propietario too'Migrated SQL Server secundario ', en el ejemplo de Hola a continuación, 'dansqlams5':</span><span class="sxs-lookup"><span data-stu-id="bf1e9-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="bf1e9-544">Una vez que se establece puede conmutar por error y, cuando se migra el último nodo de Hola Hola posibles propietarios debe editarse para que ese nodo se agrega como un propietario posible:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="bf1e9-546">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bf1e9-546">Additional resources</span></span>
* [<span data-ttu-id="bf1e9-547">Almacenamiento Premium de Azure</span><span class="sxs-lookup"><span data-stu-id="bf1e9-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="bf1e9-548">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="bf1e9-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="bf1e9-549">SQL Server en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="bf1e9-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
