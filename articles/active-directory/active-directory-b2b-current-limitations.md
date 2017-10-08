---
title: "aaaLimitations de colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "Limitaciones actuales de la colaboración B2B de Azure Active Directory"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a>Limitaciones de colaboración B2B de Azure AD
Colaboración B2B de Active Directory (Azure AD) de Azure está actualmente limitaciones de toohello asunto descritas en este artículo.

## <a name="possible-double-multi-factor-authentication"></a>Posibilidad de doble autenticación multifactor
Con Azure AD B2B, se puede aplicar la autenticación multifactor en la organización de recursos de hello (Hola invitar a la organización). motivos de Hola de este enfoque se detallan en [acceso condicional para los usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md). Si un socio ya tiene la autenticación multifactor configurar y aplicar, sus usuarios podrían tener la autenticación de hello tooperform una vez en su organización principal y, a continuación, nuevo en suyo.

## <a name="instant-on"></a>Activación instantánea
En los flujos de colaboración de hello B2B, se agregue usuarios toohello directorio y actualizarlos dinámicamente durante el canje de invitación, asignación de aplicación y así sucesivamente. actualizaciones de Hola y escrituras normalmente se producen en la instancia de un directorio y se deben replicar a través de todas las instancias. La replicación se completa una vez que se actualicen todas las instancias. A veces cuando es escribir o actualizar en una instancia de objeto de Hola y Hola llamar tooretrieve este objeto es instancia tooanother, pueden producirse las latencias de replicación. Si esto sucede, actualice o vuelva a intentar toohelp. Si está escribiendo una aplicación con nuestra API, a continuación, reintentos con un retroceso es un tooalleviate estable, buena práctica este problema.

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
* [Uso compartido externo de Office 365](active-directory-b2b-o365-external-user.md)
