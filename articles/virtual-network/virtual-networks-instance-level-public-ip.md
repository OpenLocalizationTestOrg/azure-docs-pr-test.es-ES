---
title: "las direcciones IP públicas (clásico) aaaAzure nivel de instancia | Documentos de Microsoft"
description: "Comprender las direcciones IP (ILPIP) de públicas nivel de instancia y cómo toomanage mediante PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="80dca-103">Introducción a las direcciones IP públicas a nivel de instancia (clásica)</span><span class="sxs-lookup"><span data-stu-id="80dca-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="80dca-104">Una instancia IP pública nivel (ILPIP) es una dirección IP pública que se puede asignar directamente instancia de rol de máquina virtual o servicios en la nube tooa, en lugar del servicio de nube de toohello que la máquina virtual o instancia de rol residen en.</span><span class="sxs-lookup"><span data-stu-id="80dca-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly tooa VM or Cloud Services role instance, rather than toohello cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="80dca-105">Un ILPIP no tiene lugar de Hola de hello dirección IP virtual (VIP) que se asigna el servicio en la nube tooyour.</span><span class="sxs-lookup"><span data-stu-id="80dca-105">An ILPIP doesn’t take hello place of hello virtual IP (VIP) that is assigned tooyour cloud service.</span></span> <span data-ttu-id="80dca-106">En su lugar, es una dirección IP adicional que puede usar tooconnect directamente tooyour máquina virtual o instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="80dca-106">Rather, it’s an additional IP address that you can use tooconnect directly tooyour VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80dca-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80dca-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="80dca-108">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="80dca-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="80dca-109">Microsoft recomienda crear máquinas virtuales a través de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="80dca-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="80dca-110">Asegúrese de que comprende cómo funcionan las [direcciones IP](virtual-network-ip-addresses-overview-classic.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="80dca-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Diferencia entre ILPIP y VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="80dca-112">Como se muestra en la figura 1, se tiene acceso al servicio de nube de hello mediante una VIP, mientras Hola máquinas virtuales individuales son accesibles normalmente mediante la VIP:&lt;número de puerto&gt;.</span><span class="sxs-lookup"><span data-stu-id="80dca-112">As shown in Figure 1, hello cloud service is accessed using a VIP, while hello individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="80dca-113">Asignando un tooa ILPIP VM específica, que pueden ser máquinas virtuales acceso directamente mediante esa dirección IP.</span><span class="sxs-lookup"><span data-stu-id="80dca-113">By assigning an ILPIP tooa specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="80dca-114">Cuando se crea un servicio de nube en Azure, registros DNS A correspondientes se crean automáticamente servicio de toohello de tooallow acceso a través de un nombre de dominio completo (FQDN), en lugar de usar Hola real VIP.</span><span class="sxs-lookup"><span data-stu-id="80dca-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically tooallow access toohello service through a fully qualified domain name (FQDN), instead of using hello actual VIP.</span></span> <span data-ttu-id="80dca-115">Hola mismo proceso se produce para un ILPIP, lo que permite acceso toohello máquina virtual o instancia de rol mediante el FQDN en lugar de hello ILPIP.</span><span class="sxs-lookup"><span data-stu-id="80dca-115">hello same process happens for an ILPIP, allowing access toohello VM or role instance by FQDN instead of hello ILPIP.</span></span> <span data-ttu-id="80dca-116">Por ejemplo, si crea un servicio de nube denominado *contosoadservice*, y configurar un rol web denominado *contosoweb* con dos instancias, hello Azure registros siguientes A registros para instancias de hello:</span><span class="sxs-lookup"><span data-stu-id="80dca-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers hello following A records for hello instances:</span></span>

