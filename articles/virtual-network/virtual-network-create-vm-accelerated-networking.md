---
title: "aaaCreate una máquina virtual de Azure con Accelerated redes | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con Accelerated redes."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="9facc-103">Creación de una máquina virtual con Accelerated Networking</span><span class="sxs-lookup"><span data-stu-id="9facc-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="9facc-104">En este tutorial, aprenderá cómo toocreate una máquina Virtual (VM) de Azure con Accelerated redes.</span><span class="sxs-lookup"><span data-stu-id="9facc-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="9facc-105">Las redes aceleradas están en disponibilidad general para Windows y en versión preliminar pública para distribuciones de Linux específicas.</span><span class="sxs-lookup"><span data-stu-id="9facc-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="9facc-106">Redes acelerada permite tooa virtualización (SR-IOV) de E/S de raíz única máquina virtual, se mejora significativamente el rendimiento de red.</span><span class="sxs-lookup"><span data-stu-id="9facc-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="9facc-107">Esta ruta de acceso de alto rendimiento omite host Hola de ruta de datos de hello reduce la latencia y vibración, uso de CPU, para su uso con hello más exigentes red cargas de trabajo en tipos admitidos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="9facc-108">Hola la siguiente imagen se muestra en comunicación entre dos máquinas virtuales (VM) con y sin redes acelerada:</span><span class="sxs-lookup"><span data-stu-id="9facc-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![De comparación](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="9facc-110">Sin red acelerado, todo el tráfico de red dentro y fuera de hello VM debe atravesar host Hola y el conmutador virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="9facc-111">conmutador virtual de Hello exige la aplicación de directiva de todos los, tales como grupos de seguridad de red acceso a listas de control, aislamiento y otro tráfico de toonetwork de servicios de red virtualizado.</span><span class="sxs-lookup"><span data-stu-id="9facc-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="9facc-112">más información acerca de los modificadores virtuales, leer hello toolearn [virtualización de red de Hyper-V y el conmutador virtual](https://technet.microsoft.com/library/jj945275.aspx) artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="9facc-113">Con las redes acelerada, el tráfico de red llega a la interfaz de red (NIC) de la máquina virtual de hello y, a continuación, se reenvía toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="9facc-114">Se aplica todas las directivas de red que Hola conmutador virtual sin redes acelerada se descarga y se aplican en hardware.</span><span class="sxs-lookup"><span data-stu-id="9facc-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="9facc-115">Aplicar directiva de hardware permite Hola NIC tooforward tráfico de red directamente toohello VM, omitiendo el host de Hola y el conmutador virtual de hello, al tiempo que mantiene todas las directivas de Hola aplica en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="9facc-116">Hello ventajas de las redes acelerada solo aplican toohello máquina virtual que se ha habilitado en.</span><span class="sxs-lookup"><span data-stu-id="9facc-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="9facc-117">Para obtener mejores resultados de hello, resulta ideal tooenable esta característica en al menos dos máquinas virtuales conectadas toohello misma red Virtual de Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="9facc-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="9facc-118">Cuando se comunica a través de redes virtuales o conexión de forma local, esta característica tiene una latencia toooverall un impacto mínimo.</span><span class="sxs-lookup"><span data-stu-id="9facc-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="9facc-119">Este Linux versión preliminar pública que no tenga Hola son del mismo nivel de disponibilidad y confiabilidad como características que por lo general versión de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="9facc-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="9facc-120">características de Hello no se admiten, pueden haber limitado las capacidades y pueden no estar disponibles en todas las ubicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="9facc-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="9facc-121">Para hello más las notificaciones de actualización de disponibilidad y estado de esta característica, consulte la página de actualizaciones de red Virtual de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="9facc-122">Ventajas</span><span class="sxs-lookup"><span data-stu-id="9facc-122">Benefits</span></span>
* <span data-ttu-id="9facc-123">**Menor latencia / superior paquetes por segundo (pps):** conmutador virtual de hello Removing de ruta de datos de hello quita tiempo Hola dedican de paquetes en el host de hello para el procesamiento de directiva y aumenta Hola número de paquetes que se pueden procesar dentro de hello VM.</span><span class="sxs-lookup"><span data-stu-id="9facc-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="9facc-124">**Reduce la vibración:** conmutador Virtual de procesamiento depende de la cantidad de Hola de directiva que necesita toobe aplicado y carga de trabajo Hola de hello CPU que realiza el procesamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="9facc-125">La descarga de hardware de toohello de cumplimiento de directiva de hello quita esa variabilidad proporcionando paquetes directamente toohello máquina virtual, quite interrupciones de software y contexto de comunicación con el host tooVM hello y todos los conmutadores.</span><span class="sxs-lookup"><span data-stu-id="9facc-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="9facc-126">**Reduce el uso de CPU:** omisión Hola del conmutador virtual de host de hello conduce uso de CPU que no requiere herramientas para procesar el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="9facc-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="9facc-127"><a name="Limitations"></a>Limitaciones</span><span class="sxs-lookup"><span data-stu-id="9facc-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="9facc-128">Hola siguientes limitaciones existe cuando se usa esta capacidad:</span><span class="sxs-lookup"><span data-stu-id="9facc-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="9facc-129">**Creación de interfaz de red:** Accelerated Networking solo se puede habilitar para una nueva interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="9facc-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="9facc-130">No se puede habilitar para una NIC existente.</span><span class="sxs-lookup"><span data-stu-id="9facc-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="9facc-131">**Creación de máquinas virtuales:** una NIC con redes acelerada habilitada puede solo tooa adjunto VM cuando hello máquina virtual se creará.</span><span class="sxs-lookup"><span data-stu-id="9facc-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="9facc-132">Hola NIC no puede ser tooan adjunto existente de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="9facc-133">**Regiones:** la mayoría de las regiones de Azure ofrecen máquinas virtuales de Windows con Accelerated Networking.</span><span class="sxs-lookup"><span data-stu-id="9facc-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="9facc-134">En numerosas regiones se ofrecen máquinas virtuales de Linux con redes aceleradas.</span><span class="sxs-lookup"><span data-stu-id="9facc-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="9facc-135">se está expandiendo regiones Hola esta capacidad está disponible en.</span><span class="sxs-lookup"><span data-stu-id="9facc-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="9facc-136">Vea el blog de las actualizaciones de red Virtual de Azure de Hola a continuación para obtener información más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="9facc-137">**Sistemas operativos compatibles:** para Windows, Microsoft Windows Server 2012 R2 Datacenter y Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="9facc-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="9facc-138">Para Linux, Ubuntu Server 16.04 LTS con kernel 4.4.0-77 o superior, SLES 12 SP2, RHEL 7.3 y CentOS 7.3 (publicado por Rogue Wave Software).</span><span class="sxs-lookup"><span data-stu-id="9facc-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="9facc-139">**Tamaño de máquina virtual:** instancias de uso general y de proceso optimizado con ocho o más núcleos.</span><span class="sxs-lookup"><span data-stu-id="9facc-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="9facc-140">Para obtener más información, vea hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) y [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículos de tamaños de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="9facc-141">Hola se expandirá conjunto de tamaños de instancia de máquina virtual admitidos en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="9facc-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="9facc-142">**Implementación mediante Azure Resource Manager (ARM):** la funcionalidad de redes aceleradas no se puede implementar mediante ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="9facc-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="9facc-143">Limitaciones de toothese de cambios se anuncian a través de hello [red Virtual de Azure actualiza](https://azure.microsoft.com/updates/accelerated-networking-in-preview) página.</span><span class="sxs-lookup"><span data-stu-id="9facc-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="9facc-144">Creación de una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="9facc-144">Create a Windows VM</span></span>
<span data-ttu-id="9facc-145">Puede usar Hola portal de Azure o Azure [PowerShell](#windows-powershell) toocreate Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="9facc-146"><a name="windows-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="9facc-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="9facc-147">Desde un explorador de Internet, abra hello Azure [portal](https://portal.azure.com) e inicie sesión con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9facc-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9facc-148">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9facc-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="9facc-149">En el portal de hello, haga clic en **+ nuevo** > **proceso** > **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="9facc-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="9facc-150">Hola **Windows Server 2016 Datacenter** hoja que aparece, deje *el Administrador de recursos* seleccionado en **seleccionar un modelo de implementación**y haga clic en **crear **.</span><span class="sxs-lookup"><span data-stu-id="9facc-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="9facc-151">Hola **Fundamentos** hoja que aparece, escriba Hola después de valores, deje Hola restantes opciones predeterminadas o seleccione o escriba sus propios valores y haga clic en hello **Aceptar** botón:</span><span class="sxs-lookup"><span data-stu-id="9facc-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="9facc-152">Configuración</span><span class="sxs-lookup"><span data-stu-id="9facc-152">Setting</span></span>|<span data-ttu-id="9facc-153">Valor</span><span class="sxs-lookup"><span data-stu-id="9facc-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="9facc-154">Nombre</span><span class="sxs-lookup"><span data-stu-id="9facc-154">Name</span></span>|<span data-ttu-id="9facc-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="9facc-155">MyVm</span></span>|
    |<span data-ttu-id="9facc-156">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="9facc-156">Resource group</span></span>|<span data-ttu-id="9facc-157">Deje seleccionado **Crear nuevo** y escriba *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9facc-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="9facc-158">Ubicación</span><span class="sxs-lookup"><span data-stu-id="9facc-158">Location</span></span>|<span data-ttu-id="9facc-159">Oeste de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="9facc-159">West US 2</span></span>|

    <span data-ttu-id="9facc-160">Si es nuevo tooAzure, obtenga más información sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [suscripciones](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), y [ubicaciones](https://azure.microsoft.com/regions) (que también aparecen tooas regiones).</span><span class="sxs-lookup"><span data-stu-id="9facc-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="9facc-161">Hola **elegir un tamaño de** hoja que aparece, escriba *8* en hello **cantidad mínima de núcleos** cuadro, a continuación, haga clic en **todas las ver**.</span><span class="sxs-lookup"><span data-stu-id="9facc-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="9facc-162">Haga clic en **DS4_V2 estándar**, o cualquier admitido VM, a continuación, haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="9facc-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="9facc-163">Hola **configuración** hoja que aparece, deje todos los valores de configuración como-es, pero sin hacer clic **habilitado** en **Accelerated redes**, a continuación, haga clic en hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="9facc-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="9facc-164">**Nota:** si, en los pasos anteriores, seleccionó valores de tamaño VM, el sistema operativo o la ubicación que no aparezcan en hello [limitaciones](#Limitations) sección de este artículo, **acelerado redes**no está visible.</span><span class="sxs-lookup"><span data-stu-id="9facc-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="9facc-165">Hola **resumen** hoja que aparece, haga clic en hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="9facc-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="9facc-166">Azure comienza a crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="9facc-167">La creación tarda unos minutos.</span><span class="sxs-lookup"><span data-stu-id="9facc-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="9facc-168">Hola tooinstall accelerated controlador de redes para Windows, Hola completa los pasos de hello [configurar Windows](#configure-windows) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="9facc-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="9facc-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="9facc-170">Instale Hola la versión más reciente de hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo.</span><span class="sxs-lookup"><span data-stu-id="9facc-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="9facc-171">Si es nuevo tooAzure PowerShell, leer hello [Introducción a Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="9facc-172">Iniciar una sesión de PowerShell haciendo clic en el botón de inicio de Windows hello, escriba **powershell**, a continuación, haga clic en **PowerShell** en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="9facc-173">En la ventana de PowerShell, escriba Hola `login-azurermaccount` toosign de comando con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9facc-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9facc-174">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9facc-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="9facc-175">En el explorador, copie Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="9facc-175">In your browser, copy hello following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="9facc-176">En la ventana de PowerShell, haga clic en el script de Hola toopaste e iniciará ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="9facc-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="9facc-177">Se le pide un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="9facc-177">You are prompted for a username and password.</span></span> <span data-ttu-id="9facc-178">Usar estas credenciales toolog en toohello VM al conectarse tooit en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="9facc-179">Si se produce un error en la secuencia de comandos de Hola y cambiar valores en el script de Hola antes de ejecutarlo, confirme los valores de hello que ha utilizado para el tamaño de máquina virtual, sistema operativo, y ubicación se muestran en hello [limitaciones](#Limitations) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="9facc-180">Hola tooinstall accelerated controlador de redes para Windows, Hola completa los pasos de hello [configurar Windows](#configure-windows) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="9facc-181"><a name="configure-windows"></a>Configuración de Windows</span><span class="sxs-lookup"><span data-stu-id="9facc-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="9facc-182">Una vez que cree Hola VM en Azure, debe instalar el controlador de red acelerada de Hola para Windows.</span><span class="sxs-lookup"><span data-stu-id="9facc-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="9facc-183">Antes de completar Hola pasos, debe haber creado una máquina virtual de Windows con redes acelerada con cualquier hello [portal](#windows-portal) o [PowerShell](#windows-powershell) los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="9facc-184">Desde un explorador de Internet, abra hello Azure [portal](https://portal.azure.com) e inicie sesión con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9facc-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9facc-185">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9facc-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="9facc-186">En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="9facc-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="9facc-187">Cuando **MyVm** aparece en los resultados de búsqueda de hello, haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="9facc-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="9facc-188">Hola **MyVm** hoja que aparece, haga clic en hello **conectar** botón en hello la esquina superior izquierda de la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="9facc-189">**Nota:** si **crear** está visible en hello **conectar** botón, Azure no ha terminado de crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="9facc-190">Haga clic en **conectar** sólo después de que ya no verá **crear** en hello **conectar** botón.</span><span class="sxs-lookup"><span data-stu-id="9facc-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="9facc-191">Permitir su Hola de explorador toodownload **MyVm.rdp** archivo.</span><span class="sxs-lookup"><span data-stu-id="9facc-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="9facc-192">Una vez descargado, haga clic en hello archivo tooopen lo.</span><span class="sxs-lookup"><span data-stu-id="9facc-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="9facc-193">Haga clic en hello **conectar** botón en hello **conexión a Escritorio remoto** cuadro que aparece, le notifica que hello no se puede identificar el Editor de conexión remota de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="9facc-194">Hola **la seguridad de Windows** cuadro que aparece, haga clic en **más opciones**, a continuación, haga clic en **Use otra cuenta**.</span><span class="sxs-lookup"><span data-stu-id="9facc-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="9facc-195">Escriba el nombre de usuario de Hola y la contraseña que especificó en el paso 4, haga clic en hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="9facc-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="9facc-196">Haga clic en hello **Sí** en botón del cuadro de conexión a Escritorio remoto de Hola que aparece, le notifica que no se puede comprobar la identidad de hello del equipo remoto Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="9facc-197">Haga clic en el botón de inicio de Windows hello y haga clic en **el Administrador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="9facc-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="9facc-198">Expanda hello **adaptadores de red** nodo.</span><span class="sxs-lookup"><span data-stu-id="9facc-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="9facc-199">Confirme que hello **Mellanox ConnectX-3 adaptador de Ethernet de función Virtual** aparece como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="9facc-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![Administrador de dispositivos](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="9facc-201">Las redes aceleradas ya están habilitadas para su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="9facc-202">Creación de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="9facc-202">Create a Linux VM</span></span>
<span data-ttu-id="9facc-203">Puede usar Hola portal de Azure o Azure [PowerShell](#linux-powershell) toocreate un Ubuntu o SLES VM.</span><span class="sxs-lookup"><span data-stu-id="9facc-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="9facc-204">En el caso de las máquinas virtuales RHEL y CentOS, el flujo de trabajo es diferente.</span><span class="sxs-lookup"><span data-stu-id="9facc-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="9facc-205">Consulte las instrucciones de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="9facc-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="9facc-206"><a name="linux-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="9facc-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="9facc-207">Registro de hello accelerated redes de Linux preview siguiendo los pasos del 1 al 5 del programa Hola a [crear una VM Linux - PowerShell](#linux-powershell) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="9facc-208">No se puede registrar para la vista previa de hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="9facc-209">Complete los pasos 1-8 en hello [crear una VM de Windows - portal](#windows-portal) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="9facc-210">En el paso 2, haga clic en **Ubuntu Server 16.04 LTS** en lugar de **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="9facc-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="9facc-211">Para este tutorial, elija toouse una contraseña, en lugar de una clave SSH, aunque para las implementaciones de producción, puede usar.</span><span class="sxs-lookup"><span data-stu-id="9facc-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="9facc-212">Si **Accelerated redes** no aparece cuando se completa el paso 7 de hello [crear una VM de Windows - portal](#windows-portal) sección de este artículo, es probable para uno de hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="9facc-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="9facc-213">No se ha registrado para la vista previa de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="9facc-214">Confirme que el estado de registro es **registrado**, tal como se describe en el paso 4 de hello [crear una VM Linux - Powershell](#linux-powershell) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="9facc-215">**Nota:** si ha participado en hello acelerado de red para la vista previa de máquinas virtuales de Windows (su ningún toouse tooregister necesarios más acelerado de redes para máquinas virtuales de Windows), no se registra automáticamente para hello acelerado red para Obtener una vista previa en máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="9facc-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="9facc-216">Debe registrar para hello acelerado de red para obtener una vista previa en máquinas virtuales de Linux tooparticipate en ella.</span><span class="sxs-lookup"><span data-stu-id="9facc-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="9facc-217">No se ha seleccionado un tamaño VM, el sistema operativo o la ubicación que se indica en hello [limitaciones](#limitations) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="9facc-218">Hola tooinstall accelerated controlador de redes de Linux, Hola completa los pasos de hello [configurar Linux](#configure-linux) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="9facc-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="9facc-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="9facc-220">Si crear máquinas virtuales de Linux con redes acelerada en una suscripción y, a continuación, intente toocreate una VM de Windows con las redes acelerada de Hola misma suscripción, que puede producir un error Hola creación de VM de Windows.</span><span class="sxs-lookup"><span data-stu-id="9facc-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="9facc-221">Durante esta versión preliminar, se recomienda probar las máquinas virtuales Windows y Linux con Accelerated Networking en suscripciones independientes.</span><span class="sxs-lookup"><span data-stu-id="9facc-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="9facc-222">Instale Hola la versión más reciente de hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo.</span><span class="sxs-lookup"><span data-stu-id="9facc-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="9facc-223">Si es nuevo tooAzure PowerShell, leer hello [Introducción a Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="9facc-224">Iniciar una sesión de PowerShell haciendo clic en el botón de inicio de Windows hello, escriba **powershell**, a continuación, haga clic en **PowerShell** en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="9facc-225">En la ventana de PowerShell, escriba Hola `login-azurermaccount` toosign de comando con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9facc-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9facc-226">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9facc-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="9facc-227">Registrarme para hello accelerated redes de Azure preview siguiendo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9facc-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="9facc-228">Enviar un correo electrónico demasiado[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) con su Id. de suscripción de Azure y el uso previsto.</span><span class="sxs-lookup"><span data-stu-id="9facc-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="9facc-229">Espere a recibir una confirmación por correo electrónico de Microsoft que le indique que la suscripción está habilitada.</span><span class="sxs-lookup"><span data-stu-id="9facc-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="9facc-230">Escriba Hola después tooconfirm de comando que se registra para la vista previa de hello:</span><span class="sxs-lookup"><span data-stu-id="9facc-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="9facc-231">No continúe con el paso 5 hasta que **registrado** aparece en hello después de escribir el comando anterior Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="9facc-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="9facc-232">El resultado debe ser similar siguiente de hello resultado antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="9facc-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="9facc-233">Si ha participado en hello acelerado de red para la vista previa de máquinas virtuales de Windows (su ningún toouse tooregister necesarios más acelerado de redes para máquinas virtuales de Windows), no se registra automáticamente para hello acelerado de la red para la vista previa de las máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="9facc-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="9facc-234">Debe registrar para hello acelerado de red para obtener una vista previa en máquinas virtuales de Linux tooparticipate en ella.</span><span class="sxs-lookup"><span data-stu-id="9facc-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="9facc-235">En el explorador, copie Hola siguiente secuencia de comandos sustituyendo Ubuntu o SLES según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9facc-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="9facc-236">Redhat y CentOS tienen un flujo de trabajo diferente, que se describe a continuación:</span><span class="sxs-lookup"><span data-stu-id="9facc-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="9facc-237">En la ventana de PowerShell, haga clic en el script de Hola toopaste e iniciará ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="9facc-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="9facc-238">Se le pide un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="9facc-238">You are prompted for a username and password.</span></span> <span data-ttu-id="9facc-239">Usar estas credenciales toolog en toohello VM al conectarse tooit en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="9facc-240">Si se produce un error en la secuencia de comandos de hello, confirme:</span><span class="sxs-lookup"><span data-stu-id="9facc-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="9facc-241">Se registran para la vista previa de hello, tal como se describe en el paso 4</span><span class="sxs-lookup"><span data-stu-id="9facc-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="9facc-242">Si cambia de tamaño, el tipo de sistema operativo o los valores de ubicación en el script de Hola VM antes de ejecutarlo y que se mostrarán los valores de hello en hello [limitaciones](#Limitations) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="9facc-243">Hola tooinstall accelerated controlador de redes de Linux, Hola completa los pasos de hello [configurar Linux](#configure-linux) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="9facc-244"><a name="configure-linux"></a>Configuración de Linux</span><span class="sxs-lookup"><span data-stu-id="9facc-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="9facc-245">Una vez que cree Hola VM en Azure, debe instalar el controlador de red acelerada de Hola para Linux.</span><span class="sxs-lookup"><span data-stu-id="9facc-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="9facc-246">Antes de completar Hola pasos, debe haber creado una VM de Linux con redes acelerada con cualquier hello [portal](#linux-portal) o [PowerShell](#linux-powershell) los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9facc-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="9facc-247">Desde un explorador de Internet, abra hello Azure [portal](https://portal.azure.com) e inicie sesión con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="9facc-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="9facc-248">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="9facc-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="9facc-249">En parte superior de Hola de hello portal, toohello derecha hello *buscar recursos* barra, haga clic en hello **> _** icono toostart un shell de Bash en la nube (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="9facc-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="9facc-250">Hello panel de shell de Bash en la nube aparece en hello parte inferior del portal de Hola y después de unos segundos, se presenta un ** username@Azure:~ $** símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="9facc-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="9facc-251">Aunque puede SSH toohello máquina virtual desde su equipo, en lugar de shell en la nube de hello, instrucciones de hello en este tutorial en el que se supone que usa el shell de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="9facc-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="9facc-252">Hola parte superior de portal de hello, en el cuadro de Hola que contiene texto hello *buscar recursos*, tipo *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="9facc-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="9facc-253">Cuando **MyVm** aparece en los resultados de búsqueda de hello, haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="9facc-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="9facc-254">Hola **MyVm** hoja que aparece, haga clic en hello **conectar** botón en hello la esquina superior izquierda de la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="9facc-255">**Nota:** si **crear** está visible en hello **conectar** botón, Azure no ha terminado de crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="9facc-256">Haga clic en **conectar** sólo después de que ya no verá **crear** en hello **conectar** botón.</span><span class="sxs-lookup"><span data-stu-id="9facc-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="9facc-257">Azure abre un cuadro que indique hello tooenter `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="9facc-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="9facc-258">Escriba este comando en hello en la nube shell (o copia del cuadro de Hola que aparecían en el paso 4 y péguelo en el shell de nube toohello), a continuación, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="9facc-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="9facc-259">ENTRAR **Sí** toohello preguntando si desea conectar toocontinue, a continuación, presionar ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="9facc-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="9facc-260">Escriba la contraseña de Hola que especificó al crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="9facc-261">Una vez ha iniciado sesión correctamente en toohello de máquina virtual, verá un adminuser@MyVm:~ símbolo del sistema de $.</span><span class="sxs-lookup"><span data-stu-id="9facc-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="9facc-262">Ahora se registran en toohello máquina virtual a través de la sesión de shell de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="9facc-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="9facc-263">**Nota:** Las sesiones de Cloud Shell agotan el tiempo de espera tras 10 minutos de inactividad.</span><span class="sxs-lookup"><span data-stu-id="9facc-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="9facc-264">En este momento, las instrucciones de hello varían en función de distribución de Hola que usa.</span><span class="sxs-lookup"><span data-stu-id="9facc-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="9facc-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="9facc-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="9facc-266">En el símbolo del sistema de hello, escriba `uname -r` y confirme la versión de Hola para:</span><span class="sxs-lookup"><span data-stu-id="9facc-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="9facc-267">Ubuntu: "4.4.0-77-generic," o superior</span><span class="sxs-lookup"><span data-stu-id="9facc-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="9facc-268">SLES: "4.4.59-92.20-default" o superior</span><span class="sxs-lookup"><span data-stu-id="9facc-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="9facc-269">Crear un bono entre vNIC de red estándar de Hola y Hola accelerated red vNIC mediante la ejecución de los comandos de Hola que siguen.</span><span class="sxs-lookup"><span data-stu-id="9facc-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="9facc-270">Tráfico de red usa Hola con mayor rendimiento acelerado vNIC de red, mientras bond Hola garantiza que el tráfico de red no se interrumpe en determinados cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="9facc-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="9facc-271">Después de ejecutar script de Hola, Hola VM se reiniciará después de pausar un 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="9facc-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="9facc-272">Una vez Hola VM se reinicia, vuelva a conectar tooit completando los pasos 5 a 7 nuevo.</span><span class="sxs-lookup"><span data-stu-id="9facc-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="9facc-273">Ejecute hello `ifconfig` comando y confirme que sale bond0 e interfaz Hola se muestra como arriba.</span><span class="sxs-lookup"><span data-stu-id="9facc-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="9facc-274">Las aplicaciones que usan las redes acelerada deben comunicarse a través de hello *bond0* interfaz, no *eth0*.</span><span class="sxs-lookup"><span data-stu-id="9facc-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="9facc-275">nombre de la interfaz de Hello puede cambiar antes de que las redes acelerada alcance la disponibilidad general.</span><span class="sxs-lookup"><span data-stu-id="9facc-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="9facc-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="9facc-276">RHEL/CentOS</span></span>

<span data-ttu-id="9facc-277">Creación de una Red Hat Enterprise Linux o CentOS 7.3 VM requiere algunos adicional de los pasos necesarios para SR-IOV y controlador de función Virtual (VF) de tarjeta de red de Hola Hola controladores tooload hello más recientes.</span><span class="sxs-lookup"><span data-stu-id="9facc-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="9facc-278">Hola primera fase de instrucciones de hello prepara una imagen que puede ser utilizado toomake uno o más máquinas virtuales que tienen controladores de hello previamente cargados.</span><span class="sxs-lookup"><span data-stu-id="9facc-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="9facc-279">Fase uno: preparar una imagen base de Red Hat Enterprise Linux o CentOS 7.3.</span><span class="sxs-lookup"><span data-stu-id="9facc-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="9facc-280">Aprovisione una máquina virtual que no sea SRIOV CentOS 7.3 en Azure.</span><span class="sxs-lookup"><span data-stu-id="9facc-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="9facc-281">Instale LIS 4.2.2:</span><span class="sxs-lookup"><span data-stu-id="9facc-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="9facc-282">Descargue los archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="9facc-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="9facc-283">Desaprovisione esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9facc-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="9facc-284">Desde el portal de Azure, detener esta máquina virtual; y vaya "Discos" del tooVM, capturar el URI de VHD de hello OSDisk.</span><span class="sxs-lookup"><span data-stu-id="9facc-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="9facc-285">Este URI contiene el nombre de disco duro virtual de la imagen base de Hola y su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9facc-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="9facc-286">Fase 2: aprovisionar nuevas máquinas virtuales en Azure</span><span class="sxs-lookup"><span data-stu-id="9facc-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="9facc-287">Aprovisionar nuevas máquinas virtuales según con New-AzureRMVMConfig utilizando Hola base imagen VHD capturado en la primera fase, con AcceleratedNetworking habilitado en hello vNIC:</span><span class="sxs-lookup"><span data-stu-id="9facc-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="9facc-288">Después de arrancan las máquinas virtuales, comprobar el dispositivo de VF Hola por "lspci" y compruebe la entrada del Mellanox Hola.</span><span class="sxs-lookup"><span data-stu-id="9facc-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="9facc-289">Por ejemplo, debemos vemos este elemento en la salida de hello lspci:</span><span class="sxs-lookup"><span data-stu-id="9facc-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="9facc-290">Ejecutar script de unión de Hola por:</span><span class="sxs-lookup"><span data-stu-id="9facc-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="9facc-291">Reiniciar Hola nuevas máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="9facc-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="9facc-292">Hola VM debe comenzar con hello ruta acelerado de red habilitado y bond0 configurado.</span><span class="sxs-lookup"><span data-stu-id="9facc-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="9facc-293">Ejecutar `ifconfig` tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="9facc-293">Run `ifconfig` tooconfirm.</span></span>
