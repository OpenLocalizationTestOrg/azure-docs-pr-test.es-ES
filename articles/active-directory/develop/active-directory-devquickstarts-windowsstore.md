---
title: "aaaAzure tienda de AD Windows Introducción | Documentos de Microsoft"
description: "Cree aplicaciones de la Tienda Windows que se integren con Azure AD para el inicio de sesión y la llamada a las API protegidas por Azure AD mediante OAuth."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a>Integración de Azure AD con aplicación de la Tienda Windows
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Los proyectos de Windows Store 8.1 y de la versión anterior no son compatibles con Visual Studio 2017.  Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Si está desarrollando aplicaciones para la tienda Windows hello, Azure Active Directory (Azure AD) resulta sencilla y directa tooauthenticate los usuarios con sus cuentas de Active Directory. Mediante la integración con Azure AD, una aplicación segura puede consumir cualquier API que está protegido con Azure AD, como Hola API de Office 365 o hello Azure API web.

Tienda Windows para aplicaciones de escritorio que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory (ADAL). Hola único propósito de AAL es toomake más sencilla para los tokens de acceso de tooget de aplicación Hola. toodemonstrate lo fácil que es, este artículo muestra cómo toobuild una DirectorySearcher de la tienda Windows app que:

* Obtiene acceso para llamar a API de Azure AD Graph hello mediante el uso de hello [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Busca un directorio para usuarios con un nombre principal de usuario (UPN).
* Cerrar la sesión de los usuarios

## <a name="before-you-get-started"></a>Antes de comenzar
* Descargar hello [proyecto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), o descargar hello [ejemplo completo](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip). Cada descarga es una solución de Visual Studio 2015.
* También necesita a un inquilino de Azure AD en las que los usuarios toocreate y la aplicación hello de registro. Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).

Cuando esté listo, siga los procedimientos de hello en Hola tres secciones siguientes.

