---
title: "aaaHow toorequire la autenticación multifactor | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorequire la autenticación multifactor (MFA) para había privilegiado identidades con extensión de Azure Active Directory Privileged Identity Management de Hola."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>Cómo toorequire MFA en Azure AD Privileged Identity Management
Se recomienda exigir Multi-Factor Authentication (MFA) para todos los administradores. Esto reduce el riesgo de Hola de un ataque debido contraseña tooa puesto en peligro.

Puede exigir que los usuarios completen un desafío de MFA cuando inician sesión. entrada de blog de Hola [MFA para Office 365 y autenticación Multifactor para Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) compara qué se incluye en Office y suscripciones de Azure, con características de hello incluidos en la oferta de Microsoft Azure la autenticación multifactor de Hola.

También puede exigir que los usuarios realicen un desafío de MFA cuando activan un rol en PIM de Azure AD. De esta manera, si el usuario de hello no completó un desafío MFA cuando inicia sesión, estarán toodo solicitada es así por PIM.

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>Exigencia de MFA en Privileged Identity Management de Azure AD
Al administrar identidades en PIM como administrador de roles con privilegios, puede ver las alertas que recomienda MFA para las cuentas con privilegios. Haga clic en seguridad de hello alerta en el panel de PIM de hello y una nueva hoja se abrirá con una lista de las cuentas de administrador de Hola que necesita MFA.  Puede requerir MFA seleccionando varios roles y, a continuación, haga clic en hello **corregir** botón, o haga clic en siguiente tooindividual funciones de puntos suspensivos de hello y, a continuación, haga clic en hello **corregir** botón.

> [!IMPORTANT]
> En este momento, Azure MFA solo funciona con el trabajo o escolares, no las cuentas de Microsoft (normalmente una cuenta personal que ha utilizado toosign en servicios de tooMicrosoft como Skype, Xbox, Outlook.com, etcetera.). Por este motivo, cualquier persona que utilice una cuenta de Microsoft no puede ser un administrador elegible porque no pueden usar MFA tooactivate sus roles. Si estos usuarios necesitan toocontinue administrar cargas de trabajo con una cuenta Microsoft, elevar ellos toopermanent administradores por ahora.
> 
> 

Además, puede cambiar el requisito de MFA de Hola para un rol específico haciendo clic en él en la sección Roles de panel PIM Hola Hola. A continuación, haga clic en **configuración** en la hoja de rol de hello y, a continuación, seleccione **habilitar** bajo la autenticación multifactor.

## <a name="how-azure-ad-pim-validates-mfa"></a>Cómo PIM de Azure AD valida MFA
Hay dos opciones para validar MFA cuando un usuario activa un rol.

opción más sencilla de Hello es toorely en Azure MFA para los usuarios que se va a activar un rol con privilegios. toodo, primera comprobación de que los usuarios cuentan con licencia, si es necesario y se han registrado en Azure MFA. Obtener más información sobre cómo toodo trata de un [Introducción a la autenticación multifactor Azure en la nube de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md). Se recomienda, pero no es necesario, configure tooenforce de Azure AD MFA para estos usuarios cuando inician sesión en. Esto es porque se realizarán comprobaciones MFA de Hola por PIM AD de Azure propia.

Si los usuarios se autentican en el entorno local, también puede hacer que el proveedor de identidades se encargue de MFA. Por ejemplo, si ha configurado la autenticación de basado en tarjeta inteligente toorequire de servicios de federación de AD antes de acceder a Azure AD, [recursos de nube de protección con autenticación multifactor de Azure y AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) incluye instrucciones Para configurar AD FS toosend notificaciones tooAzure AD. Cuando un usuario intenta tooactivate un rol, PIM de Azure AD aceptará que MFA ya se ha validado para el usuario de hello después de recibir notificaciones adecuadas de Hola.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

