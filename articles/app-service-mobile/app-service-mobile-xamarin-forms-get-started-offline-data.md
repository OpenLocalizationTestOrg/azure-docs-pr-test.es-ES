---
title: "Habilitación de la sincronización sin conexión para una aplicación móvil de Azure (Xamarin.Forms) | Microsoft Docs"
description: "Obtenga información acerca de cómo usar la aplicación móvil del Servicio de aplicaciones para almacenar en caché y sincronizar datos sin conexión en su aplicación Xamarin.Forms."
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
ms.openlocfilehash: f2bed0a7124517319cc82405c4ab6b4d79aacfe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="7ae0e-103">Habilitación de la sincronización sin conexión para la aplicación móvil Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="7ae0e-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="7ae0e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="7ae0e-104">Overview</span></span>
<span data-ttu-id="7ae0e-105">Este tutorial presenta la característica de sincronización sin conexión de Aplicaciones móviles de Azure para Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="7ae0e-106">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil (ver, agregar o modificar datos), incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="7ae0e-107">Los cambios se almacenan en una base de datos local.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-107">Changes are stored in a local database.</span></span> <span data-ttu-id="7ae0e-108">Una vez que el dispositivo se vuelve a conectar, estos cambios se sincronizan con el servicio remoto.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="7ae0e-109">Este tutorial se basa en la solución de inicio rápido de Xamarin.Forms para Mobile Apps que crea al completar el tutorial [Crear una aplicación Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="7ae0e-109">This tutorial is based on the Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="7ae0e-110">La solución de inicio rápido para Xamarin.Forms contiene el código para admitir la sincronización sin conexión, que solo debe habilitarse.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-110">The quickstart solution for Xamarin.Forms contains the code to support offline sync, which just needs to be enabled.</span></span> <span data-ttu-id="7ae0e-111">En este tutorial, actualizará la solución de inicio rápido para activar las características sin conexión de Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-111">In this tutorial, you update the quickstart solution to turn on the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="7ae0e-112">También nos centraremos en el código sin conexión específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-112">We also highlight the offline-specific code in the app.</span></span> <span data-ttu-id="7ae0e-113">Si no usa la solución de inicio rápido descargada, debe agregar paquetes de extensión de acceso de datos al proyecto.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-113">If you do not use the downloaded quickstart solution, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="7ae0e-114">Para obtener más información acerca de los paquetes de extensión de servidor, consulte el artículo sobre cómo [trabajar con el SDK del servidor back-end de .NET para Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="7ae0e-114">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="7ae0e-115">Para más información sobre la característica de sincronización sin conexión, consulte el tema [Sincronización de datos sin conexión en Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="7ae0e-115">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-the-quickstart-solution"></a><span data-ttu-id="7ae0e-116">Habilitación de la funcionalidad de sincronización sin conexión en la solución de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="7ae0e-116">Enable offline sync functionality in the quickstart solution</span></span>
<span data-ttu-id="7ae0e-117">Se incluye el código de sincronización sin conexión en el proyecto mediante el uso de directivas de preprocesador de C#.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-117">The offline sync code is included in the project by using C# preprocessor directives.</span></span> <span data-ttu-id="7ae0e-118">Cuando se define el símbolo **OFFLINE\_SYNC\_ENABLED**, se incluyen en la compilación estas rutas de acceso del código.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-118">When the **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in the build.</span></span> <span data-ttu-id="7ae0e-119">Para las aplicaciones de Windows, también debe instalar la plataforma de SQLite.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-119">For Windows apps, you must also install the SQLite platform.</span></span>

