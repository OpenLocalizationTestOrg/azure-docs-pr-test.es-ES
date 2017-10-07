---
title: aaaDeploying recursos de proceso de Linux con plantillas de administrador de recursos de Azure | Documentos de Microsoft
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="cd345-103">Arquitectura de aplicaciones con plantillas de Azure Resource Manager para máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="cd345-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="cd345-104">Al desarrollar una implementación de Azure Resource Manager, los requisitos de proceso necesitan toobe asignado tooAzure recursos y servicios.</span><span class="sxs-lookup"><span data-stu-id="cd345-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="cd345-105">Si una aplicación consta de varios extremos de http, una base de datos y un servicio de caché de datos, hello recursos de Azure que hospedan cada uno de estos componentes debe toobe racionalizado.</span><span class="sxs-lookup"><span data-stu-id="cd345-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="cd345-106">Por ejemplo, la aplicación de tienda de música de ejemplo de Hola incluye una aplicación web que se hospeda en una máquina virtual y una base de datos SQL, que se hospeda en la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd345-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="cd345-107">Este documento describe cómo se configuran los recursos de proceso de hello tienda de música en la plantilla de administrador de recursos de Azure de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="cd345-108">Se resaltan todas las dependencias y configuraciones únicas.</span><span class="sxs-lookup"><span data-stu-id="cd345-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="cd345-109">Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd345-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="cd345-110">plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="cd345-110">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="cd345-111">Máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cd345-111">Virtual Machine</span></span>
<span data-ttu-id="cd345-112">aplicación de la tienda de música de Hello incluye una aplicación web donde los clientes pueden examinar y comprar música.</span><span class="sxs-lookup"><span data-stu-id="cd345-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="cd345-113">Aunque hay varios servicios de Azure que pueden hospedar aplicaciones web, en este ejemplo se utiliza una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cd345-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="cd345-114">Mediante la plantilla de tienda de música de ejemplo de Hola, se implementa una máquina virtual, instalar un servidor web y sitio Web de tienda de música de hello instalado y configurado.</span><span class="sxs-lookup"><span data-stu-id="cd345-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="cd345-115">Para simplificar hello en este artículo, se detalla solamente la implementación de máquina virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="cd345-116">configuración de Hola de servidor web de Hola y aplicación hello se detalla en un artículo de una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="cd345-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="cd345-117">Puede agregarse a una máquina virtual de plantilla tooa mediante Visual Studio Agregar recurso nuevo asistente, o mediante la inserción de un valor JSON válido en la plantilla de implementación de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="cd345-118">Al implementar una máquina virtual, también se necesitan varios recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="cd345-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="cd345-119">Si usa la plantilla de Visual Studio toocreate hello, estos recursos se crean automáticamente.</span><span class="sxs-lookup"><span data-stu-id="cd345-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="cd345-120">Si manualmente creando plantilla hello, estos recursos deben toobe insertarse y configurarse.</span><span class="sxs-lookup"><span data-stu-id="cd345-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="cd345-121">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [JSON de la máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span><span class="sxs-lookup"><span data-stu-id="cd345-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
      ........<truncated>  
    }
