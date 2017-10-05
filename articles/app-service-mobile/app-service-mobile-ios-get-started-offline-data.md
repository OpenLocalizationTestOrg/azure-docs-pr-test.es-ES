---
title: "Habilitación de la sincronización sin conexión con aplicaciones móviles iOS | Microsoft Docs"
description: "Aprenda a usar App Service Mobile Apps para almacenar en caché y sincronizar datos sin conexión en aplicaciones iOS."
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 44c0d26b2d7d28322d436d4bda319d728c31a635
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="5e4cf-103">Habilitación de la sincronización sin conexión con aplicaciones móviles iOS</span><span class="sxs-lookup"><span data-stu-id="5e4cf-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="5e4cf-104">Información general</span><span class="sxs-lookup"><span data-stu-id="5e4cf-104">Overview</span></span>
<span data-ttu-id="5e4cf-105">En este tutorial, se trata la sincronización sin conexión con la característica Mobile Apps de Azure App Service para iOS.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-105">This tutorial covers offline syncing with the Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="5e4cf-106">Con la sincronización sin conexión, los usuarios finales pueden interactuar con una aplicación móvil para ver, agregar o modificar datos, incluso si carecen de conexión a red.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-106">With offline syncing end-users can interact with a mobile app to view, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="5e4cf-107">Los cambios se almacenan en una base de datos local.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-107">Changes are stored in a local database.</span></span> <span data-ttu-id="5e4cf-108">Una vez que el dispositivo se vuelve a conectar, los cambios se sincronizan con el back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-108">After the device is back online, the changes are synced with the remote back end.</span></span>

