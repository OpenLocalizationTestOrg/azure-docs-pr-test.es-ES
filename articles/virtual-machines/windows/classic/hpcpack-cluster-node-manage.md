---
title: "Administración de nodos de proceso del clúster de HPC Pack | Microsoft Docs"
description: "Obtenga información sobre las herramientas de script de PowerShell para agregar, quitar, iniciar y detener los nodos de proceso del clúster de HPC Pack 2012 R2 en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: dc9f354191b9e80ff6a01bd401a874c6998bda79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="64baf-103">Administrar el número y la disponibilidad de los nodos de ejecución en un clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="64baf-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="64baf-104">Si creó un clúster de HPC Pack 2012 R2 en las máquinas virtuales de Azure, puede que desee agregar, quitar, iniciar (aprovisionar) o detener (desaprovisionar) fácilmente algunas máquinas virtuales de nodo de ejecución en el clúster.</span><span class="sxs-lookup"><span data-stu-id="64baf-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="64baf-105">Para realizar estas tareas, ejecute los scripts de Azure PowerShell que están instalados en el nodo principal de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="64baf-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="64baf-106">Estos scripts le ayudan a controlar el número y la disponibilidad de los recursos de clúster de HPC Pack para que pueda controlar los costos.</span><span class="sxs-lookup"><span data-stu-id="64baf-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="64baf-107">La información de este artículo solo se aplica a los clústeres de HPC Pack 2012 R2 en Azure que se hayan creado con el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="64baf-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="64baf-108">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="64baf-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="64baf-109">Además, los scripts de PowerShell que se describen en este artículo no están disponibles en HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="64baf-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64baf-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="64baf-110">Prerequisites</span></span>
* <span data-ttu-id="64baf-111">**Clúster de HPC Pack 2012 R2 en máquinas virtuales de Azure**: cree un clúster de HPC Pack 2012 R2 en el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="64baf-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="64baf-112">Por ejemplo, puede automatizar la implementación mediante la imagen de la máquina virtual de HPC Pack 2012 R2 en Azure Marketplace y un script de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64baf-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="64baf-113">Para más información y ver los requisitos previos, consulte [Creación de un clúster de HPC con el script de implementación de HPC Pack IaaS](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="64baf-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="64baf-114">Después de la implementación, busque los scripts de administración de nodo en la carpeta % CCP\_HOME %bin en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="64baf-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="64baf-115">Ejecute cada uno de estos scripts como administrador.</span><span class="sxs-lookup"><span data-stu-id="64baf-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="64baf-116">**Archivo de configuración de publicación o certificado de administración de Azure**: debe llevar a cabo una de las siguientes acciones en el nodo principal:</span><span class="sxs-lookup"><span data-stu-id="64baf-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="64baf-117">**Importar el archivo de configuración de publicación de Azure**.</span><span class="sxs-lookup"><span data-stu-id="64baf-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="64baf-118">Para ello, ejecute los siguientes cmdlets de Azure PowerShell en el nodo principal:</span><span class="sxs-lookup"><span data-stu-id="64baf-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="64baf-119">**Configure el certificado de administración de Azure en el nodo principal**.</span><span class="sxs-lookup"><span data-stu-id="64baf-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="64baf-120">Si tiene el archivo .cer, impórtelo en el almacén CurrentUser\My certificate y luego ejecute el siguiente cmdlet de Azure PowerShell para su entorno de Azure (AzureCloud o AzureChinaCloud):</span><span class="sxs-lookup"><span data-stu-id="64baf-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="64baf-121">Agregar máquinas virtuales de nodo de ejecución</span><span class="sxs-lookup"><span data-stu-id="64baf-121">Add compute node VMs</span></span>
<span data-ttu-id="64baf-122">Agregue nodos de ejecución con el script **Add-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="64baf-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="64baf-123">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="64baf-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="64baf-124">parameters</span><span class="sxs-lookup"><span data-stu-id="64baf-124">Parameters</span></span>
* <span data-ttu-id="64baf-125">**ServiceName**: nombre del servicio en la nube al que se agregan las nuevas máquinas virtuales de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="64baf-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="64baf-126">**ImageName**: nombre de la imagen de máquina virtual de Azure, que puede obtenerse mediante el Portal de Azure clásico o el cmdlet de Azure PowerShell **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="64baf-126">**ImageName**: Azure VM image name, which can be obtained through the Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="64baf-127">La imagen debe cumplir los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="64baf-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="64baf-128">Debe haber instalado un sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="64baf-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="64baf-129">HPC Pack debe estar instalado en el rol del nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="64baf-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="64baf-130">La imagen debe ser una imagen privada en la categoría de usuario, no una imagen de máquina virtual de Azure pública.</span><span class="sxs-lookup"><span data-stu-id="64baf-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="64baf-131">**Quantity**: número de máquinas virtuales de nodo de ejecución que se van a agregar.</span><span class="sxs-lookup"><span data-stu-id="64baf-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="64baf-132">**InstanceSize**: tamaño de las máquinas virtuales de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="64baf-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="64baf-133">**DomainUserName**: nombre de usuario de dominio, que se usa para unir las nuevas máquinas virtuales al dominio.</span><span class="sxs-lookup"><span data-stu-id="64baf-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="64baf-134">**DomainUserPassword**: contraseña del usuario de dominio.</span><span class="sxs-lookup"><span data-stu-id="64baf-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="64baf-135">**NodeNameSeries** (opcional): modelo de nomenclatura para los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="64baf-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="64baf-136">El formato debe ser &lt;*Raíz\_Nombre*&gt;&lt;*Inicio\_Número*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="64baf-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="64baf-137">Por ejemplo, MyCN%10% se refiere a una serie de nombres de nodos de ejecución a partir de MyCN11.</span><span class="sxs-lookup"><span data-stu-id="64baf-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="64baf-138">Si no se especifica, el script usa la serie de nomenclatura de nodos configurados clúster de HPC.</span><span class="sxs-lookup"><span data-stu-id="64baf-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="64baf-139">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="64baf-139">Example</span></span>
<span data-ttu-id="64baf-140">En el ejemplo siguiente se agregan 20 máquinas virtuales grandes de nodos de proceso de gran tamaño en el servicio en la nube *hpcservice1*, según la imagen de máquina virtual *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="64baf-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="64baf-141">Quitar máquinas virtuales de nodo de ejecución</span><span class="sxs-lookup"><span data-stu-id="64baf-141">Remove compute node VMs</span></span>
<span data-ttu-id="64baf-142">Quite nodos de ejecución con el script **Remove-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="64baf-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="64baf-143">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="64baf-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="64baf-144">parameters</span><span class="sxs-lookup"><span data-stu-id="64baf-144">Parameters</span></span>
* <span data-ttu-id="64baf-145">**Name**: nombres de los nodos de clúster que se van a quitar.</span><span class="sxs-lookup"><span data-stu-id="64baf-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="64baf-146">Se admite caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="64baf-146">Wildcards are supported.</span></span> <span data-ttu-id="64baf-147">El nombre del conjunto de parámetros es Name.</span><span class="sxs-lookup"><span data-stu-id="64baf-147">The parameter set name is Name.</span></span> <span data-ttu-id="64baf-148">No se pueden especificar los dos parámetros, **Name** y **Node**.</span><span class="sxs-lookup"><span data-stu-id="64baf-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="64baf-149">**Node**: objeto HpcNode para los nodos que se van quitar, que se puede obtener a través del cmdlet de HPC PowerShell [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="64baf-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="64baf-150">El nombre del conjunto de parámetro es Node.</span><span class="sxs-lookup"><span data-stu-id="64baf-150">The parameter set name is Node.</span></span> <span data-ttu-id="64baf-151">No se pueden especificar los dos parámetros, **Name** y **Node**.</span><span class="sxs-lookup"><span data-stu-id="64baf-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="64baf-152">**DeleteVHD** (opcional): configuración para eliminar los discos asociados para las máquinas virtuales que se quitan.</span><span class="sxs-lookup"><span data-stu-id="64baf-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="64baf-153">**Force** (opcional): configuración para forzar nodos HPC sin conexión antes de quitarlos.</span><span class="sxs-lookup"><span data-stu-id="64baf-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="64baf-154">**Confirm** (opcional): solicitud de confirmación antes de ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="64baf-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="64baf-155">**WhatIf**: configuración para describir lo que sucedería si ejecutara el comando sin ejecutarlo realmente.</span><span class="sxs-lookup"><span data-stu-id="64baf-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="64baf-156">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="64baf-156">Example</span></span>
<span data-ttu-id="64baf-157">En el ejemplo siguiente se fuerzan los nodos sin conexión con nombres que comienzan por *HPCNode-CN-* y luego quita los nodos y sus discos asociados.</span><span class="sxs-lookup"><span data-stu-id="64baf-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="64baf-158">Iniciar máquinas virtuales de nodos de ejecución</span><span class="sxs-lookup"><span data-stu-id="64baf-158">Start compute node VMs</span></span>
<span data-ttu-id="64baf-159">Inicie nodos de ejecución con el script **Start-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="64baf-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="64baf-160">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="64baf-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="64baf-161">parameters</span><span class="sxs-lookup"><span data-stu-id="64baf-161">Parameters</span></span>
* <span data-ttu-id="64baf-162">**Name**: nombres de los nodos de clúster que se van a iniciar.</span><span class="sxs-lookup"><span data-stu-id="64baf-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="64baf-163">Se admite caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="64baf-163">Wildcards are supported.</span></span> <span data-ttu-id="64baf-164">El nombre del conjunto de parámetros es Name.</span><span class="sxs-lookup"><span data-stu-id="64baf-164">The parameter set name is Name.</span></span> <span data-ttu-id="64baf-165">No se pueden especificar los dos parámetros, **Name** y **Node**.</span><span class="sxs-lookup"><span data-stu-id="64baf-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="64baf-166">**Node**: objeto HpcNode para los nodos que se van a iniciar, que se puede obtener mediante el cmdlet de HPC PowerShell [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="64baf-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="64baf-167">El nombre del conjunto de parámetro es Node.</span><span class="sxs-lookup"><span data-stu-id="64baf-167">The parameter set name is Node.</span></span> <span data-ttu-id="64baf-168">No se pueden especificar los dos parámetros, **Name** y **Node**.</span><span class="sxs-lookup"><span data-stu-id="64baf-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="64baf-169">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="64baf-169">Example</span></span>
<span data-ttu-id="64baf-170">En el ejemplo siguiente se inician nodos con nombres que comienzan por *HPCNode-CN-*.</span><span class="sxs-lookup"><span data-stu-id="64baf-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="64baf-171">Detener máquinas virtuales de nodo de ejecución</span><span class="sxs-lookup"><span data-stu-id="64baf-171">Stop compute node VMs</span></span>
<span data-ttu-id="64baf-172">Detenga los nodos de proceso con el script **Stop-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="64baf-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="64baf-173">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="64baf-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="64baf-174">Parámetros</span><span class="sxs-lookup"><span data-stu-id="64baf-174">Parameters</span></span>
* <span data-ttu-id="64baf-175">**Name**: nombres de los nodos de clúster que se van a detener.</span><span class="sxs-lookup"><span data-stu-id="64baf-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="64baf-176">Se admite caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="64baf-176">Wildcards are supported.</span></span> <span data-ttu-id="64baf-177">El nombre del conjunto de parámetros es Name.</span><span class="sxs-lookup"><span data-stu-id="64baf-177">The parameter set name is Name.</span></span> <span data-ttu-id="64baf-178">No se pueden especificar los dos parámetros, **Name** y **Node**.</span><span class="sxs-lookup"><span data-stu-id="64baf-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="64baf-179">**Node**: objeto HpcNode para los nodos que se van a detener, que se puede obtener mediante el cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx)de HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64baf-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="64baf-180">El nombre del conjunto de parámetro es Node.</span><span class="sxs-lookup"><span data-stu-id="64baf-180">The parameter set name is Node.</span></span> <span data-ttu-id="64baf-181">No se pueden especificar los dos parámetros, **Name** y **Node**.</span><span class="sxs-lookup"><span data-stu-id="64baf-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="64baf-182">**Force** (opcional): configuración para forzar los nodos HPC sin conexión antes de detenerlos.</span><span class="sxs-lookup"><span data-stu-id="64baf-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="64baf-183">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="64baf-183">Example</span></span>
<span data-ttu-id="64baf-184">En el ejemplo siguiente se fuerzan nodos sin conexión con nombres que comienzan por *HPCNode-CN-* y luego se detienen los nodos.</span><span class="sxs-lookup"><span data-stu-id="64baf-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="64baf-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64baf-185">Next steps</span></span>
* <span data-ttu-id="64baf-186">Para aumentar o reducir automáticamente los nodos de clúster según la carga de trabajo actual de los trabajos y las tareas en el clúster, consulte [Aumento y reducción automáticos de los recursos de clúster de HPC Pack en Azure según la carga de trabajo de clúster](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="64baf-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