```

<span data-ttu-id="cd345-122">Una vez implementado, propiedades de la máquina virtual de hello pueden verse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd345-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![Máquina virtual](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="cd345-124">Cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="cd345-124">Storage Account</span></span>
<span data-ttu-id="cd345-125">Las cuentas de almacenamiento tienen numerosas funcionalidades y opciones de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cd345-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="cd345-126">Para el contexto de Hola de máquinas virtuales de Azure, una cuenta de almacenamiento contiene discos duros virtuales de Hola de máquina virtual de Hola y los discos de datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="cd345-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="cd345-127">ejemplo de la tienda de música de Hello incluye un almacenamiento cuenta toohold Hola disco duro virtual de cada máquina virtual en la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="cd345-128">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [cuenta de almacenamiento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span><span class="sxs-lookup"><span data-stu-id="cd345-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="cd345-129">Una cuenta de almacenamiento está asociado a una máquina virtual dentro de la declaración de plantilla de administrador de recursos de Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="cd345-130">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [asociación de la máquina Virtual y cuenta de almacenamiento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span><span class="sxs-lookup"><span data-stu-id="cd345-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="cd345-131">Después de la implementación, la cuenta de almacenamiento de hello puede verse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd345-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![Cuenta de almacenamiento](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="cd345-133">Hacer clic en el contenedor de blob de cuenta de almacenamiento de hello, se puede ver archivo de disco duro virtual de hello para cada máquina virtual implementada con plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![Unidades de disco duro virtuales](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="cd345-135">Para más información sobre Azure Storage, consulte [Documentación de Almacenamiento](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="cd345-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="cd345-136">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="cd345-136">Virtual Network</span></span>
<span data-ttu-id="cd345-137">Si una máquina virtual requiere que las redes internas como Hola capacidad toocommunicate con otras máquinas virtuales y recursos de Azure, se requiere una red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd345-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="cd345-138">Una red virtual no hacer accesible a través de máquina virtual de Hola Hola internet.</span><span class="sxs-lookup"><span data-stu-id="cd345-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="cd345-139">La conectividad pública requiere una dirección IP pública, que se detalla más adelante en esta serie.</span><span class="sxs-lookup"><span data-stu-id="cd345-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="cd345-140">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [subredes y red Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span><span class="sxs-lookup"><span data-stu-id="cd345-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

<span data-ttu-id="cd345-141">Desde el portal de Azure hello, red virtual de hello es similar a Hola después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="cd345-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="cd345-142">Observe que todas las máquinas virtuales implementadas con plantilla hello toohello adjunto de red virtual.</span><span class="sxs-lookup"><span data-stu-id="cd345-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![Virtual Network](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="cd345-144">Interfaz de red</span><span class="sxs-lookup"><span data-stu-id="cd345-144">Network Interface</span></span>
 <span data-ttu-id="cd345-145">Una interfaz de red conecta a una red virtual de máquina virtual tooa, más concretamente tooa máscara de subred que se ha definido en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="cd345-146">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [interfaz de red](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span><span class="sxs-lookup"><span data-stu-id="cd345-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="cd345-147">Cada recurso de la máquina virtual incluye un perfil de red.</span><span class="sxs-lookup"><span data-stu-id="cd345-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="cd345-148">interfaz de red de Hello está asociado a la máquina virtual de hello en este perfil.</span><span class="sxs-lookup"><span data-stu-id="cd345-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="cd345-149">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [perfil de red de máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span><span class="sxs-lookup"><span data-stu-id="cd345-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="cd345-150">Desde el portal de Azure hello, interfaz de red de hello es similar a Hola después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="cd345-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="cd345-151">dirección IP interna de Hola y asociación de la máquina virtual de hello pueden verse en el recurso de interfaz de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![Interfaz de red](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="cd345-153">Para más información acerca de Azure Virtual Network, consulte [Documentación de Red virtual](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="cd345-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="cd345-154">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cd345-154">Azure SQL Database</span></span>
<span data-ttu-id="cd345-155">Además tooa virtual machine hospedar sitios Web de la tienda de música de hello, una base de datos de SQL Azure es base de datos de implementada toohost Hola tienda de música.</span><span class="sxs-lookup"><span data-stu-id="cd345-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="cd345-156">ventaja de Hola de con la base de datos de SQL Azure aquí es que no es necesario un segundo conjunto de máquinas virtuales, y escala y disponibilidad están integradas en el servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="cd345-157">Una base de datos de SQL Azure se puede agregar utilizando Hola Visual Studio Agregar recurso nuevo asistente, o mediante la inserción de un valor JSON válido en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="cd345-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="cd345-158">Hola recurso de SQL Server incluye un nombre de usuario y una contraseña que se le conceden derechos administrativos en la instancia de SQL Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="cd345-159">Además, se agrega un recurso de firewall de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cd345-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="cd345-160">De forma predeterminada, las aplicaciones hospedadas en Azure son capaz de tooconnect con la instancia de SQL Hola.</span><span class="sxs-lookup"><span data-stu-id="cd345-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="cd345-161">aplicación externa de tooallow tal una SQL Server Management studio tooconnect toohello instancia de SQL, firewall de hello debe toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="cd345-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="cd345-162">Para simplificar Hola demostración de la tienda de música de hello, la configuración predeterminada de hello es correcto.</span><span class="sxs-lookup"><span data-stu-id="cd345-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="cd345-163">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [base de datos de SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span><span class="sxs-lookup"><span data-stu-id="cd345-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="cd345-164">Una vista de base de datos de MusicStore tal como se muestra en el portal de Azure de Hola y Hola SQL server.</span><span class="sxs-lookup"><span data-stu-id="cd345-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="cd345-166">Para más información sobre la implementación de Azure SQL Database, consulte [Documentación de Base de datos SQL](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="cd345-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="cd345-167">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="cd345-167">Next step</span></span>
<hr>

[<span data-ttu-id="cd345-168">Paso 2: acceso y seguridad en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cd345-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

