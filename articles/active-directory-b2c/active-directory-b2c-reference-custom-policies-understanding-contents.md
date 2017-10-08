---
title: "Azure B2C Directory Active: Descripción de las directivas personalizadas de módulo de inicio de Hola | Documentos de Microsoft"
description: Un tema acerca de las directivas personalizadas de Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>Descripción de las directivas personalizadas de Hola de módulo de inicio de directiva personalizada de hello Azure AD B2C

Esta sección enumeran todos los elementos básicos de Hola de directiva de hello B2C_1A_base que viene con hello **Starter Pack** y que se utiliza para crear sus propias directivas a través de la herencia de Hola de hello *B2C_1A_base_ Directiva de extensiones*.

Por lo tanto, lo más especialmente se centra en hello ya definido tipos, las transformaciones de notificaciones, las definiciones de contenido, proveedores de notificaciones con sus perfiles técnicas de notificación y Hola viajes de usuario principal.

> [!IMPORTANT]
> Microsoft no otorga ninguna garantía, expresa ni implícita, con respecto toohello información proporciona ahora en adelante. En cualquier momento se pueden introducir cambios, antes de la hora de disponibilidad general, en ese mismo momento o después.

Tanto sus propias directivas hello y B2C_1A_base_extensions directiva pueden invalidar estas definiciones y extender esta directiva principal proporcionando perfiles adicionales según sea necesario.

Hola elementos básicos de hello *B2C_1A_base directiva* son tipos de notificación, las transformaciones de notificaciones y las definiciones de contenido. Estos elementos pueden toobe susceptible al que hace referencia en sus propias directivas así como en hello *B2C_1A_base_extensions directiva*.

## <a name="claims-schemas"></a>Esquemas de notificaciones

Estos esquemas de notificaciones se dividen en tres secciones:

1.  Primera sección que enumera las notificaciones mínimo de Hola que son necesarios para hello usuario viajes toowork correctamente.
2.  Una segunda sección que listas Hola notificaciones necesarias para los parámetros de cadena de consulta y otro parámetros especiales toobe pasa tooother proveedores de notificaciones, especialmente login.microsoftonline.com para la autenticación. **No modifique estas notificaciones**.
3.  Y finalmente, una tercera sección que enumera las notificaciones adicionales y opcionales que se pueden recopilar de usuario de hello, almacenados en el directorio de Hola y envían en símbolos (tokens) durante el inicio de sesión. Pueden agregarse nuevas notificaciones tipo toobe recopilados del usuario de Hola o enviados en el token de hello en esta sección.

> [!IMPORTANT]
> esquema de notificaciones de Hello contiene restricciones en ciertas notificaciones, como contraseñas y nombres de usuario. Hola directiva de confianza Framework (TF) trata Azure AD como cualquier otro proveedor de notificaciones y todas sus restricciones se reproduzcan en la directiva de hello premium. Una directiva podría ser modificado tooadd más restricciones o utilizar otro proveedor de notificaciones para el almacenamiento de credenciales que tendrá sus propias restricciones.

tipos de notificación disponibles Hola se enumeran a continuación.

### <a name="claims-that-are-required-for-hello-user-journeys"></a>Notificaciones que son necesarios para los viajes de usuario de Hola

Hola siguientes notificaciones se necesitan para usuario viajes toowork correctamente:

