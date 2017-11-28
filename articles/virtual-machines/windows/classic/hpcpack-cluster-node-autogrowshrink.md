---
title: "Escalado automático de nodos de clúster de HPC | Microsoft Docs"
description: "Aumento y reducción automáticos del número de nodos de proceso del clúster de HPC Pack en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0dc0d15c64d8951c3c457df73588c37418a3c8a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-grow-and-shrink-the-hpc-pack-cluster-resources-in-azure-according-to-the-cluster-workload"></a><span data-ttu-id="998c7-103">Aumento y reducción automáticos de los recursos de clúster de HPC Pack en Azure según la carga de trabajo de clúster</span><span class="sxs-lookup"><span data-stu-id="998c7-103">Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload</span></span>
<span data-ttu-id="998c7-104">Si implementa nodos de "ráfaga" de Azure en su clúster de HPC Pack o crea un clúster de HPC Pack en máquinas virtuales de Azure, puede que quiera una manera de aumentar o reducir automáticamente recursos, como los nodos o los núcleos, según la carga de trabajo en el clúster.</span><span class="sxs-lookup"><span data-stu-id="998c7-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink the cluster resources such as nodes or cores according to the workload on the cluster.</span></span> <span data-ttu-id="998c7-105">El escalado de los recursos del clúster de este modo le permite usar de forma más eficaz los recursos de Azure y controlar los costos.</span><span class="sxs-lookup"><span data-stu-id="998c7-105">Scaling the cluster resources in this way allows you to use your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="998c7-106">Este artículo muestra dos maneras en que HPC Pack proporciona el escalado automático de recursos de proceso:</span><span class="sxs-lookup"><span data-stu-id="998c7-106">This article shows you two ways that HPC Pack provides to autoscale compute resources:</span></span>

* <span data-ttu-id="998c7-107">La propiedad **AutoGrowShrink** del clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="998c7-107">The HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="998c7-108">El script de PowerShell **AzureAutoGrowShrink.ps1** de HPC.</span><span class="sxs-lookup"><span data-stu-id="998c7-108">The **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="998c7-109">Actualmente solo se pueden aumentar y reducir automáticamente los nodos de proceso de HPC Pack que ejecutan un sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="998c7-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-the-autogrowshrink-cluster-property"></a><span data-ttu-id="998c7-110">Establecimiento de la propiedad de clúster AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="998c7-110">Set the AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="998c7-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="998c7-111">Prerequisites</span></span>

