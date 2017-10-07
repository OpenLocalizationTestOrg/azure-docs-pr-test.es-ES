---
title: ".NET aaaAzure AD Introducción | Documentos de Microsoft"
description: "Cómo toobuild una aplicación de escritorio de Windows de .NET que se integra con Azure AD para inicio de sesión y llama a Azure AD había protegido con OAuth de API."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>Integración de Azure AD en una aplicación WPF de escritorio de Windows
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Si está desarrollando una aplicación de escritorio, Azure AD facilita simple y sencillo para tooauthenticate los usuarios con sus cuentas de Active Directory.  También permite que su aplicación toosecurely consumir cualquier web API protegida por Azure AD, como Hola API de Office 365 u Hola API de Azure.

Para clientes nativos de .NET que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory o AAL.  Único propósito de AAL en la vida es toomake más sencilla para los tokens de acceso de tooget de su aplicación.  toodemonstrate lo fácil es, a continuación, crearemos una aplicación de lista de tareas de .NET WPF que:

* Obtiene acceso a los tokens para llamar a la API de Azure AD Graph hello mediante Hola [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Buscar un directorio para los usuarios con un alias determinado
* Cerrar la sesión de los usuarios

aplicación toobuild Hola completa trabajo, debe:

1. Registrar la aplicación con Azure AD
2. Instalar y configurar ADAL
3. Usar AAL tooget tokens de Azure AD.

tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  También necesitará a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.  Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).

## <a name="1-register-hello-directorysearcher-application"></a>1. Registrar Hola DirectorySearcher aplicación
tooenable sus tokens de tooget aplicación, primero deberá tooregister en Azure AD de los inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta y en hello **Directory** lista, elija el inquilino de Active Directory de Hola que le gustaría tooregister la aplicación.
3. Haga clic en **más servicios** en Hola nav izquierda y elija **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y elija **Agregar**.
5. Siga las indicaciones de Hola y crear un nuevo **aplicación cliente nativa**.
  * Hola **nombre** de hello aplicación describirá los tooend-usuarios de la aplicación
  * Hola **Uri de redireccionamiento** es una combinación de esquema y la cadena que Azure AD utilizará las respuestas de símbolo (token) de tooreturn.  Escriba una aplicación de tooyour específico de valor, por ejemplo, `http://DirectorySearcher`.
6. Una vez que haya completado el registro, AAD asignará a su aplicación un identificador de aplicación único.  Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la página de aplicación Hola.
7. De hello **configuración** página, elija **permisos necesarios** y elija **agregar**. Seleccione hello **Microsoft Graph** como Hola API y agregar hello **leer datos de directorio** permiso en **permisos delegados**.  Esto le permitirá la Hola de tooquery aplicación API Graph para los usuarios.

## <a name="2-install--configure-adal"></a>2. Instalar y configurar ADAL
Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad.  Para toocommunicate capaz de toobe ADAL con Azure AD, deberá tooprovide con cierta información sobre el registro de aplicación.

* Comienza agregando toohello AAL DirectorySearcher proyecto mediante la consola de administrador de paquetes de saludo.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* En el proyecto de DirectorySearcher hello, abra `app.config`.  Reemplace los valores de hello de elementos de Hola Hola `<appSettings>` Hola de sección tooreflect valores entrada en hello Portal de Azure.  El código hará referencia a estos valores siempre que use ADAL.
  * Hola `ida:Tenant` es Hola dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com
  * Hola `ida:ClientId` es clientId hello de la aplicación copian desde el portal de Hola.
  * Hola `ida:RedirectUri` es hello que registró en el portal de Hola de dirección url de redireccionamiento.

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.    Usar Tokens ADAL tooGet de AAD
Hello principio básico detrás de AAL es que cada vez que la aplicación necesita un token de acceso, simplemente llama `authContext.AcquireTokenAsync(...)`, y AAL Hola rest.  

