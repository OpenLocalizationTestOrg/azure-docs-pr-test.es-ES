---
title: "Automatización de la implementación de aplicaciones con extensiones de máquina virtual | Microsoft Docs"
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f972fef75aa8e13af7dab908c2b0e2ec28f1324
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="c9746-103">Implementación de aplicaciones con plantillas de Azure Resource Manager para máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="c9746-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="c9746-104">Una vez identificados todos los requisitos de infraestructura de Azure y traducidos en una plantilla de implementación, debe abordar la implementación de aplicaciones reales.</span><span class="sxs-lookup"><span data-stu-id="c9746-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="c9746-105">Por implementación de la aplicación, se entiende la instalación de los archivos binarios de aplicación reales en recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9746-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="c9746-106">En el ejemplo de Music Store, es necesario instalar y configurar .NET Core, NGINX y Supervisor en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9746-106">For the Music Store sample, .Net Core, NGINX, and Supervisor need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="c9746-107">Los archivos binarios de Music Store deben instalarse en la máquina virtual y la base de datos de Music Store debe crearse previamente.</span><span class="sxs-lookup"><span data-stu-id="c9746-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="c9746-108">En este documento se detalla cómo las extensiones de máquina virtual pueden automatizar la implementación y configuración de aplicaciones en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9746-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="c9746-109">Se resaltan todas las dependencias y configuraciones únicas.</span><span class="sxs-lookup"><span data-stu-id="c9746-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="c9746-110">Para obtener la mejor experiencia, realice una implementación previa de una instancia de la solución en su suscripción de Azure y trabaje con la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9746-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="c9746-111">La plantilla completa se puede encontrar aquí: [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)(Implementación de Music Store en Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c9746-111">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="c9746-112">Script de configuración</span><span class="sxs-lookup"><span data-stu-id="c9746-112">Configuration script</span></span>
<span data-ttu-id="c9746-113">Las extensiones de máquina virtual son programas especializados que se ejecutan en máquinas virtuales para automatizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="c9746-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="c9746-114">Hay extensiones disponibles para muchos fines específicos, como antivirus, configuración de registro y configuración de Docker.</span><span class="sxs-lookup"><span data-stu-id="c9746-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="c9746-115">Se puede usar una extensión de script personalizado para ejecutar cualquier script en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9746-115">A custom script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="c9746-116">En el ejemplo de Music Store, la configuración de las máquinas virtuales de Ubuntu y la instalación de la aplicación Music Store depende de la extensión de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="c9746-116">With the Music Store sample, it is up to the custom script extension to configure the Ubuntu virtual machines and install the Music Store application.</span></span> 

<span data-ttu-id="c9746-117">Antes de detallar cómo se declaran las extensiones de máquina virtual en una plantilla de Azure Resource Manager, examine el script que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="c9746-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="c9746-118">Este script configura la máquina virtual de Ubuntu para hospedar la aplicación Music Store.</span><span class="sxs-lookup"><span data-stu-id="c9746-118">This script configures the Ubuntu virtual machine to host the Music Store application.</span></span> <span data-ttu-id="c9746-119">Cuando se ejecuta, el script instala todo el software necesario, instala la aplicación Music Store desde el control de código fuente y prepara la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c9746-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

<span data-ttu-id="c9746-120">Para más información acerca de cómo hospedar una aplicación de .Net Core en Linux, consulte [Publish to a Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html)(Publicación en un entorno de producción de Linux).</span><span class="sxs-lookup"><span data-stu-id="c9746-120">To learn more about hosting a .Net Core application on Linux, see [Publish to a Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="c9746-121">Este ejemplo es para fines de demostración.</span><span class="sxs-lookup"><span data-stu-id="c9746-121">This sample is for demonstration purposes.</span></span>
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a><span data-ttu-id="c9746-122">Extensión de script de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c9746-122">VM Script Extension</span></span>
<span data-ttu-id="c9746-123">Para poder ejecutar extensiones de máquina virtual en una máquina virtual en tiempo de compilación, incluya los recursos de extensión en la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9746-123">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="c9746-124">La extensión se puede agregar con el asistente Agregar nuevo recurso de Visual Studio, o insertando un recurso JSON válido en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="c9746-124">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="c9746-125">El recurso de extensión de script se anida dentro del recurso de máquina virtual. Lo podemos ver en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="c9746-125">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="c9746-126">Siga este vínculo para ver el ejemplo de JSON en la plantilla de Resource Manager: [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359)(Extensión de script de máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="c9746-126">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="c9746-127">En el siguiente código JSON, observe que el script se almacena en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9746-127">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="c9746-128">Este script también podría almacenarse en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c9746-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="c9746-129">Además, plantillas de Azure Resource Manager permiten construir la cadena de ejecución de script de modo que los valores de los parámetros de la plantilla se puedan usar como parámetros para la ejecución del script.</span><span class="sxs-lookup"><span data-stu-id="c9746-129">Also, Azure Resource Manager templates allow the script execution string to constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="c9746-130">En este caso, los datos se proporcionan al implementar las plantillas, y estos valores pueden usarse después al ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="c9746-130">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="c9746-131">Para más información sobre el uso de la extensión de script personalizado, consulte [Uso de la extensión de script personalizado para máquinas virtuales de Linux con plantillas de Azure Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9746-131">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="c9746-132">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="c9746-132">Next Step</span></span>
<hr>

[<span data-ttu-id="c9746-133">Más plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c9746-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

