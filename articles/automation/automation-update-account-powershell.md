---
title: "aaaCreate Azure automatización de la cuenta de ejecución con PowerShell | Documentos de Microsoft"
description: "Este artículo describe cómo tooupgrade su cuenta de automatización con PowerShell toocreate hello ejecutar como cuentas si este paso no se llevó a cabo durante la creación inicial desde el portal de Hola."
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
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="91428-103">Actualización de una cuenta de ejecución de Automation mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="91428-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="91428-104">Puede usar PowerShell tooupdate su cuenta de automatización existente si:</span><span class="sxs-lookup"><span data-stu-id="91428-104">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="91428-105">Crear una cuenta de automatización, pero rechazar toocreate Hola cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="91428-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="91428-106">Ya utiliza un administrador de recursos toomanage cuenta recursos de automatización y desea tooupdate Hola cuenta tooinclude Hola cuenta de ejecución para la autenticación de runbook.</span><span class="sxs-lookup"><span data-stu-id="91428-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="91428-107">Ya utiliza un recursos clásicos de automatización de la cuenta toomanage y desea tooupdate se toouse Hola clásico cuenta de ejecución en lugar de crear una cuenta nueva y migrar su tooit runbooks y activos.</span><span class="sxs-lookup"><span data-stu-id="91428-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="91428-108">Toocreate que desee ejecutar como y una cuenta de identificación clásico mediante el uso de un certificado emitido por la entidad de certificación (CA) empresarial.</span><span class="sxs-lookup"><span data-stu-id="91428-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91428-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="91428-109">Prerequisites</span></span>

* <span data-ttu-id="91428-110">script de Hola se puede ejecutar solo en Windows 10 y Windows Server 2016 con módulos de Azure Resource Manager 2.01 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="91428-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="91428-111">No se admite en versiones anteriores de Windows.</span><span class="sxs-lookup"><span data-stu-id="91428-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="91428-112">Azure PowerShell 1.0 y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="91428-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="91428-113">Para obtener información acerca de la versión de Hola PowerShell 1.0, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91428-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="91428-114">Una cuenta de automatización, que se hace referencia como valor de Hola de hello *: AutomationAccountName* y *- ApplicationDisplayName* parámetros Hola siguiente script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91428-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="91428-115">Hola tooget los valores de *SubscriptionID*, *ResourceGroup*, y *AutomationAccountName*, que son parámetros necesarios para las secuencias de comandos de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="91428-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="91428-116">En el portal de Azure de Hola, seleccione su cuenta de automatización en hello **cuenta de automatización** hoja y, a continuación, seleccione **toda la configuración de**.</span><span class="sxs-lookup"><span data-stu-id="91428-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="91428-117">En hello **toda la configuración de** hoja, en **configuración de la cuenta**, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="91428-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="91428-118">Tenga en cuenta los valores de hello en hello **propiedades** hoja.</span><span class="sxs-lookup"><span data-stu-id="91428-118">Note hello values on hello **Properties** blade.</span></span>

