---
title: "nodos de clúster de HPC Pack aaaAutoscale | Documentos de Microsoft"
description: "Automáticamente aumentar y reducir el número de Hola de nodos de proceso de clúster de HPC Pack en Azure"
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
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="b5c89-103">Automáticamente aumentar y reducir los recursos de clúster de HPC Pack hello en Azure según la carga de trabajo de clúster toohello</span><span class="sxs-lookup"><span data-stu-id="b5c89-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="b5c89-104">Si implementar nodos de Azure "irrumpir" en el clúster de HPC Pack, o crear un clúster de HPC Pack en máquinas virtuales de Azure, puede que desee una manera de aumentar o reducir los recursos de clúster de hello como nodos o núcleos según la carga de trabajo de hello en clúster de hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b5c89-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="b5c89-105">Ajuste de escala en recursos de clúster de Hola de esta manera permite toouse los recursos de Azure más eficazmente y controlar los costes.</span><span class="sxs-lookup"><span data-stu-id="b5c89-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="b5c89-106">Este artículo muestra dos maneras de HPC Pack proporciona recursos de proceso de tooautoscale:</span><span class="sxs-lookup"><span data-stu-id="b5c89-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="b5c89-107">propiedad de clúster de HPC Pack Hello **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="b5c89-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="b5c89-108">Hola **AzureAutoGrowShrink.ps1** script de PowerShell de HPC</span><span class="sxs-lookup"><span data-stu-id="b5c89-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b5c89-109">Actualmente solo se pueden aumentar y reducir automáticamente los nodos de proceso de HPC Pack que ejecutan un sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b5c89-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="b5c89-110">Establecer la propiedad de clúster de hello AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="b5c89-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="b5c89-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b5c89-111">Prerequisites</span></span>

