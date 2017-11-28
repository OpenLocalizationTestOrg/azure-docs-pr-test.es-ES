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
# <a name="use-azure-powershell-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="d7861-104">Uso de Azure PowerShell para crear a una entidad de servicio para acceder a recursos</span><span class="sxs-lookup"><span data-stu-id="d7861-104">Use Azure PowerShell to create a service principal to access resources</span></span>

<span data-ttu-id="d7861-105">Cuando haya una aplicación o un script que necesite acceder a recursos, puede configurar una identidad para la aplicación y autenticarla con sus propias credenciales.</span><span class="sxs-lookup"><span data-stu-id="d7861-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="d7861-106">Esta identidad se conoce como una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="d7861-106">This identity is known as a service principal.</span></span> <span data-ttu-id="d7861-107">Este enfoque le permite:</span><span class="sxs-lookup"><span data-stu-id="d7861-107">This approach enables you to:</span></span>

* <span data-ttu-id="d7861-108">Asignar permisos a la identidad de la aplicación que sean diferentes a los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="d7861-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="d7861-109">Normalmente, estos permisos están restringidos a exactamente aquello que la aplicación debe hacer.</span><span class="sxs-lookup"><span data-stu-id="d7861-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="d7861-110">Usar un certificado para la autenticación al ejecutar un script desatendido.</span><span class="sxs-lookup"><span data-stu-id="d7861-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="d7861-111">En este tema se explica cómo usar [Azure PowerShell](/powershell/azure/overview) para configurar todo lo que necesita para que una aplicación se ejecute con sus propias credenciales e identidad.</span><span class="sxs-lookup"><span data-stu-id="d7861-111">This topic shows you how to use [Azure PowerShell](/powershell/azure/overview) to set up everything you need for an application to run under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="d7861-112">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="d7861-112">Required permissions</span></span>
<span data-ttu-id="d7861-113">Para completar este tema, debe tener permisos suficientes tanto en su suscripción de Azure como en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7861-113">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="d7861-114">En concreto, debe poder crear una aplicación en Azure Active Directory y asignar la entidad de servicio a un rol.</span><span class="sxs-lookup"><span data-stu-id="d7861-114">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="d7861-115">El portal representa la forma más sencilla de comprobar si su cuenta tiene los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="d7861-115">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="d7861-116">Consulte el [artículo que explica cómo comprobar el permiso requerido](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="d7861-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="d7861-117">Ahora, vaya a la sección para la autenticación con:</span><span class="sxs-lookup"><span data-stu-id="d7861-117">Now, proceed to a section for authenticating with:</span></span>

* [<span data-ttu-id="d7861-118">password</span><span class="sxs-lookup"><span data-stu-id="d7861-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="d7861-119">certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="d7861-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="d7861-120">certificado de una entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="d7861-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="d7861-121">Comandos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7861-121">PowerShell commands</span></span>

<span data-ttu-id="d7861-122">Para configurar una entidad de servicio, puede utilizar:</span><span class="sxs-lookup"><span data-stu-id="d7861-122">To set up a service principal, you use:</span></span>

| <span data-ttu-id="d7861-123">Comando</span><span class="sxs-lookup"><span data-stu-id="d7861-123">Command</span></span> | <span data-ttu-id="d7861-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="d7861-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="d7861-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="d7861-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="d7861-126">Crea una entidad de servicio de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7861-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="d7861-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="d7861-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="d7861-128">Asigna el rol de RBAC especificado a la entidad de seguridad especificada en el ámbito especificado.</span><span class="sxs-lookup"><span data-stu-id="d7861-128">Assigns the specified RBAC role to the specified principal, at the specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="d7861-129">Creación de entidad de servicio con contraseña</span><span class="sxs-lookup"><span data-stu-id="d7861-129">Create service principal with password</span></span>

<span data-ttu-id="d7861-130">Para crear una entidad de servicio con el rol de Colaborador de la suscripción, puede utilizar:</span><span class="sxs-lookup"><span data-stu-id="d7861-130">To create a service principal with the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="d7861-131">El ejemplo entra en suspensión durante 20 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7861-131">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d7861-132">Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).</span><span class="sxs-lookup"><span data-stu-id="d7861-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="d7861-133">El siguiente script le permite especificar un ámbito distinto de la suscripción predeterminada y vuelve a intentar la asignación de roles si se produce un error:</span><span class="sxs-lookup"><span data-stu-id="d7861-133">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs:</span></span>

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

<span data-ttu-id="d7861-134">Algunos elementos que hay que indicar sobre el script:</span><span class="sxs-lookup"><span data-stu-id="d7861-134">A few items to note about the script:</span></span>

