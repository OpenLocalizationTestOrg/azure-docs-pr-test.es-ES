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
# <a name="instance-level-public-ip-classic-overview"></a>Introducción a las direcciones IP públicas a nivel de instancia (clásica)
Una instancia IP pública nivel (ILPIP) es una dirección IP pública que se puede asignar directamente instancia de rol de máquina virtual o servicios en la nube tooa, en lugar del servicio de nube de toohello que la máquina virtual o instancia de rol residen en. Un ILPIP no tiene lugar de Hola de hello dirección IP virtual (VIP) que se asigna el servicio en la nube tooyour. En su lugar, es una dirección IP adicional que puede usar tooconnect directamente tooyour máquina virtual o instancia de rol.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda crear máquinas virtuales a través de Resource Manager. Asegúrese de que comprende cómo funcionan las [direcciones IP](virtual-network-ip-addresses-overview-classic.md) en Azure.

![Diferencia entre ILPIP y VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

Como se muestra en la figura 1, se tiene acceso al servicio de nube de hello mediante una VIP, mientras Hola máquinas virtuales individuales son accesibles normalmente mediante la VIP:&lt;número de puerto&gt;. Asignando un tooa ILPIP VM específica, que pueden ser máquinas virtuales acceso directamente mediante esa dirección IP.

Cuando se crea un servicio de nube en Azure, registros DNS A correspondientes se crean automáticamente servicio de toohello de tooallow acceso a través de un nombre de dominio completo (FQDN), en lugar de usar Hola real VIP. Hola mismo proceso se produce para un ILPIP, lo que permite acceso toohello máquina virtual o instancia de rol mediante el FQDN en lugar de hello ILPIP. Por ejemplo, si crea un servicio de nube denominado *contosoadservice*, y configurar un rol web denominado *contosoweb* con dos instancias, hello Azure registros siguientes A registros para instancias de hello:

* contosoweb\_IN_0.contosoadservice.cloudapp.net
* contosoweb\_IN_1.contosoadservice.cloudapp.net 

> [!NOTE]
> Solo puede asignar una ILPIP para cada máquina virtual o instancia de rol. Puede usar la too5 ILPIPs por suscripción. Las ILPIP no se admiten para las máquinas virtuales de varias NIC.
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>¿Por qué debo solicitar una ILPIP?
Si desea toobe tooconnect pueda tooyour máquina virtual o instancia de rol mediante una dirección IP asignada directamente tooit, en lugar de usar en la nube Hola VIP del servicio:&lt;número de puerto&gt;, solicitar una ILPIP para la máquina virtual o la instancia de rol.

* **FTP activo** -mediante la asignación de una máquina virtual de ILPIP tooa, puede recibir tráfico en cualquier puerto. Los puntos de conexión no son necesarias para hello tráfico tooreceive de máquina virtual.  Para obtener más información sobre el protocolo de hello FTP, vea (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [Introducción al protocolo de FTP].
* **IP de salida** : el tráfico saliente que se origina en hello máquina virtual está asignada toohello ILPIP como origen de Hola y Hola ILPIP identifica de forma única entidades de hello VM tooexternal.

> [!NOTE]
> Hola anterior, una dirección ILPIP fue tooas que se hace referencia una dirección IP (PIP) pública.
> 

## <a name="manage-an-ilpip-for-a-vm"></a>Administración de una ILPIP para una máquina virtual
Hola siguiente las tareas le permiten toocreate, asignar y quitar ILPIPs desde máquinas virtuales:

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>¿Cómo toorequest un ILPIP durante la creación de máquinas virtuales con PowerShell
Hola siguiente script de PowerShell crea un servicio de nube denominado *FTPService*, recupera una imagen de Azure, crea una máquina virtual denominada *FTPInstance* con imagen Hola recuperar, Establece Hola VM toouse un ILPIP y agrega el nuevo servicio de hello VM toohello:

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>Cómo obtener información de ILPIP tooretrieve para una máquina virtual
Hola tooview ILPIP conocer Hola máquinas virtuales crean con script anterior de hello, ejecute el siguiente comando de PowerShell de Hola y observar los valores de hello para *PublicIPAddress* y *PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

Resultado esperado:
 
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

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>¿Cómo tooremove una ILPIP de una máquina virtual
Hola tooremove ILPIP agregado toohello VM en hello secuencia de comandos anterior, ejecute el siguiente comando de PowerShell de hello:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>¿Cómo tooadd una tooan ILPIP máquina virtual existente
tooadd una toohello ILPIP máquinas virtuales creadas con script de Hola anterior, ejecute el siguiente comando de hello:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>Administración de una ILPIP para una instancia de rol de Cloud Services

tooadd una instancia de rol de servicios en la nube de tooa ILPIP, Hola completa pasos:

1. Descargar archivo de .cscfg de Hola para servicio de nube Hola siguiendo Hola los pasos de hello [cómo los servicios de nube tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artículo.
2. Archivo de .cscfg Hola de actualización mediante la adición de hello `InstanceAddress` elemento. Hello en el ejemplo siguiente agrega un ILPIP denominado *MyPublicIP* tooa instancia de rol denominado *WebRole1*: 

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
3. Cargar archivo de .cscfg de Hola para servicio de nube Hola siguiendo Hola los pasos de hello [cómo los servicios de nube tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artículo.

## <a name="next-steps"></a>Pasos siguientes
* Comprender cómo [el direccionamiento IP](virtual-network-ip-addresses-overview-classic.md) funciona en el modelo de implementación clásica de Hola.
* Obtenga información sobre las [direcciones IP reservadas](virtual-networks-reserved-public-ip.md).
