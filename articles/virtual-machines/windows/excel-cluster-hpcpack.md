---
title: "aaaHPC módulo de clúster para Excel y SOA | Documentos de Microsoft"
description: "Introducción a la ejecución de cargas de trabajo de Excel y SOA a gran escala en un clúster de HPC Pack en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="ba010-103">Introducción a la ejecución de cargas de trabajo de Excel y SOA en un clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="ba010-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="ba010-104">Este artículo muestra cómo toodeploy Microsoft HPC Pack 2012 R2 de clúster en máquinas virtuales de Azure mediante el uso de una plantilla de inicio rápido de Azure o, opcionalmente, un script de implementación de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba010-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="ba010-105">clúster de Hello usa Azure Marketplace VM imágenes diseñadas toorun Microsoft Excel o cargas de trabajo de arquitectura orientada a servicios (SOA) con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ba010-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="ba010-106">Puede usar hello toorun de clúster HPC de Excel y servicios SOA desde un equipo de cliente local.</span><span class="sxs-lookup"><span data-stu-id="ba010-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="ba010-107">Servicios de HPC de Excel de Hello incluyen la descarga del libro de Excel y funciones definidas por el usuario de Excel o UDF.</span><span class="sxs-lookup"><span data-stu-id="ba010-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ba010-108">Este artículo se basa en características, plantillas y scripts de HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="ba010-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="ba010-109">Este escenario no se admite actualmente en HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="ba010-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ba010-110">En un nivel alto, hello siguiente diagrama muestra clúster de HPC Pack Hola que haya creado.</span><span class="sxs-lookup"><span data-stu-id="ba010-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![Clúster HPC con nodos que ejecutan cargas de trabajo de Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="ba010-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ba010-112">Prerequisites</span></span>
* <span data-ttu-id="ba010-113">**Equipo cliente** -necesita un cliente basado en Windows equipo toosubmit ejemplo Excel y SOA trabajos toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="ba010-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="ba010-114">También necesita un hello toorun de equipo de Windows Azure PowerShell script de implementación de clúster (si elige ese método de implementación).</span><span class="sxs-lookup"><span data-stu-id="ba010-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="ba010-115">**Suscripción de Azure** : si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/) en un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="ba010-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="ba010-116">**Cuota de núcleos** -podría necesita tooincrease Hola cuota de núcleos, especialmente si implementa varios nodos de clúster con tamaños de máquinas virtuales con varios núcleos.</span><span class="sxs-lookup"><span data-stu-id="ba010-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="ba010-117">Si está utilizando una plantilla de inicio rápido de Azure, cuota de núcleos de hello en el Administrador de recursos es por región de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba010-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="ba010-118">En ese caso, tendrá que tooincrease cuota de hello en una región específica.</span><span class="sxs-lookup"><span data-stu-id="ba010-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="ba010-119">Consulte [Límites, cuotas y restricciones de suscripción de Azure](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="ba010-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="ba010-120">tooincrease una cuota, [abrir una solicitud de soporte al cliente en línea](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sin cargo.</span><span class="sxs-lookup"><span data-stu-id="ba010-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="ba010-121">**Licencia de Microsoft Office**: si implementa nodos de proceso con una imagen de máquina virtual de Marketplace HPC Pack 2012 R2 con Microsoft Excel, se instala una versión de evaluación de 30 días de Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="ba010-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="ba010-122">Tras el período de evaluación de hello, necesita tooprovide un válido Microsoft Office licencia tooactivate Excel toocontinue toorun cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ba010-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="ba010-123">Consulte [Activación de Excel](#excel-activation) que aparece más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ba010-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="ba010-124">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="ba010-124">Step 1.</span></span> <span data-ttu-id="ba010-125">Configuración e un clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="ba010-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="ba010-126">Se muestra dos tooset opciones de clúster de HPC Pack 2012 R2 hello: en primer lugar, mediante una plantilla de inicio rápido de Azure y Hola portal de Azure; y, después, mediante un script de implementación de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba010-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="ba010-127">Opción 1.</span><span class="sxs-lookup"><span data-stu-id="ba010-127">Option 1.</span></span> <span data-ttu-id="ba010-128">Uso de una plantilla de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="ba010-128">Use a quickstart template</span></span>
<span data-ttu-id="ba010-129">Use un tooquickly de plantilla de inicio rápido de Azure implementar un clúster de HPC Pack en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba010-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="ba010-130">Cuando se abre la plantilla de hello en el portal de hello, obtendrá una interfaz de usuario simple donde escribir valores de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="ba010-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="ba010-131">Estos son los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="ba010-132">Si lo desea, use una [plantilla de Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) que crea un clúster similar específicamente para cargas de trabajo de Excel.</span><span class="sxs-lookup"><span data-stu-id="ba010-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="ba010-133">pasos de Hello difieren ligeramente de siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="ba010-134">Visite hello [página de la plantilla de creación de clústeres de HPC en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="ba010-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="ba010-135">Si lo desea, revise la información de plantilla de Hola y código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="ba010-136">Haga clic en **implementar tooAzure** toostart una implementación con plantilla Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba010-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![Implementar la plantilla tooAzure][github]
3. <span data-ttu-id="ba010-138">En el portal de hello, siga estos parámetros de hello tooenter pasos para la plantilla de clúster HPC de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="ba010-139">a.</span><span class="sxs-lookup"><span data-stu-id="ba010-139">a.</span></span> <span data-ttu-id="ba010-140">En hello **parámetros** página, escriba o modifique los valores de parámetros de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="ba010-141">(Haga clic en configuración tooeach Hola icono siguiente para obtener información de ayuda.) Se muestran valores de ejemplo Hola después de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="ba010-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="ba010-142">Este ejemplo crea un clúster denominado *hpc01* en hello *hpc.local* nodos de proceso de dominio que consta de un nodo principal y 2.</span><span class="sxs-lookup"><span data-stu-id="ba010-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="ba010-143">nodos de proceso de Hola se crean a partir de una imagen de máquina virtual de HPC Pack que incluye Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="ba010-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Escribir parámetros][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="ba010-145">nodo principal de Hello máquinas virtuales se crean automáticamente a partir de hello [última imagen de Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) de HPC Pack 2012 R2 en Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="ba010-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="ba010-146">Actualmente la image de Hola se basa en HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="ba010-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="ba010-147">Máquinas virtuales de nodos de cálculo se crean a partir de la imagen más reciente de Hola de familia de nodo de proceso de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="ba010-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="ba010-148">Seleccione hello **ComputeNodeWithExcel** opción para hello más reciente HPC Pack proceso nodo imagen que incluye una versión de evaluación de Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="ba010-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="ba010-149">toodeploy un clúster para las sesiones SOA generales o para la descarga de UDF de Excel, elija hello **ComputeNode** opción (sin Excel instalado).</span><span class="sxs-lookup"><span data-stu-id="ba010-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="ba010-150">b.</span><span class="sxs-lookup"><span data-stu-id="ba010-150">b.</span></span> <span data-ttu-id="ba010-151">Elija la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="ba010-152">c.</span><span class="sxs-lookup"><span data-stu-id="ba010-152">c.</span></span> <span data-ttu-id="ba010-153">Crear un grupo de recursos de clúster de hello, como *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="ba010-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="ba010-154">d.</span><span class="sxs-lookup"><span data-stu-id="ba010-154">d.</span></span> <span data-ttu-id="ba010-155">Elegir una ubicación para el grupo de recursos de hello, como Central US.</span><span class="sxs-lookup"><span data-stu-id="ba010-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="ba010-156">e.</span><span class="sxs-lookup"><span data-stu-id="ba010-156">e.</span></span> <span data-ttu-id="ba010-157">En hello **condiciones legales** página, revise los términos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="ba010-158">Si está de acuerdo, haga clic en **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="ba010-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="ba010-159">A continuación, haga clic en cuando haya terminado de establecer los valores de hello para la plantilla de hello, **crear**.</span><span class="sxs-lookup"><span data-stu-id="ba010-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="ba010-160">Cuando finalice la implementación de hello (normalmente tarda unos 30 minutos), exportar el archivo de certificado de clúster de Hola desde el nodo principal del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="ba010-161">En un paso posterior, importa este certificado público en hello tooprovide Hola servidor autenticación del equipo cliente para el enlace HTTP seguro.</span><span class="sxs-lookup"><span data-stu-id="ba010-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="ba010-162">a.</span><span class="sxs-lookup"><span data-stu-id="ba010-162">a.</span></span> <span data-ttu-id="ba010-163">Hola portal de Azure, vaya toohello panel, nodo principal de hello seleccione y haga clic en **conectar** en parte superior de Hola de hello página tooconnect mediante Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="ba010-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="ba010-164">b.</span><span class="sxs-lookup"><span data-stu-id="ba010-164">b.</span></span> <span data-ttu-id="ba010-165">Utilice los procedimientos estándares de certificado de nodo principal de hello tooexport de administrador de certificados (que se encuentra bajo Cert: \LocalMachine\My) sin clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="ba010-166">En este ejemplo, exporte *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="ba010-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Exportar certificado Hola][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="ba010-168">Opción 2.</span><span class="sxs-lookup"><span data-stu-id="ba010-168">Option 2.</span></span> <span data-ttu-id="ba010-169">Usar script de implementación de IaaS de HPC Pack Hola</span><span class="sxs-lookup"><span data-stu-id="ba010-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="ba010-170">Hola script de implementación de IaaS de HPC Pack proporciona otro toodeploy versátil forma un clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ba010-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="ba010-171">Crea un clúster en el modelo de implementación clásica de hello, mientras que la plantilla Hola utiliza el modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba010-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="ba010-172">Además, el script de Hola es compatible con una suscripción en hello Global de Azure o el servicio de Azure China.</span><span class="sxs-lookup"><span data-stu-id="ba010-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="ba010-173">**Requisitos previos adicionales**</span><span class="sxs-lookup"><span data-stu-id="ba010-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="ba010-174">**Azure PowerShell** - [instale y configure Azure PowerShell](/powershell/azure/overview) (versión 0.8.10 o posterior) en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="ba010-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="ba010-175">**Script de implementación de IaaS de HPC Pack** : Descargue y descomprima la versión más reciente de Hola de script de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="ba010-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="ba010-176">Comprobar la versión de Hola de script de Hola ejecutando `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="ba010-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="ba010-177">En este artículo se basa en la versión 4.5.0 o posterior del script de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="ba010-178">**Crear archivo de configuración de Hola**</span><span class="sxs-lookup"><span data-stu-id="ba010-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="ba010-179">Hola script de implementación de IaaS de HPC Pack utiliza un archivo de configuración XML como entrada que describe la infraestructura de Hola Hola del clúster de HPC.</span><span class="sxs-lookup"><span data-stu-id="ba010-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="ba010-180">toodeploy un clúster que consta de un nodo principal y 18 proceso nodos creados a partir de la imagen del nodo de proceso de Hola que incluye Microsoft Excel, sustituya los valores para el entorno en el siguiente archivo de configuración de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="ba010-181">Para obtener más información sobre el archivo de configuración de hello, consulte el archivo Manual.rtf de hello en la carpeta de script de Hola y [crear un clúster de HPC con hello script de implementación de IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba010-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="ba010-182">**Notas sobre el archivo de configuración de Hola**</span><span class="sxs-lookup"><span data-stu-id="ba010-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="ba010-183">Hola **VMName** del nodo principal de hello **debe** Hola igual como hello **ServiceName**, o toorun producirán errores en trabajos SOA.</span><span class="sxs-lookup"><span data-stu-id="ba010-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="ba010-184">Asegúrese de especificar **EnableWebPortal** para que hello certificado del nodo principal se genera y se exportan.</span><span class="sxs-lookup"><span data-stu-id="ba010-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="ba010-185">archivo Hello especifica un script de PowerShell de configuración posteriores a la PostConfig.ps1 que se ejecuta en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="ba010-186">Hola siguiente secuencia de comandos de ejemplo configura la cadena de conexión de almacenamiento de Azure de hello, quita el rol de nodo de proceso de Hola de nodo principal de Hola y pone todos los nodos en línea cuando se implementan.</span><span class="sxs-lookup"><span data-stu-id="ba010-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="ba010-187">**Ejecutar script de Hola**</span><span class="sxs-lookup"><span data-stu-id="ba010-187">**Run hello script**</span></span>

1. <span data-ttu-id="ba010-188">Abra la consola de PowerShell de hello en el equipo de cliente hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="ba010-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="ba010-189">Cambiar la carpeta de secuencia de comandos de toohello de directorio (E:\IaaSClusterScript en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="ba010-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="ba010-190">clúster de HPC Pack en hello toodeploy, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="ba010-191">En este ejemplo se da por supuesto que se encuentra ese archivo de configuración de hello en E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="ba010-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="ba010-192">Hola script de implementación de HPC Pack se ejecuta durante algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="ba010-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="ba010-193">Un script de Hola lo hace es tooexport y descargar certificado de clúster de Hola y guárdelo en la carpeta documentos del usuario actual de hello en el equipo cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="ba010-194">script de Hola genera un siguiente toohello similar de mensaje.</span><span class="sxs-lookup"><span data-stu-id="ba010-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="ba010-195">En un paso siguiente, importar certificado hello en el almacén de certificados adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="ba010-196">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="ba010-196">Step 2.</span></span> <span data-ttu-id="ba010-197">Descarga de libros de Excel y ejecución de UDF desde un cliente local</span><span class="sxs-lookup"><span data-stu-id="ba010-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="ba010-198">Activación de Excel</span><span class="sxs-lookup"><span data-stu-id="ba010-198">Excel activation</span></span>
<span data-ttu-id="ba010-199">Cuando use Hola imagen ComputeNodeWithExcel VM para cargas de trabajo de producción, debe tooprovide un válido Microsoft Office licencia clave tooactivate Excel en los nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="ba010-200">En caso contrario, versión de evaluación de Hola de Excel expira después de 30 días, y ejecutar libros de Excel se producirá un error con hello COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="ba010-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="ba010-201">Puede rearmar Excel durante otros 30 días del período de evaluación: inicie sesión en el nodo principal de toohello y clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` en Excel todos los nodos mediante el Administrador de clústeres de HPC de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ba010-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="ba010-202">Puede rearmar un máximo de dos veces.</span><span class="sxs-lookup"><span data-stu-id="ba010-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="ba010-203">Después de eso, debe proporcionar una clave de licencia de Office válida.</span><span class="sxs-lookup"><span data-stu-id="ba010-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="ba010-204">Hola Office Professional Plus 2013 instalado en la imagen de máquina virtual de hello es una edición de volumen con una clave de licencia de volumen genérica (GVLK).</span><span class="sxs-lookup"><span data-stu-id="ba010-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="ba010-205">Puede activarla mediante el Servicio de administración de claves (KMS)/activación basada en Active Directory (AD-BA) o la clave de activación múltiple (MAK).</span><span class="sxs-lookup"><span data-stu-id="ba010-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="ba010-206">toouse KMS/AD-BA, use un servidor KMS existente o configurar uno nuevo mediante el uso de hello paquete de licencia de volumen de Microsoft Office 2013.</span><span class="sxs-lookup"><span data-stu-id="ba010-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="ba010-207">(Si desea, configurar servidor de hello en el nodo principal de Hola.) A continuación, activar la clave de host KMS de Hola a través de Internet de Hola o por teléfono.</span><span class="sxs-lookup"><span data-stu-id="ba010-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="ba010-208">A continuación, clusrun `ospp.vbs` tooset Hola servidor KMS y el puerto y activar Office en todos los nodos de cálculo de Excel de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="ba010-209">toouse MAK, primer clusrun `ospp.vbs` tooinput Hola clave y, a continuación, activar todos los nodos de cálculo de Excel de Hola a través de Internet de Hola o por teléfono.</span><span class="sxs-lookup"><span data-stu-id="ba010-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="ba010-210">Las claves de producto comercial de Office Professional Plus 2013 no se pueden usar con esta imagen de VM.</span><span class="sxs-lookup"><span data-stu-id="ba010-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="ba010-211">Si tiene claves y medios de instalación válidos para ediciones de Office o Excel distintas de esta edición por volumen de Office Professional Plus 2013, puede usarlas.</span><span class="sxs-lookup"><span data-stu-id="ba010-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="ba010-212">En primer lugar desinstale esta edición de volumen e instale la edición de Hola que se tenga.</span><span class="sxs-lookup"><span data-stu-id="ba010-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="ba010-213">Hola volver a instalar Excel de nodos de proceso se pueden capturar como un toouse de imagen de máquina virtual personalizada en una implementación a escala.</span><span class="sxs-lookup"><span data-stu-id="ba010-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="ba010-214">Descarga de libros de Excel</span><span class="sxs-lookup"><span data-stu-id="ba010-214">Offload Excel workbooks</span></span>
<span data-ttu-id="ba010-215">Siga estos toooffload pasos un libro de Excel para que se ejecute en el clúster de HPC Pack hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="ba010-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="ba010-216">toodo esto, debe tener Excel 2010 o 2013 ya instalados en el equipo cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="ba010-217">Utilice una de las opciones de hello en un clúster de HPC Pack con hello Excel del paso 1 toodeploy de proceso de imagen del nodo.</span><span class="sxs-lookup"><span data-stu-id="ba010-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="ba010-218">Obtenga el archivo de certificado de clúster de hello (.cer) y nombre de usuario del clúster y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="ba010-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="ba010-219">En el equipo de cliente hello, importe el certificado de clúster de hello en Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="ba010-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="ba010-220">Asegúrese de que Excel está instalado.</span><span class="sxs-lookup"><span data-stu-id="ba010-220">Make sure Excel is installed.</span></span> <span data-ttu-id="ba010-221">Cree un archivo Excel.exe.config con hello siguiente contenido en hello misma carpeta que Excel.exe en el equipo cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="ba010-222">Este paso garantiza que Hola complemento HPC Pack 2012 R2 Excel COM se carga correctamente.</span><span class="sxs-lookup"><span data-stu-id="ba010-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="ba010-223">Configurar el clúster de HPC Pack Hola cliente toosubmit trabajos toohello.</span><span class="sxs-lookup"><span data-stu-id="ba010-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="ba010-224">Una opción es hello toodownload completa [instalación de HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) e instalar el cliente de HPC Pack Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="ba010-225">O bien, descargue e instale hello [utilidades de cliente de HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) y Hola adecuado Visual C++ 2010 redistributable para el equipo ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="ba010-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="ba010-226">En este ejemplo, usamos un libro de Excel de ejemplo denominado ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="ba010-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="ba010-227">Puede descargarlas [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="ba010-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="ba010-228">Copie la carpeta de trabajo de tooa en libro de Excel de hello como D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="ba010-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="ba010-229">Abra el libro de Excel de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-229">Open hello Excel workbook.</span></span> <span data-ttu-id="ba010-230">En hello **desarrollar** la cinta de opciones, haga clic en **complementos COM** y confirme que hello complemento COM de Excel de HPC Pack se cargó correctamente.</span><span class="sxs-lookup"><span data-stu-id="ba010-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Complemento de Excel para HPC Pack][addin]
8. <span data-ttu-id="ba010-232">Macro VBA Hola editar HPCControlMacros en Excel cambiando Hola líneas comentadas tal y como se muestra en la siguiente secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="ba010-233">Sustituya los valores adecuados para su entorno.</span><span class="sxs-lookup"><span data-stu-id="ba010-233">Substitute appropriate values for your environment.</span></span>
   
   ![Macro de Excel para HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="ba010-235">Copie el directorio carga tooan de libro de Excel de hello como D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="ba010-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="ba010-236">Este directorio se especifica en la constante de HPC_DependsFiles de Hola de macro VBA Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="ba010-237">libro de hello toorun en clúster de hello en Azure, haga clic en hello **clúster** botón en la hoja de cálculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="ba010-238">Ejecución de UDF de Excel</span><span class="sxs-lookup"><span data-stu-id="ba010-238">Run Excel UDFs</span></span>
<span data-ttu-id="ba010-239">toorun UDF de Excel, siga Hola pasos anteriores tooset 1-3-el equipo de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="ba010-240">En las UDF de Excel, no es necesario toohave aplicación de Excel hello instalado en nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="ba010-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="ba010-241">Por lo tanto, al crear el clúster de nodos de proceso, puede elegir la imagen de un nodo de proceso normal en lugar de hello calcule la imagen del nodo con Excel.</span><span class="sxs-lookup"><span data-stu-id="ba010-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="ba010-242">Hay un límite de 34 caracteres Hola Excel 2010 y el cuadro de diálogo de conector de clúster de 2013.</span><span class="sxs-lookup"><span data-stu-id="ba010-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="ba010-243">Utilice este clúster de Hola de toospecify de cuadro de diálogo que ejecuta las UDF de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="ba010-244">Si el nombre completo del clúster de hello es mayor (por ejemplo, hpcexcelhn01.southeastasia.cloudapp.azure.com), no cabe en el cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="ba010-245">Hola solución alternativa es tooset una variable de todo el equipo como *CCP_IAASHN* con valor de Hola de nombre de clúster largo Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="ba010-246">A continuación, escriba *CCP_IAASHN %* en cuadro de diálogo de hello como nombre de nodo principal del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="ba010-247">Después de que el clúster de Hola se implementa correctamente, continúe con hello siguiendo los pasos toorun integrada una ejemplo UDF de Excel.</span><span class="sxs-lookup"><span data-stu-id="ba010-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="ba010-248">En las UDF de Excel personalizada, vea estas [recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild Hola XLL e implementarlas en clúster de IaaS de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="ba010-249">Abra un nuevo libro de Excel.</span><span class="sxs-lookup"><span data-stu-id="ba010-249">Open a new Excel workbook.</span></span> <span data-ttu-id="ba010-250">En hello **desarrollar** la cinta de opciones, haga clic en **Add-Ins**. Haga clic en el cuadro de diálogo de hello, **examinar**, desplazarse por las carpetas de %CCP_HOME%Bin\XLL32 toohello y seleccione el ejemplo hello ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="ba010-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="ba010-251">Si hello no existe ClusterUDF32 en el equipo de cliente hello, copiarlo de carpeta de %CCP_HOME%Bin\XLL32 de hello en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Seleccione Hola UDF][udf]
2. <span data-ttu-id="ba010-253">Haga clic en **Archivo** > **Opciones** > **Avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="ba010-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="ba010-254">En **fórmulas**, comprobar **permitir toorun funciones XLL definido por el usuario en un clúster de cálculo**.</span><span class="sxs-lookup"><span data-stu-id="ba010-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="ba010-255">A continuación, haga clic en **opciones** y escriba el nombre completo del clúster de hello en **nombre de nodo principal del clúster**.</span><span class="sxs-lookup"><span data-stu-id="ba010-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="ba010-256">(Como se indicó anteriormente este cuadro de entrada es limitado too34 caracteres, por lo que no puede ajustarse a un nombre de clúster largo.</span><span class="sxs-lookup"><span data-stu-id="ba010-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="ba010-257">Para un nombre de clúster largo, aquí puede usar una variable a nivel de la máquina).</span><span class="sxs-lookup"><span data-stu-id="ba010-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Configurar Hola UDF][options]
3. <span data-ttu-id="ba010-259">Hola toorun cálculo UDF en clúster de hello, haga clic en la celda de hello con valor =XllGetComputerNameC() y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="ba010-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="ba010-260">función Hello simplemente recupera Hola nombre del nodo de proceso de hello en qué Hola UDF se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="ba010-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="ba010-261">Para hello ejecuta por primera vez, un cuadro de diálogo de credenciales solicita Hola username y password tooconnect toohello clúster de IaaS.</span><span class="sxs-lookup"><span data-stu-id="ba010-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![Ejecución de UDF][run]
   
   <span data-ttu-id="ba010-263">Cuando hay muchas toocalculate de celdas, presione Mayús-Alt-Ctrl + cálculo de hello toorun F9 en todas las celdas.</span><span class="sxs-lookup"><span data-stu-id="ba010-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="ba010-264">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="ba010-264">Step 3.</span></span> <span data-ttu-id="ba010-265">Ejecución de una carga de trabajo de SOA desde un cliente local</span><span class="sxs-lookup"><span data-stu-id="ba010-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="ba010-266">toorun aplicaciones generales de SOA en clúster de IaaS de HPC Pack hello, en primer lugar usar uno de los métodos de hello en clúster de Hola de toodeploy de paso 1.</span><span class="sxs-lookup"><span data-stu-id="ba010-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="ba010-267">Especifique la imagen de un nodo de proceso genérico en este caso, dado que no necesitan Excel en los nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="ba010-268">A continuación, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="ba010-268">Then follow these steps.</span></span>

1. <span data-ttu-id="ba010-269">Después de recuperar el certificado de clúster de hello, importarlo en el equipo de cliente de hello en Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="ba010-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="ba010-270">Instalar hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) y [utilidades de cliente de HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="ba010-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="ba010-271">Estas herramientas le permiten toodevelop y ejecutan aplicaciones de cliente SOA.</span><span class="sxs-lookup"><span data-stu-id="ba010-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="ba010-272">Descargar hello HelloWorldR2 [código de ejemplo](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="ba010-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="ba010-273">Abra Hola HelloWorldR2.sln en Visual Studio 2010 o 2012.</span><span class="sxs-lookup"><span data-stu-id="ba010-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="ba010-274">(Este ejemplo no es compatible actualmente con las versiones más recientes de Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="ba010-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="ba010-275">Compile el proyecto de EchoService de hello en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="ba010-275">Build hello EchoService project first.</span></span> <span data-ttu-id="ba010-276">A continuación, implemente el clúster de IaaS de hello servicio toohello Hola se implementan igual tooan local clúster.</span><span class="sxs-lookup"><span data-stu-id="ba010-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="ba010-277">Para obtener instrucciones detalladas, consulte Hola Léame.doc en HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="ba010-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="ba010-278">Modificar y crear hello HellWorldR2 y otros proyectos, como se describe en hello siguiendo la sección toogenerate Hola SOA las aplicaciones cliente que se ejecutan en un clúster de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba010-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="ba010-279">Uso del enlace Http con colas de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ba010-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="ba010-280">enlace Http de toouse con una cola de almacenamiento de Azure, realizar algunos cambios de código de ejemplo de toohello.</span><span class="sxs-lookup"><span data-stu-id="ba010-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="ba010-281">Nombre del clúster de Hola de actualización.</span><span class="sxs-lookup"><span data-stu-id="ba010-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="ba010-282">Opcionalmente, utilice Hola predeterminada TransportScheme SessionStartInfo o establecerlo explícitamente tooHttp.</span><span class="sxs-lookup"><span data-stu-id="ba010-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="ba010-283">Usar enlace predeterminado para hello BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="ba010-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="ba010-284">O establezca explícitamente utilizando basicHttpBinding Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="ba010-285">Opcionalmente, establezca hello UseAzureQueue marca tootrue en SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="ba010-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="ba010-286">Si no se establece, se establecerá tootrue de forma predeterminada cuando el nombre del clúster de hello tiene sufijos de dominio de Azure y hello TransportScheme es Http.</span><span class="sxs-lookup"><span data-stu-id="ba010-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="ba010-287">Uso del enlace Http sin colas de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ba010-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="ba010-288">enlace Http de toouse sin una cola de almacenamiento de Azure, explícitamente conjunto hello UseAzureQueue marca toofalse Hola SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="ba010-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="ba010-289">Uso del enlace NetTcp</span><span class="sxs-lookup"><span data-stu-id="ba010-289">Use NetTcp binding</span></span>
<span data-ttu-id="ba010-290">toouse NetTcp de enlace, configuración de hello es clúster local de similar tooconnecting tooan.</span><span class="sxs-lookup"><span data-stu-id="ba010-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="ba010-291">Debe tooopen unos puntos de conexión en la máquina virtual del nodo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="ba010-292">Si utiliza clústeres de hello IaaS de HPC Pack implementación script toocreate hello, por ejemplo, establecer extremos de hello en Hola portal de Azure como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="ba010-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="ba010-293">Detener Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ba010-293">Stop hello VM.</span></span>
2. <span data-ttu-id="ba010-294">Agregar puertos TCP de hello 9090, 9087, 9091, 9094 para hello sesión, Broker, agente de trabajo y servicios de datos, respectivamente</span><span class="sxs-lookup"><span data-stu-id="ba010-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Configuración de extremos][endpoint-new-portal]
3. <span data-ttu-id="ba010-296">Iniciar VM Hola.</span><span class="sxs-lookup"><span data-stu-id="ba010-296">Start hello VM.</span></span>

<span data-ttu-id="ba010-297">aplicación de cliente SOA de Hello no requiere ningún cambio excepto Modificar Hola principal toohello IaaS clúster: nombre completo.</span><span class="sxs-lookup"><span data-stu-id="ba010-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba010-298">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba010-298">Next steps</span></span>
* <span data-ttu-id="ba010-299">Consulte [estos recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para obtener más información sobre cómo ejecutar las cargas de trabajo de Excel con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ba010-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="ba010-300">Consulte [Administración de servicios de SOA en Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) para obtener más información sobre la implementación y administración de servicios de SOA con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ba010-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