| Tipo de notificaciones | Descripción |
|-------------|-------------|
| *UserId* | Nombre de usuario |
| *signInName* | Nombre de inicio de sesión |
| *tenantId* | Identificador del inquilino (Id.) del objeto de usuario de hello en Premium de Azure AD B2C |
| *objectId* | Identificador de objeto (Id.) del objeto de usuario de hello en Premium de Azure AD B2C |
| *password* | Password |
| *newPassword* | |
| *reenterPassword* | |
| *passwordPolicies* | Directivas de contraseña que se usa seguridad de la contraseña de Azure AD B2C Premium toodetermine, expiración, etcetera. |
| *sub* | |
| *alternativeSecurityId* | |
| *identityProvider* | |
| *displayName* | |
| *strongAuthenticationPhoneNumber* | Número de teléfono del usuario. |
| *Verified.strongAuthenticationPhoneNumber* | |
| *email* | Dirección de correo electrónico que puede ser usado toocontact Hola usuario |
| *signInNamesInfo.emailAddress* | Dirección de correo electrónico Hola usuario puede usar toosign en |
| *otherMails* | Direcciones de correo electrónico que pueden ser usado toocontact Hola usuario |
| *userPrincipalName* | Nombre de usuario tal como se almacena en hello Premium de Azure AD B2C |
| *upnUserName* | Nombre de usuario para la creación del nombre principal de usuario. |
| *mailNickName* | Nombre de nick de correo electrónico del usuario tal como se almacena en hello Premium de Azure AD B2C |
| *newUser* | |
| *executed-SelfAsserted-Input* | Notificación que especifica si se recopilaron atributos de usuario de Hola |
| *executed-PhoneFactor-Input* | Notificación que especifica si se ha recopilado un nuevo número de teléfono de usuario de Hola |
| *authenticationSource* | Especifica si se autenticó el usuario de hello en el proveedor de identidades sociales, login.microsoftonline.com o cuenta local |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>Notificaciones necesarias para los parámetros de cadena de consulta y otros parámetros especiales

Hello notificaciones siguientes son necesarios toopass en proveedores de notificaciones de tooother parámetros especiales (incluidos algunos parámetros de cadena de consulta):

| Tipo de notificaciones | Descripción |
|-------------|-------------|
| *nux* | Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local |
| *nca* | Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local |
| *prompt* | Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local |
| *mkt* | Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local |
| *lc* | Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local |
| *grant_type* | Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local |
| *scope* | Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local |
| *client_id* | Parámetro especial que se pasa para toologin.microsoftonline.com de autenticación de cuenta local |
| *objectIdFromSession* | Parámetro proporcionado por hello predeterminado sesión administración proveedor tooindicate que Hola Id. de objeto se ha recuperado de una sesión SSO |
| *isActiveMFASession* | Parámetro proporcionada por hello MFA sesión administración tooindicate que Hola el usuario tiene una sesión activa de MFA |

### <a name="additional-optional-claims-that-can-be-collected"></a>Notificaciones (opcionales) adicionales que se pueden recopilar

siguiente Hola notificaciones son notificaciones adicionales que se pueden recopilar de los usuarios de hello, almacenados en el directorio de Hola y enviados en el token de Hola. Tal y como se ha descrito antes, se pueden agregar notificaciones adicionales toothis lista.

| Tipo de notificaciones | Descripción |
|-------------|-------------|
| *givenName* | Nombre dado del usuario (también conocido como nombre de pila) |
| *surname* | Apellido del usuario (también conocido como nombre de familia) |
| *Extension_picture* | Foto del usuario de las redes sociales |

## <a name="claim-transformations"></a>Transformaciones de notificación

transformaciones de notificación disponibles Hola se enumeran a continuación.

| Transformación de notificación | Descripción |
|----------------------|-------------|
| *CreateOtherMailsFromEmail* | |
| *CreateRandomUPNUserName* | |
| *CreateUserPrincipalName* | |
| *CreateSubjectClaimFromObjectID* | |
| *CreateSubjectClaimFromAlternativeSecurityId* | |
| *CreateAlternativeSecurityId* | |

## <a name="content-definitions"></a>Definiciones de contenido

En esta sección se describe las definiciones de contenido de hello ya declaradas en hello *B2C_1A_base* directiva. Estas definiciones de contenido son susceptibles de sufrir toobe al que hace referencia, se reemplaza o extender según sea necesario en sus propias directivas así como en hello *B2C_1A_base_extensions* directiva.

| Proveedor de notificaciones | Descripción |
|-----------------|-------------|
| *Facebook* | |
| *Inicio de sesión en una cuenta local* | |
| *PhoneFactor* | |
| *Azure Active Directory* | |
| *Autoafirmado* | |
| *Cuenta local* | |
| *Administración de sesiones* | |
| *Trustframework Policy Engine* | |
| *TechnicalProfiles* | |
| *Emisor de tokens* | |

## <a name="technical-profiles"></a>Perfiles técnicos

