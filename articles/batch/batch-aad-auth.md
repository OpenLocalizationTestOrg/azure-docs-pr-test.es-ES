---
title: soluciones de servicios de Azure Batch de aaaUse Azure Active Directory tooauthenticate | Documentos de Microsoft
description: "Proceso por lotes es compatible con Azure AD para la autenticación de hello servicio por lotes."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Autenticación de soluciones de servicio de Batch con Active Directory

Azure Batch admite la autenticación con [Azure Active Directory][aad_about] (Azure AD). Azure Active Directory es el directorio basado en la nube multiinquilino y el servicio de administración de identidades de Microsoft. Azure por sí mismo utiliza Azure AD tooauthenticate sus clientes, los administradores de servicios y usuarios de la organización.

Al utilizar la autenticación de Azure AD con Azure Batch, puede autenticar de una de estas dos maneras:

- Mediante el uso de **la autenticación integrada de** tooauthenticate un usuario que está interactuando con la aplicación hello. Una aplicación mediante la autenticación integrada recopila las credenciales del usuario y utiliza esas credenciales tooauthenticate acceder a tooBatch los recursos.
- Mediante el uso de un **entidad de servicio** tooauthenticate una aplicación de modo desatendida. Una entidad de servicio define Hola directiva y los permisos para una aplicación en la aplicación hello de orden toorepresent al tener acceso a recursos en tiempo de ejecución.

toolearn más información acerca de Azure AD, vea hello [documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).

## <a name="authentication-and-pool-allocation-mode"></a>Modo de autenticación y de asignación de grupo

Al crear una cuenta de Batch, puede especificar dónde se deben asignar los grupos creados para esa cuenta. Puede elegir tooallocate grupos en la suscripción al servicio de lote Hola predeterminado o en una suscripción de usuario. Su elección afecta a cómo autenticar acceso tooresources en esa cuenta.

- **Suscripción al servicio de Batch**. De forma predeterminada, los grupos de Batch se asignan en una suscripción del servicio Batch. Si elige esta opción, puede autenticar acceso tooresources en esa cuenta con [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) o con Azure AD.
- **Suscripción de usuario**. Puede elegir tooallocate grupos de proceso por lotes en una suscripción de usuario que especifique. Si elige esta opción, debe autenticarse con Azure AD.

## <a name="endpoints-for-authentication"></a>Puntos de conexión para autenticación

aplicaciones de lote tooauthenticate con Azure AD, necesita tooinclude algunos puntos de conexión conocidos en el código.

### <a name="azure-ad-endpoint"></a>Punto de conexión de Azure AD

Hola base es el extremo de la autoridad de Azure AD:

`https://login.microsoftonline.com/`

