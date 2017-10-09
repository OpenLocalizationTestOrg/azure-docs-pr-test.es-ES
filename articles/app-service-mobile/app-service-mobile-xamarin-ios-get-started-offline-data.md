---
title: "aaaEnable la sincronización sin conexión de la aplicación móvil de Azure (iOS de Xamarin)"
description: "Obtenga información acerca de cómo toouse la toocache y sincronización de datos sin conexión de aplicación del servicio de aplicaciones móviles en la aplicación de iOS de Xamarin"
documentationcenter: xamarin
author: ggailey777
manager: cfowler
editor: 
services: app-service\mobile
ms.assetid: 828a287c-5d58-4540-9527-1309ebb0f32b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5243f2d292377d8de103a40f45d649394f11b97c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinios-mobile-app"></a>Activación de la sincronización sin conexión para la aplicación móvil Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Información general
Este tutorial presenta la característica de sincronización sin conexión de Hola de aplicaciones móviles de Azure para Xamarin.iOS. Sincronización sin conexión permite toointeract de los usuarios finales con una aplicación móvil: ver, agregar o modificar los datos, incluso cuando no hay ninguna conexión de red. Los cambios se almacenan en una base de datos local. Una vez que el dispositivo de hello vuelve a estar conectado, estos cambios se sincronizan con el servicio remoto hello.

En este tutorial, actualizar el proyecto de aplicación de hello Xamarin.iOS desde [crear una aplicación de iOS de Xamarin] toosupport Hola características sin conexión de las aplicaciones móviles de Azure. Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar Hola paquetes de la extensión de acceso de datos a su proyecto. Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn más información acerca de la característica de sincronización sin conexión de hello, vea el tema de hello [sincronización de datos sin conexión en aplicaciones móviles de Azure].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Actualizar características sin conexión de toosupport la aplicación cliente hello
Características sin conexión de aplicación móvil Azure le permiten toointeract con una base de datos local, cuando se encuentre en un escenario sin conexión. toouse estas características en la aplicación, inicializar un [SyncContext] tooa de almacén local. Hacer referencia a la tabla a través de la interfaz de hello [IMobileServiceSyncTable]. SQLite se utiliza como almacén local de hello en dispositivo Hola.

1. Administrador de paquetes de NuGet Hola Abrir proyecto de Hola que completó en hello [crear una aplicación de iOS de Xamarin] tutorial, a continuación, busque e instalación hello **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet paquete.
2. Abrir archivo de QSTodoService.cs hello y quitar el comentario hello `#define OFFLINE_SYNC_ENABLED` definición.
3. Volver a generar y ejecutar la aplicación de cliente de hello. aplicación Hello funciona Hola igual que antes de habilitar la sincronización sin conexión. Sin embargo, la base de datos local de hello ahora se rellena con datos que pueden usarse en un escenario sin conexión.

## <a name="update-sync"></a>Actualizar toodisconnect de aplicación Hola de hello back-end
En esta sección, se interrumpe Hola conexión tooyour aplicación móvil back-end toosimulate una situación sin conexión. Cuando se agregan elementos de datos, el controlador de excepciones indica que la aplicación hello está en modo sin conexión. En este estado, elementos nuevos agregados en hello local almacenan y se sincronizarán para Hola back-end de aplicación móvil cuando la inserción se vuelva a ejecutar en un estado conectado.