<span data-ttu-id="5e4cf-109">Si esta es la primera vez que usa Mobile Apps, primero debería completar el tutorial [Creación de una aplicación iOS].</span><span class="sxs-lookup"><span data-stu-id="5e4cf-109">If this is your first experience with Mobile Apps, you should first complete the tutorial [Create an iOS App].</span></span> <span data-ttu-id="5e4cf-110">Si no usa el proyecto de servidor de inicio rápido descargado, debe agregar los paquetes de extensión de acceso de datos al proyecto.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-110">If you do not use the downloaded quick-start server project, you must add the data-access extension packages to your project.</span></span> <span data-ttu-id="5e4cf-111">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [Trabajar con el SDK del servidor back-end de .NET para Aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5e4cf-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="5e4cf-112">Para aprender acerca de la característica de sincronización sin conexión, consulte [Sincronización de datos sin conexión en Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="5e4cf-112">To learn more about the offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="5e4cf-113"><a name="review-sync"></a>Revisión del código de sincronización de cliente</span><span class="sxs-lookup"><span data-stu-id="5e4cf-113"><a name="review-sync"></a>Review the client sync code</span></span>
<span data-ttu-id="5e4cf-114">El proyecto de cliente que descargó para el tutorial [Creación de una aplicación iOS] ya contiene el código que admite la sincronización sin conexión con una base de datos local basada en Core Data.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-114">The client project that you downloaded for the [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="5e4cf-115">En esta sección, se resume lo que ya está incluido en el código del tutorial.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-115">This section summarizes what is already included in the tutorial code.</span></span> <span data-ttu-id="5e4cf-116">Para ver información general conceptual sobre la característica, consulte [Sincronización de datos sin conexión en Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="5e4cf-116">For a conceptual overview of the feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="5e4cf-117">Mediante la característica de sincronización de datos sin conexión de Mobile Apps, los usuarios finales pueden interactuar con una base de datos local incluso si la red no está accesible.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-117">Using the offline data-sync feature of Mobile Apps, end-users can interact with a local database even when the network is inaccessible.</span></span> <span data-ttu-id="5e4cf-118">Para utilizar estas características en su aplicación, inicialice el contexto de sincronización de `MSClient` y haga referencia a un almacén local.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-118">To use these features in your app, you initialize the sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="5e4cf-119">Después, haga referencia a la tabla mediante la interfaz **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-119">Then you reference your table through the **MSSyncTable** interface.</span></span>

<span data-ttu-id="5e4cf-120">En **QSTodoService.m** (Objective-C) o **ToDoTableViewController.swift** (Swift), tenga en cuenta que el tipo del miembro **syncTable** es **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that the type of the member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="5e4cf-121">La sincronización sin conexión usa esta interfaz de tabla de sincronización en lugar de **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="5e4cf-122">Cuando se usa una tabla de sincronización, todas las operaciones van al almacén local y solo se sincronizan con el back-end remoto con operaciones de inserción y extracción explícitas.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-122">When a sync table is used, all operations go to the local store and are synchronized only with the remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="5e4cf-123">Para obtener una referencia a una tabla de sincronización, utilice el método **syncTableWithName** en `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-123">To get a reference to a sync table, use the **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="5e4cf-124">Para quitar la funcionalidad de sincronización sin conexión, use **tableWithName** en su lugar.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-124">To remove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="5e4cf-125">Antes de poder realizar cualquier operación de tabla, se debe inicializar el almacén local.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-125">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="5e4cf-126">Este es el código pertinente:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-126">Here is the relevant code:</span></span>

* <span data-ttu-id="5e4cf-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-127">**Objective-C**.</span></span> <span data-ttu-id="5e4cf-128">En el método **QSTodoService.init**:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-128">In the **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="5e4cf-129">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-129">**Swift**.</span></span> <span data-ttu-id="5e4cf-130">En el método **ToDoTableViewController.viewDidLoad**:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-130">In the **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of the Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="5e4cf-131">Este método crea un almacén local mediante la interfaz `MSCoreDataStore`, que se proporciona en el SDK de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-131">This method creates a local store by using the `MSCoreDataStore` interface, which the Mobile Apps SDK provides.</span></span> <span data-ttu-id="5e4cf-132">Como alternativa, puede proporcionar otro almacén local mediante la implementación del protocolo `MSSyncContextDataSource`.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-132">Alternatively, you can provide a different local store by implementing the `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="5e4cf-133">Además, el primer parámetro de **MSSyncContext** se utiliza para especificar un controlador de conflictos.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-133">Also, the first parameter of **MSSyncContext** is used to specify a conflict handler.</span></span> <span data-ttu-id="5e4cf-134">Puesto que se ha pasado `nil`, se obtiene el controlador de conflictos predeterminado, que produce un error para cualquier conflicto.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-134">Because we have passed `nil`, we get the default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="5e4cf-135">Ahora, se va a realizar la operación de sincronización en sí y se van a obtener datos desde el back-end remoto:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-135">Now, let's perform the actual sync operation, and get data from the remote back end:</span></span>

* <span data-ttu-id="5e4cf-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-136">**Objective-C**.</span></span> <span data-ttu-id="5e4cf-137">`syncData` primero inserta nuevos cambios y luego llama a **pullData** para obtener datos desde el back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-137">`syncData` first pushes new changes and then calls **pullData** to get data from the remote back end.</span></span> <span data-ttu-id="5e4cf-138">A su vez, el método **pullData** obtiene datos nuevos que coinciden con una consulta:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-138">In turn, the **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in the sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from the remote server into the local table.
       // We're pulling all items and filtering in the view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets the caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="5e4cf-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via the MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep the server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation to item \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting to server's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="5e4cf-140">En la versión Objective-C, en `syncData`, se llama primero a **pushWithCompletion** en el contexto de sincronización.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-140">In the Objective-C version, in `syncData`, we first call **pushWithCompletion** on the sync context.</span></span> <span data-ttu-id="5e4cf-141">Este método es miembro de `MSSyncContext` (no de la propia tabla de sincronización), porque inserta cambios en todas las tablas.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-141">This method is a member of `MSSyncContext` (and not the sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="5e4cf-142">Solo se envían al servidor los registros que se han modificado localmente de alguna forma (mediante operaciones CUD).</span><span class="sxs-lookup"><span data-stu-id="5e4cf-142">Only records that have been modified in some way locally (through CUD operations) are sent to the server.</span></span> <span data-ttu-id="5e4cf-143">A continuación, se llama a la aplicación auxiliar **pullData**, que llama a **MSSyncTable.pullWithQuery** para recuperar datos remotos y almacenarlos en la base de datos local.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-143">Then the helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** to retrieve remote data and store it in the local database.</span></span>

<span data-ttu-id="5e4cf-144">En la versión Swift, como la operación de inserción no era estrictamente necesaria, no hay ninguna llamada a **pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-144">In the Swift version, because the push operation was not strictly necessary, there is no call to **pushWithCompletion**.</span></span> <span data-ttu-id="5e4cf-145">Si hay cambios pendientes en el contexto de sincronización para la tabla que está realizando una operación de inserción, la extracción siempre realiza primero una inserción.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-145">If there are any changes pending in the sync context for the table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="5e4cf-146">Sin embargo, si tiene más de una tabla de sincronización, es mejor llamar explícitamente a la inserción para asegurarse de que todo sea coherente en las tablas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-146">However, if you have more than one sync table, it is best to explicitly call push to ensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="5e4cf-147">Tanto en la versión Objective-C como en la Swift, puede usar el método **pullWithQuery** para especificar una consulta para filtrar los registros que desea recuperar.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-147">In both the Objective-C and Swift versions, you can use the **pullWithQuery** method to specify a query to filter the records you want to retrieve.</span></span> <span data-ttu-id="5e4cf-148">En este ejemplo, la consulta recupera todos los registros en la tabla `TodoItem` remota.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-148">In this example, the query retrieves all records in the remote `TodoItem` table.</span></span>

<span data-ttu-id="5e4cf-149">El segundo parámetro de **pullWithQuery** es un identificador de consulta que se utiliza para la *sincronización incremental*.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-149">The second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*.</span></span> <span data-ttu-id="5e4cf-150">La sincronización incremental recupera solo los registros que se modificaron desde la última sincronización, haciendo uso de la marca de tiempo `UpdatedAt` del registro (llamada `updatedAt` en el almacén local). El identificador de la consulta debe ser una cadena descriptiva que sea única para cada consulta lógica en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-150">Incremental sync retrieves only records that were modified since the last sync, using the record's `UpdatedAt` time stamp (called `updatedAt` in the local store.) The query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="5e4cf-151">Para desactivar la sincronización incremental, pase `nil` como identificador de la consulta.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-151">To opt out of incremental sync, pass `nil` as the query ID.</span></span> <span data-ttu-id="5e4cf-152">Es posible que este enfoque resulte ineficaz, ya que recupera todos los registros en cada operación de extracción.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-152">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="5e4cf-153">La aplicación Objective-C se sincroniza cuando se modifican o agregan datos, cuando un usuario realiza el gesto de actualización y en el inicio.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-153">The Objective-C app syncs when you modify or add data, when a user performs the refresh gesture, and on launch.</span></span>

<span data-ttu-id="5e4cf-154">La aplicación Swift se sincroniza cuando el usuario realiza el gesto de actualización y en el inicio.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-154">The Swift app syncs when the user performs the refresh gesture and on launch.</span></span>

<span data-ttu-id="5e4cf-155">Dado que la aplicación se sincroniza cada vez que se modifican datos (Objective-C) o siempre que se inicia la aplicación (Objective-C y Swift), la aplicación supone que el usuario está en línea.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-155">Because the app syncs whenever data is modified (Objective-C) or whenever the app starts (Objective-C and Swift), the app assumes that the user is online.</span></span> <span data-ttu-id="5e4cf-156">En una sección posterior, actualizará la aplicación para que los usuarios puedan editar incluso cuando estén sin conexión.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-156">In a later section, you will update the app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="5e4cf-157"><a name="review-core-data"></a>Revisión del modelo Core Data</span><span class="sxs-lookup"><span data-stu-id="5e4cf-157"><a name="review-core-data"></a>Review the Core Data model</span></span>
<span data-ttu-id="5e4cf-158">Cuando use el almacén sin conexión Core Data, debe definir tablas y campos determinados en el modelo de datos.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-158">When you use the Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="5e4cf-159">La aplicación de ejemplo ya incluye un modelo de datos con el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-159">The sample app already includes a data model with the right format.</span></span> <span data-ttu-id="5e4cf-160">En esta sección se le guiará por estas tablas y el modo de utilizarlas.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-160">In this section, we walk through these tables to show how they are used.</span></span>

<span data-ttu-id="5e4cf-161">Abra **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-161">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="5e4cf-162">Hay cuatro tablas definidas: tres usadas por el SDK y una para las tareas pendientes en sí:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-162">Four tables are defined--three that are used by the SDK and one that's used for the to-do items themselves:</span></span>
  * <span data-ttu-id="5e4cf-163">MS_TableOperations: realiza el seguimiento de los elementos que deben sincronizarse con el servidor.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-163">MS_TableOperations: Tracks the items that need to be synchronized with the server.</span></span>
  * <span data-ttu-id="5e4cf-164">MS_TableOperationErrors: realiza el seguimiento de los errores que se producen durante la sincronización sin conexión.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-164">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="5e4cf-165">MS_TableConfig: realiza el seguimiento de la hora de la última actualización de la última operación de sincronización para todas las operaciones de extracción.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-165">MS_TableConfig: Tracks the last updated time for the last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="5e4cf-166">TodoItem: almacena las tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-166">TodoItem: Stores the to-do items.</span></span> <span data-ttu-id="5e4cf-167">Las columnas del sistema **createdAt**, **updatedAt** y **version** son propiedades del sistema opcionales.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-167">The system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="5e4cf-168">El SDK de Mobile Apps tiene reservados los nombres de columna que empiezan por "**``**".</span><span class="sxs-lookup"><span data-stu-id="5e4cf-168">The Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="5e4cf-169">Utilice este prefijo exclusivamente para las columnas del sistema.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-169">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="5e4cf-170">De lo contrario, se modifican los nombres de las columnas cuando se usa el back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-170">Otherwise, your column names are modified when you use the remote back end.</span></span>
>
>

<span data-ttu-id="5e4cf-171">Cuando use la característica de sincronización sin conexión, defina las tres tablas del sistema y la tabla de datos.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-171">When you use the offline sync feature, define the three system tables and the data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="5e4cf-172">Tablas del sistema</span><span class="sxs-lookup"><span data-stu-id="5e4cf-172">System tables</span></span>

<span data-ttu-id="5e4cf-173">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="5e4cf-173">**MS_TableOperations**</span></span>  

![Atributos de la tabla MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="5e4cf-175">Atributo</span><span class="sxs-lookup"><span data-stu-id="5e4cf-175">Attribute</span></span> | <span data-ttu-id="5e4cf-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="5e4cf-176">Type</span></span> |
| --- | --- |
| <span data-ttu-id="5e4cf-177">id</span><span class="sxs-lookup"><span data-stu-id="5e4cf-177">id</span></span> | <span data-ttu-id="5e4cf-178">Integer 64</span><span class="sxs-lookup"><span data-stu-id="5e4cf-178">Integer 64</span></span> |
| <span data-ttu-id="5e4cf-179">itemId</span><span class="sxs-lookup"><span data-stu-id="5e4cf-179">itemId</span></span> | <span data-ttu-id="5e4cf-180">Cadena</span><span class="sxs-lookup"><span data-stu-id="5e4cf-180">String</span></span> |
| <span data-ttu-id="5e4cf-181">propiedades</span><span class="sxs-lookup"><span data-stu-id="5e4cf-181">properties</span></span> | <span data-ttu-id="5e4cf-182">Binary Data</span><span class="sxs-lookup"><span data-stu-id="5e4cf-182">Binary Data</span></span> |
| <span data-ttu-id="5e4cf-183">table</span><span class="sxs-lookup"><span data-stu-id="5e4cf-183">table</span></span> | <span data-ttu-id="5e4cf-184">Cadena</span><span class="sxs-lookup"><span data-stu-id="5e4cf-184">String</span></span> |
| <span data-ttu-id="5e4cf-185">tableKind</span><span class="sxs-lookup"><span data-stu-id="5e4cf-185">tableKind</span></span> | <span data-ttu-id="5e4cf-186">Integer 16</span><span class="sxs-lookup"><span data-stu-id="5e4cf-186">Integer 16</span></span> |


<span data-ttu-id="5e4cf-187">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="5e4cf-187">**MS_TableOperationErrors**</span></span>

 ![Atributos de la tabla MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="5e4cf-189">Atributo</span><span class="sxs-lookup"><span data-stu-id="5e4cf-189">Attribute</span></span> | <span data-ttu-id="5e4cf-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="5e4cf-190">Type</span></span> |
| --- | --- |
| <span data-ttu-id="5e4cf-191">id</span><span class="sxs-lookup"><span data-stu-id="5e4cf-191">id</span></span> |<span data-ttu-id="5e4cf-192">String</span><span class="sxs-lookup"><span data-stu-id="5e4cf-192">String</span></span> |
| <span data-ttu-id="5e4cf-193">operationId</span><span class="sxs-lookup"><span data-stu-id="5e4cf-193">operationId</span></span> |<span data-ttu-id="5e4cf-194">Integer 64</span><span class="sxs-lookup"><span data-stu-id="5e4cf-194">Integer 64</span></span> |
| <span data-ttu-id="5e4cf-195">propiedades</span><span class="sxs-lookup"><span data-stu-id="5e4cf-195">properties</span></span> |<span data-ttu-id="5e4cf-196">Binary Data</span><span class="sxs-lookup"><span data-stu-id="5e4cf-196">Binary Data</span></span> |
| <span data-ttu-id="5e4cf-197">tableKind</span><span class="sxs-lookup"><span data-stu-id="5e4cf-197">tableKind</span></span> |<span data-ttu-id="5e4cf-198">Integer 16</span><span class="sxs-lookup"><span data-stu-id="5e4cf-198">Integer 16</span></span> |

 <span data-ttu-id="5e4cf-199">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="5e4cf-199">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="5e4cf-200">Atributo</span><span class="sxs-lookup"><span data-stu-id="5e4cf-200">Attribute</span></span> | <span data-ttu-id="5e4cf-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="5e4cf-201">Type</span></span> |
| --- | --- |
| <span data-ttu-id="5e4cf-202">id</span><span class="sxs-lookup"><span data-stu-id="5e4cf-202">id</span></span> |<span data-ttu-id="5e4cf-203">String</span><span class="sxs-lookup"><span data-stu-id="5e4cf-203">String</span></span> |
| <span data-ttu-id="5e4cf-204">key</span><span class="sxs-lookup"><span data-stu-id="5e4cf-204">key</span></span> |<span data-ttu-id="5e4cf-205">Cadena</span><span class="sxs-lookup"><span data-stu-id="5e4cf-205">String</span></span> |
| <span data-ttu-id="5e4cf-206">keyType</span><span class="sxs-lookup"><span data-stu-id="5e4cf-206">keyType</span></span> |<span data-ttu-id="5e4cf-207">Integer 64</span><span class="sxs-lookup"><span data-stu-id="5e4cf-207">Integer 64</span></span> |
| <span data-ttu-id="5e4cf-208">table</span><span class="sxs-lookup"><span data-stu-id="5e4cf-208">table</span></span> |<span data-ttu-id="5e4cf-209">Cadena</span><span class="sxs-lookup"><span data-stu-id="5e4cf-209">String</span></span> |
| <span data-ttu-id="5e4cf-210">value</span><span class="sxs-lookup"><span data-stu-id="5e4cf-210">value</span></span> |<span data-ttu-id="5e4cf-211">String</span><span class="sxs-lookup"><span data-stu-id="5e4cf-211">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="5e4cf-212">Tabla de datos</span><span class="sxs-lookup"><span data-stu-id="5e4cf-212">Data table</span></span>

<span data-ttu-id="5e4cf-213">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="5e4cf-213">**TodoItem**</span></span>

| <span data-ttu-id="5e4cf-214">Atributo</span><span class="sxs-lookup"><span data-stu-id="5e4cf-214">Attribute</span></span> | <span data-ttu-id="5e4cf-215">Escriba</span><span class="sxs-lookup"><span data-stu-id="5e4cf-215">Type</span></span> | <span data-ttu-id="5e4cf-216">Nota:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-216">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e4cf-217">id</span><span class="sxs-lookup"><span data-stu-id="5e4cf-217">id</span></span> | <span data-ttu-id="5e4cf-218">Cadena, marcado obligatorio</span><span class="sxs-lookup"><span data-stu-id="5e4cf-218">String, marked required</span></span> |<span data-ttu-id="5e4cf-219">Clave principal en almacén remoto</span><span class="sxs-lookup"><span data-stu-id="5e4cf-219">Primary key in remote store</span></span> |
| <span data-ttu-id="5e4cf-220">complete</span><span class="sxs-lookup"><span data-stu-id="5e4cf-220">complete</span></span> | <span data-ttu-id="5e4cf-221">Booleano</span><span class="sxs-lookup"><span data-stu-id="5e4cf-221">Boolean</span></span> | <span data-ttu-id="5e4cf-222">Campo de tarea pendiente</span><span class="sxs-lookup"><span data-stu-id="5e4cf-222">To-do item field</span></span> |
| <span data-ttu-id="5e4cf-223">text</span><span class="sxs-lookup"><span data-stu-id="5e4cf-223">text</span></span> |<span data-ttu-id="5e4cf-224">string</span><span class="sxs-lookup"><span data-stu-id="5e4cf-224">String</span></span> |<span data-ttu-id="5e4cf-225">Campo de tarea pendiente</span><span class="sxs-lookup"><span data-stu-id="5e4cf-225">To-do item field</span></span> |
| <span data-ttu-id="5e4cf-226">createdAt</span><span class="sxs-lookup"><span data-stu-id="5e4cf-226">createdAt</span></span> | <span data-ttu-id="5e4cf-227">Date</span><span class="sxs-lookup"><span data-stu-id="5e4cf-227">Date</span></span> | <span data-ttu-id="5e4cf-228">(opcional) Se asigna a la propiedad del sistema **createdAt**</span><span class="sxs-lookup"><span data-stu-id="5e4cf-228">(optional) Maps to **createdAt** system property</span></span> |
| <span data-ttu-id="5e4cf-229">updatedAt</span><span class="sxs-lookup"><span data-stu-id="5e4cf-229">updatedAt</span></span> | <span data-ttu-id="5e4cf-230">Date</span><span class="sxs-lookup"><span data-stu-id="5e4cf-230">Date</span></span> | <span data-ttu-id="5e4cf-231">(opcional) Se asigna a la propiedad del sistema **updatedAt**</span><span class="sxs-lookup"><span data-stu-id="5e4cf-231">(optional) Maps to **updatedAt** system property</span></span> |
| <span data-ttu-id="5e4cf-232">versión</span><span class="sxs-lookup"><span data-stu-id="5e4cf-232">version</span></span> | <span data-ttu-id="5e4cf-233">String</span><span class="sxs-lookup"><span data-stu-id="5e4cf-233">String</span></span> | <span data-ttu-id="5e4cf-234">(opcional) Se usa para detectar conflictos; se asigna a version</span><span class="sxs-lookup"><span data-stu-id="5e4cf-234">(optional) Used to detect conflicts, maps to version</span></span> |

## <span data-ttu-id="5e4cf-235"><a name="setup-sync"></a>Cambio del comportamiento de sincronización de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5e4cf-235"><a name="setup-sync"></a>Change the sync behavior of the app</span></span>
<span data-ttu-id="5e4cf-236">En esta sección, modifique la aplicación para que no se sincronice al iniciarse la aplicación ni cuando se inserten y actualicen elementos.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-236">In this section, you modify the app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="5e4cf-237">Solo se sincroniza cuando se realiza el gesto de actualización.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-237">It syncs only when the refresh gesture button is performed.</span></span>

<span data-ttu-id="5e4cf-238">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-238">**Objective-C**:</span></span>

1. <span data-ttu-id="5e4cf-239">En **QSTodoListViewController.m**, cambie el método **viewDidLoad** para quitar la llamada a `[self refresh]` al final del método.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-239">In **QSTodoListViewController.m**, change the **viewDidLoad** method to remove the call to `[self refresh]` at the end of the method.</span></span> <span data-ttu-id="5e4cf-240">Ahora los datos no se han sincronizado con el servidor al iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-240">Now the data is not synced with the server on app start.</span></span> <span data-ttu-id="5e4cf-241">En su lugar, se sincronizan con el contenido del almacén local.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-241">Instead, it's synced with the contents of the local store.</span></span>
2. <span data-ttu-id="5e4cf-242">En **QSTodoService.m**, modifique la definición de `addItem` para que no se sincronice tras la inserción del elemento.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-242">In **QSTodoService.m**, modify the definition of `addItem` so that it doesn't sync after the item is inserted.</span></span> <span data-ttu-id="5e4cf-243">Quite el bloque `self syncData` y sustitúyalo por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-243">Remove the `self syncData` block and replace it with the following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="5e4cf-244">Modifique la definición de `completeItem` como se mencionó antes.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-244">Modify the definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="5e4cf-245">Quite el bloque para `self syncData` y sustitúyalo por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-245">Remove the block for `self syncData` and replace it with the following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="5e4cf-246">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-246">**Swift**:</span></span>

<span data-ttu-id="5e4cf-247">En `viewDidLoad`, en **ToDoTableViewController.swift**, convierta en comentario las dos líneas que se muestran aquí para detener la sincronización al iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-247">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out the two lines shown here, to stop syncing on app start.</span></span> <span data-ttu-id="5e4cf-248">En el momento de redactar este artículo, la aplicación Swift Todo no actualiza el servicio cuando alguien agrega o completa un elemento.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-248">At the time of this writing, the Swift Todo app does not update the service when someone adds or completes an item.</span></span> <span data-ttu-id="5e4cf-249">Solo lo actualiza en el inicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-249">It updates the service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="5e4cf-250"><a name="test-app"></a>Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5e4cf-250"><a name="test-app"></a>Test the app</span></span>
<span data-ttu-id="5e4cf-251">En esta sección, se conecta a una dirección URL no válida para simular un escenario sin conexión.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-251">In this section, you connect to an invalid URL to simulate an offline scenario.</span></span> <span data-ttu-id="5e4cf-252">Cuando agrega elementos de datos, se guardan en el almacén local Core Data, pero no se sincronizan con el back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-252">When you add data items, they're held in the local Core Data store, but they're not synced with the mobile-app back end.</span></span>

1. <span data-ttu-id="5e4cf-253">Cambie la dirección URL de la aplicación móvil en **QSTodoService.m** por una no válida y vuelva a ejecutar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-253">Change the mobile-app URL in **QSTodoService.m** to an invalid URL, and run the app again:</span></span>

   <span data-ttu-id="5e4cf-254">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-254">**Objective-C**.</span></span> <span data-ttu-id="5e4cf-255">En QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-255">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="5e4cf-256">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-256">**Swift**.</span></span> <span data-ttu-id="5e4cf-257">En ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-257">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="5e4cf-258">Agregue algunas tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-258">Add some to-do items.</span></span> <span data-ttu-id="5e4cf-259">Salga del simulador (o fuerce el cierre de la aplicación) y reinícielo.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-259">Quit the simulator (or forcibly close the app), and then restart it.</span></span> <span data-ttu-id="5e4cf-260">Compruebe que los cambios se conserven.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-260">Verify that your changes persist.</span></span>

3. <span data-ttu-id="5e4cf-261">Vea el contenido de la tabla **TodoItem** remota:</span><span class="sxs-lookup"><span data-stu-id="5e4cf-261">View the contents of the remote **TodoItem** table:</span></span>
   * <span data-ttu-id="5e4cf-262">En un back-end de Node.js, vaya a [Azure Portal](https://portal.azure.com/) y, en el back-end de su aplicación móvil, haga clic en **Tablas fáciles** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-262">For a Node.js back end, go to the [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="5e4cf-263">En un back-end de .NET, use una herramienta SQL, como SQL Server Management Studio, o un cliente REST, como Fiddler o Postman.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-263">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="5e4cf-264">Compruebe que los nuevos elementos *no* se hayan sincronizado con el servidor.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-264">Verify that the new items have *not* been synced with the server.</span></span>

5. <span data-ttu-id="5e4cf-265">Vuelva a cambiar la dirección URL por la correcta en **QSTodoService.m** y ejecute de nuevo la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-265">Change the URL back to the correct one in **QSTodoService.m**, and rerun the app.</span></span>

6. <span data-ttu-id="5e4cf-266">Realice el gesto de actualización desplegando la lista de elementos.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-266">Perform the refresh gesture by pulling down the list of items.</span></span>  
<span data-ttu-id="5e4cf-267">Se muestra un control giratorio de progreso.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-267">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="5e4cf-268">Vea los datos de **TodoItem** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-268">View the **TodoItem** data again.</span></span> <span data-ttu-id="5e4cf-269">Ahora deben aparecer las tareas nuevas y modificadas.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-269">The new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="5e4cf-270">Resumen</span><span class="sxs-lookup"><span data-stu-id="5e4cf-270">Summary</span></span>
<span data-ttu-id="5e4cf-271">Para admitir la característica de sincronización sin conexión, se usa la interfaz `MSSyncTable` y se inicializa `MSClient.syncContext` con un almacén local.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-271">To support the offline sync feature, we used the `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="5e4cf-272">En este caso, el almacén local era una base de datos Core Data.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-272">In this case, the local store was a Core Data-based database.</span></span>

<span data-ttu-id="5e4cf-273">Cuando usa un almacén local Core Data, debe definir varias tablas con las [propiedades del sistema correctas](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="5e4cf-273">When you use a Core Data local store, you must define several tables with the [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="5e4cf-274">Las operaciones normales de creación, lectura, actualización y eliminación (CRUD) para aplicaciones móviles funcionan como si la aplicación siguiera conectada, pero todas ellas se producen en el almacén local.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-274">The normal create, read, update, and delete (CRUD) operations for mobile apps work as if the app is still connected, but all the operations occur against the local store.</span></span>

<span data-ttu-id="5e4cf-275">Cuando el almacén local se sincroniza con el servidor, se usa el método **MSSyncTable.pullWithQuery**.</span><span class="sxs-lookup"><span data-stu-id="5e4cf-275">When we synchronized the local store with the server, we used the **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5e4cf-276">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5e4cf-276">Additional resources</span></span>
* <span data-ttu-id="5e4cf-277">[Sincronización de datos sin conexión en Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="5e4cf-277">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="5e4cf-278">[Cloud Cover: sincronización sin conexión en Azure Mobile Services] \(El vídeo trata sobre Mobile Services, pero la sincronización sin conexión de Mobile Apps funciona de forma similar.\)</span><span class="sxs-lookup"><span data-stu-id="5e4cf-278">[Cloud Cover: Offline Sync in Azure Mobile Services] \(The video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


<span data-ttu-id="5e4cf-279">[Creación de una aplicación iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="5e4cf-279">[Create an iOS App]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="5e4cf-280">[Sincronización de datos sin conexión en Mobile Apps]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="5e4cf-280">[Offline Data Sync in Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

<span data-ttu-id="5e4cf-281">[Cloud Cover: sincronización sin conexión en Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="5e4cf-281">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
