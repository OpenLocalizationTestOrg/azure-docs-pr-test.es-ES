---
title: "aaaOffice 365 uso compartido externo y la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a>Uso compartido externo de Office 365 y colaboración B2B de Azure Active Directory

Externo de uso compartido de Office 365 (OneDrive, SharePoint Online, grupos unificados, etc.) y B2B de Azure Active Directory (Azure AD) colaboración son técnicamente Hola mismo lo. Todas las externas compartir (excepto OneDrive y SharePoint Online), incluidos los invitados en grupos de Office 365, ya usa invitación de colaboración B2B de Azure AD hello las API para el uso compartido.

OneDrive y SharePoint Online tiene un administrador de invitaciones independiente. La compatibilidad con el uso compartido externo en OneDrive o SharePoint Online comenzó antes que Azure AD desarrollara su compatibilidad. Con el tiempo, compartir externo OneDrive y SharePoint Online ha acumulado varias características y muchos millones de usuarios que usan productos de hello en-integrada patrón de uso compartido. Sin embargo, existen algunas diferencias sutiles entre cómo funciona el uso compartido externo de OneDrive y SharePoint Online y la colaboración B2B de Azure AD:

- OneDrive y SharePoint Online agrega directorio toohello de los usuarios después de que los usuarios han canjear sus invitaciones. Por lo tanto, antes de canje, no ve el usuario de hello en el portal de Azure AD. Si otro sitio invita a un usuario en hello mientras tanto, se genera una nueva invitación. Sin embargo, cuando se usa la colaboración B2B de Azure AD, los usuarios se agregan inmediatamente cuando se les invita por lo que se muestran en todas partes.

- Hola canje experiencia en OneDrive o SharePoint Online tiene un aspecto diferente de la experiencia de hello en colaboración B2B de Azure AD. Después de que un usuario los canjea una invitación, experiencias de hello son similares.

- Los usuarios invitados a la colaboración B2B de Azure AD se pueden seleccionar en los cuadros de diálogo de uso compartido de OneDrive y SharePoint Online. Los usuarios invitados a OneDrive y SharePoint Online también se muestran en Azure AD después de que canjean sus invitaciones.

- toomanage externo compartida en OneDrive o SharePoint Online con la colaboración B2B de Azure AD, establezca hello OneDrive y SharePoint Online externo compartir configuración demasiado**sólo Permitir uso compartido con usuarios externos ya en el directorio de hello**. Los usuarios pueden ir tooexternally compartido sitios y selección de colaboradores externos que Hola administrador ha agregado. Hola, administrador puede agregar colaboradores externos de Hola a través de hello invitación de colaboración B2B API.

![Hola OneDrive y SharePoint Online configuración del uso compartido externo](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propiedades de usuario de la colaboración B2B](active-directory-b2b-user-properties.md)
* [Agregar un rol de tooa de usuario de la colaboración B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegación de las invitaciones de colaboración B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinámicos y colaboración B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboración B2B y ejemplos de PowerShell](active-directory-b2b-code-samples.md)
* [Configuración de aplicaciones de SaaS para la colaboración B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuario de colaboración B2B](active-directory-b2b-user-token.md)
* [Asignación de notificaciones de usuario de colaboración B2B](active-directory-b2b-claims-mapping.md)
* [Limitaciones actuales de la colaboración B2B](active-directory-b2b-current-limitations.md)
