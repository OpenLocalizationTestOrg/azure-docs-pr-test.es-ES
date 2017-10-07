---
title: aaaTroubleshoot verificacion | Documentos de Microsoft
description: "Este documento proporcionará a los usuarios información sobre qué toodo si se ejecutan en un problema con la autenticación multifactor Azure."
services: multi-factor-authentication
keywords: "cliente de multi-factor authentication, problema de autenticación, identificador de correlación"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: end-user
ms.openlocfilehash: f5c980d104de684b052c0f7a13394f00e9828abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-help-with-two-step-verification"></a>Obtener ayuda con la verificación en dos pasos
Este artículo se proporcionan respuestas hello más comunes preguntas sobre la verificación en dos pasos. 

## <a name="why-do-i-have-tooperform-two-step-verification-can-i-turn-it-off"></a>¿Por qué tengo verificacion de tooperform? ¿Puedo desactivarla?

Verificación en dos pasos es una característica de seguridad que su organización eligió toouse tooprotect sus cuentas. Es más segura que solo una contraseña, porque se basa en dos formas de autenticación: algo que usted sabe y algo que usted tiene. Hola algo que sabe que es su contraseña. Hola algo que tiene con usted es un teléfono o un dispositivo que tiene normalmente con usted. Si su cuenta está protegida con la verificación en dos pasos, que significa que un hacker malintencionado no puede iniciar sesión como si obtienen la contraseña de algún modo porque no tienen teléfono tooyour de acceso, demasiado. 

Microsoft ofrece verificación en dos pasos, pero la característica de hello toouse elija de su organización. Que no se puede dejar de participar si el departamento de TI lo requiere de, al igual que no se puede rechazar utilizando una contraseña tooprotect tu cuenta. 

Si tiene verificacion activado para su cuenta personal de Microsoft y desea toochange su configuración, leer [sobre la verificación en dos pasos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) en su lugar. 

## <a name="i-dont-have-my-phone-with-me-today"></a>No tengo mi teléfono conmigo hoy

Hace unos días dejar el teléfono en casa, pero que todavía necesitan toosign en el trabajo. Hola primera cosa que debe intentar es iniciar sesión con un método de verificación diferente. Al registrarse para la verificación en dos pasos, ¿se configura más de un número de teléfono? tootry inicio de sesión con un método diferente, siga estos pasos:

