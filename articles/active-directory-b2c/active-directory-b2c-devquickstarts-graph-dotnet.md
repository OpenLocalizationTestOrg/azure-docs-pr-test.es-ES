---
title: 'Azure B2C Directory Active: Hola de uso API Graph | Documentos de Microsoft'
description: "¿Cómo toocall Hola API Graph para un inquilino B2C mediante un proceso de Hola de tooautomate de identidad de aplicación."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a>B2C de Azure AD: Usar hello API Graph
Inquilinos de Azure Active Directory (Azure AD) B2C suelen toobe muy grande. Esto significa que muchas tareas comunes de administración de inquilinos necesitan toobe realizar mediante programación. Un ejemplo importante es la administración de usuarios. Tendrá que toomigrate un inquilino de B2C de tooa de almacén de usuario existente. Puede desea toohost registro de usuario en su propia página y crear cuentas de usuario en el directorio de Azure AD B2C entre bastidores de Hola. Estos tipos de tareas requieren Hola capacidad toocreate, lectura, actualización y eliminar cuentas de usuario. Puede realizar estas tareas mediante el uso de API de Azure AD Graph Hola.

Para los inquilinos B2C, hay dos modos principales de la comunicación con hello API Graph.

* Para las tareas interactivas, ejecutar una vez, debe actuar como una cuenta de administrador de inquilinos de hello B2C al realizar tareas de Hola. Este modo requiere un toosign Administrador con las credenciales antes de que un administrador puede llevar a cabo cualquier toohello llamadas API Graph.
* Para las tareas automatizadas, continuadas, debe usar algún tipo de cuenta de servicio que proporciona con las tareas de administración de tooperform de hello privilegios necesarios. En Azure AD, puede hacerlo mediante el registro de una aplicación y autenticar tooAzure AD. Esto se realiza mediante un **Id. de aplicación** que usa hello [concesión las credenciales del cliente de OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api). En este caso, aplicación hello actúa por sí misma, no como un usuario, toocall Hola API Graph.

En este artículo, analizaremos cómo tooperform Hola caso de uso automatizada. toodemonstrate, vamos a crear un .NET 4.5 `B2CGraphClient` que realiza el usuario crear, leer, actualizar y eliminar operaciones (CRUD). cliente de Hello tendrá una interfaz de línea de comandos de Windows (CLI) que permite tooinvoke diversos métodos. Sin embargo, el código de hello se escribe toobehave de forma no interactiva y automatizada.

## <a name="get-an-azure-ad-b2c-tenant"></a>Obtención de un inquilino de Azure AD B2C
Para poder crear aplicaciones o los usuarios o interactuar con Azure AD en absoluto, necesitará un inquilino de Azure AD B2C y una cuenta de administrador global de inquilino de Hola. Si aún no tiene ningún inquilino, [comience con la introducción a Azure AD B2C](active-directory-b2c-get-started.md).