* <span data-ttu-id="998c7-112">**Clúster de HPC Pack 2012 R2 Update 2 o versiones posteriores** : el nodo principal del clúster se puede implementar de forma local o en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="998c7-112">**HPC Pack 2012 R2 Update 2 or later cluster** - The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="998c7-113">Vea [configurar un clúster híbrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) para comenzar con un nodo principal local y nodos de "ráfaga" de Azure.</span><span class="sxs-lookup"><span data-stu-id="998c7-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="998c7-114">Consulte el [script de implementación de HPC Pack IaaS](hpcpack-cluster-powershell-script.md) para implementar rápidamente un clúster de HPC Pack en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="998c7-114">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="998c7-115">**Para un clúster con un nodo principal en Azure (modelo de implementación de Resource Manager)**: a partir de HPC Pack 2016, la autenticación de certificado en una aplicación de Azure Active Directory se usa para aumentar y reducir automáticamente las máquinas virtuales del clúster implementadas mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="998c7-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="998c7-116">Configure un certificado de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="998c7-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="998c7-117">Después de la implementación del clúster, conéctese mediante Escritorio remoto a un nodo principal.</span><span class="sxs-lookup"><span data-stu-id="998c7-117">After cluster deployment, connect by Remote Desktop to one head node.</span></span>

  2. <span data-ttu-id="998c7-118">Cargue el certificado (formato PFX con clave privada) en cada nodo principal e instálelo en Cert: \LocalMachine\My y Cert: \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="998c7-118">Upload the certificate (PFX format with private key) to each head node and install to Cert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="998c7-119">Inicie Azure PowerShell como administrador y ejecute los siguientes comandos en un nodo principal:</span><span class="sxs-lookup"><span data-stu-id="998c7-119">Start Azure PowerShell as an administrator and run the following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="998c7-120">Si su cuenta está en más de un inquilino de Azure Active Directory o suscripción de Azure, puede ejecutar el siguiente comando para seleccionar el inquilino y la suscripción correctos:</span><span class="sxs-lookup"><span data-stu-id="998c7-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run the following command to select the correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="998c7-121">Ejecute el siguiente comando para ver el inquilino y la suscripción seleccionados en este momento:</span><span class="sxs-lookup"><span data-stu-id="998c7-121">Run the following command to view the currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="998c7-122">Ejecute el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="998c7-122">Run the following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="998c7-123">donde</span><span class="sxs-lookup"><span data-stu-id="998c7-123">where</span></span>

    <span data-ttu-id="998c7-124">**DisplayName**: nombre para mostrar de la aplicación Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="998c7-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="998c7-125">Si la aplicación no existe, se crea en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="998c7-125">If the application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="998c7-126">**Página principal** : la página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="998c7-126">**HomePage** - The home page of the application.</span></span> <span data-ttu-id="998c7-127">Puede configurar una dirección URL ficticia, como en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="998c7-127">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="998c7-128">**IdentifierUri**: identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="998c7-128">**IdentifierUri** - Identifier of the application.</span></span> <span data-ttu-id="998c7-129">Puede configurar una dirección URL ficticia, como en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="998c7-129">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="998c7-130">**CertificateThumbprint**: huella digital del certificado instalado en el nodo principal en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="998c7-130">**CertificateThumbprint** - Thumbprint of the certificate you installed on the head node in Step 1.</span></span>

    <span data-ttu-id="998c7-131">**TenantId**: id. del inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="998c7-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="998c7-132">Puede obtener el identificador del inquilino en la página **Propiedades** del portal de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="998c7-132">You can get the Tenant ID from the Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="998c7-133">Para más información sobre **ConfigARMAutoGrowShrinkCert.ps1**, ejecute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="998c7-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="998c7-134">**Para un clúster con un nodo principal en Azure (modelo de implementación clásica)**: si usa el script de implementación de HPC Pack IaaS para crear el clúster, habilite la propiedad**AutoGrowShrink** del clúster mediante la opción AutoGrowShrink del archivo de configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="998c7-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use the HPC Pack IaaS deployment script to create the cluster in the classic deployment model, enable the **AutoGrowShrink** cluster property by setting the AutoGrowShrink option in the cluster configuration file.</span></span> <span data-ttu-id="998c7-135">Para más información, consulte la documentación que acompaña a la [descarga del script](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="998c7-135">For details, see the documentation accompanying the [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="998c7-136">También puede habilitar la propiedad **AutoGrowShrink** del clúster después de implementar este mediante los comandos de HPC PowerShell que se describen en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="998c7-136">Alternatively, enable the **AutoGrowShrink** cluster property after you deploy the cluster by using HPC PowerShell commands described in the following section.</span></span> <span data-ttu-id="998c7-137">Para prepararse para esto, complete primero los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="998c7-137">To prepare for this, first complete the following steps:</span></span>

  1. <span data-ttu-id="998c7-138">Configure un certificado de administración de Azure en el nodo principal y en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="998c7-138">Configure an Azure management certificate on the head node and in the Azure subscription.</span></span> <span data-ttu-id="998c7-139">En una implementación de prueba, puede usar el certificado autofirmado de Azure predeterminado para Microsoft HPC que HPC Pack instala en el nodo principal y luego cargar ese certificado en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="998c7-139">For a test deployment, you can use the Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on the head node, and then upload that certificate to your Azure subscription.</span></span> <span data-ttu-id="998c7-140">Para las opciones y los pasos, consulte la [Guía de la biblioteca de TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="998c7-140">For options and steps, see the [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="998c7-141">Ejecute **regedit** en el nodo principal, vaya a HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo y agregue un nuevo valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="998c7-141">Run **regedit** on the head node, go to HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="998c7-142">Establezca Value name en "ThumbPrint" y Value data en la huella digital del certificado del paso 1.</span><span class="sxs-lookup"><span data-stu-id="998c7-142">Set the Value name to “ThumbPrint”, and Value data to the thumbprint of the certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-to-set-the-autogrowshrink-property"></a><span data-ttu-id="998c7-143">Comandos de HPC PowerShell para establecer la propiedad AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="998c7-143">HPC PowerShell commands to set the AutoGrowShrink property</span></span>
<span data-ttu-id="998c7-144">Los siguientes son ejemplos de comandos de HPC PowerShell para establecer **AutoGrowShrink** y ajustar su comportamiento con parámetros adicionales.</span><span class="sxs-lookup"><span data-stu-id="998c7-144">Following are sample HPC PowerShell commands to set **AutoGrowShrink** and to tune its behavior with additional parameters.</span></span> <span data-ttu-id="998c7-145">Consulte [Parámetros de AutoGrowShrink](#AutoGrowShrink-parameters) más adelante en este artículo para obtener una lista completa de las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="998c7-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for the complete list of settings.</span></span>

<span data-ttu-id="998c7-146">Para ejecutar estos comandos, inicie HPC PowerShell en el nodo principal del clúster como administrador.</span><span class="sxs-lookup"><span data-stu-id="998c7-146">To run these commands, start HPC PowerShell on the cluster head node as an administrator.</span></span>

<span data-ttu-id="998c7-147">**Para habilitar la propiedad AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="998c7-147">**To enable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="998c7-148">**Para deshabilitar la propiedad AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="998c7-148">**To disable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="998c7-149">**Para cambiar el intervalo de aumento en minutos**</span><span class="sxs-lookup"><span data-stu-id="998c7-149">**To change the grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="998c7-150">**Para cambiar el intervalo de reducción en minutos**</span><span class="sxs-lookup"><span data-stu-id="998c7-150">**To change the shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="998c7-151">**Para ver la configuración actual de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="998c7-151">**To view the current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="998c7-152">**Para excluir grupos de nodos de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="998c7-152">**To exclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="998c7-153">Este parámetro se admite a partir de HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="998c7-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="998c7-154">Parámetros de AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="998c7-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="998c7-155">Los siguientes son parámetros de AutoGrowShrink que se pueden modificar con el comando **Set-HpcClusterProperty** .</span><span class="sxs-lookup"><span data-stu-id="998c7-155">The following are AutoGrowShrink parameters that you can modify by using the **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="998c7-156">**EnableGrowShrink**: actívelo o desactívelo para habilitar o deshabilitar la propiedad **AutoGrowShrink**.</span><span class="sxs-lookup"><span data-stu-id="998c7-156">**EnableGrowShrink** - Switch to enable or disable the **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="998c7-157">**ParamSweepTasksPerCore** : número de tareas de barrido paramétrico para aumentar un núcleo.</span><span class="sxs-lookup"><span data-stu-id="998c7-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks to grow one core.</span></span> <span data-ttu-id="998c7-158">El valor predeterminado es aumentar un núcleo por tarea.</span><span class="sxs-lookup"><span data-stu-id="998c7-158">The default is to grow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="998c7-159">HPC Pack QFE KB3134307 cambia de **ParamSweepTasksPerCore** a **TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="998c7-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** to **TasksPerResourceUnit**.</span></span> <span data-ttu-id="998c7-160">Se basa en el tipo de recurso de trabajo y puede ser un nodo, un socket o un núcleo.</span><span class="sxs-lookup"><span data-stu-id="998c7-160">It is based on the job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="998c7-161">**GrowThreshold** : umbral de tareas en cola para desencadenar el crecimiento automático.</span><span class="sxs-lookup"><span data-stu-id="998c7-161">**GrowThreshold** - Threshold of queued tasks to trigger automatic growth.</span></span> <span data-ttu-id="998c7-162">El valor predeterminado es 1, lo que significa que si hay 1 o más tareas en estado en cola, los nodos aumentarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="998c7-162">The default is 1, which means that if there are 1 or more tasks in the queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="998c7-163">**GrowInterval** : intervalo en minutos para desencadenar el aumento automático.</span><span class="sxs-lookup"><span data-stu-id="998c7-163">**GrowInterval** - Interval in minutes to trigger automatic growth.</span></span> <span data-ttu-id="998c7-164">El intervalo predeterminado es de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="998c7-164">The default interval is 5 minutes.</span></span>
* <span data-ttu-id="998c7-165">**ShrinkInterval** : intervalo en minutos para desencadenar la reducción automática.</span><span class="sxs-lookup"><span data-stu-id="998c7-165">**ShrinkInterval** - Interval in minutes to trigger automatic shrinking.</span></span> <span data-ttu-id="998c7-166">El intervalo predeterminado es de 5 minutos.|</span><span class="sxs-lookup"><span data-stu-id="998c7-166">The default interval is 5 minutes.|</span></span>
* <span data-ttu-id="998c7-167">**ShrinkIdleTimes** : número de comprobaciones continuas que indican que los nodos están inactivos para reducirlos.</span><span class="sxs-lookup"><span data-stu-id="998c7-167">**ShrinkIdleTimes** - Number of continuous checks to shrink to indicate the nodes are idle.</span></span> <span data-ttu-id="998c7-168">El valor predeterminado es 3 veces.</span><span class="sxs-lookup"><span data-stu-id="998c7-168">The default is 3 times.</span></span> <span data-ttu-id="998c7-169">Por ejemplo, si el valor de **ShrinkInterval** es 5 minutos, HPC Pack comprueba si el nodo está inactivo cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="998c7-169">For example, if the **ShrinkInterval** is 5 minutes, HPC Pack checks whether the node is idle every 5 minutes.</span></span> <span data-ttu-id="998c7-170">Si los nodos están en estado de inactividad después de 3 comprobaciones continuas (15 minutos), HPC Pack reduce ese nodo.</span><span class="sxs-lookup"><span data-stu-id="998c7-170">If the nodes are in the idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="998c7-171">**ExtraNodesGrowRatio** : porcentaje adicional de nodos que se aumentará para los trabajos de la interfaz MPI (Message Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="998c7-171">**ExtraNodesGrowRatio** - Additional percentage of nodes to grow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="998c7-172">El valor predeterminado es 1, lo que significa que HPC Pack aumenta los nodos un 1 % para los trabajos de MPI.</span><span class="sxs-lookup"><span data-stu-id="998c7-172">The default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="998c7-173">**GrowByMin** : modificador que indica si la directiva de crecimiento automático se basa en los recursos mínimos necesarios para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="998c7-173">**GrowByMin** - Switch to indicate whether the autogrow policy is based on the minimum resources required for the job.</span></span> <span data-ttu-id="998c7-174">El valor predeterminado es false, lo que significa que HPC Pack aumenta los nodos para los trabajos según los recursos máximos necesarios para los trabajos.</span><span class="sxs-lookup"><span data-stu-id="998c7-174">The default is false, which means that HPC Pack grows nodes for jobs based on the maximum resources required for the jobs.</span></span>
* <span data-ttu-id="998c7-175">**SoaJobGrowThreshold** : umbral de solicitudes de SOA entrantes para desencadenar el proceso de crecimiento automático.</span><span class="sxs-lookup"><span data-stu-id="998c7-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests to trigger the automatic grow process.</span></span> <span data-ttu-id="998c7-176">El valor predeterminado es 50 000.</span><span class="sxs-lookup"><span data-stu-id="998c7-176">The default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="998c7-177">Este parámetro se admite a partir de HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="998c7-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="998c7-178">**SoaRequestsPerCore** : número de solicitudes de SOA entrantes para aumentar un núcleo.</span><span class="sxs-lookup"><span data-stu-id="998c7-178">**SoaRequestsPerCore** -Number of incoming SOA requests to grow one core.</span></span> <span data-ttu-id="998c7-179">El valor predeterminado es 20 000.</span><span class="sxs-lookup"><span data-stu-id="998c7-179">The default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="998c7-180">Este parámetro se admite a partir de HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="998c7-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="998c7-181">**ExcludeNodeGroups**: los nodos de los grupos de nodos especificados no aumentan y disminuyen de forma automática.</span><span class="sxs-lookup"><span data-stu-id="998c7-181">**ExcludeNodeGroups** – Nodes in the specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="998c7-182">Este parámetro se admite a partir de HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="998c7-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="998c7-183">Ejemplo de MPI</span><span class="sxs-lookup"><span data-stu-id="998c7-183">MPI example</span></span>
<span data-ttu-id="998c7-184">De forma predeterminada, HPC Pack aumenta un 1 % los nodos adicionales para los trabajos de MPI (**ExtraNodesGrowRatio** se establece en 1).</span><span class="sxs-lookup"><span data-stu-id="998c7-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set to 1).</span></span> <span data-ttu-id="998c7-185">El motivo es que MPI puede necesitar varios nodos y el trabajo solo se puede ejecutar cuando todos los nodos están listos.</span><span class="sxs-lookup"><span data-stu-id="998c7-185">The reason is that MPI may require multiple nodes, and the job can only run when all nodes are ready.</span></span> <span data-ttu-id="998c7-186">Cuando Azure inicia los nodos, en ocasiones un nodo puede necesitar más tiempo para iniciarse que otros, lo que provoca que los demás nodos estén inactivos mientras esperan a que ese nodo esté preparado.</span><span class="sxs-lookup"><span data-stu-id="998c7-186">When Azure starts nodes, occasionally one node might need more time to start than others, causing other nodes to be idle while waiting for that node to get ready.</span></span> <span data-ttu-id="998c7-187">Al aumentar los nodos adicionales, HPC Pack reduce este tiempo de espera de recursos y podría ahorrar costos.</span><span class="sxs-lookup"><span data-stu-id="998c7-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="998c7-188">Para aumentar el porcentaje de nodos adicionales para los trabajos MPI (por ejemplo, al 10 %), ejecute un comando similar a</span><span class="sxs-lookup"><span data-stu-id="998c7-188">To increase the percentage of extra nodes for MPI jobs (for example, to 10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="998c7-189">Ejemplo de SOA</span><span class="sxs-lookup"><span data-stu-id="998c7-189">SOA example</span></span>
<span data-ttu-id="998c7-190">De forma predeterminada,**SoaJobGrowThreshold** se establece en 50 000 y **SoaRequestsPerCore** se establece en 200 000.</span><span class="sxs-lookup"><span data-stu-id="998c7-190">By default, **SoaJobGrowThreshold** is set to 50000 and **SoaRequestsPerCore** is set to 200000.</span></span> <span data-ttu-id="998c7-191">Si envía un trabajo SOA con 70 000 solicitudes, hay una tarea en cola y las solicitudes entrantes son 70 000.</span><span class="sxs-lookup"><span data-stu-id="998c7-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="998c7-192">En este caso, HPC Pack crece un núcleo para la tarea en cola y, para las solicitudes entrantes, crece (70 000 - 50 000)/20 000 = 1 núcleo, por lo que crece en total 2 núcleos para este trabajo SOA.</span><span class="sxs-lookup"><span data-stu-id="998c7-192">In this case HPC Pack grows 1 core for the queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-the-azureautogrowshrinkps1-script"></a><span data-ttu-id="998c7-193">Ejecución del script AzureAutoGrowShrink.ps1</span><span class="sxs-lookup"><span data-stu-id="998c7-193">Run the AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="998c7-194">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="998c7-194">Prerequisites</span></span>

* <span data-ttu-id="998c7-195">**Clúster de HPC Pack 2012 R2 Update 1 o versiones posteriores**: el script **AzureAutoGrowShrink.ps1** se instala en la carpeta %CCP_HOME%bin.</span><span class="sxs-lookup"><span data-stu-id="998c7-195">**HPC Pack 2012 R2 Update 1 or later cluster** - The **AzureAutoGrowShrink.ps1** script is installed in the %CCP_HOME%bin folder.</span></span> <span data-ttu-id="998c7-196">El nodo principal del clúster se puede implementar de forma local o en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="998c7-196">The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="998c7-197">Vea [configurar un clúster híbrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) para comenzar con un nodo principal local y nodos de "ráfaga" de Azure.</span><span class="sxs-lookup"><span data-stu-id="998c7-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="998c7-198">Consulte el [script de implementación de HPC Pack IaaS ](hpcpack-cluster-powershell-script.md) para implementar rápidamente un clúster de HPC Pack en máquinas virtuales de Azure, o use una [plantilla de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="998c7-198">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="998c7-199">**Azure PowerShell 1.4.0**: actualmente, el script depende de esta versión específica de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="998c7-199">**Azure PowerShell 1.4.0** - The script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="998c7-200">**Para un clúster con nodos de ráfaga de Azure** : ejecute el script en un equipo cliente donde esté instalado HPC Pack o en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="998c7-200">**For a cluster with Azure burst nodes** - Run the script on a client computer where HPC Pack is installed, or on the head node.</span></span> <span data-ttu-id="998c7-201">Si se ejecuta en un equipo cliente, asegúrese de establecer la variable $env:CCP_SCHEDULER para que apunte al nodo principal.</span><span class="sxs-lookup"><span data-stu-id="998c7-201">If running on a client computer, ensure that you set the variable $env:CCP_SCHEDULER to point to the head node.</span></span> <span data-ttu-id="998c7-202">Los nodos de "ráfaga" de Azure deben haberse agregado al clúster, pero es posible que se encuentren en estado No implementado.</span><span class="sxs-lookup"><span data-stu-id="998c7-202">The Azure “burst” nodes must be added to the cluster, but they may be in the Not-Deployed state.</span></span>
* <span data-ttu-id="998c7-203">**Para un clúster implementado en máquinas virtuales de Azure (modelo de implementación de Resource Manager )**, el script admite dos métodos para la autenticación de Azure: iniciar sesión en su cuenta de Azure para ejecutar el script cada vez (mediante la ejecución de `Login-AzureRmAccount` o configurar una entidad de servicio para autenticarse con un certificado.</span><span class="sxs-lookup"><span data-stu-id="998c7-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in the Resource Manager deployment model, the script supports two methods for Azure authentication: sign in to your Azure account to run the script every time (by running `Login-AzureRmAccount`, or configure a service principal to authenticate with a certificate.</span></span> <span data-ttu-id="998c7-204">HPC Pack proporciona el script **ConfigARMAutoGrowShrinkCert.ps** para crear una entidad de servicio con el certificado.</span><span class="sxs-lookup"><span data-stu-id="998c7-204">HPC Pack provides the script **ConfigARMAutoGrowShrinkCert.ps** to create a service principal with certificate.</span></span> <span data-ttu-id="998c7-205">El script crea una aplicación de Azure Active Directory (Azure AD) y una entidad de servicio y asigna el rol Colaborador a la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="998c7-205">The script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns the Contributor role to the service principal.</span></span> <span data-ttu-id="998c7-206">Para ejecutar el script, inicie Azure PowerShell como administrador y ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="998c7-206">To run the script, start Azure PowerShell  as administrator and run the following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="998c7-207">Para más información sobre **ConfigARMAutoGrowShrinkCert.ps1**, ejecute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="998c7-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="998c7-208">**Para un clúster implementado en máquinas virtuales de Azure (modelo de implementación clásica)**: ejecute el script en la máquina virtual del nodo principal, porque depende de los scripts **Start-HpcIaaSNode.ps1** y **Stop-HpcIaaSNode.ps1** que están instalados allí.</span><span class="sxs-lookup"><span data-stu-id="998c7-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run the script on the head node VM, because it depends on the **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="998c7-209">Esas scripts requieren además un certificado de administración de Azure o un archivo de configuración de publicación (consulte [Administrar nodos de ejecución en un clúster de HPC Pack en Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="998c7-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="998c7-210">Asegúrese de que todas las máquinas virtuales de nodo de ejecución que necesita ya se agregaron al clúster.</span><span class="sxs-lookup"><span data-stu-id="998c7-210">Make sure all the compute node VMs you need are already added to the cluster.</span></span> <span data-ttu-id="998c7-211">Pueden tener el estado Detenido.</span><span class="sxs-lookup"><span data-stu-id="998c7-211">They may be in the Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="998c7-212">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="998c7-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="998c7-213">Parámetros</span><span class="sxs-lookup"><span data-stu-id="998c7-213">Parameters</span></span>
* <span data-ttu-id="998c7-214">**NodeTemplates** : nombres de las plantillas de nodos para definir el ámbito de crecimiento y reducción de los nodos aumente.</span><span class="sxs-lookup"><span data-stu-id="998c7-214">**NodeTemplates** - Names of the node templates to define the scope for the nodes to grow and shrink.</span></span> <span data-ttu-id="998c7-215">Si no se especifica (el valor predeterminado es @()), todos los nodos del grupo de nodos **AzureNodes** se encuentran dentro del ámbito cuando **NodeType** tiene un valor de AzureNodes, y todos los nodos del grupo de nodos **ComputeNodes** se encuentran dentro del ámbito cuando **NodeType** tiene un valor de ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="998c7-215">If not specified (the default value is @()), all nodes in the **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in the **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="998c7-216">**JobTemplates** : nombres de las plantillas de trabajos para definir el ámbito de crecimiento de los nodos.</span><span class="sxs-lookup"><span data-stu-id="998c7-216">**JobTemplates** - Names of the job templates to define the scope for the nodes to grow.</span></span>
* <span data-ttu-id="998c7-217">**NodeType** : el tipo que se va a aumentar y a reducir.</span><span class="sxs-lookup"><span data-stu-id="998c7-217">**NodeType** - The type of node to grow and shrink.</span></span> <span data-ttu-id="998c7-218">Los valores admitidos son:</span><span class="sxs-lookup"><span data-stu-id="998c7-218">Supported values are:</span></span>

  * <span data-ttu-id="998c7-219">**AzureNodes** : para los nodos (ráfaga) de Azure PaaS en un clúster de Azure IaaS o local.</span><span class="sxs-lookup"><span data-stu-id="998c7-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="998c7-220">**ComputeNodes** : para máquinas virtuales de nodos de ejecución solo en un clúster de Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="998c7-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="998c7-221">**NumOfQueuedJobsPerNodeToGrow** : número de trabajos en cola que se requieren para aumentar un nodo.</span><span class="sxs-lookup"><span data-stu-id="998c7-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required to grow one node.</span></span>
* <span data-ttu-id="998c7-222">**NumOfQueuedJobsToGrowThreshold** : el número máximo de trabajos en cola para iniciar el proceso de crecimiento.</span><span class="sxs-lookup"><span data-stu-id="998c7-222">**NumOfQueuedJobsToGrowThreshold** - The threshold number of queued jobs to start the grow process.</span></span>
* <span data-ttu-id="998c7-223">**NumOfActiveQueuedTasksPerNodeToGrow** : el número de tareas en cola activas necesarias para aumentar un nodo.</span><span class="sxs-lookup"><span data-stu-id="998c7-223">**NumOfActiveQueuedTasksPerNodeToGrow** - The number of active queued tasks required to grow one node.</span></span> <span data-ttu-id="998c7-224">Si se especifica **NumOfQueuedJobsPerNodeToGrow** con un valor superior a 0, se omite este parámetro.</span><span class="sxs-lookup"><span data-stu-id="998c7-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="998c7-225">**NumOfActiveQueuedTasksToGrowThreshold** : el número máximo de tareas en cola activas para iniciar el proceso de crecimiento.</span><span class="sxs-lookup"><span data-stu-id="998c7-225">**NumOfActiveQueuedTasksToGrowThreshold** - The threshold number of active queued tasks to start the grow process.</span></span>
* <span data-ttu-id="998c7-226">**NumOfInitialNodesToGrow**: el número mínimo inicial de nodos que se van a aumentar si todos los nodos del ámbito tienen el estado **No implementado** o **Detenido (desasignado)**.</span><span class="sxs-lookup"><span data-stu-id="998c7-226">**NumOfInitialNodesToGrow** - The initial minimum number of nodes to grow if all the nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="998c7-227">**GrowCheckIntervalMins** : el intervalo en minutos entre comprobaciones que se van a aumentar.</span><span class="sxs-lookup"><span data-stu-id="998c7-227">**GrowCheckIntervalMins** - The interval in minutes between checks to grow.</span></span>
* <span data-ttu-id="998c7-228">**ShrinkCheckIntervalMins** : el intervalo en minutos entre comprobaciones que se van a reducir.</span><span class="sxs-lookup"><span data-stu-id="998c7-228">**ShrinkCheckIntervalMins** - The interval in minutes between checks to shrink.</span></span>
* <span data-ttu-id="998c7-229">**ShrinkCheckIdleTimes**: el número de comprobaciones de reducción continua (separadas por **ShrinkCheckIntervalMins)** para indicar que los nodos están inactivos.</span><span class="sxs-lookup"><span data-stu-id="998c7-229">**ShrinkCheckIdleTimes** - The number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) to indicate the nodes are idle.</span></span>
* <span data-ttu-id="998c7-230">**UseLastConfigurations** : las configuraciones anteriores guardadas en el archivo de argumentos.</span><span class="sxs-lookup"><span data-stu-id="998c7-230">**UseLastConfigurations** - The previous configurations saved in the argument file.</span></span>
* <span data-ttu-id="998c7-231">**ArgFile**: el nombre del archivo de argumento usado para guardar y actualizar las configuraciones para ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="998c7-231">**ArgFile**- The name of the argument file used to save and update the configurations to run the script.</span></span>
* <span data-ttu-id="998c7-232">**LogFilePrefix** : el nombre del prefijo del archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="998c7-232">**LogFilePrefix** - The prefix name of the log file.</span></span> <span data-ttu-id="998c7-233">Puede especificar una ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="998c7-233">You can specify a path.</span></span> <span data-ttu-id="998c7-234">De forma predeterminada, el registro escrito en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="998c7-234">By default the log is written to the current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="998c7-235">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="998c7-235">Example 1</span></span>
<span data-ttu-id="998c7-236">En el ejemplo siguiente se configuran los nodos de ráfaga de Azure implementados con la plantilla AzureNode predeterminada para aumentar y reducir automáticamente.</span><span class="sxs-lookup"><span data-stu-id="998c7-236">The following example configures the Azure burst nodes deployed with the Default AzureNode Template to grow and shrink automatically.</span></span> <span data-ttu-id="998c7-237">Si todos los nodos se encuentran inicialmente en el nodo **Not-Deployed** , se inician al menos 3 nodos.</span><span class="sxs-lookup"><span data-stu-id="998c7-237">If all the nodes are initially in the **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="998c7-238">Si el número de trabajos en cola es superior a 8, el script inicia nodos hasta que su número supera la proporción de trabajos en cola en **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="998c7-238">If the number of queued jobs exceeds 8, the script starts nodes until their number exceeds the ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="998c7-239">Si se descubre que un nodo está inactivo en 3 tiempos de inactividad consecutivos, se detiene.</span><span class="sxs-lookup"><span data-stu-id="998c7-239">If a node is found to be idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="998c7-240">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="998c7-240">Example 2</span></span>
<span data-ttu-id="998c7-241">En el ejemplo siguiente se configuran las máquinas virtuales del nodo de ejecución de Azure con la plantilla de ComputeNode predeterminada para aumentar y disminuir automáticamente.</span><span class="sxs-lookup"><span data-stu-id="998c7-241">The following example configures the Azure compute node VMs deployed with the Default ComputeNode Template to grow and shrink automatically.</span></span>
<span data-ttu-id="998c7-242">Los trabajos configurados por la plantilla de trabajo predeterminada definen el ámbito de la carga de trabajo en el clúster.</span><span class="sxs-lookup"><span data-stu-id="998c7-242">The jobs configured by the Default job template define the scope of the workload on the cluster.</span></span> <span data-ttu-id="998c7-243">Si todos los nodos se detienen inicialmente, se inician al menos 5 nodos.</span><span class="sxs-lookup"><span data-stu-id="998c7-243">If all the nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="998c7-244">Si el número de tareas en cola activas es superior a 15, el script inicia nodos hasta que su número supera la relación de tareas en cola activas en **NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="998c7-244">If the number of active queued tasks exceeds 15, the script starts nodes until their number exceeds the ratio of active queued tasks to **NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="998c7-245">Si se descubre que un nodo está inactivo en 10 tiempos de inactividad consecutivos, se detiene.</span><span class="sxs-lookup"><span data-stu-id="998c7-245">If a node is found to be idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
