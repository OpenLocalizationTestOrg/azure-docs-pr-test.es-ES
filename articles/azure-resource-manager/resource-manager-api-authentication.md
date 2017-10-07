---
title: "aaaAzure Active Directory autenticación y el Administrador de recursos | Documentos de Microsoft"
description: "Tooauthentication de guía del desarrollador con hello API del Administrador de recursos de Azure y Azure Active Directory para integrar una aplicación con otras suscripciones de Azure."
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>Utilizar suscripciones de tooaccess de API de autenticación de administrador de recursos
## <a name="introduction"></a>Introducción
Si es un desarrollador de software que necesita toocreate una aplicación que administra los recursos de Azure del cliente, este tema muestra cómo tooauthenticate con hello las API del Administrador de recursos de Azure y obtener acceso tooresources en otras suscripciones.

La aplicación puede tener acceso a Hola API del Administrador de recursos de dos maneras:

1. **Acceso de usuario + aplicación**: para aplicaciones que acceden a los recursos en nombre de un usuario con una sesión iniciada. Este enfoque funciona con aplicaciones, como aplicaciones web y herramientas de línea de comandos, que se encargan solo de la "administración interactiva" de los recursos de Azure.
2. **Acceso de solo aplicación**: para las aplicaciones que ejecutan servicios de demonio y trabajos programados. identidad de la aplicación Hello se concede recursos toohello de acceso directo. Este enfoque funciona para las aplicaciones que necesiten tooAzure de acceso (desatendido) sin periféricos a largo plazo.

Este tema proporciona instrucciones paso a paso toocreate una aplicación que utiliza estos métodos de autorización. Muestra cómo tooperform cada paso con API de REST o C#. está disponible en la aplicación de ASP.NET MVC completa Hello [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).

## <a name="what-hello-web-app-does"></a>¿Qué aplicación web de hello
Hola a la aplicación web:

1. Inicia sesión de un usuario de Azure.
2. Solicita acceso usuario toogrant hello web app tooResource Manager.
3. Obtiene un token de acceso de usuario + aplicación para acceder a Resource Manager.
4. Utiliza toocall token (del paso 3) el Administrador de recursos y el rol de tooa principal de servicio de la aplicación de asignar Hola de suscripción de hello, que ofrece la suscripción de toohello de acceso a largo plazo de hello aplicación.
5. Obtiene un token de acceso de solo aplicación.
6. Utiliza recursos de toomanage token (del paso 5) en la suscripción de Hola a través del Administrador de recursos.

Aquí es flujo de hello-to-end de aplicación web de Hola.

