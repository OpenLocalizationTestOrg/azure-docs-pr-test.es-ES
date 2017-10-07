---
title: "aaaHow toowork con el servidor back-end de .NET Hola SDK para aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toowork con Hola servidor back-end de .NET SDK para aplicaciones de Mobile de servicio de aplicación de Azure."
keywords: "servicio de aplicaciones, servicio de aplicaciones de azure, aplicación móvil, servicio móvil, escala, escalable, implementación de aplicaciones, implementación de aplicaciones de azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>Trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Este tema muestra cómo toouse Hola servidor de back-end de .NET SDK en escenarios de aplicaciones móviles de Azure aplicación servicio clave. Hola SDK de aplicaciones móviles de Azure le ayuda a trabajar con clientes móviles desde la aplicación de ASP.NET.

> [!TIP]
> Hola [servidor .NET SDK para aplicaciones móviles de Azure] [ 2] es código abierto en GitHub. repositorio de Hello contiene todo el código fuente como conjunto de pruebas de unidad SDK de todo el servidor de Hola y algunos proyectos de ejemplo.
>
>

## <a name="reference-documentation"></a>Documentación de referencia
documentación de referencia de Hello para el servidor de hello SDK se encuentra aquí: [referencia de .NET de aplicaciones de Azure Mobile][1].

## <a name="create-app"></a>Creación de un back-end de aplicación móvil .NET
Si está iniciando un nuevo proyecto, puede crear una aplicación de servicio de aplicaciones con cualquier hello [portal de Azure] o Visual Studio. Puede ejecutar localmente Hola aplicación de servicio de aplicaciones o publicar el proyecto tooyour en la nube servicio de aplicaciones móvil aplicación hello.