* <span data-ttu-id="80dca-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="80dca-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="80dca-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="80dca-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="80dca-119">Solo puede asignar una ILPIP para cada máquina virtual o instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="80dca-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="80dca-120">Puede usar la too5 ILPIPs por suscripción.</span><span class="sxs-lookup"><span data-stu-id="80dca-120">You can use up too5 ILPIPs per subscription.</span></span> <span data-ttu-id="80dca-121">Las ILPIP no se admiten para las máquinas virtuales de varias NIC.</span><span class="sxs-lookup"><span data-stu-id="80dca-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="80dca-122">¿Por qué debo solicitar una ILPIP?</span><span class="sxs-lookup"><span data-stu-id="80dca-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="80dca-123">Si desea toobe tooconnect pueda tooyour máquina virtual o instancia de rol mediante una dirección IP asignada directamente tooit, en lugar de usar en la nube Hola VIP del servicio:&lt;número de puerto&gt;, solicitar una ILPIP para la máquina virtual o la instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="80dca-123">If you want toobe able tooconnect tooyour VM or role instance by an IP address assigned directly tooit, rather than using hello cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="80dca-124">**FTP activo** -mediante la asignación de una máquina virtual de ILPIP tooa, puede recibir tráfico en cualquier puerto.</span><span class="sxs-lookup"><span data-stu-id="80dca-124">**Active FTP** - By assigning an ILPIP tooa VM, it can receive traffic on any port.</span></span> <span data-ttu-id="80dca-125">Los puntos de conexión no son necesarias para hello tráfico tooreceive de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80dca-125">Endpoints are not required for hello VM tooreceive traffic.</span></span>  <span data-ttu-id="80dca-126">Para obtener más información sobre el protocolo de hello FTP, vea (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [Introducción al protocolo de FTP].</span><span class="sxs-lookup"><span data-stu-id="80dca-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on hello FTP protocol.</span></span>
* <span data-ttu-id="80dca-127">**IP de salida** : el tráfico saliente que se origina en hello máquina virtual está asignada toohello ILPIP como origen de Hola y Hola ILPIP identifica de forma única entidades de hello VM tooexternal.</span><span class="sxs-lookup"><span data-stu-id="80dca-127">**Outbound IP** - Outbound traffic originating from hello VM is mapped toohello ILPIP as hello source and hello ILPIP uniquely identifies hello VM tooexternal entities.</span></span>

> [!NOTE]
> <span data-ttu-id="80dca-128">Hola anterior, una dirección ILPIP fue tooas que se hace referencia una dirección IP (PIP) pública.</span><span class="sxs-lookup"><span data-stu-id="80dca-128">In hello past, an ILPIP address was referred tooas a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="80dca-129">Administración de una ILPIP para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="80dca-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="80dca-130">Hola siguiente las tareas le permiten toocreate, asignar y quitar ILPIPs desde máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="80dca-130">hello following tasks enable you toocreate, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="80dca-131">¿Cómo toorequest un ILPIP durante la creación de máquinas virtuales con PowerShell</span><span class="sxs-lookup"><span data-stu-id="80dca-131">How toorequest an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="80dca-132">Hola siguiente script de PowerShell crea un servicio de nube denominado *FTPService*, recupera una imagen de Azure, crea una máquina virtual denominada *FTPInstance* con imagen Hola recuperar, Establece Hola VM toouse un ILPIP y agrega el nuevo servicio de hello VM toohello:</span><span class="sxs-lookup"><span data-stu-id="80dca-132">hello following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using hello retrieved image, sets hello VM toouse an ILPIP, and adds hello VM toohello new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="80dca-133">Cómo obtener información de ILPIP tooretrieve para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="80dca-133">How tooretrieve ILPIP information for a VM</span></span>
<span data-ttu-id="80dca-134">Hola tooview ILPIP conocer Hola máquinas virtuales crean con script anterior de hello, ejecute el siguiente comando de PowerShell de Hola y observar los valores de hello para *PublicIPAddress* y *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="80dca-134">tooview hello ILPIP information for hello VM created with hello previous script, run hello following PowerShell command and observe hello values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="80dca-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="80dca-135">Expected output:</span></span>
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a><span data-ttu-id="80dca-136">¿Cómo tooremove una ILPIP de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="80dca-136">How tooremove an ILPIP from a VM</span></span>
<span data-ttu-id="80dca-137">Hola tooremove ILPIP agregado toohello VM en hello secuencia de comandos anterior, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="80dca-137">tooremove hello ILPIP added toohello VM in hello previous script, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a><span data-ttu-id="80dca-138">¿Cómo tooadd una tooan ILPIP máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="80dca-138">How tooadd an ILPIP tooan existing VM</span></span>
<span data-ttu-id="80dca-139">tooadd una toohello ILPIP máquinas virtuales creadas con script de Hola anterior, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="80dca-139">tooadd an ILPIP toohello VM created using hello script previous, run hello following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="80dca-140">Administración de una ILPIP para una instancia de rol de Cloud Services</span><span class="sxs-lookup"><span data-stu-id="80dca-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="80dca-141">tooadd una instancia de rol de servicios en la nube de tooa ILPIP, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="80dca-141">tooadd an ILPIP tooa Cloud Services role instance, complete hello following steps:</span></span>

1. <span data-ttu-id="80dca-142">Descargar archivo de .cscfg de Hola para servicio de nube Hola siguiendo Hola los pasos de hello [cómo los servicios de nube tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artículo.</span><span class="sxs-lookup"><span data-stu-id="80dca-142">Download hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="80dca-143">Archivo de .cscfg Hola de actualización mediante la adición de hello `InstanceAddress` elemento.</span><span class="sxs-lookup"><span data-stu-id="80dca-143">Update hello .cscfg file by adding hello `InstanceAddress` element.</span></span> <span data-ttu-id="80dca-144">Hello en el ejemplo siguiente agrega un ILPIP denominado *MyPublicIP* tooa instancia de rol denominado *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="80dca-144">hello following sample adds an ILPIP named *MyPublicIP* tooa role instance named *WebRole1*:</span></span> 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. <span data-ttu-id="80dca-145">Cargar archivo de .cscfg de Hola para servicio de nube Hola siguiendo Hola los pasos de hello [cómo los servicios de nube tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artículo.</span><span class="sxs-lookup"><span data-stu-id="80dca-145">Upload hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80dca-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80dca-146">Next steps</span></span>
* <span data-ttu-id="80dca-147">Comprender cómo [el direccionamiento IP](virtual-network-ip-addresses-overview-classic.md) funciona en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="80dca-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="80dca-148">Obtenga información sobre las [direcciones IP reservadas](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="80dca-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
