---
title: "aaaDelegate invitaciones para la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "Las propiedades de un usuario de colaboración B2B de Azure Active Directory son configurables."
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
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Delegación de invitaciones de la colaboración B2B de Azure Active Directory

Con la colaboración de negocio a negocio (B2B) de Azure Active Directory (Azure AD), no es necesario toobe un invitaciones de toosend administrador global. En su lugar, puede usar las directivas y delegar toousers invitaciones cuyas funciones permitan toosend invitaciones. Un importante nueva manera toodelegate invitado usuario invitaciones es a través de rol de autor de la invitación invitado Hola.

## <a name="guest-inviter-role"></a>Rol de invitador de personas
Podemos asignar Hola usuario tooGuest invitaciones de toosend de rol de autor de la invitación. No tiene miembros toobe de invitaciones de toosend de rol de administrador global de Hola. De forma predeterminada, los usuarios regulares también pueden invocar API de invitación de Hola a menos que un administrador global deshabilitado invitaciones para que los usuarios normales. Un usuario también puede invocar la API de hello usando Hola portal de Azure o PowerShell.

Este es un ejemplo que muestra cómo toouse PowerShell tooadd un rol de usuario toohello Invitador invitado:

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>Controlar quién puede invitar

![Control cómo tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Con la colaboración B2B de Azure AD, un administrador de inquilinos puede establecer las siguientes directivas de invitación de hello:

- Desactivar invitaciones
- Pueden invitar solo los administradores y usuarios en función de invitado Invitador Hola
- Pueden invitar administradores, rol de autor de la invitación invitado hello y miembros
- Todos los usuarios, incluidos los invitados, pueden invitar

De forma predeterminada, los inquilinos se establecen demasiado n.º 4. (Todos los usuarios, incluidos los invitados, pueden invitar a usuarios B2B).

## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propiedades de usuario de la colaboración B2B](active-directory-b2b-user-properties.md)
* [Agregar un rol de tooa de usuario de la colaboración B2B](active-directory-b2b-add-guest-to-role.md)
* [Grupos dinámicos y colaboración B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboración B2B y ejemplos de PowerShell](active-directory-b2b-code-samples.md)
* [Configuración de aplicaciones de SaaS para la colaboración B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuario de colaboración B2B](active-directory-b2b-user-token.md)
* [Asignación de notificaciones de usuario de colaboración B2B](active-directory-b2b-claims-mapping.md)
* [Uso compartido externo de Office 365](active-directory-b2b-o365-external-user.md)
* [Limitaciones actuales de la colaboración B2B](active-directory-b2b-current-limitations.md)
