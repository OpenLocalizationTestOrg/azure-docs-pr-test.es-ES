---
title: "Clúster de HPC Pack para Excel y SOA | Microsoft Docs"
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
ms.openlocfilehash: 63babd94fdab15217cfb0757e4cd6efe458a628d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="55536-103">Introducción a la ejecución de cargas de trabajo de Excel y SOA en un clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="55536-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="55536-104">En este artículo se muestra cómo implementar un clúster de Microsoft HPC Pack 2012 R2 en máquinas virtuales de Azure con una plantilla de inicio rápido de Azure, o bien, de manera opcional, un script de implementación de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55536-104">This article shows you how to deploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="55536-105">El clúster usa imágenes de VM de Azure Marketplace diseñadas para ejecutar cargas de trabajo de Microsoft Excel o de Arquitectura orientada a servicios (SOA) con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="55536-105">The cluster uses Azure Marketplace VM images designed to run Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="55536-106">Puede usar el clúster para ejecutar servicios de SOA y Excel HPC desde un equipo cliente local.</span><span class="sxs-lookup"><span data-stu-id="55536-106">You can use the cluster to run Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="55536-107">Los servicios de Excel HPC incluyen la descarga de libros de Excel y las funciones definidas por el usuario de Excel o UDF.</span><span class="sxs-lookup"><span data-stu-id="55536-107">The Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="55536-108">Este artículo se basa en características, plantillas y scripts de HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="55536-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="55536-109">Este escenario no se admite actualmente en HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="55536-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="55536-110">En un nivel alto, el diagrama siguiente muestra el clúster de HPC Pack que crea.</span><span class="sxs-lookup"><span data-stu-id="55536-110">At a high level, the following diagram shows the HPC Pack cluster you create.</span></span>

