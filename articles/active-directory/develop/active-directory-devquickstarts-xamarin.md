---
title: "aaaAzure AD Xamarin Introducción | Documentos de Microsoft"
description: "Cree aplicaciones de Xamarin que se integren con Azure AD para el inicio de sesión y la llamada a las API protegidas por Azure AD mediante OAuth."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a>Integración de Azure AD con aplicaciones de Xamarin
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Con Xamarin, puede escribir aplicaciones móviles en C# que se pueden ejecutar en iOS, Android y Windows (dispositivos móviles y PC). Si va a compilar una aplicación con Xamarin, Azure Active Directory (Azure AD) hace tooauthenticate simple a los usuarios con sus cuentas de Azure AD. aplicación Hello también segura puede consumir cualquier API web protegida por Azure AD, como la API de Office 365 Hola o hello API de Azure.

Para las aplicaciones de Xamarin que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory (ADAL). Hola único propósito de AAL es toomake más sencilla para los tokens de acceso de tooget de aplicaciones. toodemonstrate lo fácil es, este artículo se muestra cómo toobuild DirectorySearcher aplicaciones que:

* Se ejecute en iOS, Android, Escritorio de Windows, Windows Phone y Tienda Windows.
* Usar una sola clase portable (PCL) de la biblioteca tooauthenticate usuarios y obtener tokens para hello Azure AD Graph API.
* Busque un directorio para los usuarios con un UPN determinado.

## <a name="before-you-get-started"></a>Antes de comenzar
* Descargar hello [proyecto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), o descargar hello [ejemplo completo](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip). Cada descarga es una solución de Visual Studio 2013.
* También necesita a un inquilino de Azure AD en las que los usuarios toocreate y la aplicación hello de registro. Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).

Cuando esté listo, siga los procedimientos de hello en Hola cuatro secciones siguientes.

## <a name="step-1-set-up-your-xamarin-development-environment"></a>Paso 1: Configuración del entorno de desarrollo de Xamarin
Como este tutorial incluye proyectos de iOS, Android y Windows, necesitará tanto Visual Studio como Xamarin. entorno necesarias toocreate hello, proceso de hello completa en [establecer una copia de seguridad e instale Visual Studio y Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) en MSDN. instrucciones de Hello incluyen material que puede revisar toolearn más información sobre Xamarin mientras está esperando Hola instalaciones toobe completado.

Después de haber completado el programa de instalación de hello, abra la solución de hello en Visual Studio. Encontrará seis proyectos: cinco proyectos específicos de la plataforma y una PLC, DirectorySearcher.cs, que se compartirá entre todas las plataformas.