![hoja de "Propiedades" de cuenta de automatización de Hola](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="91428-120">Creación de un script de PowerShell de una cuenta de ejecución</span><span class="sxs-lookup"><span data-stu-id="91428-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="91428-121">Este script de PowerShell incluye compatibilidad para hello siguiendo configuraciones:</span><span class="sxs-lookup"><span data-stu-id="91428-121">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="91428-122">Creación de una cuenta de ejecución mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="91428-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="91428-123">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="91428-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="91428-124">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa.</span><span class="sxs-lookup"><span data-stu-id="91428-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="91428-125">Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government.</span><span class="sxs-lookup"><span data-stu-id="91428-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="91428-126">Dependiendo de la opción de configuración de Hola que seleccione, el script de Hola crea Hola siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="91428-126">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="91428-127">**Para cuentas de ejecución:**</span><span class="sxs-lookup"><span data-stu-id="91428-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="91428-128">Crea un Azure AD aplicación toobe exportado con cualquier hello autofirmado o clave pública del certificado de la empresa, crea una cuenta de entidad de servicio para la aplicación hello en Azure AD y asigna Hola rol Colaborador para cuenta de hello en el actual suscripción.</span><span class="sxs-lookup"><span data-stu-id="91428-128">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="91428-129">Puede cambiar esta configuración tooOwner o cualquier otro rol.</span><span class="sxs-lookup"><span data-stu-id="91428-129">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="91428-130">Para más información, consulte [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="91428-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="91428-131">Crea un activo de certificado de automatización denominado *AzureRunAsCertificate* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="91428-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="91428-132">activo de certificado de Hello contiene la clave privada de hello certificado utilizado por la aplicación hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91428-132">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="91428-133">Crea un recurso de conexión de automatización denominado *AzureRunAsConnection* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="91428-133">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="91428-134">activo de conexión de Hello contiene applicationId hello, tenantId, Id. de suscripción y la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="91428-134">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="91428-135">**Para cuentas de ejecución clásicas:**</span><span class="sxs-lookup"><span data-stu-id="91428-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="91428-136">Crea un activo de certificado de automatización denominado *AzureClassicRunAsCertificate* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="91428-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="91428-137">activo de certificado de Hello contiene la clave privada del certificado Hola utilizado por el certificado de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="91428-137">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="91428-138">Crea un recurso de conexión de automatización denominado *AzureClassicRunAsConnection* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="91428-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="91428-139">activo de conexión de Hello contiene el nombre de la suscripción de hello, Id. de suscripción y el nombre del recurso de certificado.</span><span class="sxs-lookup"><span data-stu-id="91428-139">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="91428-140">Si selecciona cualquiera de las opciones para crear una cuenta de identificación clásico, después de ejecuta script de Hola, carga Hola certificado público almacén de administración de toohello (extensión de nombre de archivo .cer) para suscripción Hola esa cuenta de automatización de Hola se creó en.</span><span class="sxs-lookup"><span data-stu-id="91428-140">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="91428-141">Guardar Hola siguiente secuencia de comandos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="91428-141">Save hello following script on your computer.</span></span> <span data-ttu-id="91428-142">En este ejemplo, guárdelo con el nombre de archivo de hello *RunAsAccount.ps1 nuevo*.</span><span class="sxs-lookup"><span data-stu-id="91428-142">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
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
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

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

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="91428-143">En el equipo, inicie **Windows PowerShell** de hello **iniciar** pantalla con derechos de usuario elevados.</span><span class="sxs-lookup"><span data-stu-id="91428-143">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="91428-144">De hello elevado shell de línea de comandos, vaya toohello carpeta que contiene el script de Hola que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="91428-144">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="91428-145">Ejecutar script de Hola mediante el uso de valores de parámetro de hello para la configuración de Hola que necesite.</span><span class="sxs-lookup"><span data-stu-id="91428-145">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="91428-146">**Creación de una cuenta de ejecución mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="91428-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="91428-147">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="91428-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="91428-148">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa**</span><span class="sxs-lookup"><span data-stu-id="91428-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="91428-149">**Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government**</span><span class="sxs-lookup"><span data-stu-id="91428-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="91428-150">Una vez ejecutado el script de Hola, será tooauthenticate solicitada con Azure.</span><span class="sxs-lookup"><span data-stu-id="91428-150">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="91428-151">Inicie sesión con una cuenta que sea miembro del rol de administradores de suscripción de Hola y Coadministrador de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="91428-151">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="91428-152">Después de que el script de Hola se ha ejecutado correctamente, observe Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="91428-152">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="91428-153">Si ha creado una cuenta de identificación clásico con un certificado autofirmado público (archivo .cer), el script de Hola crea y guarda toohello carpeta de archivos temporales en el equipo en el perfil de usuario de hello *%USERPROFILE%\AppData\Local\Temp*, que ya ha utilizado la sesión de PowerShell de tooexecute Hola.</span><span class="sxs-lookup"><span data-stu-id="91428-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="91428-154">Si creó una cuenta de identificación clásica con un certificado público de empresa (archivo .cer) , use este certificado.</span><span class="sxs-lookup"><span data-stu-id="91428-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="91428-155">Siga las instrucciones de Hola para [cargar una toohello de certificado de la API de administración portal de Azure clásico](../azure-api-management-certs.md)y, a continuación, validar configuración de credencial de hello con recursos de implementación clásica mediante hello [código de ejemplo tooauthenticate con recursos de implementación de Azure clásico](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="91428-155">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="91428-156">Si lo hizo *no* crear una cuenta de identificación clásico, autenticar con recursos de administrador de recursos y validar la configuración de credencial de hello mediante hello [código de ejemplo para autenticar con la administración de servicios recursos](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="91428-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91428-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91428-157">Next steps</span></span>
* <span data-ttu-id="91428-158">Para obtener más información acerca de las entidades de servicio, consulte demasiado[objetos de entidad de servicio y aplicación](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="91428-158">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="91428-159">Para obtener más información sobre los certificados y servicios de Azure, consulte demasiado[Introducción a los certificados para servicios en la nube](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="91428-159">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
