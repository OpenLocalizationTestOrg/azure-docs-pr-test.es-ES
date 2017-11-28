---
title: "aaaAccess y seguridad en las plantillas de Azure para máquinas virtuales de Windows | Documentos de Microsoft"
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="bfdb5-103">Acceso y seguridad en plantillas de Azure Resource Manager para máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="bfdb5-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="bfdb5-104">Aplicaciones alojadas en Azure necesidad probable toobe acceso a través de hello internet o una VPN o conexión de Express Route con Azure.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="bfdb5-105">Con el ejemplo de aplicación de la tienda de música de hello, estará disponible en sitio web de Hola Hola internet con una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="bfdb5-106">Con acceso establecido, se deben proteger conexiones toohello access y aplicación toohello recursos de máquina virtual por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="bfdb5-107">Esta acceso protegido se proporciona mediante un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="bfdb5-108">Este documento describe cómo se protege la aplicación de tienda de música de Hola en la plantilla de administrador de recursos de Azure de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="bfdb5-109">Se resaltan todas las dependencias y configuraciones únicas.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="bfdb5-110">Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="bfdb5-111">plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="bfdb5-112">Dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="bfdb5-112">Public IP Address</span></span>
<span data-ttu-id="bfdb5-113">se puede utilizar tooprovide acceso público tooan recursos de Azure, un recurso de dirección IP público.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="bfdb5-114">La dirección IP pública puede configurarse con una dirección IP estática o dinámica.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="bfdb5-115">Si se utiliza una dirección dinámica, y se detiene y se cancela la asignación de máquina virtual de hello, se quita direcciones Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="bfdb5-116">Cuando se vuelva a iniciar la máquina de hello, se puede asignar una dirección IP pública diferente.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="bfdb5-117">tooprevent una IP de direcciones de cambio, puede utilizar una dirección IP reservada.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="bfdb5-118">Una dirección IP pública se pueden agregar plantilla de Azure Resource Manager tooan con hello Visual Studio agregar Asistente para nuevo recurso, o mediante la inserción de un valor JSON válido en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="bfdb5-119">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [dirección IP pública](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="bfdb5-120">Una dirección IP pública puede asociarse con un adaptador de red virtual o un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="bfdb5-121">En este ejemplo, dado que Hola sitio Web de la tienda de música tiene una carga equilibrada entre varias máquinas virtuales, Hola dirección IP pública es toohello adjunto equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="bfdb5-122">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [asociación de la dirección IP pública con el equilibrador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="bfdb5-123">Hello dirección IP pública como ver Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="bfdb5-124">Observe que la dirección IP pública hello es equilibrador de carga de tooa asociados y no en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="bfdb5-125">Equilibradores de carga de red se detallan en el siguiente documento de Hola de esta serie.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-125">Network load balancers are detailed in hello next document of this series.</span></span>

![Dirección IP pública](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="bfdb5-127">Para más información sobre direcciones IP públicas de Azure, consulte [Direcciones IP en Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="bfdb5-128">Grupo de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="bfdb5-128">Network Security Group</span></span>
<span data-ttu-id="bfdb5-129">Una vez acceso a recursos de tooAzure establecida, este acceso debe estar limitado.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="bfdb5-130">En máquinas virtuales de Azure, el acceso se protege mediante un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="bfdb5-131">Con el ejemplo de aplicación de la tienda de música de hello, todas máquinas virtuales que toohello acceso está restringido excepto a través del puerto 80 para el acceso http y el puerto 3389 para acceso RDP.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="bfdb5-132">Un grupo de seguridad de red pueden agregarse tooan Azure Resource Manager plantilla mediante Visual Studio agregar Asistente para nuevo recurso, Hola o insertando un valor JSON válido en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="bfdb5-133">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [grupo de seguridad de red](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

<span data-ttu-id="bfdb5-134">En este ejemplo, grupo de seguridad de red de hello está asociado con el objeto de subred Hola declarado en recursos de red Virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="bfdb5-135">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [asociación de grupo de seguridad de red con red Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

<span data-ttu-id="bfdb5-136">A continuación se muestra qué grupo de seguridad de red de hello aparece de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="bfdb5-137">Observe que se puede asociar un grupo de seguridad de red con una interfaz de red o subred.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="bfdb5-138">En este caso, hello NSG está asociado tooa subred.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="bfdb5-139">En esta configuración, hello las reglas de entrada aplican tooall máquinas virtuales conectadas toohello subred.</span><span class="sxs-lookup"><span data-stu-id="bfdb5-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![Grupo de seguridad de red (NSG)](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="bfdb5-141">Para más información sobre los grupos de seguridad de red, consulte [¿Qué es un grupo de seguridad de red?](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="bfdb5-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="bfdb5-142">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="bfdb5-142">Next step</span></span>
<hr>

[<span data-ttu-id="bfdb5-143">Paso 3: disponibilidad y escala en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bfdb5-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