## <a name="register-your-application-in-your-tenant"></a>Registro de la aplicación en el inquilino
Una vez que un inquilino B2C, necesita tooregister la aplicación a través de hello [Portal de Azure](https://portal.azure.com).

> [!IMPORTANT]
> toouse Hola API de Graph con su inquilino B2C, deberá tooregister una aplicación dedicada mediante el uso de hello genérico *registros de aplicaciones* hoja en el Portal de Azure, hello **no** Azure AD B2C  *Aplicaciones* hoja. No se puede reutilizar Hola ya existente B2C aplicaciones que se ha registrado en Azure AD B2C hello *aplicaciones* hoja.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD B2C seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el panel de navegación izquierdo de hello, elija **más servicios**, haga clic en **registros de aplicaciones**y haga clic en **agregar**.
4. Siga las indicaciones de Hola y cree una nueva aplicación. 
    1. Seleccione **aplicación Web / API** como Hola tipo de aplicación.    
    2. Proporcione **cualquier URI de redirección** (p. ej., https://B2CGraphAPI), ya que no es relevante para este ejemplo.  
5. Hello aplicación tendrán ahora aparecen en la lista de Hola de aplicaciones, haga clic en ella hello tooobtain **Id. de aplicación** (también conocido como Id. de cliente). Cópielo, pues lo necesitará en una sección posterior.
6. En la hoja de configuración de hello, haga clic en **claves** y agregue una nueva clave (también conocido como secreto de cliente). Cópiela también para usarla en una sección posterior.

## <a name="configure-create-read-and-update-permissions-for-your-application"></a>Configuración de permisos de creación, lectura y actualización para la aplicación
Ahora tiene que tooconfigure su tooget aplicación que Hola a todos los necesarios permisos toocreate, leer, actualizar y eliminar usuarios.

1. Continuar en Hola hoja de registros de aplicación del portal de Azure, seleccione la aplicación.
2. En la hoja de configuración de hello, haga clic en **los permisos necesarios**.
3. En la hoja de hello permisos necesarios, haga clic en **Windows Azure Active Directory**.
4. En la hoja de habilitar el acceso de hello, seleccione hello **leer y escribir datos de directorio** permiso de **permisos de aplicación** y haga clic en **guardar**.
5. Por último, nuevo en la hoja de hello permisos necesarios, haga clic en hello **conceder permisos** botón.

Ahora tiene una aplicación que tenga permiso toocreate, lectura y actualización a los usuarios de su inquilino B2C.

## <a name="configure-delete-permissions-for-your-application"></a>Configuración de permisos de eliminación para la aplicación
Actualmente, Hola *leer y escribir datos de directorio* permiso **no** incluyen hello capacidad toodo cualquier eliminación como la eliminación de los usuarios. Si desea toogive los usuarios de aplicación Hola capacidad toodelete, necesitará toodo estos pasos adicionales que implican PowerShell, de lo contrario, puede omitir la sección siguiente toohello.

En primer lugar, descargue e instale hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152). A continuación, descargue e instale hello [módulo de Azure Active Directory de 64 bits para Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).

Después de instalar el módulo de PowerShell de hello, abra PowerShell y conéctese a tooyour B2C inquilino. Después de ejecutar `Get-Credential`, se le pedirá para un nombre de usuario y contraseña, escriba el nombre de usuario de hello y una contraseña de la cuenta de administrador de inquilinos B2C.

> [!IMPORTANT]
> Necesita la cuenta de administrador de inquilinos de toouse un B2C es **local** toohello B2C inquilino. Estas cuentas tienen este aspecto: myusername@myb2ctenant.onmicrosoft.com.

```powershell
Connect-MsolService
```

Ahora vamos a usar hello **Id. de aplicación** en script de Hola tooassign Hola aplicación Hola cuenta Administrador rol de usuario que le permitirá toodelete a los usuarios. Estas funciones tienen identificadores conocidos, por lo que todo lo que necesita toodo se introduce la **Id. de aplicación** en el siguiente script de Hola.

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

La aplicación ahora también tiene permisos toodelete los usuarios del inquilino B2C.

## <a name="download-configure-and-build-hello-sample-code"></a>Descargar, configurar y compilar el código de ejemplo de Hola
En primer lugar, descargue el código de ejemplo de Hola y ejecutarlo. A continuación, lo examinaremos más de cerca.  También puede [descargar código de muestra de Hola como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip). También puede clonarlo en un directorio de su elección:

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

Abra hello `B2CGraphClient\B2CGraphClient.sln` solución de Visual Studio en Visual Studio. Hola `B2CGraphClient` proyecto, archivo abierto hello `App.config`. Reemplazar configuración de aplicación de tres de hello con sus propios valores:

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

A continuación, haga doble clic en hello `B2CGraphClient` ejemplo de Hola de solución y volver a generar. Si todo es correcto, ahora debería tener un archivo ejecutable `B2C.exe` que se encuentra en `B2CGraphClient\bin\Debug`.

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a>Generar operaciones CRUD de usuario mediante Hola API Graph
Hola toouse B2CGraphClient, abra un `cmd` Windows comando símbolo del sistema y cambie el directorio toohello `Debug` directory. A continuación, ejecute hello `B2C Help` comando.

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

Se mostrará una breve descripción de cada comando. Cada vez que uno de estos comandos, invoque `B2CGraphClient` hace un toohello de solicitud API de Azure AD Graph.

### <a name="get-an-access-token"></a>Obtención de un token de acceso
Cualquier toohello de solicitud API Graph requiere un token de acceso para la autenticación. `B2CGraphClient`toohelp de biblioteca de autenticación de Active Directory (ADAL) de código abierto de hello usa adquirir tokens de acceso. ADAL facilita la adquisición de tokens al proporcionar una API sencilla y ocuparse de algunos detalles importantes, como el almacenamiento en caché de tokens de acceso. No es necesario toouse tooget AAL tokens, aunque. También puede obtener tokens elaborando solicitudes HTTP.

> [!NOTE]
> Este ejemplo de código usa AAL v2 en orden toocommunicate con hello API Graph.  Debe usar AAL v2 o v3 en tokens de acceso de tooget de orden que se pueden usar con hello Azure AD Graph API.
> 
> 

Cuando `B2CGraphClient` se ejecuta, crea una instancia de hello `B2CGraphClient` clase. constructor de Hola para esta clase se configura una técnica de scaffolding de autenticación de ADAL:

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

Vamos a usar hello `B2C Get-User` comando como un ejemplo. Cuando `B2C Get-User` se invoca sin ninguna entrada adicional, Hola Hola de llamadas CLI `B2CGraphClient.GetAllUsers(...)` método. Este método llama a `B2CGraphClient.SendGraphGetRequest(...)`, que envía una solicitud HTTP GET, toohello API Graph. Antes de `B2CGraphClient.SendGraphGetRequest(...)` envía Hola solicitud GET, primero obtiene un token de acceso mediante el uso de ADAL:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

Puede obtener un acceso token para hello API Graph por llamada Hola AAL `AuthenticationContext.AcquireToken(...)` método. AAL, a continuación, devuelve un `access_token` que representa la identidad de la aplicación hello.

### <a name="read-users"></a>Lectura de usuarios
Cuando desee tooget una lista de usuarios o hacer que un usuario determinado de hello API Graph, puede enviar un elemento HTTP `GET` solicitar toohello `/users` punto de conexión. Una solicitud para todos los usuarios de hello en un inquilino tiene el siguiente aspecto:

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee esta solicitud, ejecute:

 ```
 > B2C Get-User
 ```

Hay dos toonote aspectos importantes:

* Hello token de acceso adquirido a través de AAL se agrega toohello `Authorization` encabezado mediante el uso de hello `Bearer` esquema.
* Para los inquilinos B2C, debe usar el parámetro de consulta de hello `api-version=1.6`.

Ambos de estos detalles se tratan en hello `B2CGraphClient.SendGraphGetRequest(...)` método:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a>Creación de cuentas de usuario consumidor
Al crear cuentas de usuario en el inquilino B2C, puede enviar un elemento HTTP `POST` solicitar toohello `/users` punto de conexión:

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

La mayoría de estas propiedades en esta solicitud es usuarios de consumidor de toocreate necesarios. más información, haga clic en la toolearn [aquí](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser). Tenga en cuenta que hello `//` comentarios se han incluido a modo de ilustración. No los incluya en una solicitud real.

solicitud de hello toosee, ejecute uno de hello siguientes comandos:

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

Hola `Create-User` comando toma un archivo .json como un parámetro de entrada. Contiene una representación JSON de un objeto de usuario. Hay dos archivos .json de ejemplo en el código de ejemplo de Hola: `usertemplate-email.json` y `usertemplate-username.json`. Puede modificar estos archivos toosuit sus necesidades. Además toohello tengan campos anteriores, se incluyen varios campos opcionales que puede usar en estos archivos. Obtener más información sobre los campos opcionales de hello puede encontrarse en hello [referencia de entidad de API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).

Puede ver cómo se construye la solicitud POST de hello en `B2CGraphClient.SendGraphPostRequest(...)`.

* Se adjunta una toohello de token de acceso `Authorization` encabezado de solicitud de saludo.
* Establece `api-version=1.6`.
* Incluye objetos de usuario JSON de hello en el cuerpo de saludo de solicitud de Hola.

> [!NOTE]
> Si hello las cuentas que desea toomigrate desde un almacén de usuario existente tiene menos seguros de contraseña que hello [intensidad de contraseña segura aplicado Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), puede deshabilitar el requisito de contraseña segura de hello mediante hello `DisableStrongPassword`valor Hola `passwordPolicies` propiedad. Por ejemplo, puede modificar Hola crear solicitud de usuario proporcionado anteriormente como sigue: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.
> 
> 

### <a name="update-consumer-user-accounts"></a>Actualización de cuentas de usuario consumidor
Al actualizar los objetos de usuario, el proceso de hello es toohello similar que utiliza objetos de usuario de toocreate. Pero este proceso utiliza Hola HTTP `PATCH` método:

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

Intente tooupdate un usuario mediante la actualización de los archivos JSON con nuevos datos. A continuación, puede usar `B2CGraphClient` toorun uno de estos comandos:

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

Inspeccionar hello `B2CGraphClient.SendGraphPatchRequest(...)` método para obtener más información acerca de cómo toosend esta solicitud.

### <a name="search-users"></a>Búsqueda de usuarios
Puede buscar usuarios en el inquilino de B2C de dos maneras. Uno, con Id. de objeto del usuario de Hola o dos, utilizando el identificador de inicio de sesión del usuario de hello (es decir, hello `signInNames` propiedad).

Ejecute uno de hello después toosearch de comandos para un usuario específico:

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

Estos son algunos ejemplos:

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a>Eliminación de usuarios
proceso de Hola para eliminar un usuario es muy sencillo. Hola use HTTP `DELETE` método y construir una URL de hello con hello corregir Id. de objeto:

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee por ejemplo, escriba este comando y vista de solicitud de eliminación de Hola que es toohello impreso consola:

```
> B2C Delete-User <object-id-of-user>
```

Inspeccionar hello `B2CGraphClient.SendGraphDeleteRequest(...)` método para obtener más información acerca de cómo toosend esta solicitud.

Puede realizar muchas otras acciones con hello Azure AD Graph API de administración de toouser de adición. La [referencia de la API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) proporciona detalles sobre cada acción, junto con solicitudes de ejemplo.

## <a name="use-custom-attributes"></a>Uso de atributos personalizados
La mayoría de las aplicaciones de consumidor necesitan toostore algún tipo de información de perfil de usuario personalizada. Una manera de hacer esto es toodefine un atributo personalizado en el inquilino B2C. A continuación, puede tratar ese Hola de atributo igual tratar cualquier otra propiedad en un objeto de usuario. Puede actualizar el atributo de hello, delete Hola atributo, consulta mediante el atributo de hello, enviar atributo hello como una notificación de tokens de inicio de sesión y mucho más.

toodefine un atributo personalizado en el inquilino B2C, consulte hello [referencia de atributo personalizado de B2C](active-directory-b2c-reference-custom-attr.md).

Puede ver los atributos personalizados de hello definidos en el inquilino B2C usando `B2CGraphClient`:

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

salida de Hello de estas funciones revela detalles Hola de cada atributo personalizado, como:

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

Puede usar Hola nombre completo, como `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, como una propiedad en los objetos de usuario.  Actualizar el archivo .json con la nueva propiedad de Hola y un valor de propiedad de hello y, a continuación, ejecute:

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

Con `B2CGraphClient`, tiene una aplicación de servicio que puede administrar sus usuarios del inquilino de B2C mediante programación. `B2CGraphClient`usa su propio toohello tooauthenticate de identidad de aplicación API de Azure AD Graph. También adquiere tokens mediante un secreto de cliente. Según vaya incorporando esta funcionalidad a su aplicación, debe recordar algunos puntos clave para las aplicaciones B2C:

* Necesita toogrant Hola aplicación Hola permisos adecuados en el inquilino de Hola.
* Por ahora, debe toouse AAL (no MSAL) tooget los tokens de acceso. (Puede también enviar mensajes de protocolo directamente, sin usar una biblioteca.)
* Cuando se llama a Hola API Graph, utilice `api-version=1.6`.
* Al crear y actualizar los usuarios consumidores, hay algunas propiedades obligatorias, tal como se describió anteriormente.

Si tiene alguna pregunta o las solicitudes para las acciones que desea que tooperform mediante la API Graph hello en el inquilino B2C, deje un comentario en este artículo o un problema de archivos en el repositorio de ejemplo de código de hello GitHub.

