---
title: "Creación de una cuenta de ejecución de Azure Automation con PowerShell | Microsoft Docs"
description: "En este artículo se describe cómo actualizar la cuenta de Automation con PowerShell para crear cuentas de ejecución si no ha realizado este paso durante la creación inicial desde el portal."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: a41a57ee3815a815c23e9bbe2dd0309e6c61c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="b79ac-103">Actualización de una cuenta de ejecución de Automation mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b79ac-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="b79ac-104">Puede usar PowerShell para actualizar su cuenta de Automation existente si:</span><span class="sxs-lookup"><span data-stu-id="b79ac-104">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="b79ac-105">Crea una cuenta de Automation, pero se rechaza la creación de la cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="b79ac-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="b79ac-106">Ya usa una cuenta de Automation para administrar recursos de Resource Manager y quiere actualizarla para incluir la cuenta de ejecución para la autenticación de runbooks.</span><span class="sxs-lookup"><span data-stu-id="b79ac-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="b79ac-107">Ya usa una cuenta de Automation para administrar recursos del modelo clásico y quiere actualizarla para usar la cuenta de ejecución en lugar de crear una nueva cuenta y migrar los runbooks y recursos a ella.</span><span class="sxs-lookup"><span data-stu-id="b79ac-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="b79ac-108">Quiere crear una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado emitido por una entidad de certificación (CA) de empresa.</span><span class="sxs-lookup"><span data-stu-id="b79ac-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b79ac-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b79ac-109">Prerequisites</span></span>

* <span data-ttu-id="b79ac-110">El script solo se puede ejecutar en Windows 10 y Windows Server 2016 con módulos de Azure Resource Manager 2.01 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="b79ac-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="b79ac-111">No se admite en versiones anteriores de Windows.</span><span class="sxs-lookup"><span data-stu-id="b79ac-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="b79ac-112">Azure PowerShell 1.0 y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="b79ac-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="b79ac-113">Para más información sobre la versión 1.0 de PowerShell, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b79ac-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b79ac-114">Una cuenta de Automation, a la que se hace referencia como el valor de los parámetros *: -AutomationAccountName* y *- ApplicationDisplayName* en el siguiente script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b79ac-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="b79ac-115">Para obtener los valores de *SubscriptionID*, *ResourceGroup* y *AutomationAccountName*, que son parámetros necesarios para los scripts, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b79ac-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="b79ac-116">En el portal de Azure, seleccione su cuenta de Automation en la hoja **Cuenta de Automation** y luego seleccione **All settings** (Toda la configuración).</span><span class="sxs-lookup"><span data-stu-id="b79ac-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="b79ac-117">En la hoja **All settings** (Toda la configuración), en **Account Settings** (Configuración de la cuenta), seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="b79ac-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="b79ac-118">Tenga en cuenta los valores de la hoja **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="b79ac-118">Note the values on the **Properties** blade.</span></span>