Si va a Agregar proyecto existente de capacidades móviles tooan, vea hello [descargar e inicializar Hola SDK](#install-sdk) sección.

### <a name="create-a-net-backend-using-hello-azure-portal"></a>Crear un back-end de .NET mediante Hola portal de Azure
toocreate un back-end de servicio de aplicaciones móvil, ya sea siga hello [tutorial rápido] [ 3] o siga estos pasos:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

En hello *Introducción* hoja, en **crear una tabla API**, elija **C#** como su **idioma de back-end**. Haga clic en **descargar**, extraer el equipo de proyecto comprimido archivos tooyour local y abra la solución de hello en Visual Studio.

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>Creación de un back-end .NET con Visual Studio 2013 y Visual Studio 2015
Instalar hello [Azure SDK para .NET] [ 4] (versión 2.9.0 o posterior) toocreate un proyecto de aplicaciones móviles de Azure en Visual Studio. Una vez haya instalado el SDK de hello, crear una aplicación de ASP.NET con hello pasos:

1. Abra hello **nuevo proyecto** diálogo (desde *archivo* > **New** > **proyecto...** ).
2. Expanda **Plantillas** > **Visual C#** y seleccione **Web**.
3. Seleccione **Aplicación web ASP.NET**.
4. Rellene el nombre del proyecto de Hola. y, a continuación, haga clic en **Aceptar**.
5. En *Plantillas de ASP.NET 4.5.2*, seleccione **Aplicación móvil de Azure**. Comprobar **Host en la nube de hello** toocreate un back-end móvil Hola toowhich puede publicar este proyecto en la nube.
6. Haga clic en **Aceptar**.

## <a name="install-sdk"></a>Cómo: descargar e inicializar Hola SDK
Hello SDK está disponible en [NuGet.org]. Este paquete incluye Hola funcionalidad base necesaria tooget iniciado mediante Hola SDK. tooinitialize Hola SDK, deberá tooperform acciones en hello **HttpConfiguration** objeto.

### <a name="install-hello-sdk"></a>Instalar SDK de Hola
Hola tooinstall SDK, el botón secundario en el proyecto de servidor de hello en Visual Studio, seleccione **administrar paquetes de NuGet**, busque hello [Microsoft.Azure.Mobile.Server] del paquete, a continuación, haga clic en  **Instalar**.

### <a name="server-project-setup"></a>Inicializar el proyecto de servidor hello
Un proyecto de servidor de back-end de .NET es inicializado similar tooother los proyectos ASP.NET, mediante la inclusión de una clase de inicio OWIN. Asegúrese de que se ha hecho referencia paquete de NuGet hello `Microsoft.Owin.Host.SystemWeb`. tooadd esta clase en Visual Studio, haga clic en el proyecto de servidor y seleccione **agregar** >
**nuevo elemento**, a continuación, **Web**  >  ** General** > **clase de inicio de OWIN**.  Se genera una clase con hello siguiente atributo:

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

Hola `Configuration()` método de la clase de inicio OWIN, use un **HttpConfiguration** entorno de aplicaciones móviles de Azure de objetos tooconfigure Hola.
Hola siguiente ejemplo inicializa el proyecto de servidor de hello con ninguna característica agregada:

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable características individuales, deben llamar a métodos de extensión en hello **MobileAppConfiguration** objeto antes de llamar a **ApplyTo**. Por ejemplo, hello siguiente código agrega predeterminado Hola enruta controladores tooall API que tienen el atributo de hello `[MobileAppController]` durante la inicialización:

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

Inicio rápido de servidor Hello de Hola llamadas portales Azure **UseDefaultConfiguration()**. Este toohello equivalente después de la instalación:

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

métodos de extensión de Hello usados son:

* `AddMobileAppHomeController()`proporciona la página de inicio de aplicaciones móviles de Azure de hello predeterminada.
* `MapApiControllers()`proporciona capacidades de API personalizadas para los controladores de WebAPI decorados con hello `[MobileAppController]` atributo.
* `AddTables()`Proporciona una asignación de hello `/tables` controladores tootable de puntos de conexión.
* `AddTablesWithEntityFramework()`es un abreviada para hello asignación `/tables` controladores basados en los extremos que usan Entity Framework.
* `AddPushNotifications()` proporciona un método sencillo de registrar los dispositivos para Notification Hubs.
* `MapLegacyCrossDomainController()` proporciona los encabezados de CORS estándar para el desarrollo local.

### <a name="sdk-extensions"></a>Extensiones de SDK
Hola siguientes paquetes de NuGet-based extensión proporciona diversas características de dispositivos móviles que se pueden usar la aplicación. Habilitar extensiones durante la inicialización mediante hello **MobileAppConfiguration** objeto.

* [Microsoft.Azure.Mobile.Server.Quickstart] admite Hola configuración básica de aplicaciones móviles. La configuración agregada toohello Hola que realiza la llamada **UseDefaultConfiguration** método de extensión durante la inicialización. Esta extensión incluye las siguientes extensiones: paquetes de notificaciones, autenticación, entidad, tablas, entre dominios y principal. Inicio rápido de aplicaciones móviles disponibles en el portal de Azure Hola Hola utiliza este paquete.
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementa de forma predeterminada hello *esta aplicación móvil esté en funcionamiento página* para la raíz del sitio web de Hola. Agregar configuración toohello mediante una llamada a la **AddMobileAppHomeController** método de extensión.
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) incluye clases para trabajar con conjuntos de datos y de canalización de datos de Hola. Agregar configuración toohello Hola llamada **AddTables** método de extensión.
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) permite que los datos de tooaccess de Entity Framework Hola Hola base de datos SQL. Agregar configuración toohello Hola llamada **AddTablesWithEntityFramework** método de extensión.
* [Microsoft.Azure.Mobile.Server.Authentication] middleware de OWIN de Hola de autenticación y conjuntos de seguridad permite usa toovalidate símbolos (tokens). Agregar configuración toohello Hola llamada **AddAppServiceAuthentication** y **IAppBuilder**. **UseAppServiceAuthentication** métodos de extensión.
* [Microsoft.Azure.Mobile.Server.Notifications] habilita las notificaciones push y define un punto de conexión de registro de inserción. Agregar configuración toohello Hola llamada **AddPushNotifications** método de extensión.
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) crea un controlador que sirve datos toolegacy exploradores web desde su aplicación móvil. Agregar configuración toohello mediante una llamada a la **MapLegacyCrossDomainController** método de extensión.
* [Microsoft.Azure.Mobile.Server.Login] proporciona hello AppServiceLoginHandler.CreateToken() método, que es un método estático que se usa en escenarios de autenticación personalizado de.

