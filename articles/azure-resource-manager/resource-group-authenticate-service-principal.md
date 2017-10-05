---
title: "Creación de identidad para aplicaciones de Azure con PowerShell | Microsoft Docs"
description: "Se describe cómo usar Azure PowerShell para crear una entidad de servicio y una aplicación de Azure Active Directory, además de cómo concederle acceso a recursos mediante el control de acceso basado en rol. Muestra cómo autenticar aplicaciones con una contraseña o un certificado."
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
ms.openlocfilehash: 55e83b0742652abbb42100a11a468bc13a7a8aed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-powershell-to-create-a-service-principal-to-access-resources"></a>Uso de Azure PowerShell para crear a una entidad de servicio para acceder a recursos

Cuando haya una aplicación o un script que necesite acceder a recursos, puede configurar una identidad para la aplicación y autenticarla con sus propias credenciales. Esta identidad se conoce como una entidad de servicio. Este enfoque le permite:

* Asignar permisos a la identidad de la aplicación que sean diferentes a los suyos propios. Normalmente, estos permisos están restringidos a exactamente aquello que la aplicación debe hacer.
* Usar un certificado para la autenticación al ejecutar un script desatendido.

En este tema se explica cómo usar [Azure PowerShell](/powershell/azure/overview) para configurar todo lo que necesita para que una aplicación se ejecute con sus propias credenciales e identidad.

## <a name="required-permissions"></a>Permisos necesarios
Para completar este tema, debe tener permisos suficientes tanto en su suscripción de Azure como en Azure Active Directory. En concreto, debe poder crear una aplicación en Azure Active Directory y asignar la entidad de servicio a un rol. 

El portal representa la forma más sencilla de comprobar si su cuenta tiene los permisos adecuados. Consulte el [artículo que explica cómo comprobar el permiso requerido](resource-group-create-service-principal-portal.md#required-permissions).

Ahora, vaya a la sección para la autenticación con:

* [password](#create-service-principal-with-password)
* [certificado autofirmado](#create-service-principal-with-self-signed-certificate)
* [certificado de una entidad de certificación](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>Comandos de PowerShell

Para configurar una entidad de servicio, puede utilizar:

| Comando | Descripción |
| ------- | ----------- | 
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Crea una entidad de servicio de Azure Active Directory |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | Asigna el rol de RBAC especificado a la entidad de seguridad especificada en el ámbito especificado. |


## <a name="create-service-principal-with-password"></a>Creación de entidad de servicio con contraseña

Para crear una entidad de servicio con el rol de Colaborador de la suscripción, puede utilizar: 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

El ejemplo entra en suspensión durante 20 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory. Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).

El siguiente script le permite especificar un ámbito distinto de la suscripción predeterminada y vuelve a intentar la asignación de roles si se produce un error:

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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

 
 # Create Service Principal for the AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Algunos elementos que hay que indicar sobre el script:

* Para conceder el acceso de identidad a la suscripción predeterminada, no es preciso proporcionar los parámetros ResourceGroup o SubscriptionId.
* Especifique el parámetro ResourceGroup solo cuando desee limitar el ámbito de la asignación de rol a un grupo de recursos.
*  En este ejemplo, la entidad de servicio se agrega al rol de colaborador. Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).
* El script entra en suspensión durante 15 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory. Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).
* Si necesita conceder a la entidad de servicio acceso a más suscripciones o grupos de recursos, vuelva a ejecutar el cmdlet `New-AzureRMRoleAssignment` con ámbitos diferentes.


### <a name="provide-credentials-through-powershell"></a>Proporcionar credenciales a través de PowerShell
Ahora, debe iniciar sesión como la aplicación para realizar operaciones. Para el nombre de usuario, use el valor de `ApplicationId` que creó para la aplicación. Para la contraseña, use la que especificó al crear la cuenta. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

El identificador del inquilino no es confidencial, por lo que se puede insertar directamente en el script. Si necesita recuperar el identificador del inquilino, use:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>Creación de una entidad de servicio con un certificado autofirmado

Para crear una entidad de servicio con un certificado autofirmado y el rol de Colaborador de la suscripción, utilice: 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

El ejemplo entra en suspensión durante 20 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory. Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).

El siguiente script le permite especificar un ámbito distinto de la suscripción predeterminada y vuelve a intentar la asignación de roles si se produce un error. Debe tener Azure PowerShell 2.0 en Windows 10 o Windows Server 2016.

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Algunos elementos que hay que indicar sobre el script:

* Para conceder el acceso de identidad a la suscripción predeterminada, no es preciso proporcionar los parámetros ResourceGroup o SubscriptionId.
* Especifique el parámetro ResourceGroup solo cuando desee limitar el ámbito de la asignación de rol a un grupo de recursos.
* En este ejemplo, la entidad de servicio se agrega al rol de colaborador. Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).
* El script entra en suspensión durante 15 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory. Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).
* Si necesita conceder a la entidad de servicio acceso a más suscripciones o grupos de recursos, vuelva a ejecutar el cmdlet `New-AzureRMRoleAssignment` con ámbitos diferentes.

