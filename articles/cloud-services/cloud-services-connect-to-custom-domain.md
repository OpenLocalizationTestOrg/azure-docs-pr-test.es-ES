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
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>Conexión personalizada de las funciones de servicios de nube de Azure tooa controlador de dominio de Active Directory hospedado en Azure
En primer lugar, vamos a configurar una red virtual en Azure. A continuación, agregaremos una red virtual de controlador de dominio de Active Directory (hospedado en una máquina Virtual de Azure) toohello. A continuación, se le agregar toohello de roles de servicio de nube existente creado previamente la red virtual y conectarlos toohello controlador de dominio.

Antes de empezar, par de cosas tookeep en cuenta:

1. Este tutorial usa PowerShell, así que asegúrese de tener PowerShell de Azure instalado y está listo toogo. tooget ayuda a configurar Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
2. Las instancias del controlador de dominio de Active Directory y el rol de trabajo o Web necesitan toobe Hola red virtual.

Siga a esta guía paso a paso y si surge algún problema, nos deja un comentario al final de hello del artículo Hola. Le llamaremos tooyou (Sí, se leen los comentarios).

Hola red al que hace referencia el servicio de nube Hola debe ser un **red virtual clásica**.

## <a name="create-a-virtual-network"></a>Creación de una red virtual
Puede crear una red Virtual en Azure mediante el portal de Azure de Hola o PowerShell. En este tutorial, usaremos PowerShell. toocreate una red Virtual con hello Azure portal, vea [crear red Virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

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

## <a name="create-a-virtual-machine"></a>Creación de una máquina virtual
Una vez haya completado la configuración de red Virtual de hello, deberá toocreate un controlador de dominio de Active Directory. En este tutorial, se va a configurar un controlador de dominio de AD en una máquina virtual de Azure.

toodo, crear una máquina virtual a través de PowerShell con hello siguientes comandos:

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

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>Promover el controlador de dominio de máquina Virtual tooa
Hola tooconfigure Máquina Virtual como un controlador de dominio de AD, necesitará toolog en toohello VM y configurarlo.

toolog en toohello VM, puede obtener el archivo RDP de hello a través de PowerShell, Hola de uso después de comandos:

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

Una vez que haya iniciado sesión toohello máquina virtual, configurar la máquina Virtual como un controlador de dominio de AD mediante la siguiente guía paso a paso de hello en [cómo tooset el controlador de dominio de AD del cliente](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).

## <a name="add-your-cloud-service-toohello-virtual-network"></a>Agregar la red Virtual de toohello de servicio en la nube
A continuación, debe tooadd su toohello de implementación del servicio de nube nueva red virtual. toodo, modificar el servicio de nube cscfg agregando Hola secciones relevantes tooyour cscfg con Visual Studio u Hola editor de su elección.

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

A continuación, compilar el proyecto de servicios de nube e implementarlo tooAzure. tooget ayuda con la implementación de su tooAzure de paquete de servicios de nube, vea [cómo tooCreate e implementar un servicio de nube](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>Conectar su dominio de toohello de roles de web y de trabajo
Una vez que se implementa el proyecto de servicio de nube en Azure, conectar su dominio de toohello AD personalizado de instancias de rol mediante Hola extensión de dominio de Active Directory. Hola tooadd implementación de servicios de dominio de Active Directory extensión tooyour existente en la nube y unirse al dominio personalizado de hello, ejecute hello siga los comandos de PowerShell:

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

Eso es todo.

Servicios en la nube deben ser tooyour Unidos a un controlador de dominio personalizado. Si desea que toolearn más información acerca de Hola distintas opciones disponibles para cómo ayudar tooconfigure extensión de dominio de Active Directory, use Hola PowerShell. A continuación verá un par de ejemplos:

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
