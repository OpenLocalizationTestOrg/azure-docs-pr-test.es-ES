---
title: "bibliotecas de autenticación de v2.0 de Active Directory aaaAzure | Documentos de Microsoft"
description: "Bibliotecas de cliente compatible y bibliotecas de middleware de servidor y biblioteca relacionado, origen y vínculos de ejemplos, para el punto de conexión de hello Azure Active Directory v2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 19cec615-e51f-4141-9f8c-aaf38ff9f746
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7affdaac3a087b951d54d96fa68edde2a065172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-authentication-libraries"></a>Bibliotecas de autenticación de Azure Active Directory v2.0
el punto de conexión de Hello Azure Active Directory (Azure AD) v2.0 admite protocolos de OAuth 2.0 y OpenID Connect 1.0 estándar del sector Hola. Puede usar distintas bibliotecas de Microsoft y otras organizaciones con el punto de conexión de hello v2.0.

Al compilar una aplicación que utiliza el punto de conexión de hello v2.0, recomendamos que utilice bibliotecas escritas por expertos de dominio de protocolo que sigan una metodología de ciclo de vida de desarrollo de seguridad (SDL), como [Hola uno seguido por Microsoft] [Microsoft-SDL]. Si decide soporte toohand código para los protocolos de hello, se recomienda seguir la metodología SDL y preste especial atención toohello consideraciones de seguridad en las especificaciones de los estándares de Hola para cada protocolo.

## <a name="types-of-libraries"></a>Tipos de bibliotecas
Azure AD v2.0 funciona con dos tipos de bibliotecas:

* **Bibliotecas de cliente**. Servidores y clientes nativos usan tokens de acceso de tooget de bibliotecas de cliente para llamar a un recurso, como Microsoft Graph.
* **Bibliotecas de middleware de servidores**. Las aplicaciones web usan bibliotecas de middleware de servidor para el inicio de sesión de usuario. Las API Web usan tokens de toovalidate de bibliotecas de middleware de servidor que se envían mediante clientes nativos o en los otros servidores.

## <a name="library-support"></a>Compatibilidad con bibliotecas
Dado que puede elegir cualquier biblioteca compatible con los estándares cuando se utiliza el punto de conexión de hello v2.0, es importante tooknow donde toogo para soporte técnico. Para problemas y las solicitudes de características en el código de biblioteca, póngase en contacto con el propietario de la biblioteca de Hola. Para las solicitudes de características de implementación de protocolo del servicio de Hola y problemas, póngase en contacto con Microsoft.

Las bibliotecas se dividen en dos categorías de soporte técnico:

* **Soporte técnico de Microsoft**. Microsoft proporciona soluciones para estas bibliotecas y ha hecho las diligencias necesarias con SDL para estas bibliotecas.
* **Compatible**. Microsoft ha probado estas bibliotecas en escenarios básicos y confirmar que funcionan con el punto de conexión de hello v2.0. Microsoft no proporciona correcciones para estas bibliotecas y no ha realizado una revisión de estas bibliotecas. Problemas y las solicitudes de características deben ser el proyecto de código abierto de la biblioteca de toohello dirigida.

Para obtener una lista de bibliotecas que funcionan con el punto de conexión de hello v2.0, consulte las secciones siguientes de Hola de este artículo.


## <a name="microsoft-supported-client-libraries"></a>Bibliotecas de cliente compatibles con Microsoft

> [!IMPORTANT]
> bibliotecas de vista previa de Hello MSAL son adecuadas para su uso en un entorno de producción. Proporcionamos Hola mismo soporte de nivel de producción de estas bibliotecas como lo hacemos nuestras bibliotecas de producción actual (AAL). Durante la vista previa de Hola que realizamos cambios toohello MSAL API, formato de caché interna, y otros mecanismos de estas bibliotecas sin previo aviso, que será necesario tootake junto con correcciones o mejoras de las características. Esto puede afectar a la aplicación. Por ejemplo, un formato de caché de toohello de cambio puede afectar a los usuarios, como el requerimiento de ellos toosign de nuevo. Un cambio en la API puede requerir tooupdate su código. Cuando se proporciona Hola versión de disponibilidad General, se requerirá tooupdate toohello Disponibilidad General versión dentro de seis meses, como las aplicaciones escritas mediante una vista previa versión de biblioteca ya no funcionen.