* <span data-ttu-id="b5c89-112">**HPC Pack 2012 R2 Update 2 o posterior clúster** -nodo principal del clúster Hola puede ser implementado de forma local o en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5c89-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="b5c89-113">Vea [configurar un clúster híbrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget a trabajar con un nodo principal en local y nodos de ráfaga de Azure"".</span><span class="sxs-lookup"><span data-stu-id="b5c89-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="b5c89-114">Vea hello [script de implementación de IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly implementar un clúster de HPC Pack en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5c89-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="b5c89-115">**Para un clúster con un nodo principal en Azure (modelo de implementación de Resource Manager)**: a partir de HPC Pack 2016, la autenticación de certificado en una aplicación de Azure Active Directory se usa para aumentar y reducir automáticamente las máquinas virtuales del clúster implementadas mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b5c89-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="b5c89-116">Configure un certificado de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="b5c89-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="b5c89-117">Después de la implementación de clúster, conéctese al nodo principal de tooone de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="b5c89-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="b5c89-118">Cargue el nodo principal de hello certificado (formato PFX con clave privada) tooeach e instale tooCert:\LocalMachine\My y Cert: \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="b5c89-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="b5c89-119">Iniciar Azure PowerShell como administrador y ejecute hello siguientes comandos en un nodo principal:</span><span class="sxs-lookup"><span data-stu-id="b5c89-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="b5c89-120">Si su cuenta está en más de un inquilino de Azure Active Directory o suscripción de Azure, puede ejecutar Hola siguiente comando inquilino correcto de tooselect Hola y de suscripción:</span><span class="sxs-lookup"><span data-stu-id="b5c89-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="b5c89-121">Ejecute hello después tooview comando hello seleccionada actualmente inquilino y la suscripción:</span><span class="sxs-lookup"><span data-stu-id="b5c89-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="b5c89-122">Ejecute la siguiente secuencia de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="b5c89-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="b5c89-123">donde</span><span class="sxs-lookup"><span data-stu-id="b5c89-123">where</span></span>

    <span data-ttu-id="b5c89-124">**DisplayName**: nombre para mostrar de la aplicación Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5c89-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="b5c89-125">Si la aplicación hello no existe, se crea en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5c89-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="b5c89-126">**Página principal de** -página principal de Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b5c89-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="b5c89-127">Puede configurar una dirección URL ficticia, como en el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="b5c89-128">**IdentifierUri** -identificador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b5c89-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="b5c89-129">Puede configurar una dirección URL ficticia, como en el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="b5c89-130">**CertificateThumbprint** -huella digital del certificado de hello instalado en el nodo principal de hello en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="b5c89-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="b5c89-131">**TenantId**: id. del inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5c89-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="b5c89-132">Puede obtener Id. de inquilino de Hola desde el portal de Azure Active Directory hello **propiedades** página.</span><span class="sxs-lookup"><span data-stu-id="b5c89-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="b5c89-133">Para más información sobre **ConfigARMAutoGrowShrinkCert.ps1**, ejecute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="b5c89-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="b5c89-134">**Para un clúster con un nodo principal en Azure (modelo de implementación clásica)** : Si utiliza Hola IaaS de HPC Pack implementación script toocreate Hola clúster en el modelo de implementación clásica de hello, habilitar hello **AutoGrowShrink** clúster propiedad estableciendo la opción de AutoGrowShrink de hello en el archivo de configuración del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="b5c89-135">Para obtener más información, consulte documentación de Hola que acompaña hello [descarga del script](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="b5c89-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="b5c89-136">También puede habilitar hello **AutoGrowShrink** propiedad del clúster después de implementar el clúster de hello mediante PowerShell de HPC comandos descrito en hello pasos de la sección.</span><span class="sxs-lookup"><span data-stu-id="b5c89-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="b5c89-137">tooprepare para esto, primera Hola completa siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="b5c89-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="b5c89-138">Configurar un certificado de administración de Azure en el nodo principal de Hola y Hola suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5c89-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="b5c89-139">Para una implementación de prueba, puede usar Hola predeterminado Microsoft HPC Azure certificado autofirmado que HPC Pack se instala en el nodo principal de hello y, a continuación, cargar ese tooyour certificado suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5c89-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="b5c89-140">Para las opciones y los pasos, vea hello [Guía de la biblioteca de TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5c89-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="b5c89-141">Ejecutar **regedit** en el nodo principal de hello, vaya tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo y agregue un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="b5c89-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="b5c89-142">Establece el nombre del valor de hello demasiado "Huella digital" y datos de valor toohello huella digital del certificado de hello en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="b5c89-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="b5c89-143">Propiedad de tooset hello AutoGrowShrink de comandos de PowerShell de HPC</span><span class="sxs-lookup"><span data-stu-id="b5c89-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="b5c89-144">Estos son tooset de comandos de PowerShell de HPC de ejemplo **AutoGrowShrink** y tootune su comportamiento con parámetros adicionales.</span><span class="sxs-lookup"><span data-stu-id="b5c89-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="b5c89-145">Vea [AutoGrowShrink parámetros](#AutoGrowShrink-parameters) más adelante en este artículo para la lista completa de Hola de configuración.</span><span class="sxs-lookup"><span data-stu-id="b5c89-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="b5c89-146">toorun estos comandos, inicie HPC PowerShell en el nodo principal del clúster de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="b5c89-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="b5c89-147">**Hola tooenable AutoGrowShrink propiedad**</span><span class="sxs-lookup"><span data-stu-id="b5c89-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="b5c89-148">**Hola toodisable AutoGrowShrink propiedad**</span><span class="sxs-lookup"><span data-stu-id="b5c89-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="b5c89-149">**Hola toochange aumentan el intervalo en minutos**</span><span class="sxs-lookup"><span data-stu-id="b5c89-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="b5c89-150">**Hola toochange reducir el intervalo en minutos**</span><span class="sxs-lookup"><span data-stu-id="b5c89-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="b5c89-151">**configuración actual de hello tooview de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="b5c89-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="b5c89-152">**grupos de nodos de tooexclude de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="b5c89-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="b5c89-153">Este parámetro se admite a partir de HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="b5c89-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="b5c89-154">Parámetros de AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="b5c89-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="b5c89-155">Hello siguientes son AutoGrowShrink parámetros que se pueden modificar mediante el uso de hello **HpcClusterProperty conjunto** comando.</span><span class="sxs-lookup"><span data-stu-id="b5c89-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="b5c89-156">**EnableGrowShrink** : cambiar tooenable o deshabilitar hello **AutoGrowShrink** propiedad.</span><span class="sxs-lookup"><span data-stu-id="b5c89-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="b5c89-157">**ParamSweepTasksPerCore** -número de barrido paramétrico tareas toogrow un núcleo.</span><span class="sxs-lookup"><span data-stu-id="b5c89-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="b5c89-158">valor predeterminado de Hello es toogrow un núcleo por tarea.</span><span class="sxs-lookup"><span data-stu-id="b5c89-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b5c89-159">Cambios de HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** demasiado**TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="b5c89-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="b5c89-160">Se basa en el tipo de recurso de trabajo de Hola y puede ser el nodo, un socket o core.</span><span class="sxs-lookup"><span data-stu-id="b5c89-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="b5c89-161">**GrowThreshold** -umbral de crecimiento automático de tootrigger de tareas en cola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="b5c89-162">valor predeterminado de Hello es 1, lo que significa que si hay 1 o más tareas en Hola estado en cola, expandir automáticamente los nodos.</span><span class="sxs-lookup"><span data-stu-id="b5c89-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="b5c89-163">**GrowInterval** -intervalo de crecimiento automático de tootrigger de minutos.</span><span class="sxs-lookup"><span data-stu-id="b5c89-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="b5c89-164">intervalo de saludo predeterminado es 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="b5c89-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="b5c89-165">**ShrinkInterval** -intervalo en minutos tootrigger reducirse de forma automática.</span><span class="sxs-lookup"><span data-stu-id="b5c89-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="b5c89-166">intervalo de saludo predeterminado es 5 minutos. |</span><span class="sxs-lookup"><span data-stu-id="b5c89-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="b5c89-167">**ShrinkIdleTimes** -número de comprobaciones continua tooshrink tooindicate Hola nodos está inactivo.</span><span class="sxs-lookup"><span data-stu-id="b5c89-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="b5c89-168">valor predeterminado de Hello es 3 veces.</span><span class="sxs-lookup"><span data-stu-id="b5c89-168">hello default is 3 times.</span></span> <span data-ttu-id="b5c89-169">Por ejemplo, si hello **ShrinkInterval** es 5 minutos, HPC Pack comprueba si el nodo de hello está inactivo cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="b5c89-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="b5c89-170">Si hay nodos de hello en estado de inactividad de Hola tras 3 continua comprobaciones (15 minutos), HPC Pack se reduce a ese nodo.</span><span class="sxs-lookup"><span data-stu-id="b5c89-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="b5c89-171">**ExtraNodesGrowRatio** -porcentaje adicional de toogrow de nodos para los trabajos de la interfaz de paso de mensajes (MPI).</span><span class="sxs-lookup"><span data-stu-id="b5c89-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="b5c89-172">valor predeterminado de Hello es 1, lo que significa que HPC Pack crece nodos 1% para los trabajos MPI.</span><span class="sxs-lookup"><span data-stu-id="b5c89-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="b5c89-173">**GrowByMin** -cambiar tooindicate si están basada en directivas de crecimiento automático de hello en recursos de hello mínimos requeridos para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="b5c89-174">Hola es false, lo que significa que HPC Pack crece nodos para los trabajos según los recursos de hello máximo requeridos para trabajos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="b5c89-175">**SoaJobGrowThreshold** -umbral de entrante Hola de tootrigger SOA solicitudes automática crecer proceso.</span><span class="sxs-lookup"><span data-stu-id="b5c89-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="b5c89-176">valor predeterminado de Hello es 50000.</span><span class="sxs-lookup"><span data-stu-id="b5c89-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b5c89-177">Este parámetro se admite a partir de HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="b5c89-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="b5c89-178">**SoaRequestsPerCore** -número de SOA entrante solicitudes toogrow un núcleo.</span><span class="sxs-lookup"><span data-stu-id="b5c89-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="b5c89-179">valor predeterminado de Hello es 20000.</span><span class="sxs-lookup"><span data-stu-id="b5c89-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b5c89-180">Este parámetro se admite a partir de HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="b5c89-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="b5c89-181">**ExcludeNodeGroups** : los nodos en hello especificar grupos de nodos aumentar y reducir de forma automática.</span><span class="sxs-lookup"><span data-stu-id="b5c89-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="b5c89-182">Este parámetro se admite a partir de HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="b5c89-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="b5c89-183">Ejemplo de MPI</span><span class="sxs-lookup"><span data-stu-id="b5c89-183">MPI example</span></span>
<span data-ttu-id="b5c89-184">De forma predeterminada HPC Pack crece 1% nodos adicionales para los trabajos MPI (**ExtraNodesGrowRatio** se establece too1).</span><span class="sxs-lookup"><span data-stu-id="b5c89-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="b5c89-185">motivo de Hello es que MPI puede requerir varios nodos, y solo se puede ejecutar el trabajo de hello cuando todos los nodos están listos.</span><span class="sxs-lookup"><span data-stu-id="b5c89-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="b5c89-186">En ocasiones cuando Azure inicia nodos, un nodo que tenga más toostart de tiempo que otras, haciendo que otros toobe nodos inactivo mientras se espera que tooget nodo preparado.</span><span class="sxs-lookup"><span data-stu-id="b5c89-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="b5c89-187">Al aumentar los nodos adicionales, HPC Pack reduce este tiempo de espera de recursos y podría ahorrar costos.</span><span class="sxs-lookup"><span data-stu-id="b5c89-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="b5c89-188">porcentaje de hello tooincrease de nodos adicionales para los trabajos MPI (por ejemplo, too10%), ejecute un comando similar a</span><span class="sxs-lookup"><span data-stu-id="b5c89-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="b5c89-189">Ejemplo de SOA</span><span class="sxs-lookup"><span data-stu-id="b5c89-189">SOA example</span></span>
<span data-ttu-id="b5c89-190">De forma predeterminada, **SoaJobGrowThreshold** se establece too50000 y **SoaRequestsPerCore** se establece too200000.</span><span class="sxs-lookup"><span data-stu-id="b5c89-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="b5c89-191">Si envía un trabajo SOA con 70 000 solicitudes, hay una tarea en cola y las solicitudes entrantes son 70 000.</span><span class="sxs-lookup"><span data-stu-id="b5c89-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="b5c89-192">En este caso HPC Pack crece 1 núcleo de hello en cola tareas y para las solicitudes entrantes, crece (70000 50000) / principales 20000 = 1, por lo que en total crece 2 núcleos para este trabajo SOA.</span><span class="sxs-lookup"><span data-stu-id="b5c89-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="b5c89-193">Ejecutar script de Hola AzureAutoGrowShrink.ps1</span><span class="sxs-lookup"><span data-stu-id="b5c89-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="b5c89-194">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b5c89-194">Prerequisites</span></span>

* <span data-ttu-id="b5c89-195">**HPC Pack 2012 R2 Update 1 o posterior clúster** : hello **AzureAutoGrowShrink.ps1** está instalado en la carpeta Hola % CCP_HOME % bin.</span><span class="sxs-lookup"><span data-stu-id="b5c89-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="b5c89-196">nodo principal del clúster Hola puede ser implementado de forma local o en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5c89-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="b5c89-197">Vea [configurar un clúster híbrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget a trabajar con un nodo principal en local y nodos de ráfaga de Azure"".</span><span class="sxs-lookup"><span data-stu-id="b5c89-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="b5c89-198">Vea hello [script de implementación de IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly implementar un clúster de HPC Pack en máquinas virtuales de Azure o use un [plantilla de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="b5c89-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="b5c89-199">**Azure PowerShell 1.4.0** -script de Hola actualmente depende de esta versión específica de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5c89-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="b5c89-200">**Para un clúster con Azure en ráfagas nodos** -ejecutar script de Hola en un equipo cliente donde se instaló el paquete de HPC, o en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="b5c89-201">Si se ejecuta en un equipo cliente, asegúrese de establecer hello $env variable: nodo principal de CCP_SCHEDULER toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="b5c89-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="b5c89-202">se deben agregar nodos de Azure «"ráfaga" Hello toohello clúster, pero pueden encontrarse en hello estado no implementado.</span><span class="sxs-lookup"><span data-stu-id="b5c89-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="b5c89-203">**Para un clúster implementado en máquinas virtuales de Azure (modelo de implementación de administrador de recursos)** -para un clúster de máquinas virtuales de Azure implementadas en el modelo de implementación del Administrador de recursos de hello, el script de Hola admite dos métodos para la autenticación de Azure: inicie sesión en tooyour cuenta de Azure script de Hola toorun cada vez (mediante la ejecución de `Login-AzureRmAccount`, o configurar un tooauthenticate principal de servicio con un certificado.</span><span class="sxs-lookup"><span data-stu-id="b5c89-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="b5c89-204">HPC Pack proporciona el script de Hola **ConfigARMAutoGrowShrinkCert.ps** toocreate una entidad de servicio con el certificado.</span><span class="sxs-lookup"><span data-stu-id="b5c89-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="b5c89-205">script de Hola crea una aplicación de Azure Active Directory (Azure AD) y una entidad de servicio y asigna la entidad de servicio de toohello de rol de colaborador de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="b5c89-206">script de Hola toorun, iniciar Azure PowerShell como administrador y ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="b5c89-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="b5c89-207">Para más información sobre **ConfigARMAutoGrowShrinkCert.ps1**, ejecute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="b5c89-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="b5c89-208">**Para un clúster implementado en máquinas virtuales de Azure (modelo de implementación clásica)** -ejecutar script de Hola en máquina virtual del nodo principal Hola porque depende de hello **Start-HpcIaaSNode.ps1** y **Stop-HpcIaaSNode.ps1**secuencias de comandos que están instalados allí.</span><span class="sxs-lookup"><span data-stu-id="b5c89-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="b5c89-209">Esas scripts requieren además un certificado de administración de Azure o un archivo de configuración de publicación (consulte [Administrar nodos de ejecución en un clúster de HPC Pack en Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="b5c89-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="b5c89-210">Asegúrese de que Hola todas las máquinas virtuales que se necesita del nodo ya se han agregado toohello clúster de proceso.</span><span class="sxs-lookup"><span data-stu-id="b5c89-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="b5c89-211">Pueden encontrarse en estado detenido Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="b5c89-212">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="b5c89-212">Syntax</span></span>
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
### <a name="parameters"></a><span data-ttu-id="b5c89-213">parameters</span><span class="sxs-lookup"><span data-stu-id="b5c89-213">Parameters</span></span>
* <span data-ttu-id="b5c89-214">**NodeTemplates** -nombres de toodefine de plantillas de nodo de Hola Hola ámbito para toogrow de nodos de Hola y reducir.</span><span class="sxs-lookup"><span data-stu-id="b5c89-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="b5c89-215">Si no se especifica (valor predeterminado de hello es @()), todos los nodos de hello **AzureNodes** grupo de nodos están dentro del ámbito cuando **NodeType** tiene un valor de AzureNodes y todos los nodos en hello **ComputeNodes** grupo de nodos están dentro del ámbito cuando **NodeType** tiene un valor de ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="b5c89-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="b5c89-216">**JobTemplates** -nombres de hello ámbito plantillas toodefine Hola Hola nodos toogrow del trabajo.</span><span class="sxs-lookup"><span data-stu-id="b5c89-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="b5c89-217">**NodeType** : tipo de nodo toogrow de Hola y reducir.</span><span class="sxs-lookup"><span data-stu-id="b5c89-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="b5c89-218">Los valores admitidos son:</span><span class="sxs-lookup"><span data-stu-id="b5c89-218">Supported values are:</span></span>

  * <span data-ttu-id="b5c89-219">**AzureNodes** : para los nodos (ráfaga) de Azure PaaS en un clúster de Azure IaaS o local.</span><span class="sxs-lookup"><span data-stu-id="b5c89-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="b5c89-220">**ComputeNodes** : para máquinas virtuales de nodos de ejecución solo en un clúster de Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="b5c89-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="b5c89-221">**NumOfQueuedJobsPerNodeToGrow** -número de trabajos en cola requiere toogrow un nodo.</span><span class="sxs-lookup"><span data-stu-id="b5c89-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="b5c89-222">**NumOfQueuedJobsToGrowThreshold** -número de umbral de Hola de hello toostart de trabajos en cola crezca proceso.</span><span class="sxs-lookup"><span data-stu-id="b5c89-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="b5c89-223">**NumOfActiveQueuedTasksPerNodeToGrow** -número de Hola de tareas en cola activas necesarias toogrow un nodo.</span><span class="sxs-lookup"><span data-stu-id="b5c89-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="b5c89-224">Si se especifica **NumOfQueuedJobsPerNodeToGrow** con un valor superior a 0, se omite este parámetro.</span><span class="sxs-lookup"><span data-stu-id="b5c89-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="b5c89-225">**NumOfActiveQueuedTasksToGrowThreshold** -número de umbral de Hola de Hola de tareas en cola activas toostart aumenta de proceso.</span><span class="sxs-lookup"><span data-stu-id="b5c89-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="b5c89-226">**NumOfInitialNodesToGrow** : hello inicial número mínimo de nodos toogrow si todos los nodos de hello en el ámbito son **no implementado** o **detenido (desasignado)**.</span><span class="sxs-lookup"><span data-stu-id="b5c89-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="b5c89-227">**GrowCheckIntervalMins** -intervalo de saludo en minutos entre comprobaciones toogrow.</span><span class="sxs-lookup"><span data-stu-id="b5c89-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="b5c89-228">**ShrinkCheckIntervalMins** -intervalo de saludo en minutos entre comprobaciones tooshrink.</span><span class="sxs-lookup"><span data-stu-id="b5c89-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="b5c89-229">**ShrinkCheckIdleTimes** -Hola número de comprobaciones de reducción continuas (separadas por **ShrinkCheckIntervalMins**) tooindicate Hola nodos están inactivos.</span><span class="sxs-lookup"><span data-stu-id="b5c89-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="b5c89-230">**UseLastConfigurations** -Hola configuraciones anteriores guardadas en un archivo de argumento Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="b5c89-231">**ArgFile**: Hola nombre de toosave de archivo que se utiliza de argumento de Hola y Hola configuraciones toorun Hola script de actualización.</span><span class="sxs-lookup"><span data-stu-id="b5c89-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="b5c89-232">**LogFilePrefix** -nombre del prefijo Hola Hola del archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="b5c89-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="b5c89-233">Puede especificar una ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="b5c89-233">You can specify a path.</span></span> <span data-ttu-id="b5c89-234">De forma predeterminada el registro de hello está escrito toohello directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="b5c89-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="b5c89-235">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="b5c89-235">Example 1</span></span>
<span data-ttu-id="b5c89-236">Hello en el ejemplo siguiente se configura hello Azure irrumpir nodos implementados con la plantilla AzureNode predeterminada toogrow y reducir automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b5c89-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="b5c89-237">Si todos los nodos están inicialmente en hello **no implementado** estado, se inician al menos 3 nodos.</span><span class="sxs-lookup"><span data-stu-id="b5c89-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="b5c89-238">Si el número de Hola de trabajos en cola supera los 8, el script de Hola inicia nodos hasta que su número supera la relación de Hola de trabajos en cola para **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="b5c89-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="b5c89-239">Si un nodo no se encuentra inactivo en 3 tiempos de inactividad consecutivas toobe, se detiene.</span><span class="sxs-lookup"><span data-stu-id="b5c89-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="b5c89-240">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="b5c89-240">Example 2</span></span>
<span data-ttu-id="b5c89-241">Hello en el ejemplo siguiente se configura hello Azure compute máquinas virtuales de nodos que se implementa con hello plantilla ComputeNode predeterminada toogrow y reducir automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b5c89-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="b5c89-242">trabajos de Hello configurados por plantilla de trabajo predeterminada de hello definen ámbito de hello de la carga de trabajo en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5c89-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="b5c89-243">Si inicialmente se detienen todos los nodos de hello, se inician al menos 5 nodos.</span><span class="sxs-lookup"><span data-stu-id="b5c89-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="b5c89-244">Si el número de Hola de tareas en cola activas supera las 15, el script de Hola inicia nodos hasta que su número supera relación de Hola de tareas en cola activas demasiado**NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="b5c89-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="b5c89-245">Si un nodo no se encuentra inactivo en 10 tiempos de inactividad consecutivas toobe, se detiene.</span><span class="sxs-lookup"><span data-stu-id="b5c89-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