## <a name="publish-server-project"></a>Cómo: Publicar proyecto de servidor hello
Esta sección muestra cómo toopublish el back-end de .NET proyecto de Visual Studio. También puede implementar el proyecto de back-end con Git o cualquiera de Hola otros métodos que se tratan en hello [documentación de implementación de servicio de aplicaciones de Azure](../app-service-web/web-sites-deploy.md).

1. En Visual Studio, vuelva a generar paquetes de NuGet de hello proyecto toorestore.
2. En el Explorador de soluciones, proyectos de Hola de menú contextual, haga clic en **publicar**. Hello primera vez que publique, deberá toodefine un perfil de publicación. Si ya tiene un perfil definido, puede seleccionarlo y hacer clic en **Publicar**.
3. Si se le solicita tooselect un destino de publicación, haga clic en **servicio de aplicaciones de Microsoft Azure** > **siguiente**, a continuación, (si es necesario) iniciar sesión con sus credenciales de Azure.
   Visual Studio descarga y almacena la configuración de publicación directamente desde Azure.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. Elija su suscripción en **Suscripción**, seleccione **Tipo de recurso** en **Vista**, expanda **Aplicación móvil** y haga clic en el back-end de aplicación móvil y en **Aceptar**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. Comprobar Hola publicar información del perfil y haga clic en **publicar**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    Cuando el back-end de la aplicación móvil se haya publicado correctamente, verá una página de aterrizaje que indica el éxito.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a> Definición de un controlador de tabla
Definir un controlador de tabla tooexpose los clientes un toomobile de tabla SQL.  La configuración de un controlador de tabla requiere tres pasos:

1. Creación de una clase Data Transfer Object (DTO).
2. Configurar una referencia de tabla en hello clase DbContext Mobile.
3. Creación de un controlador de tabla.

Un objeto de transferencia de datos (DTO) es un objeto de C# simple heredado de `EntityData`.  Por ejemplo:

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

