---
title: "Implementación de una aplicación en un conjunto de escalado de máquinas virtuales de Azure | Microsoft Docs"
description: "Obtenga información sobre cómo implementar una aplicación de escalado automático simple en un conjunto de escalado de máquinas virtuales mediante una plantilla de Azure Resource Manager."
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 07883a33382cc660b043c99872312a9e77228253
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="2b3e8-103">Implementación de una aplicación de escalado automático con una plantilla</span><span class="sxs-lookup"><span data-stu-id="2b3e8-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="2b3e8-104">Las [plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) constituyen una excelente manera de implementar grupos de recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="2b3e8-105">Este tutorial se basa en [Implementación de un conjunto de escalado sencillo](virtual-machine-scale-sets-mvss-start.md) y describe cómo implementar una aplicación de escalado automático simple en un conjunto de escalado con una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how to deploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="2b3e8-106">También puede configurar el escalado automático con PowerShell, la CLI o el portal.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-106">You can also set up autoscaling using PowerShell, CLI, or the portal.</span></span> <span data-ttu-id="2b3e8-107">Para obtener más información, consulte la [información general sobre el escalado automático](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2b3e8-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="2b3e8-108">Dos plantillas de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="2b3e8-108">Two quickstart templates</span></span>
<span data-ttu-id="2b3e8-109">Cuando implementa un conjunto de escalado, puede instalar software nuevo en una imagen de plataforma con una [extensión de VM](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="2b3e8-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="2b3e8-110">Una extensión de VM es una aplicación pequeña que realizan tareas de automatización y configuración posteriores a la implementación en máquinas virtuales de Azure, como es la implementación de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="2b3e8-111">En [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) se ofrecen dos plantillas de ejemplo distintas, las que muestran cómo implementar una aplicación de escalado automático en un conjunto de escalado con extensiones de VM.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how to deploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="2b3e8-112">Servidor HTTP de Python en Linux</span><span class="sxs-lookup"><span data-stu-id="2b3e8-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="2b3e8-113">La plantilla [Servidor HTTP de Python en Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) implementa una aplicación de escalado automático sencilla que se ejecuta en un conjunto de escalado de Linux.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-113">The [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="2b3e8-114">[Bottle](http://bottlepy.org/docs/dev/), un marco web de Python y un servidor HTTP sencillo se implementan en cada VM del conjunto de escalado con una extensión de VM de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in the scale set using a custom script VM extension.</span></span> <span data-ttu-id="2b3e8-115">Este conjunto de escalado escala verticalmente cuando el uso de CPU promedio de todas las VM supera el 60% y se reduce verticalmente cuando es menor del 30%.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-115">The scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when the average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="2b3e8-116">Además del recurso de conjunto de escalado, la plantilla de ejemplo *azuredeploy.json* también declara la red virtual, la dirección IP pública, el equilibrador de carga y los recursos de configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-116">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="2b3e8-117">Para más información sobre cómo crear estos recursos en una plantilla, consulte [Conjunto de escalado de Linux con escalado automático](virtual-machine-scale-sets-linux-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="2b3e8-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="2b3e8-118">En la plantilla *azuredeploy.json*, la propiedad `extensionProfile` del recurso `Microsoft.Compute/virtualMachineScaleSets` especifica una extensión de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-118">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="2b3e8-119">`fileUris` especifica la ubicación de los scripts.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-119">`fileUris` specifies the script(s) location.</span></span> <span data-ttu-id="2b3e8-120">En este caso, dos archivos: *workserver.py*, que define un servidor HTTP sencillo, e *installserver.sh*, que instala Bottle e inicia el servidor HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts the HTTP server.</span></span> <span data-ttu-id="2b3e8-121">`commandToExecute` especifica el comando que se debe ejecutar una vez que se implementa el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-121">`commandToExecute` specifies the command to run after the scale set has been deployed.</span></span>

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="2b3e8-122">Aplicación ASP.NET MVC en Windows</span><span class="sxs-lookup"><span data-stu-id="2b3e8-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="2b3e8-123">La plantilla de ejemplo [Aplicación ASP.NET MVC en Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) implementa una aplicación ASP.NET MVC que se ejecuta en IIS en el conjunto de escalado de Windows.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-123">The [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="2b3e8-124">IIS y la aplicación MVC se implementan con la extensión de VM [Configuración de estado deseado (DSC) de PowerShell](virtual-machine-scale-sets-dsc.md).</span><span class="sxs-lookup"><span data-stu-id="2b3e8-124">IIS and the MVC app are deployed using the [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="2b3e8-125">El conjunto de escalado escala verticalmente (una instancia de VM a la vez) cuando el uso de la CPU supera el 50% durante 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-125">The scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="2b3e8-126">Además del recurso de conjunto de escalado, la plantilla de ejemplo *azuredeploy.json* también declara la red virtual, la dirección IP pública, el equilibrador de carga y los recursos de configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-126">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="2b3e8-127">Esta plantilla también demuestra la actualización de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="2b3e8-128">Para más información sobre cómo crear estos recursos en una plantilla, consulte [Conjunto de escalado de Windows con escalado automático](virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="2b3e8-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="2b3e8-129">En la plantilla *azuredeploy.json*, la propiedad `extensionProfile` del recurso `Microsoft.Compute/virtualMachineScaleSets` especifica una extensión de [configuración de estado deseado (DSC)](virtual-machine-scale-sets-dsc.md) que instala IIS y una aplicación web predeterminada desde el paquete WebDeploy.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-129">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="2b3e8-130">El script *IISInstall.ps1* instala IIS en la máquina virtual y se encuentra en la carpeta *DSC*.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-130">The *IISInstall.ps1* script installs IIS on the virtual machine and is found in the *DSC* folder.</span></span>  <span data-ttu-id="2b3e8-131">La aplicación web MVC está en la carpeta *WebDeploy*.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-131">The MVC web app is found in the *WebDeploy* folder.</span></span>  <span data-ttu-id="2b3e8-132">Las rutas de acceso al script de instalación y la aplicación web se definen en los parámetros `powershelldscZip` y `webDeployPackage` del archivo *azuredeploy.parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-132">The paths to the install script and the web app are defined in the `powershelldscZip` and `webDeployPackage` parameters in the *azuredeploy.parameters.json* file.</span></span> 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-the-template"></a><span data-ttu-id="2b3e8-133">Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="2b3e8-133">Deploy the template</span></span>
<span data-ttu-id="2b3e8-134">La manera más sencilla de implementar la plantilla [Servidor HTTP de Python en Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) o [Aplicación ASP.NET MVC en Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) es usar el botón **Implementar en Azure** que se encuentra en los archivos Léame en GitHub.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-134">The simplest way to deploy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is to use the **Deploy to Azure** button found in the in the readme files in GitHub.</span></span>  <span data-ttu-id="2b3e8-135">También puede usar PowerShell o la CLI de Azure para implementar las plantillas de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-135">You can also use PowerShell or Azure CLI to deploy the sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="2b3e8-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b3e8-136">PowerShell</span></span>
<span data-ttu-id="2b3e8-137">Copie los archivos [Servidor HTTP de Python en Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) o [Aplicación ASP.NET MVC en Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) desde el repositorio GitHub en una carpeta del equipo local.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-137">Copy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from the GitHub repo to a folder on your local computer.</span></span>  <span data-ttu-id="2b3e8-138">Abra el archivo *azuredeploy.parameters.json* y actualice los valores predeterminados de los parámetros `vmssName`, `adminUsername` y `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-138">Open the *azuredeploy.parameters.json* file and update the default values of the `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="2b3e8-139">Guarde el siguiente script de PowerShell en el archivo *deploy.ps1*, en la misma carpeta que la plantilla *azuredeploy.json*.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-139">Save the following PowerShell script to *deploy.ps1* in the same folder as the *azuredeploy.json* template.</span></span> <span data-ttu-id="2b3e8-140">Para implementar la plantilla de ejemplo, ejecute el script *deploy.ps1* desde una ventana de comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b3e8-140">To deploy the sample template run the *deploy.ps1* script from a PowerShell command window.</span></span>

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. To create a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start the deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="2b3e8-141">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2b3e8-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a><span data-ttu-id="2b3e8-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b3e8-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
