---
title: 'Azure Active Directory B2C: Multi-Factor Authentication | Microsoft Docs'
description: "¿Cómo tooenable la autenticación multifactor en las aplicaciones orientadas al consumidor protegida por Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a>Azure Active Directory B2C: habilitación de Multi-Factor Authentication en las aplicaciones orientadas al consumidor
Azure B2C de Active Directory (Azure AD) se integra directamente con [la autenticación multifactor Azure](../multi-factor-authentication/multi-factor-authentication.md) para que pueda agregar una segunda capa de experiencias de toosign de seguridad e inicio de sesión de seguridad en las aplicaciones de consumo. Y todo esto sin necesidad de escribir una sola línea de código. Actualmente se admite la comprobación mediante llamadas de teléfono y mensajes de texto. Aunque ya haya creado directivas de registro e inicio de sesión, puede habilitar Multi-Factor Authentication.

> [!NOTE]
> También se puede habilitar Multi-Factor Authentication al crear directivas de registro e inicio de sesión, no solo mediante la edición de las directivas existentes.
> 
> 

Esta característica permite a las aplicaciones administrar escenarios como siguiente hello:

* No es necesario tooaccess una aplicación de la autenticación multifactor, pero que sea necesario tooaccess otro. Por ejemplo, puede iniciar sesión en una aplicación de seguros automáticamente con una cuenta local o sociales consumidor hello, pero debe comprobar el número de teléfono de hello antes de obtener acceso a aplicación seguros particular de hello registre en hello mismo directorio.
* Por lo general no necesita la autenticación multifactor tooaccess una aplicación, pero requiere partes importantes de hello tooaccess dentro de él. Por ejemplo, consumidor de hello puede iniciar sesión en tooa aplicación con un saldo de cuenta de comprobación y una cuenta local o sociales de banca, pero debe comprobar el número de teléfono de hello antes de intentar a una transferencia de conexión.

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a>Modificar el tooenable de directiva de suscripción a la autenticación multifactor
1. [Siga estos módulos de características de pasos toonavigate toohello B2C en hello portal de Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Haga clic en **Directivas de registro**.
3. Haga clic en la directiva de inicio de sesión (por ejemplo, "B2C_1_SiUp") tooopen.
4. Haga clic en **la autenticación multifactor** y activar hello **estado** demasiado**ON**. Haga clic en **Aceptar**.
5. Haga clic en **guardar** princip Hola de hoja de Hola.

Puede usar la característica de "Ejecutar ahora" hello en la experiencia del consumidor de hello directiva tooverify Hola. Confirmar siguiente hello:

Se crea una cuenta de cliente en el directorio antes de que se produce el paso de la autenticación multifactor de Hola. Durante el paso de hello, consumidor de Hola se solicita tooprovide su número de teléfono y compruebe si. Si la comprobación es correcta, se adjunta el número de teléfono de hello toohello cuenta de cliente para su uso posterior. Incluso si el consumidor de Hola se cancela o se quita, que se pueden hacer tooverify un número de teléfono nuevo durante Hola de inicio de sesión siguiente (con la autenticación multifactor habilitada).

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a>Modificar el tooenable de inicio de sesión de la directiva la autenticación multifactor
1. [Siga estos módulos de características de pasos toonavigate toohello B2C en hello portal de Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Haga clic en **Directivas de inicio de sesión**.
3. Haga clic en la directiva de inicio de sesión (por ejemplo, "B2C_1_SiIn") tooopen. Haga clic en **editar** princip Hola de hoja de Hola.
4. Haga clic en **la autenticación multifactor** y activar hello **estado** demasiado**ON**. Haga clic en **Aceptar**.
5. Haga clic en **guardar** princip Hola de hoja de Hola.

Puede usar la característica de "Ejecutar ahora" hello en la experiencia del consumidor de hello directiva tooverify Hola. Confirmar siguiente hello:

Al consumidor de Hola inicia sesión (con una cuenta local o sociales), si se ha adjuntado un número de teléfono comprobado toohello cuenta de cliente, se le pedirá tooverify lo. Si no se ha adjuntado ningún número de teléfono, consumidor de Hola se solicita tooprovide uno y confírmela. En comprobación correcta, se adjunta el número de teléfono de hello toohello cuenta de cliente para su uso posterior.

## <a name="multi-factor-authentication-on-other-policies"></a>Multi-Factor Authentication en otras directivas
Tal y como se ha descrito para las directivas de inicio de sesión & inicio de sesión anteriores, también es posible tooenable la autenticación multifactor en Inicio de sesión o directivas de restablecimiento de contraseña y directivas de inicio de sesión. Muy pronto estará disponible en las directivas de edición de perfiles.

