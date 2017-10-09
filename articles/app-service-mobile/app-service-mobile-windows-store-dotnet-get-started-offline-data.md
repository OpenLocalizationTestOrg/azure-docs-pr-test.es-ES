---
title: "aaaEnable la sincronización sin conexión de la aplicación de plataforma Universal de Windows (UWP) con aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse una aplicación móvil de Azure toocache y sincronización de datos sin conexión en la aplicación de plataforma Universal de Windows (UWP)."
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>Activación de la sincronización sin conexión para la aplicación de Windows
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Información general
Este tutorial muestra cómo tooadd sin conexión son compatibles con la aplicación de plataforma Universal de Windows (UWP) tooa usar un back-end de aplicación móvil de Azure. Sincronización sin conexión permite toointeract de los usuarios finales con una aplicación móvil: ver, agregar o modificar datos, incluso cuando no hay ninguna conexión de red. Los cambios se almacenan en una base de datos local. Una vez que el dispositivo de hello vuelve a estar conectado, estos cambios se sincronizan con back-end de hello remoto.

En este tutorial, va a actualizar proyecto de aplicación UWP Hola de tutorial de hello [crear una aplicación Windows] toosupport Hola características sin conexión de las aplicaciones móviles de Azure. Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto tooyour de paquetes de extensión de acceso de hello datos. Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn más información acerca de la característica de sincronización sin conexión de hello, vea el tema de hello [sincronización de datos sin conexión en aplicaciones móviles de Azure].

## <a name="requirements"></a>Requisitos
Este tutorial requiere Hola siguiendo los requisitos previos:

* Visual Studio 2013 funcionando en Windows 8.1 o versiones posteriores.
* Finalización del tutorial [Creación de una aplicación para Windows][Creación de una aplicación para Windows].
* [Almacén de SQLite de Azure Mobile Services][sqlite store nuget]
* [SQLite for Universal Windows Platform development](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>Actualizar características sin conexión de toosupport la aplicación cliente hello
Características sin conexión de aplicación móvil Azure le permiten toointeract con una base de datos local, cuando se encuentre en un escenario sin conexión. toouse estas características en la aplicación, inicializar un [SyncContext] [ synccontext] tooa de almacén local. A continuación, hacer referencia a la tabla a través de hello [IMobileServiceSyncTable][IMobileServiceSyncTable] interfaz. SQLite se utiliza como almacén local de hello en dispositivo Hola.

1. Instalar hello [en tiempo de ejecución de código de plataforma Universal de Windows hello](http://sqlite.org/2016/sqlite-uwp-3120200.vsix).
2. En Visual Studio, abra el Administrador de paquetes de NuGet hello para el proyecto de aplicación UWP Hola que completó en hello [crear una aplicación Windows] tutorial.
    Buscar e instalar hello **Microsoft.Azure.Mobile.Client.SQLiteStore** paquete NuGet.
3. En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** > **Agregar referencia...** >**Universal de Windows**>**Extensiones** y después habilite tanto **SQLite para la Plataforma universal de Windows** como **Tiempo de ejecución de Visual C++ 2015 para Aplicaciones de la Plataforma universal de Windows**.

    ![Incorporación de referencia de SQLite UWP][1]
4. Abra el archivo MainPage.xaml.cs de hello y quitar el comentario hello `#define OFFLINE_SYNC_ENABLED` definición.
5. En Visual Studio, presione hello **F5** clave toorebuild y aplicación de cliente de hello de ejecución. aplicación Hello funciona Hola igual que antes de habilitar la sincronización sin conexión. Sin embargo, la base de datos local de hello ahora se rellena con datos que pueden usarse en un escenario sin conexión.

## <a name="update-sync"></a>Actualizar toodisconnect de aplicación Hola de hello back-end
En esta sección, se interrumpe Hola conexión tooyour aplicación móvil back-end toosimulate una situación sin conexión. Cuando se agregan elementos de datos, el controlador de excepciones indica que la aplicación hello está en modo sin conexión. En este estado, elementos nuevos agregados en hello local almacenan y se sincronizarán para Hola back-end de aplicación móvil cuando la inserción se vuelva a ejecutar en un estado conectado.

1. Editar App.xaml.cs en proyecto compartido Hola. Comenta la inicialización de Hola de hello **MobileServiceClient** y agregue Hola después de línea, que utiliza una dirección URL de la aplicación móvil no válido:

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    También puede mostrar comportamiento sin conexión deshabilitando Wi-Fi y redes de telefonía móviles en dispositivo de Hola o usar el modo de avión.
2. Presione **F5** aplicación hello toobuild y ejecución. Tenga en cuenta la sincronización no se pudo al actualizar Hola cuando la aplicación inicia.
3. Escriba nuevos elementos y observe que la operación de inserción produce un error con un estado de [CancelledByNetworkError] cada vez que hace clic en **Guardar**. Sin embargo, nuevos elementos de lista de tareas Hola existen en el almacén local de hello hasta que estos se pueden insertar back-end de toohello aplicación móvil.  En uno de producción aplicación, si se suprimen las siguientes excepciones de aplicación de cliente de hello se comporta como si aún está conectado back-end de toohello aplicación móvil.
4. Cierre la aplicación hello y reiníciela tooverify que elementos nuevos de Hola que creó están almacén local toohello persistente.
5. (Opcional) En Visual Studio, abra el **Explorador de servidores**. Navegar por la base de datos de tooyour en **Azure**->**bases de datos SQL**. Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**. Ahora puede examinar la tabla de base de datos SQL tooyour y su contenido. Compruebe que los datos de hello en la base de datos de back-end de hello no han cambiado.
6. (Opcional) Usar una herramienta REST como Fiddler o Postman tooquery su backend móvil, utilizando una consulta GET con el formato `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Actualizar tooreconnect de aplicación Hola su aplicación móvil de back-end
En esta sección, se vuelve a conectar Hola aplicación toohello aplicación móvil back-end. Estos cambios simulan una reconexión de red en la aplicación hello.

Cuando ejecuta por primera vez aplicación hello, Hola `OnNavigatedTo` llamadas del controlador de eventos `InitLocalStoreAsync`. Este método llama a su vez `SyncAsync` toosync local almacenar con la base de datos de back-end de Hola. aplicación Hello intenta toosync durante el inicio.

1. Abra App.xaml.cs en proyecto compartido hello y quite la inicialización anterior de `MobileServiceClient` URL de la aplicación móvil de toouse Hola Hola correcto.
2. Hola presione **F5** clave toorebuild y aplicación hello de ejecución. Hello aplicación sincroniza los cambios locales con back-end de aplicación móvil de Azure de hello mediante las operaciones de inserción y extracción cuando hello `OnNavigatedTo` ejecuta el controlador de eventos.
3. (Opcional) Hola de vista actualiza datos mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler. Se ha sincronizado aviso Hola datos entre la base de datos de back-end de aplicación móvil de Azure de Hola y el almacén local de Hola.
4. En la aplicación hello, haga clic en comprobar de hello cuadro junto a algunos de los elementos de toocomplete ellos en el almacén local de Hola.

   `UpdateCheckedTodoItem`llamadas `SyncAsync` elemento toosync cada completado con back-end de hello aplicación móvil. `SyncAsync` llama a las operaciones de inserción y extracción. Sin embargo, **cada vez que se ejecuta una extracción en una tabla que el cliente hello ha realizado cambios a, siempre se ejecuta automáticamente una inserción**. Este comportamiento garantiza que todas las tablas de almacén local de hello junto con las relaciones siguen siendo coherentes. Este comportamiento puede provocar una inserción inesperada.  Para obtener más información sobre este comportamiento, consulte [sincronización de datos sin conexión en aplicaciones móviles de Azure].

## <a name="api-summary"></a>Resumen de la API
características sin conexión de Hola de toosupport de servicios móviles, hemos usado hello [IMobileServiceSyncTable] de la interfaz y se inicializa [MobileServiceClient.SyncContext] [ synccontext] con una base de datos local de SQLite. Cuando sin conexión, las operaciones CRUD de hello normales para aplicaciones móviles trabajar como si aplicación hello aún está conectado mientras se realizan las operaciones de hello en el almacén local de Hola. Hola siguiendo métodos es almacén local de hello toosynchronize usado con el servidor de hello:

* **[PushAsync]**  porque este método es un miembro de [IMobileServicesSyncContext], cambios de todas las tablas se insertan toohello back-end. Solo los registros con los cambios locales se envían toohello server.
* **[PullAsync]**: se inicia una extracción desde [IMobileServiceSyncTable]. Cuando hay cambios realizados en la tabla de hello, una inserción implícita se ejecuta toomake seguro de que todas las tablas de almacén local de hello junto con las relaciones siguen siendo coherentes. Hola *pushOtherTables* parámetro controla si otras tablas en el contexto de Hola se insertan en una inserción implícita. Hola *consulta* parámetro toma un [IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery] u Hola de toofilter de cadena de consulta de OData devolvió datos. Hola *queryId* parámetro se utiliza sincronización incremental toodefine. Para más información, consulte [Sincronización de datos sin conexión en Azure Mobile Apps](app-service-mobile-offline-data-sync.md#how-sync-works).
* **[PurgeAsync]**  la aplicación debe llamar periódicamente a estos datos obsoletos de método toopurge desde el almacén local Hola. Hola de uso *forzar* parámetro cuando necesite toopurge los cambios que aún no se han sincronizado.

Para obtener más información sobre estos conceptos, consulte [Sincronización de datos sin conexión en Aplicaciones móviles de Azure](app-service-mobile-offline-data-sync.md#how-sync-works).

## <a name="more-info"></a>Más información
Hello en los temas siguientes ofrecen información general adicional en la característica de sincronización sin conexión de Hola de aplicaciones móviles:

* [sincronización de datos sin conexión en aplicaciones móviles de Azure]
* [Procedimiento del SDK de .NET de Azure Mobile Apps][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[sincronización de datos sin conexión en aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md
[Creación de una aplicación para Windows]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[CancelledByNetworkError]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