![Hoja "Propiedades" de la cuenta de Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="b79ac-120">Creación de un script de PowerShell de una cuenta de ejecución</span><span class="sxs-lookup"><span data-stu-id="b79ac-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="b79ac-121">Este script de PowerShell incluye compatibilidad con las siguientes configuraciones:</span><span class="sxs-lookup"><span data-stu-id="b79ac-121">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="b79ac-122">Creación de una cuenta de ejecución mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="b79ac-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="b79ac-123">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="b79ac-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="b79ac-124">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa.</span><span class="sxs-lookup"><span data-stu-id="b79ac-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="b79ac-125">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado en la nube de Azure Government.</span><span class="sxs-lookup"><span data-stu-id="b79ac-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="b79ac-126">Dependiendo de la opción de configuración seleccionada, el script crea los siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="b79ac-126">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="b79ac-127">**Para cuentas de ejecución:**</span><span class="sxs-lookup"><span data-stu-id="b79ac-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="b79ac-128">Crea una aplicación de Azure AD que se exporta con la clave pública del certificado autofirmado o de empresa, crea una cuenta de entidad de servicio para esta aplicación en Azure AD y asigna el rol Colaborador para esta cuenta en su suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="b79ac-128">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="b79ac-129">Puede cambiar esta configuración a Propietario o cualquier otro rol.</span><span class="sxs-lookup"><span data-stu-id="b79ac-129">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="b79ac-130">Para más información, consulte [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="b79ac-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="b79ac-131">Crea un recurso de certificado de Automation llamado *AzureRunAsCertificate* en la cuenta de Automation especificada.</span><span class="sxs-lookup"><span data-stu-id="b79ac-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="b79ac-132">El recurso de certificado contiene la clave privada del certificado que usa la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b79ac-132">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="b79ac-133">Crea un recurso de conexión de Automation llamado *AzureRunAsConnection* en la cuenta de Automation especificada.</span><span class="sxs-lookup"><span data-stu-id="b79ac-133">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="b79ac-134">El recurso de conexión contiene el id. de aplicación, el id. de inquilino, el id. de suscripción y la huella digital de certificado.</span><span class="sxs-lookup"><span data-stu-id="b79ac-134">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="b79ac-135">**Para cuentas de ejecución clásicas:**</span><span class="sxs-lookup"><span data-stu-id="b79ac-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="b79ac-136">Crea un recurso de certificado de Automation llamado *AzureClassicRunAsCertificate* en la cuenta de Automation especificada.</span><span class="sxs-lookup"><span data-stu-id="b79ac-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="b79ac-137">El recurso de certificado contiene la clave privada del certificado que usa el certificado de administración.</span><span class="sxs-lookup"><span data-stu-id="b79ac-137">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="b79ac-138">Crea un recurso de conexión de Automation llamado *AzureClassicRunAsConnection* en la cuenta de Automation especificada.</span><span class="sxs-lookup"><span data-stu-id="b79ac-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="b79ac-139">El recurso de conexión contiene el nombre de la suscripción, el id. de suscripción y el nombre del recurso de certificado.</span><span class="sxs-lookup"><span data-stu-id="b79ac-139">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="b79ac-140">Si selecciona cualquiera de las opciones para crear una cuenta de ejecución clásica, cargue el certificado público (extensión de nombre del archivo .cer) en el almacén de administración para la suscripción en la que se creó la cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="b79ac-140">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="b79ac-141">Guarde el script siguiente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b79ac-141">Save the following script on your computer.</span></span> <span data-ttu-id="b79ac-142">En este ejemplo, guárdelo con el nombre *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="b79ac-142">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                    "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload the .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="b79ac-143">En el equipo, inicie **Windows PowerShell** desde la pantalla **Inicio** con permisos de usuario elevados.</span><span class="sxs-lookup"><span data-stu-id="b79ac-143">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="b79ac-144">Desde el shell de línea de comandos con privilegios elevados, vaya a la carpeta que contiene el script que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="b79ac-144">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="b79ac-145">Ejecute el script mediante los valores de parámetro de la configuración que necesita.</span><span class="sxs-lookup"><span data-stu-id="b79ac-145">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="b79ac-146">**Creación de una cuenta de ejecución mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="b79ac-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="b79ac-147">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="b79ac-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="b79ac-148">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa**</span><span class="sxs-lookup"><span data-stu-id="b79ac-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="b79ac-149">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado en la nube de Azure Government**</span><span class="sxs-lookup"><span data-stu-id="b79ac-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="b79ac-150">Después de ejecutar el script, se le pedirá que se autentique en Azure.</span><span class="sxs-lookup"><span data-stu-id="b79ac-150">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="b79ac-151">Inicie sesión con una cuenta que sea miembro del rol Administradores de suscripciones y coadministrador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b79ac-151">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="b79ac-152">Una vez que el script se ejecuta correctamente, observe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b79ac-152">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="b79ac-153">Si creó una cuenta de ejecución clásica con un certificado público autofirmado (formato .cer), el script lo crea y lo guarda en la carpeta de archivos temporales del equipo con el perfil de usuario *%USERPROFILE%\AppData\Local\Temp*, que se usa para ejecutar la sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b79ac-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="b79ac-154">Si creó una cuenta de identificación clásica con un certificado público de empresa (archivo .cer) , use este certificado.</span><span class="sxs-lookup"><span data-stu-id="b79ac-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="b79ac-155">Siga las instrucciones para [cargar un certificado de API de administración en el Portal de Azure clásico](../azure-api-management-certs.md) y luego valide la configuración de credenciales con recursos de implementación clásicos mediante el [código de ejemplo para realizar la autenticación con recursos del modelo de implementación clásica de Azure](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="b79ac-155">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="b79ac-156">Si *no* creó una cuenta de ejecución clásica, realice la autenticación con recursos de Resource Manager y valide la configuración de credenciales mediante el [código de ejemplo para la autenticación con recursos de Service Management](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="b79ac-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b79ac-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b79ac-157">Next steps</span></span>
* <span data-ttu-id="b79ac-158">Para más información acerca de las entidades de servicio, consulte [Objetos Application y objetos ServicePrincipal](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="b79ac-158">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="b79ac-159">Para más información acerca de los certificados y de los servicios de Azure, consulte [Introducción a los certificados para los servicios en la nube de Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="b79ac-159">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
