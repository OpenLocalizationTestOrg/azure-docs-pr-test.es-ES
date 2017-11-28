---
title: "aaaCreate una independiente del clúster con máquinas virtuales de Azure que ejecutan Windows | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y administrar un clúster de Azure Service Fabric en máquinas virtuales de Azure con Windows Server."
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
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="34144-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server (Creación de un clúster independiente de tres nodos de Service Fabric con máquinas virtuales de Azure con Windows Server)</span><span class="sxs-lookup"><span data-stu-id="34144-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="34144-104">Este artículo describe cómo toocreate un clúster en Windows Azure máquinas virtuales (VM), usar Hola instalador independiente de Service Fabric para Windows Server.</span><span class="sxs-lookup"><span data-stu-id="34144-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="34144-105">escenario de Hello es un caso especial de [crear y administrar un clúster que se ejecuta en Windows Server](service-fabric-cluster-creation-for-windows-server.md) donde son máquinas virtuales de hello [máquinas virtuales de Azure que ejecuta Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json); sin embargo, no está creando [un Azure clúster basado en la nube de Service Fabric](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34144-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="34144-106">distinción de Hello en seguir este patrón es ese clúster de Service Fabric Hola independiente creado por hello pasos completamente administrado por usted, mientras que administra y actualizar Hola Service Fabric Hola clústeres de Azure en la nube Service Fabric proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="34144-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="34144-107">Clúster de pasos toocreate Hola independiente</span><span class="sxs-lookup"><span data-stu-id="34144-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="34144-108">Inicie sesión en toohello portal de Azure y cree un nuevo Windows Server 2012 R2 Datacenter o máquina virtual de Windows Server 2016 centro de datos en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="34144-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="34144-109">Leer el artículo de hello [crear una VM de Windows en el portal de Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="34144-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="34144-110">Agregar un par toohello máquinas virtuales más mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="34144-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="34144-111">Asegúrese de que cada una de las máquinas virtuales de hello ha Hola mismo nombre de usuario administrador y la contraseña cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="34144-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="34144-112">Una vez creados, debería ver todas las máquinas tres virtuales Hola misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="34144-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="34144-113">Conectar tooeach de hello las máquinas virtuales y desactivar Hola Firewall de Windows con hello [administrador del servidor, el panel de servidor Local](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="34144-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="34144-114">Esto garantiza que el tráfico de red Hola puede comunicarse entre máquinas Hola.</span><span class="sxs-lookup"><span data-stu-id="34144-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="34144-115">Al equipo tooeach conectado, obtener dirección IP de hello, abra un símbolo del sistema y escriba `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="34144-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="34144-116">También puede ver Hola IP dirección de cada máquina en el portal de hello, seleccionando el recurso de red virtual de hello para el grupo de recursos de Hola y comprobación de interfaces de red de hello creadas para cada una de estas máquinas.</span><span class="sxs-lookup"><span data-stu-id="34144-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="34144-117">Conecte tooone de hello las máquinas virtuales y prueba que puede hacer ping Hola otros dos máquinas virtuales correctamente.</span><span class="sxs-lookup"><span data-stu-id="34144-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="34144-118">Conectar tooone de hello las máquinas virtuales y [Descargar paquete de Service Fabric Hola independiente para Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) en una carpeta nueva en hello automático y extraer el paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="34144-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="34144-119">Abra hello *ClusterConfig.Unsecure.MultiMachine.json* un archivo en el Bloc de notas y editar cada nodo con las direcciones IP de máquinas de Hola Hola tres.</span><span class="sxs-lookup"><span data-stu-id="34144-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="34144-120">Cambiar nombre de clúster de hello en la parte superior de Hola y guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="34144-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="34144-121">A continuación, se muestra un ejemplo parcial Hola del manifiesto de clúster.</span><span class="sxs-lookup"><span data-stu-id="34144-121">A partial example of hello cluster manifest is shown below.</span></span>
   
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
7. <span data-ttu-id="34144-122">Si piensa que este toobe un clúster segura, decidir medida de seguridad de Hola que cabe como toouse y siga los pasos de Hola de hello asociados vínculo: [X509 certificado](service-fabric-windows-cluster-x509-security.md) o [la seguridad de Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="34144-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="34144-123">Si la configuración de clúster de hello mediante la seguridad de Windows, deberá tooset seguridad un toomanage de controlador de dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="34144-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="34144-124">Tenga en cuenta no se admite el uso de una máquina de controlador de dominio como un nodo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="34144-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="34144-125">Abra una [ventana de PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="34144-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="34144-126">Desplazarse por las carpetas de toohello donde extrajo el paquete del instalador independiente descargado hello y había guarda el archivo de configuración del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="34144-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="34144-127">Ejecute hello después de clúster de Hola de toodeploy de comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="34144-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="34144-128">script de Hola configura cada clúster de Service Fabric Hola de manera remota y debe notificar el progreso como implementación pone a través de.</span><span class="sxs-lookup"><span data-stu-id="34144-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="34144-129">Después de aproximadamente un minuto, puede comprobar si el clúster de hello esté operativo conectándose toohello Service Fabric Explorer utilizando uno de la dirección IP de la máquina de hello direcciones, por ejemplo mediante el uso de `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="34144-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="34144-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34144-130">Next steps</span></span>
* [<span data-ttu-id="34144-131">Creación de clústeres independientes de Service Fabric en Windows Server o Linux</span><span class="sxs-lookup"><span data-stu-id="34144-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="34144-132">Agregar o quitar el clúster de Service Fabric de nodos tooa independiente</span><span class="sxs-lookup"><span data-stu-id="34144-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="34144-133">Opciones de configuración de clústeres de Windows independientes</span><span class="sxs-lookup"><span data-stu-id="34144-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="34144-134">Proteger un clúster independiente en Windows mediante la seguridad de Windows</span><span class="sxs-lookup"><span data-stu-id="34144-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="34144-135">Protección de un clúster de Windows independiente mediante certificados</span><span class="sxs-lookup"><span data-stu-id="34144-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