* Hola `DirectorySearcher` proyecto abierto `MainWindow.xaml.cs` y busque hello `MainWindow()` método.  primer paso de Hello es la aplicación de tooinitialize `AuthenticationContext` -ADAL de la clase principal.  Esto es donde pasas AAL Hola coordenadas debe toocommunicate con Azure AD y le indique cómo toocache símbolos (tokens).

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* Ahora busque hello `Search(...)` método, que se invocará cuando cliks de usuario de Hola Hola botón "Buscar" en la interfaz de usuario de la aplicación hello.  Este método realiza una tooquery de toohello Azure AD Graph API de solicitud GET para los usuarios cuyo UPN comienza con hello dado el término de búsqueda.  Pero en hello tooquery de orden API Graph, debe tooinclude un access_token Hola `Authorization` solicitud de encabezado de hello - aquí es donde entra AAL.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* Cuando la aplicación solicita un token mediante una llamada a `AcquireTokenAsync(...)`, AAL intentará tooreturn un token sin pedir las credenciales de usuario de Hola.  Si AAL determina que el usuario hello toosign en tooget un token es necesario, mostrar un cuadro de diálogo de inicio de sesión, recopilar las credenciales de usuario de Hola y devuelve un token después de autenticarse correctamente.  Si AAL está no se puede tooreturn un token por cualquier motivo, se producirá un `AdalException`.
* Tenga en cuenta que hello `AuthenticationResult` objeto contiene un `UserInfo` objeto que puede ser información de uso toocollect que necesite la aplicación.  Hola DirectorySearcher, `UserInfo` es la interfaz de la aplicación de uso toocustomize Hola con el Id. de usuario de Hola.
* Al usuario Hola hace clic en botón "Inicio de sesión salida" Hola, queremos tooensure que Hola siguiente llamada demasiado`AcquireTokenAsync(...)` le preguntará Hola usuario toosign en.  Con AAL, esto es tan fácil como borrar la caché de tokens de hello:

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* Sin embargo, si el usuario hello no haga clic en botón "Inicio de sesión salida" Hola, le interesará sesión del usuario de toomaintain Hola para hello próxima vez que ejecuten Hola DirectorySearcher.  Cuando se inicia la aplicación hello, puede comprobar la caché de tokens de AAL para un token existente y actualizar Hola interfaz de usuario según corresponda.  Hola `CheckForCachedToken()` método, realizar otra llamada demasiado`AcquireTokenAsync(...)`, pero esta vez pasando hello `PromptBehavior.Never` parámetro.  `PromptBehavior.Never`le indicará AAL que no debe pedirse Hola usuario para iniciar sesión, y AAL debe en su lugar producirá una excepción si resulta que no se puede tooreturn un token.

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

¡Enhorabuena! Ahora tiene una aplicación .NET WPF que tiene Hola capacidad tooauthenticate usuarios y en funcionamiento, segura llamar a API Web mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola.  Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios.  Ejecute la aplicación DirectorySearcher e inicie sesión con uno de esos usuarios.  Busque otros usuarios según su UPN.  Cierre la aplicación hello y volver a ejecutarlo.  Observe cómo la sesión del usuario de hello permanece intacta.  Cierre la sesión y vuelva a iniciarla como otro usuario.

AAL resulta fácil tooincorporate todas estas características de identidad comunes en la aplicación.  Se encarga de todo el trabajo dirty Hola para usted: administración de la caché, compatibilidad con el protocolo OAuth, presentaciones usuario Hola con un inicio de sesión de interfaz de usuario, actualizar tokens caducados y mucho más.  Todo lo que realmente necesita tooknow es una sola llamada API, `authContext.AcquireTokenAsync(...)`.

Como referencia, se proporciona el ejemplo de Hola finalizado (sin los valores de configuración) [aquí](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Ahora puede mover en escenarios de tooadditional.  Puede que desee tootry:

[Protección de una API Web .NET con Azure AD &gt;&gt;](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

