---
title: "aaaEnable la sincronización sin conexión de la aplicación móvil de Azure (Xamarin.Forms) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse la toocache y sincronización de datos sin conexión de aplicación del servicio de aplicaciones móviles en la aplicación de Xamarin.Forms"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="e8f2e-103">Habilitación de la sincronización sin conexión para la aplicación móvil Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="e8f2e-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="e8f2e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e8f2e-104">Overview</span></span>
<span data-ttu-id="e8f2e-105">Este tutorial presenta la característica de sincronización sin conexión de Hola de aplicaciones móviles de Azure para Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="e8f2e-106">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil (ver, agregar o modificar datos), incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="e8f2e-107">Los cambios se almacenan en una base de datos local.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-107">Changes are stored in a local database.</span></span> <span data-ttu-id="e8f2e-108">Una vez que el dispositivo de hello vuelve a estar conectado, estos cambios se sincronizan con el servicio remoto hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="e8f2e-109">Este tutorial se basa en hello solución de inicio rápido de Xamarin.Forms para las aplicaciones móviles que crea al completar el tutorial [crear una aplicación de iOS de Xamarin].</span><span class="sxs-lookup"><span data-stu-id="e8f2e-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="e8f2e-110">solución de inicio rápido de Hola para Xamarin.Forms contiene Hola código toosupport sincronización sin conexión, que solo necesita toobe habilitado.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="e8f2e-111">En este tutorial, va a actualizar hello tooturn de solución de inicio rápido sobre características sin conexión de Hola de aplicaciones móviles de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="e8f2e-112">También se resalte código de sin conexión específicas de hello en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="e8f2e-113">Si no utiliza soluciones de inicio rápido de hello descargado, debe agregar el proyecto tooyour de paquetes de extensión de acceso de hello datos.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="e8f2e-114">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure][1].</span><span class="sxs-lookup"><span data-stu-id="e8f2e-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="e8f2e-115">toolearn más información acerca de la característica de sincronización sin conexión de hello, vea el tema de hello [sincronización de datos sin conexión en aplicaciones móviles de Azure][2].</span><span class="sxs-lookup"><span data-stu-id="e8f2e-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="e8f2e-116">Habilitar la funcionalidad de sincronización sin conexión en la solución de inicio rápido de Hola</span><span class="sxs-lookup"><span data-stu-id="e8f2e-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="e8f2e-117">código de sincronización sin conexión de Hola se incluye en el proyecto de hello mediante el uso de directivas de preprocesador de C#.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="e8f2e-118">Cuando Hola **sin conexión\_sincronización\_habilitado** símbolo está definido, estas rutas de acceso de código se incluyen en la compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="e8f2e-119">Para las aplicaciones de Windows, también debe instalar platform de SQLite Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="e8f2e-120">En Visual Studio, haga clic en soluciones de hello > **administrar paquetes de NuGet para la solución...** , a continuación, buscar e instalar el **Microsoft.Azure.Mobile.Client.SQLiteStore** paquete NuGet para todos los proyectos de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="e8f2e-121">Hola el Explorador de soluciones, abra el archivo TodoItemManager.cs de hello del proyecto de Hola con **Portable** en nombre de hello, que es el proyecto de biblioteca de clases Portable, a continuación, quite Hola después de la directiva de preprocesador:</span><span class="sxs-lookup"><span data-stu-id="e8f2e-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="e8f2e-122">Dispositivos de Windows toosupport (opcional), instale uno de los siguientes paquetes en tiempo de ejecución de código de hello:</span><span class="sxs-lookup"><span data-stu-id="e8f2e-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="e8f2e-123">**Runtime de Windows 8.1:** instale [SQLite para Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="e8f2e-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="e8f2e-124">**Windows Phone 8.1:** instale [SQLite para Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="e8f2e-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="e8f2e-125">**Plataforma universal de Windows** instalar [SQLite para hello universales de Windows Universal][5].</span><span class="sxs-lookup"><span data-stu-id="e8f2e-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="e8f2e-126">Aunque el inicio rápido de hello no contiene un proyecto Universal de Windows, plataforma Universal de Windows de hello es compatible con Xamarin Forms.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="e8f2e-127">(Opcional) En cada proyecto de aplicación de Windows, haga clic en **referencias** > **Agregar referencia...** , expanda hello **Windows** carpeta > **extensiones**.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="e8f2e-128">Habilitar Hola adecuado **SQLite para Windows** SDK junto con hello **2013 en tiempo de ejecución para Windows de Visual C++** SDK.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="e8f2e-129">Hello SQLite SDK nombres varían ligeramente con cada plataforma de Windows.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="e8f2e-130">Revise el código de sincronización de cliente hello</span><span class="sxs-lookup"><span data-stu-id="e8f2e-130">Review hello client sync code</span></span>
<span data-ttu-id="e8f2e-131">Esta es una breve descripción de lo que ya está incluido en el código del tutorial Hola Hola `#if OFFLINE_SYNC_ENABLED` directivas.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="e8f2e-132">La funcionalidad de sincronización sin conexión está en archivo de proyecto TodoItemManager.cs de hello en el proyecto de biblioteca de clases Portable Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="e8f2e-133">Para obtener información conceptual de característica de hello, consulte [sin conexión la sincronización de datos en aplicaciones de Azure Mobile][2].</span><span class="sxs-lookup"><span data-stu-id="e8f2e-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="e8f2e-134">Para poder realizar cualquier operación de tabla, se debe inicializar el almacén local de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="e8f2e-135">base de datos del almacén local Hello se inicializa una Hola **TodoItemManager** constructor de clase mediante el uso de hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="e8f2e-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="e8f2e-136">Este código crea una nueva base de SQLite local mediante hello **MobileServiceSQLiteStore** clase.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="e8f2e-137">Hola **DefineTable** método crea una tabla de almacén local de Hola que coincida con los campos de hello en el tipo de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="e8f2e-138">tipo de Hello no tiene tooinclude todas las columnas de Hola que se encuentran en la base de datos remota Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="e8f2e-139">Es posible toostore un subconjunto de columnas.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="e8f2e-140">Hola **todoTable** campo **TodoItemManager** es un **IMobileServiceSyncTable** escriba en lugar de **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="e8f2e-141">Esta clase usa Hola base de datos local para todos los crear, leer, actualizar y eliminar operaciones (CRUD) de la tabla.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="e8f2e-142">Decidir si esos cambios se insertan back-end de aplicación móvil de toohello mediante una llamada a **PushAsync** en hello **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="e8f2e-143">Hello contexto de sincronización le ayuda a mantener las relaciones entre tablas de seguimiento e insertar los cambios en todas las tablas de una aplicación cliente modifica cuando **PushAsync** se llama.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="e8f2e-144">siguiente Hello **SyncAsync** toosync con back-end de aplicación móvil de Hola se llama al método:</span><span class="sxs-lookup"><span data-stu-id="e8f2e-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    <span data-ttu-id="e8f2e-145">Este ejemplo usa con el controlador de sincronización predeterminado de Hola de control de errores simple.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="e8f2e-146">Una aplicación real controlaría Hola varios errores al igual que las condiciones de red y el servidor está en conflicto mediante el comparador **IMobileServiceSyncHandler** implementación.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="e8f2e-147">Consideraciones sobre la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="e8f2e-147">Offline sync considerations</span></span>
<span data-ttu-id="e8f2e-148">En el ejemplo de Hola Hola **SyncAsync** solo es llamar al método de inicio y cuando se solicita una sincronización.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="e8f2e-149">tooinitiate una sincronización en una aplicación de Android o iOS, extracción hacia abajo en la lista de elementos de hello; para Windows, utilice hello **sincronización** botón.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="e8f2e-150">En una aplicación del mundo real, que podría realizar desencadenador de sincronización de hello cuando cambia el estado de la red de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="e8f2e-151">Cuando se ejecuta una extracción en una tabla que tiene pendiente actualizaciones locales realiza un seguimiento mediante el contexto de hello, que extraen operación automáticamente desencadenadores una inserción de contexto anterior.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="e8f2e-152">Al actualizar, agregar y completar los elementos en este ejemplo, puede omitir Hola explícita **PushAsync** llamar.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="e8f2e-153">En el código de hello proporcionada, se consultan todos los registros de la tabla TodoItem remota de hello, pero también es posible toofilter registros pasando un identificador de la consulta y una consulta demasiado**PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="e8f2e-154">Para obtener más información, vea la sección de hello *sincronización Incremental* en [sin conexión la sincronización de datos en aplicaciones de Azure Mobile][2].</span><span class="sxs-lookup"><span data-stu-id="e8f2e-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="e8f2e-155">Ejecutar la aplicación de cliente hello</span><span class="sxs-lookup"><span data-stu-id="e8f2e-155">Run hello client app</span></span>
<span data-ttu-id="e8f2e-156">Con ahora habilitada la sincronización sin conexión, ejecutar aplicación de cliente de hello al menos una vez en cada base de datos de almacén local de plataforma toopopulate Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="e8f2e-157">Más adelante, simular un escenario sin conexión y modificar datos de hello en el almacén local de hello mientras está sin conexión la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="e8f2e-158">Comportamiento de sincronización de Hola de aplicación de cliente de hello de la actualización</span><span class="sxs-lookup"><span data-stu-id="e8f2e-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="e8f2e-159">En esta sección, modificar Hola cliente proyecto toosimulate un escenario sin conexión mediante una dirección URL de aplicación no válido para el back-end.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="e8f2e-160">Como alternativa, puede desactivar las conexiones de red, mueva el dispositivo demasiado "Modo de avión".</span><span class="sxs-lookup"><span data-stu-id="e8f2e-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="e8f2e-161">Al agregar o cambiar los elementos de datos, estos cambios se conservan en el almacén local de hello, pero no sincronizan datos de back-end de toohello almacenan hasta que se haya restablecido la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="e8f2e-162">Hola el Explorador de soluciones, abra el archivo de proyecto de Constants.cs de Hola de hello **Portable** del proyecto y cambiar el valor de Hola de `ApplicationURL` toopoint dirección URL no válida de tooan:</span><span class="sxs-lookup"><span data-stu-id="e8f2e-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="e8f2e-163">Archivo de TodoItemManager.cs de hello abierto de hello **Portable** del proyecto, a continuación, agregue un **catch** para hello base **excepción** toohello de clase **try... catch** bloquear **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="e8f2e-164">Esto **catch** bloque escribe consola de toohello de mensaje de excepción de hello, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="e8f2e-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="e8f2e-165">Compile y ejecute la aplicación de cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-165">Build and run hello client app.</span></span>  <span data-ttu-id="e8f2e-166">Agregue nuevos elementos.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-166">Add some new items.</span></span> <span data-ttu-id="e8f2e-167">Tenga en cuenta que una excepción se registra en la consola de Hola para cada toosync intento con hello back-end.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="e8f2e-168">Estos nuevos elementos de solo existen en el almacén local de Hola hasta que estos se pueden insertar back-end de toohello móvil.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="e8f2e-169">aplicación de cliente de Hello se comporta como si estuviera conectado toohello back-end admitir que todos crear, leer, actualizar, las operaciones de eliminación (CRUD).</span><span class="sxs-lookup"><span data-stu-id="e8f2e-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="e8f2e-170">Cierre la aplicación hello y reiníciela tooverify que elementos nuevos de Hola que creó están almacén local toohello persistente.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="e8f2e-171">(Opcional) Use Visual Studio tooview su toosee de tabla de base de datos de SQL Azure Hola datos en la base de datos de back-end de hello no han cambiado.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="e8f2e-172">En Visual Studio, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="e8f2e-173">Navegar por la base de datos de tooyour en **Azure**->**bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="e8f2e-174">Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="e8f2e-175">Ahora puede examinar la tabla de base de datos SQL tooyour y su contenido.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="e8f2e-176">Actualizar tooreconnect de aplicación de cliente de hello en el back-end móvil</span><span class="sxs-lookup"><span data-stu-id="e8f2e-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="e8f2e-177">En esta sección, vuelva a conectar hello toohello móviles backend de la aplicación, que simula la aplicación hello viniendo tooan de estado en línea.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="e8f2e-178">Al realizar gestos de actualización de hello, datos están móvil tooyour sincronizados back-end.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="e8f2e-179">Vuelva a abrir Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-179">Reopen Constants.cs.</span></span> <span data-ttu-id="e8f2e-180">Hola correcto `applicationURL` toopoint toohello corrija la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="e8f2e-181">Volver a generar y ejecutar la aplicación de cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="e8f2e-182">aplicación Hello intenta toosync con back-end de aplicación móvil de hello después de iniciar.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="e8f2e-183">Compruebe que ninguna excepción se registra en la consola de depuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="e8f2e-184">(Opcional) Hola vista actualiza datos mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler o [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="e8f2e-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="e8f2e-185">Se ha sincronizado aviso Hola datos entre la base de datos de back-end de Hola y el almacén local de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="e8f2e-186">Tenga en cuenta datos Hola se ha sincronizado entre la base de datos de Hola y el almacén local de Hola y contiene elementos de hello que agregó mientras la aplicación se desconectó.</span><span class="sxs-lookup"><span data-stu-id="e8f2e-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8f2e-187">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e8f2e-187">Additional Resources</span></span>
* <span data-ttu-id="e8f2e-188">[Sincronización de datos sin conexión en Azure Mobile Apps][2]</span><span class="sxs-lookup"><span data-stu-id="e8f2e-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="e8f2e-189">[Procedimiento del SDK de .NET de Azure Mobile Apps][8]</span><span class="sxs-lookup"><span data-stu-id="e8f2e-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
