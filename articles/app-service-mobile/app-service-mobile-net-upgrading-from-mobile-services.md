---
title: "aaaUpgrade de tooAzure servicio de aplicaciones de servicios móviles"
description: "Obtenga información acerca de cómo tooeasily actualizar su tooan de aplicación de servicios móviles aplicación móvil de servicio de aplicación"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>Actualizar su tooApp de servicios móviles de Azure .NET servicio existente
Servicio de aplicaciones móviles son una nueva manera toobuild móviles las aplicaciones con Microsoft Azure. más información, consulte toolearn [¿qué aplicaciones móviles?].

Este tema se describe cómo una aplicación existente de back-end de .NET de servicios móviles de Azure tooa tooupgrade aplicaciones móviles de nueva aplicación de servicio. Cuando realiza esta actualización, la aplicación de servicios móviles existente puede seguir realizando toooperate.   Si necesita una aplicación de back-end de Node.js tooupgrade, consulte demasiado[actualizar los servicios móviles de Node.js](app-service-mobile-node-backend-upgrading-from-mobile-services.md).

Una vez un back-end móvil actualizado tooAzure servicio de aplicaciones, tiene tooall de acceso a características del servicio de aplicación y facturan según demasiado[servicio de aplicaciones precios], no los servicios móviles de precios.

## <a name="migrate-vs-upgrade"></a>Migración frente a actualización
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Se recomienda [realizar una migración](app-service-mobile-migrating-from-mobile-services.md) antes de pasar por una actualización. De esta manera, puede colocar las dos versiones de la aplicación Hola mismo Plan de servicio de aplicación y no acumulando costo adicional alguno.
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>Mejoras en el SDK de servidor .NET de Aplicaciones móviles
Actualizar toohello nueva [SDK de aplicaciones móviles](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) proporciona Hola siguientes ventajas:

* Más flexibilidad en las dependencias de NuGet. Hola entorno de hospedaje ya no proporciona sus propias versiones de paquetes de NuGet, por lo que puede usar versiones compatibles alternativas. Sin embargo, si hay nuevas bugfixes crítico o toohello de las actualizaciones de seguridad móvil Server SDK o dependencias, debe actualizar manualmente el servicio.
* Más flexibilidad en Hola SDK móvil. Puede controlar explícitamente qué características y las rutas se establecen, como la autenticación, tabla API y Hola extremo de registro de inserción. más información, consulte toolearn [cómo toouse Hola servidor .NET SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).
* Compatibilidad con otras rutas y tipos de proyecto ASP.NET. Ahora puede hospedar los controladores MVC y API Web en hello mismo proyecto como el proyecto móvil de back-end.
* Compatibilidad con nuevas características de autenticación de servicio de aplicaciones, que le permiten toouse una configuración de autenticación común a través de la web y aplicaciones móviles.

## <a name="overview"></a>Información general básica de actualización
En muchos casos, la actualización será tan sencilla como cambiar toohello nuevo servidor de aplicaciones móviles SDK y volver a publicar el código en una nueva instancia de la aplicación móvil. Sin embargo, hay algunos escenarios que requieren una configuración adicional, como los escenarios de autenticación avanzada y el trabajo con trabajos programados. Cada una de ellas se trata en hello secciones más adelante.

> [!TIP]
> Se recomienda que leer y comprender el resto de Hola de este tema completamente antes de iniciar una actualización. Tome nota de cualquier característica usada que se mencione a continuación.
>
>

SDK de cliente de servicios móviles de Hello es **no** compatibles con el servidor de aplicaciones móviles nueva Hola SDK. En orden tooprovide la continuidad del servicio para la aplicación, no debería publicar sitio tooa de cambios actualmente actúa a clientes publicados. En su lugar, debe crear una aplicación móvil que actúe como duplicado. Puede colocar esta aplicación Hola mismo servicio de aplicaciones previsto tooavoid incurrir en costes financieros adicionales.

