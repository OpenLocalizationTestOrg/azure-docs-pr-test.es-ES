---
title: "Notas de la versión de la API de .NET 2.x de Key Vault | Microsoft Docs"
description: "Los desarrolladores de .NET usarán esta API para programar para Azure Key Vault"
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
ms.openlocfilehash: c5b5fd7f16faf17d16ecc82269fb1264adf4dd06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="31791-103">.NET 2.0 de Azure Key Vault: notas de la versión y guía de migración</span><span class="sxs-lookup"><span data-stu-id="31791-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="31791-104">Tanto las notas como la guía siguientes son para desarrolladores que trabajan con la biblioteca de C# o .NET de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="31791-104">The following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="31791-105">En la transición de la versión 1.0 a la versión 2.0, se han creado una serie de actualizaciones que requerirán un trabajo de migración en su código para que pueda disfrutar de las mejoras funcionales y la incorporación de características, como, por ejemplo, la compatibilidad con **certificados de Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="31791-105">In the transition from the 1.0 version to the 2.0 version, a number of updates have been made that will require migration work in your code in order for you to benefit from the functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="31791-106">Certificados de Key Vault</span><span class="sxs-lookup"><span data-stu-id="31791-106">Key Vault certificates</span></span>

<span data-ttu-id="31791-107">La compatibilidad con certificados de Key Vault proporciona la administración de sus certificados x509 y los comportamientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="31791-107">Key Vault certificates support provides for management of your x509 certificates and the following behaviors:</span></span>  

* <span data-ttu-id="31791-108">Permite que el propietario de un certificado cree un certificado a través de un proceso de creación de Key Vault o a través de la importación de un certificado existente.</span><span class="sxs-lookup"><span data-stu-id="31791-108">Allows a certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate.</span></span> <span data-ttu-id="31791-109">Esto incluye tanto certificados autofirmados como certificados generados por una entidad de certificación.</span><span class="sxs-lookup"><span data-stu-id="31791-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="31791-110">Permite que el propietario de un certificado de Key Vault implemente un almacenamiento seguro y la administración de certificados X509 sin interacción con material de clave privada.</span><span class="sxs-lookup"><span data-stu-id="31791-110">Allows a Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="31791-111">Permite que el propietario de un certificado cree una directiva que indique a Key Vault cómo administrar el ciclo de vida de un certificado.</span><span class="sxs-lookup"><span data-stu-id="31791-111">Allows a certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.</span></span>  
* <span data-ttu-id="31791-112">Permite que los propietarios de certificados proporcionen información de contacto para la notificación de eventos del ciclo de vida de caducidad y renovación de los certificados.</span><span class="sxs-lookup"><span data-stu-id="31791-112">Allows certificate owners to provide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="31791-113">Admite la renovación automática con emisores seleccionados: proveedores de certificados X509 y entidades de certificación asociados con Key Vault.</span><span class="sxs-lookup"><span data-stu-id="31791-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="31791-114">NOTA: Los proveedores y entidades no asociados también pueden, pero en este caso no se admitirá la característica de renovación automática.</span><span class="sxs-lookup"><span data-stu-id="31791-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support the auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="31791-115">Compatibilidad con .NET</span><span class="sxs-lookup"><span data-stu-id="31791-115">.NET support</span></span>

* <span data-ttu-id="31791-116">**.NET 4.0** no es compatible con la versión 2.0 de .NET de Azure Key Vault ni con la biblioteca de C#</span><span class="sxs-lookup"><span data-stu-id="31791-116">**.NET 4.0** is not supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="31791-117">**.NET Core** no es compatible con la versión 2.0 de .NET de Azure Key Vault ni con la biblioteca de C#</span><span class="sxs-lookup"><span data-stu-id="31791-117">**.NET Core** is supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="31791-118">Espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="31791-118">Namespaces</span></span>

* <span data-ttu-id="31791-119">El espacio de nombres para **modelos** se cambia de **Microsoft.Azure.KeyVault** a **Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="31791-119">The namespace for **models** is changed from **Microsoft.Azure.KeyVault** to **Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="31791-120">El espacio de nombres **Microsoft.Azure.KeyVault.Internal** se quita.</span><span class="sxs-lookup"><span data-stu-id="31791-120">The **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="31791-121">El espacio de nombres de las dependencias del SDK de Azure se cambia de **Hyak.Common** y **Hyak.Common.Internals** a **Microsoft.Rest** y **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="31791-121">The Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** to **Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="31791-122">Cambios de tipo</span><span class="sxs-lookup"><span data-stu-id="31791-122">Type changes</span></span>

* <span data-ttu-id="31791-123">*Secret* se cambia a *SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="31791-123">*Secret* changed to *SecretBundle*</span></span>
* <span data-ttu-id="31791-124">*Dictionary* se cambia a *IDictionary*</span><span class="sxs-lookup"><span data-stu-id="31791-124">*Dictionary* changed to *IDictionary*</span></span>
* <span data-ttu-id="31791-125">*List<T>, string []* se cambia a *IList<T>*</span><span class="sxs-lookup"><span data-stu-id="31791-125">*List<T>, string []* changed to *IList<T>*</span></span>
* <span data-ttu-id="31791-126">*NextList* se cambia a  *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="31791-126">*NextList* changed to  *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="31791-127">Tipos de valor devuelto</span><span class="sxs-lookup"><span data-stu-id="31791-127">Return types</span></span>

