---
title: "Activación de la sincronización sin conexión para una aplicación móvil de Azure (Cordova) | Microsoft Docs"
description: "Obtenga información acerca de cómo usar la aplicación móvil de Servicios de aplicaciones para almacenar en caché y sincronizar datos sin conexión en su aplicación Cordova"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 45e80ca672dfdb6defc6e5c1aac3d29f5479125c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="db78d-103">Activación de la sincronización sin conexión para una aplicación móvil Cordova</span><span class="sxs-lookup"><span data-stu-id="db78d-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="db78d-104">Este tutorial presenta la característica de sincronización sin conexión de Aplicaciones móviles de Azure para Cordova.</span><span class="sxs-lookup"><span data-stu-id="db78d-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="db78d-105">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil &mdash;ver, agregar o modificar datos&mdash; aun cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="db78d-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="db78d-106">Los cambios se almacenan en una base de datos local.</span><span class="sxs-lookup"><span data-stu-id="db78d-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="db78d-107">Una vez que el dispositivo se vuelve a conectar, estos cambios se sincronizan con el servicio remoto.</span><span class="sxs-lookup"><span data-stu-id="db78d-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="db78d-108">Este tutorial se basa en la solución de inicio rápido de Cordova para aplicaciones móviles que crea al completar el tutorial [Inicio rápido de Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="db78d-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="db78d-109">En este tutorial, actualizará la solución de inicio rápido para agregar las características sin conexión de Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="db78d-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="db78d-110">También nos centraremos en el código sin conexión específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db78d-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="db78d-111">Para obtener más información acerca de la característica de sincronización sin conexión, consulte el tema [Sincronización de datos sin conexión en Aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="db78d-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="db78d-112">Para obtener detalles de uso de la API, consulte la [documentación de la API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="db78d-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="db78d-113">Adición de sincronización sin conexión a la solución de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="db78d-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="db78d-114">El código de sincronización sin conexión debe agregarse a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db78d-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="db78d-115">La sincronización sin conexión requiere el complemento cordova-sqlite-storage, que se agrega automáticamente a la aplicación cuando el complemento Aplicaciones móviles de Azure se incluye en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="db78d-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="db78d-116">El proyecto de inicio rápido incluye ambos complementos.</span><span class="sxs-lookup"><span data-stu-id="db78d-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="db78d-117">En el Explorador de soluciones de Visual Studio, abra index.js y reemplace el código siguiente</span><span class="sxs-lookup"><span data-stu-id="db78d-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="db78d-118">por este otro:</span><span class="sxs-lookup"><span data-stu-id="db78d-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="db78d-119">Luego, reemplace el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="db78d-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="db78d-120">por este otro:</span><span class="sxs-lookup"><span data-stu-id="db78d-120">with this code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="db78d-121">Las adiciones de los códigos anteriores inicializan el almacén local y definen una tabla local que coincide con los valores de columna utilizados en el back-end de Azure.</span><span class="sxs-lookup"><span data-stu-id="db78d-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="db78d-122">(No hace falta incluir todos los valores de columna en este código.)  El campo `version` se mantiene mediante el back-end móvil y se usa para la resolución de conflictos.</span><span class="sxs-lookup"><span data-stu-id="db78d-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="db78d-123">Para obtener una referencia al contexto de sincronización, llame a **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="db78d-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="db78d-124">El contexto de sincronización ayuda a mantener las relaciones entre tablas mediante el seguimiento y la inserción de los cambios en todas las tablas modificadas por una aplicación cliente cuando se llama a `.push()` .</span><span class="sxs-lookup"><span data-stu-id="db78d-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="db78d-125">Actualice la dirección URL de la aplicación a la de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="db78d-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="db78d-126">Ahora, reemplace este código:</span><span class="sxs-lookup"><span data-stu-id="db78d-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="db78d-127">por este otro:</span><span class="sxs-lookup"><span data-stu-id="db78d-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="db78d-128">El código anterior inicializa el contexto de sincronización y, después, llama a getSyncTable (en lugar de getTable) para obtener una referencia a la tabla local.</span><span class="sxs-lookup"><span data-stu-id="db78d-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="db78d-129">Este código usa la base de datos local para todas las operaciones de creación, lectura, actualización y eliminación (CRUD) de tablas.</span><span class="sxs-lookup"><span data-stu-id="db78d-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="db78d-130">En este ejemplo se realiza un control de errores simple en los conflictos de sincronización.</span><span class="sxs-lookup"><span data-stu-id="db78d-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="db78d-131">Una aplicación real controlaría los diversos errores, como los problemas en la red, los conflictos del servidor, etc.</span><span class="sxs-lookup"><span data-stu-id="db78d-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="db78d-132">Para obtener ejemplos de código, vea el [ejemplo de sincronización sin conexión].</span><span class="sxs-lookup"><span data-stu-id="db78d-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="db78d-133">A continuación, agregue esta función para realizar la sincronización real.</span><span class="sxs-lookup"><span data-stu-id="db78d-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="db78d-134">Decida cuándo se deben insertar los cambios en el back-end de Mobile App mediante la llamada a **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="db78d-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="db78d-135">Por ejemplo, podría llamar a **syncBackend** en un controlador de eventos de botón asociado a un botón de sincronización.</span><span class="sxs-lookup"><span data-stu-id="db78d-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="db78d-136">Consideraciones sobre la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="db78d-136">Offline sync considerations</span></span>

<span data-ttu-id="db78d-137">En el ejemplo, el método **push** de **syncContext** solo se llama en el inicio de la aplicación en la función de devolución de llamada del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="db78d-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="db78d-138">En una aplicación real, también puede hacer que esta funcionalidad de sincronización se desencadene manualmente cuando cambia el estado de la red.</span><span class="sxs-lookup"><span data-stu-id="db78d-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="db78d-139">Si se ejecuta una extracción en una tabla que tiene actualizaciones locales pendientes rastreadas por el contexto, la operación de extracción desencadenará de forma automática una inserción.</span><span class="sxs-lookup"><span data-stu-id="db78d-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="db78d-140">Al actualizar, agregar y completar elementos en este ejemplo, se puede omitir la llamada explícita a **push**, ya que puede ser redundante.</span><span class="sxs-lookup"><span data-stu-id="db78d-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="db78d-141">En el código proporcionado, se consultan todos los registros de la tabla todoItem remota, pero también es posible filtrar registros pasando un identificador de consulta y una consulta a **push**.</span><span class="sxs-lookup"><span data-stu-id="db78d-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="db78d-142">Para más información, consulte la sección *Sincronización incremental* en [Sincronización de datos sin conexión en Aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="db78d-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="db78d-143">(Opcional) Deshabilitación de la autenticación</span><span class="sxs-lookup"><span data-stu-id="db78d-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="db78d-144">Si no quiere configurar la autenticación antes de probar la sincronización sin conexión, convierta en comentario la función de devolución de llamada del inicio de sesión, pero deje el código de la función de devolución de llamada sin comentarios.</span><span class="sxs-lookup"><span data-stu-id="db78d-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="db78d-145">Después de convertir en comentario las líneas de inicio, sigue el código:</span><span class="sxs-lookup"><span data-stu-id="db78d-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="db78d-146">Ahora, la aplicación, cuando se ejecuta, se sincroniza con el back-end de Azure.</span><span class="sxs-lookup"><span data-stu-id="db78d-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="db78d-147">Ejecución de la aplicación cliente</span><span class="sxs-lookup"><span data-stu-id="db78d-147">Run the client app</span></span>
<span data-ttu-id="db78d-148">Con la sincronización sin conexión ahora habilitada, puede ejecutar la aplicación cliente al menos una vez en cada plataforma para rellenar la base de datos del almacén local.</span><span class="sxs-lookup"><span data-stu-id="db78d-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="db78d-149">Después, simulará un escenario sin conexión y modificará los datos del almacén local mientras la aplicación está sin conexión.</span><span class="sxs-lookup"><span data-stu-id="db78d-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="db78d-150">(Opcional) Prueba del comportamiento de la sincronización</span><span class="sxs-lookup"><span data-stu-id="db78d-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="db78d-151">En esta sección, modificará el proyecto de cliente para simular un escenario sin conexión usando una dirección URL de aplicación no válida para el back-end.</span><span class="sxs-lookup"><span data-stu-id="db78d-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="db78d-152">Al agregar o cambiar elementos de datos, estos cambios se conservan en el almacén local, pero no se sincronizan con el almacén de datos de back-end hasta que se restablece la conexión.</span><span class="sxs-lookup"><span data-stu-id="db78d-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="db78d-153">En el Explorador de soluciones, abra el archivo de proyecto index.js y cambie la dirección URL de la aplicación para que apunte a una dirección URL no válida como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="db78d-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="db78d-154">En index.html, actualice el elemento `<meta>` de CSP con la misma dirección URL no válida.</span><span class="sxs-lookup"><span data-stu-id="db78d-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="db78d-155">Compile y ejecute la aplicación cliente, y observe que se registra una excepción en la consola cuando la aplicación intenta sincronizarse con el back-end después del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="db78d-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="db78d-156">Los nuevos elementos que agrega solo existirán en el almacén local hasta que se puedan insertar en el back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="db78d-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="db78d-157">La aplicación cliente se comporta como si estuviera conectada al back-end.</span><span class="sxs-lookup"><span data-stu-id="db78d-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="db78d-158">Cierre la aplicación y reiníciela para comprobar que los nuevos elementos que creó se mantienen en el almacén local.</span><span class="sxs-lookup"><span data-stu-id="db78d-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="db78d-159">(Opcional) Use Visual Studio para ver la tabla de base de datos SQL de Azure y observar que los datos de la base de datos de back-end no han cambiado.</span><span class="sxs-lookup"><span data-stu-id="db78d-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="db78d-160">En Visual Studio, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="db78d-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="db78d-161">Vaya a la base de datos en **Azure**->**SQL Databases**.</span><span class="sxs-lookup"><span data-stu-id="db78d-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="db78d-162">Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="db78d-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="db78d-163">Ahora puede buscar la tabla de base de datos SQL y su contenido.</span><span class="sxs-lookup"><span data-stu-id="db78d-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="db78d-164">(Opcional) Prueba de la reconexión a un back-end móvil</span><span class="sxs-lookup"><span data-stu-id="db78d-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="db78d-165">En esta sección se volverá a conectar la aplicación al back-end móvil, que simula que la aplicación vuelve a un estado en línea.</span><span class="sxs-lookup"><span data-stu-id="db78d-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="db78d-166">Cuando inicia sesión, los datos se sincronizan con el back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="db78d-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="db78d-167">Vuelva a abrir index.js y restaure la dirección URL de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db78d-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="db78d-168">Vuelva a abrir index.html y corrija la dirección URL de la aplicación en el elemento `<meta>` de CSP.</span><span class="sxs-lookup"><span data-stu-id="db78d-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="db78d-169">Vuelva a compilar la aplicación cliente y ejecútela.</span><span class="sxs-lookup"><span data-stu-id="db78d-169">Rebuild and run the client app.</span></span> <span data-ttu-id="db78d-170">La aplicación intenta sincronizarse con el back-end de la aplicación móvil después del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="db78d-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="db78d-171">Compruebe que no hay excepciones registradas en la consola de depuración.</span><span class="sxs-lookup"><span data-stu-id="db78d-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="db78d-172">(Opcional) Vea los datos actualizados mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler.</span><span class="sxs-lookup"><span data-stu-id="db78d-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="db78d-173">Observe que los datos se han sincronizado entre la base de datos back-end y el almacén local.</span><span class="sxs-lookup"><span data-stu-id="db78d-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="db78d-174">Observe que los datos se han sincronizado entre la base de datos y el almacén local, y contienen los elementos que agregó mientras la aplicación estaba desconectada.</span><span class="sxs-lookup"><span data-stu-id="db78d-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="db78d-175">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="db78d-175">Additional resources</span></span>
* <span data-ttu-id="db78d-176">[Sincronización de datos sin conexión en Aplicaciones móviles de Azure]</span><span class="sxs-lookup"><span data-stu-id="db78d-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="db78d-177">[Visual Studio Tools para Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="db78d-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="db78d-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db78d-178">Next steps</span></span>
* <span data-ttu-id="db78d-179">Examine características de sincronización sin conexión más avanzadas, como la resolución de conflictos, en el [ejemplo de sincronización sin conexión]</span><span class="sxs-lookup"><span data-stu-id="db78d-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="db78d-180">Examine la referencia de API de sincronización sin conexión en la [documentación de la API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="db78d-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="db78d-181">[Inicio rápido de Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="db78d-181">[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="db78d-182">[ejemplo de sincronización sin conexión]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span><span class="sxs-lookup"><span data-stu-id="db78d-182">[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span></span>
<span data-ttu-id="db78d-183">[Sincronización de datos sin conexión en Aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="db78d-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
<span data-ttu-id="db78d-184">[Visual Studio Tools para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="db78d-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