| Plataforma | Biblioteca | Descargar | Código fuente | Muestra | Referencia
| --- | --- | --- | --- | --- | --- |
| Cliente .NET, Tienda Windows, UWP, Xamarin iOS y Android | MSAL .NET (versión preliminar) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Aplicación de escritorio](guidedsetups/active-directory-mobileanddesktopapp-windowsdesktop-intro.md) |  |
| JavaScript | MSAL.js (versión preliminar) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Aplicación de una sola página](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2) |  |
| iOS, macOS | MSAL (versión preliminar) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Aplicación para iOS](https://github.com/Azure-Samples/active-directory-msal-ios-swift) |  |
| Android | MSAL (versión preliminar) | [Hola repositorio Central](https://repo1.maven.org/maven2/com/microsoft/identity/client/msal/) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Aplicación para Android](guidedsetups/active-directory-mobileanddesktopapp-android-intro.md) | [JavaDocs](http://javadoc.io/doc/com.microsoft.identity.client/msal) |

## <a name="microsoft-supported-server-middleware-libraries"></a>Bibliotecas de middleware de servidor compatibles de Microsoft

| Plataforma | Biblioteca | Descargar | Código fuente | Muestra | Referencia
| --- | --- | --- | --- | --- | --- |
| .NET 4.x | Middleware OWIN OpenID Connect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Aplicación MVC](guidedsetups/active-directory-serversidewebapp-aspnetwebappowin-intro.md) | |
| .NET 4.x | Middleware OWIN OAuth Bearer para Azure AD |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |  | |
| .NET 4.x | Controlador JWT para .NET 4.5 | [NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/4.0.4.403061554) | [GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET Core | Middleware ASP.NET OpenID Connect |[Microsoft.AspNetCore.Authentication.OpenIdConnect (NuGet)][ServerLib-NetCore-Owin-Oidc-Lib] |[Seguridad de ASP.Net (GitHub)][ServerLib-NetCore-Owin-Oidc-Repo] |[Aplicación MVC](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2) |
| .NET Core | Middleware ASP.NET OAuth Bearer |[Microsoft.AspNetCore.Authentication.OAuth (NuGet)][ServerLib-NetCore-Owin-Oauth-Lib] |[Seguridad de ASP.Net (GitHub)][ServerLib-NetCore-Owin-Oauth-Repo] |  |
| .NET Core | Controlador JWT para .NET Core  |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Aplicación web](active-directory-v2-devquickstarts-node-web.md)| |

## <a name="compatible-client-libraries"></a>Bibliotecas de cliente compatibles
| Plataforma | Nombre de la biblioteca | Versión probada | Código fuente | Muestra |
|:---:|:---:|:---:|:---:|:---:|
| Android |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib/wiki) |0.2.1 |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib) |[Ejemplo de aplicación nativa](active-directory-v2-devquickstarts-android.md) |
| iOS |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |1.2.8 |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |[Ejemplo de aplicación nativa](active-directory-v2-devquickstarts-ios.md) |
| JavaScript |[Hello.js](https://adodson.com/hello.js/) |1.13.5 |[Hello.js](https://github.com/MrSwitch/hello.js) |[SPA](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2) |

## <a name="compatible-server-middleware-libraries"></a>Bibliotecas de middleware de servidores compatibles
| Plataforma | Nombre de la biblioteca | Versión probada | Código fuente | Muestra |
|:---:|:---:|:---:|:---:|:---:|
| Java | [Scribejava Scribe Java](https://github.com/scribejava/scribejava) | [Versión 3.2.0](https://github.com/scribejava/scribejava/releases/tag/scribejava-3.2.0) | [ScribeJava](https://github.com/scribejava/scribejava/archive/scribejava-3.2.0.zip) | |
| PHP | [Hola PHP liga oauth2-cliente](https://github.com/thephpleague/oauth2-client) | [Versión 1.4.2](https://github.com/thephpleague/oauth2-client/releases/tag/1.4.2) | [oauth2-client](https://github.com/thephpleague/oauth2-client/archive/1.4.2.zip) | |
| Python-Flask |[Matraz OAuthlib](https://github.com/lepture/flask-oauthlib) |0.9.3 |[Matraz OAuthlib](https://github.com/lepture/flask-oauthlib) |[Aplicación web](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2) |
| Ruby |[OmniAuth](https://github.com/omniauth/omniauth/wiki) |omniauth:1.3.1</br>omniauth-oauth2:1.4.0 |[OmniAuth](https://github.com/omniauth/omniauth)</br>[OmniAuth OAuth2](https://github.com/intridea/omniauth-oauth2) |  |

## <a name="related-content"></a>Contenido relacionado
Para obtener más información sobre el punto de conexión de hello Azure AD v2.0, consulte hello [información general de v2.0 del modelo de aplicaciones de Azure AD][AAD-App-Model-V2-Overview].

<!--Image references-->

<!--Reference style links -->
[AAD-App-Model-V2-Overview]: ../active-directory-appmodel-v2-overview.md
[ClientLib-NET-Lib]: http://www.nuget.org/packages/Microsoft.Identity.Client
[ClientLib-NET-Repo]: https://github.com/AzureAD/microsoft-authentication-library-for-dotnet
[ClientLib-NET-Sample]: active-directory-v2-devquickstarts-wpf.md
[ClientLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ClientLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad
[ClientLib-Node-Sample]:/
[ClientLib-Iosmac-Lib]:/
[ClientLib-Iosmac-Repo]:/
[ClientLib-Iosmac-Sample]:/
[ClientLib-Android-Lib]:/
[ClientLib-Android-Repo]:/
[ClientLib-Android-Sample]:/
[ClientLib-Js-Lib]:/
[ClientLib-Js-Repo]:/
[ClientLib-Js-Sample]:/

[Microsoft-SDL]: http://www.microsoft.com/sdl/default.aspx
[ServerLib-Net4-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/
[ServerLib-Net4-Owin-Oidc-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oidc-Sample]: active-directory-v2-devquickstarts-dotnet-web.md
[ServerLib-Net4-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OAuth/
[ServerLib-Net4-Owin-Oauth-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oauth-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-dotnet-api/
[ServerLib-Net-Jwt-Lib]: https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt
[ServerLib-Net-Jwt-Repo]: https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet
[ServerLib-Net-Jwt-Sample]:/
[ServerLib-NetCore-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/
[ServerLib-NetCore-Owin-Oidc-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oidc-Sample]: https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2
[ServerLib-NetCore-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OAuth/
[ServerLib-NetCore-Owin-Oauth-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oauth-Sample]:/
[ServerLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ServerLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad/
[ServerLib-Node-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-node-web/
