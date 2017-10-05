---
title: "Script automatizado para crear la aplicación web de Service Manager para conectarse con IT Service Management Connector en OMS | Microsoft Docs"
description: "Cree una aplicación web de Service Manager con un script automatizado para conectar con el conector de administración de servicios de TI en OMS y supervisar y administrar centralmente los elementos de trabajo ITSM."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 879e819f-d880-41c8-9775-a30907e42059
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: v-jysur
ms.openlocfilehash: ad69d82e57be8bfd9ba40dd88cbc0a979c9e1722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-service-manager-web-app-using-the-automated-script-preview"></a><span data-ttu-id="9127d-103">Creación de una aplicación web de Service Manager mediante el script automatizado (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="9127d-103">Create Service Manager Web app using the automated script (Preview)</span></span>

<span data-ttu-id="9127d-104">Use el siguiente script para crear la aplicación web para la instancia de Service Manager.</span><span class="sxs-lookup"><span data-stu-id="9127d-104">Use the following script to create the Web app for your Service Manager instance.</span></span> <span data-ttu-id="9127d-105">Aquí podrá obtener más información sobre la conexión de Service Manager: [Service Manager Web app](log-analytics-itsmc-connections.md#create-and-deploy-service-manager-web-app-service) (Aplicación web de Service Manager).</span><span class="sxs-lookup"><span data-stu-id="9127d-105">More information about Service Manager connection is here: [Service Manager Web app](log-analytics-itsmc-connections.md#create-and-deploy-service-manager-web-app-service)</span></span>

<span data-ttu-id="9127d-106">Ejecute el script proporcionando los siguientes detalles necesarios:</span><span class="sxs-lookup"><span data-stu-id="9127d-106">Run the script by providing the following required details:</span></span>

- <span data-ttu-id="9127d-107">Detalles de la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="9127d-107">Azure subscription details</span></span>
- <span data-ttu-id="9127d-108">Definición de un nombre de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9127d-108">Resource group name</span></span>
- <span data-ttu-id="9127d-109">Ubicación</span><span class="sxs-lookup"><span data-stu-id="9127d-109">Location</span></span>
- <span data-ttu-id="9127d-110">Detalles del servidor de Service Manager (nombre del servidor, dominio, nombre de usuario y contraseña)</span><span class="sxs-lookup"><span data-stu-id="9127d-110">Service Manager server details (server name,    domain, username and password)</span></span>
- <span data-ttu-id="9127d-111">Prefijo de nombre de sitio de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="9127d-111">Site name prefix for your Web app</span></span>
- <span data-ttu-id="9127d-112">Espacio de nombres de ServiceBus.</span><span class="sxs-lookup"><span data-stu-id="9127d-112">ServiceBus Namespace.</span></span>

<span data-ttu-id="9127d-113">El script creará la aplicación web con el nombre que especificó (junto con algunas cadenas adicionales para hacerlo único).</span><span class="sxs-lookup"><span data-stu-id="9127d-113">The script will create the Web app using the name that you specified (along with few additional strings to make it unique).</span></span> <span data-ttu-id="9127d-114">Genera la **dirección URL de la aplicación web**, el **id. de cliente** y el **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="9127d-114">It generates the **Web app URL**, **client ID** and **client secret**.</span></span>

<span data-ttu-id="9127d-115">Guarde estos valores, ya que los necesitará cuando cree una conexión con IT Service Management Connector.</span><span class="sxs-lookup"><span data-stu-id="9127d-115">Save these values, you will need these when you create a connection with IT Service Management Connector.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9127d-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9127d-116">Prerequisites</span></span>

 <span data-ttu-id="9127d-117">Windows Management Framework 5.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="9127d-117">Windows Management Framework 5.0 or above.</span></span>
<span data-ttu-id="9127d-118">Windows 10 tiene la versión 5.1 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9127d-118">Windows 10 has 5.1 by default.</span></span> <span data-ttu-id="9127d-119">Puede descargar el marco desde [aquí](https://www.microsoft.com/download/details.aspx?id=53347):</span><span class="sxs-lookup"><span data-stu-id="9127d-119">You can download the framework from [here](https://www.microsoft.com/download/details.aspx?id=53347):</span></span>

<span data-ttu-id="9127d-120">Use el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="9127d-120">Use the following script:</span></span>

```
####################################
# User Configuration Section Begins
####################################

# Subscription name in Azure account. Check in Azure Portal.
$azureSubscriptionName = ""

# Resource group name for resource deployment. Could be an existing resource group or a new one to be created.
$resourceGroupName = ""

# Location for existing resource group or new resource group deployment
################################### List of available regions #################################################
# centralus,eastasia,southeastasia,eastus,eastus2,westus,westus2,northcentralus,southcentralus,westcentralus,
# northeurope,westeurope,japaneast,japanwest,brazilsouth,australiasoutheast,australiaeast,westindia,southindia,
# centralindia,canadacentral,canadaeast,uksouth,ukwest.
###############################################################################################################
$location = ""

# Service Manager Authentication Settings
$serverName = ""
$domain = ""
$username = ""
$password = ""


# Azure site Name Prefix. Default is "smoc". It can be configured to any desired value.
$siteNamePrefix = ""

# Service Bus namespace. Please provide an already existing service bus namespace.
# If it doesn't exist, a new one will be created with name $siteName + "sbn" which can also be later reused for any other hybrid connections.
$serviceName = ""

##################################
# User Configuration Section Ends
##################################

################
# Installations
################

# Allowing the execution of the script for current user.  
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser -Force

Write-Host "Checking for required modules..."
if(!(Get-PackageProvider -Name NuGet))
{
   Write-Host "Installing NuGet Package Provider..."
   Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Scope CurrentUser -Force -WarningAction SilentlyContinue
}
$module = Get-Module -ListAvailable -Name AzureRM

if(!$module -or ($module[0].Version.Major -lt 4))
{
    Write-Host "Installing AzureRm Module..."  
    try
    {
        # In case of Win 10 Anniversary update
        Install-Module AzureRM -MinimumVersion 4.1.0 -Scope CurrentUser -Force -WarningAction SilentlyContinue -AllowClobber
    }
    catch
    {
        Install-Module AzureRM -MinimumVersion 4.1.0 -Scope CurrentUser -Force -WarningAction SilentlyContinue
    }

}

Write-Host "Requirement check complete!!"

#############
# Parameters
#############

$errorActionPreference = "Stop"

$templateUri = "https://raw.githubusercontent.com/SystemCenterServiceManager/SMOMSConnector/master/azuredeploy.json"

if(!$siteNamePrefix)
{
    $siteNamePrefix = "smoc"
}

Add-AzureRmAccount

$context = Set-AzureRmContext -SubscriptionName $azureSubscriptionName -WarningAction SilentlyContinue

$resourceProvider = Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web

if(!$resourceProvider -or $resourceProvider[0].RegistrationState -ne "Registered")
{
    try
    {
        Write-Host "Registering Microsoft.Web Resource Provider"
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Web
    }
    catch
    {
        Write-Host "Failed to Register Microsoft.Web Resource Provider. Please register it in Azure Portal."
        exit
    }   
}
do
{
    $rand = Get-Random -Maximum 32000

    $siteName = $siteNamePrefix + $rand

    $resource = Find-AzureRmResource -ResourceNameContains $siteName -ResourceType Microsoft.Web/sites

}while($resource)

$azureSite = "https://"+$siteName+".azurewebsites.net"

##############
# MAIN Begins
##############

# Web App Deployment
####################

$tenant = $context.Tenant.Id
if(!$tenant)
{
    #For backward compatibility with older versions
    $tenant = $context.Tenant.TenantId
}
try
{
    Get-AzureRmResourceGroup -Name $resourceGroupName
}
catch
{
    New-AzureRmResourceGroup -Location $location -Name $resourceGroupName
}

Write-Output "Web App Deployment in progress...."

New-AzureRmResourceGroupDeployment -TemplateUri $templateUri -siteName $siteName -ResourceGroupName $resourceGroupName

Write-Output "Web App Deployed successfully!!"

# AAD Authentication
####################

Add-Type -AssemblyName System.Web

$clientSecret = [System.Web.Security.Membership]::GeneratePassword(30,2).ToString()

try
{

    Write-Host "Creating AzureAD application..."

    $adApp = New-AzureRmADApplication -DisplayName $siteName -HomePage $azureSite -IdentifierUris $azureSite -Password $clientSecret

    Write-Host "AzureAD application created succesfully!!"
}
catch
{
    # Delete the deployed web app if Azure AD application fails
    Remove-AzureRmResource -ResourceGroupName $resourceGroupName -ResourceName $siteName -ResourceType Microsoft.Web/sites -Force

    Write-Host "Faiure occured in Azure AD application....Try again!!"

    exit

}

$clientId = $adApp.ApplicationId

$servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $clientId

# Web App Configuration
#######################
try
{

    Write-Host "Configuring deployed Web-App..."
    $webApp = Get-AzureRMWebAppSlot -ResourceGroupName $resourceGroupName -Name $siteName -Slot production -WarningAction SilentlyContinue

    $appSettingList = $webApp.SiteConfig.AppSettings

    $appSettings = @{}
    ForEach ($item in $appSettingList) {
        $appSettings[$item.Name] = $item.Value
    }
    $appSettings['ida:Tenant'] = $tenant
    $appSettings['ida:Audience'] = $azureSite
    $appSettings['ida:ServerName'] = $serverName
    $appSettings['ida:Domain'] = $domain
    $appSettings['ida:Username'] = $userName

    $connStrings = @{}
    $kvp = @{"Type"="Custom"; "Value"=$password}
    $connStrings['ida:Password'] = $kvp

    Set-AzureRMWebAppSlot -ResourceGroupName $resourceGroupName -Name $siteName -AppSettings $appSettings -ConnectionStrings $connStrings -Slot production -WarningAction SilentlyContinue

}
catch
{
    Write-Host "Web App configuration failed. Please ensure all values are provided in Service Manager Authentication Settings in User Configuration Section"

    # Delete the AzureRm AD Application if confiuration fails
    Remove-AzureRmADApplication -ObjectId $adApp.ObjectId -Force

    # Delete the deployed web app if configuration fails
    Remove-AzureRmResource -ResourceGroupName $resourceGroupName -ResourceName $siteName -ResourceType Microsoft.Web/sites -Force

    exit
}


# Relay Namespace
###################

if(!$serviceName)
{
    $serviceName = $siteName + "sbn"
}

$resourceProvider = Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Relay

if(!$resourceProvider -or $resourceProvider[0].RegistrationState -ne "Registered")
{
    try
    {
        Write-Host "Registering Microsoft.Relay Resource Provider"
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Relay
    }
    catch
    {
        Write-Host "Failed to Register Microsoft.Relay Resource Provider. Please register it in Azure Portal."
    }   
}

$resource = Find-AzureRmResource -ResourceNameContains $serviceName -ResourceType Microsoft.Relay/namespaces

if(!$resource)
{
    $serviceName = $siteName + "sbn"
    $properties = @{
        "sku" = @{
            "name"= "Standard"
            "tier"= "Standard"
            "capacity"= 1
         }
    }
    try
    {
        Write-Host "Creating Service Bus namespace..."
        New-AzureRmResource -ResourceName $serviceName -Location $location -PropertyObject $properties -ResourceGroupName $resourceGroupName -ResourceType Microsoft.Relay/namespaces -ApiVersion 2016-07-01 -Force
    }
    catch
    {
        $err = $TRUE
        Write-Host "Creation of Service Bus Namespace failed...Please create it manually from Azure Portal.`n"
    }

}

Write-Host "Note: Please Configure Hybrid connection in the Networking section of the web application in Azure Portal to link to the on-premises system.`n"
Write-Host "App Details"
Write-Host "============"
Write-Host "App Name:"  $siteName
Write-Host "Client Id:"  $clientId
Write-Host "Client Secret:"  $clientSecret
Write-Host "URI:"  $azureSite
if(!$err)
{
    Write-Host "ServiceBus Namespace:"  $serviceName  
}

```
## <a name="next-steps"></a><span data-ttu-id="9127d-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9127d-121">Next steps</span></span>
<span data-ttu-id="9127d-122">[Configuración de la conexión híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="9127d-122">[Configure the Hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>
