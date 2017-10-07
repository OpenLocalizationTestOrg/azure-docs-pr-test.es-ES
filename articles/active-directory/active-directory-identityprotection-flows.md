---
title: experiencias de aaaSign con Azure AD Identity Protection | Documentos de Microsoft
description: "Proporciona una visión general de la experiencia del usuario de hello cuando tiene mitiga o corregido un usuario o cuando se requiere la autenticación multifactor por una directiva de protección de identidad."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>Experiencias de inicio de sesión con Azure AD Identity Protection
Con Azure Active Directory Identity Protection, puede:

* requerir a los usuarios tooregister para la autenticación multifactor
* controlar inicios de sesión conflictivos y usuarios en peligro.

respuesta de Hola de problemas de toothese de sistema de Hola tiene un impacto en la experiencia de inicio de sesión del usuario porque solo directamente firma-en proporcionando un nombre de usuario y una contraseña no será posible ya. Pasos adicionales son tooget requiere que un usuario nuevo sin ningún riesgo en business.

En este tema se ofrece información general sobre la experiencia de inicio de sesión de usuario para todos los casos posibles.

**Multi-Factor Authentication**

* Registro de la autenticación multifactor

**Inicio de sesión en peligro**

* Recuperación de inicios de sesión peligrosos
* Inicios de sesión peligrosos bloqueados
* Registro de la autenticación multifactor durante un inicio de sesión peligroso

**Usuario en peligro**

* Recuperación de cuentas en peligro
* Cuenta en peligro bloqueada

## <a name="multi-factor-authentication-registration"></a>Registro de la autenticación multifactor
Hola mejor experiencia de usuario para ambos, Hola flujo de recuperación de cuenta en peligro y Hola a riesgo flujo de inicio de sesión, es cuando el usuario Hola automática puede recuperar. Si los usuarios se registren para la autenticación multifactor, ya tiene un número de teléfono asociado con su cuenta que puede ser utilizados toopass desafíos de seguridad. Ninguna participación del departamento de soporte o el Administrador de ayuda es necesario toorecover contra los riesgos de cuenta. Por lo tanto, recomienda en absoluto tooget los usuarios registrados para la autenticación multifactor. 

Los administradores pueden:

* establecer una directiva que requiere tooset a los usuarios configurar sus cuentas para la comprobación de seguridad adicional. 
* dejar de omitir el registro de la autenticación multifactor para los días de too30, en caso de desean que los usuarios de toogive un período de gracia antes de registrar.

**registro de la autenticación multifactor de Hello consta de tres pasos:**

1. En el primer paso de hello, usuario de hello recibe una notificación acerca de la cuenta de hello requisito tooset Hola hacia arriba para la autenticación multifactor. 
   
    ![Corrección](./media/active-directory-identityprotection-flows/140.png "Corrección")
2. tooset la autenticación multifactor seguridad, necesita toolet Hola sistema sepa cómo desea toobe conectado.
   
    ![Corrección](./media/active-directory-identityprotection-flows/141.png "Corrección")
3. sistema de Hello envía un desafío tooyou y deberá toorespond.
   
    ![Corrección](./media/active-directory-identityprotection-flows/142.png "Corrección")

## <a name="risky-sign-in-recovery"></a>Recuperación de inicios de sesión peligrosos
Cuando un administrador ha configurado una directiva para los riesgos de inicio de sesión, se notificación a los usuarios de hello afectado cuando lo intentan toosign en. 

**el flujo de inicio de sesión riesgo de Hello consta de dos pasos:** 

1. usuario de Hola se informa de que se ha detectado la algo inusual sobre su inicio de sesión, como inicio de sesión desde una nueva ubicación, dispositivo o aplicación. 
   
    ![Corrección](./media/active-directory-identityprotection-flows/120.png "Corrección")
2. usuario de Hello es necesario tooprove su identidad para resolver un desafío de seguridad. Si el usuario Hola está registrado para la autenticación multifactor necesitan tooround-un número de teléfono de tootheir de código de seguridad de ida y vuelta. Puesto que se trata de un solo un inicio de sesión arriesgado y no una cuenta en peligro, usuario de hello no tiene contraseña de hello toochange en este flujo. 
   
    ![Corrección](./media/active-directory-identityprotection-flows/121.png "Corrección")

## <a name="risky-sign-in-blocked"></a>Inicios de sesión peligrosos bloqueados
Los administradores también pueden elegir tooset a los usuarios tooblock de directiva de riesgo de inicio de sesión tras el inicio de sesión en función de nivel de riesgo de Hola. tooget desbloqueado, los usuarios finales deben ponerse en contacto con un administrador o el departamento de soporte técnico, o puede intentar iniciar sesión desde una ubicación conocida o dispositivo. La recuperación automática al resolver la autenticación multifactor no es una opción en este caso.

![Corrección](./media/active-directory-identityprotection-flows/200.png "Corrección")

## <a name="compromised-account-recovery"></a>Recuperación de cuentas en peligro
Cuando se ha configurado una directiva de seguridad de riesgo de usuario, los usuarios que cumplen usuario Hola el riesgo de nivel especificado en la directiva de hello (y, por tanto, se da por supuesto en peligro) debe pasar por el flujo de recuperación de compromiso de hello usuario antes de que puede iniciar sesión. 

**flujo de recuperación de compromiso de Hello usuario consta de tres pasos:**

1. se informa al usuario de Hola que su seguridad de la cuenta está en peligro debido a actividad sospechosa o filtren las credenciales.
   
    ![Corrección](./media/active-directory-identityprotection-flows/101.png "Corrección")
2. usuario de Hello es necesario tooprove su identidad para resolver un desafío de seguridad. Si el usuario Hola está registrado para la autenticación multifactor puede recuperar automáticamente se vean comprometidos. Necesitará tooround-un número de teléfono de tootheir de código de seguridad de ida y vuelta. 
   
   ![Corrección](./media/active-directory-identityprotection-flows/110.png "Corrección")
3. Por último, Hola usuario es toochange forzada en su contraseña, ya que otra persona que haya tenido acceso tootheir cuenta. 
   A continuación se muestran capturas de pantalla de esta experiencia.
   
   ![Corrección](./media/active-directory-identityprotection-flows/111.png "Corrección")

## <a name="compromised-account-blocked"></a>Cuenta en peligro bloqueada
tooget un usuario que se ha bloqueado por una directiva de seguridad de usuario riesgo desbloqueada, usuario Hola debe ponerse en contacto con un administrador o servicio de asistencia. La recuperación automática al resolver la autenticación multifactor no es una opción en este caso.

![Corrección](./media/active-directory-identityprotection-flows/104.png "Corrección")

## <a name="reset-password"></a>Restablecer contraseña
Si se bloquea el inicio de sesión de los usuarios en peligro, un administrador puede generar una contraseña temporal para ellos, los usuarios de Hello tendrán toochange su contraseña durante un inicio de sesión siguiente.

![Corrección](./media/active-directory-identityprotection-flows/160.png "Corrección")

## <a name="see-also"></a>Consulte también
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md) 

