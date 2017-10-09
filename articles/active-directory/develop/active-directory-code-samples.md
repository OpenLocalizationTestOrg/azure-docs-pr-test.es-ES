---
title: "Ejemplos de código de Active Directory aaaAzure | Documentos de Microsoft"
description: "Un índice de ejemplos de código de Azure Active Directory, organizados por escenario."
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Ejemplos de código de Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Puede usar Microsoft Azure Active Directory (Azure AD) tooadd autenticación y autorización tooyour aplicaciones web y las API web. En esta sección se vincula toosamples que le muestran cómo se hizo y fragmentos de código que puede usar en sus aplicaciones. En la página de ejemplo de código de hello, encontrará lectura detallada-me temas que ayudan a los requisitos, la instalación y configuración. Y código de hello está comentada toohelp entender las secciones críticas de Hola.

escenario básico de hello toounderstand para cada tipo de ejemplo, consulte escenarios de autenticación para Azure AD.

Contribuir tooour ejemplos en GitHub: [documentación y ejemplos de Microsoft Azure Active Directory](https://github.com/Azure-Samples?page=3&query=active-directory).

## <a name="web-browser-tooweb-application"></a>Explorador de Web tooWeb aplicación
Estos ejemplos muestran cómo una aplicación web que dirige toowrite Hola toosign de explorador del usuario en tooAzure AD.

| Lenguaje/plataforma | Muestra | Description |
| --- | --- | --- |
| C#/.NET |[WebApp-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Usar OpenID Connect (software intermedio ASP.Net OpenID Connect OWIN) tooauthenticate a los usuarios de un inquilino de Azure AD. |
| C#/.NET |[WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Aplicación de web .NET MVC de varios inquilinos que usa OpenID Connect (software intermedio ASP.Net OpenID Connect OWIN) tooauthenticate a los usuarios de varios inquilinos de Azure AD. |
| C#/.NET |[WebApp-WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |Utilice usuarios de tooauthenticate de WS-Federation (software intermedio ASP.Net WS-Federation OWIN) de un inquilino de Azure AD. |

## <a name="single-page-application-spa"></a>Aplicación de una sola página (SPA)
Este ejemplo muestra cómo toowrite una aplicación Web protegida con Azure AD.  

| Lenguaje/plataforma | Muestra | Description |
| --- | --- | --- |
| JavaScript, C#/.NET |[SinglePageApp-DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |Usar ADAL para JavaScript y Azure AD aplicación única página toosecure una basada en AngularJS implementada con un fondo de la API web ASP.NET. |

## <a name="native-application-tooweb-api"></a>TooWeb nativo de aplicación API
Estos ejemplos de código muestran cómo las aplicaciones de cliente nativo de toobuild que llaman a las API web que están protegidas por Azure AD. Emplean la [Biblioteca de autenticación de Azure AD (ADAL)](active-directory-authentication-libraries.md) y [OAuth 2.0 en Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Lenguaje/plataforma | Muestra | Description |
| --- | --- | --- |
| Javascript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Usar el complemento ADAL de Hola para Apache Cordova toobuild una aplicación de Apache Cordova que llama a una API web y usa Azure AD para la autenticación. |
| C#/.NET |[NativeClient-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Una aplicación .NET WPF que llama a una API web que está protegida mediante Azure AD. |
| C#/.NET |[NativeClient-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Una aplicación de la Tienda Windows que llama a una API web que está protegida con Azure AD. |
| C#/.NET |[NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Una aplicación de la Tienda Windows que llama a una API web multiempresa que está protegida con Azure AD. |
| C#/.NET |[WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |Una aplicación cliente nativa que llama a una API web, que obtiene un token tooact en nombre de usuario original de hello y, a continuación, usa Hola token toocall otra API web. |
| C#/.NET |[NativeClient-WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Una aplicación de la Tienda Windows para Windows Phone 8.1 que llama a una API web que está protegida por Azure AD. |
| ObjC |[NativeClient-iOS](https://github.com/Azure-Samples/active-directory-ios) |Una aplicación iOS que llama a una API web que requiere Azure AD para la autenticación. |
| C#/.NET |[WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |Una aplicación cliente nativa que incluye lógica tooprocess un token JWT en una API web, en lugar de usar el middleware de OWIN. |
| C#/Xamarin |[NativeClient-Xamarin-Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |Un Xamarin enlace toohello nativo AD Azure Authentication Library (AAL) para Hola biblioteca Android. |
| C#/Xamarin |[NativeClient-Xamarin-iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Un toohello de enlace Xamarin native AD Azure Authentication Library (AAL) para iOS. |
| C#/Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Un proyecto Xamarin que se dirige a cinco plataformas y llama a una API web que está protegida por Azure AD. |
| C#/.NET |[NativeClient-Headless-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |Una aplicación nativa que realiza autenticación no interactiva y llamadas a una API web que está protegida por Azure AD. |

## <a name="web-application-tooweb-api"></a>TooWeb de aplicación Web API
Estos ejemplos de código muestran cómo usar [OAuth 2.0 en Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) toobuild aplicaciones de web que llaman a las API web que están protegidas por Azure AD.

| Lenguaje/plataforma | Muestra | Description |
| --- | --- | --- |
| C#/.NET |[WebApp-WebAPI-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Llamar a una API web con hello firmado en permisos de usuario. |
| C#/.NET |[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Llamar a una API web con permisos de la aplicación hello. |
| C#/.NET |[WebApp-WebAPI-OAuth2-UserIdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |Agrega autorización con [OAuth 2.0 en Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan las aplicaciones web existentes por lo que puede llamar a una API web. |
| JavaScript |[WebAPI-Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |Configura un servicio API de REST que se integra con Azure AD para la protección de API. Incluye un servidor Node.js con una Web API. |
| C#/.NET |[WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |Aplicación que usa OpenID Connect (software intermedio ASP.Net OpenID Connect OWIN) tooauthenticate a los usuarios de un inquilino de Azure AD de web de MVC de varios inquilinos. Usa un hello tooinvoke de código de autorización API Graph. |

## <a name="server-or-daemon-application-tooweb-api"></a>Aplicación de servidor o demonio tooWeb API
Estos ejemplos de código muestran cómo toobuild un demonio o una aplicación de servidor que obtiene los recursos de una API web mediante [biblioteca de autenticación de Azure AD (AAL)](active-directory-authentication-libraries.md) y [OAuth 2.0 en Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Lenguaje/plataforma | Muestra | Description |
| --- | --- | --- |
| C#/.NET |[Daemon-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |Una aplicación de consola llama a una API web. la credencial del cliente Hello es una contraseña. |
| C#/.NET |[Daemon-CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |Una aplicación de consola que llama a una API web. la credencial del cliente Hello es un certificado. |

## <a name="calling-azure-ad-graph-api"></a>Llamada a una API Graph de Azure AD
Estos ejemplos de código se muestra cómo las aplicaciones de toobuild que llamen Hola datos de directorio de Azure AD Graph API tooread y escritura.

| Lenguaje/plataforma | Muestra | Description |
| --- | --- | --- |
| Java |[WebApp-GraphAPI-Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Una aplicación web que usa la API Graph de hello tooaccess datos de directorio de Azure AD. |
| PHP |[WebApp-GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Una aplicación web que usa la API Graph de hello tooaccess datos de directorio de Azure AD. |
| C#/.NET |[WebApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Una aplicación web que usa la API Graph de hello tooaccess datos de directorio de Azure AD. |
| C#/.NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |Esta aplicación de consola muestra comunes de lectura y escritura llamadas toohello API Graph y cómo tooexecute usuario asignación de licencia y actualice la foto en miniatura y los vínculos de un usuario. |
| C#/.NET |[ConsoleApp-GraphAPI-DiffQuery-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Una aplicación de consola que usa la consulta diferencial de hello en hello API Graph tooget periódica cambia toouser objetos en un inquilino de Azure AD. |
| C#/.NET |[WebApp-GraphAPI-DirectoryExtensions-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |Una aplicación de MVC usa API Graph consultas toogenerate un organigrama empresa simple. |
| PHP |[WebApp-GraphAPI-DirectoryExtensions-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Una aplicación PHP que llama Hola API Graph tooregister una extensión y, a continuación, lee, actualiza y elimina los valores de atributo de extensión de Hola. |

## <a name="authorization"></a>Autorización
Estos muestran ejemplos de código cómo toouse Azure AD para la autorización.

| Lenguaje/plataforma | Muestra | Description |
| --- | --- | --- |
| C#/.NET |[WebApp-GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Realiza el control de acceso basado en roles (RBAC) mediante notificaciones de grupo de Azure Active Directory en una aplicación que está integrada con Azure AD. |
| C#/.NET |[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Realiza el control de acceso basado en roles (RBAC) mediante roles de aplicación de Azure Active Directory en una aplicación que está integrada con Azure AD. |

## <a name="legacy-walkthroughs"></a>Tutoriales heredados
Estos tutoriales usan tecnología algo más antigua, pero también podrían ser de interés.

| Lenguaje/plataforma | Muestra | Description |
| --- | --- | --- |
| C#/.NET |[Autorización basada en roles y basada en ACL en una aplicación de Microsoft Azure AD](http://go.microsoft.com/fwlink/?LinkId=331694) |Realiza la autorización basada en roles (RBAC) y la autorización basada en ACL en una aplicación que se integra con Azure AD. |
| C#/.NET |[AAL, servicio de tooREST de aplicación de tienda Windows, autenticación](http://go.microsoft.com/fwlink/?LinkId=330605) |Use [biblioteca de autenticación de Azure AD (AAL)](active-directory-authentication-libraries.md) (anteriormente AAL) para la aplicación de Windows Store Beta tooadd usuario autenticación capacidades tooa tienda Windows. |
| C#/.NET |[Autenticación de ADAL, servicio de tooREST aplicación nativa, con AAD mediante el cuadro de diálogo de explorador](http://go.microsoft.com/fwlink/?LinkId=259814) |Use [biblioteca de autenticación de Azure AD (AAL)](active-directory-authentication-libraries.md) cliente WPF de tooa de las capacidades de autenticación de tooadd usuario. |
| C#/.NET |[AAL, servicio de tooREST aplicación nativa, la autenticación con ACS mediante el cuadro de diálogo de explorador](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |Use [biblioteca de autenticación de Azure AD (AAL)](active-directory-authentication-libraries.md) y [Access Control Service 2.0 (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) cliente WPF de tooa de las capacidades de autenticación de tooadd usuario. |
| C#/.NET |[AAL - tooServer autenticación de servidor](http://go.microsoft.com/fwlink/?LinkId=259816) |Use [biblioteca de autenticación de Azure AD (AAL)](active-directory-authentication-libraries.md) toosecure llamadas al servicio de un proceso de lado servidor tooan servicio REST de API de Web MVC4. |
| C#/.NET |[Agregar el inicio de sesión tooYour Web aplicaciones con Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Configurar un .NET aplicación tooperform web inicio de sesión único en su directorio empresarial de Azure AD. |
| C#/.NET |[Desarrollo de aplicaciones web multiempresa con Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Uso de Azure AD tooadd toohello single sign-on y capacidades de acceso de directorio de una toowork de aplicación de .NET en varias organizaciones. |
| Java |[Aplicación de ejemplo de Java para la API Graph de Azure AD](http://go.microsoft.com/fwlink/?LinkId=263969) |Usar datos de directorio tooaccess Hola de API Graph de Azure AD. |
| PHP |[Aplicación de ejemplo de PHP para la API Graph de Azure AD](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Usar datos de directorio tooaccess Hola de API Graph de Azure AD. |
| C#/.NET |[Aplicación de ejemplo para la API Graph de Azure AD](http://go.microsoft.com/fwlink/?LinkID=262648) |Usar datos de directorio tooaccess Hola de API Graph de Azure AD. |
| C#/.NET |[Aplicación de ejemplo para consulta diferencial de Azure AD Graph](http://go.microsoft.com/fwlink/?LinkId=275398) |Usar consulta diferencial Hola Hola API Graph tooget cambios periódicos toouser objetos en un inquilino de Azure AD. |
| C#/.NET |[Aplicación de ejemplo para integración de aplicaciones multiempresa en la nube con Azure AD](http://go.microsoft.com/fwlink/?LinkId=275397) |Integra una aplicación mutiempresa en Azure AD. |
| C#/.NET |[Protección de una aplicación de la Tienda Windows y un servicio web REST mediante Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Crear un recurso de API web simple y una aplicación de cliente de Windows Store mediante Azure AD y Hola [biblioteca de autenticación de Azure AD (AAL)](active-directory-authentication-libraries.md). |
| C#/.NET |[Uso de tooQuery de API Graph hello Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Configurar un hello toouse de aplicación de Microsoft .NET datos de Azure AD Graph API tooaccess desde un directorio de inquilino de Azure AD. |

## <a name="see-also"></a>Otras referencias
##### <a name="other-resources"></a>Otros recursos
[Guía del desarrollador de Azure Active Directory](active-directory-developers-guide.md)

[Conceptos y referencia de la API de Azure AD Graph](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Biblioteca auxiliar de la API Graph de Azure AD](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
