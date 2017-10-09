---
title: "aaaManage el almacén de claves en la pila de Azure mediante PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage el almacén de claves en la pila de Azure con PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 37adddf8da02766559f4d61134a9d5ce47377da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a><span data-ttu-id="94d85-103">Administrar Key Vault en Azure Stack mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="94d85-103">Manage Key Vault in Azure Stack using PowerShell</span></span>

<span data-ttu-id="94d85-104">En este artículo le ayuda a obtener toocreate iniciada y administrar el almacén de claves en la pila de Azure mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94d85-104">This article helps you get started toocreate and manage Key Vault in Azure Stack by using PowerShell.</span></span> <span data-ttu-id="94d85-105">cmdlets de PowerShell de almacén de claves de Hello descritos en este artículo están disponibles como parte del SDK de Azure PowerShell Hola.</span><span class="sxs-lookup"><span data-stu-id="94d85-105">hello Key Vault PowerShell cmdlets described in this article are available as a part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="94d85-106">Hello las secciones siguientes describen los cmdlets de PowerShell de Hola que son necesario toocreate un almacén, almacenar y administrar las claves criptográficas y secretos, así como para autorizar a los usuarios o aplicaciones operaciones tooinvoke en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d85-106">hello following sections describe hello PowerShell cmdlets that are required toocreate a vault, store, and manage cryptographic keys and secrets as well as authorize users or applications tooinvoke operations in hello vault.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="94d85-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="94d85-107">Prerequisites</span></span>
* [<span data-ttu-id="94d85-108">Instale PowerShell para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="94d85-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* <span data-ttu-id="94d85-109">Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d85-109">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="94d85-110">Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d85-110">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span> 
* [<span data-ttu-id="94d85-111">Configurar el entorno de PowerShell del usuario de hello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="94d85-111">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a><span data-ttu-id="94d85-112">Habilitación de la suscripción de inquilino para operaciones de almacén</span><span class="sxs-lookup"><span data-stu-id="94d85-112">Enable your tenant subscription for vault operations</span></span>

<span data-ttu-id="94d85-113">Para poder emitir cualquier operación en un almacén de claves, debe tooensure que su suscripción de inquilino está habilitada para las operaciones del almacén.</span><span class="sxs-lookup"><span data-stu-id="94d85-113">Before you can issue any operations against a key vault, you need tooensure that your tenant subscription is enabled for vault operations.</span></span> <span data-ttu-id="94d85-114">tooverify, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="94d85-114">tooverify, run hello following command:</span></span>

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
<span data-ttu-id="94d85-115">**Salida**</span><span class="sxs-lookup"><span data-stu-id="94d85-115">**Output**</span></span>

<span data-ttu-id="94d85-116">Si la suscripción está habilitada para las operaciones del almacén, la salida de hello muestra "RegistrationState" es igual a "Registrado" para todos los tipos de recursos de un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="94d85-116">If your subscription is enabled for vault operations, hello output shows “RegistrationState” equals “Registered” for all resource types of a key vault.</span></span>

![estado de registro](media/azure-stack-kv-manage-powershell/image1.png)

<span data-ttu-id="94d85-118">Si no es el caso de hello, invoque Hola después el servicio de almacén de claves de comando tooregister hello en su suscripción:</span><span class="sxs-lookup"><span data-stu-id="94d85-118">If that’s not hello case, invoke hello following command tooregister hello Key Vault service in your subscription:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

<span data-ttu-id="94d85-119">**Salida**</span><span class="sxs-lookup"><span data-stu-id="94d85-119">**Output**</span></span>

<span data-ttu-id="94d85-120">Si el registro de hello es correcta, hello siguiente resultado se devuelve:</span><span class="sxs-lookup"><span data-stu-id="94d85-120">If hello registration is successful, hello following output is returned:</span></span>

![registro](media/azure-stack-kv-manage-powershell/image2.png)

<span data-ttu-id="94d85-122">Hello las secciones siguientes se supone se registraba el servicio de almacén de claves de suscripción de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d85-122">hello following sections assume Key Vault service is registered within hello user subscription.</span></span> <span data-ttu-id="94d85-123">Al invocar comandos de almacén de claves, si se produce un error: "hello suscripción no tiene espacio de nombres registrado toouse ' Microsoft.KeyVault" a continuación, confirme que tiene [habilitado el proveedor de recursos de almacén de claves de hello](#enable-your-tenant-subscription-for-vault-operations) según las instrucciones se ha mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="94d85-123">When invoking key vault commands, if you get an error- "hello subscription is not registered toouse namespace ‘Microsoft.KeyVault" then, confirm that you have [enabled hello Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) as per instructions mentioned earlier.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="94d85-124">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="94d85-124">Create a key vault</span></span> 

<span data-ttu-id="94d85-125">Antes de crear un almacén de claves, cree un grupo de recursos para que todos los recursos relacionados con el almacén de claves se encuentren en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="94d85-125">Before you create a key vault, create a resource group so that all key vault related resources exist in a resource group.</span></span> <span data-ttu-id="94d85-126">Usar hello después comando toocreate un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="94d85-126">Use hello following command toocreate a new resource group:</span></span>

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

<span data-ttu-id="94d85-127">**Salida**</span><span class="sxs-lookup"><span data-stu-id="94d85-127">**Output**</span></span>

![nuevo grupo de recursos](media/azure-stack-kv-manage-powershell/image3.png)

<span data-ttu-id="94d85-129">Ahora, utilice hello **AzureRMKeyVault New** comando toocreate un almacén de claves de grupo de recursos de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="94d85-129">Now, use hello **New-AzureRMKeyVault** command toocreate a key vault in hello resource group that you created earlier.</span></span> <span data-ttu-id="94d85-130">Este comando lee tres parámetros obligatorios: el nombre del grupo de recursos, el nombre del almacén de claves y la ubicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="94d85-130">This command reads three mandatory parameters- resource group name, key vault name, and geographic location.</span></span> 

<span data-ttu-id="94d85-131">Ejecute hello después toocreate de comando en un almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="94d85-131">Run hello following command toocreate a key vault:</span></span>

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
<span data-ttu-id="94d85-132">**Salida**</span><span class="sxs-lookup"><span data-stu-id="94d85-132">**Output**</span></span>

![new kv](media/azure-stack-kv-manage-powershell/image4.png)

<span data-ttu-id="94d85-134">salida de Hello de este comando muestra las propiedades de Hola de almacén de claves de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="94d85-134">hello output of this command shows hello properties of hello key vault that you created.</span></span> <span data-ttu-id="94d85-135">Cuando una aplicación tiene acceso a este almacén, usa hello **almacén URI** propiedad que se muestra en la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="94d85-135">When an application accesses this vault, it uses hello **Vault URI** property shown in hello output.</span></span> <span data-ttu-id="94d85-136">Por ejemplo, el almacén de hello URI aquí es **https://vault01.vault.local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="94d85-136">For example, hello vault URI here is **https://vault01.vault.local.azurestack.external**.</span></span> <span data-ttu-id="94d85-137">Las aplicaciones que interactúan con este almacén de claves a través de la API de REST deben usar este URI.</span><span class="sxs-lookup"><span data-stu-id="94d85-137">Applications interacting with this key vault through REST API must use this URI.</span></span>

<span data-ttu-id="94d85-138">En implementaciones basadas en ADFS, al crear un almacén de claves mediante PowerShell, puede aparecer la advertencia "Access policy is not set.</span><span class="sxs-lookup"><span data-stu-id="94d85-138">In ADFS-based deployments, when you create a key vault by using PowerShell, you might receive a warning that says "Access policy is not set.</span></span> <span data-ttu-id="94d85-139">Ningún usuario o una aplicación tiene toouse de permiso de acceso a este almacén".</span><span class="sxs-lookup"><span data-stu-id="94d85-139">No user or application has access permission toouse this vault".</span></span> <span data-ttu-id="94d85-140">tooresolve este problema, establezca una directiva de acceso para el almacén de Hola por mediante hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) comando:</span><span class="sxs-lookup"><span data-stu-id="94d85-140">tooresolve this issue, set an access policy for hello vault by using hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span></span>

```PowerShell
# Obtain hello security identifier(SID) of hello active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set hello key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="94d85-141">Administración de claves y secretos</span><span class="sxs-lookup"><span data-stu-id="94d85-141">Manage keys and secrets</span></span>

<span data-ttu-id="94d85-142">Después de crear un almacén, use Hola siguiendo los pasos toocreate y administración de claves y secretos en el almacén de Hola de.</span><span class="sxs-lookup"><span data-stu-id="94d85-142">After creating a vault, use hello following steps toocreate and manage keys and secrets within hello vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="94d85-143">Crear una clave</span><span class="sxs-lookup"><span data-stu-id="94d85-143">Create a key</span></span>

<span data-ttu-id="94d85-144">Hola de uso **Add-AzureKeyVaultKey** comando toocreate o importar una clave protegida de software en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="94d85-144">Use hello **Add-AzureKeyVaultKey** command toocreate or import a software protected key in a key vault.</span></span> 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
<span data-ttu-id="94d85-145">Hola **destino** se usa el parámetro toospecify esa clave hello es un software protegido.</span><span class="sxs-lookup"><span data-stu-id="94d85-145">hello **Destination** parameter is used toospecify that hello key is software protected.</span></span> <span data-ttu-id="94d85-146">Cuando se crea correctamente la clave de hello, Hola comando da como resultado detalles Hola Hola que se creó la clave.</span><span class="sxs-lookup"><span data-stu-id="94d85-146">When hello key is successfully created, hello command outputs hello details of hello created key.</span></span>

<span data-ttu-id="94d85-147">**Salida**</span><span class="sxs-lookup"><span data-stu-id="94d85-147">**Output**</span></span>

![Nueva clave](media/azure-stack-kv-manage-powershell/image5.png)

<span data-ttu-id="94d85-149">Ahora puede hacer referencia a Hola se creó la clave mediante el uso de su URI.</span><span class="sxs-lookup"><span data-stu-id="94d85-149">You can now reference hello created key by using its URI.</span></span> <span data-ttu-id="94d85-150">Si crea o importar una clave que tenga el mismo nombre que una clave existente, clave de hello original se actualiza con los valores de hello que se especifican en la nueva clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d85-150">If you create or import a key that has same name as an existing key, hello original key is updated with hello values that are specified in hello new key.</span></span>  <span data-ttu-id="94d85-151">Se puede tener acceso versión anterior de hello mediante Hola específicos de la versión URI de clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d85-151">You can access hello previous version by using hello version-specific URI of hello key.</span></span> <span data-ttu-id="94d85-152">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="94d85-152">For example,</span></span> 

* <span data-ttu-id="94d85-153">Use **https://vault10.vault.local.azurestack.external:443/claves/key01** tooalways obtener la versión actual de Hola</span><span class="sxs-lookup"><span data-stu-id="94d85-153">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** tooalways get hello current version</span></span>  
* <span data-ttu-id="94d85-154">Use **https://vault010.vault.local.azurestack.external:443/claves/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget esta versión específica</span><span class="sxs-lookup"><span data-stu-id="94d85-154">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget this specific version</span></span>

### <a name="get-a-key"></a><span data-ttu-id="94d85-155">Obtener una clave</span><span class="sxs-lookup"><span data-stu-id="94d85-155">Get a key</span></span>

<span data-ttu-id="94d85-156">Hola de uso **Get-AzureKeyVaultKey** comandos tooread una clave y sus detalles.</span><span class="sxs-lookup"><span data-stu-id="94d85-156">Use hello **Get-AzureKeyVaultKey** command tooread a key and its details.</span></span>

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a><span data-ttu-id="94d85-157">Crear un secreto</span><span class="sxs-lookup"><span data-stu-id="94d85-157">Create a secret</span></span>

<span data-ttu-id="94d85-158">Hola de uso **AzureKeyVaultSecret conjunto** comando toocreate o actualizar un secreto en un almacén.</span><span class="sxs-lookup"><span data-stu-id="94d85-158">Use hello **Set-AzureKeyVaultSecret** command toocreate or update a secret in a vault.</span></span> <span data-ttu-id="94d85-159">Si aún no existe, y se crea una nueva versión del secreto de hello si ya existe, se crea un secreto.</span><span class="sxs-lookup"><span data-stu-id="94d85-159">A secret is created if it doesn’t already exist, and a new version of hello secret is created if it already exists.</span></span>

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

<span data-ttu-id="94d85-160">**Salida**</span><span class="sxs-lookup"><span data-stu-id="94d85-160">**Output**</span></span>

![crear secreto](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a><span data-ttu-id="94d85-162">Obtener un secreto</span><span class="sxs-lookup"><span data-stu-id="94d85-162">Get a secret</span></span>

<span data-ttu-id="94d85-163">Hola de uso **Get AzureKeyVaultSecret** comando tooread un secreto en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="94d85-163">Use hello **Get-AzureKeyVaultSecret** command tooread a secret in a key vault.</span></span> <span data-ttu-id="94d85-164">Este comando puede devolver todas las versiones de un secreto o algunas versiones concretas.</span><span class="sxs-lookup"><span data-stu-id="94d85-164">This command can return all or specific versions of a secret.</span></span> 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

<span data-ttu-id="94d85-165">Después de crear claves y secretos, puede autorizar aplicaciones externas toouse ellos.</span><span class="sxs-lookup"><span data-stu-id="94d85-165">After creating keys and secrets, you can authorize external applications toouse them.</span></span>

## <a name="authorize-an-application-toouse-a-key-or-secret"></a><span data-ttu-id="94d85-166">Autorizar una toouse una clave o un secreto de aplicación</span><span class="sxs-lookup"><span data-stu-id="94d85-166">Authorize an application toouse a key or secret</span></span>

<span data-ttu-id="94d85-167">tooauthorize una tooaccess una clave de aplicación o al secreto en hello clave almacén, use hello **Set-AzureRmKeyVaultAccessPolicy** comando.</span><span class="sxs-lookup"><span data-stu-id="94d85-167">tooauthorize an application tooaccess a key or secret in hello key vault, use hello **Set-AzureRmKeyVaultAccessPolicy** command.</span></span>
<span data-ttu-id="94d85-168">Por ejemplo, si el nombre del almacén es aplicación hello y ContosoKeyVault desea tooauthorize tiene un identificador de cliente de 8f8c4bbd 485b 45fd 98f7 ec6300b7b4ed.</span><span class="sxs-lookup"><span data-stu-id="94d85-168">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a Client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span></span> <span data-ttu-id="94d85-169">Ejecute hello tras la aplicación de comando tooauthorize Hola.</span><span class="sxs-lookup"><span data-stu-id="94d85-169">Run hello following command tooauthorize hello application.</span></span> <span data-ttu-id="94d85-170">Si lo desea, puede especificar hello **PermissionsToKeys** permisos tooset de parámetro para un usuario, aplicación o un grupo de seguridad:</span><span class="sxs-lookup"><span data-stu-id="94d85-170">Optionally, you can specify hello **PermissionsToKeys** parameter tooset permissions for a user, application, or a security group:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="94d85-171">Si desea tooauthorize ese mismo secretos tooread de aplicación en el almacén, ejecute hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="94d85-171">If you want tooauthorize that same application tooread secrets in your vault, run hello following cmdlet:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a><span data-ttu-id="94d85-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94d85-172">Next Steps</span></span>
* [<span data-ttu-id="94d85-173">Implementación de una máquina virtual con una contraseña almacenada en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="94d85-173">Deploy a VM with password stored in a Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="94d85-174">Implementación de una máquina virtual con un certificado almacenado en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="94d85-174">Deploy a VM with certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md) 
