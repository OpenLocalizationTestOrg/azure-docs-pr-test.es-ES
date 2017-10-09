---
title: "aaaMicrosoft autenticador phone inicio de sesión en cuentas de Azure y Microsoft | Documentos de Microsoft"
description: "Usar su teléfono toosign en tooyour cuenta de Microsoft en lugar de escribir la contraseña. Este artículo responde a las preguntas más frecuentes acerca de esta característica."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: a4911ff580b3ffa078299ad706d099330b75a2e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-with-your-phone-not-your-password"></a>Inicie sesión con el teléfono, no la contraseña

aplicación de Microsoft Authenticator Hello le ayuda a proteger las cuentas mediante la realización de verificación en dos pasos después de escribir la contraseña. Pero ¿sabía que puede reemplazar completamente el contraseña Hola para tu cuenta Microsoft personal? 

Esta característica está disponible en dispositivos iOS y Android, y funciona con cuentas personales de Microsoft. 

## <a name="how-it-works"></a>Cómo funciona

Aplicación de Microsoft Authenticator hello muchos de los usuarios usan para la comprobación de dos pasos cuando inicia sesión en tooyour cuenta de Microsoft. Que escriba la contraseña y luego vaya toohello aplicación tooeither aprobar una notificación u obtener un código de comprobación. Con inicio de sesión de teléfono, omitir la contraseña de Hola y hacer la comprobación de identidad en el teléfono. Porque en el inicio de sesión de teléfono es un tipo de verificación en dos pasos, todavía necesita tooprovide algo que conoce y una cosa tiene tooverify tu identidad. teléfono Hola sigue siendo lo hello que tiene, y el teléfono PIN o biométrica clave lo Hola que sabe. 

## <a name="how-tooget-started"></a>Cómo iniciar tooget

toosign en tooyour cuenta personal de Microsoft con el teléfono, siga estos pasos: 

1. Habilite el inicio de sesión con el teléfono para su cuenta. 

  - Si no tiene la aplicación de Microsoft Authenticator hello todavía, instale y agregue su cuenta Microsoft personal según los pasos de toohello en hello [página Microsoft Authenticator](microsoft-authenticator-app-how-to.md). Las cuentas recién agregadas se habilitan automáticamente, así que toogo buena.

  - Si ya utiliza Microsoft Authenticator para verificación en dos pasos, seleccione su cuenta desde la página de inicio de aplicación hello y seleccione **habilita el inicio de sesión en teléfono** desde el menú desplegable de Hola.

  >[!NOTE] 
  >tooprotect tu cuenta, necesitamos un PIN o bloqueo biométrica en el dispositivo. Si mantiene el teléfono desbloqueado, aplicación hello hará que aparezca una solicitud que le pide que tooset el bloqueo de un antes de habilitar el inicio de sesión de teléfono. 

3. La mayoría de las páginas donde normalmente escribiría la contraseña de su cuenta de Microsoft tiene un vínculo que dice **Use una aplicación en su lugar**. Seleccione este toosign vínculo con su teléfono. 

4. Microsoft envía un teléfono de tooyour de notificación. Aprobar toosign de notificación de hello en tooyour cuenta.   

## <a name="faq"></a>P+F 

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>¿Cómo es que iniciar sesión con el teléfono sea más seguro que escribir una contraseña?  

Hoy en día la mayoría de los usuarios iniciar sesión en tooweb sitios o aplicaciones que usan un nombre de usuario y una contraseña.  Desafortunadamente, las contraseñas a menudo se pierden, las roban o las adivinan los piratas informáticos. Al configurar toosign de aplicación de Microsoft Authenticator hello en, se genere una clave en el teléfono que se puede desbloquear la cuenta. Protegemos esta clave con hello PIN o biométricos que ya utilice en su teléfono.  Cuando inicia sesión con su teléfono, esta clave es tooprove usado su identidad de forma segura con dos factores: hello teléfono propio y su toounlock capacidad. 

calve de Hello es similar toohello claves que se utilizan en Windows Hello y especificaciones de BOBI Alliance UAF Hola. Su biografía datos solo están usa tooprotect Hola clave localmente y es nunca envían a o almacenado en nube Hola. 
 