Hola DTO es tabla de hello toodefine utilizados dentro de la base de datos SQL de Hola.  Hola toocreate entrada de la base de datos, agregue un `DbSet<>` propiedad a saludos DbContext utilizas.  En la plantilla de proyecto de hello predeterminada para las aplicaciones móviles de Azure, hello DbContext se denomina `Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

Si tiene instalado el SDK de Azure de Hola, ahora puede crear un controlador de tabla de plantilla como sigue:

1. Haga doble clic en la carpeta de controladores de Hola y seleccione **agregar** > **controlador...** .
2. Seleccione hello **controlador de tabla de aplicaciones de Azure Mobile** opción, a continuación, haga clic en **agregar**.
3. Hola **Agregar controlador** cuadro de diálogo:
   * Hola **clase modelo** de lista desplegable, seleccione el nuevo DTO.
   * Hola **DbContext** lista desplegable, clase de DbContext del servicio móvil de hello select.
   * nombre del controlador de Hola se crea automáticamente.
4. Haga clic en **Agregar**.

proyecto de servidor de inicio rápido de Hello contiene un ejemplo de un sencillo **TodoItemController**.

### <a name="adjust-pagesize"></a>Cómo: ajustar el tamaño de paginación de tabla Hola
De forma predeterminada, Aplicaciones móviles de Azure devuelve 50 registros por solicitud.  Paginación se asegura de que el cliente hello no atar su servidor de hello ni de subproceso de interfaz de usuario durante demasiado tiempo, garantizar una buena experiencia del usuario. tamaño de paginación de la tabla de hello toochange, lado del servidor aumento Hola "tamaño de consulta permitido" y hello página del lado cliente tamaño Hola servidor "tamaño de consulta permitido" se ajusta con hello `EnableQuery` atributo:

    [EnableQuery(PageSize = 500)]

Asegúrese de hello PageSize es hello mismo o mayor que el tamaño de hello solicitada por el cliente de Hola.  Consulte la documentación de cómo de cliente específico de toohello para obtener más información acerca de cómo cambiar el tamaño de página de cliente de Hola.

## <a name="how-to-define-a-custom-api-controller"></a>Cómo definir un controlador de API personalizada
controlador de API personalizada Hello proporciona hello más básico funcionalidad tooyour aplicación móvil back-end mediante la exposición de un punto de conexión. Puede registrar un controlador de API de mobile específica mediante el atributo Hola [MobileAppController]. Hola `MobileAppController` atributo registra ruta hello, configura el serializador de JSON de aplicaciones móviles de Hola y activará [comprobación de la versión de cliente](app-service-mobile-client-and-server-versioning.md).

1. En Visual Studio, la carpeta de controladores de menú contextual hello, a continuación, haga clic en **agregar** > **controlador**, seleccione **controlador de Web API 2&mdash;vacía** y Haga clic en **agregar**.
2. Proporcione un valor de **Nombre de controlador**, como `CustomController`, y haga clic en **Agregar**.
3. En el archivo de clase de controlador nuevo hello, agregue el siguiente de hello instrucción using:

        using Microsoft.Azure.Mobile.Server.Config;
4. Aplicar hello **[MobileAppController]** definición de clase de controlador toohello API, como en el siguiente ejemplo de Hola de atributo:

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. En el archivo de App_Start/Startup.MobileApp.cs, agregue una llamada toohello **MapApiControllers** método de extensión, como en el siguiente ejemplo de Hola:

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

También puede usar hello `UseDefaultConfiguration()` en lugar del método de extensión `MapApiControllers()`. Los clientes pueden tener acceso a un controlador aunque este no tenga un elemento **MobileAppControllerAttribute** aplicado, pero puede que no lo consuman correctamente si usan un SDK de cliente de aplicación móvil.

## <a name="how-to-work-with-authentication"></a>Procedimiento: Autenticación
Aplicaciones móviles de Azure usa la aplicación de servicio de autenticación / autorización toosecure el back-end de dispositivos móvil.  Esta sección muestra cómo hello tooperform siguientes tareas relacionadas con la autenticación en el proyecto de servidor de back-end. NET:

* [Cómo: Agregar proyecto de servidor de autenticación tooa](#add-auth)
* [Procedimiento: Uso de autenticación personalizada en la aplicación](#custom-auth)
* [Procedimiento: Recuperación de la información de usuario de autenticado](#user-info)
* [Cómo restringir el acceso a datos para los usuarios autorizados](#authorize)

### <a name="add-auth"></a>Cómo: Agregar proyecto de servidor de autenticación tooa
Puede agregar el proyecto de servidor de autenticación tooyour extendiendo hello **MobileAppConfiguration** objeto y la configuración de middleware de OWIN. Cuando instala hello [Microsoft.Azure.Mobile.Server.Quickstart] Hola de paquete y llame al método **UseDefaultConfiguration** método de extensión, puede omitir toostep 3.

1. En Visual Studio, instale hello [Microsoft.Azure.Mobile.Server.Authentication] paquete.
2. En el archivo de proyecto de hello Startup.cs, agregar Hola después de la línea de código al principio de Hola de hello **configuración** método:

        app.UseAppServiceAuthentication(config);

    Este componente de middleware OWIN valida tokens emitidos por la puerta de enlace de servicio de aplicaciones de hello asociado.
3. Agregar hello `[Authorize]` controlador tooany de atributo o un método que requiere autenticación.

toolearn acerca de cómo los clientes de tooauthenticate tooyour back-end de aplicaciones móviles, consulte [agregar autenticación tooyour aplicación](app-service-mobile-ios-get-started-users.md).

### <a name="custom-auth"></a>Procedimiento: Uso de autenticación personalizada en la aplicación
Si no desea toouse uno de los proveedores de autenticación/autorización del servicio de aplicación Hola, puede implementar su propio sistema de inicio de sesión. Instalar hello [Microsoft.Azure.Mobile.Server.Login] tooassist con generación de tokens de autenticación del paquete.  Proporcione su propio código para validar las credenciales del usuario. Por ejemplo, podría comprobar las contraseñas con sal y hash de una base de datos. En el siguiente ejemplo de Hola, Hola `isValidAssertion()` método (definido en otro lugar) es responsable de estas comprobaciones.

autenticación personalizada Hello se expone mediante la creación de un ApiController y exponer `register` y `login` acciones. cliente de Hello debería utilizar una información de hello toocollect de interfaz de usuario personalizada de usuario de Hola.  información de Hello es llamar a la API de toohello enviado con un estándar HTTP POST. Una vez que el servidor hello valida aserción hello, se emite un token con hello `AppServiceLoginHandler.CreateToken()` método.  Hola ApiController **no debería** usar hello `[MobileAppController]` atributo.

Ejemplo de la acción `login` :

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

En el anterior ejemplo de Hola, LoginResult y LoginResultUser son objetos serializables exponer propiedades necesarias. cliente de Hello espera toobe de respuestas de inicio de sesión devuelven como objetos JSON del formulario de hello:

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

Hola `AppServiceLoginHandler.CreateToken()` método incluye un *audiencia* y *emisor* parámetro. Ambos parámetros se establecen toohello URL de la raíz de la aplicación, con esquema HTTPS de Hola. Del mismo modo debe establecer *secretKey* toobe valor de saludo de la aplicación de la clave de firma. No distribuya Hola firma clave en un cliente puede ser toomint usa claves y suplantar a los usuarios. Puede obtener Hola firma clave mientras hospedada en el servicio de aplicaciones haciendo referencia a hello *sitio Web\_AUTH\_firma\_clave* variable de entorno. Si es necesario en un contexto de depuración local, siga las instrucciones de Hola Hola [depuración Local con autenticación](#local-debug) sección tooretrieve clave de Hola y almacenar como una configuración de aplicación.

También puede incluir el token emitido de Hello el resto de reclamaciones y una fecha de expiración.  Como mínimo, símbolo (token) de hello emitido debe incluir un asunto (**sub**) de notificación.

Puede admitir cliente estándar hello `loginAsync()` método mediante la sobrecarga de la ruta de autenticación de Hola.  Si llama a cliente hello `client.loginAsync('custom');` toolog en, la ruta debe ser `/.auth/login/custom`.  Puede establecer la ruta de hello para el uso de controlador de autenticación personalizada hello `MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> Con hello `loginAsync()` enfoque garantiza que se adjunta ese token de autenticación de hello tooevery llamada subsiguiente toohello servicio.
>
>

