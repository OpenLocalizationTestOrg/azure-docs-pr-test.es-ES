---
title: "aaaUpgrade de sincronización de directorios y la sincronización de AD de Azure | Documentos de Microsoft"
description: "Describe cómo tooupgrade de tooAzure de sincronización de directorios y la sincronización de AD de Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Actualización de la sincronización de Microsoft Azure Active Directory ("DirSync") y la sincronización de Azure Active Directory ("Azure AD Sync")
Azure AD Connect se Hola tooconnect de mejor manera su directorio local con Azure AD y Office 365. Se trata de un tooAzure de tooupgrade mucho tiempo AD Connect de Windows Azure Active Directory Sync (DirSync) o sincronización de Azure AD como estas herramientas están ahora en desuso y alcanzará el final del soporte técnico de 13 de abril de 2017.

Hola dos identidades herramientas de sincronización que están en desuso se proporcionaban para clientes de bosque único (DirSync) y varios bosques y otros clientes avanzados (sincronización de Azure AD). Estas herramientas anteriores se han reemplazado por una única solución disponible para todos los escenarios: Azure AD Connect. Ofrece nuevas funcionalidades, mejoras en las características y soporte técnico para nuevos escenarios. toobe toocontinue pueda toosynchronize la tooAzure de datos de identidad local AD y Office 365, recomendamos encarecidamente que actualice tooAzure AD Connect.

última versión de Hola de DirSync se publicó en julio de 2014 y la última versión de Hola de Azure AD Sync se publicó en mayo de 2015.

## <a name="what-is-azure-ad-connect"></a>Qué es Azure AD Connect
Azure AD Connect es Hola sucesor tooDirSync y sincronización de Azure AD. Combina todos los escenarios que admitían estas dos herramientas. Obtenga más información en [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>Programación de degradación
| Date | Comentario |
| --- | --- |
| 13 de abril de 2016 |Se anuncia que la sincronización de Microsoft Azure Active Directory (“DirSync”) y la sincronización de Microsoft Azure Active Directory (“Azure AD Sync”) están en desuso. |
| 13 de abril de 2017 |Finaliza el soporte técnico. Los clientes ya no será capaz de tooopen un caso de soporte sin actualizar tooAzure AD conectarse primero. |
|31 de diciembre de 2017|Azure AD dejará de aceptar comunicaciones procedentes de la sincronización de Windows Azure Active Directory ("DirSync") y de la sincronización de Microsoft Azure Active Directory ("Azure AD Sync").

## <a name="how-tootransition-tooazure-ad-connect"></a>Cómo tootransition tooAzure AD Connect
Si usa DirSync, hay dos formas de actualizar: mediante una actualización local y mediante una implementación paralela. Recomendamos la actualización local a la mayoría de los clientes, en caso de que tengan un sistema operativo reciente y menos de 50 000 objetos. En otros casos, se recomienda toodo una implementación paralela donde la configuración de sincronización de directorios es mover tooa nuevo servidor que ejecuta Azure AD Connect.

Si usa Azure AD Sync, se recomienda una actualización local. Si desea, es posible tooinstall un nuevo servidor de Azure AD Connect en paralelo y realizar una migración de recorrido de la tooAzure de servidor de sincronización de AD de Azure AD Connect.

| Solución | Escenario |
| --- | --- |
| [Actualización desde DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Si tiene un servidor de DirSync existente que ya se está ejecutando.</li> |
| [Actualización desde Sincronización de Azure AD](active-directory-aadconnect-upgrade-previous-version.md) |<li>Si va a trasladarse desde Azure AD Sync.</li> |

Si desea toosee cómo toodo in situ actualizar desde DirSync tooAzure AD Connect, a continuación, vea este vídeo de Channel 9:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>P+F
**He recibido una notificación de correo electrónico de Hola, equipo de Azure o un mensaje desde el centro de mensajes de Hola Office 365, pero estoy usando conectar.**  
También se envió a notificación de Hello toocustomers mediante Azure AD Connect con un número de compilación 1.0. \*.0 (con una versión anterior 1.1). Microsoft recomienda a los clientes libera toostay actual con Azure AD Connect. Hola [la actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md) característica se introdujo en 1.1 resulta fácil tooalways tiene una versión reciente de Azure AD Connect instalada.

**P: ¿Dejarán de funcionar DirSync o Azure AD Sync el 13 de abril de 2017?**  
DirSync/Azure AD Sync continuará toowork en 13 de abril de 2017.  Sin embargo, Azure AD ya no aceptará las comunicaciones procedentes de DirSync/Azure AD Sync el 31 de diciembre de 2017.

**P: ¿Desde qué versiones de DirSync se puede actualizar?**  
Es compatible tooupgrade desde cualquier versión de sincronización de directorios que se usan.

**P: ¿qué hay de hello conector de Azure AD para FIM o MIM?**  
Conector de Azure AD para FIM o MIM Hello tiene **no** sido anunció su eliminación. Se trata de una **inmovilización de características**; es decir, no se le agregan funcionalidades nuevas y no recibe correcciones de errores. Microsoft recomienda a los clientes que usan tooplan toomove de él tooAzure AD Connect. Es muy recomendado toonot inicio todas las implementaciones nuevas usarlo. Este conector se anunciará en desuso en hello futuras.

## <a name="additional-resources"></a>Recursos adicionales
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