* <span data-ttu-id="d7861-135">Para conceder el acceso de identidad a la suscripción predeterminada, no es preciso proporcionar los parámetros ResourceGroup o SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="d7861-135">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="d7861-136">Especifique el parámetro ResourceGroup solo cuando desee limitar el ámbito de la asignación de rol a un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d7861-136">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
*  <span data-ttu-id="d7861-137">En este ejemplo, la entidad de servicio se agrega al rol de colaborador.</span><span class="sxs-lookup"><span data-stu-id="d7861-137">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="d7861-138">Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d7861-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="d7861-139">El script entra en suspensión durante 15 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7861-139">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d7861-140">Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).</span><span class="sxs-lookup"><span data-stu-id="d7861-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="d7861-141">Si necesita conceder a la entidad de servicio acceso a más suscripciones o grupos de recursos, vuelva a ejecutar el cmdlet `New-AzureRMRoleAssignment` con ámbitos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d7861-141">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="d7861-142">Proporcionar credenciales a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7861-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="d7861-143">Ahora, debe iniciar sesión como la aplicación para realizar operaciones.</span><span class="sxs-lookup"><span data-stu-id="d7861-143">Now, you need to log in as the application to perform operations.</span></span> <span data-ttu-id="d7861-144">Para el nombre de usuario, use el valor de `ApplicationId` que creó para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7861-144">For the user name, use the `ApplicationId` that you created for the application.</span></span> <span data-ttu-id="d7861-145">Para la contraseña, use la que especificó al crear la cuenta.</span><span class="sxs-lookup"><span data-stu-id="d7861-145">For the password, use the one you specified when creating the account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="d7861-146">El identificador del inquilino no es confidencial, por lo que se puede insertar directamente en el script.</span><span class="sxs-lookup"><span data-stu-id="d7861-146">The tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="d7861-147">Si necesita recuperar el identificador del inquilino, use:</span><span class="sxs-lookup"><span data-stu-id="d7861-147">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="d7861-148">Creación de una entidad de servicio con un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="d7861-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="d7861-149">Para crear una entidad de servicio con un certificado autofirmado y el rol de Colaborador de la suscripción, utilice:</span><span class="sxs-lookup"><span data-stu-id="d7861-149">To create a service principal with a self-signed certificate and the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="d7861-150">El ejemplo entra en suspensión durante 20 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7861-150">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d7861-151">Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).</span><span class="sxs-lookup"><span data-stu-id="d7861-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="d7861-152">El siguiente script le permite especificar un ámbito distinto de la suscripción predeterminada y vuelve a intentar la asignación de roles si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="d7861-152">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs.</span></span> <span data-ttu-id="d7861-153">Debe tener Azure PowerShell 2.0 en Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d7861-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

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

<span data-ttu-id="d7861-154">Algunos elementos que hay que indicar sobre el script:</span><span class="sxs-lookup"><span data-stu-id="d7861-154">A few items to note about the script:</span></span>

* <span data-ttu-id="d7861-155">Para conceder el acceso de identidad a la suscripción predeterminada, no es preciso proporcionar los parámetros ResourceGroup o SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="d7861-155">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="d7861-156">Especifique el parámetro ResourceGroup solo cuando desee limitar el ámbito de la asignación de rol a un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d7861-156">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
* <span data-ttu-id="d7861-157">En este ejemplo, la entidad de servicio se agrega al rol de colaborador.</span><span class="sxs-lookup"><span data-stu-id="d7861-157">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="d7861-158">Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d7861-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="d7861-159">El script entra en suspensión durante 15 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7861-159">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d7861-160">Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).</span><span class="sxs-lookup"><span data-stu-id="d7861-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="d7861-161">Si necesita conceder a la entidad de servicio acceso a más suscripciones o grupos de recursos, vuelva a ejecutar el cmdlet `New-AzureRMRoleAssignment` con ámbitos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d7861-161">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="d7861-162">Si **no tiene Windows 10 o Windows Server 2016 Technical Preview**, descargue el [generador de certificados autofirmados](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) del sitio Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="d7861-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need to download the [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="d7861-163">Extraiga el contenido e importe el cmdlet que necesita.</span><span class="sxs-lookup"><span data-stu-id="d7861-163">Extract its contents and import the cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="d7861-164">En el script, sustituya las dos líneas siguientes para generar el certificado.</span><span class="sxs-lookup"><span data-stu-id="d7861-164">In the script, substitute the following two lines to generate the certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="d7861-165">Proporcionar un certificado a través de un script automatizado de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7861-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="d7861-166">Cada vez que inicie sesión como entidad de servicio, debe proporcionar el id. del inquilino del directorio para la aplicación de AD.</span><span class="sxs-lookup"><span data-stu-id="d7861-166">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="d7861-167">Un inquilino es una instancia de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7861-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="d7861-168">Si solo tiene una suscripción, puede utilizar:</span><span class="sxs-lookup"><span data-stu-id="d7861-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="d7861-169">Ni el identificador de la aplicación ni el identificador del inquilino son confidenciales, por lo que se pueden integrar directamente en el script.</span><span class="sxs-lookup"><span data-stu-id="d7861-169">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="d7861-170">Si necesita recuperar el identificador del inquilino, use:</span><span class="sxs-lookup"><span data-stu-id="d7861-170">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="d7861-171">Si necesita recuperar el identificador de la aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="d7861-171">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="d7861-172">Creación de una entidad de servicio con un certificado de una entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="d7861-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="d7861-173">Para usar un certificado emitido por una entidad de certificación para crear una entidad de servicio, use el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="d7861-173">To use a certificate issued from a Certificate Authority to create service principal, use the following script:</span></span>

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