## <a name="step-2-register-hello-directorysearcher-app"></a>Paso 2: Registrar aplicación de DirectorySearcher hello
tooenable Hola aplicación tooget símbolos (tokens), primero debe tooregister en Azure AD de inquilinos y otórguele Hola de permiso tooaccess API de Azure AD Graph. Este es el procedimiento:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta. A continuación, en hello **Directory** inquilinos de Active Directory de hello seleccione donde desea que la aplicación de hello tooregister, la lista.
3. Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.
5. toocreate un nuevo **aplicación cliente nativa**, siga las indicaciones de Hola.
  * **Nombre** describe hello toousers de aplicación.
  * **URI de redireccionamiento** es una combinación de esquema y la cadena que Azure AD usa tooreturn token respuestas. Escriba un valor (por ejemplo, http://DirectorySearcher).
6. Una vez completado el registro, Azure AD le asigna aplicación hello un identificador de aplicación único. Copiar valor de Hola de hello **aplicación** ficha, porque lo necesitará más adelante.
7. En hello **configuración** página, seleccione **permisos necesarios**y, a continuación, seleccione **agregar**.
8. Seleccione **Microsoft Graph** como Hola API. En **permisos delegados**, agregar hello **leer datos de directorio** permiso.  
Esta acción habilita Hola Hola tooquery API Graph aplicación para los usuarios.

## <a name="step-3-install-and-configure-adal"></a>Paso 3: Instalación y configuración de ADAL
Ahora que tiene una aplicación en Azure AD, puede instalar ADAL y escribir el código relacionado con la identidad. tooenable toocommunicate ADAL con Azure AD proporciona cierta información sobre el registro de una aplicación Hola.

1. Agregar toohello AAL DirectorySearcher proyecto mediante el uso de la consola de administrador de paquetes de saludo.

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    Tenga en cuenta que se han agregado dos referencias de biblioteca de proyecto tooeach: Hola PCL parte de AAL y una parte específica de la plataforma.
2. En el proyecto DirectorySearcherLib de hello, abra DirectorySearcher.cs.
3. Reemplazar valores de miembro de clase de hello con valores de hello que escribió en hello portal de Azure. El código hace referencia a valores de toothese cada vez que usa AAL.

  * Hola *inquilino* es Hola dominio del inquilino de Azure AD (por ejemplo, contoso.onmicrosoft.com).
  * Hola *clientId* es Hola Id. de cliente de la aplicación hello, que se copió desde el portal de Hola.
  * Hola *returnUri* es Hola redirección URI especificado en el portal de hello (por ejemplo, http://DirectorySearcher).

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a>Paso 4: Usar AAL tooget los tokens de Azure AD
Casi todo de lógica de autenticación de la aplicación hello se encuentra en `DirectorySearcher.SearchByAlias(...)`. Todo lo que es necesario en los proyectos específicos de la plataforma de hello es toopass un toohello parámetro contextual `DirectorySearcher` PCL.

1. Abra DirectorySearcher.cs y, a continuación, agregue un nuevo toohello parámetro `SearchByAlias(...)` método. `IPlatformParameters`es que la autenticación de ADAL necesidades tooperform Hola de objetos de parámetro contextual hello que encapsula Hola específica de la plataforma.

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. Inicializar `AuthenticationContext`, que es la clase principal de hello de AAL.  
Este Hola AAL de fases de acción coordina necesidades toocommunicate con Azure AD.
3. Llame a `AcquireTokenAsync(...)`, que acepta hello `IPlatformParameters` objeto e invoca el flujo de autenticación de Hola que sea necesario tooreturn una aplicación toohello símbolo (token).

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    `AcquireTokenAsync(...)`primer intentos tooreturn un token para hello requerido recurso (Hola API Graph en este caso) sin preguntar tooenter a los usuarios sus credenciales (mediante el almacenamiento en caché o actualizar tokens anteriores). Según sea necesario, muestra a los usuarios hello Azure AD inicio de sesión página antes de adquirir el token solicitado Hola.
4. Asociar la solicitud de API Graph de toohello token de acceso de Hola Hola **autorización** encabezado:

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

Eso es todo para hello `DirectorySearcher` código relacionadas con la identidad de hello y PCL la aplicación. Todo lo que queda es hello toocall `SearchByAlias(...)` método en las vistas de cada plataforma y, en caso necesario, tooadd código para controlar correctamente Hola del ciclo de vida de la interfaz de usuario.

### <a name="android"></a>Android
1. En MainActivity.cs, agregue una llamada demasiado`SearchByAlias(...)` botón Hola de controlador de clic:

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. Invalidar hello `OnActivityResult` tooforward de método de ciclo de vida cualquier autenticación redirige el método adecuado de toohello atrás. ADAL proporciona un método auxiliar para esto en Android:

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a>Escritorio de Windows
En MainWindow.xaml.cs, realizar una llamada demasiado`SearchByAlias(...)` pasando un `WindowInteropHelper` en desktop hello `PlatformParameters` objeto:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a>iOS
En DirSearchClient_iOSViewController.cs, Hola iOS `PlatformParameters` objeto toma un controlador de vista de toohello de referencia:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a>Windows Universal
En universales de Windows, abra MainPage.xaml.cs y, a continuación, implementar hello `Search` método. Este método usa un método auxiliar en un proyecto compartido de tooupdate interfaz de usuario según sea necesario.

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a>Pasos siguientes
Ahora dispone de una aplicación de Xamarin que funciona que puede autenticar a los usuarios y llamar a API web de forma segura mediante OAuth 2.0 en cinco plataformas diferentes.

Si ya no ha rellenado al inquilino con usuarios, ahora es Hola tiempo toodo para.

1. Ejecutar la aplicación DirectorySearcher y, a continuación, inicie sesión con uno de los usuarios de Hola.
2. Busque otros usuarios según su UPN.

ADAL facilita la fácil tooincorporate características de identidad comunes en la aplicación hello. Se encarga de todo el trabajo dirty Hola para usted, como la administración de memoria caché, compatibilidad con el protocolo OAuth, presentar usuario Hola con una interfaz de usuario de inicio de sesión y actualizar expirado símbolos (tokens). Necesita llamada tooknow solo una única API, `authContext.AcquireToken*(…)`.

Como referencia, descargar hello [ejemplo completado](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (sin los valores de configuración).

Ahora puede mover en escenarios de identidad tooadditional. Por ejemplo, pruebe [Protección de una API web de .NET con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