![Clúster HPC con nodos que ejecutan cargas de trabajo de Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="55536-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="55536-112">Prerequisites</span></span>
* <span data-ttu-id="55536-113">**Equipo cliente** : necesita un equipo cliente basado en Windows para enviar ejemplos de trabajos de Excel y SOA al clúster.</span><span class="sxs-lookup"><span data-stu-id="55536-113">**Client computer** - You need a Windows-based client computer to submit sample Excel and SOA jobs to the cluster.</span></span> <span data-ttu-id="55536-114">También necesitará un equipo Windows para ejecutar el script de implementación de clúster de Azure PowerShell (si elige ese método de pago).</span><span class="sxs-lookup"><span data-stu-id="55536-114">You also need a Windows computer to run the Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="55536-115">**Suscripción de Azure** : si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/) en un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="55536-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="55536-116">**Cuota de núcleos** : tal vez tenga que aumentar la cuota de núcleos, especialmente si implementa varios nodos de clúster con tamaños de máquina virtual de múltiples núcleos.</span><span class="sxs-lookup"><span data-stu-id="55536-116">**Cores quota** - You might need to increase the quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="55536-117">Si usa una plantilla de inicio rápido de Azure, la cuota de núcleos en Resource Manager es por región de Azure.</span><span class="sxs-lookup"><span data-stu-id="55536-117">If you are using an Azure quickstart template, the cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="55536-118">En ese caso, puede que necesite aumentar la cuota en una región específica.</span><span class="sxs-lookup"><span data-stu-id="55536-118">In that case, you might need to increase the quota in a specific region.</span></span> <span data-ttu-id="55536-119">Consulte [Límites, cuotas y restricciones de suscripción de Azure](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="55536-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="55536-120">Para aumentar una cuota, [abra una solicitud de soporte técnico al cliente en línea](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sin cargo alguno.</span><span class="sxs-lookup"><span data-stu-id="55536-120">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="55536-121">**Licencia de Microsoft Office**: si implementa nodos de proceso con una imagen de máquina virtual de Marketplace HPC Pack 2012 R2 con Microsoft Excel, se instala una versión de evaluación de 30 días de Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="55536-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="55536-122">Después del período de evaluación, debe proporcionar una licencia de Microsoft Office válida para activar Excel y seguir ejecutando cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="55536-122">After the evaluation period, you need to provide a valid Microsoft Office license to activate Excel to continue to run workloads.</span></span> <span data-ttu-id="55536-123">Consulte [Activación de Excel](#excel-activation) que aparece más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="55536-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="55536-124">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="55536-124">Step 1.</span></span> <span data-ttu-id="55536-125">Configuración e un clúster de HPC Pack en Azure</span><span class="sxs-lookup"><span data-stu-id="55536-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="55536-126">Mostramos 2 opciones para configurar el clúster de HPC Pack 2012 R2: primero, con una plantilla de inicio rápido de Azure y Azure Portal, y segundo, con un script de implementación de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55536-126">We show two options to set up the HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and the Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="55536-127">Opción 1.</span><span class="sxs-lookup"><span data-stu-id="55536-127">Option 1.</span></span> <span data-ttu-id="55536-128">Uso de una plantilla de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="55536-128">Use a quickstart template</span></span>
<span data-ttu-id="55536-129">Use una plantilla de inicio rápido de Azure para implementar rápidamente un clúster de HPC Pack en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="55536-129">Use an Azure quickstart template to quickly deploy an HPC Pack cluster in the Azure portal.</span></span> <span data-ttu-id="55536-130">Al abrir la plantilla en el portal, obtendrá una interfaz de usuario simple donde debe especifique la configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="55536-130">When you open the template in the portal, you get a simple UI where you enter the settings for your cluster.</span></span> <span data-ttu-id="55536-131">A continuación se muestran los pasos que se deben seguir.</span><span class="sxs-lookup"><span data-stu-id="55536-131">Here are the steps.</span></span> 

> [!TIP]
> <span data-ttu-id="55536-132">Si lo desea, use una [plantilla de Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) que crea un clúster similar específicamente para cargas de trabajo de Excel.</span><span class="sxs-lookup"><span data-stu-id="55536-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="55536-133">Los pasos son ligeramente distintos a los siguientes.</span><span class="sxs-lookup"><span data-stu-id="55536-133">The steps differ slightly from the following.</span></span>
> 
> 

1. <span data-ttu-id="55536-134">Visite la página [Creación de plantilla de clúster HPC en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="55536-134">Visit the [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="55536-135">Si lo desea, revise la información sobre la plantilla y el código de origen.</span><span class="sxs-lookup"><span data-stu-id="55536-135">If you want, review information about the template and the source code.</span></span>
2. <span data-ttu-id="55536-136">Haga clic en **Implementar en Azure** para iniciar una implementación con la plantilla en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="55536-136">Click **Deploy to Azure** to start a deployment with the template in the Azure portal.</span></span>
   
   ![Implementación de plantillas en Azure][github]
3. <span data-ttu-id="55536-138">En el portal, siga estos pasos para especificar los parámetros de la plantilla de clúster HPC.</span><span class="sxs-lookup"><span data-stu-id="55536-138">In the portal, follow these steps to enter the parameters for the HPC cluster template.</span></span>
   
   <span data-ttu-id="55536-139">a.</span><span class="sxs-lookup"><span data-stu-id="55536-139">a.</span></span> <span data-ttu-id="55536-140">En la página **Parámetros** , escriba o modifique los valores de los parámetros de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="55536-140">On the **Parameters** page, enter or modify values for the template parameters.</span></span> <span data-ttu-id="55536-141">(haga clic en el icono junto a cada valor para obtener información de ayuda). En la pantalla siguiente se muestran valores de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="55536-141">(Click the icon next to each setting for help information.) Sample values are shown in the following screen.</span></span> <span data-ttu-id="55536-142">En este ejemplo se crea un clúster denominado *hpc01* en el dominio *hpc.local* que consta de un nodo principal y 2 nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="55536-142">This example creates a cluster named *hpc01* in the *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="55536-143">Los nodos de proceso se crean a partir de una imagen de VM de HPC Pack que incluye Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="55536-143">The compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Escribir parámetros][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="55536-145">La VM del nodo principal se crea automáticamente a partir de la [imagen de Marketplace más reciente](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) de HPC Pack 2012 R2 en Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="55536-145">The head node VM is created automatically from the [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="55536-146">Actualmente, la imagen se basa en HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="55536-146">Currently the image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="55536-147">Las VM del nodo de proceso se crean a partir de la imagen más reciente de la familia de nodos de proceso seleccionada.</span><span class="sxs-lookup"><span data-stu-id="55536-147">Compute node VMs are created from the latest image of the selected compute node family.</span></span> <span data-ttu-id="55536-148">Seleccione la opción **ComputeNodeWithExcel** para la imagen del nodo de proceso de HPC Pack más reciente que incluye una versión de evaluación de Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="55536-148">Select the **ComputeNodeWithExcel** option for the latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="55536-149">Para implementar un clúster para sesiones generales de SOA o para la descarga de UDF de Excel, elija la opción **ComputeNode** (sin Excel instalado).</span><span class="sxs-lookup"><span data-stu-id="55536-149">To deploy a cluster for general SOA sessions or for Excel UDF offloading, choose the **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="55536-150">b.</span><span class="sxs-lookup"><span data-stu-id="55536-150">b.</span></span> <span data-ttu-id="55536-151">Elija la suscripción.</span><span class="sxs-lookup"><span data-stu-id="55536-151">Choose the subscription.</span></span>
   
   <span data-ttu-id="55536-152">c.</span><span class="sxs-lookup"><span data-stu-id="55536-152">c.</span></span> <span data-ttu-id="55536-153">Cree un grupo de recursos para el clúster, como *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="55536-153">Create a resource group for the cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="55536-154">d.</span><span class="sxs-lookup"><span data-stu-id="55536-154">d.</span></span> <span data-ttu-id="55536-155">Elija una ubicación para el grupo de recursos, como Centro de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="55536-155">Choose a location for the resource group, such as Central US.</span></span>
   
   <span data-ttu-id="55536-156">e.</span><span class="sxs-lookup"><span data-stu-id="55536-156">e.</span></span> <span data-ttu-id="55536-157">En la página **Términos legales** , revise los términos.</span><span class="sxs-lookup"><span data-stu-id="55536-157">On the **Legal terms** page, review the terms.</span></span> <span data-ttu-id="55536-158">Si está de acuerdo, haga clic en **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="55536-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="55536-159">Luego, cuando termine de establecer los valores de la plantilla, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="55536-159">Then, when you are finished setting the values for the template, click **Create**.</span></span>
4. <span data-ttu-id="55536-160">Cuando se completa la implementación (normalmente tarda unos 30 minutos), exporte el archivo de certificado del clúster desde el nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="55536-160">When the deployment completes (it typically takes around 30 minutes), export the cluster certificate file from the cluster head node.</span></span> <span data-ttu-id="55536-161">En un paso posterior, importa este certificado público en el equipo cliente para proporcionar la autenticación del lado servidor para el enlace HTTP seguro.</span><span class="sxs-lookup"><span data-stu-id="55536-161">In a later step, you import this public certificate on the client computer to provide the server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="55536-162">a.</span><span class="sxs-lookup"><span data-stu-id="55536-162">a.</span></span> <span data-ttu-id="55536-163">En Azure Portal, vaya al panel, seleccione el nodo principal y haga clic en **Conectar** en la parte superior de la página para conectarse mediante Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="55536-163">In the Azure portal, go to the dashboard, select the head node, and click **Connect** at the top of the page to connect using Remote Desktop.</span></span>
   
    <!-- ![Connect to the head node][connect] -->
   
   <span data-ttu-id="55536-164">b.</span><span class="sxs-lookup"><span data-stu-id="55536-164">b.</span></span> <span data-ttu-id="55536-165">Siga los procedimientos estándar en Administrador de certificados para exportar el certificado del nodo principal (que se encuentra en Cert:\LocalMachine\My) sin la clave privada.</span><span class="sxs-lookup"><span data-stu-id="55536-165">Use standard procedures in Certificate Manager to export the head node certificate (located under Cert:\LocalMachine\My) without the private key.</span></span> <span data-ttu-id="55536-166">En este ejemplo, exporte *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="55536-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Exportación de certificados][cert]

### <a name="option-2-use-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="55536-168">Opción 2.</span><span class="sxs-lookup"><span data-stu-id="55536-168">Option 2.</span></span> <span data-ttu-id="55536-169">Uso del script de implementación de HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="55536-169">Use the HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="55536-170">El script de implementación de HPC Pack IaaS proporciona otra manera versátil de implementar un clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="55536-170">The HPC Pack IaaS deployment script provides another versatile way to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="55536-171">Crea un clúster en el modelo de implementación clásica, siempre que la plantilla use el modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55536-171">It creates a cluster in the classic deployment model, whereas the template uses the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="55536-172">Además, el script es compatible con una suscripción en el servicio Azure Global o Azure China.</span><span class="sxs-lookup"><span data-stu-id="55536-172">Also, the script is compatible with a subscription in either the Azure Global or Azure China service.</span></span>

<span data-ttu-id="55536-173">**Requisitos previos adicionales**</span><span class="sxs-lookup"><span data-stu-id="55536-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="55536-174">**Azure PowerShell** - [instale y configure Azure PowerShell](/powershell/azure/overview) (versión 0.8.10 o posterior) en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="55536-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="55536-175">**Script de implementación de HPC Pack IaaS** : descargue y desempaquete la versión más reciente del script en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="55536-175">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="55536-176">Compruebe la versión del script ejecutando `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="55536-176">Check the version of the script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="55536-177">Este artículo se basa en la versión 4.5.0 (o posterior) del script.</span><span class="sxs-lookup"><span data-stu-id="55536-177">This article is based on version 4.5.0 or later of the script.</span></span>

<span data-ttu-id="55536-178">**Creación del archivo de configuración**</span><span class="sxs-lookup"><span data-stu-id="55536-178">**Create the configuration file**</span></span>

 <span data-ttu-id="55536-179">El script de implementación de HPC Pack IaaS usa un archivo de configuración XML como entrada que describe la infraestructura del clúster HPC.</span><span class="sxs-lookup"><span data-stu-id="55536-179">The HPC Pack IaaS deployment script uses an XML configuration file as input that describes the infrastructure of the HPC cluster.</span></span> <span data-ttu-id="55536-180">Para implementar un clúster que consta de un nodo principal y 18 nodos de proceso creados a partir de la imagen del nodo de proceso que incluye Microsoft Excel, sustituya los valores para el entorno en el siguiente archivo de configuración de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="55536-180">To deploy a cluster consisting of a head node and 18 compute nodes created from the compute node image that includes Microsoft Excel, substitute values for your environment into the following sample configuration file.</span></span> <span data-ttu-id="55536-181">Para más información sobre el archivo de configuración, vea el archivo Manual.rtf en la carpeta de script y [Creación de un clúster de HPC de Windows con el script de implementación HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55536-181">For more information about the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="55536-182">**Notas sobre el archivo de configuración**</span><span class="sxs-lookup"><span data-stu-id="55536-182">**Notes about the configuration file**</span></span>

* <span data-ttu-id="55536-183">El valor **VMName** del nodo principal **DEBE** ser igual que el valor de **ServiceName** o los trabajos de SOA no se ejecutarán.</span><span class="sxs-lookup"><span data-stu-id="55536-183">The **VMName** of the head node **MUST** be the same as the **ServiceName**, or SOA jobs fail to run.</span></span>
* <span data-ttu-id="55536-184">Asegúrese de especificar **EnableWebPortal** para que se genere y se exporte el certificado del nodo principal.</span><span class="sxs-lookup"><span data-stu-id="55536-184">Make sure you specify **EnableWebPortal** so that the head node certificate is generated and exported.</span></span>
* <span data-ttu-id="55536-185">El archivo especifica un script de PowerShell posterior a la configuración, PostConfig.ps1, que se ejecuta en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="55536-185">The file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on the head node.</span></span> <span data-ttu-id="55536-186">El ejemplo de script siguiente configura la cadena de conexión de Almacenamiento de Azure, quita el rol del nodo de proceso del nodo principal y pone en línea todos los nodos cuando están implementados.</span><span class="sxs-lookup"><span data-stu-id="55536-186">THe following sample script configures the Azure storage connection string, removes the compute node role from the head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add the HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set the Azure storage connection string for the cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove the compute node role for head node to make sure the Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in the deployment including the head node and compute nodes, which should match the number specified in the XML configuration file
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

<span data-ttu-id="55536-187">**Ejecute el script**</span><span class="sxs-lookup"><span data-stu-id="55536-187">**Run the script**</span></span>

1. <span data-ttu-id="55536-188">Abra la consola de PowerShell en el equipo cliente como administrador.</span><span class="sxs-lookup"><span data-stu-id="55536-188">Open the PowerShell console on the client computer as an administrator.</span></span>
2. <span data-ttu-id="55536-189">Cambie el directorio a la carpeta de script (E:\IaaSClusterScript en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="55536-189">Change directory to the script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="55536-190">Ejecute el comando siguiente para implementar el clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="55536-190">To deploy the HPC Pack cluster, run the following command.</span></span> <span data-ttu-id="55536-191">En este ejemplo se supone que el archivo de configuración se encuentra en E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="55536-191">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="55536-192">El script de implementación de HPC Pack se ejecuta durante algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="55536-192">The HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="55536-193">Una de las cosas que hace el script es exportar y descargar el certificado del clúster y guardarlo en la carpeta Documentos del usuario actual en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="55536-193">One thing the script does is to export and download the cluster certificate and save it in the current user’s Documents folder on the client computer.</span></span> <span data-ttu-id="55536-194">El script genera un mensaje similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="55536-194">The script generates a message similar to the following.</span></span> <span data-ttu-id="55536-195">En un paso posterior, importa el certificado en el almacén de certificados adecuado.</span><span class="sxs-lookup"><span data-stu-id="55536-195">In a following step, you import the certificate in the appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import the following certificate in the Trusted Root Certification Authorities certificate store on the computer where you are submitting job or accessing the HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="55536-196">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="55536-196">Step 2.</span></span> <span data-ttu-id="55536-197">Descarga de libros de Excel y ejecución de UDF desde un cliente local</span><span class="sxs-lookup"><span data-stu-id="55536-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="55536-198">Activación de Excel</span><span class="sxs-lookup"><span data-stu-id="55536-198">Excel activation</span></span>
<span data-ttu-id="55536-199">Cuando usa la imagen de VM ComputeNodeWithExcel para las cargas de trabajo de producción, debe brindar una clave de licencia de Microsoft Office válida para activar Excel en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="55536-199">When using the ComputeNodeWithExcel VM image for production workloads, you need to provide a valid Microsoft Office license key to activate Excel on the compute nodes.</span></span> <span data-ttu-id="55536-200">De lo contrario, la versión de evaluación de Excel expirará después 30 días y la ejecución de libros de Excel presentará errores con la excepción COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="55536-200">Otherwise, the evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with the COMException (0x800AC472).</span></span> 

<span data-ttu-id="55536-201">Puede rearmar Excel para otro período de evaluación de 30 días: inicie sesión en el nodo principal y ejecute `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` en todos los nodos de proceso de Excel a través del Administración de clústeres de HPC.</span><span class="sxs-lookup"><span data-stu-id="55536-201">You can rearm Excel for another 30 days of evaluation time: Log on to the head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="55536-202">Puede rearmar un máximo de dos veces.</span><span class="sxs-lookup"><span data-stu-id="55536-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="55536-203">Después de eso, debe proporcionar una clave de licencia de Office válida.</span><span class="sxs-lookup"><span data-stu-id="55536-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="55536-204">La versión de Office Professional Plus 2013 instalada en la imagen de la VM es una edición por volumen con una clave de licencia por volumen genérica (GVLK).</span><span class="sxs-lookup"><span data-stu-id="55536-204">The Office Professional Plus 2013 installed on the VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="55536-205">Puede activarla mediante el Servicio de administración de claves (KMS)/activación basada en Active Directory (AD-BA) o la clave de activación múltiple (MAK).</span><span class="sxs-lookup"><span data-stu-id="55536-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="55536-206">Para usar KMS/AD-BA, emplee un servidor de KMS existente o configure uno nuevo mediante el paquete de licencias por volumen de Microsoft Office 2013.</span><span class="sxs-lookup"><span data-stu-id="55536-206">To use KMS/AD-BA, use an existing KMS server or set up a new one by using the Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="55536-207">(Si lo desea, configure el servidor en el nodo principal). Luego, active la clave de host de KMS a través de Internet o por teléfono.</span><span class="sxs-lookup"><span data-stu-id="55536-207">(If you want to, set up the server on the head node.) Then, activate the KMS host key via the Internet or telephone.</span></span> <span data-ttu-id="55536-208">Luego, ejecute `ospp.vbs` para definir el puerto y el servidor de KMS y activar Office en todos los nodos de proceso de Excel.</span><span class="sxs-lookup"><span data-stu-id="55536-208">Then clusrun `ospp.vbs` to set the KMS server and port and activate Office on all the Excel compute nodes.</span></span> 

    * <span data-ttu-id="55536-209">Para usar MAK, primero ejecute `ospp.vbs` para insertar la clave y, luego, active todos los nodos de proceso de Excel a través de Internet o por teléfono.</span><span class="sxs-lookup"><span data-stu-id="55536-209">To use MAK, first clusrun `ospp.vbs` to input the key and then activate all the Excel compute nodes via the Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="55536-210">Las claves de producto comercial de Office Professional Plus 2013 no se pueden usar con esta imagen de VM.</span><span class="sxs-lookup"><span data-stu-id="55536-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="55536-211">Si tiene claves y medios de instalación válidos para ediciones de Office o Excel distintas de esta edición por volumen de Office Professional Plus 2013, puede usarlas.</span><span class="sxs-lookup"><span data-stu-id="55536-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="55536-212">En primer lugar, desinstale esta edición por volumen e instale la edición que tiene.</span><span class="sxs-lookup"><span data-stu-id="55536-212">First uninstall this volume edition and install the edition that you have.</span></span> <span data-ttu-id="55536-213">De ese modo, el nodo de proceso de Excel reinstalado se puede capturar como imagen de VM personalizada para así usarlo en una implementación a escala.</span><span class="sxs-lookup"><span data-stu-id="55536-213">The reinstalled Excel compute node can be captured as a customized VM image to use in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="55536-214">Descarga de libros de Excel</span><span class="sxs-lookup"><span data-stu-id="55536-214">Offload Excel workbooks</span></span>
<span data-ttu-id="55536-215">Siga estos pasos para descargar un libro de Excel para que se ejecute en el clúster de HPC Pack en Azure.</span><span class="sxs-lookup"><span data-stu-id="55536-215">Follow these steps to offload an Excel workbook so that it runs on the HPC Pack cluster in Azure.</span></span> <span data-ttu-id="55536-216">Para ello, debe tener Excel 2010 o 2013 ya instalado en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="55536-216">To do this, you must have Excel 2010 or 2013 already installed on the client computer.</span></span>

1. <span data-ttu-id="55536-217">Use una de las opciones descritas en el paso 1 para implementar un clúster de HPC Pack con la imagen del nodo de proceso de Excel.</span><span class="sxs-lookup"><span data-stu-id="55536-217">Use one of the options in Step 1 to deploy an HPC Pack cluster with the Excel compute node image.</span></span> <span data-ttu-id="55536-218">Obtenga el archivo de certificado del clúster (.cer) y el nombre de usuario y la contraseña del clúster.</span><span class="sxs-lookup"><span data-stu-id="55536-218">Obtain the cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="55536-219">En el equipo cliente, importe el certificado del clúster que se encuentra en Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="55536-219">On the client computer, import the cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="55536-220">Asegúrese de que Excel está instalado.</span><span class="sxs-lookup"><span data-stu-id="55536-220">Make sure Excel is installed.</span></span> <span data-ttu-id="55536-221">Cree un archivo Excel.exe.config con el siguiente contenido en la misma carpeta que Excel.exe en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="55536-221">Create an Excel.exe.config file with the following contents in the same folder as Excel.exe on the client computer.</span></span> <span data-ttu-id="55536-222">Este paso garantiza que el complemento HPC Pack 2012 R2 Excel COM se cargue correctamente.</span><span class="sxs-lookup"><span data-stu-id="55536-222">This step ensures that the HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="55536-223">Configure el cliente para enviar trabajos al clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="55536-223">Set up the client to submit jobs to the HPC Pack cluster.</span></span> <span data-ttu-id="55536-224">Una opción es descargar la [instalación completa de HPC Pack 2012 R2 actualización 3](http://www.microsoft.com/download/details.aspx?id=49922) e instale el cliente de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="55536-224">One option is to download the full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install the HPC Pack client.</span></span> <span data-ttu-id="55536-225">De manera alternativa, descargue e instale las [utilidades de cliente de HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) y el paquete redistribuible de Visual C++ 2010 adecuado para su equipo ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="55536-225">Alternatively, download and install the [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and the appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="55536-226">En este ejemplo, usamos un libro de Excel de ejemplo denominado ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="55536-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="55536-227">Puede descargarlas [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="55536-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="55536-228">Copie el libro de Excel en una carpeta de trabajo como D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="55536-228">Copy the Excel workbook to a working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="55536-229">Abra el libro de Excel.</span><span class="sxs-lookup"><span data-stu-id="55536-229">Open the Excel workbook.</span></span> <span data-ttu-id="55536-230">En la cinta **Desarrollar**, haga clic en **Complementos COM** y confirme que el complemento COM de HPC Pack Excel se cargó correctamente.</span><span class="sxs-lookup"><span data-stu-id="55536-230">On the **Develop** ribbon, click **COM Add-Ins** and confirm that the HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Complemento de Excel para HPC Pack][addin]
8. <span data-ttu-id="55536-232">Modifique la macro HPCControlMacros de VBA en Excel cambiando las líneas comentadas, como se muestra en el script siguiente.</span><span class="sxs-lookup"><span data-stu-id="55536-232">Edit the VBA macro HPCControlMacros in Excel by changing the commented lines as shown in the following script.</span></span> <span data-ttu-id="55536-233">Sustituya los valores adecuados para su entorno.</span><span class="sxs-lookup"><span data-stu-id="55536-233">Substitute appropriate values for your environment.</span></span>
   
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
9. <span data-ttu-id="55536-235">Copie el libro de Excel para en un directorio de carga, como D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="55536-235">Copy the Excel workbook to an upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="55536-236">Este directorio se especifica en la constante HPC_DependsFiles de la macro de VBA.</span><span class="sxs-lookup"><span data-stu-id="55536-236">This directory is specified in the HPC_DependsFiles constant in the VBA macro.</span></span>
10. <span data-ttu-id="55536-237">Para ejecutar el libro en el clúster en Azure, haga clic en el botón **Clúster** que aparece en la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="55536-237">To run the workbook on the cluster in Azure, click the **Cluster** button on the worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="55536-238">Ejecución de UDF de Excel</span><span class="sxs-lookup"><span data-stu-id="55536-238">Run Excel UDFs</span></span>
<span data-ttu-id="55536-239">Para ejecutar UDF de Excel, siga los pasos de 1 a 3 anteriores para configurar el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="55536-239">To run Excel UDFs, follow the preceding steps 1 – 3 to set up the client computer.</span></span> <span data-ttu-id="55536-240">En el caso de los UDF de Excel, no necesita tener instalada la aplicación de Excel en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="55536-240">For Excel UDFs, you don't need to have the Excel application installed on compute nodes.</span></span> <span data-ttu-id="55536-241">Por lo tanto, cuando crea los nodos de proceso del clúster, puede elegir una imagen de nodo de proceso normal en lugar de la imagen de nodo de proceso con Excel.</span><span class="sxs-lookup"><span data-stu-id="55536-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of the compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="55536-242">Hay un límite de 34 caracteres en el cuadro de diálogo del conector de clúster de Excel 2010 y 2013.</span><span class="sxs-lookup"><span data-stu-id="55536-242">There is a 34 character limit in the Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="55536-243">Este cuadro de diálogo se usa para especificar el clúster que ejecuta los UDF.</span><span class="sxs-lookup"><span data-stu-id="55536-243">You use this dialog box to specify the cluster that runs the UDFs.</span></span> <span data-ttu-id="55536-244">Si el nombre completo del clúster es más largo (por ejemplo, hpcexcelhn01.southeastasia.cloudapp.azure.com), no cabe en el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55536-244">If the full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in the dialog box.</span></span> <span data-ttu-id="55536-245">La solución alternativa es establecer una variable a nivel de máquina, como *CCP_IAASHN*, con el valor del nombre largo del clúster.</span><span class="sxs-lookup"><span data-stu-id="55536-245">The workaround is to set a machine-wide variable such as *CCP_IAASHN* with the value of the long cluster name.</span></span> <span data-ttu-id="55536-246">Luego, escriba *%CCP_IAASHN%* en el cuadro de diálogo como el nombre del nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="55536-246">Then, enter *%CCP_IAASHN%* in the dialog box as the cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="55536-247">Una vez que el clúster esté implementado correctamente, siga estos pasos para ejecutar una UDF de Excel integrada de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="55536-247">After the cluster is successfully deployed, continue with the following steps to run a sample built-in Excel UDF.</span></span> <span data-ttu-id="55536-248">Para UDF personalizadas de Excel, consulte los [recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para compilar las funciones XLL e implementarlas en el clúster de IaaS.</span><span class="sxs-lookup"><span data-stu-id="55536-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) to build the XLLs and deploy them on the IaaS cluster.</span></span>

1. <span data-ttu-id="55536-249">Abra un nuevo libro de Excel.</span><span class="sxs-lookup"><span data-stu-id="55536-249">Open a new Excel workbook.</span></span> <span data-ttu-id="55536-250">En la cinta **Desarrollar**, haga clic en **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="55536-250">On the **Develop** ribbon, click **Add-Ins**.</span></span> <span data-ttu-id="55536-251">En el cuadro de diálogo, haga clic en **Examinar**, vaya a la carpeta %CCP_HOME%Bin\XLL32 y seleccione el archivo ClusterUDF32.xll de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="55536-251">Then, in the dialog box, click **Browse**, navigate to the %CCP_HOME%Bin\XLL32 folder, and select the sample ClusterUDF32.xll.</span></span> <span data-ttu-id="55536-252">Si ClusterUDF32 no existe en el equipo cliente, cópielo de la carpeta %CCP_HOME%Bin\XLL32 en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="55536-252">If the ClusterUDF32 doesn't exist on the client machine, copy it from the %CCP_HOME%Bin\XLL32 folder on the head node.</span></span>
   
   ![Selección de UDF][udf]
2. <span data-ttu-id="55536-254">Haga clic en **Archivo** > **Opciones** > **Avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="55536-254">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="55536-255">En **Fórmulas**, active **Allow user-defined XLL functions to run a compute cluster** (Permitir ejecución de funciones XLL definidas por el usuario en un clúster de proceso).</span><span class="sxs-lookup"><span data-stu-id="55536-255">Under **Formulas**, check **Allow user-defined XLL functions to run a compute cluster**.</span></span> <span data-ttu-id="55536-256">A continuación, haga clic en **Opciones** y escriba el nombre completo del clúster en **Cluster head node name** (Nombre del nodo principal del clúster).</span><span class="sxs-lookup"><span data-stu-id="55536-256">Then click **Options** and enter the full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="55536-257">(Como se indicó anteriormente, este cuadro de entrada está limitado a 34 caracteres, por lo que un nombre de clúster largo no cabrá.</span><span class="sxs-lookup"><span data-stu-id="55536-257">(As noted previously this input box is limited to 34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="55536-258">Para un nombre de clúster largo, aquí puede usar una variable a nivel de la máquina).</span><span class="sxs-lookup"><span data-stu-id="55536-258">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Configuración de UDF][options]
3. <span data-ttu-id="55536-260">Para ejecutar el cálculo de UDF en el clúster, haga clic en la celda con el valor =XllGetComputerNameC() y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="55536-260">To run the UDF calculation on the cluster, click the cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="55536-261">La función simplemente recupera el nombre del nodo de proceso en el que se ejecuta el UDF.</span><span class="sxs-lookup"><span data-stu-id="55536-261">The function simply retrieves the name of the compute node on which the UDF runs.</span></span> <span data-ttu-id="55536-262">Para la primera ejecución, un cuadro de diálogo de credenciales solicita el nombre de usuario y la contraseña para conectarse al clúster de IaaS.</span><span class="sxs-lookup"><span data-stu-id="55536-262">For the first run, a credentials dialog box prompts for the username and password to connect to the IaaS cluster.</span></span>
   
   ![Ejecución de UDF][run]
   
   <span data-ttu-id="55536-264">Cuando haya una gran cantidad de celdas para calcular, presione Alt+Mayús+Ctrl+F9 para ejecutar el cálculo en todas las celdas.</span><span class="sxs-lookup"><span data-stu-id="55536-264">When there are many cells to calculate, press Alt-Shift-Ctrl + F9 to run the calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="55536-265">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="55536-265">Step 3.</span></span> <span data-ttu-id="55536-266">Ejecución de una carga de trabajo de SOA desde un cliente local</span><span class="sxs-lookup"><span data-stu-id="55536-266">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="55536-267">Para ejecutar aplicaciones generales de SOA en el clúster de HPC Pack IaaS, use primero uno de los métodos que aparecen en el paso 1 para implementar el clúster.</span><span class="sxs-lookup"><span data-stu-id="55536-267">To run general SOA applications on the HPC Pack IaaS cluster, first use one of the methods in Step 1 to deploy the cluster.</span></span> <span data-ttu-id="55536-268">En este caso, especifique una imagen de nodo de proceso genérica porque no necesita tener instalado Excel en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="55536-268">Specify a generic compute node image in this case, because you do not need Excel on the compute nodes.</span></span> <span data-ttu-id="55536-269">A continuación, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="55536-269">Then follow these steps.</span></span>

1. <span data-ttu-id="55536-270">Después de recuperar el certificado del clúster, impórtelo en el equipo cliente en Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="55536-270">After retrieving the cluster certificate, import it on the client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="55536-271">Instale el [SDK de HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49921) y las utilidades de cliente de [HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="55536-271">Install the [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="55536-272">Estas herramientas le permiten desarrollar y ejecutar aplicaciones cliente de SOA.</span><span class="sxs-lookup"><span data-stu-id="55536-272">These tools enable you to develop and run SOA client applications.</span></span>
3. <span data-ttu-id="55536-273">Descargue el [código de ejemplo](https://www.microsoft.com/download/details.aspx?id=41633)de HelloWorldR2.</span><span class="sxs-lookup"><span data-stu-id="55536-273">Download the HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="55536-274">Abra HelloWorldR2.sln en Visual Studio 2010 o 2012.</span><span class="sxs-lookup"><span data-stu-id="55536-274">Open the HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="55536-275">(Este ejemplo no es compatible actualmente con las versiones más recientes de Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="55536-275">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="55536-276">Primero compile el proyecto EchoService.</span><span class="sxs-lookup"><span data-stu-id="55536-276">Build the EchoService project first.</span></span> <span data-ttu-id="55536-277">Luego, implemente el servicio en el clúster de IaaS de la misma manera que se implementa en un clúster local.</span><span class="sxs-lookup"><span data-stu-id="55536-277">Then, deploy the service to the IaaS cluster in the same way you deploy to an on-premises cluster.</span></span> <span data-ttu-id="55536-278">Para obtener pasos detallados, consulte el archivo Léame.doc en HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="55536-278">For detailed steps, see the Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="55536-279">Modifique y compile HelloWorldR2 y otros proyectos tal como se describe en la sección siguiente para generar las aplicaciones cliente de SOA que se ejecutan en un clúster de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="55536-279">Modify and build the HellWorldR2 and other projects as described in the following section to generate the SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="55536-280">Uso del enlace Http con colas de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="55536-280">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="55536-281">Para usar el enlace Http con una cola de almacenamiento de Azure, haga algunos cambios en el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="55536-281">To use Http binding with an Azure storage queue, make a few changes to the sample code.</span></span>

* <span data-ttu-id="55536-282">Actualice el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="55536-282">Update the cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="55536-283">O bien, use el valor TransportScheme predeterminado en SessionStartInfo o establézcalo explícitamente en Http.</span><span class="sxs-lookup"><span data-stu-id="55536-283">Optionally, use the default TransportScheme in SessionStartInfo or explicitly set it to Http.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="55536-284">Use el enlace predeterminado para BrokerClient</span><span class="sxs-lookup"><span data-stu-id="55536-284">Use default binding for the BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="55536-285">o establézcalo explícitamente con basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="55536-285">Or set explicitly using the basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="55536-286">De manera opcional, puede establecer la marca UseAzureQueue en true en SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="55536-286">Optionally, set the UseAzureQueue flag to true in SessionStartInfo.</span></span> <span data-ttu-id="55536-287">Si no se establece, se establecerá en true de forma predeterminada cuando el nombre del clúster tenga sufijos de dominio de Azure y el valor de TransportScheme sea Http.</span><span class="sxs-lookup"><span data-stu-id="55536-287">If not set, it will be set to true by default when the cluster name has Azure domain suffixes and the TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="55536-288">Uso del enlace Http sin colas de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="55536-288">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="55536-289">Para usar el enlace Http sin una cola de Almacenamiento de Azure, establezca de manera explícita la marca UseAzureQueue en false en SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="55536-289">To use Http binding without an Azure storage queue, explicitly set the UseAzureQueue flag to false in the SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="55536-290">Uso del enlace NetTcp</span><span class="sxs-lookup"><span data-stu-id="55536-290">Use NetTcp binding</span></span>
<span data-ttu-id="55536-291">Para usar el enlace NetTcp, la configuración es similar que al conectarse a un clúster local.</span><span class="sxs-lookup"><span data-stu-id="55536-291">To use NetTcp binding, the configuration is similar to connecting to an on-premises cluster.</span></span> <span data-ttu-id="55536-292">Debe abrir algunos puntos de conexión en la VM del nodo principal.</span><span class="sxs-lookup"><span data-stu-id="55536-292">You need to open a few endpoints on the head node VM.</span></span> <span data-ttu-id="55536-293">Por ejemplo, si usó el script de implementación de HPC Pack IaaS para crear el clúster, establezca los puntos de conexión en Azure Portal como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="55536-293">If you used the HPC Pack IaaS deployment script to create the cluster, for example, set the endpoints in the Azure portal as follows.</span></span>

1. <span data-ttu-id="55536-294">Pare la VM.</span><span class="sxs-lookup"><span data-stu-id="55536-294">Stop the VM.</span></span>
2. <span data-ttu-id="55536-295">Agregue los puertos TCP 9090, 9087, 9091, 9094 para Sesión, Agente, Trabajo de agente y Servicios de datos, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="55536-295">Add the TCP ports 9090, 9087, 9091, 9094 for the Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Configuración de extremos][endpoint-new-portal]
3. <span data-ttu-id="55536-297">Inicie la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="55536-297">Start the VM.</span></span>

<span data-ttu-id="55536-298">La aplicación cliente de SOA no requiere cambios excepto modificar el nombre principal por el nombre completo del clúster de IaaS.</span><span class="sxs-lookup"><span data-stu-id="55536-298">The SOA client application requires no changes except altering the head name to the IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55536-299">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="55536-299">Next steps</span></span>
* <span data-ttu-id="55536-300">Consulte [estos recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para obtener más información sobre cómo ejecutar las cargas de trabajo de Excel con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="55536-300">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="55536-301">Consulte [Administración de servicios de SOA en Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) para obtener más información sobre la implementación y administración de servicios de SOA con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="55536-301">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

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
