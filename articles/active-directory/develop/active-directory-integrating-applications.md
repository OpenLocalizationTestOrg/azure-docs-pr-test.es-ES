---
title: aaaIntegrating aplicaciones con Azure Active Directory | Documentos de Microsoft
description: "Información detallada sobre cómo tooadd, actualizar o quitar una aplicación en Azure Active Directory (Azure AD)."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: mbaldwin
ms.assetid: ae637be5-0b71-4b1e-b1fe-b83df3eb4845
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: lenalepa
ms.custom: aaddev
ms.reviewer: luleon
ms.openlocfilehash: c6bf1123bb3a4d78b55c1c55558e684fb844e687
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>Integración de aplicaciones con Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Los desarrolladores empresariales y proveedores de software como-servicio (SaaS) pueden desarrollar servicios comerciales en la nube o la línea de aplicaciones de negocio que se puede integrar con Azure Active Directory (Azure AD) tooprovide seguro iniciar sesión y la autorización para su servicios. toointegrate una aplicación o servicio con Azure AD, un desarrollador debe registrar primero detalles Hola de su aplicación con Azure AD a través de hello portal de Azure clásico.

Este artículo muestra cómo tooadd, actualizar o quitar una aplicación en Azure AD. Obtendrá información sobre los diferentes tipos de aplicaciones que se pueden integrar con Azure AD, cómo de hello tooconfigure su tooaccess aplicaciones otros recursos como las API web y mucho más.

vea toolearn más información acerca de los dos objetos de Azure AD de Hola que representan una relación de hello entre ellos, y la aplicación registrada [objetos de entidad de servicio y aplicación](active-directory-application-objects.md); toolearn más información acerca de las directrices de personalización de marca de Hola debe usar al desarrollar aplicaciones con Azure Active Directory, vea [directrices de personalización de marca para aplicaciones integradas](active-directory-branding-guidelines.md).

## <a name="adding-an-application"></a>Agregar una aplicación
Cualquier aplicación que desea que las capacidades de hello toouse de Azure AD debe registrarse primero en un inquilino de Azure AD. Este proceso de registro implica proporcionar a Azure AD detalles acerca de la aplicación, como la dirección URL de Hola donde se encuentra, Hola URL toosend respuestas después de que un usuario se autentica, Hola URI que identifica la aplicación hello y así sucesivamente.

