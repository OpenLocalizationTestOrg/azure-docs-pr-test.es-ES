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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="0213d-104">Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="0213d-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="0213d-105">Cuando haya una aplicación o un script que necesita tooaccess recursos, puede configurar una identidad para la aplicación hello y autenticar la aplicación hello con sus propias credenciales.</span><span class="sxs-lookup"><span data-stu-id="0213d-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="0213d-106">Esta identidad se conoce como una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="0213d-106">This identity is known as a service principal.</span></span> <span data-ttu-id="0213d-107">Este enfoque le permite:</span><span class="sxs-lookup"><span data-stu-id="0213d-107">This approach enables you to:</span></span>

* <span data-ttu-id="0213d-108">Asignar permisos de identidad de aplicación de toohello que son diferentes de sus propios permisos.</span><span class="sxs-lookup"><span data-stu-id="0213d-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="0213d-109">Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo.</span><span class="sxs-lookup"><span data-stu-id="0213d-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="0213d-110">Usar un certificado para la autenticación al ejecutar un script desatendido.</span><span class="sxs-lookup"><span data-stu-id="0213d-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="0213d-111">Este tema muestra cómo toouse [Azure PowerShell](/powershell/azure/overview) tooset todo lo que necesita para una toorun de aplicación en sus propias credenciales y la identidad.</span><span class="sxs-lookup"><span data-stu-id="0213d-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="0213d-112">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="0213d-112">Required permissions</span></span>
<span data-ttu-id="0213d-113">toocomplete en este tema, debe tener permisos suficientes en Azure Active Directory y la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0213d-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="0213d-114">En concreto, debe ser capaz de toocreate una aplicación en Azure Active Directory hello y asignar Hola servicio principal tooa rol.</span><span class="sxs-lookup"><span data-stu-id="0213d-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="0213d-115">Hola más fácil manera toocheck si su cuenta tiene los permisos adecuados es a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="0213d-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="0213d-116">Consulte el [artículo que explica cómo comprobar el permiso requerido](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="0213d-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="0213d-117">Ahora, continúe tooa sección para la autenticación con:</span><span class="sxs-lookup"><span data-stu-id="0213d-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="0213d-118">password</span><span class="sxs-lookup"><span data-stu-id="0213d-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="0213d-119">certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="0213d-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="0213d-120">certificado de una entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="0213d-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="0213d-121">Comandos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0213d-121">PowerShell commands</span></span>

<span data-ttu-id="0213d-122">tooset configurar un servicio principal, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="0213d-123">Comando</span><span class="sxs-lookup"><span data-stu-id="0213d-123">Command</span></span> | <span data-ttu-id="0213d-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="0213d-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="0213d-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="0213d-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="0213d-126">Crea una entidad de servicio de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0213d-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="0213d-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="0213d-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="0213d-128">Hola asigna especifica la entidad de seguridad de RBAC rol toohello especificada, en hello especifica el ámbito.</span><span class="sxs-lookup"><span data-stu-id="0213d-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="0213d-129">Creación de entidad de servicio con contraseña</span><span class="sxs-lookup"><span data-stu-id="0213d-129">Create service principal with password</span></span>

<span data-ttu-id="0213d-130">toocreate una entidad de servicio con el rol de colaborador de Hola para su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="0213d-131">ejemplo de Hola a en suspensión durante 20 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0213d-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0213d-132">Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."</span><span class="sxs-lookup"><span data-stu-id="0213d-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="0213d-133">Hello siguiente secuencia de comandos permite toospecify un ámbito distinto suscripción predeterminada de Hola y reintentos Hola asignación de roles si se produce un error:</span><span class="sxs-lookup"><span data-stu-id="0213d-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

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

<span data-ttu-id="0213d-134">Unos toonote de artículos acerca de la secuencia de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="0213d-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="0213d-135">toogrant Hola identidad acceso toohello suscripción predeterminada y no se es necesario tooprovide parámetros ResourceGroup o Id. de suscripción.</span><span class="sxs-lookup"><span data-stu-id="0213d-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="0213d-136">Especifique el parámetro de grupo de recursos de hello únicamente cuando desee que el ámbito de hello toolimit Hola rol asignación tooa del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0213d-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="0213d-137">En este ejemplo, agregar rol de colaborador de hello servicio toohello principal.</span><span class="sxs-lookup"><span data-stu-id="0213d-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="0213d-138">Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0213d-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="0213d-139">script de Hola en suspensión durante 15 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0213d-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0213d-140">Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."</span><span class="sxs-lookup"><span data-stu-id="0213d-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="0213d-141">Si necesita suscripciones de toomore de acceso principal de toogrant Hola servicio o grupos de recursos, ejecute hello `New-AzureRMRoleAssignment` cmdlet nuevo con ámbitos diferentes.</span><span class="sxs-lookup"><span data-stu-id="0213d-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="0213d-142">Proporcionar credenciales a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0213d-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="0213d-143">Ahora, debe toolog en como operaciones de tooperform aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="0213d-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="0213d-144">Nombre de usuario de hello, use hello `ApplicationId` que creó para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0213d-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="0213d-145">Contraseña de hello, utilice Hola especificada al crear la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="0213d-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="0213d-146">Id. de inquilino de Hello no es confidencial, por lo que se puede incrustar directamente en la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="0213d-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="0213d-147">Si necesita Id. de inquilino de hello tooretrieve, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="0213d-148">Creación de una entidad de servicio con un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="0213d-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="0213d-149">toocreate una entidad de servicio con un certificado autofirmado y un rol de colaborador de Hola para su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="0213d-150">ejemplo de Hola a en suspensión durante 20 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0213d-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0213d-151">Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."</span><span class="sxs-lookup"><span data-stu-id="0213d-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="0213d-152">Hello siguiente secuencia de comandos permite toospecify un ámbito distinto suscripción predeterminada de Hola y reintentos Hola asignación de roles si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="0213d-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="0213d-153">Debe tener Azure PowerShell 2.0 en Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0213d-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

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

<span data-ttu-id="0213d-154">Unos toonote de artículos acerca de la secuencia de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="0213d-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="0213d-155">toogrant Hola identidad acceso toohello suscripción predeterminada y no se es necesario tooprovide parámetros ResourceGroup o Id. de suscripción.</span><span class="sxs-lookup"><span data-stu-id="0213d-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="0213d-156">Especifique el parámetro de grupo de recursos de hello únicamente cuando desee que el ámbito de hello toolimit Hola rol asignación tooa del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0213d-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="0213d-157">En este ejemplo, agregar rol de colaborador de hello servicio toohello principal.</span><span class="sxs-lookup"><span data-stu-id="0213d-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="0213d-158">Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0213d-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="0213d-159">script de Hola en suspensión durante 15 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0213d-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0213d-160">Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."</span><span class="sxs-lookup"><span data-stu-id="0213d-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="0213d-161">Si necesita suscripciones de toomore de acceso principal de toogrant Hola servicio o grupos de recursos, ejecute hello `New-AzureRMRoleAssignment` cmdlet nuevo con ámbitos diferentes.</span><span class="sxs-lookup"><span data-stu-id="0213d-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="0213d-162">Si se **no tiene Windows 10 o Windows Server 2016 Technical Preview**, necesita hello toodownload [generador certificado autofirmado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) desde Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="0213d-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="0213d-163">Extraer su contenido e importar cmdlet Hola que necesita.</span><span class="sxs-lookup"><span data-stu-id="0213d-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="0213d-164">En el script de Hola, sustituya Hola siguiendo el certificado de dos líneas toogenerate Hola.</span><span class="sxs-lookup"><span data-stu-id="0213d-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="0213d-165">Proporcionar un certificado a través de un script automatizado de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0213d-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="0213d-166">Siempre que inicie sesión como una entidad de servicio, necesita Id. de inquilino de hello tooprovide del directorio de hello para la aplicación de AD.</span><span class="sxs-lookup"><span data-stu-id="0213d-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="0213d-167">Un inquilino es una instancia de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0213d-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="0213d-168">Si solo tiene una suscripción, puede utilizar:</span><span class="sxs-lookup"><span data-stu-id="0213d-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="0213d-169">Id. y el Id. de inquilino de la aplicación Hello no son confidenciales, por lo que se puede incrustar directamente en la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="0213d-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="0213d-170">Si necesita Id. de inquilino de hello tooretrieve, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="0213d-171">Si necesita el identificador de la aplicación hello tooretrieve, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="0213d-172">Creación de una entidad de servicio con un certificado de una entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="0213d-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="0213d-173">toouse un certificado emitido por una entidad de servicio de entidad emisora de certificados toocreate, Hola de uso siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="0213d-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

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

<span data-ttu-id="0213d-174">Unos toonote de artículos acerca de la secuencia de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="0213d-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="0213d-175">El acceso es suscripción toohello con ámbito.</span><span class="sxs-lookup"><span data-stu-id="0213d-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="0213d-176">En este ejemplo, agregar rol de colaborador de hello servicio toohello principal.</span><span class="sxs-lookup"><span data-stu-id="0213d-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="0213d-177">Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0213d-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="0213d-178">script de Hola en suspensión durante 15 segundos tooallow algún tiempo Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0213d-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="0213d-179">Si la secuencia de comandos no se espera durante el tiempo suficiente, verá un error que indica: "PrincipalNotFound: {id} de la entidad de seguridad no existe en el directorio de hello."</span><span class="sxs-lookup"><span data-stu-id="0213d-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="0213d-180">Si necesita suscripciones de toomore de acceso principal de toogrant Hola servicio o grupos de recursos, ejecute hello `New-AzureRMRoleAssignment` cmdlet nuevo con ámbitos diferentes.</span><span class="sxs-lookup"><span data-stu-id="0213d-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="0213d-181">Proporcionar un certificado a través de un script automatizado de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0213d-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="0213d-182">Siempre que inicie sesión como una entidad de servicio, necesita Id. de inquilino de hello tooprovide del directorio de hello para la aplicación de AD.</span><span class="sxs-lookup"><span data-stu-id="0213d-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="0213d-183">Un inquilino es una instancia de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0213d-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="0213d-184">Id. y el Id. de inquilino de la aplicación Hello no son confidenciales, por lo que se puede incrustar directamente en la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="0213d-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="0213d-185">Si necesita Id. de inquilino de hello tooretrieve, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="0213d-186">Si necesita el identificador de la aplicación hello tooretrieve, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="0213d-187">Cambio de credenciales</span><span class="sxs-lookup"><span data-stu-id="0213d-187">Change credentials</span></span>

<span data-ttu-id="0213d-188">las credenciales de hello toochange para una aplicación de AD, ya sea debido a un riesgo de seguridad o una expiración de la credencial, utilice hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) y [AzureRmADAppCredential New](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="0213d-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="0213d-189">tooremove todas las credenciales de Hola para una aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="0213d-190">tooadd una contraseña, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="0213d-191">tooadd un valor de certificado, cree un certificado autofirmado como se muestra en este tema.</span><span class="sxs-lookup"><span data-stu-id="0213d-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="0213d-192">A continuación, use:</span><span class="sxs-lookup"><span data-stu-id="0213d-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="0213d-193">Guardar access token toosimplify iniciar en</span><span class="sxs-lookup"><span data-stu-id="0213d-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="0213d-194">tooavoid proporcionar Hola servicio principal credenciales cada vez que necesita toolog en, puede guardar el token de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="0213d-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="0213d-195">toouse Hola actual token de acceso en una sesión posterior, Guardar perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="0213d-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="0213d-196">Abra el perfil de Hola y examinar su contenido.</span><span class="sxs-lookup"><span data-stu-id="0213d-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="0213d-197">Observe que contiene un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="0213d-197">Notice that it contains an access token.</span></span> <span data-ttu-id="0213d-198">En lugar de iniciar la sesión manualmente en el nuevo, basta con cargar el perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="0213d-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="0213d-199">token de acceso de Hello expira, por lo que usar un perfil guardado funciona solo para mientras Hola token es válido.</span><span class="sxs-lookup"><span data-stu-id="0213d-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="0213d-200">Como alternativa, puede invocar operaciones de REST de toolog de PowerShell en.</span><span class="sxs-lookup"><span data-stu-id="0213d-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="0213d-201">De respuesta de autenticación de hello, puede recuperar el token de acceso de Hola para su uso con otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="0213d-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="0213d-202">Para obtener un ejemplo de recuperación de token de acceso de hello mediante la invocación de operaciones REST, consulte [generar un Token de acceso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="0213d-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="0213d-203">Depurar</span><span class="sxs-lookup"><span data-stu-id="0213d-203">Debug</span></span>

<span data-ttu-id="0213d-204">Puede encontrar Hola siguientes errores al crear a una entidad de servicio:</span><span class="sxs-lookup"><span data-stu-id="0213d-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="0213d-205">**"Authentication_Unauthorized"** o **"ninguna suscripción encontrado en el contexto de Hola".**</span><span class="sxs-lookup"><span data-stu-id="0213d-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="0213d-206">-Ve este error cuando la cuenta no tiene hello [los permisos necesarios](#required-permissions) en hello Azure Active Directory tooregister una aplicación.</span><span class="sxs-lookup"><span data-stu-id="0213d-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="0213d-207">Por lo general, este error aparece cuando los usuarios administradores de Azure Active Directory son los únicos que pueden registrar las aplicaciones y la cuenta no es de un administrador. Pida a su administrador tooeither asignar rol Administrador tooan o tooenable usuarios tooregister aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0213d-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="0213d-208">Su cuenta **"no tiene autorización tooperform acción 'Microsoft.Authorization/roleAssignments/write' sobre el ámbito '/ subscriptions / {guid}'."**  -Verá este error cuando su cuenta no tiene suficiente tooassign permisos una identidad de tooan de rol.</span><span class="sxs-lookup"><span data-stu-id="0213d-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="0213d-209">Pida el tooadd de administrador de suscripción rol Administrador de acceso tooUser.</span><span class="sxs-lookup"><span data-stu-id="0213d-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="0213d-210">Aplicaciones de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0213d-210">Sample applications</span></span>
<span data-ttu-id="0213d-211">Para obtener información sobre cómo iniciar sesión como aplicación Hola a través de distintas plataformas, vea:</span><span class="sxs-lookup"><span data-stu-id="0213d-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="0213d-212">.NET</span><span class="sxs-lookup"><span data-stu-id="0213d-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="0213d-213">Java</span><span class="sxs-lookup"><span data-stu-id="0213d-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="0213d-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="0213d-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="0213d-215">Python</span><span class="sxs-lookup"><span data-stu-id="0213d-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="0213d-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="0213d-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="0213d-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0213d-217">Next steps</span></span>
* <span data-ttu-id="0213d-218">Para obtener instrucciones detalladas sobre cómo integrar una aplicación en Azure para administrar recursos, vea [tooauthorization de guía del desarrollador con hello API de Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0213d-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="0213d-219">Para obtener una explicación más detallada de las aplicaciones y entidades de servicio, consulte [Objetos de aplicación y de entidad de servicio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="0213d-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="0213d-220">Para más información sobre la autenticación de Azure Active Directory, consulte [Escenarios de autenticación para Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="0213d-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="0213d-221">Para obtener una lista de las acciones disponibles que puede otorgar o denegar toousers, consulte [las operaciones de proveedor de recursos del Administrador de recursos de Azure](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="0213d-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