* <span data-ttu-id="31791-128">**KeyList** y **SecretList** devolverán *IPage<T>* en lugar de *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="31791-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="31791-129">El valor **BackupKeyAsync** generado devolverá *BackupKeyResult*, que contiene *Value* (blob de copia de seguridad).</span><span class="sxs-lookup"><span data-stu-id="31791-129">The generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="31791-130">Antes se ajustó el método, devolviendo solo el valor.</span><span class="sxs-lookup"><span data-stu-id="31791-130">Before the method was wrapped and returning only the value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="31791-131">Excepciones</span><span class="sxs-lookup"><span data-stu-id="31791-131">Exceptions</span></span>

* <span data-ttu-id="31791-132">*KeyVaultClientException* se cambia a *KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="31791-132">*KeyVaultClientException* is changed to *KeyVaultErrorException*</span></span>
* <span data-ttu-id="31791-133">El error de servicio se cambia de *exception.Error* a *exception.Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="31791-133">The service error is changed from *exception.Error* to *exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="31791-134">Información adicional quitada del mensaje de error para **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="31791-134">Removed additional info from the error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="31791-135">Constructores</span><span class="sxs-lookup"><span data-stu-id="31791-135">Constructors</span></span>

* <span data-ttu-id="31791-136">En lugar de aceptar *HttpClient* como argumento de constructor, el constructor solo acepta *HttpClientHandler* o *DelegatingHandler[]*.</span><span class="sxs-lookup"><span data-stu-id="31791-136">Instead of accepting an *HttpClient* as a constructor argument, the constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="31791-137">Paquetes descargados</span><span class="sxs-lookup"><span data-stu-id="31791-137">Downloaded packages</span></span>

<span data-ttu-id="31791-138">Al procesar un cliente una dependencia en Key Vault, se descargaron los siguientes</span><span class="sxs-lookup"><span data-stu-id="31791-138">When a client is processing a  dependency on Key Vault the following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="31791-139">Lista de paquetes anterior</span><span class="sxs-lookup"><span data-stu-id="31791-139">Previous package list</span></span>

* <span data-ttu-id="31791-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="31791-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="31791-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="31791-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="31791-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="31791-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="31791-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="31791-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="31791-148">Lista de paquetes actual</span><span class="sxs-lookup"><span data-stu-id="31791-148">Current package list</span></span>

* <span data-ttu-id="31791-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="31791-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="31791-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="31791-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="31791-152">Cambios de clase</span><span class="sxs-lookup"><span data-stu-id="31791-152">Class changes</span></span>

* <span data-ttu-id="31791-153">Se ha quitado la clase **UnixEpoch**</span><span class="sxs-lookup"><span data-stu-id="31791-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="31791-154">El nombre de la clase **Base64UrlConverter** se ha cambiado a **Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="31791-154">**Base64UrlConverter** class is renamed to **Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="31791-155">Otros cambios</span><span class="sxs-lookup"><span data-stu-id="31791-155">Other changes</span></span>

* <span data-ttu-id="31791-156">La compatibilidad con la configuración de la directiva de reintentos de operaciones de KV sobre errores transitorios se ha agregado a esta versión de la API.</span><span class="sxs-lookup"><span data-stu-id="31791-156">Support for the configuration of KV operation retry policy on transient failures has been added to this version of the API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="31791-157">NuGet Microsoft.Azure.Management.KeyVault</span><span class="sxs-lookup"><span data-stu-id="31791-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="31791-158">Para las operaciones que devolvieron un *almacén*, el tipo de valor devuelto era una clase que contenía una propiedad Vault.</span><span class="sxs-lookup"><span data-stu-id="31791-158">For the operations that returned a *vault*, the return type was a class that contained a Vault property.</span></span> <span data-ttu-id="31791-159">Ahora el tipo de valor devuelto es *Vault*.</span><span class="sxs-lookup"><span data-stu-id="31791-159">The return type is now *Vault*.</span></span>
* <span data-ttu-id="31791-160">Ahora *PermissionsToKeys* y *PermissionsToSecrets* son *Permissions.Keys* y *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="31791-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="31791-161">Algunos de los cambios de tipos de valor devuelto se aplican también al plano de control.</span><span class="sxs-lookup"><span data-stu-id="31791-161">Some of the return types changes apply to the control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="31791-162">NuGet Microsoft.Azure.KeyVault.Extensions</span><span class="sxs-lookup"><span data-stu-id="31791-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="31791-163">El paquete se divide en **Microsoft.Azure.KeyVault.Extensions** y **Microsoft.Azure.KeyVault.Cryptography** para las operaciones de criptografía.</span><span class="sxs-lookup"><span data-stu-id="31791-163">The package is broken up to **Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for the cryptography operations.</span></span>

