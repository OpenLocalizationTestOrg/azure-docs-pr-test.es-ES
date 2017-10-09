---
title: "Notas de la versión de API de .NET de almacén 2.x aaaKey | Documentos de Microsoft"
description: "Los desarrolladores de .NET utilizará este toocode API para el almacén de claves de Azure"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="fa2cd-103">.NET 2.0 de Azure Key Vault: notas de la versión y guía de migración</span><span class="sxs-lookup"><span data-stu-id="fa2cd-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="fa2cd-104">Hello siguiente notas e instrucciones son para los desarrolladores que trabajan con Azure Key Vault .NET / biblioteca de C#.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-104">hello following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="fa2cd-105">En transición Hola desde la versión 1.0 de hello versión toohello 2.0, un número de actualizaciones se introdujeron que requieren el trabajo de migración en el código en orden para toobenefit de mejoras funcionales de Hola y adiciones de características como **el almacén de claves certificados** admite.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-105">In hello transition from hello 1.0 version toohello 2.0 version, a number of updates have been made that will require migration work in your code in order for you toobenefit from hello functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="fa2cd-106">Certificados de Key Vault</span><span class="sxs-lookup"><span data-stu-id="fa2cd-106">Key Vault certificates</span></span>

<span data-ttu-id="fa2cd-107">Proporciona compatibilidad con certificados de almacén de claves para la administración de su x509 hello siguientes comportamientos y certificados:</span><span class="sxs-lookup"><span data-stu-id="fa2cd-107">Key Vault certificates support provides for management of your x509 certificates and hello following behaviors:</span></span>  

* <span data-ttu-id="fa2cd-108">Permite un toocreate de propietario del certificado a un certificado a través de un proceso de creación del almacén de claves o importación de Hola de un certificado existente.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-108">Allows a certificate owner toocreate a certificate through a Key Vault creation process or through hello import of an existing certificate.</span></span> <span data-ttu-id="fa2cd-109">Esto incluye tanto certificados autofirmados como certificados generados por una entidad de certificación.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="fa2cd-110">Permite que un propietario de certificado del almacén de claves tooimplement de almacenamiento seguro y la administración de X509 certificados sin la interacción con el material de clave privada.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-110">Allows a Key Vault certificate owner tooimplement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="fa2cd-111">Permite un toocreate de propietario del certificado a una directiva que dirige el almacén de claves toomanage Hola ciclo de vida de un certificado.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-111">Allows a certificate owner toocreate a policy that directs Key Vault toomanage hello life-cycle of a certificate.</span></span>  
* <span data-ttu-id="fa2cd-112">Permite a los propietarios de certificados tooprovide información de contacto para la notificación sobre los eventos de ciclo de vida de expiración y la renovación de certificado.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-112">Allows certificate owners tooprovide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="fa2cd-113">Admite la renovación automática con emisores seleccionados: proveedores de certificados X509 y entidades de certificación asociados con Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="fa2cd-114">Nota: proveedores/entidades no se ha asociado también se permiten pero no admite la característica de renovación automática de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support hello auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="fa2cd-115">Compatibilidad con .NET</span><span class="sxs-lookup"><span data-stu-id="fa2cd-115">.NET support</span></span>

* <span data-ttu-id="fa2cd-116">**.NET 4.0** no es compatible con la versión de Hola 2.0 de hello .NET de almacén de claves de Azure / biblioteca de C#</span><span class="sxs-lookup"><span data-stu-id="fa2cd-116">**.NET 4.0** is not supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="fa2cd-117">**.NET core** es compatible con la versión de Hola 2.0 de hello .NET de almacén de claves de Azure / biblioteca de C#</span><span class="sxs-lookup"><span data-stu-id="fa2cd-117">**.NET Core** is supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="fa2cd-118">Espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="fa2cd-118">Namespaces</span></span>

* <span data-ttu-id="fa2cd-119">Hola espacio de nombres para **modelos** se cambia de **Microsoft.Azure.KeyVault** demasiado**Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-119">hello namespace for **models** is changed from **Microsoft.Azure.KeyVault** too**Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="fa2cd-120">Hola **Microsoft.Azure.KeyVault.Internal** se quita el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-120">hello **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="fa2cd-121">espacio de nombres de las dependencias de Hello Azure SDK se cambian de **Hyak.Common** y **Hyak.Common.Internals** demasiado**Microsoft.Rest** y  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="fa2cd-121">hello Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** too**Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="fa2cd-122">Cambios de tipo</span><span class="sxs-lookup"><span data-stu-id="fa2cd-122">Type changes</span></span>

* <span data-ttu-id="fa2cd-123">*Secreto* cambiado demasiado*SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="fa2cd-123">*Secret* changed too*SecretBundle*</span></span>
* <span data-ttu-id="fa2cd-124">*Diccionario* cambiado demasiado*IDictionary*</span><span class="sxs-lookup"><span data-stu-id="fa2cd-124">*Dictionary* changed too*IDictionary*</span></span>
* <span data-ttu-id="fa2cd-125">*Lista<T>, string []* cambiado demasiado*IList<T>*</span><span class="sxs-lookup"><span data-stu-id="fa2cd-125">*List<T>, string []* changed too*IList<T>*</span></span>
* <span data-ttu-id="fa2cd-126">*NextList* cambiado demasiado *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="fa2cd-126">*NextList* changed too *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="fa2cd-127">Tipos de valor devuelto</span><span class="sxs-lookup"><span data-stu-id="fa2cd-127">Return types</span></span>

