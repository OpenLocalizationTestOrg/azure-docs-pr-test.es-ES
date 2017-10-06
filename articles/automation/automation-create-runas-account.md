---
title: "aaaCreate Azure Automation cuentas de ejecución | Documentos de Microsoft"
description: "Este artículo se describe cómo tooupdate la automatización de la cuenta y crear cuentas de ejecución con PowerShell o desde el portal de Hola."
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
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a>Actualizar la autenticación de la cuenta de Automation con cuentas de ejecución 
Puede actualizar su cuenta de automatización existente desde el portal de Hola o usar PowerShell si:

* Crear una cuenta de automatización, pero rechazar toocreate Hola cuenta de ejecución.
* Ya utiliza un administrador de recursos toomanage cuenta recursos de automatización y desea tooupdate Hola cuenta tooinclude Hola cuenta de ejecución para la autenticación de runbook.
* Ya utiliza un recursos clásicos de automatización de la cuenta toomanage y desea tooupdate se toouse Hola clásico cuenta de ejecución en lugar de crear una cuenta nueva y migrar su tooit runbooks y activos.   
* Toocreate que desee ejecutar como y una cuenta de identificación clásico mediante el uso de un certificado emitido por la entidad de certificación (CA) empresarial.

## <a name="prerequisites"></a>Requisitos previos

* script de Hola puede ejecutar solo en Windows 10 y Windows Server 2016 con módulos de Azure Resource Manager 3.0.0 y versiones posteriores. No se admite en versiones anteriores de Windows.
* Azure PowerShell 1.0 y versiones superiores. Para obtener información acerca de la versión de Hola PowerShell 1.0, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).
* Una cuenta de automatización, que se hace referencia como valor de Hola de hello *: AutomationAccountName* y *- ApplicationDisplayName* parámetros Hola siguiente script de PowerShell.

Hola tooget los valores de *SubscriptionID*, *ResourceGroup*, y *AutomationAccountName*, que son parámetros necesarios para la secuencia de comandos de hello, Hola siguientes:

1. En el portal de Azure de Hola, seleccione su cuenta de automatización en hello **cuenta de automatización** hoja y, a continuación, seleccione **toda la configuración de**.  
2. En hello **toda la configuración de** hoja, en **configuración de la cuenta**, seleccione **propiedades**. 
3. Tenga en cuenta los valores de hello en hello **propiedades** hoja.<br><br> ![hoja de "Propiedades" de cuenta de automatización de Hola](media/automation-create-runas-account/automation-account-properties.png)  

### <a name="required-permissions-tooupdate-your-automation-account"></a>Requiere permisos tooupdate su cuenta de automatización
tooupdate una cuenta de automatización, debe tener Hola después determinados privilegios y permisos necesarios toocomplete en este tema.   
 
