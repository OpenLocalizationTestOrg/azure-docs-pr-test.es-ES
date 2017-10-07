---
title: "acceso de aaaConditional para los usuarios de la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "Colaboración B2B de Active Directory de Azure es compatible con la autenticación multifactor (MFA) para las aplicaciones corporativas acceso selectivo tooyour"
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
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>Acceso condicional para usuarios de colaboración B2B

## <a name="multi-factor-authentication-for-b2b-users"></a>Multi-Factor Authentication para usuarios B2B
Con la colaboración B2B de Azure AD, las organizaciones pueden exigir directivas de autenticación multifactor (MFA) para usuarios de B2B. Estas directivas se pueden aplicar en el nivel de usuario individual, aplicación o inquilino Hola Hola igual que están habilitados para los empleados a jornada completa y los miembros de la organización de Hola. Se aplican las directivas MFA en la organización de recursos de Hola.

Ejemplo:
1. Trabajo de administrador o información de la compañía A invita a usuario de la aplicación de la compañía B tooan *Foo* de compañía A.
2. Aplicación *Foo* de compañía A es toorequire configurado MFA en el acceso.
3. Cuando el usuario de saludo de la compañía B intente tooaccess aplicación *Foo* en un inquilino de empresa de hello, son más frecuentes toocomplete un desafío MFA.
4. Hola usuario puede configurar su MFA con la compañía A y elige la opción de MFA.
5. Este escenario funciona con cualquier identidad (Azure AD o MSA, por ejemplo, si los usuarios de la empresa B se autentican con un identificador social).
6. La empresa A debe tener suficientes licencias de Azure AD Premium que admitan MFA. usuario de saludo de la compañía B utiliza esta licencia de compañía A.

arquitectura multiempresa invitar a Hello siempre es responsable de MFA para los usuarios de la organización del asociado de hello, incluso si la organización del asociado de hello tiene capacidades de MFA.

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>Configuración de Multi-Factor Authentication para los usuarios de colaboración B2B
toodiscover lo fácil que es tooset MFA de para los usuarios de la colaboración B2B, vea cómo en Hola después de vídeo:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>Experiencia de MFA de los usuarios B2B para el canje de ofertas
Extraer del repositorio Hola después de la experiencia de animación toosee Hola canje:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>Restablecimiento de la MFA para los usuarios de colaboración B2B
Actualmente, Hola, administrador puede requerir volver a tooproof de los usuarios de la colaboración B2B de únicamente mediante Hola siguientes cmdlets de PowerShell:

1. Conectar tooAzure AD

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. Obtenga todos los usuarios con los métodos de prueba.

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  Aquí tiene un ejemplo:

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. Restablecer el método MFA de hello para un usuario específico toorequire Hola B2B colaboración usuario tooset prueba métodos de nuevo. Ejemplo:

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>¿Por qué se realizar MFA en inquilinos de recursos de hello?

En la versión actual de hello, MFA siempre está en inquilinos de recursos de hello, por motivos de la predicción. Por ejemplo, supongamos que un usuario de Contoso (Sally) es tooFabrikam invitado y Fabrikam habilitó MFA para usuarios de B2B.

Si Contoso tiene una directiva MFA habilitada para App1 pero no App2, a continuación, si miramos Hola notificación Contoso MFA en el token de hello, tengamos que vemos Hola siguiente problema:

* Día 1: un usuario tiene MFA en Contoso y accede a App1; así que no se muestra ningún mensaje adicional de MFA en Fabrikam.

* Día 2: Hola usuario tiene acceso a 2 de la aplicación en Contoso, por lo que ahora al tener acceso a Fabrikam, deben registrarse para MFA no existe.

Este proceso puede resultar confuso y podría provocar toodrop en las finalizaciones de inicio de sesión.

Además, incluso si Contoso tiene capacidad MFA, no siempre es Hola Hola mayúsculas Fabrikam confiarán en hello directiva de MFA de Contoso.

Por último, el MFA del inquilino de recursos también funciona en las MSA y los identificadores sociales, así como en las organizaciones asociadas que no tengan una configuración de MFA.

Por lo tanto, la recomendación de Hola para MFA para los usuarios de B2B es tooalways requerir MFA Hola invitar a los inquilinos. Este requisito puede provocar toodouble MFA en algunos casos, pero cada vez que se obtiene acceso a los inquilinos invitar a hello, experiencia de los usuarios finales de hello es predecible: Sally debe registrar para MFA con inquilinos invitar a Hola.

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>Acceso condicional basado en el dispositivo, la ubicación y el riesgo para usuarios de B2B

Cuando Contoso permite que las directivas de acceso condicional basado en el dispositivo para datos de su empresa, se impida el acceso desde dispositivos que no están administrados por Contoso y no son compatibles con las directivas de dispositivo de Contoso Hola.

Si no administra el dispositivo del usuario de hello B2B por Contoso, acceso de B2B a los usuarios de organizaciones de socios comerciales de hello está bloqueado en el contexto de estas directivas se aplican. Sin embargo, Contoso puede crear listas que contengan socio específico a los usuarios tooexclude de Hola directiva de acceso condicional basado en dispositivos de exclusión.

#### <a name="location-based-conditional-access-for-b2b"></a>Acceso condicional basado en ubicación para B2B

Las directivas de acceso condicional basado en la ubicación se pueden aplicar para que los usuarios de B2B si organización invitar a hello es capaz de toocreate un intervalo de direcciones IP confianza que define sus organizaciones de socios comerciales.

#### <a name="risk-based-conditional-access-for-b2b"></a>Acceso condicional basado en riesgos para B2B

Actualmente, directivas basadas en el riesgo de inicio de sesión no pueden ser tooB2B aplicados a los usuarios, ya que se realiza la evaluación del riesgo de hello en organización principal del usuario de hello B2B.

## <a name="next-steps"></a>Pasos siguientes

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
* [Incorporación de usuarios de colaboración B2B sin invitación](active-directory-b2b-add-user-without-invite.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
