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
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>.NET 2.0 de Azure Key Vault: notas de la versión y guía de migración
Hello siguiente notas e instrucciones son para los desarrolladores que trabajan con Azure Key Vault .NET / biblioteca de C#. En transición Hola desde la versión 1.0 de hello versión toohello 2.0, un número de actualizaciones se introdujeron que requieren el trabajo de migración en el código en orden para toobenefit de mejoras funcionales de Hola y adiciones de características como **el almacén de claves certificados** admite.

## <a name="key-vault-certificates"></a>Certificados de Key Vault

Proporciona compatibilidad con certificados de almacén de claves para la administración de su x509 hello siguientes comportamientos y certificados:  

* Permite un toocreate de propietario del certificado a un certificado a través de un proceso de creación del almacén de claves o importación de Hola de un certificado existente. Esto incluye tanto certificados autofirmados como certificados generados por una entidad de certificación.
* Permite que un propietario de certificado del almacén de claves tooimplement de almacenamiento seguro y la administración de X509 certificados sin la interacción con el material de clave privada.  
* Permite un toocreate de propietario del certificado a una directiva que dirige el almacén de claves toomanage Hola ciclo de vida de un certificado.  
* Permite a los propietarios de certificados tooprovide información de contacto para la notificación sobre los eventos de ciclo de vida de expiración y la renovación de certificado.  
* Admite la renovación automática con emisores seleccionados: proveedores de certificados X509 y entidades de certificación asociados con Key Vault.
  
  * Nota: proveedores/entidades no se ha asociado también se permiten pero no admite la característica de renovación automática de Hola.

## <a name="net-support"></a>Compatibilidad con .NET

* **.NET 4.0** no es compatible con la versión de Hola 2.0 de hello .NET de almacén de claves de Azure / biblioteca de C#
* **.NET core** es compatible con la versión de Hola 2.0 de hello .NET de almacén de claves de Azure / biblioteca de C#

## <a name="namespaces"></a>Espacios de nombres

* Hola espacio de nombres para **modelos** se cambia de **Microsoft.Azure.KeyVault** demasiado**Microsoft.Azure.KeyVault.Models**.
* Hola **Microsoft.Azure.KeyVault.Internal** se quita el espacio de nombres.
* espacio de nombres de las dependencias de Hello Azure SDK se cambian de **Hyak.Common** y **Hyak.Common.Internals** demasiado**Microsoft.Rest** y  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>Cambios de tipo

* *Secreto* cambiado demasiado*SecretBundle*
* *Diccionario* cambiado demasiado*IDictionary*
* *Lista<T>, string []* cambiado demasiado*IList<T>*
* *NextList* cambiado demasiado *NextPageLink*

## <a name="return-types"></a>Tipos de valor devuelto

* **KeyList** y **SecretList** devolverán *IPage<T>* en lugar de *ListKeysResponseMessage*
* Hola genera **BackupKeyAsync** devolverá *BackupKeyResult* que contiene *valor* (blob de copia de seguridad). Antes de hello método era ajustada y devolver el valor Hola única.

## <a name="exceptions"></a>Excepciones

* *KeyVaultClientException* cambia demasiado*KeyVaultErrorException*
* error del servicio de Hola se cambia de *excepción. Error* demasiado*excepción. Body.Error.Message*.
* Quita información adicional del mensaje de error de Hola para **[JsonExtensionData]**.

## <a name="constructors"></a>Constructores

* En lugar de aceptar un *HttpClient* como un argumento de constructor, constructor Hola solo acepta *HttpClientHandler* o *[] DelegatingHandler*.

## <a name="downloaded-packages"></a>Paquetes descargados

Cuando un cliente se está procesando una dependencia en se descargaron siguiente Hola de almacén de claves

### <a name="previous-package-list"></a>Lista de paquetes anterior

* package id="Hyak.Common" version="1.0.2" targetFramework="net45"
* package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"
* package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"
* package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"
* package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"
* package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"

### <a name="current-package-list"></a>Lista de paquetes actual

* package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"

## <a name="class-changes"></a>Cambios de clase

* Se ha quitado la clase **UnixEpoch**
* **Base64UrlConverter** clase se cambia el nombre demasiado**Base64UrlJsonConverter**

## <a name="other-changes"></a>Otros cambios

* Compatibilidad para la configuración de Hola de directiva de reintentos de operación KV en errores transitorios se ha agregado toothis versión de hello API.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>NuGet Microsoft.Azure.Management.KeyVault

* Para las operaciones de Hola que devuelven un *almacén*, tipo de valor devuelto de hello era una clase que contiene una propiedad de almacén. Hola tipo de valor devuelto es ahora *almacén*.
* Ahora *PermissionsToKeys* y *PermissionsToSecrets* son *Permissions.Keys* y *Permissions.Secrets*
* Algunas de hello devuelven tipos de cambios toohello plano de control también aplican.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>NuGet Microsoft.Azure.KeyVault.Extensions

* paquete de Hola se divide demasiado**Microsoft.Azure.KeyVault.Extensions** y **Microsoft.Azure.KeyVault.Cryptography** para operaciones criptográficas de Hola.