A continuación, tendrá dos versiones de la aplicación hello: uno que permanece Hola igual y sirve de las aplicaciones publicadas en hello y Hola comodín sí que, a continuación, puede actualizar y destino con una nueva versión de cliente. Puede mover y probar el código a su ritmo, pero debe asegurarse de que las correcciones de errores de que asegúrese obtener tooboth aplicada. Cuando se sienta que un número deseado de las aplicaciones de cliente en hello comodín actualizaron versión más reciente de toohello, puede eliminar la aplicación migrada de hello original si así lo desea.

descripción completa del Hola de proceso de actualización de hello es como sigue:

1. Creación de una aplicación móvil
2. Actualización Hola proyecto toouse Hola nuevos SDK de servidor
3. Publique una versión nueva de la aplicación cliente
4. (Opcional) Eliminación de la instancia original migrada

## <a name="mobile-app-version"></a>Creación de una segunda instancia de aplicación
Hola primer paso en la actualización es recursos de aplicación móvil de hello toocreate que hospedarán la nueva versión de hello de la aplicación. Si ya se ha migrado un servicio móvil existente, deberá toocreate esta versión en hello mismo plan de hospedaje. Abra hello [portal de Azure] y navegue tooyour migrar la aplicación. Tome nota de hello Plan del servicio de aplicación que se ejecuta.

A continuación, crear la segunda instancia de la aplicación de Hola Hola siguiente [instrucciones de creación de back-end de .NET](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app). Cuando tooselect solicitada, Plan de servicio de aplicación o "plan de hospedaje" Elija Hola plan de la aplicación migrada.

Probablemente deseará toouse Hola la misma base de datos y el centro de notificaciones como se hacía en servicios móviles. Puede copiar estos valores abriendo [portal de Azure] y, a continuación, navegar por los toohello de aplicación original, haga clic en **configuración** > **configuración de la aplicación**. En **Cadenas de conexión**, copie `MS_NotificationHubConnectionString` y `MS_TableConnectionString`. Navegar por el nuevo sitio de actualización tooyour y péguelos en, sobrescribiendo los valores existentes. Repita este proceso para cualquier otra opción de configuración de la aplicación que la aplicación requiera. Si no utiliza un servicio migrado, puede leer las cadenas de conexión y configuración de la aplicación de hello **configurar** ficha de la sección de servicios móviles de Hola Hola [portal de Azure clásico].

Realizar una copia del proyecto ASP.NET de hello de la aplicación y publicarla tooyour nuevo sitio. Con una copia de la aplicación de cliente actualizada con la nueva dirección URL de hello, validar que todo funciona según lo previsto.

## <a name="updating-hello-server-project"></a>Actualizando el proyecto de servidor hello
Aplicaciones móviles proporciona un nuevo [Mobile SDK para aplicaciones de servidor] que proporciona gran parte de hello misma funcionalidad que en tiempo de ejecución de servicios móviles de Hola. En primer lugar, debe quitar todos los paquetes de servicios móviles de toohello de referencias. En el Administrador de paquetes de NuGet hello, buscar `WindowsAzure.MobileServices.Backend`. En la mayoría de aplicaciones se verán varios paquetes aquí, incluidos `WindowsAzure.MobileServices.Backend.Tables` y `WindowsAzure.MobileServices.Backend.Entity`. En tal caso, comience con paquete más bajo de hello en el árbol de dependencias de hello, como `Entity`y lo quitará. Cuando se le pregunte, no quite todos los paquetes dependientes. Repita este proceso hasta que haya quitado el propio `WindowsAzure.MobileServices.Backend` .

En este punto, tendrá un proyecto que ya no hace referencia a los SDK de Servicios móviles.

A continuación agregará referencias Hola SDK de aplicaciones móviles. Para esta actualización, la mayoría de los desarrolladores se desea toodownload e instalar hello `Microsoft.Azure.Mobile.Server.Quickstart` del paquete, tal y como se extraerá set requeridas de hello todo.

Habrá errores del compilador bastantes resultante de las diferencias entre el SDK de hello, pero estos son tooaddress fácil y en el resto de Hola de esta sección se tratan.

### <a name="base-configuration"></a>Configuración base
Luego, en WebApiConfig.cs, puede reemplazar.

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