1. Inicie sesión como lo haría normalmente.
2. Cuando se abre la página de comprobación de hello en dos pasos, elija **usar otra opción de comprobación**.

   ![Comprobación distinta](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. Seleccione la opción de comprobación de Hola que desee toouse.
4. Continúe con la verificación en dos pasos.

Si no ve hello **usar otra opción de comprobación** vincular, a continuación, que significa que no ha configurado métodos alternativos cuando registraron por primera vez para la verificación en dos pasos. Póngase en contacto con la Ayuda de tooget del departamento de TI tooyour cuenta de inicio de sesión. Una vez que ha iniciado sesión, asegúrese de que demasiado[administrar la configuración de](multi-factor-authentication-end-user-manage-settings.md) tooadd métodos de comprobación adicional para la próxima vez. 

Si ve hello **usar otra opción de comprobación** vínculo, pero no dispone de métodos alternativos de acceso tooyour bien, póngase en contacto con la Ayuda de tooget del departamento de TI tooyour cuenta de inicio de sesión. 

## <a name="i-lost-my-phone-or-got-a-new-number"></a>Perdí mi teléfono o cambié de número
Hay dos tooget maneras en tooyour cuenta. Hola en primer lugar es toosign sesión con su número de teléfono de autenticación alternativo, si ha configurado uno. Hola en segundo lugar es tooask su tooclear del departamento de TI la configuración.

Si perdió el teléfono o se lo robaron, también le recomendamos que se lo diga al departamento de TI para que restablezca las contraseñas de aplicación y borre todos los dispositivos recordados. 

### <a name="use-an-alternate-phone-number"></a>Usar un número de teléfono alternativo
Si ha configurado varias opciones de comprobación, incluido un número de teléfono secundario o una aplicación de autenticador en un dispositivo distinto, puede usar uno de ellos toosign en.

toosign sesión con el número de teléfono alternativo de hello, siga estos pasos:

1. Inicie sesión como lo haría normalmente.
2. Cuando toofurther solicitada comprobar tu cuenta, elija **usar otra opción de comprobación**.
   
   ![Comprobación distinta](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. Seleccione el número de teléfono de Hola o dispositivo que tenga acceso a.
4. Una vez que haya en su cuenta, [administrar la configuración de](multi-factor-authentication-end-user-manage-settings.md) toochange número de teléfono de la autenticación.

### <a name="clear-your-settings"></a>Borrar su configuración
Si no ha configurado un número de teléfono de autenticación secundaria, deberá toocontact el departamento de TI para obtener ayuda. Ha ellos borrar la configuración de modo que Hola la próxima vez inicie sesión, se le pedirá demasiado[registrar para la verificación en dos pasos](multi-factor-authentication-end-user-first-time.md) nuevo.

## <a name="i-am-not-receiving-a-text-or-call-on-my-phone"></a>No recibo ningún mensaje o llamada en el teléfono
Hay varios motivos por qué puede intente toosign en, pero no recibe la llamada de teléfono o el texto hello. Si ha recibido correctamente textos o llamadas de teléfono tooyour teléfono Hola anteriores, a continuación, probablemente es un problema con el proveedor de servicio telefónico hello, no su cuenta. Asegúrese de que tiene celda buena señal y si está tratando de tooreceive un mensaje de texto Asegúrese de que es capaz de toorecieve los mensajes de texto. Solicitar un toocall friend se o texto como una prueba. 

Si ha esperado varios minutos para una llamada o el texto, hello tooget de manera más rápida en su cuenta es tootry una opción diferente.

1. Seleccione **usar otra opción de comprobación** en las páginas de Hola que está esperando que la comprobación.
   
    ![Comprobación distinta](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)
2. Seleccione el método de entrega o número de la teléfono de Hola que desee toouse.
   
    Si recibe varios códigos de comprobación, utilice hello más reciente.

Si no tienes otro método configurado, póngase en contacto con el departamento de TI y pídale que tooclear su configuración. Hello próxima vez que inicie sesión, se le pedirá demasiado[configurar la autenticación multifactor](multi-factor-authentication-end-user-first-time.md) nuevo.

Si tiene a menudo retrasos debido toobad señal de celda, se recomienda usar hello [aplicación Microsoft Authenticator](microsoft-authenticator-app-how-to.md) en tu smartphone. aplicación Hello puede generar los códigos de seguridad aleatorio que usan toosign en, y estos códigos no requieren ninguna celda señal o conexión a internet.

## <a name="app-passwords-are-not-working"></a>Las contraseñas de la aplicación no funcionan
En primer lugar, asegúrese de que ha escrito correctamente contraseña de aplicación Hola. contraseña de aplicación Hola genera reemplaza la contraseña normal, pero solo para aplicaciones de escritorio más antiguos que no son compatibles con la verificación en dos pasos. Si sigue sin funcionar, intente iniciar sesión y [cree una nueva contraseña de aplicación](multi-factor-authentication-end-user-app-passwords.md).  Si aún no funciona, póngase en contacto con el departamento de TI, pídale que [elimine sus contraseñas de aplicación existentes](../multi-factor-authentication-manage-users-and-devices.md) y luego puede crear otra.

## <a name="i-didnt-find-an-answer-toomy-problem"></a>No se encontró un problema de toomy de respuesta.
Si probó estos pasos para solucionar los problemas pero estos no desaparecen, póngase en contacto con el departamento de TI. Deben ser capaz de tooassist.

## <a name="related-topics"></a>Temas relacionados
* [Administración de la configuración de la comprobación en dos pasos](multi-factor-authentication-end-user-manage-settings.md)  
* [Preguntas más frecuentes de la aplicación Microsoft Authenticator](microsoft-authenticator-app-faq.md)

