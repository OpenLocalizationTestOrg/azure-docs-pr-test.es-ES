---
title: "inicio de sesión en aaaAzure MFA con la verificacion | Documentos de Microsoft"
description: "Esta página le proporcionará instrucciones en donde toogo toosee Hola distintos inicio de sesión métodos disponibles con Azure MFA."
keywords: "autenticación de usuario, experiencia de inicio de sesión, inicio de sesión con el teléfono móvil, inicio de sesión con el teléfono del trabajo"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>experiencia de inicio de sesión de Hello con autenticación multifactor de Azure
> [!NOTE]
> Hola de este artículo sirve toowalk a través de una experiencia de inicio de sesión típica. Para obtener ayuda con el inicio de sesión o tootroubleshoot problemas, consulte [tenga problemas con la autenticación multifactor Azure](multi-factor-authentication-end-user-troubleshoot.md).

## <a name="what-will-your-sign-in-experience-be"></a>¿Cómo se presenta la experiencia de inicio de sesión?
La experiencia de inicio de sesión depende de cuál sea su elección toouse como el segundo factor: una llamada de teléfono, una aplicación de autenticación o textos. Elija la opción de Hola que mejor describa lo que está haciendo:

| ¿Cómo se puede iniciar sesión? | 
| --- |
| [Con un teléfono móvil o de office del toomy de llamada de teléfono](#signing-in-with-a-phone-call) |
| [Con un toomy texto a teléfono móvil](#signing-in-with-a-text-message)
| [Con las notificaciones de la aplicación de Microsoft Authenticator hello](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [Con los códigos de verificación de aplicación de Microsoft Authenticator hello](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [Con un método alternativo, ya que ahora no puedo usar mi método preferido](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>Inicio de sesión con una llamada de teléfono
Hola siguiente información describe hello en dos pasos comprobación experiencia con un tooyour de llamada de teléfono móvil o teléfono del trabajo.

1. Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña.  
2. Microsoft lo llamará.  
3. Responda Hola teléfono y pulse Hola # tecla.  

## <a name="signing-in-with-a-text-message"></a>Inicio de sesión con un mensaje de texto
Hola siguiente información describe la experiencia de comprobación de dos pasos de hello con un mensaje texto tooyour a teléfono móvil:

1. Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña. 
2. Microsoft envía un mensaje de texto que contiene un código numérico. 
3. Escriba el código de hello en cuadro Hola proporcionada en página de inicio de sesión de Hola. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Inicio de sesión con la aplicación de Microsoft Authenticator hello 
Hello siguiente información describe Hola experiencia de usuario de aplicación de Microsoft Authenticator hello para comprobaciones de dos pasos. Hay dos maneras diferentes toouse Hola aplicación. Puede recibir notificaciones de inserción en el dispositivo, o puede abrir Hola aplicación tooget un código de comprobación.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>toosign con una notificación de aplicación de Microsoft Authenticator hello
1. Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña.
2. Microsoft envía una aplicación de Microsoft Authenticator toohello de notificación en el dispositivo.

  ![Microsoft envía una notificación](./media/multi-factor-authentication-end-user-signin/notify.png)

3. Notificación de hello abierto en su teléfono y seleccione hello **compruebe** clave. Si su empresa requiere un PIN, escríbalo aquí.
4. Con esto debe haber iniciado sesión.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>toosign sesión utilizando un código de comprobación con la aplicación de Microsoft Authenticator hello

Si utiliza códigos de verificación de hello Microsoft Authenticator aplicación tooget, a continuación, cuando se abre la aplicación hello aparece un número en su nombre de cuenta. Este número cambia cada 30 segundos para que no use Hola mismo número dos veces. Cuando se le pregunte para un código de comprobación, abra la aplicación hello y usar cualquier número se muestra actualmente. 

1. Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña.
2. Microsoft le pedirá un código de verificación.

  ![Escribir el código de comprobación](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. Abra la aplicación de Microsoft Authenticator hello en el teléfono y escriba el código de hello en donde va a iniciar sesión en el cuadro de Hola.

## <a name="signing-in-with-an-alternate-method"></a>Inicio de sesión con un método alternativo
En ocasiones, no tienes teléfono de Hola o dispositivo que configuró como método de comprobación preferida. Esta situación es el motivo por el que se recomienda configurar métodos de copia de seguridad para la cuenta. Hello siguiente sección muestra cómo toosign con un método alternativo en su método principal podría no estar disponible.

1. Inicie sesión en tooan aplicación o servicio, como Office 365 con su nombre de usuario y contraseña.
2. Seleccione **Usar otra opción de comprobación**. Verá distintas opciones de comprobación en función del número de ellas que haya configurado.
3. Elija un método alternativo e inicie sesión.

  ![Usar método alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>Pasos siguientes

Si tiene problemas para iniciar sesión con la verificación en dos pasos, obtenga más información en [Problemas con Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).

Obtenga información acerca de cómo demasiado[administrar la configuración de comprobación de dos pasos](multi-factor-authentication-end-user-manage-settings.md).

Obtener información sobre cómo demasiado[Introducción a la aplicación de Microsoft Authenticator hello](microsoft-authenticator-app-how-to.md) para que pueda utilizar toosign de notificaciones, en lugar de textos y llamadas de teléfono. 
