---
title: "nodos de proceso de clúster de HPC Pack aaaManage | Documentos de Microsoft"
description: "Obtenga información acerca de tooadd de herramientas de script de PowerShell, quitar, iniciar y detener nodos de proceso de clúster de HPC Pack 2012 R2 en Azure"
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
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="d68cf-103">Administrar el número de Hola y la disponibilidad de nodos de proceso en un clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="d68cf-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="d68cf-104">Si ha creado un clúster de HPC Pack 2012 R2 en máquinas virtuales de Azure, conviene formas tooeasily agregar, quitar, iniciar (aprovisionar) o detenga (Cancelar aprovisionamiento) algunas máquinas virtuales de nodos del clúster de proceso.</span><span class="sxs-lookup"><span data-stu-id="d68cf-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="d68cf-105">toodo estas tareas, ejecutar scripts de PowerShell de Azure que están instalados en la máquina virtual del nodo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="d68cf-106">Estos scripts ayudan a controlar el número de Hola y la disponibilidad de los recursos de clúster de HPC Pack para poder controlar los costos.</span><span class="sxs-lookup"><span data-stu-id="d68cf-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d68cf-107">En este artículo se aplica solo tooHPC Pack 2012 R2 clústeres en Azure creados mediante el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="d68cf-108">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="d68cf-109">Además, los scripts de PowerShell de Hola se describe en este artículo no están disponibles en HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="d68cf-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d68cf-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d68cf-110">Prerequisites</span></span>
* <span data-ttu-id="d68cf-111">**Clúster de HPC Pack 2012 R2 en máquinas virtuales de Azure**: crear un clúster de HPC Pack 2012 R2 en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="d68cf-112">Por ejemplo, puede automatizar la implementación de hello mediante un script de PowerShell de Azure y de imagen de máquina virtual de HPC Pack 2012 R2 de hello en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d68cf-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="d68cf-113">Para obtener información y requisitos previos, consulte [crear un clúster de HPC con hello script de implementación de IaaS de HPC Pack](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="d68cf-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="d68cf-114">Después de la implementación, encontrar Hola scripts de administración de nodo en Hola % CCP\_carpeta principal % bin en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="d68cf-115">Ejecutar cada una de las secuencias de comandos de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="d68cf-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="d68cf-116">**Certificado de administración o el archivo de configuración de publicación de Azure**: necesita toodo uno de los siguientes hello en el nodo principal de hello:</span><span class="sxs-lookup"><span data-stu-id="d68cf-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="d68cf-117">**Archivo de configuración de publicación de hello importación Azure**.</span><span class="sxs-lookup"><span data-stu-id="d68cf-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="d68cf-118">toodo, ejecución Hola siguientes cmdlets de PowerShell de Azure en el nodo principal de hello:</span><span class="sxs-lookup"><span data-stu-id="d68cf-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="d68cf-119">**Configurar certificado de administración de Azure de hello en el nodo principal de hello**.</span><span class="sxs-lookup"><span data-stu-id="d68cf-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="d68cf-120">Si tiene el archivo .cer de hello, impórtelo en el almacén de certificados de hello CurrentUser\My y, a continuación, ejecute Hola siguiente cmdlet de PowerShell de Azure para el entorno de Azure (nube de Azure o AzureChinaCloud):</span><span class="sxs-lookup"><span data-stu-id="d68cf-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="d68cf-121">Agregar máquinas virtuales de nodo de ejecución</span><span class="sxs-lookup"><span data-stu-id="d68cf-121">Add compute node VMs</span></span>
<span data-ttu-id="d68cf-122">Agregar nodos de proceso con hello **Add-HpcIaaSNode.ps1** secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="d68cf-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="d68cf-123">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="d68cf-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="d68cf-124">parameters</span><span class="sxs-lookup"><span data-stu-id="d68cf-124">Parameters</span></span>
* <span data-ttu-id="d68cf-125">**ServiceName**: nombre del servicio de nube de Hola que calculan nuevas máquinas virtuales de nodos se agregan a.</span><span class="sxs-lookup"><span data-stu-id="d68cf-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="d68cf-126">**ImageName**: nombre de imagen de máquina virtual de Azure, que puede obtenerse a través del portal de Azure clásico de Hola o cmdlet de PowerShell de Azure **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="d68cf-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="d68cf-127">imagen de Hello debe cumplir Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="d68cf-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="d68cf-128">Debe haber instalado un sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="d68cf-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="d68cf-129">HPC Pack debe instalarse en función del nodo de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="d68cf-130">imagen de Hello debe ser una imagen privada en la categoría de usuario de hello, no es una imagen de máquina virtual de Azure pública.</span><span class="sxs-lookup"><span data-stu-id="d68cf-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="d68cf-131">**Cantidad**: número de toobe de las máquinas virtuales de nodo de proceso agregado.</span><span class="sxs-lookup"><span data-stu-id="d68cf-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="d68cf-132">**InstanceSize**: tamaño de hello máquinas virtuales de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="d68cf-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="d68cf-133">**Dominionombre_de_usuario**: nombre de usuario de dominio, que es usado toojoin Hola nuevas máquinas virtuales toohello dominio.</span><span class="sxs-lookup"><span data-stu-id="d68cf-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="d68cf-134">**DomainUserPassword**: contraseña de usuario de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="d68cf-135">**NodeNameSeries** (opcional): modelo de nomenclatura para hello nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="d68cf-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="d68cf-136">Hola formato debe ser &lt; *raíz\_nombre*&gt;&lt;*iniciar\_número*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="d68cf-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="d68cf-137">Por ejemplo, Mine % 10% significa una serie de hello calcula nombres de nodo a partir de MyCN11.</span><span class="sxs-lookup"><span data-stu-id="d68cf-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="d68cf-138">Si no se especifica, Hola script utiliza Hola configurado serie de nombres de nodo de clúster de HPC de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="d68cf-139">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="d68cf-139">Example</span></span>
<span data-ttu-id="d68cf-140">Hello en el ejemplo siguiente se agrega 20 máquinas virtuales de nodos de proceso gran tamaño en el servicio de nube de hello *hpcservice1*, en función de la imagen de máquina virtual de hello *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="d68cf-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="d68cf-141">Quitar máquinas virtuales de nodo de ejecución</span><span class="sxs-lookup"><span data-stu-id="d68cf-141">Remove compute node VMs</span></span>
<span data-ttu-id="d68cf-142">Quitar nodos de proceso con hello **Remove-HpcIaaSNode.ps1** secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="d68cf-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="d68cf-143">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="d68cf-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d68cf-144">parameters</span><span class="sxs-lookup"><span data-stu-id="d68cf-144">Parameters</span></span>
* <span data-ttu-id="d68cf-145">**Nombre**: quitan nombres de toobe de nodos de clúster.</span><span class="sxs-lookup"><span data-stu-id="d68cf-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="d68cf-146">Se admite caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="d68cf-146">Wildcards are supported.</span></span> <span data-ttu-id="d68cf-147">nombre de conjunto de parámetros de Hello es nombre.</span><span class="sxs-lookup"><span data-stu-id="d68cf-147">hello parameter set name is Name.</span></span> <span data-ttu-id="d68cf-148">No se pueden especificar ambos hello **nombre** y **nodo** parámetros.</span><span class="sxs-lookup"><span data-stu-id="d68cf-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="d68cf-149">**Nodo**: objeto HpcNode Hola para hello nodos toobe quitado, que puede obtenerse a través del cmdlet de PowerShell de HPC de hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="d68cf-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="d68cf-150">nombre de conjunto de parámetros de Hello es nodo.</span><span class="sxs-lookup"><span data-stu-id="d68cf-150">hello parameter set name is Node.</span></span> <span data-ttu-id="d68cf-151">No se pueden especificar ambos hello **nombre** y **nodo** parámetros.</span><span class="sxs-lookup"><span data-stu-id="d68cf-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="d68cf-152">**DeleteVHD** (opcional): configuración toodelete discos Hola asociado para hello las máquinas virtuales que se quitan.</span><span class="sxs-lookup"><span data-stu-id="d68cf-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="d68cf-153">**Force** (opcional): configuración tooforce los nodos HPC antes de eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="d68cf-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="d68cf-154">**Confirmar** (opcional): pedir confirmación antes de ejecutar el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="d68cf-155">**WhatIf**: configuración toodescribe lo que sucedería si ejecutara Hola comando sin realmente ejecutar comando Hola.</span><span class="sxs-lookup"><span data-stu-id="d68cf-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="d68cf-156">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="d68cf-156">Example</span></span>
<span data-ttu-id="d68cf-157">Hello en el ejemplo siguiente se fuerza nodos sin conexión hello cuyos nombres empiezan *HPCNode-CN -* y ellos elimina los nodos de Hola y sus discos asociados.</span><span class="sxs-lookup"><span data-stu-id="d68cf-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="d68cf-158">Iniciar máquinas virtuales de nodos de ejecución</span><span class="sxs-lookup"><span data-stu-id="d68cf-158">Start compute node VMs</span></span>
<span data-ttu-id="d68cf-159">Inicio de proceso nodos con hello **Start-HpcIaaSNode.ps1** secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="d68cf-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="d68cf-160">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="d68cf-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="d68cf-161">parameters</span><span class="sxs-lookup"><span data-stu-id="d68cf-161">Parameters</span></span>
* <span data-ttu-id="d68cf-162">**Nombre**: nombres de toobe de nodos de clúster de hello iniciado.</span><span class="sxs-lookup"><span data-stu-id="d68cf-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="d68cf-163">Se admite caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="d68cf-163">Wildcards are supported.</span></span> <span data-ttu-id="d68cf-164">nombre de conjunto de parámetros de Hello es nombre.</span><span class="sxs-lookup"><span data-stu-id="d68cf-164">hello parameter set name is Name.</span></span> <span data-ttu-id="d68cf-165">No se pueden especificar ambos hello **nombre** y **nodo** parámetros.</span><span class="sxs-lookup"><span data-stu-id="d68cf-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="d68cf-166">**Nodo**-objeto HpcNode Hola para hello nodos toobe iniciado, que puede obtenerse a través del cmdlet de PowerShell de HPC de hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="d68cf-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="d68cf-167">nombre de conjunto de parámetros de Hello es nodo.</span><span class="sxs-lookup"><span data-stu-id="d68cf-167">hello parameter set name is Node.</span></span> <span data-ttu-id="d68cf-168">No se pueden especificar ambos hello **nombre** y **nodo** parámetros.</span><span class="sxs-lookup"><span data-stu-id="d68cf-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="d68cf-169">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="d68cf-169">Example</span></span>
<span data-ttu-id="d68cf-170">Hello en el ejemplo siguiente se inicia nodos cuyos nombres empiezan *HPCNode-CN -*.</span><span class="sxs-lookup"><span data-stu-id="d68cf-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="d68cf-171">Detener máquinas virtuales de nodo de ejecución</span><span class="sxs-lookup"><span data-stu-id="d68cf-171">Stop compute node VMs</span></span>
<span data-ttu-id="d68cf-172">Detener nodos de proceso con hello **Stop-HpcIaaSNode.ps1** secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="d68cf-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="d68cf-173">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="d68cf-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d68cf-174">parameters</span><span class="sxs-lookup"><span data-stu-id="d68cf-174">Parameters</span></span>
* <span data-ttu-id="d68cf-175">**Nombre de**-nombres de toobe de nodos de clúster de hello detenido.</span><span class="sxs-lookup"><span data-stu-id="d68cf-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="d68cf-176">Se admite caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="d68cf-176">Wildcards are supported.</span></span> <span data-ttu-id="d68cf-177">nombre de conjunto de parámetros de Hello es nombre.</span><span class="sxs-lookup"><span data-stu-id="d68cf-177">hello parameter set name is Name.</span></span> <span data-ttu-id="d68cf-178">No se pueden especificar ambos hello **nombre** y **nodo** parámetros.</span><span class="sxs-lookup"><span data-stu-id="d68cf-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="d68cf-179">**Nodo**: objeto HpcNode Hola para hello nodos toobe detenido, que puede obtenerse a través del cmdlet de PowerShell de HPC de hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="d68cf-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="d68cf-180">nombre de conjunto de parámetros de Hello es nodo.</span><span class="sxs-lookup"><span data-stu-id="d68cf-180">hello parameter set name is Node.</span></span> <span data-ttu-id="d68cf-181">No se pueden especificar ambos hello **nombre** y **nodo** parámetros.</span><span class="sxs-lookup"><span data-stu-id="d68cf-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="d68cf-182">**Force** (opcional): configuración tooforce los nodos HPC antes de detenerlos.</span><span class="sxs-lookup"><span data-stu-id="d68cf-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="d68cf-183">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="d68cf-183">Example</span></span>
<span data-ttu-id="d68cf-184">Hello en el ejemplo siguiente se fuerza sin conexión nodos cuyos nombres empiezan *HPCNode-CN -* y, a continuación, se detiene Hola nodos.</span><span class="sxs-lookup"><span data-stu-id="d68cf-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="d68cf-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d68cf-185">Next steps</span></span>
* <span data-ttu-id="d68cf-186">tooautomatically aumentar o reducir los nodos del clúster Hola según la carga de trabajo actual de Hola de trabajos y tareas en clúster de hello, consulte [automáticamente aumentar y reducir los recursos de clúster de HPC Pack hello en Azure correspondiente toohello clúster cargas de trabajo](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="d68cf-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

