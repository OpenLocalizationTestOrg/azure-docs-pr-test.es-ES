---
title: "aaaDeploy una aplicación en un conjunto de escalas de máquina virtual de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de una aplicación simple de escalado automático en una escala de máquinas virtuales que se establecen a través de una plantilla de Azure Resource Manager toodeploy."
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
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a>Implementación de una aplicación de escalado automático con una plantilla

[Plantillas de administrador de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) es una excelente manera toodeploy grupos de recursos relacionados. Este tutorial se basa en [implementar un conjunto de escala simple](virtual-machine-scale-sets-mvss-start.md) y describe la forma toodeploy una aplicación simple de escalado automático en una escala establece usando una plantilla de Azure Resource Manager.  También puede configurar el escalado automático con PowerShell, CLI o portal Hola. Para obtener más información, consulte la [información general sobre el escalado automático](virtual-machine-scale-sets-autoscale-overview.md).

## <a name="two-quickstart-templates"></a>Dos plantillas de inicio rápido
Cuando implementa un conjunto de escalado, puede instalar software nuevo en una imagen de plataforma con una [extensión de VM](../virtual-machines/virtual-machines-windows-extensions-features.md). Una extensión de VM es una aplicación pequeña que realizan tareas de automatización y configuración posteriores a la implementación en máquinas virtuales de Azure, como es la implementación de una aplicación. Proporciona dos plantillas de muestra diferente en [Azure/azure-inicio rápido: plantillas](https://github.com/Azure/azure-quickstart-templates) que muestran cómo toodeploy una aplicación de escalado automático en una escala establece utilizando extensiones de máquina virtual.

### <a name="python-http-server-on-linux"></a>Servidor HTTP de Python en Linux
Hola [servidor HTTP de Python en Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) plantilla de ejemplo implementa una aplicación simple de escalado automático que se ejecuta en un conjunto de escalas de Linux.  [Bottle](http://bottlepy.org/docs/dev/), un marco de trabajo de web de Python y un sencillo servidor HTTP se implementan en cada máquina virtual en escala de hello establecida con un script personalizado de extensión de máquina virtual. escala de Hello configura escalas cuando es mayor que 60% de uso promedio de CPU a través de todas las máquinas virtuales y escala hacia abajo cuando el uso promedio de CPU de hello es inferior a 30%.

Además toohello conjunto de escalado de recursos, hello *azuredeploy.json* plantilla de ejemplo también declara red virtual, la dirección IP pública, equilibrador de carga y recursos de la configuración de escalado automático.  Para más información sobre cómo crear estos recursos en una plantilla, consulte [Conjunto de escalado de Linux con escalado automático](virtual-machine-scale-sets-linux-autoscale.md).

Hola *azuredeploy.json* plantilla, hello `extensionProfile` propiedad de hello `Microsoft.Compute/virtualMachineScaleSets` recurso especifica una extensión de script personalizado. `fileUris`Especifica la ubicación de secuencias de comandos de Hola. En este caso, se restauran dos archivos: *workserver.py*, que define un servidor HTTP sencillo, y *installserver.sh*, que instala Bottle e inicia Hola servidor HTTP. `commandToExecute`Especifica Hola comando toorun una vez implementado el conjunto de escalas de Hola.

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

### <a name="aspnet-mvc-application-on-windows"></a>Aplicación ASP.NET MVC en Windows
Hola [aplicación de MVC de ASP.NET en Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) plantilla de ejemplo implementa una aplicación ASP.NET MVC sencilla que se ejecutan en IIS en el conjunto de escalas de Windows.  Hello aplicación MVC y IIS se implementan utilizando hello [(DSC de) la configuración de estado deseado de PowerShell](virtual-machine-scale-sets-dsc.md) extensión de máquina virtual.  escala de Hello configurado escalas (en la instancia de máquina virtual a la vez) cuando el uso de CPU es mayor del 50 por ciento durante 5 minutos. 

Además toohello conjunto de escalado de recursos, hello *azuredeploy.json* plantilla de ejemplo también declara red virtual, la dirección IP pública, equilibrador de carga y recursos de la configuración de escalado automático. Esta plantilla también demuestra la actualización de la aplicación.  Para más información sobre cómo crear estos recursos en una plantilla, consulte [Conjunto de escalado de Windows con escalado automático](virtual-machine-scale-sets-windows-autoscale.md).

Hola *azuredeploy.json* plantilla, hello `extensionProfile` propiedad de hello `Microsoft.Compute/virtualMachineScaleSets` recursos Especifica un [configuración de estado deseado (DSC)](virtual-machine-scale-sets-dsc.md) extensión que se instala IIS y su valor predeterminado aplicación Web de un paquete de WebDeploy.  Hola *IISInstall.ps1* script instala IIS en la máquina virtual de Hola y se encuentra en hello *DSC* carpeta.  aplicación web MVC de Hola se encuentra en hello *WebDeploy* carpeta.  script de instalación de toohello de rutas de acceso de Hola y Hola web app se definen en hello `powershelldscZip` y `webDeployPackage` parámetros en hello *azuredeploy.parameters.json* archivo. 

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

## <a name="deploy-hello-template"></a>Implementar la plantilla de Hola
Hola de toodeploy de manera más sencilla de Hello [servidor HTTP de Python en Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) o [aplicación de MVC de ASP.NET en Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) plantilla es hello toouse **implementar tooAzure** encuentra el botón en hello en los archivos Léame de hello en GitHub.  También puede utilizar plantillas de ejemplo de Hola toodeploy PowerShell o CLI de Azure.

### <a name="powershell"></a>PowerShell
Hola copia [servidor HTTP de Python en Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) o [aplicación de MVC de ASP.NET en Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) archivos desde la carpeta de tooa de repositorio de GitHub de hello en el equipo local.  Abra hello *azuredeploy.parameters.json* archivo y actualización Hola valores de hello `vmssName`, `adminUsername`, y `adminPassword` parámetros. Guardar Hola siguiente script de PowerShell demasiado*deploy.ps1* Hola misma carpeta que hello *azuredeploy.json* plantilla. Hola de plantilla ejecutar de ejemplo de Hola toodeploy *deploy.ps1* secuencia de comandos desde una ventana de comandos de PowerShell.

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
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a>CLI de Azure
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

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
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
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

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
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

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
