---
title: "petición de consentimiento de aaaUnexpected al iniciar sesión en la aplicación tooan | Documentos de Microsoft"
description: "¿Cómo tootroubleshoot cuando un usuario ve una solicitud de consentimiento para una aplicación ha integrado con Azure AD que no esperaba"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Petición de consentimiento inesperado al iniciar sesión en la aplicación de tooan

Muchas aplicaciones que se integran con Azure Active Directory requieren recursos de toovarious de permisos en orden toorun. Cuando estos recursos también están integrados con Azure Active Directory, tooaccess permisos ellos se solicita mediante hello Azure AD consentimiento framework. 

Esto produce una solicitud de consentimiento que se está mostrando Hola primera vez que se usa una aplicación, que suele ser una operación única. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Escenarios en los que los usuarios ven solicitudes de consentimiento

Se pueden esperar más solicitudes en distintos escenarios:

* conjunto de Hola de permisos requeridos por la aplicación hello ha cambiado.

* usuario de Hola que originalmente dado su consentimiento toohello aplicación no era administrador, y ahora un usuario diferente (no administrativos) utiliza aplicación hello para hello primera vez.

* usuario de Hola que originalmente dado su consentimiento toohello aplicación era administrador, pero no dar el consentimiento en nombre de toda la organización Hola.

* está usando la aplicación Hello [consentimiento incremental y dinámico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest de permisos adicionales después de haberse otorgado inicialmente consentimiento. Esto se suele usar cuando las características opcionales de una aplicación adicional requieren permisos más allá de los que se requieren para la funcionalidad de línea base.

* Se ha revocado el consentimiento después de que inicialmente se otorgó.

* desarrollador de Hello configuró Hola aplicación toorequire una solicitud de consentimiento cada vez que se utiliza (Nota: esto no es recomendable).

## <a name="next-steps"></a>Pasos siguientes

-   [Aplicaciones, permisos y consentimiento en Azure Active Directory (punto de conexión v1.0)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Ámbitos, permisos y consentimiento de hello Azure Active Directory (extremo v2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


