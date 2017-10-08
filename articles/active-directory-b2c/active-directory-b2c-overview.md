---
title: "Introducción a Azure AD B2C | Microsoft Docs"
description: Desarrollo de aplicaciones orientadas al consumidor con Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c465dbde-f800-4f2e-8814-0ff5f5dae610
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: saeedakhter-msft
ms.openlocfilehash: abfd742e710458de3193dc5051de7818a112376c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-focus-on-your-app-let-us-worry-about-sign-up-and-sign-in"></a>Azure AD B2C: céntrese en su aplicación y deje que nosotros nos encarguemos del registro y el inicio de sesión

Azure AD B2C es una solución de administración de identidades en la nube, destinada a aplicaciones móviles y web. Es un servicio global de alta disponibilidad que escala toohundreds de millones de identidades. Basado en una plataforma segura de nivel empresarial, Azure AD B2C protege las aplicaciones, la empresa y los clientes.

Con la configuración mínima, Azure AD B2C permite su tooauthenticate de aplicación:

* **Cuentas sociales** (como Facebook, Google, LinkedIn, etc.)
* **Cuentas de empresa** (mediante protocolos estándar abiertos, OpenID Connect o SAML)
* **Cuentas locales** (dirección de correo electrónico y contraseña, o nombre de usuario y contraseña)

## <a name="get-started"></a>Primeros pasos

En primer lugar, obtener su propio inquilino mediante el uso de pasos de hello descritos en [crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).

Después, elija su escenario de desarrollo de aplicaciones:

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Aplicaciones para dispositivos móviles y de escritorio](../active-directory/develop/media/active-directory-developers-guide/NativeApp_Icon.png)<br />Aplicaciones para dispositivos móviles y de escritorio</center> | [Información general](active-directory-b2c-reference-oauth-code.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br /><br />[iOS](https://github.com/Azure-Samples/active-directory-b2c-ios-swift-native-msal)<br /><br />[Android](https://github.com/Azure-Samples/active-directory-b2c-android-native-msal) | [.NET](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop)<br /><br />[Xamarin](https://github.com/Azure-Samples/active-directory-b2c-xamarin-native) |  |
| <center>![Web Apps](../active-directory/develop/media/active-directory-developers-guide/Web_app.png)<br />Web Apps</center> | [Información general](active-directory-b2c-reference-oidc.md)<br /><br />[ASP.NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)<br /><br />[ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapp) | [Node.js](active-directory-b2c-devquickstarts-web-node.md) |  |
| <center>![Aplicaciones de una sola página](../active-directory/develop/media/active-directory-developers-guide/SPA.png)<br />Aplicaciones de una sola página</center> | [Información general](active-directory-b2c-reference-spa.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp)<br /><br /> |  |  |
| <center>![API web](../active-directory/develop/media/active-directory-developers-guide/Web_API.png)<br />API web</center> | [ASP.NET](active-directory-b2c-devquickstarts-api-dotnet.md)<br /><br /> [ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)<br /><br /> [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) | [Llamada de una API web de .NET](active-directory-b2c-devquickstarts-web-api-dotnet.md) |

## <a name="whats-new"></a>Novedades

Vuelva a comprobar a menudo toolearn sobre cambios futuros toohello Azure Active Directory B2C. También enviaremos tweets acerca de las actualizaciones mediante @AzureAD.

* Además demasiado Hola "Directivas integradas" (Disponibilidad General), ["Directivas personalizadas"](active-directory-b2c-overview-custom.md) característica ahora está disponible en vista previa pública.  Las directivas personalizadas son para los profesionales de TI de identidad que tenga control sobre la composición de Hola de su experiencia de identidad.
* Hola [Token de acceso](https://azure.microsoft.com/en-us/blog/azure-ad-b2c-access-tokens-now-in-public-preview) característica ahora está disponible en vista previa pública.
* Se ha anunciado la [disponibilidad general de directorios de Azure AD B2C basados en Europa](https://azure.microsoft.com/en-us/blog/azuread-b2c-ga-eu/).
* Consulte nuestra biblioteca cada vez mayor de [ejemplos de código en GitHub](https://github.com/Azure-Samples?q=b2c).

## <a name="how-tooarticles"></a>Cómo tooarticles

Obtenga información acerca de cómo toouse determinadas características de Azure Active Directory B2C:

* Configure las cuentas de [Facebook](active-directory-b2c-setup-fb-app.md), [Google+](active-directory-b2c-setup-goog-app.md), [Cuenta Microsoft](active-directory-b2c-setup-msa-app.md), [Amazon](active-directory-b2c-setup-amzn-app.md) y [LinkedIn](active-directory-b2c-setup-li-app.md) para usarlas en las aplicaciones orientadas al consumidor.
* [Utilizar atributos personalizados toocollect información acerca de los consumidores](active-directory-b2c-reference-custom-attr.md).
* [Habilitación de Azure Multi-Factor Authentication en las aplicaciones orientadas al consumidor](active-directory-b2c-reference-mfa.md).
* [Configuración del restablecimiento de contraseña de autoservicio para los consumidores](active-directory-b2c-reference-sspr.md).
* [Personalizar Hola apariencia y comportamiento de inicio de sesión, inicie sesión en y otras páginas de consumo](active-directory-b2c-reference-ui-customization.md) que se sirven mediante Azure Active Directory B2C.
* [Use Hola API Graph de Azure Active Directory tooprogrammatically crear, leer, actualizar y eliminar los consumidores](active-directory-b2c-devquickstarts-graph-dotnet.md) en su inquilino de Azure Active Directory B2C.

## <a name="next-steps"></a>Pasos siguientes

Estos vínculos son útiles para explorar el servicio de hello en profundidad:

* Vea hello [información sobre los precios de Azure Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).
* Revise nuestros [ejemplos de código](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory&term=b2c) para Azure Active Directory B2C. 
* Obtener ayuda acerca del desbordamiento de pila mediante hello [azure-ad-b2c](http://stackoverflow.com/questions/tagged/azure-ad-b2c) etiqueta.
* Envíenos sus ideas utilizando [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c), queremos toohear ellos!
* Hola de revisión [referencia del protocolo de Azure AD B2C](active-directory-b2c-reference-protocols.md).
* Hola de revisión [referencia símbolo (token) de Azure AD B2C](active-directory-b2c-reference-tokens.md).
* Hola de lectura [Azure Active Directory B2C preguntas más frecuentes sobre](active-directory-b2c-faqs.md).
* [Presentación de solicitudes de soporte técnico para Azure Active Directory B2C](active-directory-b2c-support.md).

## <a name="get-security-updates-for-our-products"></a>Obtención de actualizaciones de seguridad para nuestros productos

Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.