por

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> Si desea más información acerca de hello nuevo .NET server SDK y cómo tooadd o quitar características de la aplicación toolearn, vea hello [cómo toouse Hola servidor .NET SDK] tema.
>
>

Si la aplicación realiza el uso de características de autenticación de hello, también necesitará tooregister un middleware OWIN. En este caso, debe mover Hola por encima del código de configuración en una nueva clase de inicio de OWIN.

1. Agregar paquete de NuGet hello `Microsoft.Owin.Host.SystemWeb` si ya no está incluido en el proyecto.
2. En Visual Studio, haga clic con el botón derecho en el proyecto y seleccione **Agregar** -> **Nuevo elemento**. Seleccione **Web** -> **General** -> **Clase de inicio OWIN**.
3. Mover Hola por encima del código de MobileAppConfiguration de `WebApiConfig.Register()` toohello `Configuration()` método de la nueva clase de inicio.

Asegúrese de hello seguro `Configuration()` método termina con:

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

No hay cambios adicionales tooauthentication relacionados que se tratan en la siguiente sección de autenticación completa de Hola.

### <a name="working-with-data"></a>Trabajo con datos
En servicios móviles, nombre de la aplicación móvil de hello sirve como nombre de esquema predeterminado de hello en el programa de instalación de hello Entity Framework.

tooensure que tienes Hola mismo esquema que se hace referencia como antes, Hola de uso después de esquema de hello tooset Hola DbContext para la aplicación:

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

Asegúrese de que tiene MS_MobileServiceName establecer si Hola anteriormente. También puede especificar otro nombre de esquema si la aplicación lo personalizó anteriormente.

### <a name="system-properties"></a>Propiedades del sistema
#### <a name="naming"></a>Nomenclatura
En el servidor de servicios móviles de Azure de hello SDK, propiedades del sistema siempre contienen un carácter de subrayado doble (`__`) prefijo para las propiedades de hello:

* __createdAt
* __updatedAt
* __deleted
* __version

SDK de cliente de servicios móviles de Hello tiene una lógica especial para el análisis de propiedades del sistema en este formato.

En aplicaciones móviles de Azure, propiedades del sistema ya no tienen una clase especial de formato y tienen Hola después de nombres:

* createdAt
* updatedAt
* deleted
* versión

Hello aplicaciones móviles SDK uso Hola nuevo sistema propiedades nombres de cliente, por lo que ningún cambio necesario tooclient código. Sin embargo, si está directamente realizar REST llamadas tooyour servicio, a continuación, debe cambiar las consultas como corresponda.

#### <a name="local-store"></a>Almacén local.
Hola cambios toohello nombres de propiedades del sistema significan que una base de datos local de sincronización sin conexión para servicios móviles no es compatible con aplicaciones móviles. Si es posible, debe evitar la actualización de las aplicaciones cliente de tooMobile de servicios móviles que aplicaciones hasta después de los cambios pendientes se han enviado toohello server. A continuación, Hola actualizado aplicación debe utilizar un nombre de archivo de base de datos nueva.

Si una aplicación cliente se actualiza desde servicios móviles tooMobile aplicaciones mientras hay cambios sin conexión pendientes en cola de la operación de hello, base de datos de sistema de hello debe ser actualizada toouse Hola nuevos nombres de columna. En iOS, esto puede lograrse mediante nombres de columna de migraciones ligera toochange Hola. En el cliente administrado .NET hello y Android, debe escribir columnas Hola de toorename personalizado de SQL para las tablas de objeto de datos.

En iOS, debe cambiar el esquema de datos principal para su siguiente de Hola de toomatch de entidades de datos. Tenga en cuenta que Hola propiedades `createdAt`, `updatedAt` y `version` ya no tiene un `ms_` prefijo:

| Atributo | Escriba | Nota: |
| --- | --- | --- |
| id |Cadena, marcado obligatorio |primary key in remote store |
| createdAt |Date |propiedad del sistema toocreatedAt mapas (opcional) |
| updatedAt |Date |propiedad del sistema tooupdatedAt mapas (opcional) |
| versión |String |(opcional) toodetect utilizados entra en conflicto, tooversion de mapas |