Si va a compilar una aplicación web que solo se necesita inicio de sesión en toosupport para los usuarios en Azure AD, simplemente puede seguir estas instrucciones Hola. Si la aplicación necesita las credenciales o permisos API web de tooaccess tooa o tooallow a los usuarios de otras es necesario Azure AD a los inquilinos tooaccess, consulte [actualizar una aplicación](#updating-an-application) toocontinue de la sección Configuración de la aplicación.

### <a name="tooregister-a-new-application-in-hello-azure-portal"></a>tooregister una nueva aplicación Hola portal de Azure
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el panel de navegación izquierdo de hello, elija **más servicios**, haga clic en **registros de aplicaciones**y haga clic en **agregar**.
4. Siga las indicaciones de Hola y cree una nueva aplicación. Si desea ejemplos específicos de aplicaciones web o aplicaciones nativa, visite nuestras [guías de inicio rápido](active-directory-developers-guide.md).
  * Para aplicaciones Web, proporcione hello **dirección URL de inicio de sesión**, que es Hola dirección URL base de la aplicación, donde los usuarios pueden iniciar sesión en, por ejemplo, `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Para aplicaciones nativas, proporcionar un **URI de redireccionamiento**, que Azure AD usa tooreturn token respuestas. Escriba una aplicación de tooyour específico de valor,. por ejemplo`http://MyFirstAADApp`
5. Una vez completado el registro, Azure AD le asigna la aplicación un identificador de cliente único, hello identificador de aplicación. Se ha agregado la aplicación y se le llevará toohello página de inicio rápido de la aplicación. Dependiendo de si la aplicación es una aplicación web o nativa, verá opciones diferentes acerca de cómo aplicación tooyour de tooadd funcionalidades adicionales. Una vez agregada la aplicación, puede empezar a actualizar su toosign de los usuarios de aplicación tooenable en las API web de acceso en otras aplicaciones o configuren la aplicación multiempresa (que permite a otras organizaciones tooaccess la aplicación).

> [!NOTE]
> De forma predeterminada, el registro de aplicaciones de hello recién creado es tooallow configurado a los usuarios de su toosign de directorio de aplicación de tooyour.
> 
> 

## <a name="updating-an-application"></a>Actualización de una aplicación
Una vez que la aplicación se ha registrado con Azure AD, puede que necesite toobe actualiza tooprovide obtener acceso a las API tooweb, pondrá a disposición de otras organizaciones y mucho más. Esta sección describen distintas formas en que puede ser necesario tooconfigure aún más la aplicación. En primer lugar se iniciará una visión general de hello marco de consentimiento, que es toounderstand importante si va a compilar aplicaciones de API de recursos/que usarán las aplicaciones de cliente generadas por los desarrolladores de su organización o de otra organización.

Para obtener más información sobre Hola autenticación forma funciona en Azure AD, consulte [escenarios de autenticación para Azure AD](active-directory-authentication-scenarios.md).

### <a name="overview-of-hello-consent-framework"></a>Información general del marco de consentimiento de Hola
Marco de consentimiento de Azure AD le resultará fácil toodevelop web para varios inquilinos y las aplicaciones cliente nativas que necesitan tooaccess web API protegidas por un inquilino de Azure AD, diferente de hello uno donde se registra la aplicación de cliente de Hola. Estas API web incluyen hello Microsoft Graph API (tooaccess Azure Active Directory, Intune y servicios de Office 365) y otras API de servicios de Microsoft, además tooyour posee las API web. marco de Hola se basa en un usuario o un administrador que da su consentimiento tooan aplicación que solicita toobe registradas en el directorio, que puede implicar el acceso a datos de directorio.

Por ejemplo, si una aplicación cliente web necesita información del calendario tooread acerca del usuario de Hola de Office 365, dicho usuario será necesario tooconsent toohello cliente aplicación. Después de dar su consentimiento, aplicación de cliente de hello ser capaz de toocall Hola API Graph de Microsoft en nombre de usuario de Hola y usar la información del calendario Hola según sea necesario. Hola [Microsoft Graph API](https://graph.microsoft.io) proporciona acceso toodata en Office 365 (por ejemplo, calendarios y mensajes de Exchange, sitios y listas de SharePoint, los documentos de OneDrive, blocs de notas de OneNote, las tareas de programador, los libros de Excel, etc.), así como a los usuarios y grupos de Azure AD y otros objetos de datos de varios servicios de nube de Microsoft. 

marco de consentimiento de Hola se basa en OAuth 2.0 y sus distintos flujos, como el código de autorización concesión credenciales de cliente y grant, mediante clientes públicos o confidenciales. Mediante el uso de OAuth 2.0, Azure AD facilita toobuild posibles muchos tipos diferentes de aplicaciones de cliente, como en un teléfono, tableta, servidor o una aplicación web y obtener acceso a recursos toohello necesario.

Para obtener más información sobre el marco de consentimiento de hello, consulte [OAuth 2.0 en Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx), [escenarios de autenticación para Azure AD](active-directory-authentication-scenarios.md)y para obtener información sobre cómo obtener acceso no autorizado tooOffice 365 a través de Microsoft Graph, consulte [autenticación de la aplicación con Microsoft Graph](https://graph.microsoft.io/docs/authorization/auth_overview).

#### <a name="example-of-hello-consent-experience"></a>Ejemplo de Hola experiencia de consentimiento
Hello siguientes pasos le mostrarán cómo funciona la experiencia de consentimiento de hello para el desarrollador de la aplicación hello y usuario.

1. En la página de configuración de la aplicación de cliente web en hello portal de Azure, establezca permisos de Hola que requiere que la aplicación mediante los menús de Hola Hola sección permisos necesarios.
   
    ![Permisos tooother aplicaciones](./media/active-directory-integrating-applications/requiredpermissions.png)
2. Tenga en cuenta que se actualizaron los permisos de su aplicación, se ejecuta la aplicación hello, y un usuario es sobre toouse para hello primera vez. Si la aplicación hello no ha adquirido una aplicación Hola símbolo (token), de acceso o una actualización debe tooobtain de extremo de autorización toogo tooAzure de AD un código de autorización que puede ser utilizado tooacquire un nuevo acceso y token de actualización.
3. Si el usuario de hello ya no está autenticado, le pedirá toosign en tooAzure AD.
   
    ![Inicio de sesión de usuario o un administrador en tooAzure AD](./media/active-directory-integrating-applications/usersignin.png)
4. Después de hello usuario haya iniciado sesión, Azure AD determinará si es usuario de Hola necesario toobe que se muestra una página de consentimiento. Esta determinación se basa en si el usuario de hello (o el Administrador de su organización) haya concedido ya consentimiento de aplicación Hola. Si no se ha concedido ya consentimiento, Azure AD le solicitará el consentimiento del usuario hello y mostrará los permisos de hello necesario que necesita toofunction. conjunto de Hola de permisos que se muestra en el cuadro de diálogo de consentimiento de Hola se Hola igual que lo que se ha seleccionado en permisos delegados de Hola Hola portal de Azure.
   
    ![Experiencia de consentimiento de usuario](./media/active-directory-integrating-applications/consent.png)
5. Después de usuario de hello concede el consentimiento, se devuelve un código de autorización aplicación tooyour, que puede ser recuperada tooacquire un token de acceso y token de actualización. Para obtener más información acerca de este flujo, vea hello [web de la sección aplicación tooweb API](active-directory-authentication-scenarios.md#web-application-to-web-api) sección [escenarios de autenticación para Azure AD](active-directory-authentication-scenarios.md).

6. Como administrador, también puede consentir permisos delegados de la aplicación tooan en nombre de todos los usuarios de hello en el inquilino. Esto impedirá que aparecen para todos los usuarios del inquilino de hello cuadro de diálogo de consentimiento de Hola. Puede hacerlo desde hello [portal de Azure](https://portal.azure.com) desde la página de aplicación. De hello **configuración** hoja para la aplicación, haga clic en **permisos necesarios** y haga clic en hello **conceder permisos** botón. 

    ![Concesión de permisos para el consentimiento explícito del administrador](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> Concesión de consentimiento explícito con hello **conceder permisos** botón actualmente se requiere para aplicaciones de una página (SPA) mediante ADAL.js, tal y como se solicita el token de acceso de hello sin preguntar al usuario su consentimiento, que se producirá un error si no se encuentra su consentimiento ya se ha concedido.   

### <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configurar una aplicación de cliente tooaccess web API
Para una tooparticipate de capaz de web/confidencial cliente aplicación toobe en un flujo de concesión de autorización que requiere autenticación (y obtener un token de acceso), debe establecer credenciales seguras. método de autenticación predeterminado de Hello admitido Hola portal de Azure es el Id. de cliente + clave simétrica. En esta sección se tratará clave secreta de hello configuración pasos necesarios tooprovide hello las credenciales de su cliente.

Además, antes de un cliente puede acceso a una API web expuestas por una aplicación de recursos (es decir: API Graph de Microsoft), marco de consentimiento de Hola se asegurará de cliente hello obtiene Hola permiso concedido permisos de hello necesarios, en función de solicitado. De forma predeterminada, todas las aplicaciones pueden elegir permisos de Azure Active Directory (API de Graph) y API de administración de servicios de Azure, con permiso de "Habilitar inicio de sesión y perfil de usuario de lectura" hello Azure AD ya seleccionado de forma predeterminada. Si la aplicación cliente está registrada en un inquilino de Azure AD de Office 365, las API web y los permisos de SharePoint y Exchange Online también estarán disponibles para seleccionarse. Puede seleccionar entre [dos tipos de permisos](active-directory-dev-glossary.md#permissions) Hola menús desplegables toohello siguiente deseado web API:

* Permisos de la aplicación: La aplicación cliente debe tooaccess hello web API directamente por sí misma (sin contexto de usuario). Este tipo de permiso requiere el consentimiento del administrador y no está disponible para aplicaciones cliente nativas.
* Permisos delegados: La aplicación cliente debe tooaccess hello web API como usuario con sesión iniciada hello, pero con acceso limitado por el permiso de hello seleccionado. Este tipo de permiso se puede conceder a un usuario a menos que el permiso de hello está configurada como la necesidad de consentimiento del administrador. 

> [!NOTE]
> Agregar una aplicación de tooan de permiso delegado no concede automáticamente consentimiento toohello usuarios dentro de inquilino de hello, tal y como se hacía en hello Portal clásico de Azure. Hello usuarios deben manualmente dar su consentimiento para hello agregado delega permisos en tiempo de ejecución, a menos que el Administrador de hello hace clic en hello **conceder permisos** botón de hello **permisos necesarios** sección de página de aplicación Hola Hola portal de Azure. 

#### <a name="tooadd-credentials-or-permissions-tooaccess-web-apis"></a>credenciales de tooadd o tooaccess permisos web API
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el menú superior de hello, elija **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, haga clic en aplicación hello desea tooconfigure. Esto se dirigirá la página de inicio rápido de la aplicación toohello, así como abrir la hoja de configuración de hello para la aplicación hello.
4. tooadd una clave secreta para las credenciales de la aplicación web, haga clic en la sección "Claves" de Hola de hoja de configuración de Hola.  
   
   * Agregue una descripción para la clave y seleccione 1 o 2 años de duración. 
   * columna del extremo derecho Hola contendrá clave-valor hello, después de guardar los cambios de configuración de Hola. Toocome seguro volver toothis sección y copiar después de llegar a ahorrar, por lo que tendrá para utilizan en la aplicación de cliente durante la autenticación en tiempo de ejecución.
5. tooadd permisos tooaccess API de recursos desde el cliente, haga clic en "Permisos necesarios" hello sección hoja de configuración de Hola. 
   
   * En primer lugar, haga clic en el botón de "Agregar" hello.
   * Haga clic en "Seleccionar una API" tooselect Hola de recursos que desee toopick desde.
   * Examine la lista de Hola de las API disponibles o use tooselect de cuadro de búsqueda de Hola desde aplicaciones de recursos disponibles de hello en el directorio que exponen una API web. Haga clic en recurso de Hola que está interesado en, a continuación, haga clic en **seleccione**.
   * Una vez seleccionado, puede mover toohello **permisos Select** menú, donde puede seleccionar Hola "permisos de la aplicación" y "Permisos delegados" para la aplicación.
   
6. Cuando termine, haga clic en hello **realiza** botón.

> [!NOTE]
> Si hace clic en hello **realiza** botón establece automáticamente permisos de hello para la aplicación en el directorio de aplicaciones basadas en permisos de hello tooother que ha configurado.  Puede ver estos permisos de aplicación mirando la aplicación hello **configuración** hoja.
> 
> 

### <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configuración de una aplicación de recursos tooexpose web API
Puede desarrollar una API web y hacerla disponible tooclient aplicaciones mediante la exposición de acceso [ámbitos](active-directory-dev-glossary.md#scopes) y [roles](active-directory-dev-glossary.md#roles). Una API web configurada correctamente debe ponerse a disposición como Hola otras API, incluidos Hola API Graph de web de Microsoft y Hola API de Office 365. Los ámbitos y los roles de acceso se exponen a través del [manifiesto de la aplicación](active-directory-dev-glossary.md#application-manifest), que es un archivo JSON que representa la configuración de identidad de la aplicación.  

Hola siguiente sección le mostrará cómo tooexpose acceso ámbitos, mediante la modificación de manifiesto de la aplicación de recursos de Hola.

#### <a name="adding-access-scopes-tooyour-resource-application"></a>Agregar aplicación de recursos de tooyour de ámbitos de acceso
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el menú superior de hello, elija **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, haga clic en aplicación hello desea tooconfigure. Esto se dirigirá la página de inicio rápido de la aplicación toohello, así como abrir la hoja de configuración de hello para la aplicación hello.
4. Haga clic en **manifiesto** de hello aplicación página tooopen Hola alineado editor de manifiestos. 
5. Reemplace "oauth2Permissions" nodo con hello siguiente fragmento de JSON. Este fragmento de código es un ejemplo de cómo tooexpose un ámbito que se denomina "suplantación de usuario", lo que permite un toogive de propietario de recursos en una aplicación cliente de un tipo de delegado acceso tooa recursos. Asegúrese de cambiar texto hello y valores para su propia aplicación:
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow hello application full access toohello Todo List service on behalf of hello signed-in     user",
            "adminConsentDisplayName": "Have full access toohello Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow hello application full access toohello todo service on your behalf",
            "userConsentDisplayName": "Have full access toohello todo service",
            "value": "user_impersonation"
            }
        ],
   
    valor de identificador Hello debe ser un GUID generado nuevo que se crea mediante un [herramienta de generación de GUID](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx) o mediante programación. Representa un identificador único para el permiso de Hola que se expone mediante la API web de Hola. Una vez que el cliente está configurado correctamente tooyour web API de toorequest acceso y las llamadas API web de Hola, presentará un token de JWT de OAuth 2.0 que tiene Hola ámbito (scp) notificación conjunto toohello valor anterior, que en este caso es user_impersonation.
   
   > [!NOTE]
   > Puede exponer ámbitos adicionales posteriormente si es necesario. Tenga en cuenta que la API web podría exponer varios ámbitos asociados a diversas funciones diferentes. Ahora puede controlar la notificación de API web mediante el uso de ámbito (scp) de hello toohello de acceso en el token de JWT de OAuth 2.0 Hola recibido.
   > 
   > 
6. Haga clic en **guardar** toosave manifiesto de Hola. La web que API está ahora configurado toobe usado por otras aplicaciones en el directorio.

#### <a name="tooverify-hello-web-api-is-exposed-tooother-applications-in-your-directory"></a>API de web de hello tooverify es tooother expuesto aplicaciones del directorio
1. En el menú superior de hello, haga clic en **registros de aplicación**, seleccione Hola deseado de aplicación de cliente que desee tooconfigure acceso toohello web API y navegar por hoja de configuración de toohello.
2. De hello **permisos necesarios** sección, seleccione hello web API que acaba de exponer un permiso. Desde el menú desplegable de hello permisos delegados, seleccione Nuevo permiso de Hola.

![Se muestran los permisos de la lista de tareas](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-hello-application-manifest"></a>Obtener más información sobre el manifiesto de aplicación Hola
manifiesto de aplicación Hola realmente actúa como un mecanismo para actualizar la entidad de aplicación hello, que define todos los atributos de configuración de identidad de una aplicación de Azure AD, incluidos los ámbitos de acceso de API de hello analizamos. Para obtener más información sobre Hola entidad de aplicación, vea hello [documentación de entidad de aplicación de API de Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity). En él, encontrará información de referencia completa en hello aplicación entidad miembros utilizados toospecify permisos de la API:  

* miembro de appRoles Hello, que es una colección de [AppRole](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type) entidades que pueden ser utilizados toodefine hello **permisos de aplicación** para una API web  
* miembro de oauth2Permissions Hello, que es una colección de [OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type) entidades que pueden ser utilizados toodefine hello **permisos delegados** para una API web

Para obtener más información sobre la aplicación de conceptos de manifiesto en general, consulte demasiado[manifiesto de aplicación en Azure Active Directory descripción hello](active-directory-application-manifest.md).

### <a name="accessing-hello-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>Hola acceso a Azure AD Graph y Office 365 a través de la API de gráficos de Microsoft  
Como los mencionados anteriormente, además tooexposing/obtener acceso a las API en sus propias aplicaciones de recursos, también puede actualizar su tooaccess de aplicación de cliente API expuestas por los recursos de Microsoft.  Hola API de Graph de Microsoft, que se denomina "Microsoft Graph" en la lista de Hola de aplicaciones de tooother de permisos, está disponible o en todas las aplicaciones que se registran con Azure AD. Si va a registrar la aplicación cliente en un inquilino de Azure AD que se haya proporcionado por Office 365, puede tener acceso todos los permisos de hello expuestos por hello Microsoft Graph API toovarious recursos de Office 365.

Para una descripción completa de los ámbitos de acceso expuesto por la API de Microsoft Graph, vea hello [ámbitos de permiso | Conceptos de API de Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes) artículo.

> [!NOTE]
> Debido a las limitaciones actuales tooa, las aplicaciones cliente nativas solo pueden llamar a hello Azure AD Graph API si usan el permiso de "Acceso al directorio de su organización" Hola.  Esta restricción no se aplica a las aplicaciones web.
> 
> 

### <a name="configuring-multi-tenant-applications"></a>Configuración de aplicaciones multiempresa
Cuando se agrega un tooAzure de aplicación AD, puede que desee su toobe de aplicación solo accedan los usuarios de su organización. Como alternativa, puede que desee su toobe aplicación accedan los usuarios de organizaciones externas. Estos dos tipos de aplicaciones se denominan aplicaciones multiempresa y aplicaciones de un solo inquilino. Puede modificar configuración de Hola de un toomake de aplicación de un solo inquilino, una aplicación de varios inquilinos, que en esta sección se describe a continuación.

Es importante toonote diferencias de hello entre un solo inquilino y una aplicación de varios inquilinos:  

* La finalidad de una aplicación de un solo inquilino es su uso en una sola organización. Suele tratarse de aplicaciones de línea de negocio (LOB) escritas por un desarrollador de la empresa. Una aplicación de un solo inquilino solo necesita toobe tienen acceso los usuarios en un directorio y, como resultado, solo necesita toobe aprovisiona en un directorio.
* La finalidad de una aplicación multiempresa es su uso en muchas organizaciones. Se trata de aplicaciones web de software como servicio (SaaS) que suelen ser creadas por un proveedor de software independiente (ISV). Las aplicaciones de varios inquilinos necesitan toobe aprovisionado en cada directorio donde se van a utilizar, lo que requiere tooregister de consentimiento de usuario o el administrador les admite a través del marco de consentimiento de hello Azure AD. Tenga en cuenta que todas las aplicaciones de cliente nativo multiempresa de forma predeterminada tal y como están instalados en el dispositivo del propietario del recurso de Hola. Vea Hola información general de hello sección del marco de consentimiento anterior para obtener más detalles en el marco de consentimiento de Hola.

#### <a name="enabling-external-users-toogrant-your-application-access-tootheir-resources"></a>Habilitar usuarios externos toogrant los recursos de tootheir de acceso de aplicación
Si está escribiendo una aplicación que desea toomake tooyour disponibles clientes o socios fuera de su organización, deberá tooupdate definición de la aplicación Hola Hola portal de Azure.

> [!NOTE]
> Al habilitar el tipo multiinquilino, debe asegurarse de que el URI del identificador de la aplicación pertenece a un dominio comprobado. Además, la dirección URL de retorno de Hola debe comenzar con https://. Para obtener más información, vea [Objetos de aplicación y objetos de entidad de servicio](active-directory-application-objects.md).
> 
> 

tooenable acceso tooyour aplicación para usuarios externos: 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el menú superior de hello, elija **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, haga clic en aplicación hello desea tooconfigure. Esto se dirigirá la página de inicio rápido de la aplicación toohello, así como abrir la hoja de configuración de hello para la aplicación hello.
4. En la hoja de configuración de hello, haga clic en **propiedades** hello voltear y **con inquilinos múltiples** cambiar demasiado**Sí**.

Una vez haya realizado Hola cambiar anteriormente, los usuarios y administradores de otras organizaciones será capaz de toogrant su directorio de tootheir de acceso de aplicación y otros datos.

#### <a name="triggering-hello-azure-ad-consent-framework-at-runtime"></a>Desencadenar el marco de consentimiento de hello Azure AD en tiempo de ejecución
marco de consentimiento de hello toouse, las aplicaciones cliente de varios inquilinos deben solicitar autorización mediante OAuth 2.0. [Ejemplos de código](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant) están disponible tooshow cómo una aplicación web, la aplicación nativa o la autorización de las solicitudes de aplicación de demonio/servidor códigos y tener acceso a los tokens de toocall las API web.

Es posible que la aplicación web ofrezca también una experiencia de suscripción para los usuarios. Si ofrece una experiencia de inicio de sesión, se espera que ese usuario Hola hará clic en un botón de suscripción que redirección Hola explorador toohello OAuth2.0 de Azure AD autorizará extremo o un punto de conexión OpenID Connect de la información de usuario. Estos extremos permiten Hola aplicación tooget saber nuevo usuario de hello inspeccionando id_token Hola. Después de la fase de inicio de sesión de hello usuario Hola aparecerá con un toohello similar prompt de consentimiento se muestra anteriormente en hello información general de hello sección del marco de consentimiento.

Como alternativa, la aplicación web también puede ofrecer una experiencia que permite a los administradores demasiado "suscribir mi compañía". Esta experiencia también podría redireccionar Hola usuario toohello Azure AD OAuth 2.0 extremo authorize. En este caso, sin embargo, pasar un símbolo del sistema = admin_consent toohello parámetro autorizar extremo tooforce Hola administrador experiencia de consentimiento, donde el Administrador de hello concederá consentimiento en nombre de su organización. Solo un usuario que se autentica con una cuenta que pertenezca el rol de administrador Global de toohello puede dar su consentimiento; otros usuarios recibirán un error. En el consentimiento correcto, respuesta de hello contendrá admin_consent = true. Al canjear un token de acceso, también recibirá un id_token que proporcionará información sobre la organización de Hola y el Administrador de Hola que registró para la aplicación.

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>Habilitación de la concesión implícita de OAuth 2.0 para aplicaciones de una sola página
Normalmente están estructurada única página de la aplicación (SPAs) con un front-end pesado de JavaScript que se ejecuta en el Explorador de hello, que llama tooperform de back-end de API web de la aplicación hello su lógica de negocios. Para SPAs hospedados en Azure AD, que usar usuario de concesión implícita OAuth 2.0 tooauthenticate Hola con Azure AD y obtener un token que puede usar toosecure devuelve la llamada de tooits de cliente de JavaScript de la aplicación hello final web API. Después de usuario de hello concedió consentimiento, este mismo protocolo de autenticación puede ser usado tooobtain tokens toosecure llamadas entre el cliente de Hola y otros recursos de API web configurados para la aplicación hello. toolearn más información sobre concesión de autorización implícita de Hola y ayudarle a decidir si es adecuado para su escenario de aplicaciones, consulte [Hola descripción OAuth2 implícita conceder flujo en Azure Active Directory ](active-directory-dev-understanding-oauth2-implicit-grant.md).

De forma predeterminada, la concesión implícita de OAuth 2.0 está deshabilitada para las aplicaciones. Puede habilitar la concesión implícita OAuth 2.0 para la aplicación por establecer hello `oauth2AllowImplicitFlow` valor en su [manifiesto de aplicación](active-directory-application-manifest.md), que es un archivo JSON que representa la configuración de la identidad de la aplicación.

#### <a name="tooenable-oauth-20-implicit-grant"></a>concesión implícita OAuth 2.0 tooenable
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el menú superior de hello, elija **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, haga clic en aplicación hello desea tooconfigure. Esto se dirigirá la página de inicio rápido de la aplicación toohello, así como abrir la hoja de configuración de hello para la aplicación hello.
4. En la página de aplicación Hola, haga clic en **manifiesto** editor de manifiestos de tooopen hello en línea.
   Busque y establezca el valor de "oauth2AllowImplicitFlow" hello demasiado "true". De forma predeterminada, es "false".
   
    `"oauth2AllowImplicitFlow": true,`
5. Guarde el manifiesto de hello actualizado. Una vez guardado, web que API está configurado ahora los usuarios tooauthenticate de concesión implícita OAuth 2.0 toouse.


## <a name="removing-an-application"></a>Eliminación de una aplicación
Esta sección describe cómo tooremove una aplicación de Azure AD de inquilinos.

### <a name="removing-an-application-authored-by-your-organization"></a>Eliminación de una aplicación creada por su organización
Estas son aplicaciones de Hola que se muestran en filtro de "Las aplicaciones que tiene mi compañía" hello en página principal de "Aplicaciones" de hello para el inquilino de Azure AD. En términos técnicos, estas aplicaciones registradas manualmente a través del portal de Azure clásico hello, o mediante programación a través de PowerShell u Hola API Graph. Más específicamente, se representan mediante un objeto Application y ServicePrincipal en el inquilino. Para más información, consulte [Objetos Application y objetos ServicePrincipal](active-directory-application-objects.md) .

#### <a name="tooremove-a-single-tenant-application-from-your-directory"></a>tooremove una aplicación de un solo inquilino de su directorio
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el menú superior de hello, elija **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, haga clic en aplicación hello desea tooconfigure. Esto se dirigirá la página de inicio rápido de la aplicación toohello, así como abrir la hoja de configuración de hello para la aplicación hello.
4. En la página de aplicación Hola, haga clic en **eliminar**.
5. Haga clic en **Sí** en el mensaje de confirmación de saludo.

#### <a name="tooremove-a-multi-tenant-application-from-your-directory"></a>tooremove una aplicación multiempresa de su directorio
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Elija al inquilino de Azure AD seleccionando su cuenta en hello superior derecho de la página de Hola.
3. En el menú superior de hello, elija **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, haga clic en aplicación hello desea tooconfigure. Esto se dirigirá la página de inicio rápido de la aplicación toohello, así como abrir la hoja de configuración de hello para la aplicación hello.
4. En la hoja de configuración de hello, elija **propiedades** hello voltear y **con inquilinos múltiples** cambiar demasiado**No**. Esto convierte a su aplicación toobe un solo inquilino, pero la aplicación hello seguirá estando en una organización que ya se ha dado su consentimiento tooit.
5. Haga clic en hello **eliminar** botón desde la página de aplicación Hola.
6. Haga clic en **Sí** en el mensaje de confirmación de saludo.

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>Eliminación de una aplicación multiinquilino autorizada por otra organización
Se trata de un subconjunto de las aplicaciones de Hola que se muestran en hello "Aplicaciones que usa mi compañía" filtro en la página de principal "Applications" hello para el inquilino de Azure AD, Hola específicamente los que no aparecen en la lista de "Aplicaciones que tiene mi compañía" Hola. En términos técnicos, estas son aplicaciones de varios inquilinos registradas durante el proceso de consentimiento de Hola. Más específicamente, se representan solo mediante un objeto ServicePrincipal en su inquilino. Para más información, consulte [Objetos Application y objetos ServicePrincipal](active-directory-application-objects.md) .

En orden tooremove directorio de la aplicación de varios inquilinos acceso tooyour (después de haber concedido el consentimiento), Administrador de la compañía de hello debe tener un acceso de tooremove de suscripción de Azure a través de hello portal de Azure. Como alternativa, el Administrador de empresa de hello puede usar hello [Cmdlets de PowerShell de Azure AD](http://go.microsoft.com/fwlink/?LinkId=294151) tooremove acceso.

## <a name="next-steps"></a>Pasos siguientes
* Vea hello [directrices de personalización de marca para aplicaciones integradas](active-directory-branding-guidelines.md) para obtener sugerencias sobre guía visual para la aplicación.
* Para obtener más detalles sobre la relación de hello entre objetos de aplicación y entidad de servicio de una aplicación, consulte [objetos de entidad de servicio y aplicación](active-directory-application-objects.md).
* toolearn más información acerca de Hola Hola aplicación manifiesto juegos de roles, consulte [manifiesto de aplicación en Azure Active Directory descripción Hola](active-directory-application-manifest.md)
* Vea hello [Glosario de Azure AD para desarrolladores](active-directory-dev-glossary.md) para obtener definiciones de algunos de los conceptos de desarrollador de hello principales Azure Active Directory (AD).
* Visite hello [Guía del desarrollador de Active Directory](active-directory-developers-guide.md) para obtener información general de todos los desarrolladores de contenido relacionado.

