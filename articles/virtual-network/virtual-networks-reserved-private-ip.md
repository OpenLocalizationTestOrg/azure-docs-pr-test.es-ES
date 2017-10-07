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
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>¿Cómo tooset una dirección IP estática de privada interna trata acerca del uso de PowerShell (clásico)
En la mayoría de los casos, no tendrá toospecify una dirección IP interna estática para su máquina virtual. Las máquinas virtuales de una red virtual recibirán automáticamente una dirección IP interna dentro de un intervalo que especifique. Pero en algunos casos, tiene sentido especificar una dirección IP estática para una máquina virtual concreta. Por ejemplo, si la máquina virtual es continuo toorun DNS o será un controlador de dominio. Una dirección IP interna estática permanece con hello VM incluso a través de un estado de detención o desaprovisionamiento. 

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que las implementaciones de la mayoría de los nuevos usen hello [modelo de implementación del Administrador de recursos](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>¿Cómo tooverify si hay una dirección IP específica
tooverify si hello dirección IP *10.0.0.7* está disponible en una red virtual denominada *TestVnet*, ejecute el siguiente comando de PowerShell de Hola y comprobar el valor de Hola para *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Si desea que el comando de hello tootest anteriormente en un entorno seguro siga directrices de hello en [crear una red virtual (clásica)](virtual-networks-create-vnet-classic-pportal.md) toocreate una red virtual denominada *TestVnet* y asegurarse de que utiliza hello  *10.0.0.0/8* espacio de direcciones.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>¿Cómo toospecify una dirección IP interna estática al crear una máquina virtual
Hola script de PowerShell siguiente crea un nuevo servicio de nube denominado *TestService*, a continuación, recupera una imagen de Azure, a continuación, crea una máquina virtual denominada *TestVM* en hello nuevo servicio en la nube con imagen Hola recuperar, conjuntos de Hola toobe de máquina virtual en una subred denominada *Subnet-1*y establece *10.0.0.7* como una dirección IP interna estática para hello VM:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>¿Cómo tooretrieve interno información de IP estática para una máquina virtual
tooview Hola estático interno IP información acerca de hello máquinas virtuales crean con script de Hola anterior, ejecute el siguiente comando de PowerShell de Hola y observar los valores de hello para *IpAddress*:

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

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>¿Cómo tooremove una dirección IP interna estática de una máquina virtual
tooremove Hola dirección IP interna estática agregó toohello VM en el script de Hola anterior, ejecute hello siguiente comando de PowerShell:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>¿Cómo tooadd un tooan IP interna estática VM existente
tooadd un toohello IP interna estática máquinas virtuales creadas con script de Hola anteriormente, ejecución el siguiente comando:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Pasos siguientes
[IP reservada](virtual-networks-reserved-public-ip.md)

[IP pública a nivel de instancia (ILIP)](virtual-networks-instance-level-public-ip.md)

[API de REST de IP reservada](https://msdn.microsoft.com/library/azure/dn722420.aspx)