### <a name="user-info"></a>Procedimiento: Recuperación de la información de usuario de autenticado
Cuando un usuario se autentica por el servicio de aplicaciones, puede tener acceso a Hola asignado el Id. de usuario y otra información en el código de back-end. NET. información de usuario de Hello puede usarse para tomar las decisiones de autorización Hola back-end. Hello código siguiente obtiene Hola Id. de usuario asociada a una solicitud:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

Hola SID se deriva de Id. de usuario específica del proveedor de Hola y es estático para un usuario determinado y un proveedor de inicio de sesión.  Hola SID es null para los tokens de autenticación no válida.

El Servicio de aplicaciones también le permite solicitar notificaciones específicas de su proveedor de inicio de sesión. Cada proveedor de identidades puede proporcionar más información mediante el SDK del proveedor de identidades.  Por ejemplo, puede usar hello Graph API de Facebook para obtener información de amigos.  Puede especificar demandas solicitadas en la hoja de proveedor de Hola Hola portal de Azure. Algunas notificaciones requieren configuración adicional con el proveedor de identidades de Hola.

Hola de llamadas de código siguiente Hello **GetAppServiceIdentityAsync** extensión método tooget Hola credenciales inicio de sesión, que incluyen las solicitudes de token toomake necesarios de hello acceso contra Hola Graph API de Facebook:

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