Si **no tiene Windows 10 o Windows Server 2016 Technical Preview**, descargue el [generador de certificados autofirmados](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) del sitio Microsoft Script Center. Extraiga el contenido e importe el cmdlet que necesita.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
En el script, sustituya las dos líneas siguientes para generar el certificado.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>Proporcionar un certificado a través de un script automatizado de PowerShell
Cada vez que inicie sesión como entidad de servicio, debe proporcionar el id. del inquilino del directorio para la aplicación de AD. Un inquilino es una instancia de Azure Active Directory. Si solo tiene una suscripción, puede utilizar:

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

Ni el identificador de la aplicación ni el identificador del inquilino son confidenciales, por lo que se pueden integrar directamente en el script. Si necesita recuperar el identificador del inquilino, use:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Si necesita recuperar el identificador de la aplicación, use:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>Creación de una entidad de servicio con un certificado de una entidad de certificación
Para usar un certificado emitido por una entidad de certificación para crear una entidad de servicio, use el siguiente script:

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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

Algunos elementos que hay que indicar sobre el script:

* El acceso se limita a la suscripción.
* En este ejemplo, la entidad de servicio se agrega al rol de colaborador. Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).
* El script entra en suspensión durante 15 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory. Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).
* Si necesita conceder a la entidad de servicio acceso a más suscripciones o grupos de recursos, vuelva a ejecutar el cmdlet `New-AzureRMRoleAssignment` con ámbitos diferentes.

### <a name="provide-certificate-through-automated-powershell-script"></a>Proporcionar un certificado a través de un script automatizado de PowerShell
Cada vez que inicie sesión como entidad de servicio, debe proporcionar el id. del inquilino del directorio para la aplicación de AD. Un inquilino es una instancia de Azure Active Directory.

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

Ni el identificador de la aplicación ni el identificador del inquilino son confidenciales, por lo que se pueden integrar directamente en el script. Si necesita recuperar el identificador del inquilino, use:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Si necesita recuperar el identificador de la aplicación, use:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>Cambio de credenciales

Para cambiar las credenciales de una aplicación de AD, ya sea debido a un riesgo de seguridad o a la expiración de una credencial, use los cmdlets [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) y [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential).

Para quitar todas las credenciales de una aplicación, use:

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

Para agregar una contraseña, use:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

Para agregar un valor de certificado, cree un certificado autofirmado, como se muestra en este tema. A continuación, use:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-to-simplify-log-in"></a>Guardado del token de acceso para simplificar el inicio de sesión
Para evitar tener que especificar las credenciales de la entidad de servicio cada vez que necesite iniciar sesión, puede guardar el token de acceso.

Para usar el token de acceso actual en una sesión posterior, guarde el perfil.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Abra el perfil y examine su contenido. Observe que contiene un token de acceso. En lugar de tener que volver a iniciar sesión manualmente, solo tiene que cargar el perfil.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> El token de acceso expirará y, por lo tanto, el uso de un perfil guardado solo funcionará mientras el token sea válido.
>  

Como alternativa, puede invocar operaciones de REST desde PowerShell para iniciar sesión. De la respuesta de autenticación, puede recuperar el token de acceso para su uso con otras operaciones. Para ver un ejemplo de recuperación del token de acceso mediante la invocación de operaciones REST, consulte [Generación de un token de acceso](resource-manager-rest-api.md#generating-an-access-token).

## <a name="debug"></a>Depurar

Durante la creación de una entidad de servicio pueden producirse los siguientes errores:

* **"Authentication_Unauthorized"** o **"No subscription found in the context"** (No se encuentra una suscripción en el contexto). - Este error se ve cuando la cuenta no tiene los [permisos necesarios](#required-permissions) en Azure Active Directory para registrar una aplicación. Por lo general, este error aparece cuando los usuarios administradores de Azure Active Directory son los únicos que pueden registrar las aplicaciones y la cuenta no es de un administrador. Pida al administrador que le asigne un rol de administrador o que permita a los usuarios registrar aplicaciones.

* Su cuenta **"no tiene autorización para realizar la acción 'Microsoft.Authorization/roleAssignments/write' en el ámbito '/ subscriptions / {guid}'."**  - Este error aparece cuando la cuenta no tiene permisos suficientes para asignar un rol a una identidad. Pida al administrador de suscripciones que le agregue al rol de administrador de acceso de usuario.

## <a name="sample-applications"></a>Aplicaciones de ejemplo
Para información sobre el inicio de sesión como en la aplicación a través de distintas plataformas, consulte:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Pasos siguientes
* Si desea conocer los pasos detallados de la integración de una aplicación en Azure para administrar recursos, consulte [Guía del desarrollador para la autorización con la API de Azure Resource Manager](resource-manager-api-authentication.md).
* Para obtener una explicación más detallada de las aplicaciones y entidades de servicio, consulte [Objetos de aplicación y de entidad de servicio](../active-directory/active-directory-application-objects.md). 
* Para más información sobre la autenticación de Azure Active Directory, consulte [Escenarios de autenticación para Azure AD](../active-directory/active-directory-authentication-scenarios.md).
* Para obtener una lista de las acciones que puede conceder o denegar a los usuarios, consulte [Operaciones del proveedor de recursos de Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).