* <span data-ttu-id="fa2cd-128">**KeyList** y **SecretList** devolverán *IPage<T>* en lugar de *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="fa2cd-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="fa2cd-129">Hola genera **BackupKeyAsync** devolverá *BackupKeyResult* que contiene *valor* (blob de copia de seguridad).</span><span class="sxs-lookup"><span data-stu-id="fa2cd-129">hello generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="fa2cd-130">Antes de hello método era ajustada y devolver el valor Hola única.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-130">Before hello method was wrapped and returning only hello value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="fa2cd-131">Excepciones</span><span class="sxs-lookup"><span data-stu-id="fa2cd-131">Exceptions</span></span>

* <span data-ttu-id="fa2cd-132">*KeyVaultClientException* cambia demasiado*KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="fa2cd-132">*KeyVaultClientException* is changed too*KeyVaultErrorException*</span></span>
* <span data-ttu-id="fa2cd-133">error del servicio de Hola se cambia de *excepción. Error* demasiado*excepción. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-133">hello service error is changed from *exception.Error* too*exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="fa2cd-134">Quita información adicional del mensaje de error de Hola para **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-134">Removed additional info from hello error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="fa2cd-135">Constructores</span><span class="sxs-lookup"><span data-stu-id="fa2cd-135">Constructors</span></span>

* <span data-ttu-id="fa2cd-136">En lugar de aceptar un *HttpClient* como un argumento de constructor, constructor Hola solo acepta *HttpClientHandler* o *[] DelegatingHandler*.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-136">Instead of accepting an *HttpClient* as a constructor argument, hello constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="fa2cd-137">Paquetes descargados</span><span class="sxs-lookup"><span data-stu-id="fa2cd-137">Downloaded packages</span></span>

<span data-ttu-id="fa2cd-138">Cuando un cliente se está procesando una dependencia en se descargaron siguiente Hola de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="fa2cd-138">When a client is processing a  dependency on Key Vault hello following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="fa2cd-139">Lista de paquetes anterior</span><span class="sxs-lookup"><span data-stu-id="fa2cd-139">Previous package list</span></span>

* <span data-ttu-id="fa2cd-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="fa2cd-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="fa2cd-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="fa2cd-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="fa2cd-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="fa2cd-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="fa2cd-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="fa2cd-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="fa2cd-148">Lista de paquetes actual</span><span class="sxs-lookup"><span data-stu-id="fa2cd-148">Current package list</span></span>

* <span data-ttu-id="fa2cd-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="fa2cd-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="fa2cd-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="fa2cd-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="fa2cd-152">Cambios de clase</span><span class="sxs-lookup"><span data-stu-id="fa2cd-152">Class changes</span></span>

* <span data-ttu-id="fa2cd-153">Se ha quitado la clase **UnixEpoch**</span><span class="sxs-lookup"><span data-stu-id="fa2cd-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="fa2cd-154">**Base64UrlConverter** clase se cambia el nombre demasiado**Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="fa2cd-154">**Base64UrlConverter** class is renamed too**Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="fa2cd-155">Otros cambios</span><span class="sxs-lookup"><span data-stu-id="fa2cd-155">Other changes</span></span>

* <span data-ttu-id="fa2cd-156">Compatibilidad para la configuración de Hola de directiva de reintentos de operación KV en errores transitorios se ha agregado toothis versión de hello API.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-156">Support for hello configuration of KV operation retry policy on transient failures has been added toothis version of hello API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="fa2cd-157">NuGet Microsoft.Azure.Management.KeyVault</span><span class="sxs-lookup"><span data-stu-id="fa2cd-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="fa2cd-158">Para las operaciones de Hola que devuelven un *almacén*, tipo de valor devuelto de hello era una clase que contiene una propiedad de almacén.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-158">For hello operations that returned a *vault*, hello return type was a class that contained a Vault property.</span></span> <span data-ttu-id="fa2cd-159">Hola tipo de valor devuelto es ahora *almacén*.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-159">hello return type is now *Vault*.</span></span>
* <span data-ttu-id="fa2cd-160">Ahora *PermissionsToKeys* y *PermissionsToSecrets* son *Permissions.Keys* y *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="fa2cd-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="fa2cd-161">Algunas de hello devuelven tipos de cambios toohello plano de control también aplican.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-161">Some of hello return types changes apply toohello control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="fa2cd-162">NuGet Microsoft.Azure.KeyVault.Extensions</span><span class="sxs-lookup"><span data-stu-id="fa2cd-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="fa2cd-163">paquete de Hola se divide demasiado**Microsoft.Azure.KeyVault.Extensions** y **Microsoft.Azure.KeyVault.Cryptography** para operaciones criptográficas de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa2cd-163">hello package is broken up too**Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for hello cryptography operations.</span></span>