tooauthenticate con Azure AD, use este extremo junto con el Id. de inquilino de hello (Id. de directorio). Id. de inquilino de Hello identifica hello toouse de inquilino de Azure AD para la autenticación. tooretrieve Hola Id. de inquilino, siga los pasos de hello descritos en [obtener Id. de inquilino de Hola para Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> extremo específico del inquilino de Hello es necesaria cuando se autentica con una entidad de servicio. 
> 
> extremo específico del inquilino de Hello es opcional cuando se autentica mediante la autenticación integrada, pero se recomienda. Sin embargo, también puede utilizar el punto de conexión común de hello Azure AD. punto de conexión común Hola proporciona una credencial genérica recopilación interfaz cuando no se ha proporcionado un específicos del inquilino. punto de conexión común de Hello es `https://login.microsoftonline.com/common`.
>
>

Para más información sobre los puntos de conexión de Azure AD, consulte [Escenarios de autenticación para Azure AD][aad_auth_scenarios].

### <a name="batch-resource-endpoint"></a>Punto de conexión de recursos de Batch

Hola de uso **punto de conexión de recursos de Azure Batch** tooacquire un token para autenticar solicitudes de servicio por lotes de toohello:

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>Registro de la aplicación con un inquilino

primer paso de Hola para utilizar Azure AD tooauthenticate está registrando su aplicación en un inquilino de Azure AD. Registrar la aplicación le permite toocall hello Azure [biblioteca de autenticación de Active Directory] [ aad_adal] (AAL) desde el código. Hola AAL proporciona una API para autenticar con Azure AD desde la aplicación. Registrando su aplicación es necesario si tiene previsto toouse la autenticación integrada o una entidad de servicio.

Al registrar la aplicación, se facilita información sobre su tooAzure aplicación AD. Azure AD, a continuación, proporciona un identificador de la aplicación usa tooassociate de su aplicación con Azure AD en tiempo de ejecución. vea toolearn más información sobre el identificador de la aplicación hello [aplicación y objetos de entidad de servicio en Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

tooregister la aplicación de lote, siga los pasos de Hola Hola [agregar una aplicación](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sección [integrar aplicaciones con Azure Active Directory][aad_integrate]. Si se registra la aplicación como una aplicación nativa, puede especificar cualquier URI válido para hello **URI de redireccionamiento**. No es necesario toobe un punto de conexión real.

Después de registrar la aplicación, verá el identificador de la aplicación hello:

![Registro de la aplicación de Batch con Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

Para más información sobre el registro de una aplicación, consulte [Escenarios de autenticación para Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).

## <a name="get-hello-tenant-id-for-your-active-directory"></a>Obtener Id. de inquilino de Hola de su Active Directory

Id. de inquilino de Hello identifica el inquilino de Azure AD de Hola que proporciona servicios de autenticación tooyour aplicaciones. tooget Hola Id. de inquilino, siga estos pasos:

1. Hola portal de Azure, seleccione su Active Directory.
2. Haga clic en **Propiedades**.
3. Copiar valor GUID de hello previsto Hola Id. de directorio. Este valor también se denomina identificador del inquilino Hola.

![Id. de directorio Hola](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>Uso de autenticación integrada

tooauthenticate con la autenticación integrada, deberá toogrant la toohello de tooconnect de permisos de aplicación API de servicio de lote. Este paso permite que la API de servicio de aplicación tooauthenticate llamadas toohello por lotes con Azure AD.

Una vez que se haya [registrar la aplicación](#register-your-application-with-an-azure-ad-tenant), siga estos pasos en hello Azure toogrant portal que tener acceso el servicio por lotes toohello:

1. En el panel de navegación izquierdo de Hola de hello portal de Azure, elija **más servicios**, haga clic en **registros de aplicación**.
2. Busque el nombre de saludo de la aplicación en la lista de Hola de registros de aplicación:

    ![Buscar el nombre de la aplicación](./media/batch-aad-auth/search-app-registration.png)

3. Abra hello **configuración** hoja para la aplicación. Hola **el acceso de API** sección, seleccione **los permisos necesarios**.
4. Hola **los permisos necesarios** hoja, haga clic en hello **agregar** botón.
5. En el paso 1, busque Hola API de lote. Buscar cada una de estas cadenas hasta que encuentre Hola API:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. Los inquilinos más recientes de Azure AD pueden utilizar este nombre.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** es Id. de Hola para hello API de lote. 
6. Una vez que encuentre Hola API de lote, selecciónelo y haga clic en hello **seleccione** botón.
6. En el paso 2, seleccione Hola casilla de verificación junto demasiado**servicio de lote de Azure de acceso** y haga clic en hello **seleccione** botón.
7. Haga clic en hello **realiza** botón.

Hola **permisos necesarios** hoja ahora muestra que la aplicación de Azure AD tiene acceso a tooboth AAL y Hola API del servicio de lote. Los permisos se conceden tooADAL automáticamente al registrar primero la aplicación con Azure AD.

![Concesión de permisos de API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>Uso de una entidad de servicio 

tooauthenticate una aplicación que se ejecuta desatendida, utilice a una entidad de servicio. Una vez que ha registrado su aplicación, siga estos pasos en hello tooconfigure portal Azure una entidad de servicio:

1. Solicite una clave secreta para la aplicación.
2. Asignar una aplicación de tooyour de rol RBAC.

### <a name="request-a-secret-key-for-your-application"></a>Solicitud de una clave secreta para la aplicación

Cuando la aplicación se autentica con una entidad de servicio, envía Hola Id. de aplicación y un secreto tooAzure clave AD. Podrá necesita toocreate y copiar toouse de clave secreta de Hola desde el código.

Siga estos pasos en hello portal de Azure:

1. En el panel de navegación izquierdo de Hola de hello portal de Azure, elija **más servicios**, haga clic en **registros de aplicación**.
2. Buscar Hola nombre de la aplicación en la lista de Hola de registros de aplicación.
3. Hola de presentación **configuración** hoja. Hola **el acceso de API** sección, seleccione **claves**.
4. toocreate una clave, escriba una descripción para la clave de Hola. A continuación, seleccione una duración para la clave de Hola de uno o dos años. 
5. Haga clic en hello **guardar** botón toocreate y mostrar hello clave. Copie lugar seguro de hello clave-valor tooa, no será capaz de tooaccess nuevo después de deje de hoja de Hola. 

    ![Creación de una clave secreta](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>Asignar una aplicación de RBAC rol tooyour

tooauthenticate con una entidad de servicio, necesita una aplicación de RBAC rol tooyour tooassign. Siga estos pasos:

1. Hola portal de Azure, navegue toohello cuenta de lote utilizado por la aplicación.
2. Hola **configuración** hoja de cuenta de lote de hello, seleccione **Control de acceso (IAM)**.
3. Haga clic en hello **agregar** botón. 
4. De hello **rol** lista desplegable, elija cualquier hello _colaborador_ o _lector_ rol para la aplicación. Para obtener más información sobre estas funciones, vea [empezar a trabajar con Control de acceso basado en roles en el portal de Azure hello](../active-directory/role-based-access-control-what-is.md).  
5. Hola **seleccione** , escriba el nombre de saludo de la aplicación. Seleccione la aplicación de lista de Hola y haga clic en **guardar**.

La aplicación debe aparecer ahora en la configuración de control de acceso con un rol RBAC asignado. 

![Asignar una aplicación de RBAC rol tooyour](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>Obtener Id. de inquilino de Hola para Azure Active Directory

Id. de inquilino de Hello identifica el inquilino de Azure AD de Hola que proporciona servicios de autenticación tooyour aplicaciones. tooget Hola Id. de inquilino, siga estos pasos:

1. Hola portal de Azure, seleccione su Active Directory.
2. Haga clic en **Propiedades**.
3. Copiar valor GUID de hello previsto Hola Id. de directorio. Este valor también se denomina identificador del inquilino Hola.

![Id. de directorio Hola](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>Ejemplos de código

ejemplos de código de Hello en esta sección muestran cómo tooauthenticate con Azure AD mediante la autenticación integrada y con una entidad de servicio. Estos ejemplos de código usa .NET pero Hola conceptos son similares para otros idiomas.

> [!NOTE]
> Un token de autenticación de Azure AD expira después de una hora. Cuando se usa una larga duración **BatchClient** de objeto, se recomienda que recuperar un token de ADAL en cada solicitud tooensure siempre tiene un token válido. 
>
>
> tooachieve en. NET, escribir un método que recupera Hola símbolo (token) de Azure AD y pasa ese método tooa **BatchTokenCredentials** objeto como un delegado. se llama el método de delegado de Hello en cada tooensure servicio de lote toohello de la solicitud que se proporciona un token válido. De forma predeterminada ADAL almacena en caché los tokens, por lo que solo se recuperará un nuevo token de Azure AD si es necesario. Para más información, consulte [Escenarios de autenticación para Azure AD][aad_auth_scenarios].
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>Ejemplo de código: uso de la autenticación integrada de Azure AD con .NET de Batch

tooauthenticate con la autenticación integrada de .NET de lote, Hola referencia [.NET de lote de Azure](https://www.nuget.org/packages/Azure.Batch/) hello y paquete [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paquete.

Hola siguientes `using` las instrucciones en el código:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Id. de inquilino de hello referencia extremo de Azure AD en el código, incluidas Hola tooretrieve Hola Id. de inquilino, siga los pasos de hello descritos en [obtener Id. de inquilino de Hola para Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Extremo del recurso de servicio de referencia Hola por lotes:

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Haga referencia a la cuenta de Batch:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Especifique el Id. de aplicación de hello (Id. de cliente) para la aplicación. Identificador de la aplicación Hello está disponible desde el registro de una aplicación Hola portal de Azure:

```csharp
private const string ClientId = "<application-id>";
```

Copie también URI especificado durante el proceso de registro de hello de redirección de Hola. Hola redirección URI especificado en el código debe coincidir con el URI que proporcionó al registrar la aplicación hello de redirección de hello:

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Escribir un token de autenticación de devolución de llamada método tooacquire Hola de Azure AD. Hola **GetAuthenticationTokenAsync** método de devolución de llamada que se muestra a continuación llama a un usuario que está interactuando con la aplicación hello tooauthenticate ADAL. Hola **AcquireTokenAsync** método proporcionado por AAL indicaciones Hola usuario sus credenciales y aplicación hello una vez continúa usuario Hola les proporciona (a menos que ya ha almacenado en caché de credenciales):

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

Construir un **BatchTokenCredentials** objeto que toma el delegado de Hola como un parámetro. Usar esas credenciales tooopen un **BatchClient** objeto. También puede usarlo **BatchClient** objeto para las operaciones posteriores contra Hola servicio por lotes:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>Ejemplo de código: uso de una entidad de servicio de Azure AD con .NET de Batch

tooauthenticate con una entidad de servicio de lote de. NET, Hola de referencia [.NET de lote de Azure](https://www.nuget.org/packages/Azure.Batch/) hello y paquete [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paquete.

Hola siguientes `using` las instrucciones en el código:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Id. de inquilino de hello referencia extremo de Azure AD en el código, incluidas Hola Cuando se usa una entidad de servicio, debe proporcionar un punto de conexión específico del inquilino. tooretrieve Hola Id. de inquilino, siga los pasos de hello descritos en [obtener Id. de inquilino de Hola para Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Extremo del recurso de servicio de referencia Hola por lotes:  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Haga referencia a la cuenta de Batch:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Especifique el Id. de aplicación de hello (Id. de cliente) para la aplicación. Identificador de la aplicación Hello está disponible desde el registro de una aplicación Hola portal de Azure:

```csharp
private const string ClientId = "<application-id>";
```

Especifique la clave secreta de Hola que copió de hello portal de Azure:

```csharp
private const string ClientKey = "<secret-key>";
```

Escribir un token de autenticación de devolución de llamada método tooacquire Hola de Azure AD. Hola **GetAuthenticationTokenAsync** método de devolución de llamada que se muestra aquí llamadas AAL para la autenticación desatendida:

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

Construir un **BatchTokenCredentials** objeto que toma el delegado de Hola como un parámetro. Usar esas credenciales tooopen un **BatchClient** objeto. A continuación, puede usar **BatchClient** objeto para las operaciones posteriores contra Hola servicio por lotes:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de Azure AD, vea hello [documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/). Ejemplos detallados que muestran cómo toouse AAL está disponible en hello [ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteca.

toolearn más información acerca de las entidades de seguridad de servicio, consulte [aplicación y objetos de entidad de servicio en Azure Active Directory](../active-directory/develop/active-directory-application-objects.md). toocreate un servicio principal mediante hello Azure portal, vea [usar la aplicación de portal toocreate Active Directory y la entidad de servicio que puede tener acceso a recursos](../resource-group-create-service-principal-portal.md). Las entidades de servicio también se pueden crear con PowerShell o la CLI de Azure. 

las aplicaciones de administración de lotes tooauthenticate mediante Azure AD, vea [soluciones de administración de lote autenticarse con Active Directory](batch-aad-auth-management.md). 

[aad_about]: ../active-directory/active-directory-whatis.md "¿Qué es Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Escenarios de autenticación para Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integración de aplicaciones con Azure Active Directory"
[azure_portal]: http://portal.azure.com
