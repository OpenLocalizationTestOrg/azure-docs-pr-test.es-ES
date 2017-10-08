---
title: aaaAzure Active Directory para desarrolladores | Documentos de Microsoft
description: "En este artículo se proporciona información general de inicio de sesión en las cuentas de trabajo y educativas de Microsoft con Azure Active Directory."
services: active-directory
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5c872c89-ef04-4f4c-98de-bc0c7460c7c2
ms.service: active-directory
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4dbbea6c1e0b8a70c0c36ddd1caec5658130a003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-for-developers"></a>Azure Active Directory para desarrolladores
Azure Active Directory es un servicio de identidad de nube que permite a los desarrolladores toosecurely inicio de sesión de cualquier usuario con una cuenta profesional o educativa respaldado por Microsoft.  documentación de Hello aquí muestra cómo tooadd Azure AD son compatibles con la aplicación tooyour uso de protocolos de autenticación estándar del sector, OAuth y OpenID Connect.

| | |
| --- | --- |
|[Conceptos básicos de autenticación](active-directory-authentication-scenarios.md) | Un tooauthentication introducción con Azure AD |
|[Tipos de aplicaciones](active-directory-authentication-scenarios.md#application-types-and-scenarios) | Información general de escenarios de autenticación de hello compatibles con Azure AD |                                
                                                                              
## <a name="get-started"></a>Primeros pasos
Estos programas de instalación interactiva le guiará en la utilización de nuestro toosign de bibliotecas de autenticación de usuarios de Azure Active Directory.

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Aplicaciones para dispositivos móviles y de escritorio](./media/active-directory-developers-guide/NativeApp_Icon.png)<br />Aplicaciones para dispositivos móviles y de escritorio</center> | [Información general](active-directory-authentication-scenarios.md#native-application-to-web-api)<br /><br />[iOS](active-directory-devquickstarts-ios.md)<br /><br />[Android](active-directory-devquickstarts-android.md) | [.NET](active-directory-devquickstarts-dotnet.md)<br /><br />[Windows](active-directory-devquickstarts-windowsstore.md)<br /><br />[Xamarin](active-directory-devquickstarts-xamarin.md) | [Cordova](active-directory-devquickstarts-cordova.md)<br /><br />[OAuth 2.0](active-directory-protocols-oauth-code.md) |
| <center>![Web Apps](./media/active-directory-developers-guide/Web_app.png)<br />Web Apps</center> | [Información general](active-directory-authentication-scenarios.md#web-browser-to-web-application)<br /><br />[ASP.NET](active-directory-devquickstarts-webapp-dotnet.md)<br /><br />[Java](active-directory-devquickstarts-webapp-java.md) | [NodeJS](active-directory-devquickstarts-openidconnect-nodejs.md)<br /><br />[OpenID Connect 1.0](active-directory-protocols-openid-connect-code.md) |  |
| <center>![Aplicaciones de una sola página](./media/active-directory-developers-guide/SPA.png)<br />Aplicaciones de una sola página</center> | [Información general](active-directory-authentication-scenarios.md#single-page-application-spa)<br /><br />[AngularJS](active-directory-devquickstarts-angular.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) |  |  |
| <center>![API web](./media/active-directory-developers-guide/Web_API.png)<br />API web</center> | [Información general](active-directory-authentication-scenarios.md#web-application-to-web-api)<br /><br />[ASP.NET](active-directory-devquickstarts-webapi-dotnet.md)<br /><br />[NodeJS](active-directory-devquickstarts-webapi-nodejs.md) | &nbsp; |
| <center>![Service-to-service](./media/active-directory-developers-guide/Service_App.png)<br />Service-to-Service</center> | [Información general](active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)<br /><br />[.NET](active-directory-code-samples.md#server-or-daemon-application-to-web-api)<br /><br />[Credenciales del cliente de OAuth 2.0](active-directory-protocols-oauth-service-to-service.md) |  |

## <a name="guides"></a>Guías
Estos artículos le informan cómo las tareas comunes de tooperform con Azure Active Directory.

|                                                                           |  |
|---------------------------------------------------------------------------| --- |
|[Registro de aplicaciones](active-directory-integrating-applications.md)           | ¿Cómo tooregister una aplicación en Azure AD |
|[Aplicaciones multiinquilino](active-directory-devhowto-multi-tenant-overview.md)    | Cómo funcionan los toosign en cualquier producto de Microsoft en la cuenta |
|[OAuth y OpenID Connect](active-directory-protocols-openid-connect-code.md)| Cómo toosign en usuarios y llamar a las API web mediante nuestras protocolos de autenticación moderna |
|[Más guías...](active-directory-developers-guide-index.md#guides)        |     |

## <a name="reference"></a>Referencia
En estos artículos se detallan las API, los mensajes de protocolo y los términos que se usan en Azure Active Directory.

|                                                                                   | |
| ----------------------------------------------------------------------------------| --- |
| [Bibliotecas de autenticación (ADAL)](active-directory-authentication-libraries.md)   | Información general de las bibliotecas de hello & SDK proporcionado por Azure AD |
| [Ejemplos de código](active-directory-code-samples.md)                                  | Lista de todos los ejemplos de código de Azure AD |
| [Glosario](active-directory-dev-glossary.md)                                      | Terminología y definiciones de palabras que se utilizan en esta documentación |
| [Más material de referencia...](active-directory-developers-guide-index.md#reference)|     |

## <a name="help--support"></a>Ayuda y soporte técnico
Se trata de hello mejores lugares tooget ayuda con el desarrollo en Azure Active Directory.

|  |  
|---|
|[`azure-active-directory` de Stack Overflow y etiquetas `adal`](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)      |
|[Comentarios sobre Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)|
| [Pruebe Microsoft Dev Chat (gratis durante un tiempo limitado)](http://aka.ms/devchat) |

<br />

> [!NOTE]
> Si necesita toosign en Microsoft cuentas personales, puede que desee tooconsider con hello [punto de conexión de Azure AD v2.0](active-directory-appmodel-v2-overview.md).  el punto de conexión de Hello Azure AD v2.0 es unificación de Hola de cuentas personales de Microsoft y cuentas de trabajo de Microsoft (de Azure AD) en un sistema de autenticación único.