## <a name="step-1-register-hello-directorysearcher-app"></a>Paso 1: Registrar aplicación de DirectorySearcher hello
tooenable Hola aplicación tooget símbolos (tokens), primero debe tooregister en Azure AD de inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph. Este es el procedimiento:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta. A continuación, en hello **Directory** inquilinos de Active Directory de hello seleccione donde desea que la aplicación de hello tooregister, la lista.
3. Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.
5. Siga Hola indicaciones toocreate una **aplicación cliente nativa**.
  * **Nombre** describe hello toousers de aplicación.
  * **URI de redireccionamiento** es una combinación de esquema y la cadena que Azure AD usa tooreturn token respuestas. Por ahora, escriba un valor de marcador de posición (por ejemplo, **http://DirectorySearcher**). Reemplace el valor de hello más tarde.
6. Después de haber completado el registro de hello, Azure AD le asigna aplicación hello un identificador de aplicación único. Copiar valor de hello en hello **aplicación** ficha, porque lo necesitará más adelante.
7. En hello **configuración** página, seleccione **permisos necesarios**y, a continuación, seleccione **agregar**.
8. Para hello **Azure Active Directory** aplicación, seleccione **Microsoft Graph** como Hola API.
9. En **permisos delegados**, agregar hello **obtener acceso al directorio de hello como usuario con sesión iniciada hello** permiso. Al hacerlo, permite Hola Hola tooquery API Graph aplicación para los usuarios.

## <a name="step-2-install-and-configure-adal"></a>Paso 2: Instalación y configuración de ADAL
Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad. tooenable toocommunicate ADAL con Azure AD proporciona cierta información sobre el registro de una aplicación Hola.

1. Agregar toohello AAL DirectorySearcher proyecto mediante el uso de la consola de administrador de paquetes de saludo.

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. En el proyecto de DirectorySearcher hello, abra MainPage.xaml.cs.
3. Reemplace los valores de hello en hello **valores de configuración** región con valores de hello que escribió en hello portal de Azure. El código hace referencia a valores de toothese cada vez que usa AAL.
  * Hola *inquilino* es Hola dominio del inquilino de Azure AD (por ejemplo, contoso.onmicrosoft.com).
  * Hola *clientId* es Hola Id. de cliente de la aplicación hello, que se copió desde el portal de Hola.
4. Ahora debe devolución de llamada de toodiscover Hola URI para la aplicación de la tienda de Windows. Define un punto de interrupción en esta línea de hello `MainPage` método:
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. Crear solución de hello, asegurándose de que se restauran todas las referencias de paquete. Si faltan algunos paquetes, abra el Administrador de paquetes de NuGet Hola y restaurarlos.
6. Ejecutar aplicación hello y copie el valor de Hola de `redirectUri` cuando se visita el punto de interrupción de Hola. valor de Hello debe tener un aspecto similar Hola siguiente:

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. En hello **configuración** pestaña de aplicación Hola Hola portal de Azure, agregue un **RedirectUri** con hello anterior valor.  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>Paso 3: Usar AAL tooget los tokens de Azure AD
Hello principio básico detrás de AAL es que cada vez que la aplicación hello necesita un token de acceso, simplemente llama `authContext.AcquireToken(…)`, y AAL Hola rest.  

1. Inicializar la aplicación hello `AuthenticationContext`, que es la clase principal de hello de AAL. Esta acción pasa coordenadas de hello AAL necesarios toocommunicate con Azure AD y le diga cómo toocache símbolos (tokens).

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. Busque hello `Search(...)` método, que se invoca cuando los usuarios hacen clic hello **búsqueda** botón en la interfaz de usuario de la aplicación hello. Este método realiza una tooquery de toohello Azure AD Graph API de solicitud get para los usuarios cuyo UPN comienza con hello dado el término de búsqueda. Hola tooquery API Graph, incluir un token de acceso en la solicitud de hello **autorización** encabezado. Aquí es donde entra en juego AAL.

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    Cuando la aplicación hello solicita un token mediante una llamada a `AcquireTokenAsync(...)`, AAL intenta tooreturn un token sin pedir las credenciales de usuario de Hola. Si AAL determina que el usuario hello toosign en tooget un token es necesario, muestra un cuadro de diálogo de inicio de sesión, recopila las credenciales de usuario de Hola y devuelve un token después de la autenticación se realiza correctamente. Si AAL está no se puede tooreturn un token por cualquier motivo, Hola *AuthenticationResult* estado es un error.
3. Ahora es el token de acceso de tiempo toouse Hola que acaba de adquirir. También en hello `Search(...)` método, adjuntar hello toohello token solicitud de obtención de API Graph en hello **autorización** encabezado:

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. Puede usar hello `AuthenticationResult` toodisplay información acerca del usuario de hello en la aplicación hello, como un identificador de usuario de hello del objeto:

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. También puede usar ADAL toosign usuarios fuera de la aplicación hello. Cuando el usuario de hello hace clic en hello **cerrar sesión** botón, asegúrese de esa llamada siguiente Hola demasiado`AcquireTokenAsync(...)` muestra una vista de inicio de sesión. Con AAL, esta acción es tan fácil como borrar la caché de tokens de hello:

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>Pasos siguientes
Ahora tiene una aplicación de la tienda de Windows que puede autenticar a los usuarios, seguro llamar a las API mediante OAuth 2.0 web y obtener información básica acerca del usuario de hello en funcionamiento.

Si ya no ha rellenado al inquilino con usuarios, ahora es Hola tiempo toodo para.
1. Ejecutar la aplicación DirectorySearcher y, a continuación, inicie sesión con uno de los usuarios de Hola.
2. Busque otros usuarios según su UPN.
3. Cierre la aplicación hello y volver a ejecutarla. Observe cómo la sesión del usuario de hello permanece intacta.
4. Cerrar la sesión haciendo clic en la barra de toodisplay Hola inferior y, a continuación, vuelva a iniciarla como otro usuario.

AAL resulta fácil tooincorporate todas estas características comunes de identidad en la aplicación hello. Se encarga de todo el trabajo dirty Hola para usted, como la administración de memoria caché, compatibilidad con el protocolo OAuth, presentar usuario Hola con una interfaz de usuario de inicio de sesión y actualizar expirado símbolos (tokens). Necesita llamada tooknow solo una única API, `authContext.AcquireToken*(…)`.

Como referencia, descargar hello [ejemplo completado](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (sin los valores de configuración).

Ahora puede mover en escenarios de identidad tooadditional. Por ejemplo, pruebe [Protección de una API web de .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