![Flujo de autenticación de Resource Manage](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

Como un usuario, puede proporcionar el Id. de suscripción de hello para la suscripción de hello desea toouse:

![proporcionar id. de suscripción](./media/resource-manager-api-authentication/sample-ux-1.png)

Seleccione hello toouse de cuenta de inicio de sesión.

![seleccionar cuenta](./media/resource-manager-api-authentication/sample-ux-2.png)

Proporcione sus credenciales.

![proporcionar credenciales](./media/resource-manager-api-authentication/sample-ux-3.png)

Conceder tooyour de acceso de aplicación hello las suscripciones de Azure:

![Conceder acceso](./media/resource-manager-api-authentication/sample-ux-4.png)

Administre las suscripciones conectadas:

![Conectar suscripción](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>Registre la aplicación
Antes de comenzar a codificar, registre la aplicación web con Azure Active Directory (AD). registro de una aplicación Hola crea una identidad central para la aplicación en Azure AD. Contiene información básica acerca de la aplicación como identificador de cliente OAuth, direcciones URL de respuesta y las credenciales que su aplicación usa tooauthenticate y acceso a las API del Administrador de recursos de Azure. registro de una aplicación Hola también registra Hola distintos permisos que necesita la aplicación al tener acceso a Microsoft APIs en nombre de usuario de Hola de delegados.

Dado que la aplicación tiene acceso a otra suscripción, debe configurarla como una aplicación multiinquilino. validación de toopass, proporcionar un dominio asociado con su Active Directory de Azure. dominios de hello toosee asociados con Azure Active Directory, inicio de sesión toohello [portal clásico](https://manage.windowsazure.com). Seleccione Azure Active Directory y luego **Dominios**.

Hola de ejemplo siguiente muestra cómo tooregister Hola aplicación mediante Azure PowerShell. Debe tener Hola versión más reciente (agosto de 2016) de PowerShell de Azure para este comando toowork.

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

toolog en como Hola aplicación de AD, necesita contraseña e Id. de aplicación de Hola. identificador de la aplicación de hello toosee que se devuelve desde el comando anterior hello, use:

    $app.ApplicationId

Hola de ejemplo siguiente muestra cómo tooregister Hola aplicación mediante Azure CLI.

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

los resultados de Hello incluyen hello AppId, que necesita autenticarse como aplicación hello.

### <a name="optional-configuration---certificate-credential"></a>Configuración opcional: credencial de certificado
Azure AD también admite credenciales de certificado para las aplicaciones: crear un certificado autofirmado, mantenga la clave privada de Hola y agregar el registro de la aplicación hello tooyour clave pública Azure AD. Para la autenticación, la aplicación envía una tooAzure carga pequeña AD firmada con la clave privada y Azure AD valida la firma de hello mediante clave pública de Hola que haya registrado.

Para obtener información acerca de cómo crear una aplicación de AD con un certificado, consulte [toocreate de PowerShell de Azure Use una entidad de servicio recursos tooaccess](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) o [toocreate de CLI de Azure Use una entidad de servicio tooaccess recursos](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>Obtención de un identificador de inquilino a partir del identificador de suscripción
toorequest un símbolo (token) que puede ser toocall usa el Administrador de recursos, la aplicación necesita tooknow el identificador del inquilino de Hola de hello Azure AD que hospeda Hola suscripción de Azure. Es muy probable que los usuarios conozcan sus identificadores de suscripción, pero quizá no sus identificadores de inquilino para Azure Active Directory. tooget Hola Id. de inquilino del usuario, solicitar el usuario de Hola Hola Id. de suscripción. Al enviar una solicitud acerca de la suscripción de Hola, proporcionar ese identificador de suscripción:

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

solicitud de Hello produce un error porque el usuario hello no ha registrado aún en, pero se puede recuperar el Id. de inquilino de Hola de respuesta de Hola. En esa excepción, recuperar el Id. de inquilino de hello del valor del encabezado de respuesta de Hola para **WWW-Authenticate**. Vea esta implementación en hello [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) método.

## <a name="get-user--app-access-token"></a>Obtención de un token de acceso de usuario + aplicación
La aplicación redirige Hola usuario tooAzure AD con un OAuth 2.0 autorizar solicitudes - las credenciales de usuario de tooauthenticate hello y devolver un código de autorización. La aplicación usa tooget de código de autorización de hello un token de acceso para el Administrador de recursos. Hola [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) método crea la solicitud de autorización de Hola.

En este tema muestra las solicitudes de API de REST de hello tooauthenticate usuario de Hola. También puede utilizar autenticación de tooperform de bibliotecas de ayuda en el código. Para obtener más información sobre estas bibliotecas, consulte [Bibliotecas de autenticación de Azure Active Directory](../active-directory/active-directory-authentication-libraries.md). Para obtener instrucciones sobre la integración de la administración de identidades en una aplicación, consulte la [Guía del desarrollador de Azure Active Directory](../active-directory/active-directory-developers-guide.md).

### <a name="auth-request-oauth-20"></a>Solicitud de autenticación (OAuth 2.0)
Emitir un punto de conexión abierto conectar/OAuth2.0 autorizar solicitudes de identificador de autorizar toohello Azure AD:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

parámetros de cadena de consulta de Hola que están disponibles para esta solicitud se describen en hello [solicitar un código de autorización](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) tema.

Hola siguiente ejemplo se muestra cómo toorequest autorización de OAuth2.0:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

Azure AD autentica el usuario de hello y, si es necesario, le pide permiso toohello aplicación de hello usuario toogrant. Devuelve toohello de código de autorización de hello dirección URL de respuesta de la aplicación. Función hello solicitado response_mode, Azure AD cualquiera le responde Hola datos de cadena de consulta o como datos de entrada.

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>Solicitud de autenticación (Open ID Connect)
Si lo desea tooaccess Azure Resource Manager en nombre de usuario de Hola y también permite Hola usuario toosign en aplicación tooyour con su cuenta de Azure AD, emitir una abra conectarse autorizar solicitudes de identificador. Con Connect de identificador abierto, la aplicación también recibe un id_token de Azure AD que puede usar su aplicación toosign en usuario Hola.

parámetros de cadena de consulta de Hola que están disponibles para esta solicitud se describen en hello [Hola inicio de sesión de solicitud de envío](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) tema.

Este es un ejemplo de solicitud de Open ID Connect:

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

Azure AD autentica el usuario de hello y, si es necesario, le pide permiso toohello aplicación de hello usuario toogrant. Devuelve toohello de código de autorización de hello dirección URL de respuesta de la aplicación. Función hello solicitado response_mode, Azure AD cualquiera le responde Hola datos de cadena de consulta o como datos de entrada.

Este es un ejemplo de respuesta de Open ID Connect:

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>Solicitud de token (flujo de concesión de códigos de OAuth2.0)
Ahora que la aplicación ha recibido el código de autorización de Hola de Azure AD, es el token de acceso de tiempo tooget hello para el Administrador de recursos de Azure.  Exponga un extremo de Token de Azure AD toohello OAuth2.0 código Grant símbolo (token) de solicitud:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

parámetros de cadena de consulta de Hola que están disponibles para esta solicitud se describen en hello [usar código de autorización de hello](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) tema.

Hola de ejemplo siguiente muestra una solicitud de token de concesión de código con la credencial de contraseña:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Cuando se trabaja con las credenciales de certificado, cree un JSON Web Token (JWT) y el inicio de sesión (RSA SHA256) con clave privada de Hola de credencial de certificado de la aplicación. tipos de notificación de token de Hola Hola se muestran una en [notificaciones de tokens de JWT](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims). Como referencia, vea hello [código biblioteca de autenticación de Active Directory (.NET)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign tokens de JWT de aserción de cliente.

Vea hello [conectarse de identificador abierto especificación](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) para obtener más información acerca de la autenticación de cliente.

Hola de ejemplo siguiente muestra una solicitud de token de concesión de código con credenciales de certificado:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

Un ejemplo de respuesta de token de concesión de códigos:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>Control de la respuesta de token de concesión de códigos
Una respuesta correcta del token contiene el token de acceso de hello (usuario + aplicación) para el Administrador de recursos de Azure. La aplicación usa este tooaccess de token de acceso el Administrador de recursos en nombre de usuario de Hola. duración de Hola de tokens de acceso emitido por Azure AD es una hora. No es probable que la aplicación web necesita el token de acceso de toorenew Hola (usuario + aplicación). Si es necesario el token de acceso de toorenew hello, usar el token de actualización de Hola que recibe la aplicación en respuesta de token de Hola. Exponga un extremo de Token de Azure AD toohello OAuth2.0 de solicitud de Token:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Hello toouse de parámetros con la solicitud de actualización de Hola se describen en [actualizar token de acceso de hello](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).

Hello en el ejemplo siguiente se muestra cómo toouse Hola el token de actualización:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Aunque los tokens de actualización pueden ser utilizados tooget nuevos tokens de acceso para el Administrador de recursos de Azure, no son adecuados para el acceso sin conexión a la aplicación. se limita la duración de tokens de actualización de Hola y tokens de actualización son usuario toohello enlazado. Si el usuario de hello abandona la organización de hello, aplicación hello mediante el token de actualización de hello pierda el acceso. Este enfoque no es apta para las aplicaciones que son utilizados por los equipos toomanage sus recursos de Azure.

## <a name="check-if-user-can-assign-access-toosubscription"></a>Compruebe si el usuario puede asignar acceso toosubscription
La aplicación ahora tiene un token tooaccess Azure Resource Manager en nombre de usuario de Hola. paso siguiente Hello es tooconnect su suscripción de toohello de aplicación. Después de conectarse, la aplicación puede administrar las suscripciones incluso cuando el usuario de hello no está presente (acceso sin conexión a largo plazo).

Para cada tooconnect de suscripción, llame a hello [permisos de lista del Administrador de recursos](https://docs.microsoft.com/rest/api/authorization/permissions) toodetermine API si el usuario de hello tiene derechos de administración de acceso para la suscripción de Hola.

Hola [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) método de hello aplicación de ejemplo de ASP.NET MVC implementa esta llamada.

Hola siguiente ejemplo se muestra cómo toorequest permisos de un usuario en una suscripción. 83cfe939-2402-4581-b761-4f59b0a041e4 es el Id. de Hola de suscripción de Hola.

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

Es un ejemplo de permisos del usuario de hello respuesta tooget suscripción:

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

permisos de Hello API devuelve varios permisos. Cada permiso consta de acciones permitidas (actions) y acciones no permitidas (notactions). Si una acción está presente en hello lista de acciones de cualquier permiso de elementos permitido y no está presente en lista de notactions Hola de ese permiso, hello es permitido tooperform esa acción. **Microsoft.Authorization/RoleAssignments/Write** es la acción de Hola que conceda acceso de rights management. La aplicación debe analizar toolook de resultado de hello permisos para una coincidencia de expresión regular con esta cadena de acción en las acciones de Hola y notactions de cada permiso.

## <a name="get-app-only-access-token"></a>Obtención de un token de acceso de solo aplicación
Ahora, sabrá si el usuario Hola puede asignar acceso toohello suscripción de Azure. pasos siguientes Hola son:

1. Asignar Hola adecuado RBAC rol tooyour identidad de la aplicación en la suscripción de Hola.
2. Validar la asignación de acceso de hello mediante una consulta para el permiso de la aplicación hello en suscripción de Hola o mediante el acceso a Administrador de recursos usando solo de aplicación de símbolo (token).
3. Conexión de hello registros en la estructura de datos de aplicaciones "conectado suscripciones" - conservar el identificador de Hola de suscripción de Hola.

Echemos un vistazo más de cerca en el primer paso de Hola. tooassign Hola adecuado RBAC rol toohello identidad de la aplicación, debe determinar:

* Id. de objeto de Hola de identidad de la aplicación en Azure Active Directory del usuario de hello
* Hola identificador del rol RBAC Hola que requiera la aplicación de suscripción de Hola

Cuando la aplicación autentica a un usuario desde un directorio de Azure AD, crea un objeto de entidad de servicio para la aplicación en dicho directorio de Azure AD. Azure permite RBAC roles toobe asignado a las entidades de seguridad tooservice toocorresponding aplicaciones de acceso directo de toogrant en recursos de Azure. Esta acción es exactamente lo que deseamos toodo. Consulta hello Azure AD Graph API toodetermine Hola identificador de entidad de servicio de saludo de la aplicación de usuario que inició sesión hello's Azure AD.

Solo tiene un token de acceso para el Administrador de recursos de Azure, necesita un hello toocall símbolo (token) de acceso nueva API de Azure AD Graph. Todas las aplicaciones de Azure AD tiene permiso tooquery su propio objeto de entidad de servicio, por lo que un token de acceso de solo de aplicación es suficiente.

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>Obtención de token de acceso de solo aplicación para la API de Azure AD Graph
tooauthenticate tu aplicación y un token tooAzure AD Graph API, emitir un extremo de token de tooAzure AD de OAuth2.0 de concesión de credenciales de cliente flujo solicitud de token (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/Token**).

Hola [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) método de aplicación de ejemplo de ASP.net MVC obtiene acceso solo de aplicación token para el uso de API Graph de hello Hola biblioteca de autenticación de Active Directory para. NET.

parámetros de cadena de consulta de Hola que están disponibles para esta solicitud se describen en hello [solicitar un Token de acceso](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) tema.

Una solicitud de ejemplo de token de concesión de credenciales de cliente:

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

Una respuesta de ejemplo de token de concesión de credenciales de cliente:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>Obtención del id. de objeto de entidad de servicio de aplicación en la instancia de Azure AD de usuario
Ahora, utilice Hola de tooquery token de acceso de solo aplicación Hola [entidades de servicio de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) Hola de toodetermine API Id. de objeto de entidad de servicio de la aplicación hello en el directorio de Hola.

Hola [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) método de hello aplicación de ejemplo de ASP.net MVC implementa esta llamada.

Hola siguiente ejemplo se muestra cómo toorequest entidad de servicio de la aplicación. a0448380-c346-4f9f-b897-c18733de9394 es el identificador de cliente de Hola de aplicación hello.

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

Hello en el ejemplo siguiente se muestra una respuesta toohello solicitud de servicio de la aplicación principal

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>Obtención del identificador del rol RBAC de Azure
tooassign Hola adecuado RBAC tooyour servicio de rol entidad de seguridad, debe determinar identificador hello del rol de hello RBAC de Azure.

rol RBAC correcto de Hello para la aplicación:

* Si la aplicación solo supervisa la suscripción de hello, sin realizar ningún cambio, requiere solo permisos de lector de suscripción de Hola. Asignar Hola **lector** rol.
* Si la aplicación administra la suscripción de Azure hello, crear, modificar o eliminar entidades, requiere uno de los permisos de colaborador de Hola.
  * toomanage un determinado tipo de recurso, asignar roles de colaborador específico del recurso de hello (colaborador de la máquina Virtual, colaborador de red Virtual, colaborador de la cuenta de almacenamiento, etcetera.)
  * toomanage cualquier tipo de recurso, asignar Hola **colaborador** rol.

asignación de roles de Hello para la aplicación es toousers visible, por lo que seleccione Hola requiere menos privilegios.

Llamar a hello [definición de roles de administrador de recursos API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist todas las funciones de RBAC de Azure y búsqueda, a continuación, recorrer en iteración Hola Hola de toofind resultado deseado de definición de función por su nombre.

Hola [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) método de hello aplicación de ejemplo de ASP.net MVC implementa esta llamada.

solicitud de siguiente de Hello en el ejemplo se muestra cómo tooget identificador de rol de RBAC de Azure. 09cbd307-aa71-4aca-b346-5f253e6e3ebb es el Id. de Hola de suscripción de Hola.

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

respuesta de Hello es Hola siguiendo el formato:

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

No es necesario toocall esta API de forma continuada. Una vez que haya determinado Hola GUID conocido de definición de roles de hello, puede construir Id. de definición de rol de hello como:

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

Estos son Hola GUID conocido de uso frecuente funciones integradas:

| Rol | Guid |
| --- | --- |
| Lector |acdd72a7-3385-48ef-bd42-f606fba81ae7 |
| Colaborador |b24988ac-6180-42a0-ab88-20f7382dd24c |
| Colaborador de la máquina virtual |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| Colaborador de la red virtual |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| Colaborador de la cuenta de almacenamiento |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| Colaborador de sitio web |de139f84-1756-47ae-9be6-808fbbe84772 |
| Colaborador de plan web |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| Colaborador de SQL Server |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| Colaborador de SQL DB |9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>Asignar RBAC rol tooapplication
Todo lo que necesita tooassign Hola adecuado RBAC rol tooyour entidad de servicio mediante el uso de hello tiene [Administrador de recursos de crear la asignación de roles](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.

Hola [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) método de hello aplicación de ejemplo de ASP.net MVC implementa esta llamada.

Un ejemplo solicitud tooassign RBAC rol tooapplication:

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

En la solicitud de hello, se utiliza Hola siguientes valores:

| Guid | Description |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |Id. de Hola de suscripción de Hola |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |Id. de objeto de Hola de entidad de servicio de Hola de aplicación hello |
| acdd72a7-3385-48ef-bd42-f606fba81ae7 |Id. de Hello del rol de lector de Hola |
| 4f87261d-2816-465d-8311-70a27558df4c |un nuevo guid creado para la nueva asignación de roles Hola |

respuesta de Hello es Hola siguiendo el formato:

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>Obtención de token de acceso de solo aplicación para Azure Resource Manager
toovalidate que la aplicación tiene acceso de hello deseado en la suscripción de hello, lleve a cabo una tarea de prueba en suscripción de hello mediante un símbolo (token) solo de aplicación.

tooget un token de acceso de solo de aplicación, siga las instrucciones de la sección [obtener acceso de solo aplicación token para Azure AD Graph API](#app-azure-ad-graph), con un valor diferente para el parámetro de recurso de hello:

    https://management.core.windows.net/

Hola [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) método de aplicación de ejemplo de ASP.NET MVC obtiene acceso solo de aplicación símbolo (token) para usar el Administrador de recursos de Azure de hello Hola biblioteca de autenticación de Active Directory para. NET.

#### <a name="get-applications-permissions-on-subscription"></a>Obtención de permisos de la aplicación en la suscripción
toocheck que la aplicación ha Hola deseado de acceso en una suscripción de Azure, también puede llamar a hello [permisos de administrador de recursos](https://docs.microsoft.com/rest/api/authorization/permissions) API. Este enfoque es similar toohow determina si el usuario de hello tiene derechos de administración de acceso para la suscripción de Hola. Sin embargo, en este momento, llamar a API de permisos de hello con token de acceso de solo de aplicación de Hola que recibió en el paso anterior de Hola.

Hola [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) método de hello aplicación de ejemplo de ASP.NET MVC implementa esta llamada.

## <a name="manage-connected-subscriptions"></a>Administración de suscripciones conectadas
Cuando rol RBAC adecuado de Hola se asigna entidad de servicio de la aplicación tooyour de suscripción de hello, la aplicación puede mantener supervisión/administrando con tokens de acceso de solo de aplicación para el Administrador de recursos de Azure.

Si el propietario de la suscripción Quita la asignación de roles de la aplicación mediante el portal clásico de Hola o herramientas de línea de comandos, la aplicación es tooaccess ya no es capaz de esa suscripción. En ese caso, debe notificar al usuario de Hola que se ha roto la conexión de hello con suscripción de Hola desde la aplicación hello exterior y asígneles una opción demasiado "reparar" conexión de Hola. "Reparar" simplemente crearía volver a asignación de roles de Hola que se eliminó sin conexión.

Tal y como había habilitado aplicación tooyour de hello usuario tooconnect suscripciones, se deben permitir suscripciones de hello usuario toodisconnect. Desde un punto de vista de la administración de acceso, desconecte significa quitar asignación de roles de Hola que disponga de entidad de servicio de la aplicación hello en suscripción Hola. Opcionalmente, cualquier estado de aplicación hello para la suscripción de hello podría quitarse demasiado.
Solo los usuarios con permiso de administración de acceso de suscripción de hello son toodisconnect capaz de suscripción de Hola.

Hola [RevokeRoleFromServicePrincipalOnSubscription método](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) de hello MVC de ASP.net, aplicación de ejemplo implementa esta llamada.

Eso es todo: los usuarios ya pueden conectarse y administrar fácilmente sus suscripciones de Azure con su aplicación.