<span data-ttu-id="d7861-174">Algunos elementos que hay que indicar sobre el script:</span><span class="sxs-lookup"><span data-stu-id="d7861-174">A few items to note about the script:</span></span>

* <span data-ttu-id="d7861-175">El acceso se limita a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="d7861-175">Access is scoped to the subscription.</span></span>
* <span data-ttu-id="d7861-176">En este ejemplo, la entidad de servicio se agrega al rol de colaborador.</span><span class="sxs-lookup"><span data-stu-id="d7861-176">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="d7861-177">Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d7861-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="d7861-178">El script entra en suspensión durante 15 segundos para dar tiempo a que la nueva entidad de servicio se propague por Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7861-178">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d7861-179">Si el script no espera el tiempo suficiente, verá un mensaje de error que dice: "PrincipalNotFound: Principal {id} does not exist in the directory" (PrincipalNotFound: la entidad de servicio {id} no existe en el directorio).</span><span class="sxs-lookup"><span data-stu-id="d7861-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="d7861-180">Si necesita conceder a la entidad de servicio acceso a más suscripciones o grupos de recursos, vuelva a ejecutar el cmdlet `New-AzureRMRoleAssignment` con ámbitos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d7861-180">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="d7861-181">Proporcionar un certificado a través de un script automatizado de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7861-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="d7861-182">Cada vez que inicie sesión como entidad de servicio, debe proporcionar el id. del inquilino del directorio para la aplicación de AD.</span><span class="sxs-lookup"><span data-stu-id="d7861-182">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="d7861-183">Un inquilino es una instancia de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7861-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="d7861-184">Ni el identificador de la aplicación ni el identificador del inquilino son confidenciales, por lo que se pueden integrar directamente en el script.</span><span class="sxs-lookup"><span data-stu-id="d7861-184">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="d7861-185">Si necesita recuperar el identificador del inquilino, use:</span><span class="sxs-lookup"><span data-stu-id="d7861-185">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="d7861-186">Si necesita recuperar el identificador de la aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="d7861-186">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="d7861-187">Cambio de credenciales</span><span class="sxs-lookup"><span data-stu-id="d7861-187">Change credentials</span></span>

