---
title: "Bibliotecas de autenticación de Active Directory aaaAzure | Documentos de Microsoft"
description: "Hola biblioteca de autenticación de Azure AD (AAL) permite que los desarrolladores de aplicaciones cliente tooeasily autenticar usuarios toocloud o Active Directory (AD) local y, a continuación, obtener tokens de acceso para proteger las llamadas API."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: mbaldwin
ms.assetid: 2e4fc79a-0285-40be-8c77-65edee408a22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 20fae18807ef03463ab1bc218e5f3548b5bd5717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-authentication-libraries"></a>Bibliotecas de autenticación de Azure Active Directory
tooeasily del cliente aplicación a los desarrolladores de Hello biblioteca de autenticación de Active Directory (ADAL) de Azure permite autenticar a los usuarios toocloud o Active Directory (AD) local y obtener tokens de acceso para proteger las llamadas de API. ADAL facilita la autenticación para los desarrolladores a través de características como:
 - compatibilidad para las llamadas de método asincrónico
 - una caché de tokens configurable que almacena tokens de acceso y tokens de actualización
 - actualización de tokens automática disponible cuando expira un token de acceso y un token de actualización
 - y mucho más...
 
Controlar la mayor parte de la complejidad de hello, AAL ayuda a los programadores centrarse en la lógica de negocios y proteger fácilmente los recursos, sin necesidad de ser un experto en seguridad.

ADAL está disponible en diversas plataformas.

### <a name="client-libraries"></a>Bibliotecas de cliente

