---
title: "aaaEnable la sincronización sin conexión de la aplicación móvil de Azure (Cordova) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse la toocache y sincronización de datos sin conexión de aplicación del servicio de aplicaciones móviles en la aplicación de Cordova"
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
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="2a689-103">Activación de la sincronización sin conexión para una aplicación móvil Cordova</span><span class="sxs-lookup"><span data-stu-id="2a689-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="2a689-104">Este tutorial presenta la característica de sincronización sin conexión de Hola de aplicaciones móviles de Azure para Cordova.</span><span class="sxs-lookup"><span data-stu-id="2a689-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="2a689-105">Sincronización sin conexión permite toointeract de los usuarios finales con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="2a689-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="2a689-106">Los cambios se almacenan en una base de datos local.</span><span class="sxs-lookup"><span data-stu-id="2a689-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="2a689-107">Una vez que el dispositivo de hello vuelve a estar conectado, estos cambios se sincronizan con el servicio remoto hello.</span><span class="sxs-lookup"><span data-stu-id="2a689-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="2a689-108">Este tutorial se basa en hello solución de inicio rápido de Cordova para aplicaciones móviles que crea al completar Hola tutorial [inicio rápido de Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="2a689-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="2a689-109">En este tutorial, va a actualizar Hola quickstart solución tooadd características sin conexión de las aplicaciones móviles de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a689-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="2a689-110">También se resalte código de sin conexión específicas de hello en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2a689-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="2a689-111">toolearn más información acerca de la característica de sincronización sin conexión de hello, vea el tema de hello [sincronización de datos sin conexión en aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="2a689-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="2a689-112">Para obtener detalles de uso de la API, vea hello [documentación de la API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="2a689-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="2a689-113">Agregar la solución de inicio rápido de toohello de sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="2a689-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="2a689-114">se debe agregar código de sincronización sin conexión de Hello toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a689-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="2a689-115">Sincronización sin conexión requiere el complemento de almacenamiento de sqlite cordova hello, que automáticamente se agrega tooyour aplicación al complemento de aplicaciones móviles de Azure Hola se incluye en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a689-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="2a689-116">proyecto de inicio rápido de Hello incluye los dos de estos complementos.</span><span class="sxs-lookup"><span data-stu-id="2a689-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="2a689-117">En el Explorador de soluciones de Visual Studio, abra index.js y reemplace Hola después de código</span><span class="sxs-lookup"><span data-stu-id="2a689-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="2a689-118">por este otro:</span><span class="sxs-lookup"><span data-stu-id="2a689-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="2a689-119">A continuación, reemplace Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="2a689-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="2a689-120">por este otro:</span><span class="sxs-lookup"><span data-stu-id="2a689-120">with this code:</span></span>

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

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    <span data-ttu-id="2a689-121">inicializar el almacén local de Hola Hola adiciones de código anterior y definir una tabla local que coincida con los valores de columna de hello utilizados en Azure back-end.</span><span class="sxs-lookup"><span data-stu-id="2a689-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="2a689-122">(No es necesario tooinclude todos los valores de columna en este código.)  Hola `version` campo se mantiene Hola móviles servidor back-end y se utiliza para la resolución de conflictos.</span><span class="sxs-lookup"><span data-stu-id="2a689-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="2a689-123">Obtiene un contexto de sincronización de toohello de referencia mediante una llamada a **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="2a689-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="2a689-124">Hello contexto de sincronización le ayuda a mantener las relaciones entre tablas de seguimiento e insertar los cambios en todas las tablas de una aplicación cliente modifica cuando `.push()` se llama.</span><span class="sxs-lookup"><span data-stu-id="2a689-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="2a689-125">Actualice la URL de aplicación de la aplicación móvil de tooyour de hello aplicación dirección URL.</span><span class="sxs-lookup"><span data-stu-id="2a689-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="2a689-126">Ahora, reemplace este código:</span><span class="sxs-lookup"><span data-stu-id="2a689-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="2a689-127">por este otro:</span><span class="sxs-lookup"><span data-stu-id="2a689-127">with this code:</span></span>

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="2a689-128">Hello anterior código inicializa el contexto de sincronización de hello y, a continuación, llama tooget getSyncTable (en lugar de getTable) una tabla de referencia toohello local.</span><span class="sxs-lookup"><span data-stu-id="2a689-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="2a689-129">Este código usa Hola base de datos local para todos los crear, leer, actualizar y eliminar operaciones (CRUD) de la tabla.</span><span class="sxs-lookup"><span data-stu-id="2a689-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="2a689-130">En este ejemplo se realiza un control de errores simple en los conflictos de sincronización.</span><span class="sxs-lookup"><span data-stu-id="2a689-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="2a689-131">Una aplicación real controlaría Hola varios errores como las condiciones de red, servidor entra en conflicto y otros.</span><span class="sxs-lookup"><span data-stu-id="2a689-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="2a689-132">Para obtener ejemplos de código, vea hello [ejemplo de sincronización sin conexión].</span><span class="sxs-lookup"><span data-stu-id="2a689-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="2a689-133">A continuación, agregue esta sincronización real de función tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="2a689-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="2a689-134">Decidir cuándo toopush cambia back-end de aplicación móvil de toohello mediante una llamada a **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="2a689-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="2a689-135">Por ejemplo, podría llamar a **syncBackend** en un botón de sincronización de tooa relacionados del controlador de eventos de botón.</span><span class="sxs-lookup"><span data-stu-id="2a689-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="2a689-136">Consideraciones sobre la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="2a689-136">Offline sync considerations</span></span>

<span data-ttu-id="2a689-137">En el ejemplo de Hola Hola **inserción** método **syncContext** solo se llama en el inicio de la aplicación en función de devolución de llamada de hello para el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2a689-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="2a689-138">En una aplicación del mundo real, también puede realizar esta funcionalidad de sincronización de forma manual o cuando cambia el estado de la red de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a689-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="2a689-139">Cuando se ejecuta una extracción en una tabla que tiene pendiente actualizaciones locales realiza un seguimiento mediante el contexto de hello, que extraen operación automáticamente desencadenadores una inserción.</span><span class="sxs-lookup"><span data-stu-id="2a689-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="2a689-140">Al actualizar, agregar y completar los elementos en este ejemplo, puede omitir Hola explícita **inserción** llamar, dado que puede ser redundante.</span><span class="sxs-lookup"><span data-stu-id="2a689-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="2a689-141">En el código de hello proporcionada, se consultan todos los registros de la tabla todoItem remoto de hello, pero también es posible toofilter registros pasando un identificador de la consulta y una consulta demasiado**inserción**.</span><span class="sxs-lookup"><span data-stu-id="2a689-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="2a689-142">Para obtener más información, vea la sección de hello *sincronización Incremental* en [sincronización de datos sin conexión en aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="2a689-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="2a689-143">(Opcional) Deshabilitación de la autenticación</span><span class="sxs-lookup"><span data-stu-id="2a689-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="2a689-144">Si no desea tooset la autenticación antes de probar la sincronización sin conexión, comente la función de devolución de llamada de hello para el inicio de sesión, pero deje el código de hello dentro de la función de devolución de llamada de hello sin comentarios.</span><span class="sxs-lookup"><span data-stu-id="2a689-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="2a689-145">Después de la creación de comentarios de las líneas de inicio de sesión de hello, código de hello sigue:</span><span class="sxs-lookup"><span data-stu-id="2a689-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="2a689-146">Ahora, Hola aplicación se sincronice con hello Azure back-end cuando se ejecuta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2a689-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="2a689-147">Ejecutar la aplicación de cliente hello</span><span class="sxs-lookup"><span data-stu-id="2a689-147">Run hello client app</span></span>
<span data-ttu-id="2a689-148">Con ahora habilitada la sincronización sin conexión, puede ejecutar aplicaciones de cliente de Hola de al menos una vez en cada plataforma para rellenar la base de datos de almacén local de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a689-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="2a689-149">Más adelante, simular un escenario sin conexión y modificar datos de hello en el almacén local de hello mientras está sin conexión la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2a689-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="2a689-150">(Opcional) Probar el comportamiento de sincronización de Hola</span><span class="sxs-lookup"><span data-stu-id="2a689-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="2a689-151">En esta sección, se modifique Hola cliente proyecto toosimulate un escenario sin conexión mediante el uso de una dirección URL de aplicación no válido para el back-end.</span><span class="sxs-lookup"><span data-stu-id="2a689-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="2a689-152">Al agregar o cambiar los elementos de datos, estos cambios se mantienen en el almacén local, pero no están sincronizados toohello almacén de datos de back-end hasta que se haya restablecido la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a689-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="2a689-153">Hola el Explorador de soluciones, abrir archivo de proyecto de hello index.js y cambie toopoint de dirección URL de aplicación Hola a una dirección URL no válida, como el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="2a689-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="2a689-154">En index.html, actualizar Hola CSP `<meta>` elemento con Hola la misma dirección URL no válido.</span><span class="sxs-lookup"><span data-stu-id="2a689-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="2a689-155">Crear y ejecutar la aplicación de cliente de hello y observe que una excepción se registra en la consola de hello cuando la aplicación hello intenta sincronizar con back-end de hello después de iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="2a689-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="2a689-156">Los elementos nuevos que agregue solo existen en almacén local de hello hasta que se insertan back-end de toohello móvil.</span><span class="sxs-lookup"><span data-stu-id="2a689-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="2a689-157">aplicación de cliente de Hello se comporta como si estuviera conectada toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="2a689-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="2a689-158">Cierre la aplicación hello y reiníciela tooverify que elementos nuevos de Hola que creó están almacén local toohello persistente.</span><span class="sxs-lookup"><span data-stu-id="2a689-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="2a689-159">(Opcional) Use Visual Studio tooview su toosee de tabla de base de datos de SQL Azure Hola datos en la base de datos de back-end de hello no han cambiado.</span><span class="sxs-lookup"><span data-stu-id="2a689-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="2a689-160">En Visual Studio, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="2a689-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="2a689-161">Navegar por la base de datos de tooyour en **Azure**->**bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="2a689-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="2a689-162">Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="2a689-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="2a689-163">Ahora puede examinar la tabla de base de datos SQL tooyour y su contenido.</span><span class="sxs-lookup"><span data-stu-id="2a689-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="2a689-164">(Opcional) Prueba Hola reconexión tooyour móviles back-end</span><span class="sxs-lookup"><span data-stu-id="2a689-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="2a689-165">En esta sección, se vuelve a conectar hello toohello móviles backend de la aplicación, que simula la aplicación hello que vuelve al estado en línea.</span><span class="sxs-lookup"><span data-stu-id="2a689-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="2a689-166">Cuando inicie sesión, los datos son móviles tooyour sincronizados back-end.</span><span class="sxs-lookup"><span data-stu-id="2a689-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="2a689-167">Vuelva a abrir index.js y restaurar la dirección URL de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2a689-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="2a689-168">Vuelva a abrir index.html y corrija la dirección URL de la aplicación Hola Hola CSP `<meta>` elemento.</span><span class="sxs-lookup"><span data-stu-id="2a689-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="2a689-169">Volver a generar y ejecutar la aplicación de cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="2a689-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="2a689-170">aplicación Hello intenta toosync con back-end de aplicación móvil de hello después de iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="2a689-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="2a689-171">Compruebe que ninguna excepción se registra en la consola de depuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a689-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="2a689-172">(Opcional) Hola de vista actualiza datos mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler.</span><span class="sxs-lookup"><span data-stu-id="2a689-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="2a689-173">Se ha sincronizado aviso Hola datos entre la base de datos de back-end de Hola y el almacén local de Hola.</span><span class="sxs-lookup"><span data-stu-id="2a689-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="2a689-174">Tenga en cuenta datos Hola se ha sincronizado entre la base de datos de Hola y el almacén local de Hola y contiene elementos de hello que agregó mientras la aplicación se desconectó.</span><span class="sxs-lookup"><span data-stu-id="2a689-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2a689-175">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2a689-175">Additional resources</span></span>
* <span data-ttu-id="2a689-176">[sincronización de datos sin conexión en aplicaciones móviles de Azure]</span><span class="sxs-lookup"><span data-stu-id="2a689-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="2a689-177">[Visual Studio Tools para Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="2a689-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a689-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a689-178">Next steps</span></span>
* <span data-ttu-id="2a689-179">Revisión de características de sincronización sin conexión, como la resolución de conflictos en hello más avanzadas [ejemplo de sincronización sin conexión]</span><span class="sxs-lookup"><span data-stu-id="2a689-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="2a689-180">Revise la sincronización sin conexión de hello referencia de API en hello [documentación de la API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="2a689-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[inicio rápido de Apache Cordova]: app-service-mobile-cordova-get-started.md
[ejemplo de sincronización sin conexión]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[sincronización de datos sin conexión en aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