<span data-ttu-id="d7861-188">Para cambiar las credenciales de una aplicación de AD, ya sea debido a un riesgo de seguridad o a la expiración de una credencial, use los cmdlets [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) y [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential).</span><span class="sxs-lookup"><span data-stu-id="d7861-188">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use the [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="d7861-189">Para quitar todas las credenciales de una aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="d7861-189">To remove all the credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="d7861-190">Para agregar una contraseña, use:</span><span class="sxs-lookup"><span data-stu-id="d7861-190">To add a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="d7861-191">Para agregar un valor de certificado, cree un certificado autofirmado, como se muestra en este tema.</span><span class="sxs-lookup"><span data-stu-id="d7861-191">To add a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="d7861-192">A continuación, use:</span><span class="sxs-lookup"><span data-stu-id="d7861-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-to-simplify-log-in"></a><span data-ttu-id="d7861-193">Guardado del token de acceso para simplificar el inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="d7861-193">Save access token to simplify log in</span></span>
<span data-ttu-id="d7861-194">Para evitar tener que especificar las credenciales de la entidad de servicio cada vez que necesite iniciar sesión, puede guardar el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="d7861-194">To avoid providing the service principal credentials every time it needs to log in, you can save the access token.</span></span>

<span data-ttu-id="d7861-195">Para usar el token de acceso actual en una sesión posterior, guarde el perfil.</span><span class="sxs-lookup"><span data-stu-id="d7861-195">To use the current access token in a later session, save the profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="d7861-196">Abra el perfil y examine su contenido.</span><span class="sxs-lookup"><span data-stu-id="d7861-196">Open the profile and examine its contents.</span></span> <span data-ttu-id="d7861-197">Observe que contiene un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="d7861-197">Notice that it contains an access token.</span></span> <span data-ttu-id="d7861-198">En lugar de tener que volver a iniciar sesión manualmente, solo tiene que cargar el perfil.</span><span class="sxs-lookup"><span data-stu-id="d7861-198">Instead of manually logging in again, simply load the profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="d7861-199">El token de acceso expirará y, por lo tanto, el uso de un perfil guardado solo funcionará mientras el token sea válido.</span><span class="sxs-lookup"><span data-stu-id="d7861-199">The access token expires, so using a saved profile only works for as long as the token is valid.</span></span>
>  

<span data-ttu-id="d7861-200">Como alternativa, puede invocar operaciones de REST desde PowerShell para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="d7861-200">Alternatively, you can invoke REST operations from PowerShell to log in.</span></span> <span data-ttu-id="d7861-201">De la respuesta de autenticación, puede recuperar el token de acceso para su uso con otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="d7861-201">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="d7861-202">Para ver un ejemplo de recuperación del token de acceso mediante la invocación de operaciones REST, consulte [Generación de un token de acceso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="d7861-202">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="d7861-203">Depurar</span><span class="sxs-lookup"><span data-stu-id="d7861-203">Debug</span></span>

<span data-ttu-id="d7861-204">Durante la creación de una entidad de servicio pueden producirse los siguientes errores:</span><span class="sxs-lookup"><span data-stu-id="d7861-204">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="d7861-205">**"Authentication_Unauthorized"** o **"No subscription found in the context"** (No se encuentra una suscripción en el contexto).</span><span class="sxs-lookup"><span data-stu-id="d7861-205">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="d7861-206">- Este error se ve cuando la cuenta no tiene los [permisos necesarios](#required-permissions) en Azure Active Directory para registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7861-206">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="d7861-207">Por lo general, este error aparece cuando los usuarios administradores de Azure Active Directory son los únicos que pueden registrar las aplicaciones y la cuenta no es de un administrador.</span><span class="sxs-lookup"><span data-stu-id="d7861-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="d7861-208">Pida al administrador que le asigne un rol de administrador o que permita a los usuarios registrar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7861-208">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="d7861-209">Su cuenta **"no tiene autorización para realizar la acción 'Microsoft.Authorization/roleAssignments/write' en el ámbito '/ subscriptions / {guid}'."**  - Este error aparece cuando la cuenta no tiene permisos suficientes para asignar un rol a una identidad.</span><span class="sxs-lookup"><span data-stu-id="d7861-209">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="d7861-210">Pida al administrador de suscripciones que le agregue al rol de administrador de acceso de usuario.</span><span class="sxs-lookup"><span data-stu-id="d7861-210">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="d7861-211">Aplicaciones de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d7861-211">Sample applications</span></span>
<span data-ttu-id="d7861-212">Para información sobre el inicio de sesión como en la aplicación a través de distintas plataformas, consulte:</span><span class="sxs-lookup"><span data-stu-id="d7861-212">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="d7861-213">.NET</span><span class="sxs-lookup"><span data-stu-id="d7861-213">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="d7861-214">Java</span><span class="sxs-lookup"><span data-stu-id="d7861-214">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="d7861-215">Node.js</span><span class="sxs-lookup"><span data-stu-id="d7861-215">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="d7861-216">Python</span><span class="sxs-lookup"><span data-stu-id="d7861-216">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="d7861-217">Ruby</span><span class="sxs-lookup"><span data-stu-id="d7861-217">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="d7861-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7861-218">Next steps</span></span>
* <span data-ttu-id="d7861-219">Si desea conocer los pasos detallados de la integración de una aplicación en Azure para administrar recursos, consulte [Guía del desarrollador para la autorización con la API de Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d7861-219">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="d7861-220">Para obtener una explicación más detallada de las aplicaciones y entidades de servicio, consulte [Objetos de aplicación y de entidad de servicio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="d7861-220">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="d7861-221">Para más información sobre la autenticación de Azure Active Directory, consulte [Escenarios de autenticación para Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="d7861-221">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="d7861-222">Para obtener una lista de las acciones que puede conceder o denegar a los usuarios, consulte [Operaciones del proveedor de recursos de Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d7861-222">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

