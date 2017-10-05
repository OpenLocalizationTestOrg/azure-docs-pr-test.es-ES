---
title: "Activación de la sincronización sin conexión para la aplicación móvil de Azure (Xamarin Android)"
description: "Obtenga información acerca de cómo usar la aplicación móvil del Servicio de aplicaciones para almacenar en caché y sincronizar datos sin conexión en su aplicación Xamarin Android."
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
ms.openlocfilehash: 471433c7ef2f6f128210ed145f685b42b44eea92
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a><span data-ttu-id="28323-103">Activación de la sincronización sin conexión para la aplicación móvil Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="28323-103">Enable offline sync for your Xamarin.Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="28323-104">Información general</span><span class="sxs-lookup"><span data-stu-id="28323-104">Overview</span></span>
<span data-ttu-id="28323-105">Este tutorial presenta la característica de sincronización sin conexión de Aplicaciones móviles de Azure para Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="28323-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Android.</span></span> <span data-ttu-id="28323-106">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil (ver, agregar o modificar datos), incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="28323-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="28323-107">Los cambios se almacenan en una base de datos local.</span><span class="sxs-lookup"><span data-stu-id="28323-107">Changes are stored in a local database.</span></span>
<span data-ttu-id="28323-108">Una vez que el dispositivo se vuelve a conectar, estos cambios se sincronizan con el servicio remoto.</span><span class="sxs-lookup"><span data-stu-id="28323-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="28323-109">En este tutorial, se actualiza el proyecto de cliente del tutorial [Creación de una aplicación Xamarin.Android] para conseguir compatibilidad con las características sin conexión de Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="28323-109">In this tutorial, you update the client project from the tutorial [Create a Xamarin Android app] to support the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="28323-110">Si no usa el proyecto de servidor de inicio rápido descargado, debe agregar paquetes de extensión de acceso de datos al proyecto.</span><span class="sxs-lookup"><span data-stu-id="28323-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="28323-111">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [Trabajar con el SDK del servidor back-end de .NET para Aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="28323-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="28323-112">Para obtener más información acerca de la característica de sincronización sin conexión, consulte el tema [Sincronización de datos sin conexión en Aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="28323-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-client-app-to-support-offline-features"></a><span data-ttu-id="28323-113">Actualización de la aplicación cliente para que admita características sin conexión</span><span class="sxs-lookup"><span data-stu-id="28323-113">Update the client app to support offline features</span></span>
<span data-ttu-id="28323-114">Las características sin conexión de Aplicaciones móviles de Azure permiten interactuar con una base de datos local cuando el usuario se encuentra en un escenario sin conexión.</span><span class="sxs-lookup"><span data-stu-id="28323-114">Azure Mobile App offline features allow you to interact with a local database when you are in an offline scenario.</span></span> <span data-ttu-id="28323-115">Para usar estas características en una aplicación, inicialice [SyncContext] en un almacén local.</span><span class="sxs-lookup"><span data-stu-id="28323-115">To use these features in your app, you initialize a [SyncContext] to a local store.</span></span> <span data-ttu-id="28323-116">A continuación, haga referencia a su tabla mediante la interfaz [IMobileServiceSyncTable][IMobileServiceSyncTable].</span><span class="sxs-lookup"><span data-stu-id="28323-116">Then reference your table through the [IMobileServiceSyncTable][IMobileServiceSyncTable] interface.</span></span> <span data-ttu-id="28323-117">SQLite se utiliza como almacén local en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="28323-117">SQLite is used as the local store on the device.</span></span>

1. <span data-ttu-id="28323-118">En Visual Studio, abra el administrador de paquetes NuGet en el proyecto que completó en el tutorial [Creación de una aplicación Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="28323-118">In Visual Studio, open the NuGet package manager in the project that you completed in the [Create a Xamarin Android app] tutorial.</span></span>  <span data-ttu-id="28323-119">Busque e instale el paquete NuGet **Microsoft.Azure.Mobile.Client.SQLiteStore**.</span><span class="sxs-lookup"><span data-stu-id="28323-119">Search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package.</span></span>
2. <span data-ttu-id="28323-120">Abra el archivo ToDoActivity.cs y quite la marca de comentario de la definición de `#define OFFLINE_SYNC_ENABLED`.</span><span class="sxs-lookup"><span data-stu-id="28323-120">Open the ToDoActivity.cs file and uncomment the `#define OFFLINE_SYNC_ENABLED` definition.</span></span>
3. <span data-ttu-id="28323-121">En Visual Studio, presione la tecla **F5** para volver a compilar y ejecutar la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="28323-121">In Visual Studio, press the **F5** key to rebuild and run the client app.</span></span> <span data-ttu-id="28323-122">La aplicación funciona igual que lo hacía antes de habilitar la sincronización sin conexión.</span><span class="sxs-lookup"><span data-stu-id="28323-122">The app works the same as it did before you enabled offline sync.</span></span> <span data-ttu-id="28323-123">Sin embargo, la base de datos se rellena con datos que pueden utilizarse en un escenario sin conexión.</span><span class="sxs-lookup"><span data-stu-id="28323-123">However, the local database is now populated with data that can be used in an offline scenario.</span></span>

## <span data-ttu-id="28323-124"><a name="update-sync"></a>Actualización de la aplicación para desconectarla del back-end</span><span class="sxs-lookup"><span data-stu-id="28323-124"><a name="update-sync"></a>Update the app to disconnect from the backend</span></span>
<span data-ttu-id="28323-125">En esta sección, se interrumpe la conexión con el back-end de aplicación móvil para simular un escenario sin conexión.</span><span class="sxs-lookup"><span data-stu-id="28323-125">In this section, you break the connection to your Mobile App backend to simulate an offline situation.</span></span> <span data-ttu-id="28323-126">Al agregar elementos de datos, el controlador de excepciones le indicará que la aplicación está en modo sin conexión.</span><span class="sxs-lookup"><span data-stu-id="28323-126">When you add data items, your exception handler tells you that the app is in offline mode.</span></span> <span data-ttu-id="28323-127">En este estado, se agregan nuevos elementos al almacén local y se sincronizan con el back-end de la aplicación móvil cuando se ejecute una inserción en estado conectado.</span><span class="sxs-lookup"><span data-stu-id="28323-127">In this state, new items added in the local store and are synced to the mobile app backend when a push is executed in a connected state.</span></span>

1. <span data-ttu-id="28323-128">Edite ToDoActivity.cs en el proyecto compartido.</span><span class="sxs-lookup"><span data-stu-id="28323-128">Edit ToDoActivity.cs in the shared project.</span></span> <span data-ttu-id="28323-129">Cambie **applicationURL** para que apunte a una dirección URL no válida:</span><span class="sxs-lookup"><span data-stu-id="28323-129">Change the **applicationURL** to point to an invalid URL:</span></span>

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    <span data-ttu-id="28323-130">Además, puede mostrar el comportamiento sin conexión mediante la deshabilitación de las redes Wi-Fi y móvil en el dispositivo o el uso del modo avión.</span><span class="sxs-lookup"><span data-stu-id="28323-130">You can also demonstrate offline behavior by disabling wifi and cellular networks on the device or using airplane mode.</span></span>
2. <span data-ttu-id="28323-131">Presione **F5** para compilar y ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28323-131">Press **F5** to build and run the app.</span></span> <span data-ttu-id="28323-132">Observe que la sincronización no se pudo actualizar cuando se inició la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28323-132">Notice your sync failed on refresh when the app launched.</span></span>
3. <span data-ttu-id="28323-133">Escriba nuevos elementos y observe que la operación de inserción produce un error con un estado de [CancelledByNetworkError] cada vez que hace clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="28323-133">Enter new items and notice that push fails with a [CancelledByNetworkError] status each time you click **Save**.</span></span> <span data-ttu-id="28323-134">No obstante, los nuevos elementos Todo están en el almacén local hasta que se puedan insertar en el back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="28323-134">However, the new todo items exist in the local store until they can be pushed to the mobile app backend.</span></span>  <span data-ttu-id="28323-135">En una aplicación de producción, si suprime estas excepciones, la aplicación cliente se comporta como si aún estuviera conectada al back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="28323-135">In a production app, if you suppress these exceptions the client app behaves as if it's still connected to the mobile app backend.</span></span>
4. <span data-ttu-id="28323-136">Cierre la aplicación y reiníciela para comprobar que los nuevos elementos que creó se mantienen en el almacén local.</span><span class="sxs-lookup"><span data-stu-id="28323-136">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="28323-137">(Opcional) En Visual Studio, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="28323-137">(Optional) In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="28323-138">Vaya a la base de datos en **Azure**->**SQL Databases**.</span><span class="sxs-lookup"><span data-stu-id="28323-138">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="28323-139">Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="28323-139">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="28323-140">Ahora puede buscar la tabla de base de datos SQL y su contenido.</span><span class="sxs-lookup"><span data-stu-id="28323-140">Now you can browse to your SQL database table and its contents.</span></span> <span data-ttu-id="28323-141">Compruebe que no han cambiado los datos de la base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="28323-141">Verify that the data in the backend database has not changed.</span></span>
6. <span data-ttu-id="28323-142">(Opcional) Use una herramienta REST como Fiddler o Postman para consultar el back-end móvil mediante una consulta GET con la forma `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="28323-142">(Optional) Use a REST tool such as Fiddler or Postman to query your mobile backend, using a GET query in the form `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.</span></span>

## <span data-ttu-id="28323-143"><a name="update-online-app"></a>Actualización de la aplicación para volver a conectar el back-end de la aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="28323-143"><a name="update-online-app"></a>Update the app to reconnect your Mobile App backend</span></span>
<span data-ttu-id="28323-144">En esta sección, vuelva a conectar la aplicación al back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="28323-144">In this section, reconnect the app to the mobile app backend.</span></span> <span data-ttu-id="28323-145">La primera vez que se ejecuta la aplicación, el controlador de eventos `OnCreate` llama a `OnRefreshItemsSelected`.</span><span class="sxs-lookup"><span data-stu-id="28323-145">When you first run the application, the `OnCreate` event handler calls `OnRefreshItemsSelected`.</span></span> <span data-ttu-id="28323-146">Este método llama a `SyncAsync` para sincronizar el almacén local con la base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="28323-146">This method calls `SyncAsync` to sync your local store with the backend database.</span></span>

1. <span data-ttu-id="28323-147">Abra ToDoActivity.cs en el proyecto compartido y revierta el cambio de la propiedad **applicationURL**.</span><span class="sxs-lookup"><span data-stu-id="28323-147">Open ToDoActivity.cs in the shared project, and revert your change of the **applicationURL** property.</span></span>
2. <span data-ttu-id="28323-148">Presione la tecla **F5** para volver a compilar y ejecutar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="28323-148">Press the **F5** key to rebuild and run the app.</span></span> <span data-ttu-id="28323-149">La aplicación sincroniza los cambios locales con el back-end de Azure Mobile App mediante operaciones de inserción e incorporación de cambios cuando se ejecuta el método `OnRefreshItemsSelected`.</span><span class="sxs-lookup"><span data-stu-id="28323-149">The app syncs your local changes with the Azure Mobile App backend using push and pull operations when the `OnRefreshItemsSelected` method executes.</span></span>
3. <span data-ttu-id="28323-150">(Opcional) Vea los datos actualizados mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler.</span><span class="sxs-lookup"><span data-stu-id="28323-150">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="28323-151">Observe que los datos se han sincronizado entre la base de datos del back-end de la aplicación móvil de Azure y el almacén local.</span><span class="sxs-lookup"><span data-stu-id="28323-151">Notice the data has been synchronized between the Azure Mobile App backend database and the local store.</span></span>
4. <span data-ttu-id="28323-152">En la aplicación, haga clic en la casilla situada junto a algunos elementos para completarlos en el almacén local.</span><span class="sxs-lookup"><span data-stu-id="28323-152">In the app, click the check box beside a few items to complete them in the local store.</span></span>

   <span data-ttu-id="28323-153">`CheckItem` llama a `SyncAsync` para sincronizar cada elemento completado con el back-end de Mobile App.</span><span class="sxs-lookup"><span data-stu-id="28323-153">`CheckItem` calls `SyncAsync` to sync each completed item with the Mobile App backend.</span></span> <span data-ttu-id="28323-154">`SyncAsync` llama a las operaciones de inserción y extracción.</span><span class="sxs-lookup"><span data-stu-id="28323-154">`SyncAsync` calls both push and pull.</span></span> <span data-ttu-id="28323-155">**Cada vez que se ejecuta una incorporación de cambios en una tabla en la que el cliente ha realizado cambios, siempre se ejecuta automáticamente una inserción**.</span><span class="sxs-lookup"><span data-stu-id="28323-155">**Whenever you execute a pull against a table that the client has made changes to, a push is always executed automatically**.</span></span> <span data-ttu-id="28323-156">De este modo se garantiza la coherencia de todas las tablas del almacén local, junto con sus relaciones.</span><span class="sxs-lookup"><span data-stu-id="28323-156">This ensures all tables in the local store along with relationships remain consistent.</span></span> <span data-ttu-id="28323-157">Este comportamiento puede provocar una inserción inesperada.</span><span class="sxs-lookup"><span data-stu-id="28323-157">This behavior may result in an unexpected push.</span></span> <span data-ttu-id="28323-158">Para obtener más información sobre este comportamiento, consulte [Sincronización de datos sin conexión en Aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="28323-158">For more information on this behavior, see [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="28323-159">Revisión del código de sincronización de cliente</span><span class="sxs-lookup"><span data-stu-id="28323-159">Review the client sync code</span></span>
<span data-ttu-id="28323-160">El proyecto de cliente de Xamarin que descargó cuando completó el tutorial [Creación de una aplicación Xamarin.Android] ya contiene el código que admite la sincronización sin conexión con una base de datos SQLite local.</span><span class="sxs-lookup"><span data-stu-id="28323-160">The Xamarin client project that you downloaded when you completed the tutorial [Create a Xamarin Android app] already contains code supporting offline synchronization using a local SQLite database.</span></span> <span data-ttu-id="28323-161">Esta es una breve descripción de lo que ya está incluido en el código del tutorial.</span><span class="sxs-lookup"><span data-stu-id="28323-161">Here is a brief overview of what is already included in the tutorial code.</span></span> <span data-ttu-id="28323-162">Para obtener información general conceptual de la característica, consulte [Sincronización de datos sin conexión en Aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="28323-162">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps].</span></span>

* <span data-ttu-id="28323-163">Antes de poder realizar cualquier operación de tabla, se debe inicializar el almacén local.</span><span class="sxs-lookup"><span data-stu-id="28323-163">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="28323-164">La base de datos del almacén local se inicializa cuando `ToDoActivity.OnCreate()` ejecuta `ToDoActivity.InitLocalStoreAsync()`.</span><span class="sxs-lookup"><span data-stu-id="28323-164">The local store database is initialized when `ToDoActivity.OnCreate()` executes `ToDoActivity.InitLocalStoreAsync()`.</span></span> <span data-ttu-id="28323-165">Este método crea una base de datos SQLite local que usa la clase `MobileServiceSQLiteStore` que proporciona el SDK de cliente de Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="28323-165">This method creates a local SQLite database using the `MobileServiceSQLiteStore` class provided by the Azure Mobile Apps client SDK.</span></span>

    <span data-ttu-id="28323-166">El método `DefineTable` crea una tabla en el almacén local que coincide con los campos del tipo proporcionado, `ToDoItem` en este caso.</span><span class="sxs-lookup"><span data-stu-id="28323-166">The `DefineTable` method creates a table in the local store that matches the fields in the provided type, `ToDoItem` in this case.</span></span> <span data-ttu-id="28323-167">El tipo no tiene que incluir todas las columnas que se encuentran en la base de datos remota.</span><span class="sxs-lookup"><span data-stu-id="28323-167">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="28323-168">Es posible almacenar solo un subconjunto de columnas.</span><span class="sxs-lookup"><span data-stu-id="28323-168">It is possible to store just a subset of columns.</span></span>

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code to initialize the SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses the default conflict handler, which fails on conflict
            // To use a different conflict handler, pass a parameter to InitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* <span data-ttu-id="28323-169">El miembro `toDoTable` de `ToDoActivity` es del tipo `IMobileServiceSyncTable` en lugar de `IMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="28323-169">The `toDoTable` member of `ToDoActivity` is of the `IMobileServiceSyncTable` type instead of `IMobileServiceTable`.</span></span> <span data-ttu-id="28323-170">IMobileServiceSyncTable dirige todas las operaciones de la tabla de creación, lectura, actualización y eliminación (CRUD) a la base de datos del almacén local.</span><span class="sxs-lookup"><span data-stu-id="28323-170">The IMobileServiceSyncTable directs all create, read, update, and delete (CRUD) table operations to the local store database.</span></span>

    <span data-ttu-id="28323-171">Usted decide en qué momento se insertan los cambios en el back-end Azure Mobile App mediante una llamada a `IMobileServiceSyncContext.PushAsync()`.</span><span class="sxs-lookup"><span data-stu-id="28323-171">You decide when changes are pushed to the Azure Mobile App backend by calling `IMobileServiceSyncContext.PushAsync()`.</span></span> <span data-ttu-id="28323-172">El contexto de sincronización ayuda a mantener las relaciones entre tablas mediante el seguimiento y la inserción de los cambios en todas las tablas modificadas por una aplicación cliente cuando se llama a `PushAsync` .</span><span class="sxs-lookup"><span data-stu-id="28323-172">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `PushAsync` is called.</span></span>

    <span data-ttu-id="28323-173">El código proporcionado llama a `ToDoActivity.SyncAsync()` para sincronizarse cada vez que se actualiza la lista todoitem o se agrega o completa un todoitem.</span><span class="sxs-lookup"><span data-stu-id="28323-173">The provided code calls `ToDoActivity.SyncAsync()` to sync whenever the todoitem list is refreshed or a todoitem is added or completed.</span></span> <span data-ttu-id="28323-174">El código se sincroniza después de cada cambio local.</span><span class="sxs-lookup"><span data-stu-id="28323-174">The code syncs after every local change.</span></span>

    <span data-ttu-id="28323-175">En el ejemplo proporcionado, se consultan todos los registros de la tabla `TodoItem` remota, pero también es posible filtrar registros pasando un identificador de consulta y una consulta a `PushAsync`.</span><span class="sxs-lookup"><span data-stu-id="28323-175">In the provided code, all records in the remote `TodoItem` table are queried, but it is also possible to filter records by passing a query id and query to `PushAsync`.</span></span> <span data-ttu-id="28323-176">Para más información, consulte la sección *Sincronización incremental* en [Sincronización de datos sin conexión en Aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="28323-176">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating the Mobile Service. Verify the URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a><span data-ttu-id="28323-177">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="28323-177">Additional Resources</span></span>
* <span data-ttu-id="28323-178">[Sincronización de datos sin conexión en Aplicaciones móviles de Azure]</span><span class="sxs-lookup"><span data-stu-id="28323-178">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="28323-179">[Procedimiento del SDK de .NET de Azure Mobile Apps][8]</span><span class="sxs-lookup"><span data-stu-id="28323-179">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
<span data-ttu-id="28323-180">[Creación de una aplicación Xamarin.Android]: ../app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="28323-180">[Create a Xamarin Android app]: ../app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="28323-181">[Sincronización de datos sin conexión en Aplicaciones móviles de Azure]: ../app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="28323-181">[Offline Data Sync in Azure Mobile Apps]: ../app-service-mobile-offline-data-sync.md</span></span>

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="28323-182">[Creación de una aplicación Xamarin Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="28323-182">[Create a Xamarin Android app]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="28323-183">[Sincronización de datos sin conexión en Aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="28323-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
<span data-ttu-id="28323-184">[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="28323-184">[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx</span></span>
[8]: app-service-mobile-dotnet-how-to-use-client-library.md