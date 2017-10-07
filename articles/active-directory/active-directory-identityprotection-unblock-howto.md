---
title: "aaaAzure Active Directory Identity Protection - cómo los usuarios de toounblock | Documentos de Microsoft"
description: Aprenda a desbloquear usuarios bloqueados por una directiva de Azure Active Directory Identity Protection.
services: active-directory
keywords: 'azure active directory identity protection: desbloquear usuario'
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Azure Active Directory Identity Protection - cómo los usuarios de toounblock
Con Azure Active Directory Identity Protection, puede configurar directivas tooblock usuarios Hola configurando condiciones se cumplen. Por lo general, un usuario bloqueado contactos help desk toobecome desbloqueado. Estos temas se explican los pasos de hello puede realizar toounblock un usuario bloqueado.

## <a name="determine-hello-reason-for-blocking"></a>Determinar el motivo de Hola para bloquear
Como un primer paso toounblock un usuario, necesita toodetermine Hola tipo de directiva que ha bloqueado el usuario Hola porque son según los pasos siguientes.
Con Azure Active Directory Identity Protection, se puede bloquear a un usuario con una directiva de riesgo de inicio de sesión o con una directiva de riesgo de usuario.

Se puede obtener el tipo de saludo de directiva que ha bloqueado un usuario de encabezado de hello en cuadro de diálogo de Hola que presentó toohello usuario durante un intento de inicio de sesión:

| Directiva | Cuadro de diálogo usuario |
| --- | --- |
| Riesgo de inicio de sesión |![Inicio de sesión bloqueado](./media/active-directory-identityprotection-unblock-howto/02.png) |
| Riesgo de usuario |![Cuenta bloqueada](./media/active-directory-identityprotection-unblock-howto/104.png) |

Un usuario que está bloqueado por:

* Una directiva de riesgo de inicio de sesión también es conocida como inicio de sesión sospechoso
* Una directiva de riesgo de usuario también es conocida como una cuenta en riesgo

## <a name="unblocking-suspicious-sign-ins"></a>Desbloqueo de inicios de sesión sospechosos
toounblock un inicio de sesión de sospechosa, deberá Hola siguientes opciones:

1. **Iniciar sesión desde una ubicación o dispositivo conocidos**: una razón común para el bloqueo de inicios de sesión sospechosos es que se intente iniciar sesión desde ubicaciones o dispositivos desconocidos. Los usuarios pueden determinar rápidamente si se trata de hello bloqueo motivo realizando en toosign desde una ubicación conocida o dispositivo.
2. **Excluir de la directiva** : si piensa que de la directiva de inicio de sesión en la configuración actual de hello está causando problemas para usuarios específicos, puede excluir usuarios Hola de él. Para más información, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
3. **Deshabilitar directiva** : si piensa que la configuración de directiva está causando problemas para todos los usuarios, puede deshabilitar la directiva de Hola. Para más información, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

## <a name="unblocking-accounts-at-risk"></a>Desbloqueo de cuentas en riesgo
toounblock una cuenta en peligro, deberá Hola siguientes opciones:

1. **Restablecimiento de contraseñas** -puede restablecer la contraseña del usuario de Hola. Para más información, consulte [Restablecimiento manual de una contraseña segura](active-directory-identityprotection.md#manual-secure-password-reset) .
2. **Descartar todos los eventos de riesgo** -directiva de riesgo de hello usuario impide que un usuario si se ha alcanzado el nivel de riesgo de usuario de hello configurado para bloquear el acceso. Para reducir el nivel de riesgo de un usuario, cierre manualmente los eventos de riesgo notificados. Para más información, consulte [Cierre manual de eventos de riesgo](active-directory-identityprotection.md#closing-risk-events-manually).
3. **Excluir de la directiva** : si piensa que de la directiva de inicio de sesión en la configuración actual de hello está causando problemas para usuarios específicos, puede excluir usuarios Hola de él. Para más información, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
4. **Deshabilitar directiva** : si piensa que la configuración de directiva está causando problemas para todos los usuarios, puede deshabilitar la directiva de Hola. Para más información, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

## <a name="next-steps"></a>Pasos siguientes
 ¿Desea más información acerca de Azure AD Identity Protection tooknow? Consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
