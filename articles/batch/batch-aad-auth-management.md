---
title: "soluciones de administración de lotes de aaaUse Azure Active Directory tooauthenticate | Documentos de Microsoft"
description: Las aplicaciones compilan con el Administrador de recursos de Azure y proveedor de recursos de proceso por lotes de hello autenticarse con Azure AD.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>Autenticación de soluciones de administración de Batch con Active Directory

Las aplicaciones que llaman a servicio de administración de lotes de Azure de hello autenticarse con [Azure Active Directory] [ aad_about] (Azure AD). Azure Active Directory es el directorio basado en la nube multiinquilino y el servicio de administración de identidades de Microsoft. Azure por sí mismo utiliza Azure AD para la autenticación de Hola de sus clientes, los administradores de servicios y usuarios de la organización.

biblioteca de .NET de administración de lotes de Hello expone tipos para trabajar con cuentas de lote, las claves de cuenta, aplicaciones y paquetes de aplicaciones. biblioteca de .NET de administración de lotes de Hello es un cliente de proveedor de recursos de Azure y se utiliza junto con [Azure Resource Manager] [ resman_overview] toomanage estos recursos mediante programación. Azure AD es las solicitudes de tooauthenticate necesario realizadas a través de cualquier cliente de proveedor de recursos de Azure, incluidos la biblioteca de .NET de administración de lotes de hello y [Azure Resource Manager][resman_overview].

En este artículo se explican cómo utilizar el tooauthenticate de Azure AD desde las aplicaciones que utilizan la biblioteca de .NET de administración de lotes de Hola. Le mostramos cómo toouse Azure AD tooauthenticate un administrador de la suscripción o Coadministrador, mediante la autenticación integrada. Usamos hello [AccountManagment] [ acct_mgmt_sample] proyecto de ejemplo, disponible en GitHub, toowalk a través mediante Azure AD con la biblioteca de .NET de administración de lotes de Hola.

vea toolearn más sobre el uso de la biblioteca de .NET de administración de lotes de Hola y ejemplo de Hola a AccountManagement, [lote administrar cuentas y cuotas con la biblioteca de cliente de administración de lotes de Hola para .NET](batch-management-dotnet.md).

## <a name="register-your-application-with-azure-ad"></a>Registro de la aplicación con Azure AD