### <a name="where-can-i-use-my-phone-tooreplace-my-password-and-where-would-i-still-need-hello-password"></a>¿Donde puedo usar mi teléfono tooreplace mi contraseña, y donde necesitaría todavía contraseña Hola?  

En la actualidad, característica de inicio de sesión de teléfono de hello solo funciona con aplicaciones web y servicios que usan la tecnología personales cuentas de Microsoft, iOS o Android aplicaciones que usan una cuenta Microsoft personal y aplicaciones en Windows 10 que usan una cuenta Microsoft personal. Cuando inicias sesión en tooone de estos sitios web o aplicaciones, en la página Hola donde normalmente se escribe la contraseña es un vínculo que dice **usar una aplicación en su lugar**. 

Inicio de sesión de teléfono no puede ser cualquier versión de escritorio de las aplicaciones de Microsoft, como las aplicaciones de Office, XBOX o toounlock usa un equipo con Windows en este momento. 
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>¿Reemplaza esto la verificación en dos pasos? ¿Debo apagarla?   

A veces. Estamos trabajando para expandiendo Hola ámbito del inicio de sesión de teléfono, pero por ahora aún hay lugares en el ecosistema de Microsoft de Hola que no son compatibles con. En esos lugares se usa todavía la verificación en dos pasos para el inicio de sesión seguro. Por esa razón, no debería desactivar la comprobación en dos pasos para su cuenta. 
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-tooapprove-two-notifications"></a>¿Bien, si la persistencia de verificacion activado para mi cuenta tengo tooapprove dos notificaciones?

No, para nada. Inicio de sesión tooyour cuenta Microsoft con su teléfono cuenta como la verificación en dos pasos. En lugar de escribir la contraseña, a continuación, aprobar una notificación demostrar su identidad por conocer cómo toounlock su teléfono y, a continuación, aprobar una notificación. No enviará una segunda tooapprove de notificación.

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>¿Qué ocurre si pierdo mi teléfono o no lo tengo conmigo?, ¿cómo puedo acceder a mi cuenta?  

Siempre puede hacer clic en **utilice una contraseña en su lugar** en tooswitch de la página de inicio de sesión de hello realice copia toousing su contraseña. Tenga en cuenta que si usa la verificación en dos pasos, todavía necesita un segundo tooverify método el inicio de sesión de. Por eso es muy recomendable que toomake Asegúrese de que tiene información de seguridad adicional, actualizada en tu cuenta. Puede administrar la información de seguridad en https://account.live.com/proofs/manage. 
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-tooentering-my-password"></a>¿Cómo dejar de usar esta característica y volver atrás tooentering mi contraseña?

Haga clic en **Use su contraseña en su lugar** al iniciar sesión. Se recuerda su elección más reciente y ofrecen Hola de manera predeterminada gracias a la próxima vez que inicie sesión en. Si alguna vez quieres toogo atrás toosigning con su teléfono, haga clic en **usar una aplicación en su lugar**. 
 
### <a name="can-i-use-hello-app-toosign-in-tooall-my-accounts-with-microsoft"></a>¿Puedo usar toosign de aplicación hello en tooall Mis cuentas con Microsoft?   
Por ahora, esta funcionalidad solo está disponible para cuentas personales de Microsoft. 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>¿Puedo iniciar sesión en mi PC con el teléfono?  
Para el PC, se recomienda iniciar sesión con Windows Hello de Windows 10 con la cara, la huella digital o un PIN.   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>¿Puedo iniciar sesión con mi Windows Phone?  
En este momento, no estamos desarrollando esta funcionalidad en hello Microsoft Authenticator en Windows Phone. 

## <a name="next-steps"></a>Pasos siguientes
Si ha descargado la aplicación de Microsoft Authenticator hello, desprotegerlo. está disponible para la aplicación Hello [de Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), y en el inicio de sesión de teléfono está disponible en la aplicación de Microsoft Authenticator hello para [Android](http://go.microsoft.com/fwlink/?Linkid=825072) y [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

Si tiene preguntas acerca de la aplicación hello en general, eche un vistazo a hello [preguntas más frecuentes de Microsoft autenticador](microsoft-authenticator-app-faq.md)
