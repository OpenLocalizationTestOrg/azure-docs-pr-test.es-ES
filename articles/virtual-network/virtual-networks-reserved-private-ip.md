---
title: "aaaStatic interna privada clásico IP - VM de Azure:"
description: "Descripción de direcciones IP internas (DIP) estática y cómo toomanage ellos"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="4005e-103">¿Cómo tooset una dirección IP estática de privada interna trata acerca del uso de PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="4005e-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="4005e-104">En la mayoría de los casos, no tendrá toospecify una dirección IP interna estática para su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4005e-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="4005e-105">Las máquinas virtuales de una red virtual recibirán automáticamente una dirección IP interna dentro de un intervalo que especifique.</span><span class="sxs-lookup"><span data-stu-id="4005e-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="4005e-106">Pero en algunos casos, tiene sentido especificar una dirección IP estática para una máquina virtual concreta.</span><span class="sxs-lookup"><span data-stu-id="4005e-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="4005e-107">Por ejemplo, si la máquina virtual es continuo toorun DNS o será un controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="4005e-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="4005e-108">Una dirección IP interna estática permanece con hello VM incluso a través de un estado de detención o desaprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="4005e-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4005e-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4005e-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4005e-110">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="4005e-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="4005e-111">Microsoft recomienda que las implementaciones de la mayoría de los nuevos usen hello [modelo de implementación del Administrador de recursos](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4005e-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="4005e-112">¿Cómo tooverify si hay una dirección IP específica</span><span class="sxs-lookup"><span data-stu-id="4005e-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="4005e-113">tooverify si hello dirección IP *10.0.0.7* está disponible en una red virtual denominada *TestVnet*, ejecute el siguiente comando de PowerShell de Hola y comprobar el valor de Hola para *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="4005e-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="4005e-114">Si desea que el comando de hello tootest anteriormente en un entorno seguro siga directrices de hello en [crear una red virtual (clásica)](virtual-networks-create-vnet-classic-pportal.md) toocreate una red virtual denominada *TestVnet* y asegurarse de que utiliza hello  *10.0.0.0/8* espacio de direcciones.</span><span class="sxs-lookup"><span data-stu-id="4005e-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="4005e-115">¿Cómo toospecify una dirección IP interna estática al crear una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4005e-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="4005e-116">Hola script de PowerShell siguiente crea un nuevo servicio de nube denominado *TestService*, a continuación, recupera una imagen de Azure, a continuación, crea una máquina virtual denominada *TestVM* en hello nuevo servicio en la nube con imagen Hola recuperar, conjuntos de Hola toobe de máquina virtual en una subred denominada *Subnet-1*y establece *10.0.0.7* como una dirección IP interna estática para hello VM:</span><span class="sxs-lookup"><span data-stu-id="4005e-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="4005e-117">¿Cómo tooretrieve interno información de IP estática para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4005e-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="4005e-118">tooview Hola estático interno IP información acerca de hello máquinas virtuales crean con script de Hola anterior, ejecute el siguiente comando de PowerShell de Hola y observar los valores de hello para *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="4005e-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="4005e-119">¿Cómo tooremove una dirección IP interna estática de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4005e-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="4005e-120">tooremove Hola dirección IP interna estática agregó toohello VM en el script de Hola anterior, ejecute hello siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4005e-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="4005e-121">¿Cómo tooadd un tooan IP interna estática VM existente</span><span class="sxs-lookup"><span data-stu-id="4005e-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="4005e-122">tooadd un toohello IP interna estática máquinas virtuales creadas con script de Hola anteriormente, ejecución el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4005e-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="4005e-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4005e-123">Next steps</span></span>
[<span data-ttu-id="4005e-124">IP reservada</span><span class="sxs-lookup"><span data-stu-id="4005e-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="4005e-125">IP pública a nivel de instancia (ILIP)</span><span class="sxs-lookup"><span data-stu-id="4005e-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="4005e-126">API de REST de IP reservada</span><span class="sxs-lookup"><span data-stu-id="4005e-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

