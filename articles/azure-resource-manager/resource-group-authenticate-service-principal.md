---
title: "aaaCreate identidad de aplicación de Azure con PowerShell | Documentos de Microsoft"
description: "Describe cómo controlan toouse Azure PowerShell toocreate una aplicación de Azure Active Directory y entidad de servicio y lo acceso tooresources a través del acceso basado en roles. Muestra cómo tooauthenticate aplicación con una contraseña o un certificado."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de PowerShell de Azure

Cuando haya una aplicación o un script que necesita tooaccess recursos, puede configurar una identidad para la aplicación hello y autenticar la aplicación hello con sus propias credenciales. Esta identidad se conoce como una entidad de servicio. Este enfoque le permite:

* Asignar permisos de identidad de aplicación de toohello que son diferentes de sus propios permisos. Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo.
* Usar un certificado para la autenticación al ejecutar un script desatendido.

Este tema muestra cómo toouse [Azure PowerShell](/powershell/azure/overview) tooset todo lo que necesita para una toorun de aplicación en sus propias credenciales y la identidad.

## <a name="required-permissions"></a>Permisos necesarios
toocomplete en este tema, debe tener permisos suficientes en Azure Active Directory y la suscripción de Azure. En concreto, debe ser capaz de toocreate una aplicación en Azure Active Directory hello y asignar Hola servicio principal tooa rol. 