1. <span data-ttu-id="7ae0e-120">En Visual Studio, haga clic con el botón derecho en la solución > **Administrar paquetes NuGet para la solución...** y, después, busque e instale el paquete NuGet **Microsoft.Azure.Mobile.Client.SQLiteStore** en todos los proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-120">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="7ae0e-121">En el Explorador de soluciones, abra el archivo TodoItemManager.cs desde el proyecto con **Portable** en el nombre, que es el proyecto de biblioteca de clases portable, y, después, quite la directiva de preprocesador siguiente:</span><span class="sxs-lookup"><span data-stu-id="7ae0e-121">In the Solution Explorer, open the TodoItemManager.cs file from the project with **Portable** in the name, which is Portable Class Library project, then uncomment the following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="7ae0e-122">(Opcional) Para admitir dispositivos de Windows, instale uno de los siguientes paquetes en el sistema de tiempo de ejecución de SQLite:</span><span class="sxs-lookup"><span data-stu-id="7ae0e-122">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="7ae0e-123">**Runtime de Windows 8.1:** instale [SQLite para Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="7ae0e-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="7ae0e-124">**Windows Phone 8.1:** instale [SQLite para Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="7ae0e-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="7ae0e-125">**Plataforma universal de Windows**: instale [SQLite para la plataforma universal de Windows][5].</span><span class="sxs-lookup"><span data-stu-id="7ae0e-125">**Universal Windows Platform** Install [SQLite for the Universal Windows Universal][5].</span></span>

     <span data-ttu-id="7ae0e-126">Aunque el tutorial rápido no contiene un proyecto de Windows universal, la plataforma de Windows universal es compatible con Xamarin Forms.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-126">Although the quickstart does not contain a Universal Windows project, the Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="7ae0e-127">(Opcional) En cada proyecto de aplicación de Windows, haga clic con el botón derecho en **Referencias** > **Agregar referencia...**, amplíe la carpeta **Windows** > **Extensiones**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="7ae0e-128">Habilite el SDK de **SQLite para Windows** junto con el SDK **Visual C++ 2013 Runtime para Windows**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-128">Enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="7ae0e-129">Los nombres de SDK de SQLite varían ligeramente con cada plataforma de Windows.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-129">The SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="7ae0e-130">Revisión del código de sincronización de cliente</span><span class="sxs-lookup"><span data-stu-id="7ae0e-130">Review the client sync code</span></span>
<span data-ttu-id="7ae0e-131">Esta es una breve descripción de lo que ya está incluido en el código del tutorial dentro de las directivas `#if OFFLINE_SYNC_ENABLED` .</span><span class="sxs-lookup"><span data-stu-id="7ae0e-131">Here is a brief overview of what is already included in the tutorial code inside the `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="7ae0e-132">La funcionalidad de sincronización sin conexión está en el archivo de proyecto TodoItemManager.cs en el proyecto de biblioteca de clases portable.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-132">The offline sync functionality is in the TodoItemManager.cs project file in the Portable Class Library project.</span></span> <span data-ttu-id="7ae0e-133">Para obtener información general conceptual de la característica, consulte [Sincronización de datos sin conexión en Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="7ae0e-133">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="7ae0e-134">Antes de poder realizar cualquier operación de tabla, se debe inicializar el almacén local.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-134">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="7ae0e-135">La base de datos del almacén local se inicializa en el constructor de clase **TodoItemManager** con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="7ae0e-135">The local store database is initialized in the **TodoItemManager** class constructor by using the following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes the SyncContext using the default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="7ae0e-136">Este código crea una nueva SQLite local con la clase **MobileServiceSQLiteStore**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-136">This code creates a new local SQLite database using the **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="7ae0e-137">El método **DefineTable** crea una tabla en el almacén local que coincide con los campos del tipo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-137">The **DefineTable** method creates a table in the local store that matches the fields in the provided type.</span></span>  <span data-ttu-id="7ae0e-138">El tipo no tiene que incluir todas las columnas que se encuentran en la base de datos remota.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-138">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="7ae0e-139">Es posible almacenar solo un subconjunto de columnas.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-139">It is possible to store a subset of columns.</span></span>
* <span data-ttu-id="7ae0e-140">El campo **todoTable** de **TodoItemManager** es un tipo **IMobileServiceSyncTable** en lugar de **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-140">The **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="7ae0e-141">Esta clase usa la base de datos local para todas las operaciones de creación, lectura, actualización y eliminación (CRUD) de tablas.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-141">This class uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="7ae0e-142">Para decidir cuándo se deben integrar esos cambios en el back-end de aplicación móvil, llame a **PushAsync** en el método **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-142">You decide when those changes are pushed to the Mobile App backend by calling **PushAsync** on the **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="7ae0e-143">El contexto de sincronización ayuda a mantener las relaciones entre tablas mediante el seguimiento y la inserción de los cambios en todas las tablas modificadas por una aplicación cliente cuando se llama a **PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-143">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="7ae0e-144">El siguiente método **SyncAsync** se llama para realizar la sincronización con el back-end de aplicación móvil:</span><span class="sxs-lookup"><span data-stu-id="7ae0e-144">The following **SyncAsync** method is called to sync with the Mobile App backend:</span></span>

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
                        //Update failed, reverting to server's copy.
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

    <span data-ttu-id="7ae0e-145">Este ejemplo utiliza un control de errores sencillo con el controlador de sincronización predeterminado.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-145">This sample uses simple error handling with the default sync handler.</span></span> <span data-ttu-id="7ae0e-146">Una aplicación real controlaría los diversos errores como condiciones de red y conflictos de red mediante el uso de una implementación personalizada de **IMobileServiceSyncHandler** .</span><span class="sxs-lookup"><span data-stu-id="7ae0e-146">A real application would handle the various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="7ae0e-147">Consideraciones sobre la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="7ae0e-147">Offline sync considerations</span></span>
<span data-ttu-id="7ae0e-148">En el ejemplo, solo se llama al método **SyncAsync** al inicio y cuando se solicita una sincronización.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-148">In the sample, the **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="7ae0e-149">Para iniciar la sincronización en una aplicación Android o iOS, despliegue la lista de elementos; para Windows, utilice el botón **Sincronizar** .</span><span class="sxs-lookup"><span data-stu-id="7ae0e-149">To initiate a sync in an Android or iOS app, pull down on the items list; for Windows, use the **Sync** button.</span></span> <span data-ttu-id="7ae0e-150">En una aplicación real, también puede hacer que la sincronización se desencadene cuando cambia el estado de la red.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-150">In a real-world application, you could also make the sync trigger when the network state changes.</span></span>

<span data-ttu-id="7ae0e-151">Si se ejecuta una extracción en una tabla que tiene actualizaciones locales pendientes seguidas por el contexto, la operación de extracción desencadenará de forma automática una inserción de contexto anterior.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-151">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="7ae0e-152">Al actualizar, agregar y completar elementos en este ejemplo, se puede omitir la llamada explícita a **PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-152">When refreshing, adding, and completing items in this sample, you can omit the explicit **PushAsync** call.</span></span>

<span data-ttu-id="7ae0e-153">En el ejemplo proporcionado, se consultan todos los registros de la tabla TodoItem remota, pero también es posible filtrar registros pasando un identificador de consulta y una consulta a **PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-153">In the provided code, all records in the remote TodoItem table are queried, but it is also possible to filter records by passing a query id and query to **PushAsync**.</span></span> <span data-ttu-id="7ae0e-154">Para más información, consulte la sección *Sincronización incremental* en [Sincronización de datos sin conexión en Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="7ae0e-154">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="7ae0e-155">Ejecución de la aplicación cliente</span><span class="sxs-lookup"><span data-stu-id="7ae0e-155">Run the client app</span></span>
<span data-ttu-id="7ae0e-156">Con la sincronización sin conexión habilitada, ejecute la aplicación cliente al menos una vez en cada plataforma para rellenar la base de datos del almacén local.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-156">With offline sync now enabled, run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="7ae0e-157">Después, simulará un escenario sin conexión y modificará los datos del almacén local mientras la aplicación está sin conexión.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-157">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="update-the-sync-behavior-of-the-client-app"></a><span data-ttu-id="7ae0e-158">Actualización del comportamiento de sincronización de la aplicación cliente</span><span class="sxs-lookup"><span data-stu-id="7ae0e-158">Update the sync behavior of the client app</span></span>
<span data-ttu-id="7ae0e-159">En esta sección, modificará el proyecto de cliente para simular un escenario sin conexión usando una dirección URL de aplicación no válida para el back-end.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-159">In this section, modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="7ae0e-160">Como alternativa, puede desactivar las conexiones de red cambiando el dispositivo a "Modo de avión".</span><span class="sxs-lookup"><span data-stu-id="7ae0e-160">Alternatively, you can turn off network connections by moving your device to "Airplane mode."</span></span>  <span data-ttu-id="7ae0e-161">Al agregar o cambiar elementos de datos, estos cambios se conservan en el almacén local, pero no se sincronizan con el almacén de datos de back-end hasta que se restablezca la conexión.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-161">When you add or change data items, these changes are held in the local store, but not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="7ae0e-162">En el Explorador de soluciones, abra el archivo de proyecto Constants.cs desde el proyecto **Portable** y cambie el valor de `ApplicationURL` para que apunte a una dirección URL no válida:</span><span class="sxs-lookup"><span data-stu-id="7ae0e-162">In the Solution Explorer, open the Constants.cs project file from the **Portable** project and change the value of `ApplicationURL` to point to an invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="7ae0e-163">Abra el archivo TodoItemManager.cs desde el proyecto **Portable**, agregue después un valor **catch** adicional para la clase **Exception** de base al bloque **try...catch** de **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-163">Open the TodoItemManager.cs file from the **Portable** project, then add a **catch** for the base **Exception** class to the **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="7ae0e-164">Este bloque **catch** escribe el mensaje de excepción en la consola, de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="7ae0e-164">This **catch** block writes the exception message to the console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="7ae0e-165">Compile y ejecute la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-165">Build and run the client app.</span></span>  <span data-ttu-id="7ae0e-166">Agregue nuevos elementos.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-166">Add some new items.</span></span> <span data-ttu-id="7ae0e-167">Tenga en cuenta que la excepción se registra en la consola para cada intento de sincronización con el back-end.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-167">Notice that an exception is logged in the console for each attempt to sync with the backend.</span></span> <span data-ttu-id="7ae0e-168">Estos nuevos elementos solo existirán en el almacén local hasta que se puedan insertar en el back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-168">These new items exist only in the local store until they can be pushed to the mobile backend.</span></span> <span data-ttu-id="7ae0e-169">La aplicación cliente se comporta como si estuviera conectada al back-end y admite todas las operaciones de creación, lectura, actualización y eliminación (CRUD).</span><span class="sxs-lookup"><span data-stu-id="7ae0e-169">The client app behaves as if it is connected to the backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="7ae0e-170">Cierre la aplicación y reiníciela para comprobar que los nuevos elementos que creó se mantienen en el almacén local.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-170">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="7ae0e-171">(Opcional) Use Visual Studio para ver la tabla de base de datos SQL de Azure y observar que los datos de la base de datos de back-end no han cambiado.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-171">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="7ae0e-172">En Visual Studio, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="7ae0e-173">Vaya a la base de datos en **Azure**->**SQL Databases**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-173">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="7ae0e-174">Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="7ae0e-175">Ahora puede buscar la tabla de base de datos SQL y su contenido.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-175">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="update-the-client-app-to-reconnect-your-mobile-backend"></a><span data-ttu-id="7ae0e-176">Actualización de la aplicación cliente para volver a conectar el back-end móvil</span><span class="sxs-lookup"><span data-stu-id="7ae0e-176">Update the client app to reconnect your mobile backend</span></span>
<span data-ttu-id="7ae0e-177">En esta sección se volverá a conectar la aplicación al back-end móvil, que simula que la aplicación vuelve a un estado en línea.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-177">In this section, reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="7ae0e-178">Al realizar el gesto de la actualización, los datos se sincronizarán con el back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-178">When you perform the refresh gesture, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="7ae0e-179">Vuelva a abrir Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-179">Reopen Constants.cs.</span></span> <span data-ttu-id="7ae0e-180">Corrija `applicationURL` para que apunte a la dirección URL correcta.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-180">Correct the `applicationURL` to point to the correct URL.</span></span>
2. <span data-ttu-id="7ae0e-181">Vuelva a compilar la aplicación cliente y ejecútela.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-181">Rebuild and run the client app.</span></span> <span data-ttu-id="7ae0e-182">La aplicación intenta sincronizarse con el back-end de aplicación móvil después de iniciarse.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-182">The app attempts to sync with the mobile app backend after launching.</span></span> <span data-ttu-id="7ae0e-183">Compruebe que no hay excepciones registradas en la consola de depuración.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-183">Verify that no exceptions are logged in the debug console.</span></span>
3. <span data-ttu-id="7ae0e-184">(Opcional) Vea los datos actualizados mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler o [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="7ae0e-184">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="7ae0e-185">Observe que los datos se han sincronizado entre la base de datos back-end y el almacén local.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-185">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="7ae0e-186">Observe que los datos se han sincronizado entre la base de datos y el almacén local, y contienen los elementos que agregó mientras la aplicación estaba desconectada.</span><span class="sxs-lookup"><span data-stu-id="7ae0e-186">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ae0e-187">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7ae0e-187">Additional Resources</span></span>
* <span data-ttu-id="7ae0e-188">[Sincronización de datos sin conexión en Azure Mobile Apps][2]</span><span class="sxs-lookup"><span data-stu-id="7ae0e-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="7ae0e-189">[Procedimiento del SDK de .NET de Azure Mobile Apps][8]</span><span class="sxs-lookup"><span data-stu-id="7ae0e-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
