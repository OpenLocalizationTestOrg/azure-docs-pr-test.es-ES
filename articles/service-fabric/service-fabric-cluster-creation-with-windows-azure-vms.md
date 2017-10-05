---
title: "Creación de un clúster independiente con VM de Azure con Windows | Microsoft Docs"
description: "Obtenga información sobre cómo crear y administrar un clúster de Azure Service Fabric en máquinas virtuales de Azure con Windows Server."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: f8a0305a22c00f9bdbdb1bdb06dc299cccee23dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="d729d-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server (Creación de un clúster independiente de tres nodos de Service Fabric con máquinas virtuales de Azure con Windows Server)</span><span class="sxs-lookup"><span data-stu-id="d729d-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="d729d-104">En este artículo se describe cómo crear un clúster en máquinas virtuales de Azure basadas en Windows con el instalador independiente de Service Fabric para Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d729d-104">This article describes how to create a cluster on Windows-based Azure virtual machines (VMs), using the standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="d729d-105">Este escenario es un caso especial de [Creación y administración de un clúster que se ejecute en Windows Server](service-fabric-cluster-creation-for-windows-server.md), donde las máquinas virtuales son [máquinas virtuales de Azure que ejecutan Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), pero no creará [un clúster de Service Fabric basado en la nube de Azure](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d729d-105">The scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where the VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="d729d-106">La distinción al seguir este patrón es que usted administra completamente el clúster independiente de Service Fabric que se crea con los pasos siguientes, mientras que es el proveedor de recursos de Service Fabric quien administra y actualiza los clústeres de Service Fabric basados en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="d729d-106">The distinction in following this pattern is that the standalone Service Fabric cluster created by the following steps is entirely managed by you, whereas the Azure cloud-based Service Fabric clusters are managed and upgraded by the Service Fabric resource provider.</span></span>

