---
title: "aaaAzure objetos de entidad de servicio y aplicación de Active Directory | Documentos de Microsoft"
description: "Obtener una explicación de la relación de hello entre la aplicación y los objetos de entidad de servicio en Azure Active Directory"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Objetos de aplicación y de entidad de servicio de Azure Active Directory (Azure AD)
A veces Hola significado del término Hola puede malinterpretarse "application" cuando se utiliza en el contexto de Hola de Azure AD. objetivo de Hola de este artículo es toomake lo más clara, al clarificar aspectos concretos y conceptuales de integración de aplicaciones de Azure AD, con una ilustración de registro y su consentimiento para un [aplicación multiempresa](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Información general
Una aplicación que se ha integrado con Azure AD tiene implicaciones que van más allá de los aspectos de software de Hola. "Aplicación" se suele usar como un término conceptual, que hace referencia toonot solo Hola Hola software de la aplicación, pero también su registro de Azure AD y roles en la autenticación/autorización "conversaciones" en tiempo de ejecución. Por definición, una aplicación puede funcionar en un [cliente](active-directory-dev-glossary.md#client-application) rol (consume un recurso), un [servidor de recursos](active-directory-dev-glossary.md#resource-server) rol (expone las API tooclients), o incluso ambos. Protocolo de conversación Hola se define mediante una [flujo de concesión de autorización de OAuth 2.0](active-directory-dev-glossary.md#authorization-grant), lo que permite Hola cliente/recursos tooaccess/proteger los datos de un recurso respectivamente. Ahora vamos a un nivel más profundo y ver cómo el modelo de aplicación hello Azure AD representa una aplicación en tiempo de diseño y tiempo de ejecución. 

## <a name="application-registration"></a>Registro de la aplicación
Al registrar una aplicación de Azure AD en hello [portal de Azure][AZURE-Portal], se crean dos objetos en el inquilino de Azure AD: un objeto de aplicación y un objeto de entidad de servicio.

#### <a name="application-object"></a>Objeto de aplicación
Una aplicación de Azure AD se define mediante su uno y solo objeto de aplicación, que reside en el inquilino de Azure AD Hola donde se registró la aplicación hello, conocido como inquilino de la aplicación hello "inicio". Hello Azure AD Graph [entidad aplicaciones] [ AAD-Graph-App-Entity] define el esquema de Hola para las propiedades de un objeto de aplicación. 

#### <a name="service-principal-object"></a>Objeto de entidad de servicio
objeto de entidad de servicio de Hello define Hola directiva y los permisos de uso de una aplicación en un específicos del inquilino, proporcionando la base de Hola para una aplicación de hello toorepresent principal de seguridad en tiempo de ejecución. Hello Azure AD Graph [entidad ServicePrincipal] [ AAD-Graph-Sp-Entity] define Hola esquema para las propiedades de un objeto principal de servicio. 

#### <a name="application-and-service-principal-relationship"></a>Relación entre la aplicación y la entidad de servicio
Considere la posibilidad de objeto de la aplicación hello como hello *global* representación de la aplicación para su uso en todos los inquilinos y entidad de servicio de hello como hello *local* representación para su uso en un determinado inquilino. Hello objeto application actúa como hello plantilla desde qué comunes y propiedades predeterminadas son *derivado* para su uso en la creación de objetos de entidad de seguridad de servicio correspondientes. Por lo tanto, un objeto de aplicación tiene una relación de 1:1 con la aplicación de software de hello y una relación de 1: muchas con sus correspondientes objetos de entidad de seguridad de servicio.

Una entidad de servicio debe crearse en todos los inquilinos en su aplicación hello se usará, lo que le tooestablish una identidad para el inicio de sesión o tooresources de acceso está protegida por inquilino Hola. Una aplicación de un único inquilino tendrá solo una entidad de servicio (en su inquilino principal), que normalmente se crea y consiente para su uso durante el registro de aplicación. Una aplicación Web de varios inquilinos/API también tendrá una entidad de servicio creada en cada inquilino donde un usuario de ese inquilino ha dado su consentimiento tooits uso.  

> [!NOTE]
> Los cambios que realice tooyour objeto de aplicación, también se reflejan en su objeto de entidad de seguridad de servicio en particular inquilinos la aplicación hello sólo (donde se registró un inquilino hello). Para las aplicaciones de varios inquilinos, objeto de aplicación de toohello de cambios no se reflejan en objetos de entidad de servicio de los inquilinos de cualquier consumidor, hasta que se quite el acceso de Hola a través de hello [Panel de acceso de la aplicación](https://myapps.microsoft.com) y concedido de nuevo.
><br>  
> Tenga en cuenta también que las aplicaciones nativas se registran como multiinquilino de forma predeterminada.
> 
> 

## <a name="example"></a>Ejemplo
Hello siguiente diagrama ilustra Hola relación entre una aplicación objeto de aplicación y servicio correspondiente objetos de entidad de seguridad, en el contexto de Hola de una aplicación de varios inquilinos de ejemplo denominados **HR app**. En este escenario hay tres inquilinos de Azure AD: 

* **Adatum** : hello inquilinos utilizado por la compañía de Hola que desarrolló hello **HR app**
* **Contoso** : hello inquilinos utilizado por hello organización de Contoso, que es un consumidor de hello **HR app**
* **Fabrikam** : hello inquilinos utilizado por la organización de Fabrikam, lo que también consume Hola Hola **HR app**

![Relación entre un objeto de aplicación y un objeto de entidad de servicio](./media/active-directory-application-objects/application-objects-relationship.png)

En el diagrama anterior de hello, paso 1 es proceso Hola de creación de aplicación hello y objetos de entidad de servicio de inquilino principal de la aplicación hello.

En el paso 2, cuando los administradores de Contoso y Fabrikam completar su consentimiento, un objeto de entidad de servicio se crea en inquilino de Azure AD de su empresa y los permisos de hello asignado ese administrador Hola concedido. También tenga en cuenta que la aplicación hello recursos humanos puede consentimiento tooallow configurado/diseñado por los usuarios para uso individual.

En el paso 3, los inquilinos de consumidor de Hola de aplicación de recursos humanos (Contoso y Fabrikam) cada hello tienen su propio objeto de entidad de servicio. Cada uno representa el uso de una instancia de la aplicación hello en tiempo de ejecución, regido Hola dado su consentimiento de permisos de administrador respectivos Hola.

## <a name="next-steps"></a>Pasos siguientes
Objeto de aplicación de la aplicación son accesibles a través de la API de Azure AD Graph, Hola hello [portal de Azure] [ AZURE-Portal] editor de manifiestos de aplicación, o [cmdlets de PowerShell de Azure AD](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), tal como está representado por su OData [entidad aplicaciones][AAD-Graph-App-Entity].

Objeto de entidad de servicio de una aplicación son accesibles a través de la API de Azure AD Graph Hola o [cmdlets de PowerShell de Azure AD](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), tal como está representado por su OData [entidad ServicePrincipal] [ AAD-Graph-Sp-Entity].

Hola [Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/) es útil para consultar la aplicación hello y objetos de entidad de servicio.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