En esta sección se describe perfiles técnica Hola ya declarados por el proveedor de notificaciones en hello *B2C_1A_base* directiva. Estos perfiles técnicos son susceptibles de sufrir toobe más al que hace referencia, se reemplaza o extender según sea necesario en sus propias directivas así como en hello *B2C_1A_base_extensions* directiva.

### <a name="technical-profiles-for-facebook"></a>Perfiles técnicos de Facebook

| Perfil técnico | Descripción |
|-------------------|-------------|
| *Facebook-OAUTH* | |

### <a name="technical-profiles-for-local-account-signin"></a>Perfiles técnicos de inicio de sesión en una cuenta local

| Perfil técnico | Descripción |
|-------------------|-------------|
| *Login-NonInteractive* | |

### <a name="technical-profiles-for-phone-factor"></a>Perfiles técnicos de Phone Factor

| Perfil técnico | Descripción |
|-------------------|-------------|
| *PhoneFactor-Input* | |
| *PhoneFactor-InputOrVerify* | |
| *PhoneFactor-Verify* | |

### <a name="technical-profiles-for-azure-active-directory"></a>Perfiles técnicos de Azure Active Directory

| Perfil técnico | Descripción |
|-------------------|-------------|
| *AAD-Common* | Perfil técnica incluido por Hola otros perfiles técnicas AAD-xxx |
| *AAD-UserWriteUsingAlternativeSecurityId* | Perfil técnico de inicios de sesión sociales |
| *AAD-UserReadUsingAlternativeSecurityId* | Perfil técnico de inicios de sesión sociales |
| *AAD-UserReadUsingAlternativeSecurityId-NoError* | Perfil técnico de inicios de sesión sociales |
| *AAD-UserWritePasswordUsingLogonEmail* | Perfil técnico de cuentas locales |
| *AAD-UserReadUsingEmailAddress* | Perfil técnico de cuentas locales |
| *AAD-UserWriteProfileUsingObjectId* | Perfil técnico de actualización de registros de usuario mediante objectId |
| *AAD-UserWritePhoneNumberUsingObjectId* | Perfil técnico de actualización de registros de usuario mediante objectId |
| *AAD-UserWritePasswordUsingObjectId* | Perfil técnico de actualización de registros de usuario mediante objectId |
| *AAD-UserReadUsingObjectId* | Perfil técnica es datos tooread usado cuando se autentica el usuario |

### <a name="technical-profiles-for-self-asserted"></a>Perfiles técnicos autoafirmados

| Perfil técnico | Descripción |
|-------------------|-------------|
| *SelfAsserted-Social* | |
| *SelfAsserted-ProfileUpdate* | |

### <a name="technical-profiles-for-local-account"></a>Perfiles técnicos de cuenta local

| Perfil técnico | Descripción |
|-------------------|-------------|
| *LocalAccountSignUpWithLogonEmail* | |

### <a name="technical-profiles-for-session-management"></a>Perfiles técnicos de administración de sesiones

| Perfil técnico | Descripción |
|-------------------|-------------|
| *SM-Noop* | |
| *SM-AAD* | |
| *SM-SocialSignup* | Nombre del perfil se sesión AAD toodisambiguate utilizado entre el inicio de sesión y la puesta iniciar sesión en |
| *SM-SocialLogin* | |
| *SM-MFA* | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Perfiles técnicos de Trustframework Policy Engine TechnicalProfiles

Actualmente, no hay perfiles técnicas se definen para hello **TechnicalProfiles de motor de directiva de Trustframework** proveedor de notificaciones.

### <a name="technical-profiles-for-token-issuer"></a>Perfiles técnicos del emisor de tokens

| Perfil técnico | Descripción |
|-------------------|-------------|
| *JwtIssuer* | |

## <a name="user-journeys"></a>Recorridos de usuario

Esta sección describe los viajes de usuario de hello ya declarados en hello *B2C_1A_base* directiva. Estos desplazamientos de usuario son susceptibles de sufrir toobe más al que hace referencia, se reemplaza o extender según sea necesario en sus propias directivas así como en hello *B2C_1A_base_extensions* directiva.

| Recorrido de usuario | Descripción |
|--------------|-------------|
| *SignUp* | |
| *SignIn* | |
| *SignUpOrSignIn* | |
| *EditProfile* | |
| *PasswordReset* | |
