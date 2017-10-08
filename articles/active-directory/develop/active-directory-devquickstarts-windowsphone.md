---
title: "aaaAzure de Windows Phone AD Introducción | Documentos de Microsoft"
description: "Cómo toobuild una aplicación de Windows Phone que se integra con Azure AD para inicio de sesión y llama a Azure AD había protegido con OAuth de API."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>Integración de Azure AD con una aplicación de Windows Phone
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Los proyectos de Windows Phone 8.1 y de la versión anterior no son compatibles con Visual Studio 2017.  Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Si está desarrollando una aplicación de Windows Phone 8.1, Azure AD facilita simple y sencillo para tooauthenticate los usuarios con sus cuentas de Active Directory.  También permite que su aplicación toosecurely consumir cualquier web API protegida por Azure AD, como Hola API de Office 365 u Hola API de Azure.

> [!NOTE]
> Este ejemplo de código usa ADAL v2.0.  Para la tecnología más reciente de hello, puede que desee tooinstead try nuestro [Tutorial Universal de Windows mediante AAL v3.0](active-directory-devquickstarts-windowsstore.md).  Si realmente está creando una aplicación para Windows Phone 8.1, éste es el lugar de derecho de Hola.  AAL v2.0 sigue siendo totalmente compatible y está hello forma recomendada de desarrollo de aplicaciones de agianst Windows Phone 8.1 con Azure AD.
> 
> 

Para clientes nativos de .NET que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory o AAL.  Único propósito de AAL en la vida es toomake más sencilla para los tokens de acceso de tooget de su aplicación.  toodemonstrate lo fácil es, a continuación, crearemos una aplicación de Windows Phone 8.1 "directorio buscador" que:

