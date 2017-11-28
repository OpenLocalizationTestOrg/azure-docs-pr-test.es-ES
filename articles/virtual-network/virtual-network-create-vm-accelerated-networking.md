---
title: "Creación de una máquina virtual de Azure con Accelerated Networking | Microsoft Docs"
description: "Aprenda a crear una máquina virtual con Accelerated Networking."
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
ms.openlocfilehash: 449425189a3b42dcb2c31316c1c8e38fac69d761
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="22eeb-103">Creación de una máquina virtual con Accelerated Networking</span><span class="sxs-lookup"><span data-stu-id="22eeb-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="22eeb-104">En este tutorial, obtendrá información sobre cómo crear una máquina virtual de Azure con Accelerated Networking.</span><span class="sxs-lookup"><span data-stu-id="22eeb-104">In this tutorial, you learn how to create an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="22eeb-105">Las redes aceleradas están en disponibilidad general para Windows y en versión preliminar pública para distribuciones de Linux específicas.</span><span class="sxs-lookup"><span data-stu-id="22eeb-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="22eeb-106">Accelerated Networking habilita la virtualización de E/S de raíz única (SR-IOV) en una máquina virtual (VM), lo que mejora significativamente su rendimiento en la red.</span><span class="sxs-lookup"><span data-stu-id="22eeb-106">Accelerated networking enables single root I/O virtualization (SR-IOV) to a VM, greatly improving its networking performance.</span></span> <span data-ttu-id="22eeb-107">Esta ruta de alto rendimiento omite el host de la ruta de acceso de datos, lo que reduce la latencia, la inestabilidad y la utilización de la CPU para su uso con las cargas de trabajo de red más exigentes en tipos de máquina virtual compatibles.</span><span class="sxs-lookup"><span data-stu-id="22eeb-107">This high-performance path bypasses the host from the datapath reducing latency, jitter, and CPU utilization, for use with the most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="22eeb-108">En la siguiente imagen, se muestra la comunicación entre dos máquinas virtuales (VM) con y sin Accelerated Networking:</span><span class="sxs-lookup"><span data-stu-id="22eeb-108">The following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![De comparación](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="22eeb-110">Sin Accelerated Networking, todo el tráfico de red de entrada y salida de la máquina virtual tiene que atravesar el host y el conmutador virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-110">Without accelerated networking, all networking traffic in and out of the VM must traverse the host and the virtual switch.</span></span> <span data-ttu-id="22eeb-111">El conmutador virtual se encarga de toda la aplicación de directivas, como grupos de seguridad de red, listas de control de acceso, aislamiento y otros servicios virtualizados de red, al tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="22eeb-111">The virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services to network traffic.</span></span> <span data-ttu-id="22eeb-112">Para más información sobre los conmutadores virtuales, lea el artículo sobre [virtualización de red y conmutador virtual de Hyper-V](https://technet.microsoft.com/library/jj945275.aspx).</span><span class="sxs-lookup"><span data-stu-id="22eeb-112">To learn more about virtual switches, read the [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="22eeb-113">Con Accelerated Networking, el tráfico de red llega a la interfaz de red (NIC) de la máquina virtual y se reenvía después a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-113">With accelerated networking, network traffic arrives at the VM's network interface (NIC), and is then forwarded to the VM.</span></span> <span data-ttu-id="22eeb-114">Todas las directivas de red que el conmutador virtual aplica sin Accelerated Networking se descargan y aplican en el hardware.</span><span class="sxs-lookup"><span data-stu-id="22eeb-114">All network policies that the virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="22eeb-115">La aplicación de directivas en hardware permite que la NIC reenvíe el tráfico de red directamente a la máquina virtual, pasando por alto el host y el conmutador virtual, al mismo tiempo que se mantienen todas las directivas aplicadas en el host.</span><span class="sxs-lookup"><span data-stu-id="22eeb-115">Applying policy in hardware enables the NIC to forward network traffic directly to the VM, bypassing the host and the virtual switch, while maintaining all the policy it applied in the host.</span></span>

<span data-ttu-id="22eeb-116">Las ventajas de Accelerated Networking solo se aplican a la máquina virtual donde esté habilitado.</span><span class="sxs-lookup"><span data-stu-id="22eeb-116">The benefits of accelerated networking only apply to the VM that it is enabled on.</span></span> <span data-ttu-id="22eeb-117">Para obtener resultados óptimos, lo ideal es habilitar esta característica en al menos dos máquinas virtuales conectadas a la misma instancia de Azure Virtual Network (VNet).</span><span class="sxs-lookup"><span data-stu-id="22eeb-117">For the best results, it is ideal to enable this feature on at least two VMs connected to the same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="22eeb-118">Al comunicarse entre redes virtuales o conectarse de forma local, esta característica tiene un efecto mínimo sobre la latencia total.</span><span class="sxs-lookup"><span data-stu-id="22eeb-118">When communicating across VNets or connecting on-premises, this feature has minimal impact to overall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="22eeb-119">Esta versión preliminar pública de Linux podría no tener el mismo nivel de disponibilidad y confiabilidad que las características que se encuentran en las versiones de disponibilidad general.</span><span class="sxs-lookup"><span data-stu-id="22eeb-119">This Linux Public Preview may not have the same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="22eeb-120">Esta característica no se admite, puede tener funcionalidades limitadas y no estar disponible en todas las ubicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="22eeb-120">The feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="22eeb-121">Para ver las notificaciones más actuales sobre la disponibilidad y el estado de esta característica, consulte la página de actualizaciones de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="22eeb-121">For the most up-to-date notifications on availability and status of this feature, check the Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="22eeb-122">Ventajas</span><span class="sxs-lookup"><span data-stu-id="22eeb-122">Benefits</span></span>
* <span data-ttu-id="22eeb-123">**Menor latencia/Más paquetes por segundo (pps):** al quitarse el conmutador virtual de la ruta de acceso de datos, se elimina el tiempo que los paquetes pasan en el host para el procesamiento de las directivas y se aumenta el número de paquetes que se pueden procesar dentro de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-123">**Lower Latency / Higher packets per second (pps):** Removing the virtual switch from the datapath removes the time packets spend in the host for policy processing and increases the number of packets that can be processed inside the VM.</span></span>
* <span data-ttu-id="22eeb-124">**Inestabilidad reducida:** el procesamiento del conmutador virtual depende de la cantidad de directivas que deben aplicarse y la carga de trabajo de la CPU que se encarga del procesamiento.</span><span class="sxs-lookup"><span data-stu-id="22eeb-124">**Reduced jitter:** Virtual switch processing depends on the amount of policy that needs to be applied and the workload of the CPU that is doing the processing.</span></span> <span data-ttu-id="22eeb-125">Al descargarse la aplicación de directivas en el hardware, se elimina esa variabilidad, ya que los paquetes se entregan directamente a la máquina virtual y se elimina el host de la comunicación de la máquina virtual, así como todas las interrupciones de software y los cambios de contexto.</span><span class="sxs-lookup"><span data-stu-id="22eeb-125">Offloading the policy enforcement to the hardware removes that variability by delivering packets directly to the VM, removing the host to VM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="22eeb-126">**Disminución de la utilización de la CPU:** el pasar por alto el conmutador virtual en el host conlleva una disminución de la utilización de la CPU para procesar el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="22eeb-126">**Decreased CPU utilization:** Bypassing the virtual switch in the host leads to less CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="22eeb-127"><a name="Limitations"></a>Limitaciones</span><span class="sxs-lookup"><span data-stu-id="22eeb-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="22eeb-128">Cuando se utiliza esta funcionalidad, existen las siguientes limitaciones:</span><span class="sxs-lookup"><span data-stu-id="22eeb-128">The following limitations exist when using this capability:</span></span>

* <span data-ttu-id="22eeb-129">**Creación de interfaz de red:** Accelerated Networking solo se puede habilitar para una nueva interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="22eeb-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="22eeb-130">No se puede habilitar para una NIC existente.</span><span class="sxs-lookup"><span data-stu-id="22eeb-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="22eeb-131">**Creación de máquina virtual:** una NIC con Accelerated Networking habilitado solo se puede asociar a una máquina virtual cuando esta se crea.</span><span class="sxs-lookup"><span data-stu-id="22eeb-131">**VM creation:** A NIC with accelerated networking enabled can only be attached to a VM when the VM is created.</span></span> <span data-ttu-id="22eeb-132">La NIC no puede asociarse a una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="22eeb-132">The NIC cannot be attached to an existing VM.</span></span>
* <span data-ttu-id="22eeb-133">**Regiones:** la mayoría de las regiones de Azure ofrecen máquinas virtuales de Windows con Accelerated Networking.</span><span class="sxs-lookup"><span data-stu-id="22eeb-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="22eeb-134">En numerosas regiones se ofrecen máquinas virtuales de Linux con redes aceleradas.</span><span class="sxs-lookup"><span data-stu-id="22eeb-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="22eeb-135">El número de regiones en las que esta funcionalidad está disponible va en aumento.</span><span class="sxs-lookup"><span data-stu-id="22eeb-135">The regions this capability is available in is expanding.</span></span> <span data-ttu-id="22eeb-136">Consulte más abajo el blog de actualizaciones de redes virtuales de Azure para ver la información más reciente.</span><span class="sxs-lookup"><span data-stu-id="22eeb-136">Please see the Azure Virtual Networking Updates blog below for the latest information.</span></span>   
* <span data-ttu-id="22eeb-137">**Sistemas operativos compatibles:** para Windows, Microsoft Windows Server 2012 R2 Datacenter y Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="22eeb-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="22eeb-138">Para Linux, Ubuntu Server 16.04 LTS con kernel 4.4.0-77 o superior, SLES 12 SP2, RHEL 7.3 y CentOS 7.3 (publicado por Rogue Wave Software).</span><span class="sxs-lookup"><span data-stu-id="22eeb-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="22eeb-139">**Tamaño de máquina virtual:** instancias de uso general y de proceso optimizado con ocho o más núcleos.</span><span class="sxs-lookup"><span data-stu-id="22eeb-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="22eeb-140">Para más información, consulte los artículos sobre los tamaños de máquina virtual de [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) y de [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22eeb-140">For more information, see the [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="22eeb-141">El conjunto de tamaños de instancia de máquina virtual compatibles se ampliará en el futuro.</span><span class="sxs-lookup"><span data-stu-id="22eeb-141">The set of supported VM instance sizes will expand in the future.</span></span>
* <span data-ttu-id="22eeb-142">**Implementación mediante Azure Resource Manager (ARM):** la funcionalidad de redes aceleradas no se puede implementar mediante ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="22eeb-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="22eeb-143">Los cambios en estas limitaciones se anunciarán a través de la página de [actualizaciones para Azure Virtual Networking](https://azure.microsoft.com/updates/accelerated-networking-in-preview).</span><span class="sxs-lookup"><span data-stu-id="22eeb-143">Changes to these limitations are announced through the [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="22eeb-144">Creación de una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="22eeb-144">Create a Windows VM</span></span>
<span data-ttu-id="22eeb-145">Puede usar Azure Portal o Azure [PowerShell](#windows-powershell) para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-145">You can use the Azure portal or Azure [PowerShell](#windows-powershell) to create the VM.</span></span>

### <span data-ttu-id="22eeb-146"><a name="windows-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="22eeb-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="22eeb-147">Desde un explorador de Internet, abra[Azure Portal](https://portal.azure.com) e inicie sesión con su [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) de Azure.</span><span class="sxs-lookup"><span data-stu-id="22eeb-147">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="22eeb-148">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="22eeb-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="22eeb-149">En el portal, haga clic en **Nuevo** > **Compute** > **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-149">In the portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="22eeb-150">En la hoja **Windows Server 2016 Datacenter**, deje seleccionado *Resource Manager* en **Seleccionar un modelo de implementación** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-150">In the **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="22eeb-151">En la hoja **Datos básicos** que aparece, escriba los valores a continuación, deje las opciones restantes con las opciones predeterminadas o seleccione o escriba sus propios valores y haga clic en el botón **Aceptar**:</span><span class="sxs-lookup"><span data-stu-id="22eeb-151">In the **Basics** blade that appears, enter the following values, leave the remaining default options or select or enter your own values, and click the **OK** button:</span></span>

    |<span data-ttu-id="22eeb-152">Configuración</span><span class="sxs-lookup"><span data-stu-id="22eeb-152">Setting</span></span>|<span data-ttu-id="22eeb-153">Valor</span><span class="sxs-lookup"><span data-stu-id="22eeb-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="22eeb-154">Nombre</span><span class="sxs-lookup"><span data-stu-id="22eeb-154">Name</span></span>|<span data-ttu-id="22eeb-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="22eeb-155">MyVm</span></span>|
    |<span data-ttu-id="22eeb-156">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="22eeb-156">Resource group</span></span>|<span data-ttu-id="22eeb-157">Deje seleccionado **Crear nuevo** y escriba *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="22eeb-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="22eeb-158">Ubicación</span><span class="sxs-lookup"><span data-stu-id="22eeb-158">Location</span></span>|<span data-ttu-id="22eeb-159">Oeste de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="22eeb-159">West US 2</span></span>|

    <span data-ttu-id="22eeb-160">Si no está familiarizado con Azure, consulte más información sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [suscripciones](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) y [ubicaciones](https://azure.microsoft.com/regions) (también denominadas regiones).</span><span class="sxs-lookup"><span data-stu-id="22eeb-160">If you're new to Azure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred to as regions).</span></span>
5. <span data-ttu-id="22eeb-161">En la hoja **Elegir un tamaño** que aparece, escriba *8* en el cuadro **Minimum cores** (cantidad mínima de núcleos), a continuación, haga clic en **Ver todos**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-161">In the **Choose a size** blade that appears, enter *8* in the **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="22eeb-162">Haga clic en **DS4_V2 Standard** o en cualquier máquina virtual compatible y, después, en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-162">Click **DS4_V2 Standard**, or any supported VM, then click the **Select** button.</span></span>
7. <span data-ttu-id="22eeb-163">En el hoja **Configuración** que aparece, deje todos los valores como están excepto **Habilitado**, haga clic en esta opción en **Accelerated Networking**, a continuación, haga clic en el botón **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-163">In the **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click the **OK** button.</span></span> <span data-ttu-id="22eeb-164">**Nota:** Si en los pasos anteriores, seleccionó valores de tamaño de máquina virtual, sistema operativo o ubicación que no aparecen en la sección [Limitaciones](#Limitations) de este artículo, **Accelerated Networking** no estará visible.</span><span class="sxs-lookup"><span data-stu-id="22eeb-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in the [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="22eeb-165">En la hoja **Resumen** que aparece, haga clic en el botón **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-165">In the **Summary** blade that appears, click the **OK** button.</span></span> <span data-ttu-id="22eeb-166">Azure comienza a crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-166">Azure starts creating the VM.</span></span> <span data-ttu-id="22eeb-167">La creación tarda unos minutos.</span><span class="sxs-lookup"><span data-stu-id="22eeb-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="22eeb-168">Para instalar el controlador de Accelerated Networking para Windows, complete los pasos descritos en la sección [Configuración de Windows](#configure-windows) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-168">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="22eeb-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="22eeb-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="22eeb-170">Instale la versión más reciente del módulo [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22eeb-170">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="22eeb-171">Si no está familiarizado con Azure PowerShell, consulte el artículo [Introducción a Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22eeb-171">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="22eeb-172">Inicie una sesión de PowerShell haciendo clic en el botón Inicio de Windows, luego escriba **Powershell** y, a continuación, en los resultados de búsqueda, haga clic en **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-172">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="22eeb-173">En la ventana de PowerShell, escriba el comando `login-azurermaccount` para iniciar sesión con su [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) de Azure.</span><span class="sxs-lookup"><span data-stu-id="22eeb-173">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="22eeb-174">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="22eeb-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="22eeb-175">En su explorador, copie el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="22eeb-175">In your browser, copy the following script:</span></span>
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

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
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

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="22eeb-176">En la ventana de PowerShell, haga clic con el botón derecho para pegar el script y empezar a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-176">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="22eeb-177">Se le pide un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="22eeb-177">You are prompted for a username and password.</span></span> <span data-ttu-id="22eeb-178">Use estas credenciales para iniciar sesión en la máquina virtual cuando se conecte a ella en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="22eeb-178">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="22eeb-179">Si ha cambiado valores en el script antes de ejecutarlo y se produce un error en el script, confirme que los valores que utilizó para el tamaño, sistema operativo, y ubicación de la máquina virtual se muestran en la sección [Limitaciones](#Limitations) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-179">If the script fails, and you changed values in the script before executing it, confirm the values you used for VM size, operating system, and location are listed in the [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="22eeb-180">Para instalar el controlador de Accelerated Networking para Windows, complete los pasos descritos en la sección [Configuración de Windows](#configure-windows) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-180">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="22eeb-181"><a name="configure-windows"></a>Configuración de Windows</span><span class="sxs-lookup"><span data-stu-id="22eeb-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="22eeb-182">Una vez creada la máquina virtual en Azure, tiene que instalar al controlador de Accelerated Networking para Windows.</span><span class="sxs-lookup"><span data-stu-id="22eeb-182">Once you create the VM in Azure, you must install the accelerated networking driver for Windows.</span></span> <span data-ttu-id="22eeb-183">Antes de completar los pasos a continuación, tiene que haber creado una máquina virtual Windows con Accelerated Networking mediante los pasos indicados para el [Portal](#windows-portal) o para [PowerShell](#windows-powershell) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-183">Before completing the following steps, you must have created a Windows VM with accelerated networking using either the [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="22eeb-184">Desde un explorador de Internet, abra[Azure Portal](https://portal.azure.com) e inicie sesión con su [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) de Azure.</span><span class="sxs-lookup"><span data-stu-id="22eeb-184">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="22eeb-185">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="22eeb-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="22eeb-186">En el cuadro que contiene el texto *Buscar recursos*, en la parte superior de Azure Portal, escriba *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="22eeb-186">In the box that contains the text *Search resources* at the top of the Azure portal, type *MyVm*.</span></span> <span data-ttu-id="22eeb-187">Haga clic en **MyVm** cuando aparezca en los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="22eeb-187">When **MyVm** appears in the search results, click it.</span></span>
3. <span data-ttu-id="22eeb-188">En la hoja **MyVm** que aparece, haga clic en el botón **Conectar** en la esquina superior izquierda de la hoja.</span><span class="sxs-lookup"><span data-stu-id="22eeb-188">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="22eeb-189">**Nota:** Si **Creando** está visible en el botón **Conectar**, Azure no ha terminado de crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-189">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="22eeb-190">Haga clic en **Conectar** solo después de que ya no se vea **Creando** en el botón **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-190">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
4. <span data-ttu-id="22eeb-191">Permita que el explorador descargue el archivo **MyVm.rdp**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-191">Allow your browser to download the **MyVm.rdp** file.</span></span>  <span data-ttu-id="22eeb-192">Una vez descargado, haga clic en el archivo para abrirlo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-192">Once downloaded, click the file to open it.</span></span> 
5. <span data-ttu-id="22eeb-193">Haga clic en el botón **Conectar** en el cuadro **Conexión a Escritorio remoto** que aparece notificándole que el publicador de esta conexión remota no se puede identificar.</span><span class="sxs-lookup"><span data-stu-id="22eeb-193">Click the **Connect** button in the **Remote Desktop Connection** box that appears, notifying you that the publisher of the remote connection can't be identified.</span></span>
6. <span data-ttu-id="22eeb-194">En el cuadro **Seguridad de Windows** que aparece, haga clic en **Más opciones**, a continuación, haga clic en **Usar otra cuenta**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-194">In the **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="22eeb-195">Escriba el nombre de usuario y la contraseña que escribió en el paso 4, a continuación, haga clic en el botón **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-195">Enter the username and password you entered in step 4, then click the **OK** button.</span></span>
7. <span data-ttu-id="22eeb-196">Haga clic en el botón **Sí** en el cuadro Conexión a Escritorio remoto que le informa de que no se puede comprobar la identidad del equipo remoto.</span><span class="sxs-lookup"><span data-stu-id="22eeb-196">Click the **Yes** button in the Remote Desktop Connection box that appears, notifying you that the identity of the remote computer cannot be verified.</span></span>
8. <span data-ttu-id="22eeb-197">Haga clic con el botón derecho en el botón Inicio de Windows y haga clic en **Administrador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-197">Right-click the Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="22eeb-198">Expanda el nodo **Adaptadores de red**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-198">Expand the **Network adapters** node.</span></span> <span data-ttu-id="22eeb-199">Compruebe que el **Adaptador Ethernet de función virtual ConnectX-3 de Mellanox** aparezca como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="22eeb-199">Confirm that the **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in the following picture:</span></span>
   
    ![Administrador de dispositivos](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="22eeb-201">Las redes aceleradas ya están habilitadas para su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="22eeb-202">Creación de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="22eeb-202">Create a Linux VM</span></span>
<span data-ttu-id="22eeb-203">Puede usar Azure Portal o Azure [PowerShell](#linux-powershell) para crear una máquina virtual Ubuntu o SLES.</span><span class="sxs-lookup"><span data-stu-id="22eeb-203">You can use the Azure portal or Azure [PowerShell](#linux-powershell) to create an Ubuntu or SLES VM.</span></span> <span data-ttu-id="22eeb-204">En el caso de las máquinas virtuales RHEL y CentOS, el flujo de trabajo es diferente.</span><span class="sxs-lookup"><span data-stu-id="22eeb-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="22eeb-205">Vea las instrucciones que se describen a continuación.</span><span class="sxs-lookup"><span data-stu-id="22eeb-205">Please see the instructions below.</span></span>

### <span data-ttu-id="22eeb-206"><a name="linux-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="22eeb-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="22eeb-207">Regístrese para Accelerated Networking para la versión preliminar de Linux siguiendo los pasos del 1 al 5 de la sección [Creación de una máquina virtual Linux: PowerShell](#linux-powershell) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-207">Register for the accelerated networking for Linux preview by completing steps 1-5 of the [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="22eeb-208">No se puede registrar para versión preliminar en el portal.</span><span class="sxs-lookup"><span data-stu-id="22eeb-208">You cannot register for the preview in the portal.</span></span>
2. <span data-ttu-id="22eeb-209">Complete los pasos del 1 al 8 en la sección [Creación de una máquina virtual Windows: Portal](#windows-portal) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-209">Complete steps 1-8 in the [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="22eeb-210">En el paso 2, haga clic en **Ubuntu Server 16.04 LTS** en lugar de **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="22eeb-211">Para este tutorial, elija utilizar una contraseña en lugar de una clave SSH, aunque para las implementaciones de producción, puede usar cualquiera de las dos opciones.</span><span class="sxs-lookup"><span data-stu-id="22eeb-211">For this tutorial, choose to use a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="22eeb-212">Si **Accelerated Networking** no aparece cuando se completa el paso 7 de la sección [Creación de una máquina virtual Windows: Portal](#windows-portal) de este artículo, es probable que sea por uno de los siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="22eeb-212">If **Accelerated networking** does not appear when you complete step 7 of the [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of the following reasons:</span></span>
    - <span data-ttu-id="22eeb-213">No se ha registrado para la versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="22eeb-213">You are not yet registered for the preview.</span></span> <span data-ttu-id="22eeb-214">Confirme que su estado de registro es **Registrado**, tal como se describe en el paso 4 de la sección [Creación de una máquina virtual Linux: PowerShell](#linux-powershell) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-214">Confirm that your registration state is **Registered**, as explained in step 4 of the [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="22eeb-215">**Nota:** Si participó en la versión preliminar de Accelerated Networking para máquinas virtuales de Windows (ya no es necesario registrarse para usar Accelerated Networking para máquinas virtuales de Windows), no se registrará automáticamente para la versión preliminar de Accelerated Networking para máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="22eeb-215">**Note:** If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="22eeb-216">Para poder participar en la versión preliminar de Accelerated Networking para máquinas virtuales de Linux, tiene que registrarse.</span><span class="sxs-lookup"><span data-stu-id="22eeb-216">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
    - <span data-ttu-id="22eeb-217">No ha seleccionado el tamaño de máquina virtual, el sistema operativo o la ubicación que se enumeran en la sección [Limitaciones](#limitations) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-217">You have not selected a VM size, operating system, or location listed in the [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="22eeb-218">Para instalar el controlador de Accelerated Networking para Linux, complete los pasos descritos en la sección [Configuración de Linux](#configure-linux) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-218">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="22eeb-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="22eeb-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="22eeb-220">Si crea máquinas virtuales de Linux con Accelerated Networking en una suscripción y después intenta crear una máquina virtual Windows con Accelerated Networking en la misma suscripción, se puede producir un error en la creación de la máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="22eeb-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt to create a Windows VM with accelerated networking in the same subscription, the Windows VM creation may fail.</span></span> <span data-ttu-id="22eeb-221">Durante esta versión preliminar, se recomienda probar las máquinas virtuales Windows y Linux con Accelerated Networking en suscripciones independientes.</span><span class="sxs-lookup"><span data-stu-id="22eeb-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="22eeb-222">Instale la versión más reciente del módulo [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22eeb-222">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="22eeb-223">Si no está familiarizado con Azure PowerShell, consulte el artículo [Introducción a Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22eeb-223">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="22eeb-224">Inicie una sesión de PowerShell haciendo clic en el botón Inicio de Windows, luego escriba **Powershell** y, a continuación, en los resultados de búsqueda, haga clic en **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-224">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="22eeb-225">En la ventana de PowerShell, escriba el comando `login-azurermaccount` para iniciar sesión con su [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) de Azure.</span><span class="sxs-lookup"><span data-stu-id="22eeb-225">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="22eeb-226">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="22eeb-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="22eeb-227">Regístrese para la versión preliminar de Accelerated Networking para Azure siguiendo los pasos a continuación:</span><span class="sxs-lookup"><span data-stu-id="22eeb-227">Register for the accelerated networking for Azure preview by completing the following steps:</span></span>
    - <span data-ttu-id="22eeb-228">Envíe un correo electrónico a [axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) con su identificador de suscripción de Azure y el uso previsto.</span><span class="sxs-lookup"><span data-stu-id="22eeb-228">Send an email to [axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="22eeb-229">Espere a recibir una confirmación por correo electrónico de Microsoft que le indique que la suscripción está habilitada.</span><span class="sxs-lookup"><span data-stu-id="22eeb-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="22eeb-230">Escriba el siguiente comando para confirmar que está registrado para la versión preliminar:</span><span class="sxs-lookup"><span data-stu-id="22eeb-230">Enter the following command to confirm you are registered for the preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="22eeb-231">No continúe con el paso 5 hasta que aparezca **Registrado** en la salida después de escribir el comando anterior.</span><span class="sxs-lookup"><span data-stu-id="22eeb-231">Do not continue with step 5 until **Registered** appears in the output after you enter the previous command.</span></span> <span data-ttu-id="22eeb-232">El resultado debe ser similar a la salida siguiente antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="22eeb-232">Your output must look like the following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="22eeb-233">Si participó en la versión preliminar de Accelerated Networking para máquinas virtuales de Windows (ya no es necesario registrarse para usar Accelerated Networking para máquinas virtuales de Windows), no se registrará automáticamente para la versión preliminar de Accelerated Networking para máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="22eeb-233">If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="22eeb-234">Para poder participar en la versión preliminar de Accelerated Networking para máquinas virtuales de Linux, tiene que registrarse.</span><span class="sxs-lookup"><span data-stu-id="22eeb-234">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
      >
5. <span data-ttu-id="22eeb-235">En el explorador, copie el script siguiente y sustituya Ubuntu o SLES según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="22eeb-235">In your browser, copy the following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="22eeb-236">Redhat y CentOS tienen un flujo de trabajo diferente, que se describe a continuación:</span><span class="sxs-lookup"><span data-stu-id="22eeb-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

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

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define the new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
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

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="22eeb-237">En la ventana de PowerShell, haga clic con el botón derecho para pegar el script y empezar a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-237">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="22eeb-238">Se le pide un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="22eeb-238">You are prompted for a username and password.</span></span> <span data-ttu-id="22eeb-239">Use estas credenciales para iniciar sesión en la máquina virtual cuando se conecte a ella en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="22eeb-239">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="22eeb-240">Si se produce un error en el script, confirme que:</span><span class="sxs-lookup"><span data-stu-id="22eeb-240">If the script fails, confirm that:</span></span>
    - <span data-ttu-id="22eeb-241">Se registró para la versión preliminar, tal como se describe en el paso 4</span><span class="sxs-lookup"><span data-stu-id="22eeb-241">You are registered for the preview, as explained in step 4</span></span>
    - <span data-ttu-id="22eeb-242">Si ha cambiado los valores de tamaño de máquina virtual, tipo de sistema operativo o ubicación en el script antes de ejecutarlo, confirme que los valores que ha utilizado se muestran en la sección [Limitaciones](#Limitations) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-242">If you changed VM size, operating system type, or location values in the script before executing it, that the values are listed in the [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="22eeb-243">Para instalar el controlador de Accelerated Networking para Linux, complete los pasos descritos en la sección [Configuración de Linux](#configure-linux) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-243">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="22eeb-244"><a name="configure-linux"></a>Configuración de Linux</span><span class="sxs-lookup"><span data-stu-id="22eeb-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="22eeb-245">Una vez creada la máquina virtual en Azure, tiene que instalar al controlador de Accelerated Networking para Linux.</span><span class="sxs-lookup"><span data-stu-id="22eeb-245">Once you create the VM in Azure, you must install the accelerated networking driver for Linux.</span></span> <span data-ttu-id="22eeb-246">Antes de completar los pasos a continuación, tiene que haber creado una máquina virtual Linux con Accelerated Networking mediante los pasos indicados para el [Portal](#linux-portal) o para [PowerShell](#linux-powershell) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-246">Before completing the following steps, you must have created a Linux VM with accelerated networking using either the [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="22eeb-247">Desde un explorador de Internet, abra[Azure Portal](https://portal.azure.com) e inicie sesión con su [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) de Azure.</span><span class="sxs-lookup"><span data-stu-id="22eeb-247">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="22eeb-248">Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="22eeb-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="22eeb-249">En la parte superior del portal, a la derecha de la barra *Buscar recursos*, haga clic en el icono **>_** para iniciar una instancia de Cloud Shell de Bash (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="22eeb-249">At the top of the portal, to the right of the *Search resources* bar, click the **>_** icon to start a Bash cloud shell (Preview).</span></span> <span data-ttu-id="22eeb-250">El panel de Cloud Shell de Bash aparece en la parte inferior del portal y, después de unos segundos, presenta el símbolo del sistema **username@Azure:~ $**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-250">The Bash cloud shell pane appears at the bottom of the portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="22eeb-251">Aunque puede conectarse mediante SSH a la máquina virtual desde su equipo, en lugar de mediante Cloud Shell, las instrucciones de este tutorial asumen que está usando Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="22eeb-251">Though you can SSH to the VM from your computer, rather than the cloud shell, the instructions in this tutorial assume you're using the cloud shell.</span></span>
3. <span data-ttu-id="22eeb-252">En la parte superior de Azure Portal, en el cuadro que contiene el texto *Buscar recursos*, escriba *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="22eeb-252">At the top of the portal, in the box that contains the text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="22eeb-253">Haga clic en **MyVm** cuando aparezca en los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="22eeb-253">When **MyVm** appears in the search results, click it.</span></span>
4. <span data-ttu-id="22eeb-254">En la hoja **MyVm** que aparece, haga clic en el botón **Conectar** en la esquina superior izquierda de la hoja.</span><span class="sxs-lookup"><span data-stu-id="22eeb-254">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="22eeb-255">**Nota:** Si **Creando** está visible en el botón **Conectar**, Azure no ha terminado de crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-255">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="22eeb-256">Haga clic en **Conectar** solo después de que ya no se vea **Creando** en el botón **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="22eeb-256">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
5. <span data-ttu-id="22eeb-257">Azure abre un cuadro que le pide que escriba la `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="22eeb-257">Azure opens a box telling you to enter the `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="22eeb-258">Escriba este comando en Cloud Shell (o cópielo en el cuadro que aparece en el paso 4 y péguelo en Cloud Shell) y luego presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="22eeb-258">Enter this command in the cloud shell (or copy it from the box that appeared in step 4 and paste it in to the cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="22eeb-259">Seleccione **Sí** como respuesta a la pregunta de si desea seguir conectado, luego presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="22eeb-259">Enter **yes** to the question asking you if you want to continue connecting, then press Enter.</span></span>
7. <span data-ttu-id="22eeb-260">Escriba la contraseña que especificó al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-260">Enter the password you entered when creating the VM.</span></span> <span data-ttu-id="22eeb-261">Una vez iniciada sesión correctamente en la máquina virtual, verá un símbolo del sistema adminuser@MyVm:~$.</span><span class="sxs-lookup"><span data-stu-id="22eeb-261">Once successfully logged in to the VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="22eeb-262">Ahora tiene iniciada sesión en la máquina virtual a través de la sesión de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="22eeb-262">You are now logged in to the VM through the cloud shell session.</span></span> <span data-ttu-id="22eeb-263">**Nota:** Las sesiones de Cloud Shell agotan el tiempo de espera tras 10 minutos de inactividad.</span><span class="sxs-lookup"><span data-stu-id="22eeb-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="22eeb-264">Llegados a este punto, las instrucciones difieren en función de la distribución que se use.</span><span class="sxs-lookup"><span data-stu-id="22eeb-264">At this point, the instructions vary based on the distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="22eeb-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="22eeb-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="22eeb-266">En el símbolo del sistema, escriba `uname -r` y confirme la versión para:</span><span class="sxs-lookup"><span data-stu-id="22eeb-266">At the prompt, enter `uname -r` and confirm the version for:</span></span>

    * <span data-ttu-id="22eeb-267">Ubuntu: "4.4.0-77-generic," o superior</span><span class="sxs-lookup"><span data-stu-id="22eeb-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="22eeb-268">SLES: "4.4.59-92.20-default" o superior</span><span class="sxs-lookup"><span data-stu-id="22eeb-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="22eeb-269">Cree un bond entre la vNIC de redes estándar y la vNIC de Accelerated Networking mediante la ejecución de los comandos que siguen.</span><span class="sxs-lookup"><span data-stu-id="22eeb-269">Create a bond between the standard networking vNIC and the accelerated networking vNIC by running the commands that follow.</span></span> <span data-ttu-id="22eeb-270">El tráfico de red utiliza la vNIC de Accelerated Networking que tiene mayor rendimiento, mientras el bond garantiza que el tráfico de redes no se interrumpe en determinados cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="22eeb-270">Network traffic uses the higher performing accelerated networking vNIC, while the bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="22eeb-271">Después de ejecutar el script, la máquina virtual se reiniciará al cabo de una pausa de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="22eeb-271">After running the script, the VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="22eeb-272">Una vez que se reinicia la máquina virtual, vuelva a conectarse a ello completando de nuevo los pasos del 5 al 7.</span><span class="sxs-lookup"><span data-stu-id="22eeb-272">Once the VM is restarted, reconnect to it by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="22eeb-273">Ejecute el comando `ifconfig` y confirme que sale bond0 y se muestra la interfaz como UP.</span><span class="sxs-lookup"><span data-stu-id="22eeb-273">Run the `ifconfig` command and confirm that bond0 has come up and the interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="22eeb-274">Las aplicaciones que usen redes aceleradas deben comunicarse a través de la interfaz *bond0*, no de la interfaz *eth0*.</span><span class="sxs-lookup"><span data-stu-id="22eeb-274">Applications using accelerated networking must communicate over the *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="22eeb-275">El nombre de la interfaz puede cambiar antes de que Accelerated Networking alcance la disponibilidad general.</span><span class="sxs-lookup"><span data-stu-id="22eeb-275">The interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="22eeb-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="22eeb-276">RHEL/CentOS</span></span>

<span data-ttu-id="22eeb-277">Para crear una máquina virtual de Red Hat Enterprise Linux o CentOS 7.3, debe seguir algunos pasos adicionales para cargar los controladores más recientes necesarios para SR-IOV y el controlador de función virtual (VF) de la tarjeta de red.</span><span class="sxs-lookup"><span data-stu-id="22eeb-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps to load the latest drivers needed for SR-IOV and the Virtual Function (VF) driver for the network card.</span></span> <span data-ttu-id="22eeb-278">En la primera fase de las instrucciones se prepara una imagen que puede usarse para crear una o varias máquinas virtuales que tengan los controladores precargados.</span><span class="sxs-lookup"><span data-stu-id="22eeb-278">The first phase of the instructions prepares an image that can be used to make one or more virtual machines that have the drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="22eeb-279">Fase uno: preparar una imagen base de Red Hat Enterprise Linux o CentOS 7.3.</span><span class="sxs-lookup"><span data-stu-id="22eeb-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="22eeb-280">Aprovisione una máquina virtual que no sea SRIOV CentOS 7.3 en Azure.</span><span class="sxs-lookup"><span data-stu-id="22eeb-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="22eeb-281">Instale LIS 4.2.2:</span><span class="sxs-lookup"><span data-stu-id="22eeb-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="22eeb-282">Descargue los archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="22eeb-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="22eeb-283">Desaprovisione esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22eeb-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="22eeb-284">Desde Azure Portal, detenga esta máquina virtual, vaya a "Discos" en la máquina virtual y capture el URI de VHD de OSDisk.</span><span class="sxs-lookup"><span data-stu-id="22eeb-284">From Azure portal, stop this VM; and go to VM’s "Disks", capture the OSDisk’s VHD URI.</span></span> <span data-ttu-id="22eeb-285">Este URI contiene el nombre de VHD de la imagen base y su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="22eeb-285">This URI contains the base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="22eeb-286">Fase 2: aprovisionar nuevas máquinas virtuales en Azure</span><span class="sxs-lookup"><span data-stu-id="22eeb-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="22eeb-287">Aprovisione nuevas máquinas virtuales con New-AzureRMVMConfig por medio del VHD de la imagen base capturado en la fase uno, con AcceleratedNetworking habilitado en la vNIC:</span><span class="sxs-lookup"><span data-stu-id="22eeb-287">Provision new VMs based with New-AzureRMVMConfig using the base image VHD captured in phase one, with AcceleratedNetworking enabled on the vNIC:</span></span>

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
    
    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify the base image's VHD URI (from phase one step 5). 
    # Note: The storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need to replace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for the location from which the new image binary large object (BLOB) is copied to start the virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
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
    
    # Create the virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="22eeb-288">Una vez que las máquinas virtuales hayan arrancado, compruebe el dispositivo de función virtual mediante el comando "lspci" y consulte la entrada Mellanox.</span><span class="sxs-lookup"><span data-stu-id="22eeb-288">After VMs boot up, check the VF device by "lspci" and check the Mellanox entry.</span></span> <span data-ttu-id="22eeb-289">Por ejemplo, debería ver este elemento en la salida de lspci:</span><span class="sxs-lookup"><span data-stu-id="22eeb-289">For example, we should see this item in the lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="22eeb-290">Ejecute el script de unión:</span><span class="sxs-lookup"><span data-stu-id="22eeb-290">Run the bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="22eeb-291">Reinicie las máquinas virtuales nuevas:</span><span class="sxs-lookup"><span data-stu-id="22eeb-291">Reboot the new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="22eeb-292">La máquina virtual debe arrancar con bond0 configurado y la ruta de acceso de las redes aceleradas habilitada.</span><span class="sxs-lookup"><span data-stu-id="22eeb-292">The VM should start with bond0 configured and the Accelerated Networking path enabled.</span></span>  <span data-ttu-id="22eeb-293">Ejecute `ifconfig` para confirmarlo.</span><span class="sxs-lookup"><span data-stu-id="22eeb-293">Run `ifconfig` to confirm.</span></span>