#### <a name="querying-system-properties"></a>Consulta de propiedades del sistema
En servicios móviles de Azure, propiedades del sistema no se envían de forma predeterminada, pero solo cuando se solicitan mediante la cadena de consulta de hello `__systemProperties`. En cambio, en el sistema de aplicaciones móviles de Azure son propiedades **siempre activada** ya que forman parte del modelo de objetos de hello server SDK.

Este cambio afecta principalmente a las implementaciones personalizadas de los administradores de dominio, como las extensiones de `MappedEntityDomainManager`. En servicios móviles, si un cliente no solicita nunca las propiedades del sistema, es posible toouse un `MappedEntityDomainManager` que realmente no asignar todas las propiedades. Pero, en Aplicaciones móviles de Azure, estas propiedades sin asignar producirán un error en las consultas GET.

Hola problema de Hola de tooresolve de manera más sencilla es toomodify su dto para que se heredan de `ITableData` en lugar de `EntityData`. A continuación, agregue hello `[NotMapped]` atributo toohello campos que se deben omitir.

Por ejemplo, define la siguiente hello `TodoItem` sin propiedades de sistema:

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

Nota: si se producen errores en `NotMapped`, agregar un ensamblado de referencia toohello `System.ComponentModel.DataAnnotations`.

### <a name="cors"></a>CORS
Servicios móviles incluye cierta compatibilidad para CORS ajustando Hola solución ASP.NET CORS. Esta capa de ajuste ha sido eliminado toogive para desarrolladores de hello más control, lo que permite aprovechar directamente [compatibilidad de ASP.NET CORS](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

Hello principales áreas problemáticas si mediante CORS son ese hello `eTag` y `Location` encabezados deben estar habilitados en orden para hello cliente SDK toowork correctamente.

### <a name="push-notifications"></a>Notificaciones de inserción
Para que la inserción, elemento principal de Hola que es posible que falten en hello SDK de servidor es la clase de PushRegistrationHandler de Hola. Los registros se controlan de forma ligeramente diferente en las aplicaciones móviles y los registros sin etiqueta están habilitados de forma predeterminada. Se puede lograr la administración de etiquetas mediante API personalizadas. Vea hello [registrar para etiquetas](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) instrucciones para obtener más información.

### <a name="scheduled-jobs"></a>Trabajos programados
Los trabajos programados no se compilan en aplicaciones móviles, por lo que los trabajos existentes que tienen en el back-end de .NET deberá toobe actualizar de manera individual. Una opción es un programada toocreate [trabajo Web] en el sitio de código de aplicación móvil de Hola. También puede configurar un controlador que contiene el código de trabajo y configurar hello [Azure Scheduler] toohit ese punto de conexión en programación de hello esperado.

### <a name="miscellaneous-changes"></a>Cambios varios
Todos los ApiControllers que va a ser utilizados por un cliente móvil debe tener ahora hello `[MobileAppController]` atributo. Ya no se incluye de forma predeterminada para que otros toogo ApiControllers no afecta Hola a formateadores móviles.

Hola `ApiServices` objeto ya no forma parte de hello SDK. tooaccess configuración de aplicación móvil, puede utilizar Hola siguiente:

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

De forma similar, el registro ahora se realiza mediante la escritura de seguimiento ASP.NET estándar hello:

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>Consideraciones de autenticación
Ahora que se han movido los componentes de autenticación de Hello de servicios móviles de característica de autenticación/autorización del servicio de aplicación Hola. Puede obtener información acerca de cómo habilitar para el sitio por leer hello [aplicación móvil de agregar autenticación tooyour](app-service-mobile-ios-get-started-users.md) tema.

Para algunos proveedores, como AAD y Facebook, Google, debe ser registro existente de tooleverage capaz de Hola desde la aplicación de copia. Simplemente necesita portal del proveedor de identidades de toonavigate toohello y agregar un nuevo registro de toohello de dirección URL de redireccionamiento. A continuación, configurar autenticación/autorización del servicio de aplicación con el identificador de cliente de Hola y el secreto.

### <a name="controller-action-authorization"></a>Autorización de acción de controlador
Todas las instancias de hello `[AuthorizeLevel(AuthorizationLevel.User)]` atributo ahora debe ser modificada toouse Hola ASP.NET estándar `[Authorize]` atributo. Además, los controladores son ahora de tipo anónimo de forma predeterminada, al igual que en otras aplicaciones de ASP.NET.
Si se usa uno de hello otras opciones de AuthorizeLevel, como administrador o aplicación, tenga en cuenta que estos han desaparecido. En su lugar, puede configurar los AuthorizationFilters para secretos compartidos o configurar de forma segura un llamadas de servicio a servicio tooenable de entidad de servicio de AAD.

### <a name="getting-additional-user-information"></a>Información adicional del usuario
Para obtener información adicional del usuario, incluidos los tokens de acceso a través de hello `GetAppServiceIdentityAsync()` método:

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

Además, si la aplicación tiene dependencias en identificadores, de usuario como almacenarlas en una base de datos, es importante toonote que Hola identificadores de usuario entre servicios móviles y la aplicación del servicio de aplicaciones móviles son diferentes. Aunque todavía puede obtener Hola identificador de usuario de servicios móviles. Todas las subclases de hello ProviderCredentials tienen una propiedad de identificador de usuario. Por lo que continuar de ejemplo de Hola antes:

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

Si la aplicación realiza todas las dependencias en el Id. de usuario, es importante que aproveche Hola mismo registro con un proveedor de identidad si es posible. Id. de usuario es toohello normalmente con ámbito registro de la aplicación que se utilizó, por lo que introducir un nuevo registro podría crear problemas con los usuarios tootheir datos coincidentes.

### <a name="custom-authentication"></a>Autenticación personalizada
Si la aplicación está utilizando una solución de autenticación personalizada, le interesará toomake que ese sitio actualizado Hola tenga acceso toohello sistema. Siga las instrucciones nuevo de hello para la autenticación personalizada en hello [información general del SDK de .NET server] toointegrate la solución. Tenga en cuenta que los componentes de autenticación personalizada de Hola son todavía en la vista previa.

## <a name="updating-clients"></a>Actualización de clientes
Cuando tenga un back-end de aplicación móvil operativo, podrá trabajar en una nueva versión de la aplicación cliente que lo usa. Aplicaciones móviles también incluye una nueva versión del SDK de cliente de Hola y similar toohello actualización del servidor anterior, deberá tooremove todas las referencias de SDK de servicios móviles de toohello antes de instalar las versiones de aplicaciones móviles de Hola.

Uno de los cambios principales de hello entre las versiones de hello es que los constructores de hello ya no necesitan una clave de aplicación. Ahora basta con pasa en dirección URL de saludo de la aplicación móvil. Por ejemplo, en los clientes de .NET de hello, Hola `MobileServiceClient` constructor está ahora:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

Puede leer acerca de cómo instalar Hola nuevos SDK y el uso de la nueva estructura de Hola a través de vínculos de hello siguientes:

* [iOS versión 3.0.0 o posterior](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) versión 2.0.0 o posterior](app-service-mobile-dotnet-how-to-use-client-library.md)

Si la aplicación realiza el uso de notificaciones de inserción, tome nota de hello instrucciones de registro específico para cada plataforma, tal y como han habido algunos cambios también.

Cuando haya Hola nueva versión de cliente listo, pruébelo en su proyecto de servidor actualizado. Después de comprobar que funciona, puede liberar una nueva versión de la aplicación toocustomers. Finalmente, una vez que los clientes han tenido una oportunidad tooreceive estas actualizaciones, puede eliminar la versión de servicios móviles de saludo de la aplicación. En este punto, ha actualizado completamente tooan aplicación móvil de servicio de aplicación con el servidor de aplicaciones móviles más reciente de hello SDK.

<!-- URLs. -->

[portal de Azure]: https://portal.azure.com/
[portal de Azure clásico]: https://manage.windowsazure.com/
[¿qué aplicaciones móviles?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile SDK para aplicaciones de servidor]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[trabajo Web]: ../app-service-web/websites-webjobs-resources.md
[cómo toouse Hola servidor .NET SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[servicio de aplicaciones precios]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[información general del SDK de .NET server]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