## <a name="steps-to-create-the-standalone-cluster"></a><span data-ttu-id="d729d-107">Pasos para crear el clúster independiente</span><span class="sxs-lookup"><span data-stu-id="d729d-107">Steps to create the standalone cluster</span></span>
1. <span data-ttu-id="d729d-108">Inicie sesión en Azure Portal y cree una máquina virtual de Windows Server 2012 R2 Datacenter o Windows Server 2016 Datacenter en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d729d-108">Sign in to the Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="d729d-109">Para más información, vea el artículo [Crear una VM de Windows en Azure Portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d729d-109">Read the article [Create a Windows VM in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="d729d-110">Agregue un par de máquinas virtuales más al mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d729d-110">Add a couple more VMs to the same resource group.</span></span> <span data-ttu-id="d729d-111">Asegúrese de que cada una ellas tenga el mismo nombre de usuario administrador y contraseña que cuando se creó.</span><span class="sxs-lookup"><span data-stu-id="d729d-111">Ensure that each of the VMs has the same administrator user name and password when created.</span></span> <span data-ttu-id="d729d-112">Una vez creada, verá las tres máquinas virtuales en la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="d729d-112">Once created you should see all three VMs in the same virtual network.</span></span>
3. <span data-ttu-id="d729d-113">Conéctese a cada una de ellas y desactive el Firewall de Windows mediante el [Administrador del servidor, panel Servidor local](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="d729d-113">Connect to each of the VMs and turn off the Windows Firewall using the [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="d729d-114">Esto garantiza que el tráfico de red pueda comunicarse entre las máquinas.</span><span class="sxs-lookup"><span data-stu-id="d729d-114">This ensures that the network traffic can communicate between the machines.</span></span> <span data-ttu-id="d729d-115">Mientras esté conectado a cada máquina, abra un símbolo del sistema y escriba `ipconfig`para obtener la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="d729d-115">While connected to each machine, get the IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="d729d-116">También puede ver la dirección IP de cada equipo del portal seleccionando el recurso de red virtual del grupo de recursos y comprobando las interfaces de red creadas para cada una de estas máquinas.</span><span class="sxs-lookup"><span data-stu-id="d729d-116">Alternatively you can see the IP address of each machine on the portal, by selecting the virtual network resource for the resource group and checking the network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="d729d-117">Conéctese a una de las VM y pruebe si puede hacer ping correctamente a las otras dos.</span><span class="sxs-lookup"><span data-stu-id="d729d-117">Connect to one of the VMs and test that you can ping the other two VMs successfully.</span></span>
5. <span data-ttu-id="d729d-118">Conéctese a una de las VM, [descargue el paquete de Service Fabric independiente para Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) a una carpeta nueva en la máquina y extráigalo.</span><span class="sxs-lookup"><span data-stu-id="d729d-118">Connect to one of the VMs and [download the standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on the machine and extract the package.</span></span>
6. <span data-ttu-id="d729d-119">Abra el archivo *ClusterConfig.Unsecure.MultiMachine.json* en el Bloc de notas y edite cada nodo con las tres direcciones IP de las máquinas.</span><span class="sxs-lookup"><span data-stu-id="d729d-119">Open the *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with the three IP addresses of the machines.</span></span> <span data-ttu-id="d729d-120">Cambie el nombre del clúster en la parte superior y guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="d729d-120">Change the cluster name at the top and save the file.</span></span>  <span data-ttu-id="d729d-121">A continuación, se puede ver un ejemplo parcial del manifiesto de clúster.</span><span class="sxs-lookup"><span data-stu-id="d729d-121">A partial example of the cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="d729d-122">Si piensa que va a ser un clúster seguro, decida la medida de seguridad que le gustaría usar y siga los pasos descritos en el vínculo asociado: [Certificado X509](service-fabric-windows-cluster-x509-security.md) o [Seguridad de Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="d729d-122">If you intend this to be a secure cluster, decide the security measure you would like to use and follow the steps at the associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="d729d-123">Si desea configurar el clúster con la seguridad de Windows, debe configurar un controlador de dominio para administrar Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d729d-123">If setting up the cluster using Windows Security, you will need to set up a domain controller to manage Active Directory.</span></span> <span data-ttu-id="d729d-124">Tenga en cuenta no se admite el uso de una máquina de controlador de dominio como un nodo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d729d-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="d729d-125">Abra una [ventana de PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="d729d-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="d729d-126">Vaya a la carpeta donde extrajo el paquete del instalador independiente que descargó y donde guardó el archivo de configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="d729d-126">Navigate to the folder where you extracted the downloaded standalone installer package and saved the cluster configuration file.</span></span> <span data-ttu-id="d729d-127">Ejecute el comando de PowerShell siguiente para implementar el clúster:</span><span class="sxs-lookup"><span data-stu-id="d729d-127">Run the following PowerShell command to deploy the cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="d729d-128">El script va a configurar de manera remota el clúster de Service Fabric y debe notificar el progreso a medida que se desarrolla la implementación.</span><span class="sxs-lookup"><span data-stu-id="d729d-128">The script will remotely configure the Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="d729d-129">Después de aproximadamente un minuto, puede comprobar si el clúster está operativo. Para ello, conéctese a Service Fabric Explorer con una de las direcciones IP de la máquina, como `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="d729d-129">After about a minute, you can check if the cluster is operational by connecting to the Service Fabric Explorer using one of the machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d729d-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d729d-130">Next steps</span></span>
* [<span data-ttu-id="d729d-131">Creación de clústeres independientes de Service Fabric en Windows Server o Linux</span><span class="sxs-lookup"><span data-stu-id="d729d-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="d729d-132">Incorporación o eliminación de nodos de un clúster de Service Fabric independiente</span><span class="sxs-lookup"><span data-stu-id="d729d-132">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="d729d-133">Opciones de configuración de clústeres de Windows independientes</span><span class="sxs-lookup"><span data-stu-id="d729d-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="d729d-134">Proteger un clúster independiente en Windows mediante la seguridad de Windows</span><span class="sxs-lookup"><span data-stu-id="d729d-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="d729d-135">Protección de un clúster de Windows independiente mediante certificados</span><span class="sxs-lookup"><span data-stu-id="d729d-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

