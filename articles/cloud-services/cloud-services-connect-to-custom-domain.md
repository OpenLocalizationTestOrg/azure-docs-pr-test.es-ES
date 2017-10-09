---
title: un servicio en la nube tooa aaaConnect controlador de dominio personalizado | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect roles web o de trabajo tooa personalizado del dominio de Active Directory con PowerShell y extensión de dominio de AD"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="37ff6-103">Conexión personalizada de las funciones de servicios de nube de Azure tooa controlador de dominio de Active Directory hospedado en Azure</span><span class="sxs-lookup"><span data-stu-id="37ff6-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="37ff6-104">En primer lugar, vamos a configurar una red virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="37ff6-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="37ff6-105">A continuación, agregaremos una red virtual de controlador de dominio de Active Directory (hospedado en una máquina Virtual de Azure) toohello.</span><span class="sxs-lookup"><span data-stu-id="37ff6-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="37ff6-106">A continuación, se le agregar toohello de roles de servicio de nube existente creado previamente la red virtual y conectarlos toohello controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="37ff6-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="37ff6-107">Antes de empezar, par de cosas tookeep en cuenta:</span><span class="sxs-lookup"><span data-stu-id="37ff6-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="37ff6-108">Este tutorial usa PowerShell, así que asegúrese de tener PowerShell de Azure instalado y está listo toogo.</span><span class="sxs-lookup"><span data-stu-id="37ff6-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="37ff6-109">tooget ayuda a configurar Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="37ff6-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="37ff6-110">Las instancias del controlador de dominio de Active Directory y el rol de trabajo o Web necesitan toobe Hola red virtual.</span><span class="sxs-lookup"><span data-stu-id="37ff6-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="37ff6-111">Siga a esta guía paso a paso y si surge algún problema, nos deja un comentario al final de hello del artículo Hola.</span><span class="sxs-lookup"><span data-stu-id="37ff6-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="37ff6-112">Le llamaremos tooyou (Sí, se leen los comentarios).</span><span class="sxs-lookup"><span data-stu-id="37ff6-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="37ff6-113">Hola red al que hace referencia el servicio de nube Hola debe ser un **red virtual clásica**.</span><span class="sxs-lookup"><span data-stu-id="37ff6-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="37ff6-114">Creación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="37ff6-114">Create a Virtual Network</span></span>
<span data-ttu-id="37ff6-115">Puede crear una red Virtual en Azure mediante el portal de Azure de Hola o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37ff6-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="37ff6-116">En este tutorial, usaremos PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37ff6-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="37ff6-117">toocreate una red Virtual con hello Azure portal, vea [crear red Virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="37ff6-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="37ff6-118">Creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="37ff6-118">Create a Virtual Machine</span></span>
<span data-ttu-id="37ff6-119">Una vez haya completado la configuración de red Virtual de hello, deberá toocreate un controlador de dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37ff6-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="37ff6-120">En este tutorial, se va a configurar un controlador de dominio de AD en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="37ff6-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="37ff6-121">toodo, crear una máquina virtual a través de PowerShell con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="37ff6-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="37ff6-122">Promover el controlador de dominio de máquina Virtual tooa</span><span class="sxs-lookup"><span data-stu-id="37ff6-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="37ff6-123">Hola tooconfigure Máquina Virtual como un controlador de dominio de AD, necesitará toolog en toohello VM y configurarlo.</span><span class="sxs-lookup"><span data-stu-id="37ff6-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="37ff6-124">toolog en toohello VM, puede obtener el archivo RDP de hello a través de PowerShell, Hola de uso después de comandos:</span><span class="sxs-lookup"><span data-stu-id="37ff6-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="37ff6-125">Una vez que haya iniciado sesión toohello máquina virtual, configurar la máquina Virtual como un controlador de dominio de AD mediante la siguiente guía paso a paso de hello en [cómo tooset el controlador de dominio de AD del cliente](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="37ff6-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="37ff6-126">Agregar la red Virtual de toohello de servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="37ff6-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="37ff6-127">A continuación, debe tooadd su toohello de implementación del servicio de nube nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="37ff6-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="37ff6-128">toodo, modificar el servicio de nube cscfg agregando Hola secciones relevantes tooyour cscfg con Visual Studio u Hola editor de su elección.</span><span class="sxs-lookup"><span data-stu-id="37ff6-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

<span data-ttu-id="37ff6-129">A continuación, compilar el proyecto de servicios de nube e implementarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="37ff6-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="37ff6-130">tooget ayuda con la implementación de su tooAzure de paquete de servicios de nube, vea [cómo tooCreate e implementar un servicio de nube](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="37ff6-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="37ff6-131">Conectar su dominio de toohello de roles de web y de trabajo</span><span class="sxs-lookup"><span data-stu-id="37ff6-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="37ff6-132">Una vez que se implementa el proyecto de servicio de nube en Azure, conectar su dominio de toohello AD personalizado de instancias de rol mediante Hola extensión de dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37ff6-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="37ff6-133">Hola tooadd implementación de servicios de dominio de Active Directory extensión tooyour existente en la nube y unirse al dominio personalizado de hello, ejecute hello siga los comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37ff6-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="37ff6-134">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="37ff6-134">And that's it.</span></span>

<span data-ttu-id="37ff6-135">Servicios en la nube deben ser tooyour Unidos a un controlador de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="37ff6-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="37ff6-136">Si desea que toolearn más información acerca de Hola distintas opciones disponibles para cómo ayudar tooconfigure extensión de dominio de Active Directory, use Hola PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37ff6-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="37ff6-137">A continuación verá un par de ejemplos:</span><span class="sxs-lookup"><span data-stu-id="37ff6-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
