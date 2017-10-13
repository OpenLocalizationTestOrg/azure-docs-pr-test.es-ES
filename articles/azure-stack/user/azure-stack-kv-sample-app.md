---
title: "Permitir a aplicaciones recuperar secretos del almacén de claves de Azure Stack | Microsoft Docs"
description: "Usar una aplicación de ejemplo para trabajar con el almacén de claves de Azure Stack"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2017
ms.author: sngun
ms.openlocfilehash: 7cfb78cc5219d4adab5ceddc9d7eb8d1fc71b678
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="sample-application-that-uses-keys-and-secrets-stored-in-a-key-vault"></a><span data-ttu-id="8cb00-103">Aplicación de ejemplo que usa claves y secretos almacenados en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="8cb00-103">Sample application that uses keys and secrets stored in a key vault</span></span>

<span data-ttu-id="8cb00-104">En este artículo, le mostraremos cómo ejecutar una aplicación de ejemplo (HelloKeyVault) que recupera las claves y secretos de un almacén de claves en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8cb00-104">In this article, we show you how to run a sample application (HelloKeyVault) that retrieves keys and secrets from a key vault in Azure Stack.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cb00-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8cb00-105">Prerequisites</span></span> 

<span data-ttu-id="8cb00-106">Implemente los siguientes requisitos previos desde el [kit de desarrollo](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) o desde un cliente externo basado en Windows, si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="8cb00-106">Run the following prerequisites either from the [Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="8cb00-107">Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="8cb00-107">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="8cb00-108">Descargue las [herramientas necesarias para trabajar con Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="8cb00-108">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="create-and-get-the-key-vault-and-application-settings"></a><span data-ttu-id="8cb00-109">Creación y obtención del almacén de claves y la configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8cb00-109">Create and get the key vault and application settings</span></span>

<span data-ttu-id="8cb00-110">En primer lugar, debe crear un almacén de claves en Azure Stack y registrar una aplicación en Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8cb00-110">First, you should create a key vault in Azure Stack, and register an application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8cb00-111">Puede crear y registrar los almacenes de claves mediante Azure Portal o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cb00-111">You can create and register the key vaults by using the Azure portal or PowerShell.</span></span> <span data-ttu-id="8cb00-112">En este artículo se muestra la forma de hacer las tareas de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cb00-112">This article shows you the PowerShell way to do the tasks.</span></span> <span data-ttu-id="8cb00-113">De forma predeterminada, este script de PowerShell crea una aplicación nueva en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8cb00-113">By default, this PowerShell script creates a new application in Active Directory.</span></span> <span data-ttu-id="8cb00-114">Sin embargo, también puede usar una de las aplicaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="8cb00-114">However, you can also use one of your existing applications.</span></span> <span data-ttu-id="8cb00-115">Asegúrese de proporcionar un valor para las variables `aadTenantName` y `applicationPassword`.</span><span class="sxs-lookup"><span data-stu-id="8cb00-115">Make sure to provide a value for the `aadTenantName` and `applicationPassword` variables.</span></span> <span data-ttu-id="8cb00-116">Si no especifica ningún valor para la variable `applicationPassword` este script generará una contraseña aleatoria.</span><span class="sxs-lookup"><span data-stu-id="8cb00-116">If you don't specify a value for the `applicationPassword` variable, this script generates a random password.</span></span> 

```powershell
$vaultName           = 'myVault'
$resourceGroupName   = 'myResourceGroup'
$applicationName     = 'myApp'
$location            = 'local' 

# Password for the application. If not specified, this script will generate a random password during app creation.
$applicationPassword = '' 
                         
# Function to generate a random password for the application.
Function GenerateSymmetricKey()
{
    $key = New-Object byte[](32)
    $rng = [System.Security.Cryptography.RNGCryptoServiceProvider]::Create()
    $rng.GetBytes($key)
    return [System.Convert]::ToBase64String($key)
}

Write-Host 'Please log into your Azure Stack user environment' -foregroundcolor Green

$tenantARM = "https://management.local.azurestack.external"
$aadTenantName = "PLEASE FILL THIS IN WITH YOUR AAD TENANT NAME. FOR EXAMPLE: myazurestack.onmicrosoft.com"

# Configure the Azure Stack operator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackUser" `
  -ArmEndpoint $tenantARM

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $aadTenantName `
  -EnvironmentName AzureStackUser

# Sign in to the user portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackUser" `
  -TenantId $TenantID `
  
$now = [System.DateTime]::Now
$oneYearFromNow = $now.AddYears(1)

$applicationPassword = GenerateSymmetricKey
    
# Create a new Azure AD application.
$identifierUri = [string]::Format("http://localhost:8080/{0}",[Guid]::NewGuid().ToString("N"))
$homePage = "http://contoso.com"

Write-Host "Creating a new AAD Application"
$ADApp = New-AzureRmADApplication `
  -DisplayName $applicationName `
  -HomePage $homePage `
  -IdentifierUris $identifierUri `
  -StartDate $now `
  -EndDate $oneYearFromNow `
  -Password $applicationPassword

Write-Host "Creating a new AAD service principal"
$servicePrincipal = New-AzureRmADServicePrincipal `
  -ApplicationId $ADApp.ApplicationId

# Create a new resource group and a key vault within that resource group.
New-AzureRmResourceGroup `
  -Name $resourceGroupName `
  -Location $location   

Write-Host "Creating vault $vaultName"
$vault = New-AzureRmKeyVault -VaultName $vaultName `
  -ResourceGroupName $resourceGroupName `
  -Sku standard `
  -Location $location

# Specify full privileges to the vault for the application.
Write-Host "Setting access policy"
Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName `
  -ObjectId $servicePrincipal.Id `
  -PermissionsToKeys all `
  -PermissionsToSecrets all

Write-Host "Paste the following settings into the app.config file for the HelloKeyVault project:"
'<add key="VaultUrl" value="' + $vault.VaultUri + '"/>'
'<add key="AuthClientId" value="' + $servicePrincipal.ApplicationId + '"/>'
'<add key="AuthClientSecret" value="' + $applicationPassword + '"/>'
Write-Host

``` 

<span data-ttu-id="8cb00-117">La captura de pantalla siguiente muestra la salida del script anterior:</span><span class="sxs-lookup"><span data-stu-id="8cb00-117">The following screenshot shows the output of the previous script:</span></span>

![Configuración de la aplicación](media/azure-stack-kv-sample-app/settingsoutput.png)

<span data-ttu-id="8cb00-119">Tome nota de los valores de **VaultUrl**, **AuthClientId** y **AuthClientSecret** que devolvió el script anterior.</span><span class="sxs-lookup"><span data-stu-id="8cb00-119">Make a note of the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span></span> <span data-ttu-id="8cb00-120">Para ejecutar la aplicación HelloKeyVault, utilizará estos valores.</span><span class="sxs-lookup"><span data-stu-id="8cb00-120">You use these values to run the HelloKeyVault application.</span></span>

## <a name="download-and-run-the-sample-application"></a><span data-ttu-id="8cb00-121">Descarga y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8cb00-121">Download and run the sample application</span></span>

<span data-ttu-id="8cb00-122">Descargue el ejemplo de almacén de claves de la página de Azure [Key vault client samples](https://www.microsoft.com/en-us/download/details.aspx?id=45343) (ejemplos de cliente del almacén de claves).</span><span class="sxs-lookup"><span data-stu-id="8cb00-122">Download the key vault sample from the Azure [Key Vault client samples](https://www.microsoft.com/en-us/download/details.aspx?id=45343) page.</span></span> <span data-ttu-id="8cb00-123">Extraiga el contenido del archivo .zip en la estación de trabajo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="8cb00-123">Extract the contents of the .zip file onto your development workstation.</span></span> <span data-ttu-id="8cb00-124">Hay dos ejemplos dentro de la carpeta de ejemplos.</span><span class="sxs-lookup"><span data-stu-id="8cb00-124">There are two samples within the samples folder.</span></span> <span data-ttu-id="8cb00-125">En este tema, usamos el ejemplo HellpKeyVault.</span><span class="sxs-lookup"><span data-stu-id="8cb00-125">We use the HellpKeyVault sample in this topic.</span></span> <span data-ttu-id="8cb00-126">Navegue hasta los ejemplos **Microsoft.Azure.KeyVault.Samples** > **, carpeta**  > **HelloKeyVault** y abra la aplicación HelloKeyVault en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8cb00-126">Browse to the **Microsoft.Azure.KeyVault.Samples** > **samples** > **HelloKeyVault** folder and open the HelloKeyVault application in Visual Studio.</span></span> 

<span data-ttu-id="8cb00-127">Abra el archivo HelloKeyVault\App.config y reemplace los valores del elemento <appSettings> con los valores de **VaultUrl**, **AuthClientId** y **AuthClientSecret**devueltos por el script anterior.</span><span class="sxs-lookup"><span data-stu-id="8cb00-127">Open the HelloKeyVault\App.config file and replace the values of the <appSettings> element with the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span></span> <span data-ttu-id="8cb00-128">Tenga en cuenta que, de forma predeterminada, el archivo App.config contiene el marcador de posición para *AuthCertThumbprint*, pero usará *AuthClientSecret* en su lugar.</span><span class="sxs-lookup"><span data-stu-id="8cb00-128">Note that by default the App.config contains a placeholder for *AuthCertThumbprint*, but use *AuthClientSecret* instead.</span></span> <span data-ttu-id="8cb00-129">Después de reemplazar la configuración, vuelva a compilar la solución e inicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8cb00-129">After you replace the settings, rebuild the solution and start the application.</span></span>

![Configuración de la aplicación](media/azure-stack-kv-sample-app/appconfig.png)
 
<span data-ttu-id="8cb00-131">La aplicación inicia una sesión en Azure AD y, a continuación, utiliza ese token para autenticarse en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8cb00-131">The application signs in to Azure AD, and then uses that token to authenticate to the key vault in Azure Stack.</span></span> <span data-ttu-id="8cb00-132">La aplicación realiza las operaciones, como crear, cifrar, ajustar y eliminar, en las claves y secretos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="8cb00-132">The application performs operations like create, encrypt, wrap, and delete on the keys and secrets of the key vault.</span></span> <span data-ttu-id="8cb00-133">También puede pasar parámetros específicos, como *encrypt* y *decrypt* a la aplicación, lo que asegura que la aplicación ejecuta solo esas operaciones en el almacén.</span><span class="sxs-lookup"><span data-stu-id="8cb00-133">You can also pass specific parameters such as *encrypt* and *decrypt* to the application, which makes sure that the application executes only those operations against the vault.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="8cb00-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8cb00-134">Next steps</span></span>
[<span data-ttu-id="8cb00-135">Implementación de una máquina virtual con una contraseña de Key Vault</span><span class="sxs-lookup"><span data-stu-id="8cb00-135">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="8cb00-136">Implementación de una máquina virtual con un certificado de Key Vault</span><span class="sxs-lookup"><span data-stu-id="8cb00-136">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)



