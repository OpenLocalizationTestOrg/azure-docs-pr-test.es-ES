---
title: "aaaEnable la sincronización sin conexión de la aplicación móvil de Azure (Xamarin Android)"
description: "Obtenga información acerca de cómo toouse la toocache y sincronización de datos sin conexión de aplicación del servicio de aplicaciones móviles en la aplicación de Xamarin para Android"
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 91d59e4b-abaa-41f4-80cf-ee7933b32568
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 216ba76ae49f583273cc61b63114a415eca2477b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a>Activación de la sincronización sin conexión para la aplicación móvil Xamarin.Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Información general
Este tutorial presenta la característica de sincronización sin conexión de Hola de aplicaciones móviles de Azure para Xamarin.Android. Sincronización sin conexión permite toointeract de los usuarios finales con una aplicación móvil: ver, agregar o modificar los datos, incluso cuando no hay ninguna conexión de red. Los cambios se almacenan en una base de datos local.
Una vez que el dispositivo de hello vuelve a estar conectado, estos cambios se sincronizan con el servicio remoto hello.

En este tutorial, Actualizar proyecto de cliente de hello del tutorial de Hola de [crear una aplicación de Xamarin para Android] toosupport Hola características sin conexión de las aplicaciones móviles de Azure. Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto tooyour de paquetes de extensión de acceso de hello datos. Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn más información acerca de la característica de sincronización sin conexión de hello, vea el tema de hello [sincronización de datos sin conexión en aplicaciones móviles de Azure].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Actualizar características sin conexión de toosupport la aplicación cliente hello
Características sin conexión de aplicación móvil Azure le permiten toointeract con una base de datos local, cuando se encuentre en un escenario sin conexión. toouse estas características en la aplicación, inicializar un [SyncContext] tooa de almacén local. A continuación, hacer referencia a la tabla a través de hello [IMobileServiceSyncTable] [IMobileServiceSyncTable] interfaz. SQLite se utiliza como almacén local de hello en dispositivo Hola.

1. En Visual Studio, abra el Administrador de paquetes de NuGet hello en proyecto de Hola que completó en hello [crear una aplicación de Xamarin para Android] tutorial.  Buscar e instalar hello **Microsoft.Azure.Mobile.Client.SQLiteStore** paquete NuGet.
2. Abrir archivo de ToDoActivity.cs hello y quitar el comentario hello `#define OFFLINE_SYNC_ENABLED` definición.
3. En Visual Studio, presione hello **F5** clave toorebuild y aplicación de cliente de hello de ejecución. aplicación Hello funciona Hola igual que antes de habilitar la sincronización sin conexión. Sin embargo, la base de datos local de hello ahora se rellena con datos que pueden usarse en un escenario sin conexión.

## <a name="update-sync"></a>Actualizar toodisconnect de aplicación Hola de hello back-end
En esta sección, se interrumpe Hola conexión tooyour aplicación móvil back-end toosimulate una situación sin conexión. Cuando se agregan elementos de datos, el controlador de excepciones indica que la aplicación hello está en modo sin conexión. En este estado, elementos nuevos agregados en hello local almacenan y se sincronizan con back-end de aplicación móvil de hello cuando se ejecuta una inserción en un estado conectado.