Agregue un mediante declaración para `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** método de extensión.

### <a name="authorize"></a>Cómo restringir el acceso a datos para los usuarios autorizados
En la sección anterior de hello, mostramos cómo tooretrieve Hola Id. de usuario de un usuario autenticado. Puede restringir el acceso toodata y otros recursos en función de este valor. Por ejemplo, agregar un tootables de la columna de identificador de usuario y filtrar resultados de la consulta de Hola por Id. de usuario de hello son un toolimit de manera sencilla devuelve solo los usuarios tooauthorized datos. Hello código siguiente devuelve filas de datos solo cuando Hola SID coincide con el valor de columna de identificador de usuario de hello en la tabla TodoItem de hello:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

Hola `Query()` método devuelve un `IQueryable` que se pueden manipular mediante el filtrado de toohandle LINQ.

## <a name="how-to-add-push-notifications-tooa-server-project"></a>Cómo: Agregar proyecto de servidor de tooa de notificaciones de inserción
Agregar proyecto de servidor de tooyour de notificaciones de inserción mediante la extensión de hello **MobileAppConfiguration** objeto y la creación de un cliente de los centros de notificaciones.

1. En Visual Studio, haga clic en proyecto de servidor de Hola y haga clic en **administrar paquetes de NuGet**, busque `Microsoft.Azure.Mobile.Server.Notifications`, a continuación, haga clic en **instalar**.
2. Repita este Hola de tooinstall paso `Microsoft.Azure.NotificationHubs` paquete, que incluye la biblioteca de cliente de hello centros de notificaciones.
3. En App_Start/Startup.MobileApp.cs y agregue una llamada toohello **AddPushNotifications()** método de extensión durante la inicialización:

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. Agregue Hola después el código que crea a un cliente de los centros de notificaciones:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

Ahora puede usar Hola centros de notificaciones toosend inserción notificaciones tooregistered los dispositivos cliente. Para obtener más información, consulte [aplicación de tooyour de notificaciones de inserción de agregar](app-service-mobile-ios-get-started-push.md). toolearn más información acerca de los centros de notificaciones, consulte [información general de los centros de notificación](../notification-hubs/notification-hubs-push-notification-overview.md).

## <a name="tags"></a>Habilitación de la inserción de destino mediante etiquetas
Los centros de notificaciones le permite enviar notificaciones de destino toospecific registros mediante el uso de etiquetas. Se crean varias etiquetas automáticamente:

* Hola identificador de instalación identifica un dispositivo específico.
* Hello Id. de usuario basado en hello autenticado SID identifica a un usuario específico.

Hola instalación identificador puede tener acceso desde hello **installationId** propiedad hello **MobileServiceClient**.  Hello en el ejemplo siguiente se muestra cómo utilizar un tooadd de Id. de instalación específicas de instalación de tooa etiqueta en los centros de notificaciones:

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

Hola back-end omite las etiquetas proporcionadas por el cliente de Hola durante el registro de notificaciones de inserción cuando se crea la instalación de Hola. tooenable un tooadd cliente etiquetas toohello instalación, debe crear una API personalizada que agrega etiquetas mediante Hola anterior patrón.

Vea [etiquetas de notificación de inserción de cliente agregado] [ 5] en el ejemplo de tutorial rápido completada de aplicación del servicio de aplicaciones móviles de Hola para obtener un ejemplo.

## <a name="push-user"></a>Cómo: tooan de notificaciones de inserción de envío autentica el usuario
Cuando un usuario autenticado se registra para las notificaciones de inserción, una etiqueta de Id. de usuario se agrega automáticamente el registro de toohello. Mediante el uso de esta etiqueta, puede enviar inserción dispositivos de tooall notificaciones registrados por esa persona. Hello código siguiente obtiene Hola SID del usuario que realiza la solicitud y envía un registro de dispositivos plantilla tooevery de notificación de inserción para esa persona:

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

Cuando se registre para notificaciones push desde un cliente autenticado, asegúrese de que la autenticación se ha completado antes de intentar el registro. Para obtener más información, consulte [Push toousers] [ 6] de ejemplo de tutorial rápido completada de aplicación del servicio de aplicaciones móviles de Hola de back-end. NET.

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>Cómo: depurar y solucionar problemas de hello .NET SDK de servidor
El Servicio de aplicaciones de Azure proporciona varias técnicas de depuración y solución de problemas para las aplicaciones ASP.NET.

* [Supervisión de Aplicaciones web en el Servicio de aplicaciones de Azure](../app-service-web/web-sites-monitor.md)
* [Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure](../app-service-web/web-sites-enable-diagnostic-log.md)
* [Solución de problemas del Servicio de aplicaciones de Azure en Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>Registro
Puede escribir tooApp registros de diagnóstico de servicio mediante el uso de escritura de seguimiento ASP.NET estándar Hola. Antes de poder escribir toohello registros, debe habilitar los diagnósticos en su aplicación móvil de back-end.

registros de toohello de escritura y diagnóstico tooenable:

1. Siga los pasos de hello en [cómo diagnósticos tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).
2. Agregue los siguiente hello mediante declaración en el archivo de código:

        using System.Web.Http.Tracing;
3. Crear un toowrite de escritor de seguimiento de hello .NET back-end toohello registros de diagnóstico, como se indica a continuación:

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. Volver a publicar el proyecto de servidor y ruta de código de hello tooexecute back-end de aplicación móvil Hola con el registro de hello de acceso.
5. Descargue y evalúe los registros de hello, como se describe en [Cómo: descargar registros](../app-service-web/web-sites-enable-diagnostic-log.md#download).

### <a name="local-debug"></a>Depuración local con autenticación
Puede ejecutar la aplicación localmente tootest cambia antes de publicarlos en la nube toohello. Para la mayoría de los servidores back-end de Azure Mobile Apps, presione *F5* mientras está en Visual Studio. Sin embargo, hay algunas consideraciones adicionales cuando se usa la autenticación.

Debe tener una aplicación móvil en la nube con aplicación de servicio de autenticación/autorización configurado, y el cliente debe tener el extremo de nube Hola especificado como host de inicio de sesión alternativo de Hola. Consulte la documentación de hello para la plataforma de cliente para obtener pasos específicos Hola necesarios.

Asegúrese de que el back-end tenga instalado [Microsoft.Azure.Mobile.Server.Authentication] . A continuación, en la clase de inicio de la aplicación OWIN, agregue siguiente hello, después de `MobileAppConfiguration` se ha aplicado tooyour `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

En el anterior ejemplo de Hola, debe configurar hello *authAudience* y *authIssuer* aplicación en el archivo Web.config del archivo de configuración tooeach sea la dirección URL de la raíz de la aplicación, con hello HTTPS esquema. Del mismo modo debe establecer *authSigningKey* toobe valor de saludo de la aplicación de la clave de firma.
clave de firma de Hola tooobtain:

1. Navegar por la aplicación tooyour en hello [portal de Azure]
2. Haga clic en **Herramientas**, **Kudu**, **Ir**.
3. En el sitio de administración de Kudu hello, haga clic en **entorno**.
4. Buscar valor Hola para *sitio Web\_AUTH\_firma\_clave*.

Hola de uso clave para hello firma *authSigningKey* parámetro en la configuración de la aplicación local.  El back-end móvil ya está equipado toovalidate tokens cuando se ejecuta localmente, qué cliente hello Obtiene el token de Hola desde el punto de conexión de hello en la nube.

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portal de Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
