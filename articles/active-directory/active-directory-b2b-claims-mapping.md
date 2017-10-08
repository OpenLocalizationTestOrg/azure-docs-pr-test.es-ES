---
title: "asignación en Azure Active Directory las notificaciones de usuario de colaboración aaaB2B | Documentos de Microsoft"
description: "referencia de asignación de notificaciones para la colaboración B2B de Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a>Asignación de notificaciones de usuario de colaboración B2B de Azure Active Directory

Azure Active Directory (Azure AD) es compatible con personalizar las notificaciones de hello emitidas en el token SAML de Hola para los usuarios de la colaboración B2B. Cuando un usuario autentica toohello aplicación, Azure AD emite una aplicación de toohello token de SAML que contiene información (o notificaciones) acerca del usuario de Hola que identifica de forma única a ellos. De forma predeterminada, esto incluye el nombre de usuario, dirección de correo electrónico, nombre y apellido del usuario de Hola. Puede ver o editar notificaciones Hola enviados en la aplicación de toohello token de SAML en la ficha de atributos de Hola Hola.

Hay dos razones posibles por las que puede necesitar notificaciones de hello tooedit emitidas en el token SAML de Hola.

1. aplicación Hello se ha escrito toorequire otro conjunto de notificaciones URI o valores de notificación

2. La aplicación necesita toobe de notificación de NameIdentifier Hola algo distinto de nombre principal de usuario Hola almacenado en Azure Active Directory.

  ![Visualización de notificaciones en el token SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

Para obtener información sobre cómo tooadd y editar notificaciones, consulte este artículo sobre la personalización de notificaciones, [personalizar las notificaciones emitidas en el token SAML de Hola para las aplicaciones previamente integradas en Azure Active Directory](develop/active-directory-saml-claims-customization.md). Para los usuarios de colaboración B2B, por motivos de seguridad, se evita realizar la asignación de NameID y UPD entre inquilinos.


## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propiedades de usuario de la colaboración B2B](active-directory-b2b-user-properties.md)
* [Agregar un rol de tooa de usuario de la colaboración B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegación de las invitaciones de colaboración B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinámicos y colaboración B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboración B2B y ejemplos de PowerShell](active-directory-b2b-code-samples.md)
* [Configuración de aplicaciones de SaaS para la colaboración B2B](active-directory-b2b-configure-saas-apps.md)
* [Uso compartido externo de Office 365](active-directory-b2b-o365-external-user.md)
* [Tokens de usuario de colaboración B2B](active-directory-b2b-user-token.md)
* [Limitaciones actuales de la colaboración B2B](active-directory-b2b-current-limitations.md)