Hola más fácil manera toocheck si su cuenta tiene los permisos adecuados es a través del portal de Hola. Consulte el [artículo que explica cómo comprobar el permiso requerido](resource-group-create-service-principal-portal.md#required-permissions).

Ahora, continúe tooa sección para la autenticación con:

* [password](#create-service-principal-with-password)
* [certificado autofirmado](#create-service-principal-with-self-signed-certificate)
* [certificado de una entidad de certificación](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>Comandos de PowerShell

tooset configurar un servicio principal, use:

| Comando | Descripción |
| ------- | ----------- | 
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Crea una entidad de servicio de Azure Active Directory |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | Hola asigna especifica la entidad de seguridad de RBAC rol toohello especificada, en hello especifica el ámbito. |


## <a name="create-service-principal-with-password"></a>Creación de entidad de servicio con contraseña

toocreate una entidad de servicio con el rol de colaborador de Hola para su suscripción, use: 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

ejemplo de Hola a en suspensión durante 20 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory. Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."

Hello siguiente secuencia de comandos permite toospecify un ámbito distinto suscripción predeterminada de Hola y reintentos Hola asignación de roles si se produce un error:

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Unos toonote de artículos acerca de la secuencia de comandos de hello:

* toogrant Hola identidad acceso toohello suscripción predeterminada y no se es necesario tooprovide parámetros ResourceGroup o Id. de suscripción.
* Especifique el parámetro de grupo de recursos de hello únicamente cuando desee que el ámbito de hello toolimit Hola rol asignación tooa del grupo de recursos.
*  En este ejemplo, agregar rol de colaborador de hello servicio toohello principal. Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).
* script de Hola en suspensión durante 15 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory. Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."
* Si necesita suscripciones de toomore de acceso principal de toogrant Hola servicio o grupos de recursos, ejecute hello `New-AzureRMRoleAssignment` cmdlet nuevo con ámbitos diferentes.


### <a name="provide-credentials-through-powershell"></a>Proporcionar credenciales a través de PowerShell
Ahora, debe toolog en como operaciones de tooperform aplicación Hola. Nombre de usuario de hello, use hello `ApplicationId` que creó para la aplicación hello. Contraseña de hello, utilice Hola especificada al crear la cuenta de hello. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

Id. de inquilino de Hello no es confidencial, por lo que se puede incrustar directamente en la secuencia de comandos. Si necesita Id. de inquilino de hello tooretrieve, use:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>Creación de una entidad de servicio con un certificado autofirmado

toocreate una entidad de servicio con un certificado autofirmado y un rol de colaborador de Hola para su suscripción, use: 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

ejemplo de Hola a en suspensión durante 20 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory. Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."

Hello siguiente secuencia de comandos permite toospecify un ámbito distinto suscripción predeterminada de Hola y reintentos Hola asignación de roles si se produce un error. Debe tener Azure PowerShell 2.0 en Windows 10 o Windows Server 2016.

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Unos toonote de artículos acerca de la secuencia de comandos de hello:

* toogrant Hola identidad acceso toohello suscripción predeterminada y no se es necesario tooprovide parámetros ResourceGroup o Id. de suscripción.
* Especifique el parámetro de grupo de recursos de hello únicamente cuando desee que el ámbito de hello toolimit Hola rol asignación tooa del grupo de recursos.
* En este ejemplo, agregar rol de colaborador de hello servicio toohello principal. Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).
* script de Hola en suspensión durante 15 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory. Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."
* Si necesita suscripciones de toomore de acceso principal de toogrant Hola servicio o grupos de recursos, ejecute hello `New-AzureRMRoleAssignment` cmdlet nuevo con ámbitos diferentes.

Si se **no tiene Windows 10 o Windows Server 2016 Technical Preview**, necesita hello toodownload [generador certificado autofirmado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) desde Microsoft Script Center. Extraer su contenido e importar cmdlet Hola que necesita.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
En el script de Hola, sustituya Hola siguiendo el certificado de dos líneas toogenerate Hola.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>Proporcionar un certificado a través de un script automatizado de PowerShell
Siempre que inicie sesión como una entidad de servicio, necesita Id. de inquilino de hello tooprovide del directorio de hello para la aplicación de AD. Un inquilino es una instancia de Azure Active Directory. Si solo tiene una suscripción, puede utilizar:

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

Id. y el Id. de inquilino de la aplicación Hello no son confidenciales, por lo que se puede incrustar directamente en la secuencia de comandos. Si necesita Id. de inquilino de hello tooretrieve, use:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Si necesita el identificador de la aplicación hello tooretrieve, use:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>Creación de una entidad de servicio con un certificado de una entidad de certificación
toouse un certificado emitido por una entidad de servicio de entidad emisora de certificados toocreate, Hola de uso siguiente secuencia de comandos:

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

Unos toonote de artículos acerca de la secuencia de comandos de hello:

* El acceso es suscripción toohello con ámbito.
* En este ejemplo, agregar rol de colaborador de hello servicio toohello principal. Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).
* script de Hola en suspensión durante 15 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory. Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."
* Si necesita suscripciones de toomore de acceso principal de toogrant Hola servicio o grupos de recursos, ejecute hello `New-AzureRMRoleAssignment` cmdlet nuevo con ámbitos diferentes.

### <a name="provide-certificate-through-automated-powershell-script"></a>Proporcionar un certificado a través de un script automatizado de PowerShell
Siempre que inicie sesión como una entidad de servicio, necesita Id. de inquilino de hello tooprovide del directorio de hello para la aplicación de AD. Un inquilino es una instancia de Azure Active Directory.

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

Id. y el Id. de inquilino de la aplicación Hello no son confidenciales, por lo que se puede incrustar directamente en la secuencia de comandos. Si necesita Id. de inquilino de hello tooretrieve, use:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Si necesita el identificador de la aplicación hello tooretrieve, use:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>Cambio de credenciales

las credenciales de hello toochange para una aplicación de AD, ya sea debido a un riesgo de seguridad o una expiración de la credencial, utilice hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) y [AzureRmADAppCredential New](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.

tooremove todas las credenciales de Hola para una aplicación, use:

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

tooadd una contraseña, use:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

tooadd un valor de certificado, cree un certificado autofirmado como se muestra en este tema. A continuación, use:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>Guardar access token toosimplify iniciar en
tooavoid proporcionar Hola servicio principal credenciales cada vez que necesita toolog en, puede guardar el token de acceso de Hola.

toouse Hola actual token de acceso en una sesión posterior, Guardar perfil de Hola.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Abra el perfil de Hola y examinar su contenido. Observe que contiene un token de acceso. En lugar de iniciar la sesión manualmente en el nuevo, basta con cargar el perfil de Hola.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> token de acceso de Hello expira, por lo que usar un perfil guardado funciona solo para mientras Hola token es válido.
>  

Como alternativa, puede invocar operaciones de REST de toolog de PowerShell en. De respuesta de autenticación de hello, puede recuperar el token de acceso de Hola para su uso con otras operaciones. Para obtener un ejemplo de recuperación de token de acceso de hello mediante la invocación de operaciones REST, consulte [generar un Token de acceso](resource-manager-rest-api.md#generating-an-access-token).

## <a name="debug"></a>Depurar

Puede encontrar Hola siguientes errores al crear a una entidad de servicio:

* **"Authentication_Unauthorized"** o **"ninguna suscripción encontrado en el contexto de Hola".** -Ve este error cuando la cuenta no tiene hello [los permisos necesarios](#required-permissions) en hello Azure Active Directory tooregister una aplicación. Por lo general, este error aparece cuando los usuarios administradores de Azure Active Directory son los únicos que pueden registrar las aplicaciones y la cuenta no es de un administrador. Pida a su administrador tooeither asignar rol Administrador tooan o tooenable usuarios tooregister aplicaciones.

* Su cuenta **"no tiene autorización tooperform acción 'Microsoft.Authorization/roleAssignments/write' sobre el ámbito '/ subscriptions / {guid}'."**  -Verá este error cuando su cuenta no tiene suficiente tooassign permisos una identidad de tooan de rol. Pida el tooadd de administrador de suscripción rol Administrador de acceso tooUser.

## <a name="sample-applications"></a>Aplicaciones de ejemplo
Para obtener información sobre cómo iniciar sesión como aplicación Hola a través de distintas plataformas, vea:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Pasos siguientes
* Para obtener instrucciones detalladas sobre cómo integrar una aplicación en Azure para administrar recursos, vea [tooauthorization de guía del desarrollador con hello API de Azure Resource Manager](resource-manager-api-authentication.md).
* Para obtener una explicación más detallada de las aplicaciones y entidades de servicio, consulte [Objetos de aplicación y de entidad de servicio](../active-directory/active-directory-application-objects.md). 
* Para más información sobre la autenticación de Azure Active Directory, consulte [Escenarios de autenticación para Azure AD](../active-directory/active-directory-authentication-scenarios.md).
* Para obtener una lista de las acciones disponibles que puede otorgar o denegar toousers, consulte [las operaciones de proveedor de recursos del Administrador de recursos de Azure](../active-directory/role-based-access-control-resource-provider-operations.md).