| Plataforma | Biblioteca | Descargar | Código fuente | Muestra | Referencia
| --- | --- | --- | --- | --- | --- |
| Cliente .NET, Tienda Windows, UWP, Xamarin iOS y Android |MSAL para .NET (versión preliminar) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client/1.1.0-preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Aplicación de escritorio](~/articles/active-directory/develop/guidedsetups/active-directory-windesktop.md) |[Referencia](https://docs.microsoft.com/dotnet/api/?view=identityclient-1.1.0-preview) | 
| JavaScript |MSAL para JavaScript (versión preliminar) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Aplicación de una sola página](~/articles/active-directory/develop/GuidedSetups/active-directory-javascriptspa.md) | [Referencia](https://htmlpreview.github.io/?https://raw.githubusercontent.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/docs/classes/_useragentapplication_.msal.useragentapplication.html) | 
| iOS |MSAL para iOS (versión preliminar) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Aplicación para iOS](~/articles/active-directory/develop/GuidedSetups/active-directory-ios.md) | [Referencia](https://azuread.github.io/docs/objc/) |
| Android |MSAL para Android (versión preliminar) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Aplicación para Android](~/articles/active-directory/develop/GuidedSetups/active-directory-android.md) | [Referencia](http://javadoc.io/doc/com.microsoft.identity.client/msal/0.1.1) |
| Cliente .NET, Tienda Windows, UWP, Xamarin iOS y Android |ADAL .NET v3 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) | [Aplicación de escritorio](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-dotnet) |[Referencia](https://docs.microsoft.com/dotnet/api/?view=identitymodelclientsad-3.13.9) | 
| Cliente .NET, Tienda Windows, Windows Phone 8.1 |ADAL .NET v2 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.4) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/releases/tag/v2.28.4) | [Aplicación de escritorio](https://github.com/AzureADQuickStarts/NativeClient-DotNet/releases/tag/v2.X) | | 
| JavaScript |ADAL.js |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[Aplicación de una sola página](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | |
| iOS, macOS |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc) |[Aplicación para iOS](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-ios) | [Referencia](https://cocoapods.org/pods/ADAL)|
| Android |ADAL |[Hola repositorio Central](http://search.maven.org/remotecontent?filepath=com/microsoft/aad/adal/) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android) |[Aplicación para Android](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-android) | [JavaDocs](http://javadoc.io/doc/com.microsoft.aad/adal/)|
| Node.js |ADAL |[npm](https://www.npmjs.com/package/adal-node) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) | | |
| Java |ADAL4J |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[Aplicaciones web de Java](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-java) | |
| Python |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) | | |
### <a name="server-libraries"></a>Bibliotecas de servidor 

| Plataforma | Biblioteca | Descargar | Código fuente | Muestra | Referencia
| --- | --- | --- | --- | --- | --- |
| .NET |OWIN para AzureAD|[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |[Aplicación MVC](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-dotnet) | |
| .NET |OWIN para OpenIDConnect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Aplicación web](https://github.com/AzureADSamples/WebApp-OpenIDConnect-DotNet) | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [API web](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapi-nodejs)| |
| .NET |OWIN para WS-Federation |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) |[CodePlex](http://katanaproject.codeplex.com) |[Aplicación web MVC](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) | |
| .NET |Extensiones de protocolo de identidad para .NET Framework 4.5 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Protocol.Extensions) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET |Controlador JWT para .NET 4.5 |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |



## <a name="scenarios"></a>Escenarios

A continuación presentamos tres escenarios comunes en los que se puede usar ADAL para la autenticación de un cliente que accede a un recurso remoto:  

### <a name="authenticating-users-of-a-native-client-application-running-on-a-device"></a>Autenticación de los usuarios de una aplicación cliente nativa que se ejecuta en un dispositivo 

En este escenario, un desarrollador tiene una aplicación de cliente WPF, que necesita tooaccess un recurso remoto protegido con Azure AD, como una API web. Tiene una suscripción de Azure, sabe cómo tooinvoke Hola API web descendente y conoce hello Azure inquilino de AD que Hola utiliza API web. Como resultado, puede usar autenticación de ADAL toofacilitate con Azure AD, delegando por completo tooADAL de experiencia de autenticación de Hola o controlando de manera explícita las credenciales de usuario. ADAL facilita el usuario de hello tooauthenticate fácil, obtener un token de acceso y el token de actualización de Azure AD y, a continuación, usar Hola acceso toomake token solicitudes toohello web API.

Para obtener un ejemplo de código que muestra este escenario mediante la autenticación tooAzure AD, consulte [tooWeb de aplicación de WPF cliente nativa API](https://github.com/azureadsamples/nativeclient-dotnet).

### <a name="authenticating-a-confidential-client-application-running-on-a-web-server"></a>Autenticación de una aplicación cliente confidencial que se ejecuta en un servidor web

En este escenario, un desarrollador tiene una aplicación que se ejecuta en un servidor que necesita tooaccess un recurso remoto protegido con Azure AD, como una API web. Tiene una suscripción de Azure, sabe cómo tooinvoke Hola servicio descendente y conoce el inquilino hello web API de hello Azure AD utiliza. Como resultado, puede usar autenticación de ADAL toofacilitate con Azure AD controlando de manera explícita las credenciales de la aplicación hello. AAL hace fácil tooretrieve un token de Azure AD mediante la credencial del cliente de la aplicación hello y, a continuación, usar esa API web de toohello de token toomake solicitudes. AAL también controladores de administración de vigencia de Hola de hello token de acceso, almacenarlos en caché y renovándolo según sea necesario. Para obtener un ejemplo de código que muestre este escenario, vea [tooWeb de aplicación de consola de demonio API](https://github.com/AzureADSamples/Daemon-DotNet).

### <a name="authenticating-a-confidential-client-application-running-on-a-server-on-behalf-of-a-user"></a>Autenticación de una aplicación cliente confidencial que se ejecuta en un servidor web en nombre de un usuario 

En este escenario, un desarrollador tiene una aplicación que se ejecuta en un servidor que necesita tooaccess un recurso remoto protegido con Azure AD, como una API web. solicitud de Hello también necesita toobe realizada en nombre de un usuario de Azure AD. Tiene una suscripción de Azure, sabe cómo tooinvoke Hola API web descendente y conoce Hola servicio de hello del inquilino de Azure AD utiliza. Una vez usuario Hola aplicación web de toohello autenticado, aplicación hello puede obtener un código de autorización para el usuario de Hola de Azure AD. aplicación web de Hello, a continuación, puede usar ADAL tooobtain un token de acceso y el token de actualización en nombre del usuario con credenciales de cliente y código de la autorización de hello asociadas con la aplicación hello de Azure AD. Una vez que la aplicación web de hello está en posesión del token de acceso de hello, puede llamar a API web de hello hasta que expire el token de Hola. Cuando expira el token de hello, aplicación web de hello puede usar ADAL tooget un nuevo token de acceso mediante el uso de token de actualización de Hola que se recibió anteriormente. Para obtener un ejemplo de código que muestre este escenario, vea [tooWeb tooWeb API de cliente nativo API](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof).

## <a name="see-also"></a>Otras referencias

- [Hola a Guía del desarrollador de Azure Active Directory](active-directory-developers-guide.md)
- [Escenarios de autenticación para Azure Active Directory](active-directory-authentication-scenarios.md)
- [Ejemplos de código de Azure Active Directory](active-directory-code-samples.md)
