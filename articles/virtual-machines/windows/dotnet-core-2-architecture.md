---
title: "Implementación de recursos de proceso Windows con plantillas de Azure Resource Manager | Microsoft Docs"
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8a8b888195e52ea9669922a6a00a873025f3c375
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="41b8b-103">Arquitectura de aplicaciones con plantillas de Azure Resource Manager para máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="41b8b-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="41b8b-104">Al desarrollar una implementación de Azure Resource Manager, los requisitos de procesos deben asignarse a servicios y recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="41b8b-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="41b8b-105">Si una aplicación consta de puntos de conexión HTTP, una base de datos y un servicio de almacenamiento en caché de datos, los recursos de Azure que hospedan cada uno de estos componentes deben racionalizarse.</span><span class="sxs-lookup"><span data-stu-id="41b8b-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="41b8b-106">Por ejemplo, la aplicación Music Store de ejemplo incluye una aplicación web que se hospeda en una máquina virtual y una base de datos SQL que se hospeda en la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="41b8b-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="41b8b-107">Este documento describe cómo se configuran los recursos de procesos de Music Store en la plantilla de Azure Resource Manager de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="41b8b-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="41b8b-108">Se resaltan todas las dependencias y configuraciones únicas.</span><span class="sxs-lookup"><span data-stu-id="41b8b-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="41b8b-109">Para obtener la mejor experiencia, realice una implementación previa de una instancia de la solución en su suscripción de Azure y trabaje con la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="41b8b-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="41b8b-110">La plantilla completa se puede encontrar aquí: [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)(Implementación de Music Store en Windows).</span><span class="sxs-lookup"><span data-stu-id="41b8b-110">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="41b8b-111">Máquina virtual</span><span class="sxs-lookup"><span data-stu-id="41b8b-111">Virtual Machine</span></span>
<span data-ttu-id="41b8b-112">La aplicación Music Store incluye una aplicación web donde los clientes pueden buscar y comprar música.</span><span class="sxs-lookup"><span data-stu-id="41b8b-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="41b8b-113">Aunque hay varios servicios de Azure que pueden hospedar aplicaciones web, en este ejemplo se utiliza una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41b8b-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="41b8b-114">Con la plantilla de Music Store de ejemplo, se implementa una máquina virtual, se instala un servidor web, y se instala y configura el sitio web de Music Store.</span><span class="sxs-lookup"><span data-stu-id="41b8b-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="41b8b-115">Este artículo se centra únicamente en la implementación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41b8b-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="41b8b-116">La configuración del servidor web y la aplicación se detalla en un artículo posterior.</span><span class="sxs-lookup"><span data-stu-id="41b8b-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="41b8b-117">Se puede agregar una máquina virtual a una plantilla mediante el asistente Agregar nuevo recurso de Visual Studio o insertando un recurso JSON válido en la plantilla de implementación.</span><span class="sxs-lookup"><span data-stu-id="41b8b-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="41b8b-118">Al implementar una máquina virtual, también se necesitan varios recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="41b8b-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="41b8b-119">Si utiliza Visual Studio para crear la plantilla, estos recursos se crean automáticamente.</span><span class="sxs-lookup"><span data-stu-id="41b8b-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="41b8b-120">Si la plantilla se crea manualmente, estos recursos deben insertarse y configurarse.</span><span class="sxs-lookup"><span data-stu-id="41b8b-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="41b8b-121">Siga este vínculo para ver el ejemplo de JSON en la plantilla de Resource Manager: [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285)(JSON de máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="41b8b-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