* Su cuenta de usuario de AD necesita toobe tooa agregado rol con el rol de colaborador de toohello equivalente de permisos para recursos de Microsoft.Automation tal como se describe en el artículo [control de acceso basado en roles en automatización de Azure](automation-role-based-access-control.md#contributor-role-permissions).  
* Los usuarios sin privilegios de administrador en el inquilino de Azure AD pueden [registrar aplicaciones AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) si los registros de aplicación Hola configuración se establece demasiado**Sí**.  Si los registros de aplicación Hola configuración se establece demasiado**n**, usuario Hola realizar esta acción debe ser un administrador global de Azure AD. 

Si no eres un miembro de instancia de Active Directory de la suscripción de hello antes de que se agreguen toohello global administrador o coadministrator-administrator roles de suscripción de hello, se agregan tooActive directorio como invitado. En este caso, recibirá un "no tiene permisos toocreate..." Advertencia de hello **agregar una cuenta de automatización** hoja. Los usuarios que se agregaron toohello global administrador o coadministrator-administrator roles en primer lugar se pueden quitar de la instancia de Active Directory de la suscripción de Hola y vuelva a agregan toomake a un usuario en Active Directory completo. tooverify esta situación, hello **Azure Active Directory** panel Hola portal de Azure, seleccione **usuarios y grupos**, seleccione **todos los usuarios** y, después de seleccionar Hola un usuario específico, seleccione **perfil**. Hola valo hello **tipo de usuario** atributo en el perfil de los usuarios de hello no debería ser igual **invitado**.

## <a name="create-run-as-account-from-hello-portal"></a>Crear cuenta de ejecución desde el portal de Hola
En esta sección, realizar Hola siguiendo los pasos tooupdate su cuenta de automatización de Azure desde Hola portal de Azure.  Crear Hola identificación clásico y ejecutar como cuentas individualmente y si no necesita recursos toomanage en portal de Azure clásico hello, solo puede crear hello Azure cuenta de ejecución.  

proceso de Hello crea Hola siguientes elementos en su cuenta de automatización.

**Para cuentas de ejecución:**

* Crea una aplicación de Azure AD con un certificado autofirmado, crea una cuenta de entidad de servicio para la aplicación hello en Azure AD y asigna el rol de colaborador de hello para la cuenta de hello en su suscripción actual. Puede cambiar esta configuración tooOwner o cualquier otro rol. Para más información, consulte [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md).
* Crea un activo de certificado de automatización denominado *AzureRunAsCertificate* en hello especifica la cuenta de automatización. activo de certificado de Hello contiene la clave privada de hello certificado utilizado por la aplicación hello Azure AD.
* Crea un recurso de conexión de automatización denominado *AzureRunAsConnection* en hello especifica la cuenta de automatización. activo de conexión de Hello contiene applicationId hello, tenantId, Id. de suscripción y la huella digital del certificado.

**Para cuentas de ejecución clásicas:**

* Crea un activo de certificado de automatización denominado *AzureClassicRunAsCertificate* en hello especifica la cuenta de automatización. activo de certificado de Hello contiene la clave privada del certificado Hola utilizado por el certificado de administración de Hola.
* Crea un recurso de conexión de automatización denominado *AzureClassicRunAsConnection* en hello especifica la cuenta de automatización. activo de conexión de Hello contiene el nombre de la suscripción de hello, Id. de suscripción y el nombre del recurso de certificado.

1. Inicie sesión en toohello portal de Azure con una cuenta que sea miembro del rol de los administradores de suscripciones de Hola y Coadministrador de suscripción de Hola.
2. En la hoja de la cuenta de automatización de hello, seleccione **cuentas de ejecución** en la sección de hello **configuración de la cuenta**.  
3. En función de la cuenta que necesite, seleccione **Cuenta de ejecución de Azure** o **Cuenta de ejecución de Azure clásica**.  Después de seleccionar cualquier hello **agregar Azure identificación** o **agregar clásico ejecutar como cuenta de Azure** hoja aparece y después de revisar la información general de hello, haga clic en **crear** tooproceed con la creación de cuentas de ejecución.  
4. Mientras Azure crea la cuenta de identificación de hello, puede seguir el progreso de hello en **notificaciones** de hello menú y un banner se muestra que indica que se está creando la cuenta de hello.  Este proceso puede tardar unos toocomplete minutos.  

## <a name="create-run-as-account-using-powershell-script"></a>Creación de una cuenta de ejecución con un script de PowerShell
Este script de PowerShell incluye compatibilidad para hello siguiendo configuraciones:

* Creación de una cuenta de ejecución mediante un certificado autofirmado.
* Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado.
* Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa.
* Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government.

Dependiendo de la opción de configuración de Hola que seleccione, el script de Hola crea Hola siguientes elementos.

**Para cuentas de ejecución:**

* Crea un Azure AD aplicación toobe exportado con cualquier hello autofirmado o clave pública del certificado de la empresa, crea una cuenta de entidad de servicio para la aplicación hello en Azure AD y asigna Hola rol Colaborador para cuenta de hello en el actual suscripción. Puede cambiar esta configuración tooOwner o cualquier otro rol. Para más información, consulte [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md).
* Crea un activo de certificado de automatización denominado *AzureRunAsCertificate* en hello especifica la cuenta de automatización. activo de certificado de Hello contiene la clave privada de hello certificado utilizado por la aplicación hello Azure AD.
* Crea un recurso de conexión de automatización denominado *AzureRunAsConnection* en hello especifica la cuenta de automatización. activo de conexión de Hello contiene applicationId hello, tenantId, Id. de suscripción y la huella digital del certificado.

**Para cuentas de ejecución clásicas:**

* Crea un activo de certificado de automatización denominado *AzureClassicRunAsCertificate* en hello especifica la cuenta de automatización. activo de certificado de Hello contiene la clave privada del certificado Hola utilizado por el certificado de administración de Hola.
* Crea un recurso de conexión de automatización denominado *AzureClassicRunAsConnection* en hello especifica la cuenta de automatización. activo de conexión de Hello contiene el nombre de la suscripción de hello, Id. de suscripción y el nombre del recurso de certificado.

>[!NOTE]
> Si selecciona cualquiera de las opciones para crear una cuenta de identificación clásico, después de ejecuta script de Hola, carga Hola certificado público almacén de administración de toohello (extensión de nombre de archivo .cer) para suscripción Hola esa cuenta de automatización de Hola se creó en.
> 

1. Guardar Hola siguiente secuencia de comandos en el equipo. En este ejemplo, guárdelo con el nombre de archivo de hello *RunAsAccount.ps1 nuevo*.

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
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
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
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. En el equipo, inicie **Windows PowerShell** de hello **iniciar** pantalla con derechos de usuario elevados.
3. De hello elevado shell de línea de comandos, vaya toohello carpeta que contiene el script de Hola que creó en el paso 1.  
4. Ejecutar script de Hola mediante el uso de valores de parámetro de hello para la configuración de Hola que necesite.

    **Creación de una cuenta de ejecución mediante un certificado autofirmado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Una vez ejecutado el script de Hola, será tooauthenticate solicitada con Azure. Inicie sesión con una cuenta que sea miembro del rol de administradores de suscripción de Hola y Coadministrador de suscripción de Hola.
    >
    >

Después de que el script de Hola se ha ejecutado correctamente, observe Hola siguiente:
* Si ha creado una cuenta de identificación clásico con un certificado autofirmado público (archivo .cer), el script de Hola crea y guarda toohello carpeta de archivos temporales en el equipo en el perfil de usuario de hello *%USERPROFILE%\AppData\Local\Temp*, que ya ha utilizado la sesión de PowerShell de tooexecute Hola.
* Si creó una cuenta de identificación clásica con un certificado público de empresa (archivo .cer) , use este certificado. Siga las instrucciones de Hola para [cargar una toohello de certificado de la API de administración portal de Azure clásico](../azure-api-management-certs.md)y, a continuación, validar configuración de credencial de hello con recursos de implementación clásica mediante hello [código de ejemplo tooauthenticate con recursos de implementación de Azure clásico](automation-verify-runas-authentication.md#classic-run-as-authentication). 
* Si lo hizo *no* crear una cuenta de identificación clásico, autenticar con recursos de administrador de recursos y validar la configuración de credencial de hello mediante hello [código de ejemplo para autenticar con la administración de servicios recursos](automation-verify-runas-authentication.md#automation-run-as-authentication).

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información acerca de las entidades de servicio, consulte demasiado[objetos de entidad de servicio y aplicación](../active-directory/active-directory-application-objects.md).
* Para obtener más información sobre los certificados y servicios de Azure, consulte demasiado[Introducción a los certificados para servicios en la nube](../cloud-services/cloud-services-certs-create.md).