* Obtiene acceso a los tokens para llamar a la API de Azure AD Graph hello mediante Hola [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Busque un directorio para los usuarios con un UPN determinado.
* Cerrar la sesión de los usuarios

aplicación toobuild Hola completa trabajo, debe:

1. Registrar la aplicación con Azure AD
2. Instalar y configurar ADAL
3. Usar AAL tooget tokens de Azure AD.

tooget iniciado, [descargar un proyecto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Cualquiera de los dos es una solución de Visual Studio 2013.  También necesitará a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.  Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).

## <a name="1-register-hello-directory-searcher-application"></a>1. Registrar Hola aplicación buscador de directorio
tooenable sus tokens de tooget aplicación, primero deberá tooregister en Azure AD de los inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta y en hello **Directory** lista, elija el inquilino de Active Directory de Hola que le gustaría tooregister la aplicación.
3. Haga clic en **más servicios** en Hola nav izquierda y elija **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y elija **Agregar**.
5. Siga las indicaciones de Hola y crear un nuevo **aplicación cliente nativa**.
  * Hola **nombre** de hello aplicación describirá los tooend-usuarios de la aplicación
  * Hola **Uri de redireccionamiento** es una combinación de esquema y la cadena que Azure AD utilizará las respuestas de símbolo (token) de tooreturn.  Escriba un valor de marcador de posición por ahora, por ejemplo, `http://DirectorySearcher`.  Reemplazaremos este valor más adelante.
6. Una vez que haya completado el registro, AAD asignará a su aplicación un identificador de aplicación único.  Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la pestaña de la aplicación hello.
7. De hello **configuración** página, elija **permisos necesarios** y elija **agregar**. Seleccione hello **Microsoft Graph** como Hola API y agregar hello **leer datos de directorio** permiso en **permisos delegados**.  Esto le permitirá la Hola de tooquery aplicación API Graph para los usuarios.

## <a name="2-install--configure-adal"></a>2. Instalar y configurar ADAL
Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.  Para toocommunicate capaz de toobe ADAL con Azure AD, deberá tooprovide con cierta información sobre el registro de aplicación.

* Comienza agregando toohello AAL DirectorySearcher proyecto mediante la consola de administrador de paquetes de saludo.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* En el proyecto de DirectorySearcher hello, abra `MainPage.xaml.cs`.  Reemplace los valores de hello en hello `Config Values` Hola de región tooreflect valores entrada en hello Portal de Azure.  El código hará referencia a estos valores siempre que use ADAL.
  * Hola `tenant` es Hola dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com
  * Hola `clientId` es clientId hello de la aplicación copian desde el portal de Hola.
* Ahora debe uri de devolución de llamada de hello toodiscover para la aplicación de Windows Phone.  Define un punto de interrupción en esta línea de hello `MainPage` método:

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* Ejecutar aplicación hello y reserva Copiar valor de Hola de `redirectUri` cuando se visita el punto de interrupción de Hola.  Debe tener un aspecto similar al siguiente.

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* En hello **configurar** pestaña de la aplicación Hola Portal de administración de Azure, reemplace el valor de Hola de hello **RedirectUri** con este valor.  

## <a name="3-use-adal-tooget-tokens-from-aad"></a>3. Usar Tokens ADAL tooGet de AAD
Hello principio básico detrás de AAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama `authContext.AcquireToken(…)`, y AAL Hola rest.  

* primer paso de Hello es la aplicación de tooinitialize `AuthenticationContext` -ADAL de la clase principal.  Esto es donde pasas AAL Hola coordenadas debe toocommunicate con Azure AD y le indique cómo toocache símbolos (tokens).

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* Ahora busque hello `Search(...)` método, que se invocará cuando cliks de usuario de Hola Hola botón "Buscar" en la interfaz de usuario de la aplicación hello.  Este método realiza una tooquery de toohello Azure AD Graph API de solicitud GET para los usuarios cuyo UPN comienza con hello dado el término de búsqueda.  Pero en hello tooquery de orden API Graph, debe tooinclude un access_token Hola `Authorization` solicitud de encabezado de hello - aquí es donde entra AAL.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* Si es necesaria la autenticación interactiva, AAL usará Broker de autenticación de Web de Windows Phone (WAB) y [modelo de continuación](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD iniciar sesión en la página.  Cuando Hola usuario inicia sesión, la aplicación debe toopass resultados de AAL hello de interacción de WAB Hola.  Esto es tan sencillo como implementar hello `ContinueWebAuthentication` interfaz:

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* Ahora es Hola de tiempo toouse `AuthenticationResult` que AAL devuelve tooyour aplicación.  Hola `QueryGraph(...)` devolución de llamada, adjuntar access_token Hola adquirió toohello GET solicitud en el encabezado de autorización de hello:

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* También puede usar hello `AuthenticationResult` toodisplay información acerca del usuario de hello en la aplicación del objeto. Hola  `QueryGraph(...)` /método siguiente, Id. del usuario de uso Hola resultado tooshow hello en la página de hello:

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* Por último, puede usar ADAL toosign Hola usuario fuera de la aplicación.  Al usuario Hola hace clic en botón "Inicio de sesión salida" Hola, queremos tooensure que Hola siguiente llamada demasiado`AcquireTokenSilentAsync(...)` se producirá un error.  Con AAL, esto es tan fácil como borrar la caché de tokens de hello:

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

¡Enhorabuena! Ahora tiene una aplicación de Windows Phone que tiene Hola capacidad tooauthenticate usuarios en funcionamiento, segura llamar a API Web mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola.  Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios.  Ejecute la aplicación DirectorySearcher e inicie sesión con uno de esos usuarios.  Busque otros usuarios según su UPN.  Cierre la aplicación hello y volver a ejecutarlo.  Observe cómo la sesión del usuario de hello permanece intacta.  Cierre la sesión y vuelva a iniciarla como otro usuario.

AAL resulta fácil tooincorporate todas estas características de identidad comunes en la aplicación.  Se encarga de todo el trabajo dirty Hola para usted: administración de la caché, compatibilidad con el protocolo OAuth, presentaciones usuario Hola con un inicio de sesión de interfaz de usuario, actualizar tokens caducados y mucho más.  Todo lo que realmente necesita tooknow es una sola llamada API, `authContext.AcquireToken*(…)`.

Como referencia, se proporciona el ejemplo de Hola finalizado (sin los valores de configuración) [aquí](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Ahora puede mover en escenarios de identidad tooadditional.  Puede que desee tootry:

[Protección de una API Web .NET con Azure AD &gt;&gt;](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

