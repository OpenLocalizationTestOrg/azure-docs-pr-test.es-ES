---
title: "Guía de administrador de licencias de colaboración de aaaAzure B2B de Active Directory | Documentos de Microsoft"
description: "La colaboración B2B de Azure Active Directory no necesita licencias de Azure AD de pago, pero también puede obtener características de pago para los usuarios invitados de B2B"
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
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: 8e15d66209b090bff210674ecdacc88cd642dcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a>Guía de concesión de licencias de colaboración B2B de Azure Active Directory

Puede usar usuarios invitados de Azure AD B2B colaboración capacidades tooinvite en su tooallow del inquilino de Azure AD les tooaccess servicios de Azure AD y otros recursos de su organización. Si desea características de tooprovide acceso toopaid Azure AD, B2B deben tener una licencia de usuarios invitados de colaboración con las licencias de Azure AD correspondientes. 

Concretamente:
* Las funcionalidades de Azure AD Free están disponibles para usuarios invitados sin licencias adicionales.
* Si desea que los usuarios tooB2B de características de Azure AD de toopaid de tooprovide acceso, debe tener suficiente toosupport licencias esos usuarios invitados de B2B.
* Un inquilino invitar a con una licencia de pago de Azure AD tiene B2B colaboración uso rights tooan adicionales cinco B2B invitados usuarios invitados toohello inquilinos.
* cliente de Hello propietario Hola invitar a inquilino debe ser Hola uno toodetermine cuántos usuarios de colaboración B2B necesitan capacidades de Azure AD de pago. Función hello Azure AD de pago características que desea para los usuarios de invitado, debe tener suficiente Azure AD de pago licencias a los usuarios de colaboración de toocover B2B Hola misma relación de 5:1.

Un usuario invitado de colaboración B2B se agrega como usuario de una compañía de un partner, no como empleado de la organización o como empleado de otra empresa del conglomerado. Un usuario invitado de B2B puede iniciar sesión con credenciales externas o credenciales pertenecientes a la organización, como se describe en este artículo. 

En otras palabras, licencias de B2B se establece no por cómo se autentica el usuario de hello sino por relación de Hola de organización de hello usuario tooyour. Si estos usuarios no son partners, reciben un tratamiento diferente en términos de licencia. No se consideran toobe un usuario de la colaboración B2B con fines de licencia incluso si su UserType está marcada como "Invitado". Deben tener licencia de la forma habitual, en una licencia por usuario. Entre estos usuarios se incluyen:
* Sus empleados
* Personal que inicia sesión con identidades externas
* Un empleado de otra empresa del conglomerado


## <a name="licensing-examples"></a>Ejemplos de concesión de licencias
- Un cliente desea tooinvite 100 B2B colaboración a los usuarios tooits inquilino de Azure AD. cliente de Hello asigna administración de acceso y el aprovisionamiento para todos los usuarios, pero 50 usuarios también requieren MFA y el acceso condicional. Este cliente debe adquirir licencias de Azure AD Basic 10 y 10 toocover de licencias de Azure AD Premium P1 estos usuarios B2B correctamente. Si cliente hello planes de características de protección de la identidad de toouse con usuarios de B2B, deben tener los usuarios de Azure AD Premium P2 licencias toocover Hola invitó Hola misma relación de 5:1.
- Un cliente tiene 10 empleados y todos ellos tienen licencias actualmente en el nivel Premium P1 de Azure AD. Ahora que desean tooinvite 60 B2B a los usuarios que requieren la autenticación multifactor (MFA). Con la regla de licencias de 5:1 Hola, cliente hello debe tener al menos 12 toocover de licencias de Azure AD Premium P1 todos los usuarios de la colaboración B2B 60. Dado que ya tienen 10 Premium P1 licencias para sus 10 empleados, tienen derechos tooinvite 50 B2B a los usuarios con las características Premium P1 como MFA. En este ejemplo, a continuación, deben adquirir 2 Premium P1 licencias adicionales toocover Hola 10 B2B colaboración usuarios restantes.

> [!NOTE]
> No hay ninguna manera aún tooassign licencias directamente toohello B2B usuarios tooenable estos derechos de usuario de la colaboración B2B.

cliente de Hello propietario Hola invitar a inquilino debe ser Hola uno toodetermine cuántos usuarios de colaboración B2B necesitan capacidades de Azure AD de pago. Función que paga características de Azure AD que desee para los usuarios de invitado, debe tener pago usuarios de colaboración B2B de licencias toocover en proporción de 5:1 de Hola de suficientemente Azure AD. 

## <a name="additional-licensing-details"></a>Detalles de licencias adicionales
- No hay cuentas de usuario de tooactually asignar licencias tooB2B. En función de la relación de 5:1 de Hola, Administrador de licencias se automáticamente calcula y notifica.
- Si pago licencia de Azure AD no existe ninguna en el inquilino de hello, derechos de obtiene Hola cada usuarios invitados que hello Azure AD Free ofertas de edición.
- Si un usuario de colaboración ya tiene un pago Azure AD de B2B de licencia de su organización, aunque no consuman una de las licencias de colaboración de hello B2B del inquilino invitar a Hola.

## <a name="advanced-discussion-what-are-hello-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a>Advanced discusión: ¿Cuáles son las consideraciones de licencia de hello cuando se agrega a los usuarios de una organización conglomerada como "miembros" usando las API?
Un usuario de invitado B2B es aquel que recibe una invitación de un toowork de organización de asociado con la organización del host de Hola. Por lo general, cualquier otro caso no se considerará apto para B2B aunque use características de B2B. Echemos un vistazo a estos dos casos en particular:

1. Si un host invita a un empleado que usa una dirección de consumidor
  * Este escenario no es compatible con nuestras directivas de licencias y no se recomienda.

2. Si una organización host agrega un usuario de otra organización conglomerado
  1. En este caso, Hola usuario recibe una invitación mediante las API de B2B, pero en este caso no es tradicionalmente B2B. Lo ideal es que, si tenemos estas organizaciones invitación Hola a otros usuarios de organizaciones como miembros (nuestra API permite que). En este caso, licencias tienen toobe asignado a miembros toothese para ellos recursos tooaccess Hola invitar a la organización.

  2. Algunas organizaciones podrían desear hello tooadd toobe de los usuarios de otra organización agrega como "Invitado" como una directiva. Estos son dos casos:
      * Hello conglomerado organización ya usa Azure AD y los usuarios de hello invitado se licencia Hola otra organización: en este caso, no esperamos Hola de usuarios invitados tooneed toofollow dispuesto de fórmula 1 / 5 anteriormente en este documento. 

      * no se está usando Azure AD Hello conglomerado organización o no tiene licencias adecuados: en este caso, siga Hola dispuesto de fórmula 1 / 5 anteriormente en este documento.

## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](active-directory-b2b-admin-add-users.md)
* [¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saludo de correo electrónico de invitación de colaboración B2B de hello](active-directory-b2b-invitation-email.md)
* [Canje de invitación de colaboración B2B](active-directory-b2b-redemption-experience.md)
* [Solución de problemas de colaboración B2B de Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)](active-directory-b2b-faq.md)
* [Personalización y API de colaboración B2B de Azure Active Directory](active-directory-b2b-api.md)
* [Autenticación multifactor para usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md)
* [Incorporación de usuarios de colaboración B2B sin invitación](active-directory-b2b-add-user-without-invite.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
