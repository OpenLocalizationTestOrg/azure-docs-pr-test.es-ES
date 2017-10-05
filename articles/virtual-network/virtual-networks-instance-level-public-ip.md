---
title: "Direcciones IP públicas a nivel de instancia (clásica) de Azure mediante | Microsoft Docs"
description: "Comprenda las direcciones públicas de nivel de instancia (ILPIP) y cómo administrarlas con PowerShell."
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
ms.openlocfilehash: 773043f2841ec7539b0d49357dec6bcb9f4f78a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="efcad-103">Introducción a las direcciones IP públicas a nivel de instancia (clásica)</span><span class="sxs-lookup"><span data-stu-id="efcad-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="efcad-104">Una IP pública de nivel de instancia (ILPIP) es una dirección IP pública que se puede asignar directamente a la máquina virtual o a la instancia de rol de Cloud Services, en lugar de a un servicio en la nube en el que reside la máquina virtual o la instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="efcad-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly to a VM or Cloud Services role instance, rather than to the cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="efcad-105">Un ILPIP no reemplaza a la dirección IP virtual (VIP) que está asignada al servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="efcad-105">An ILPIP doesn’t take the place of the virtual IP (VIP) that is assigned to your cloud service.</span></span> <span data-ttu-id="efcad-106">Es más bien una dirección IP adicional que puede usar para conectarse directamente a la máquina virtual o instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="efcad-106">Rather, it’s an additional IP address that you can use to connect directly to your VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efcad-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efcad-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="efcad-108">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="efcad-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="efcad-109">Microsoft recomienda crear máquinas virtuales a través de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="efcad-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="efcad-110">Asegúrese de que comprende cómo funcionan las [direcciones IP](virtual-network-ip-addresses-overview-classic.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="efcad-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Diferencia entre ILPIP y VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="efcad-112">Como se muestra en la Figura 1, se accede al servicio en la nube mediante una VIP, mientras que normalmente se accede a las máquinas virtuales individuales mediante VIP:&lt;número de puerto&gt;.</span><span class="sxs-lookup"><span data-stu-id="efcad-112">As shown in Figure 1, the cloud service is accessed using a VIP, while the individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="efcad-113">Al asignar una ILPIP a una máquina virtual específica, se puede tener acceso directamente a esa máquina virtual mediante esa dirección IP.</span><span class="sxs-lookup"><span data-stu-id="efcad-113">By assigning an ILPIP to a specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="efcad-114">Cuando se crea un servicio en la nube en Azure, los registros de DNS A correspondientes se crean automáticamente para permitir el acceso al servicio mediante un nombre de dominio completo (FQDN) en lugar de usar la VIP real.</span><span class="sxs-lookup"><span data-stu-id="efcad-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically to allow access to the service through a fully qualified domain name (FQDN), instead of using the actual VIP.</span></span> <span data-ttu-id="efcad-115">Se produce el mismo proceso para la ILPIP, lo que permite el acceso a la máquina virtual o instancia de rol mediante el FQDN en lugar de la ILPIP.</span><span class="sxs-lookup"><span data-stu-id="efcad-115">The same process happens for an ILPIP, allowing access to the VM or role instance by FQDN instead of the ILPIP.</span></span> <span data-ttu-id="efcad-116">Por ejemplo, si crea un servicio en la nube denominado *contosoadservice* y configura un rol web denominado *contosoweb* con dos instancias, Azure registra los siguientes registros A para las instancias:</span><span class="sxs-lookup"><span data-stu-id="efcad-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers the following A records for the instances:</span></span>

* <span data-ttu-id="efcad-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="efcad-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="efcad-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="efcad-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="efcad-119">Solo puede asignar una ILPIP para cada máquina virtual o instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="efcad-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="efcad-120">Puede usar hasta 5 ILPIP por suscripción.</span><span class="sxs-lookup"><span data-stu-id="efcad-120">You can use up to 5 ILPIPs per subscription.</span></span> <span data-ttu-id="efcad-121">Las ILPIP no se admiten para las máquinas virtuales de varias NIC.</span><span class="sxs-lookup"><span data-stu-id="efcad-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="efcad-122">¿Por qué debo solicitar una ILPIP?</span><span class="sxs-lookup"><span data-stu-id="efcad-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="efcad-123">Si desea poder conectarse a la máquina virtual o a la instancia de rol mediante una dirección IP asignada directamente a ella, en lugar de usar la VIP:&lt;número de puerto&gt; del servicio en la nube, solicite una ILPIP para la máquina virtual o la instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="efcad-123">If you want to be able to connect to your VM or role instance by an IP address assigned directly to it, rather than using the cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="efcad-124">**FTP activo**: mediante la asignación de una ILPIP a una máquina virtual, puede recibir tráfico en cualquier puerto.</span><span class="sxs-lookup"><span data-stu-id="efcad-124">**Active FTP** - By assigning an ILPIP to a VM, it can receive traffic on any port.</span></span> <span data-ttu-id="efcad-125">Los puntos de conexión no son necesarios para que la máquina virtual reciba tráfico.</span><span class="sxs-lookup"><span data-stu-id="efcad-125">Endpoints are not required for the VM to receive traffic.</span></span>  <span data-ttu-id="efcad-126">Consulte la información general que se da en (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] sobre el protocolo FTP para conocer los detalles sobre este último.</span><span class="sxs-lookup"><span data-stu-id="efcad-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on the FTP protocol.</span></span>
* <span data-ttu-id="efcad-127">**IP de salida**: el tráfico de salida procedente de la máquina virtual se asigna a la ILPIP como origen y, de esta forma, esta última identifica de forma exclusiva la máquina virtual ante entidades externas.</span><span class="sxs-lookup"><span data-stu-id="efcad-127">**Outbound IP** - Outbound traffic originating from the VM is mapped to the ILPIP as the source and the ILPIP uniquely identifies the VM to external entities.</span></span>

> [!NOTE]
> <span data-ttu-id="efcad-128">Antes, a la dirección ILPIP se le conocía como dirección IP pública (PIP).</span><span class="sxs-lookup"><span data-stu-id="efcad-128">In the past, an ILPIP address was referred to as a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="efcad-129">Administración de una ILPIP para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="efcad-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="efcad-130">Las tareas siguientes le permiten crear, asignar y quitar ILPIP de máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="efcad-130">The following tasks enable you to create, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-to-request-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="efcad-131">Solicitud de una ILPIP durante la creación de máquinas virtuales mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="efcad-131">How to request an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="efcad-132">El script de PowerShell siguiente crea un servicio en la nube denominado *FTPService*, recupera una imagen de Azure, crea una máquina virtual denominada *FTPInstance* usando la imagen recuperada, establece la máquina virtual para que use una ILPIP y agrega la máquina virtual al nuevo servicio:</span><span class="sxs-lookup"><span data-stu-id="efcad-132">The following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using the retrieved image, sets the VM to use an ILPIP, and adds the VM to the new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-to-retrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="efcad-133">Recuperación de información de ILPIP para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="efcad-133">How to retrieve ILPIP information for a VM</span></span>
<span data-ttu-id="efcad-134">Para ver la información de ILPIP para la máquina virtual creada con el script anterior, ejecute el siguiente comando de PowerShell y observe los valores de *PublicIPAddress* y *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="efcad-134">To view the ILPIP information for the VM created with the previous script, run the following PowerShell command and observe the values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="efcad-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="efcad-135">Expected output:</span></span>
 
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

### <a name="how-to-remove-an-ilpip-from-a-vm"></a><span data-ttu-id="efcad-136">Supresión de una ILPIP de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="efcad-136">How to remove an ILPIP from a VM</span></span>
<span data-ttu-id="efcad-137">Para quitar la ILPIP agregada a la máquina virtual en el script anterior, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="efcad-137">To remove the ILPIP added to the VM in the previous script, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-to-add-an-ilpip-to-an-existing-vm"></a><span data-ttu-id="efcad-138">Agregación de una ILPIP a una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="efcad-138">How to add an ILPIP to an existing VM</span></span>
<span data-ttu-id="efcad-139">Para agregar una ILPIP a la máquina virtual creada con el script anterior, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="efcad-139">To add an ILPIP to the VM created using the script previous, run the following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="efcad-140">Administración de una ILPIP para una instancia de rol de Cloud Services</span><span class="sxs-lookup"><span data-stu-id="efcad-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="efcad-141">Para agregar una ILPIP a una instancia de rol de Cloud Services, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="efcad-141">To add an ILPIP to a Cloud Services role instance, complete the following steps:</span></span>

1. <span data-ttu-id="efcad-142">Descargue el archivo .cscfg para el servicio en la nube siguiendo los pasos descritos en el artículo sobre [cómo configurar Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg).</span><span class="sxs-lookup"><span data-stu-id="efcad-142">Download the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="efcad-143">Actualice el archivo .cscfg y agregue el elemento `InstanceAddress`.</span><span class="sxs-lookup"><span data-stu-id="efcad-143">Update the .cscfg file by adding the `InstanceAddress` element.</span></span> <span data-ttu-id="efcad-144">El ejemplo siguiente agrega una ILPIP denominada *MyPublicIP* a una instancia de rol denominada *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="efcad-144">The following sample adds an ILPIP named *MyPublicIP* to a role instance named *WebRole1*:</span></span> 

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
3. <span data-ttu-id="efcad-145">Cargue el archivo .cscfg para el servicio en la nube siguiendo los pasos descritos en el artículo sobre [cómo configurar Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg).</span><span class="sxs-lookup"><span data-stu-id="efcad-145">Upload the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efcad-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="efcad-146">Next steps</span></span>
* <span data-ttu-id="efcad-147">Descubra cómo funcionan las [direcciones IP](virtual-network-ip-addresses-overview-classic.md) en el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="efcad-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="efcad-148">Obtenga información sobre las [direcciones IP reservadas](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="efcad-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