1. Editar QSToDoService.cs en el proyecto compartido Hola. Hola de cambio **ApplicationUrl del** toopoint dirección URL no válida de tooan:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    También puede mostrar el comportamiento sin conexión deshabilitando Wi-Fi y redes de telefonía móviles en dispositivo de Hola o utilizando el modo de avión.
2. Compile y ejecute la aplicación hello. Tenga en cuenta la sincronización no se pudo al actualizar Hola cuando la aplicación inicia.
3. Escriba nuevos elementos y observe que la operación de inserción produce un error con un estado de [CancelledByNetworkError] cada vez que hace clic en **Guardar**. Sin embargo, nuevos elementos de lista de tareas Hola existen en el almacén local de hello hasta que estos se pueden insertar back-end de toohello aplicación móvil.  En uno de producción aplicación, si se suprimen las siguientes excepciones de aplicación de cliente de hello se comporta como si aún está conectado back-end de toohello aplicación móvil.
4. Cierre la aplicación hello y reiníciela tooverify que elementos nuevos de Hola que creó están almacén local toohello persistente.
5. (Opcional) Si Visual Studio está instalado en un equipo, abra **Explorador de servidores**. Navegar por la base de datos de tooyour en **Azure**-> **bases de datos SQL**. Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**. Ahora puede examinar la tabla de base de datos SQL tooyour y su contenido. Compruebe que los datos de hello en la base de datos de back-end de hello no han cambiado.
6. (Opcional) Usar una herramienta REST como Fiddler o Postman tooquery su backend móvil, utilizando una consulta GET con el formato `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Actualizar tooreconnect de aplicación Hola su aplicación móvil de back-end
En esta sección, vuelva a conectar Hola aplicación toohello aplicación móvil back-end. Esto simula la aplicación hello mover desde un estado en línea de estado sin conexión tooan con back-end de aplicación móvil de Hola.   Si simula la ruptura de red de hello mediante la desactivación de conectividad de red, se necesita ningún cambio de código.
Red de hello volver a activar.  Cuando ejecuta por primera vez aplicación hello, Hola `RefreshDataAsync` se llama al método. Esto llama a su vez `SyncAsync` toosync local almacenar con la base de datos de back-end de Hola.

1. Abra QSToDoService.cs en el proyecto compartido hello y revertir el cambio de hello **ApplicationUrl del** propiedad.
2. Volver a generar y ejecutar la aplicación hello. Hello aplicación sincroniza los cambios locales con back-end de aplicación móvil de Azure de hello mediante las operaciones de inserción y extracción cuando hello `OnRefreshItemsSelected` el método se ejecuta.
3. (Opcional) Hola de vista actualiza datos mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler. Se ha sincronizado aviso Hola datos entre la base de datos de back-end de aplicación móvil de Azure de Hola y el almacén local de Hola.
4. En la aplicación hello, haga clic en comprobar de hello cuadro junto a algunos de los elementos de toocomplete ellos en el almacén local de Hola.

   `CompleteItemAsync`llamadas `SyncAsync` elemento toosync cada completado con back-end de hello aplicación móvil. `SyncAsync` llama a las operaciones de inserción y extracción.
   **Cada vez que se ejecuta una extracción en una tabla que el cliente hello ha realizado cambios a, una inserción en el contexto de sincronización de cliente hello siempre se ejecuta en primer lugar automáticamente**. inserción implícita Hola garantiza que todas las tablas de almacén local de hello junto con las relaciones siguen siendo coherentes. Para obtener más información sobre este comportamiento, consulte [sincronización de datos sin conexión en aplicaciones móviles de Azure].

## <a name="review-hello-client-sync-code"></a>Revise el código de sincronización de cliente hello
proyecto de cliente de Xamarin Hola que ha descargado al completar el tutorial de hello [crear una aplicación de iOS de Xamarin] ya contiene código que respalda la sincronización sin conexión con una base de datos local de SQLite. Esta es una breve descripción de lo que ya está incluido en el código del tutorial Hola. Para obtener información conceptual de característica de hello, consulte [sincronización de datos sin conexión en aplicaciones móviles de Azure].

* Para poder realizar cualquier operación de tabla, se debe inicializar el almacén local de Hola. Hello base de datos del almacén local se inicializa cuando `QSTodoListViewController.ViewDidLoad()` ejecuta `QSTodoService.InitializeStoreAsync()`. Este método crea una nueva base de SQLite local mediante hello `MobileServiceSQLiteStore` clase proporcionada por el SDK del cliente de aplicación móvil de Azure Hola.

    Hola `DefineTable` método crea una tabla de almacén local de Hola que coincida con los campos de hello en el tipo de hello proporcionado, `ToDoItem` en este caso. tipo de Hello no tiene tooinclude todas las columnas de Hola que se encuentran en la base de datos remota Hola. Es posible toostore solo un subconjunto de columnas.

        // QSTodoService.cs

        public async Task InitializeStoreAsync()
        {
            var store = new MobileServiceSQLiteStore(localDbPath);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            await client.SyncContext.InitializeAsync(store);
        }
* Hola `todoTable` miembro de `QSTodoService` es de hello `IMobileServiceSyncTable` escriba en lugar de `IMobileServiceTable`. Hola IMobileServiceSyncTable dirige todo crear, leer, actualizar y eliminar (CRUD) base de datos de tabla operaciones toohello almacén local.

    Decidir si esos cambios se insertan back-end de toohello aplicación móvil de Azure mediante una llamada a `IMobileServiceSyncContext.PushAsync()`. Hello contexto de sincronización le ayuda a mantener las relaciones entre tablas de seguimiento e insertar los cambios en todas las tablas de una aplicación cliente modifica cuando `PushAsync` se llama.

    llamadas de código de Hello proporciona `QSTodoService.SyncAsync()` toosync cada vez que se actualiza la lista de todoitem de Hola o un todoitem se agrega o se ha completado. La aplicación se sincroniza inmediatamente después de cada cambio local. Si una extracción se ejecuta en una tabla que contiene las actualizaciones locales pendientes marcas según el contexto de hello, esa operación de extracción desencadenará automáticamente una inserción de contexto en primer lugar.

    En el código de hello proporcionado, todos los registros en hello remoto `TodoItem` se consultan la tabla, pero también es posible toofilter registros pasando un identificador de la consulta y una consulta demasiado`PushAsync`. Para obtener más información, vea la sección de hello *sincronización Incremental* en [sincronización de datos sin conexión en aplicaciones móviles de Azure].

        // QSTodoService.cs
        public async Task SyncAsync()
        {
            try
            {
                await client.SyncContext.PushAsync();
                await todoTable.PullAsync("allTodoItems", todoTable.CreateQuery()); // query ID is used for incremental sync
            }

            catch (MobileServiceInvalidOperationException e)
            {
                Console.Error.WriteLine(@"Sync Failed: {0}", e.Message);
            }
        }

## <a name="additional-resources"></a>Recursos adicionales
* [sincronización de datos sin conexión en aplicaciones móviles de Azure]
* [Procedimiento del SDK de .NET de Azure Mobile Apps][8]

<!-- Images -->

<!-- URLs. -->
[crear una aplicación de iOS de Xamarin]: app-service-mobile-xamarin-ios-get-started.md
[sincronización de datos sin conexión en aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