```json
{
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

<span data-ttu-id="41b8b-122">Una vez implementada, las propiedades de la máquina virtual pueden verse en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="41b8b-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![Máquina virtual](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="41b8b-124">Cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="41b8b-124">Storage Account</span></span>
<span data-ttu-id="41b8b-125">Las cuentas de almacenamiento tienen numerosas funcionalidades y opciones de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="41b8b-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="41b8b-126">En el contexto de las máquinas virtuales de Azure, una cuenta de almacenamiento contiene los discos duros virtuales de la máquina virtual y todos los discos de datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="41b8b-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="41b8b-127">El ejemplo de Music Store incluye una cuenta de almacenamiento que contiene la unidad de disco duro virtual de cada máquina virtual de la implementación.</span><span class="sxs-lookup"><span data-stu-id="41b8b-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="41b8b-128">Siga este vínculo para ver el ejemplo de JSON en la plantilla de Resource Manager: [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98)(Cuenta de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="41b8b-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

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

<span data-ttu-id="41b8b-129">Una cuenta de almacenamiento se asocia a una máquina virtual dentro de la declaración de plantilla de Resource Manager de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41b8b-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="41b8b-130">Siga este vínculo para ver el ejemplo de JSON en la plantilla de Resource Manager: [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321)(Asociación de cuenta de almacenamiento con una máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="41b8b-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

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

<span data-ttu-id="41b8b-131">Después de la implementación, la cuenta de almacenamiento puede verse en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="41b8b-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![Cuenta de almacenamiento](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="41b8b-133">Si hace clic en el contenedor de blobs de la cuenta de almacenamiento, puede ver el archivo de unidad de disco duro virtual para cada máquina virtual implementada con la plantilla.</span><span class="sxs-lookup"><span data-stu-id="41b8b-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![Unidades de disco duro virtuales](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="41b8b-135">Para más información sobre Azure Storage, consulte [Documentación de Almacenamiento](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="41b8b-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="41b8b-136">Red virtual</span><span class="sxs-lookup"><span data-stu-id="41b8b-136">Virtual Network</span></span>
<span data-ttu-id="41b8b-137">Si una máquina virtual requiere una conexión en red interna, como la capacidad de comunicarse con otras máquinas virtuales y recursos de Azure, se requiere Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="41b8b-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="41b8b-138">Una red virtual no permite el acceso a la máquina virtual a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="41b8b-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="41b8b-139">La conectividad pública requiere una dirección IP pública, que se detalla más adelante en esta serie.</span><span class="sxs-lookup"><span data-stu-id="41b8b-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="41b8b-140">Siga este vínculo para ver el ejemplo de JSON en la plantilla de Resource Manager: [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126)(Red virtual y subredes).</span><span class="sxs-lookup"><span data-stu-id="41b8b-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

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

<span data-ttu-id="41b8b-141">En Azure Portal, la red virtual se asemeja a la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="41b8b-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="41b8b-142">Observe que todas las máquinas virtuales que se implementan con la plantilla están conectadas a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="41b8b-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![Red virtual](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="41b8b-144">Interfaz de red</span><span class="sxs-lookup"><span data-stu-id="41b8b-144">Network Interface</span></span>
 <span data-ttu-id="41b8b-145">Una interfaz de red conecta una máquina virtual a una red virtual, en concreto a una subred que se ha definido en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="41b8b-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="41b8b-146">Siga este vínculo para ver el ejemplo de JSON en la plantilla de Resource Manager: [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156)(Interfaz de red).</span><span class="sxs-lookup"><span data-stu-id="41b8b-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
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
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
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
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="41b8b-147">Cada recurso de la máquina virtual incluye un perfil de red.</span><span class="sxs-lookup"><span data-stu-id="41b8b-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="41b8b-148">La interfaz de red está asociada a la máquina virtual de este perfil.</span><span class="sxs-lookup"><span data-stu-id="41b8b-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="41b8b-149">Siga este vínculo para ver el ejemplo de JSON en la plantilla de Resource Manager: [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330)(Perfil de red de la máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="41b8b-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="41b8b-150">En Azure Portal, la red virtual se asemeja a la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="41b8b-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="41b8b-151">La dirección IP interna y la asociación de la máquina virtual pueden verse en el recurso de la interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="41b8b-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![Interfaz de red](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="41b8b-153">Para más información acerca de Azure Virtual Network, consulte [Documentación de Red virtual](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="41b8b-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="41b8b-154">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="41b8b-154">Azure SQL Database</span></span>
<span data-ttu-id="41b8b-155">Además de la máquina virtual que hospeda el sitio web de Music Store, se implementa Azure SQL Database para hospedar la base de datos de la tienda de música.</span><span class="sxs-lookup"><span data-stu-id="41b8b-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="41b8b-156">La ventaja de utilizar Azure SQL Database aquí es que no es necesario un segundo conjunto de máquinas virtuales, además de que en el servicio se integran la disponibilidad y la escala.</span><span class="sxs-lookup"><span data-stu-id="41b8b-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="41b8b-157">Se puede agregar una base de datos SQL de Azure mediante el asistente Agregar nuevo recurso de Visual Studio o insertando un recurso JSON válido en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="41b8b-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="41b8b-158">El recurso de SQL Server incluye un nombre de usuario y una contraseña con derechos administrativos concedidos en la instancia de SQL.</span><span class="sxs-lookup"><span data-stu-id="41b8b-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="41b8b-159">Además, se agrega un recurso de firewall de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="41b8b-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="41b8b-160">De forma predeterminada, las aplicaciones hospedadas en Azure pueden conectarse con la instancia de SQL.</span><span class="sxs-lookup"><span data-stu-id="41b8b-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="41b8b-161">Para permitir que una aplicación externa, como SQL Server Management Studio, se conecte a la instancia de SQL, debe configurarse el firewall.</span><span class="sxs-lookup"><span data-stu-id="41b8b-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="41b8b-162">Para esta demostración de Music Store, la configuración predeterminada es correcta.</span><span class="sxs-lookup"><span data-stu-id="41b8b-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="41b8b-163">Siga este vínculo para ver el ejemplo de JSON en la plantilla de Resource Manager: [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span><span class="sxs-lookup"><span data-stu-id="41b8b-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="41b8b-164">Vista del servidor SQL y la base de datos de Music Store tal como se muestran en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="41b8b-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="41b8b-166">Para más información sobre la implementación de Azure SQL Database, consulte [Documentación de Base de datos SQL](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="41b8b-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="41b8b-167">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="41b8b-167">Next step</span></span>
<hr>

[<span data-ttu-id="41b8b-168">Paso 2: acceso y seguridad en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="41b8b-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

