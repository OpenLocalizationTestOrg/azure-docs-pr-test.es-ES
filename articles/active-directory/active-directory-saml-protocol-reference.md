---
title: Referencia del protocolo SAML AD aaaAzure | Documentos de Microsoft
description: "Este artículo proporciona información general sobre los perfiles de inicio de sesión único y SAML de cierre de sesión único de hello en Azure Active Directory."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.openlocfilehash: d540b8cd9352e3196a0f4a40f0070d0e61127bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Cómo Azure Active Directory usa el protocolo SAML de Hola
Azure Active Directory (Azure AD) usa Hola experiencia tootheir usuarios de aplicaciones tooprovide un inicio de sesión único de SAML 2.0 protocolo tooenable. Hola [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) y [cierre de sesión único](active-directory-single-sign-out-protocol-reference.md) perfiles SAML de Azure AD explican cómo se usan las aserciones de SAML, protocolos y enlaces en el servicio de proveedor de identidad de Hola.

Protocolo SAML requiere el proveedor de identidades de hello (Azure AD) y Hola proveedor (aplicación hello) tooexchange información sobre ellos mismos.

Cuando una aplicación se registra con Azure AD, el desarrollador de aplicaciones de Hola registra información relacionada con la federación con Azure AD. Esto incluye hello **URI de redireccionamiento** de aplicación hello.

Azure Active Directory expone puntos de conexión de inicio y cierre de sesión único comunes y específicos del inquilino (independientes del inquilino). Estas direcciones URL representan ubicaciones direccionables, no son únicamente identificadores--para que pueda ir toohello extremo tooread Hola metadatos.

* extremo de Hello específico del inquilino se encuentra en `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.  Hola <TenantDomainName> marcador de posición representa un nombre de dominio registrado o GUID de TenantID de un inquilino de Azure AD. Por ejemplo, están Hola de metadatos de federación del inquilino de contoso.com hello en: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* extremo de Hello independientes del inquilino se encuentra en `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. En esta dirección de extremo, **común** aparece, en lugar de un identificador o el nombre de dominio de inquilino

Para obtener información acerca de los documentos de metadatos de federación de Hola que Azure AD publica, vea [metadatos de federación](active-directory-federation-metadata.md).