1. Editar ToDoActivity.cs en el proyecto compartido Hola. Hola de cambio **ApplicationUrl del** toopoint dirección URL no válida de tooan:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    También puede mostrar el comportamiento sin conexión deshabilitando Wi-Fi y redes de telefonía móviles en dispositivo de Hola o utilizando el modo de avión.
2. Presione **F5** aplicación hello toobuild y ejecución. Tenga en cuenta la sincronización no se pudo al actualizar Hola cuando la aplicación inicia.
3. Escriba nuevos elementos y observe que la operación de inserción produce un error con un estado de [CancelledByNetworkError] cada vez que hace clic en **Guardar**. Sin embargo, nuevos elementos de lista de tareas Hola existen en el almacén local de hello hasta que estos se pueden insertar back-end de toohello aplicación móvil.  En uno de producción aplicación, si se suprimen las siguientes excepciones de aplicación de cliente de hello se comporta como si aún está conectado back-end de toohello aplicación móvil.
4. Cierre la aplicación hello y reiníciela tooverify que elementos nuevos de Hola que creó están almacén local toohello persistente.
5. (Opcional) En Visual Studio, abra el **Explorador de servidores**. Navegar por la base de datos de tooyour en **Azure**->**bases de datos SQL**. Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**. Ahora puede examinar la tabla de base de datos SQL tooyour y su contenido. Compruebe que los datos de hello en la base de datos de back-end de hello no han cambiado.
6. (Opcional) Usar una herramienta REST como Fiddler o Postman tooquery su backend móvil, utilizando una consulta GET con el formato `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Actualizar tooreconnect de aplicación Hola su aplicación móvil de back-end
En esta sección, vuelva a conectar Hola aplicación toohello aplicación móvil back-end. Cuando ejecuta por primera vez aplicación hello, Hola `OnCreate` llamadas del controlador de eventos `OnRefreshItemsSelected`. Este método llama `SyncAsync` toosync local almacenar con la base de datos de back-end de Hola.

1. Abra ToDoActivity.cs en el proyecto compartido hello y revertir el cambio de hello **ApplicationUrl del** propiedad.
2. Hola presione **F5** clave toorebuild y aplicación hello de ejecución. Hello aplicación sincroniza los cambios locales con back-end de aplicación móvil de Azure de hello mediante las operaciones de inserción y extracción cuando hello `OnRefreshItemsSelected` el método se ejecuta.
3. (Opcional) Hola de vista actualiza datos mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler. Se ha sincronizado aviso Hola datos entre la base de datos de back-end de aplicación móvil de Azure de Hola y el almacén local de Hola.
4. En la aplicación hello, haga clic en comprobar de hello cuadro junto a algunos de los elementos de toocomplete ellos en el almacén local de Hola.

   `CheckItem`llamadas `SyncAsync` elemento toosync cada completado con back-end de hello aplicación móvil. `SyncAsync` llama a las operaciones de inserción y extracción. **Cada vez que se ejecuta una extracción en una tabla que el cliente hello ha realizado cambios a, siempre se ejecuta automáticamente una inserción**. De este modo se garantiza la coherencia de todas las tablas del almacén local, junto con sus relaciones. Este comportamiento puede provocar una inserción inesperada. Para obtener más información sobre este comportamiento, consulte [sincronización de datos sin conexión en aplicaciones móviles de Azure].

## <a name="review-hello-client-sync-code"></a>Revise el código de sincronización de cliente hello
proyecto de cliente de Xamarin Hola que ha descargado al completar el tutorial de hello [crear una aplicación de Xamarin para Android] ya contiene código que respalda la sincronización sin conexión con una base de datos local de SQLite. Esta es una breve descripción de lo que ya está incluido en el código del tutorial Hola. Para obtener información conceptual de característica de hello, consulte [sincronización de datos sin conexión en aplicaciones móviles de Azure].

* Para poder realizar cualquier operación de tabla, se debe inicializar el almacén local de Hola. Hello base de datos del almacén local se inicializa cuando `ToDoActivity.OnCreate()` ejecuta `ToDoActivity.InitLocalStoreAsync()`. Este método crea una base de datos local de SQLite con hello `MobileServiceSQLiteStore` clase proporcionada por el SDK del cliente de aplicaciones móviles de Azure Hola.

    Hola `DefineTable` método crea una tabla de almacén local de Hola que coincida con los campos de hello en el tipo de hello proporcionado, `ToDoItem` en este caso. tipo de Hello no tiene tooinclude todas las columnas de Hola que se encuentran en la base de datos remota Hola. Es posible toostore solo un subconjunto de columnas.

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code tooinitialize hello SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            // toouse a different conflict handler, pass a parameter tooInitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* Hola `toDoTable` miembro de `ToDoActivity` es de hello `IMobileServiceSyncTable` escriba en lugar de `IMobileServiceTable`. Hola IMobileServiceSyncTable dirige todo crear, leer, actualizar y eliminar (CRUD) base de datos de tabla operaciones toohello almacén local.

    Decidir cuándo cambios se insertan back-end de toohello aplicación móvil de Azure mediante una llamada a `IMobileServiceSyncContext.PushAsync()`. Hello contexto de sincronización le ayuda a mantener las relaciones entre tablas de seguimiento e insertar los cambios en todas las tablas de una aplicación cliente modifica cuando `PushAsync` se llama.

    llamadas de código de Hello proporciona `ToDoActivity.SyncAsync()` toosync cada vez que se actualiza la lista de todoitem de Hola o un todoitem se agrega o se ha completado. sincronizaciones de código de Hello después de cada cambio local.

    En el código de hello proporcionado, todos los registros en hello remoto `TodoItem` se consultan la tabla, pero también es posible toofilter registros pasando un identificador de la consulta y una consulta demasiado`PushAsync`. Para obtener más información, vea la sección de hello *sincronización Incremental* en [sincronización de datos sin conexión en aplicaciones móviles de Azure].

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating hello Mobile Service. Verify hello URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a>Recursos adicionales
* [sincronización de datos sin conexión en aplicaciones móviles de Azure]
* [Procedimiento del SDK de .NET de Azure Mobile Apps][8]

<!-- URLs. -->
[crear una aplicación de Xamarin para Android]: ../app-service-mobile-xamarin-android-get-started.md
[sincronización de datos sin conexión en aplicaciones móviles de Azure]: ../app-service-mobile-offline-data-sync.md

<!-- Images -->

<!-- URLs. -->
[Creación de una aplicación Xamarin Android]: app-service-mobile-xamarin-android-get-started.md
[Sincronización de datos sin conexión en Aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
