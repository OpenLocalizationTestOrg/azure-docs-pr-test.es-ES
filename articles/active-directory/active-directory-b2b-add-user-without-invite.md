---
title: "aaaAdd B2B colaboración a los usuarios tooAzure Active Directory sin una invitación | Documentos de Microsoft"
description: "Puede permitir que un usuario invitado agregar otro tooyour de los usuarios invitados Azure AD sin canjear una invitación en colaboración B2B de Azure Active Directory."
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a>Incorporación de usuarios de colaboración B2B sin invitación

Puede permitir que a un usuario, como un socio comercial representativo, tooadd los usuarios de hello asociado tooyour organización sin necesidad de toobe invitaciones canjeado. Todo lo que debe hacer es conceder ese usuario privilegios de enumeración en directorio de Hola que está usando para org de hello asociado. 

Conceda estos privilegios cuando se den estas condiciones:

1. Un usuario de hello host organización (por ejemplo, WoodGrove) invita a un usuario de la organización del asociado de hello (por ejemplo, Sam@litware.com) como invitado.
2. Hola, Administrador de organización de host de hello configura directivas que permiten Sam tooidentify y agregar otros usuarios de la organización del asociado de hello (Litware).
3. Sam ahora puede agregar otros usuarios del directorio de Litware toohello WoodGrove, grupos o las aplicaciones sin necesidad de toobe invitaciones canjeado. Si Sam tiene privilegios de la enumeración adecuada de hello en Litware, se produce automáticamente.

### <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](active-directory-b2b-admin-add-users.md)
* [¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saludo de correo electrónico de invitación de colaboración B2B de hello](active-directory-b2b-invitation-email.md)
* [Canje de invitación de colaboración B2B](active-directory-b2b-redemption-experience.md)
* [Concesión de licencias de colaboración B2B de Azure AD](active-directory-b2b-licensing.md)
* [Solución de problemas de colaboración B2B de Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)](active-directory-b2b-faq.md)
* [Personalización y API de colaboración B2B de Azure Active Directory](active-directory-b2b-api.md)
* [Autenticación multifactor para usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)