Hello Azure [biblioteca de autenticación de Active Directory] [ aad_adal] (AAL) proporciona una interfaz de programación de tooAzure AD para su uso dentro de las aplicaciones. toocall AAL desde su aplicación, debe registrar la aplicación en un inquilino de Azure AD. Al registrar la aplicación, se facilita Azure AD con información acerca de la aplicación, incluido un nombre para ella en el inquilino de Azure AD Hola. Azure AD, a continuación, proporciona un identificador de la aplicación usa tooassociate de su aplicación con Azure AD en tiempo de ejecución. vea toolearn más información sobre el identificador de la aplicación hello [aplicación y objetos de entidad de servicio en Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

Hola tooregister aplicación de ejemplo de AccountManagement, siga los pasos de Hola Hola [agregar una aplicación](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sección [integrar aplicaciones con Azure Active Directory] [ aad_integrate]. Especifique **aplicación cliente nativa** para el tipo de saludo de la aplicación. Hola sector estándar OAuth 2.0 URI para hello **URI de redireccionamiento** es `urn:ietf:wg:oauth:2.0:oob`. Sin embargo, puede especificar cualquier URI válido (como `http://myaccountmanagementsample`) para hello **URI de redireccionamiento**, ya que no es necesario toobe un punto de conexión real:

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

Cuando se haya completado el proceso de registro de hello, verá Id. de aplicación de Hola y Hola identificador de objeto (entidad de servicio) que aparece para la aplicación.  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>Conceda acceso tooyour aplicación de hello API del Administrador de recursos de Azure

A continuación, deberá toodelegate acceso tooyour aplicación toohello API del Administrador de recursos de Azure. identificador de Hello Azure AD para hello API del Administrador de recursos es **API de administración de servicios de Windows Azure**.

Siga estos pasos en hello portal de Azure:

1. En el panel de navegación izquierdo de Hola de hello portal de Azure, elija **más servicios**, haga clic en **registros de aplicaciones**y haga clic en **agregar**.
2. Busque el nombre de saludo de la aplicación en la lista de Hola de registros de aplicación:

    ![Buscar el nombre de la aplicación](./media/batch-aad-auth-management/search-app-registration.png)

3. Hola de presentación **configuración** hoja. Hola **el acceso de API** sección, seleccione **los permisos necesarios**.
4. Haga clic en **agregar** tooadd un nuevo permiso requerido. 
5. En el paso 1, escriba **API de administración de servicios de Windows Azure**, seleccione esa API de lista de Hola de resultados y haga clic en hello **seleccione** botón.
6. En el paso 2, seleccione Hola casilla de verificación junto demasiado**modelo de implementación clásica de Azure de acceso como los usuarios de la organización**y haga clic en hello **seleccione** botón.
7. Haga clic en hello **realiza** botón.

Hola **permisos necesarios** hoja ahora muestra que aplicación de tooyour permisos se conceden tooboth Hola AAL y las API del Administrador de recursos. Se conceden permisos tooADAL de forma predeterminada al registrar primero la aplicación con Azure AD.

![Delegar permisos toohello API del Administrador de recursos de Azure](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Puntos de conexión de Azure AD

tooauthenticate sus soluciones de administración de lotes con Azure AD, necesitará dos puntos de conexión conocidos.

- Hola **extremo comunes de Azure AD** proporciona una credencial genérica recopilación interfaz cuando no se proporciona un inquilino específico, como en caso de hello de la autenticación integrada:

    `https://login.microsoftonline.com/common`

- Hola **punto de conexión de Azure Resource Manager** es tooacquire usa un token para autenticar el servicio de administración de solicitudes toohello por lotes:

    `https://management.core.windows.net/`

aplicación de ejemplo de AccountManagement Hola define las constantes para estos puntos de conexión. No cambie estas constantes:

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>Referencia al identificador de aplicación 

La aplicación cliente usa tooaccess (también denominado tooas Hola Id. de cliente) de Id. de aplicación hello Azure AD en tiempo de ejecución. Una vez que ha registrado su aplicación Hola portal de Azure, actualice el identificador de aplicación de código toouse Hola proporcionado por Azure AD para la aplicación registrada. En la aplicación de ejemplo de AccountManagement hello, copie el identificador de la aplicación de constante adecuada de hello toohello de portal de Azure:

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
Copie también URI especificado durante el proceso de registro de hello de redirección de Hola. Hola redirección URI especificado en el código debe coincidir con el URI que proporcionó al registrar la aplicación hello de redirección de Hola.

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>Adquisición de un token de autenticación de Azure AD

Después de registrar el ejemplo de Hola AccountManagement en inquilino de Azure AD de Hola y actualizar el código fuente de ejemplo de Hola con sus valores, el ejemplo hello es tooauthenticate listo con Azure AD. Al ejecutar el ejemplo hello, Hola AAL intenta tooacquire un token de autenticación. En este paso, le pedirá las credenciales de Microsoft: 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

Después de proporcionar sus credenciales, aplicación de ejemplo de Hola puede continuar tooissue autenticado las solicitudes toohello servicio de administración de proceso por lotes. 

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de cómo ejecutar hello [aplicación de ejemplo de AccountManagement][acct_mgmt_sample], consulte [lote administrar cuentas y cuotas con la biblioteca de cliente de administración de lotes de Hola para .NET](batch-management-dotnet.md).

toolearn más información acerca de Azure AD, vea hello [documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/). Ejemplos detallados que muestran cómo toouse AAL está disponible en hello [ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteca.

las aplicaciones de servicio de lote tooauthenticate mediante Azure AD, vea [soluciones de servicio de lote autenticarse con Active Directory](batch-aad-auth.md). 


[aad_about]: ../active-directory/active-directory-whatis.md "¿Qué es Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Escenarios de autenticación para Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integración de aplicaciones con Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
