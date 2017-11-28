---
title: "sincronización sin conexión aaaEnable con aplicaciones móviles iOS | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse servicio de aplicaciones de Azure aplicaciones móviles toocache y sincronización de datos sin conexión en aplicaciones de iOS."
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
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="cd299-103">Habilitación de la sincronización sin conexión con aplicaciones móviles iOS</span><span class="sxs-lookup"><span data-stu-id="cd299-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="cd299-104">Información general</span><span class="sxs-lookup"><span data-stu-id="cd299-104">Overview</span></span>
<span data-ttu-id="cd299-105">Este tutorial trata la sincronización sin conexión con la característica de aplicaciones móviles Hola de servicio de aplicaciones de Azure para iOS.</span><span class="sxs-lookup"><span data-stu-id="cd299-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="cd299-106">Con los usuarios finales de sincronización sin conexión pueden interactuar con una aplicación móvil tooview, agregar o modificar los datos, incluso cuando no haya ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="cd299-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="cd299-107">Los cambios se almacenan en una base de datos local.</span><span class="sxs-lookup"><span data-stu-id="cd299-107">Changes are stored in a local database.</span></span> <span data-ttu-id="cd299-108">Cuando el dispositivo de hello vuelve a estar conectado, los cambios de Hola se sincronizan con remoto back-end Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="cd299-109">Si se trata de la primera experiencia con aplicaciones móviles, primero debe completar el tutorial Hola [crear una aplicación iOS].</span><span class="sxs-lookup"><span data-stu-id="cd299-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="cd299-110">Si no utiliza Hola Descargar proyecto de inicio rápido de servidor, debe agregar proyecto de tooyour de paquetes de extensión de acceso a datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="cd299-111">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="cd299-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="cd299-112">toolearn más información acerca de la característica de sincronización sin conexión de hello, consulte [sincronización de datos sin conexión en aplicaciones móviles].</span><span class="sxs-lookup"><span data-stu-id="cd299-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="cd299-113"><a name="review-sync"></a>Revise el código de sincronización de cliente hello</span><span class="sxs-lookup"><span data-stu-id="cd299-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="cd299-114">proyecto de cliente de Hola que has descargado para hello [crear una aplicación iOS] tutorial ya contiene código que admite la sincronización sin conexión con una base de datos local de bases de datos principal.</span><span class="sxs-lookup"><span data-stu-id="cd299-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="cd299-115">Esta sección resume lo que ya está incluido en el código del tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="cd299-116">Para obtener información conceptual de característica de hello, consulte [sincronización de datos sin conexión en aplicaciones móviles].</span><span class="sxs-lookup"><span data-stu-id="cd299-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="cd299-117">Característica de sincronización de datos sin conexión de Hola de aplicaciones móviles, los usuarios finales pueden interactuar con una base de datos local incluso cuando la red de hello es inaccesible.</span><span class="sxs-lookup"><span data-stu-id="cd299-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="cd299-118">toouse estas características en la aplicación, inicializa el contexto de sincronización de Hola de `MSClient` y hacer referencia a un almacén local.</span><span class="sxs-lookup"><span data-stu-id="cd299-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="cd299-119">A continuación, hace referencia a la tabla a través de hello **MSSyncTable** interfaz.</span><span class="sxs-lookup"><span data-stu-id="cd299-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="cd299-120">En **QSTodoService.m** (Objective-C) o **ToDoTableViewController.swift** (Swift), tenga en cuenta que Hola tipo de miembro de hello **syncTable** es  **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="cd299-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="cd299-121">La sincronización sin conexión usa esta interfaz de tabla de sincronización en lugar de **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="cd299-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="cd299-122">Cuando se utiliza una tabla de sincronización, todas las operaciones va almacén local de toohello y se sincronizan sólo con hello remoto back-end con inserción explícita y las operaciones de extracción.</span><span class="sxs-lookup"><span data-stu-id="cd299-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="cd299-123">tooget una tabla de sincronización de tooa de referencia, utilice hello **syncTableWithName** método en `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="cd299-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="cd299-124">la funcionalidad de sincronización sin conexión tooremove, use **tableWithName** en su lugar.</span><span class="sxs-lookup"><span data-stu-id="cd299-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="cd299-125">Para poder realizar cualquier operación de tabla, se debe inicializar el almacén local de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="cd299-126">Este es el código relevante hello:</span><span class="sxs-lookup"><span data-stu-id="cd299-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="cd299-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="cd299-127">**Objective-C**.</span></span> <span data-ttu-id="cd299-128">Hola **QSTodoService.init** método:</span><span class="sxs-lookup"><span data-stu-id="cd299-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="cd299-129">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="cd299-129">**Swift**.</span></span> <span data-ttu-id="cd299-130">Hola **ToDoTableViewController.viewDidLoad** método:</span><span class="sxs-lookup"><span data-stu-id="cd299-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="cd299-131">Este método crea un almacén local mediante el uso de hello `MSCoreDataStore` proporciona la interfaz que Hola SDK de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="cd299-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="cd299-132">Como alternativa, puede proporcionar un almacén local diferente mediante la implementación de hello `MSSyncContextDataSource` protocolo.</span><span class="sxs-lookup"><span data-stu-id="cd299-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="cd299-133">Además, Hola primer parámetro de **MSSyncContext** es toospecify usa un controlador de conflictos.</span><span class="sxs-lookup"><span data-stu-id="cd299-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="cd299-134">Porque nos hemos pasado `nil`, obtenemos un controlador de conflictos predeterminado hello, que se produce un error en cualquier conflicto.</span><span class="sxs-lookup"><span data-stu-id="cd299-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="cd299-135">Ahora, vamos a realizar la operación de sincronización real de Hola y obtener datos de back-end remoto hello:</span><span class="sxs-lookup"><span data-stu-id="cd299-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="cd299-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="cd299-136">**Objective-C**.</span></span> <span data-ttu-id="cd299-137">`syncData`primero inserta nuevos cambios y, a continuación, se llama **pullData** tooget datos de back-end remoto Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="cd299-138">A su vez, Hola **pullData** método obtiene datos nuevos que coincide con una consulta:</span><span class="sxs-lookup"><span data-stu-id="cd299-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="cd299-139">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="cd299-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="cd299-140">En la versión de Hola Objective-C, en `syncData`, llamamos primero **pushWithCompletion** en el contexto de sincronización de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="cd299-141">Este método es un miembro de `MSSyncContext` (y no Hola sincronización propia tabla) porque aplica los cambios realizados en todas las tablas.</span><span class="sxs-lookup"><span data-stu-id="cd299-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="cd299-142">Solo los registros que se han modificado de alguna manera localmente (a través de operaciones CUD) se envían toohello server.</span><span class="sxs-lookup"><span data-stu-id="cd299-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="cd299-143">Hola, a continuación, la aplicación auxiliar **pullData** se llama, que llama **MSSyncTable.pullWithQuery** tooretrieve de datos remotos y almacenarlos en la base de datos local de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="cd299-144">En la versión de Swift hello, porque no estaba estrictamente necesaria, la operación de inserción de hello hay ninguna llamada demasiado**pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="cd299-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="cd299-145">Si hay cambios pendientes en el contexto de sincronización de hello para la tabla de Hola que está realizando una operación de inserción, extracción siempre realiza una inserción en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="cd299-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="cd299-146">Sin embargo, si tiene más de una tabla de sincronización, es mejor tooensure de inserción de llamada tooexplicitly que todo lo que sea coherente en las tablas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="cd299-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="cd299-147">En hello Objective-C y versiones Swift, puede usar hello **pullWithQuery** método toospecify un toofilter consulta Hola registros que desean tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="cd299-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="cd299-148">En este ejemplo, consulta Hola recupera todos los registros de hello remoto `TodoItem` tabla.</span><span class="sxs-lookup"><span data-stu-id="cd299-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="cd299-149">Hola segundo parámetro de **pullWithQuery** es un identificador de la consulta que se usa para *sincronización incremental*. Sincronización incremental recupera únicamente los registros que se han modificado desde la última sincronización hello, uso del registro de hello `UpdatedAt` marca de tiempo (llamado `updatedAt` en hello el almacén local.) Hola identificador de la consulta debe ser una cadena descriptiva que es única para cada consulta lógica en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cd299-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="cd299-150">tooopt dejen de estar sincronizados incremental, pasar `nil` como Hola Id. de consulta.</span><span class="sxs-lookup"><span data-stu-id="cd299-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="cd299-151">Es posible que este enfoque resulte ineficaz, ya que recupera todos los registros en cada operación de extracción.</span><span class="sxs-lookup"><span data-stu-id="cd299-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="cd299-152">aplicación de Hello Objective-C se sincroniza al modificar o agregar datos, cuando un usuario realiza gestos de actualización de Hola y de inicio.</span><span class="sxs-lookup"><span data-stu-id="cd299-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="cd299-153">aplicación de Swift Hello se sincroniza cuando el usuario de hello realiza gestos de actualización de Hola y al iniciar.</span><span class="sxs-lookup"><span data-stu-id="cd299-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="cd299-154">Porque las sincronizaciones siempre que hay datos de aplicación hello modificación (Objective-C) o cada vez que inicia de aplicación hello (Objective-C y Swift), aplicación hello se da por supuesto que el usuario Hola está en línea.</span><span class="sxs-lookup"><span data-stu-id="cd299-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="cd299-155">En una sección posterior, se actualizará la aplicación hello para que los usuarios pueden editar incluso cuando están sin conexión.</span><span class="sxs-lookup"><span data-stu-id="cd299-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="cd299-156"><a name="review-core-data"></a>Modelo de datos de núcleo de Hola de revisión</span><span class="sxs-lookup"><span data-stu-id="cd299-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="cd299-157">Cuando se usa el almacén sin conexión de datos principal de hello, debe definir tablas y campos en el modelo de datos.</span><span class="sxs-lookup"><span data-stu-id="cd299-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="cd299-158">aplicación de ejemplo de Hola ya incluye un modelo de datos con formato correcto de saludo.</span><span class="sxs-lookup"><span data-stu-id="cd299-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="cd299-159">En esta sección, se guiará a través de estas tablas tooshow cómo se utilizan.</span><span class="sxs-lookup"><span data-stu-id="cd299-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="cd299-160">Abra **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="cd299-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="cd299-161">Cuatro tablas son definidos: Hola tres que usan SDK y uno que se utiliza para tareas de hello elementos propios:</span><span class="sxs-lookup"><span data-stu-id="cd299-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="cd299-162">MS_TableOperations: Pistas Hola elementos que se deben toobe sincronizado con el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="cd299-163">MS_TableOperationErrors: realiza el seguimiento de los errores que se producen durante la sincronización sin conexión.</span><span class="sxs-lookup"><span data-stu-id="cd299-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="cd299-164">MS_TableConfig: Pistas Hola la última vez que se actualizó para la última operación de sincronización Hola para todas las operaciones de extracción.</span><span class="sxs-lookup"><span data-stu-id="cd299-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="cd299-165">TodoItem: Almacena elementos de hello pendientes.</span><span class="sxs-lookup"><span data-stu-id="cd299-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="cd299-166">las columnas del sistema de Hola **registroen**, **updatedAt**, y **versión** son propiedades del sistema opcional.</span><span class="sxs-lookup"><span data-stu-id="cd299-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="cd299-167">Hola SDK de aplicaciones móviles reserva los nombres de columna que comienzan por "**``**".</span><span class="sxs-lookup"><span data-stu-id="cd299-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="cd299-168">Utilice este prefijo exclusivamente para las columnas del sistema.</span><span class="sxs-lookup"><span data-stu-id="cd299-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="cd299-169">En caso contrario, se modifican los nombres de columna cuando se usa remoto back-end Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="cd299-170">Cuando se usa la característica de sincronización sin conexión de hello, definir tres tablas del sistema hello y una tabla de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="cd299-171">Tablas del sistema</span><span class="sxs-lookup"><span data-stu-id="cd299-171">System tables</span></span>

<span data-ttu-id="cd299-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="cd299-172">**MS_TableOperations**</span></span>  

![Atributos de la tabla MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="cd299-174">Atributo</span><span class="sxs-lookup"><span data-stu-id="cd299-174">Attribute</span></span> | <span data-ttu-id="cd299-175">Tipo</span><span class="sxs-lookup"><span data-stu-id="cd299-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="cd299-176">id</span><span class="sxs-lookup"><span data-stu-id="cd299-176">id</span></span> | <span data-ttu-id="cd299-177">Integer 64</span><span class="sxs-lookup"><span data-stu-id="cd299-177">Integer 64</span></span> |
| <span data-ttu-id="cd299-178">itemId</span><span class="sxs-lookup"><span data-stu-id="cd299-178">itemId</span></span> | <span data-ttu-id="cd299-179">Cadena</span><span class="sxs-lookup"><span data-stu-id="cd299-179">String</span></span> |
| <span data-ttu-id="cd299-180">propiedades</span><span class="sxs-lookup"><span data-stu-id="cd299-180">properties</span></span> | <span data-ttu-id="cd299-181">Binary Data</span><span class="sxs-lookup"><span data-stu-id="cd299-181">Binary Data</span></span> |
| <span data-ttu-id="cd299-182">table</span><span class="sxs-lookup"><span data-stu-id="cd299-182">table</span></span> | <span data-ttu-id="cd299-183">Cadena</span><span class="sxs-lookup"><span data-stu-id="cd299-183">String</span></span> |
| <span data-ttu-id="cd299-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="cd299-184">tableKind</span></span> | <span data-ttu-id="cd299-185">Integer 16</span><span class="sxs-lookup"><span data-stu-id="cd299-185">Integer 16</span></span> |


<span data-ttu-id="cd299-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="cd299-186">**MS_TableOperationErrors**</span></span>

 ![Atributos de la tabla MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="cd299-188">Atributo</span><span class="sxs-lookup"><span data-stu-id="cd299-188">Attribute</span></span> | <span data-ttu-id="cd299-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="cd299-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="cd299-190">id</span><span class="sxs-lookup"><span data-stu-id="cd299-190">id</span></span> |<span data-ttu-id="cd299-191">String</span><span class="sxs-lookup"><span data-stu-id="cd299-191">String</span></span> |
| <span data-ttu-id="cd299-192">operationId</span><span class="sxs-lookup"><span data-stu-id="cd299-192">operationId</span></span> |<span data-ttu-id="cd299-193">Integer 64</span><span class="sxs-lookup"><span data-stu-id="cd299-193">Integer 64</span></span> |
| <span data-ttu-id="cd299-194">propiedades</span><span class="sxs-lookup"><span data-stu-id="cd299-194">properties</span></span> |<span data-ttu-id="cd299-195">Binary Data</span><span class="sxs-lookup"><span data-stu-id="cd299-195">Binary Data</span></span> |
| <span data-ttu-id="cd299-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="cd299-196">tableKind</span></span> |<span data-ttu-id="cd299-197">Integer 16</span><span class="sxs-lookup"><span data-stu-id="cd299-197">Integer 16</span></span> |

 <span data-ttu-id="cd299-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="cd299-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="cd299-199">Atributo</span><span class="sxs-lookup"><span data-stu-id="cd299-199">Attribute</span></span> | <span data-ttu-id="cd299-200">Tipo</span><span class="sxs-lookup"><span data-stu-id="cd299-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="cd299-201">id</span><span class="sxs-lookup"><span data-stu-id="cd299-201">id</span></span> |<span data-ttu-id="cd299-202">String</span><span class="sxs-lookup"><span data-stu-id="cd299-202">String</span></span> |
| <span data-ttu-id="cd299-203">key</span><span class="sxs-lookup"><span data-stu-id="cd299-203">key</span></span> |<span data-ttu-id="cd299-204">Cadena</span><span class="sxs-lookup"><span data-stu-id="cd299-204">String</span></span> |
| <span data-ttu-id="cd299-205">keyType</span><span class="sxs-lookup"><span data-stu-id="cd299-205">keyType</span></span> |<span data-ttu-id="cd299-206">Integer 64</span><span class="sxs-lookup"><span data-stu-id="cd299-206">Integer 64</span></span> |
| <span data-ttu-id="cd299-207">table</span><span class="sxs-lookup"><span data-stu-id="cd299-207">table</span></span> |<span data-ttu-id="cd299-208">Cadena</span><span class="sxs-lookup"><span data-stu-id="cd299-208">String</span></span> |
| <span data-ttu-id="cd299-209">value</span><span class="sxs-lookup"><span data-stu-id="cd299-209">value</span></span> |<span data-ttu-id="cd299-210">String</span><span class="sxs-lookup"><span data-stu-id="cd299-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="cd299-211">Tabla de datos</span><span class="sxs-lookup"><span data-stu-id="cd299-211">Data table</span></span>

<span data-ttu-id="cd299-212">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="cd299-212">**TodoItem**</span></span>

| <span data-ttu-id="cd299-213">Atributo</span><span class="sxs-lookup"><span data-stu-id="cd299-213">Attribute</span></span> | <span data-ttu-id="cd299-214">Escriba</span><span class="sxs-lookup"><span data-stu-id="cd299-214">Type</span></span> | <span data-ttu-id="cd299-215">Nota:</span><span class="sxs-lookup"><span data-stu-id="cd299-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cd299-216">id</span><span class="sxs-lookup"><span data-stu-id="cd299-216">id</span></span> | <span data-ttu-id="cd299-217">Cadena, marcado obligatorio</span><span class="sxs-lookup"><span data-stu-id="cd299-217">String, marked required</span></span> |<span data-ttu-id="cd299-218">Clave principal en almacén remoto</span><span class="sxs-lookup"><span data-stu-id="cd299-218">Primary key in remote store</span></span> |
| <span data-ttu-id="cd299-219">complete</span><span class="sxs-lookup"><span data-stu-id="cd299-219">complete</span></span> | <span data-ttu-id="cd299-220">Booleano</span><span class="sxs-lookup"><span data-stu-id="cd299-220">Boolean</span></span> | <span data-ttu-id="cd299-221">Campo de tarea pendiente</span><span class="sxs-lookup"><span data-stu-id="cd299-221">To-do item field</span></span> |
| <span data-ttu-id="cd299-222">text</span><span class="sxs-lookup"><span data-stu-id="cd299-222">text</span></span> |<span data-ttu-id="cd299-223">string</span><span class="sxs-lookup"><span data-stu-id="cd299-223">String</span></span> |<span data-ttu-id="cd299-224">Campo de tarea pendiente</span><span class="sxs-lookup"><span data-stu-id="cd299-224">To-do item field</span></span> |
| <span data-ttu-id="cd299-225">createdAt</span><span class="sxs-lookup"><span data-stu-id="cd299-225">createdAt</span></span> | <span data-ttu-id="cd299-226">Date</span><span class="sxs-lookup"><span data-stu-id="cd299-226">Date</span></span> | <span data-ttu-id="cd299-227">(opcional) Se asigna demasiado**registroen** propiedad del sistema</span><span class="sxs-lookup"><span data-stu-id="cd299-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="cd299-228">updatedAt</span><span class="sxs-lookup"><span data-stu-id="cd299-228">updatedAt</span></span> | <span data-ttu-id="cd299-229">Date</span><span class="sxs-lookup"><span data-stu-id="cd299-229">Date</span></span> | <span data-ttu-id="cd299-230">(opcional) Se asigna demasiado**updatedAt** propiedad del sistema</span><span class="sxs-lookup"><span data-stu-id="cd299-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="cd299-231">versión</span><span class="sxs-lookup"><span data-stu-id="cd299-231">version</span></span> | <span data-ttu-id="cd299-232">String</span><span class="sxs-lookup"><span data-stu-id="cd299-232">String</span></span> | <span data-ttu-id="cd299-233">(opcional) Conflictos de toodetect usado, tooversion de mapas</span><span class="sxs-lookup"><span data-stu-id="cd299-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="cd299-234"><a name="setup-sync"></a>Cambiar el comportamiento de sincronización de Hola de aplicación hello</span><span class="sxs-lookup"><span data-stu-id="cd299-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="cd299-235">En esta sección, modificar aplicación hello para que no se sincroniza en el inicio de aplicación o al insertar y actualizar los elementos.</span><span class="sxs-lookup"><span data-stu-id="cd299-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="cd299-236">Se sincroniza cuando se realice el botón de gesto de hello actualizar.</span><span class="sxs-lookup"><span data-stu-id="cd299-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="cd299-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="cd299-237">**Objective-C**:</span></span>

1. <span data-ttu-id="cd299-238">En **QSTodoListViewController.m**, cambiar hello **viewDidLoad** método tooremove Hola llamada demasiado`[self refresh]` final Hola del método hello.</span><span class="sxs-lookup"><span data-stu-id="cd299-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="cd299-239">Ahora datos hello no se ha sincronizado con el servidor de hello en el inicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cd299-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="cd299-240">En su lugar, se se ha sincronizado con contenido de hello del almacén local de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="cd299-241">En **QSTodoService.m**, modifique la definición de Hola de `addItem` para que lo no sincronizará después de que se inserta el elemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="cd299-242">Quitar hello `self syncData` bloquear y reemplazarlo por siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="cd299-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="cd299-243">Modificar la definición de Hola de `completeItem` tal y como se mencionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cd299-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="cd299-244">Quite el bloque de Hola para `self syncData` y reemplazarlo por siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="cd299-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="cd299-245">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="cd299-245">**Swift**:</span></span>

<span data-ttu-id="cd299-246">En `viewDidLoad`, en **ToDoTableViewController.swift**, comenta dos líneas de Hola se muestra aquí, toostop sincronización en el inicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cd299-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="cd299-247">En tiempo de Hola de redactar este artículo, aplicación de lista de tareas de Swift hello no actualizar el servicio de hello, cuando un usuario agrega o completa un elemento.</span><span class="sxs-lookup"><span data-stu-id="cd299-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="cd299-248">Actualiza servicio Hola solo en el inicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cd299-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="cd299-249"><a name="test-app"></a>Probar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="cd299-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="cd299-250">En esta sección, se conectará toosimulate de dirección URL no válido de tooan un escenario sin conexión.</span><span class="sxs-lookup"><span data-stu-id="cd299-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="cd299-251">Cuando se agregan elementos de datos, que están mantenían en hello almacenar datos locales de núcleos, pero no están sincronizados con back-end de aplicación móvil de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="cd299-252">Cambiar dirección URL de la aplicación móvil de hello en **QSTodoService.m** tooan dirección URL no válida y vuelva a la aplicación hello ejecución:</span><span class="sxs-lookup"><span data-stu-id="cd299-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="cd299-253">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="cd299-253">**Objective-C**.</span></span> <span data-ttu-id="cd299-254">En QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="cd299-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="cd299-255">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="cd299-255">**Swift**.</span></span> <span data-ttu-id="cd299-256">En ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="cd299-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="cd299-257">Agregue algunas tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="cd299-257">Add some to-do items.</span></span> <span data-ttu-id="cd299-258">Salga de simulador de hello (o aplicación hello forzosamente cerrar) y, a continuación, reiniciarlo.</span><span class="sxs-lookup"><span data-stu-id="cd299-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="cd299-259">Compruebe que los cambios se conserven.</span><span class="sxs-lookup"><span data-stu-id="cd299-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="cd299-260">Ver contenido de Hola de hello remoto **TodoItem** tabla:</span><span class="sxs-lookup"><span data-stu-id="cd299-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="cd299-261">Para un back-end de Node.js, visite toohello [portal de Azure](https://portal.azure.com/) y, en su aplicación móvil de back-end, haga clic en **tablas fácil** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="cd299-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="cd299-262">En un back-end de .NET, use una herramienta SQL, como SQL Server Management Studio, o un cliente REST, como Fiddler o Postman.</span><span class="sxs-lookup"><span data-stu-id="cd299-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="cd299-263">Compruebe que dispone de nuevos elementos de hello *no* está sincronizado con el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="cd299-264">Cambio Hola URL atrás toohello corregir uno en **QSTodoService.m**y la aplicación hello vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="cd299-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="cd299-265">Realizar gestos de actualización de hello desplazando hacia abajo de la lista de Hola de elementos.</span><span class="sxs-lookup"><span data-stu-id="cd299-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="cd299-266">Se muestra un control giratorio de progreso.</span><span class="sxs-lookup"><span data-stu-id="cd299-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="cd299-267">Hola de vista **TodoItem** datos de nuevo.</span><span class="sxs-lookup"><span data-stu-id="cd299-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="cd299-268">elementos de tareas nuevas y modificadas de Hello ahora deben aparecer.</span><span class="sxs-lookup"><span data-stu-id="cd299-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="cd299-269">Resumen</span><span class="sxs-lookup"><span data-stu-id="cd299-269">Summary</span></span>
<span data-ttu-id="cd299-270">característica de sincronización sin conexión de hello toosupport, hemos usado hello `MSSyncTable` de la interfaz y se inicializa `MSClient.syncContext` con un almacén local.</span><span class="sxs-lookup"><span data-stu-id="cd299-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="cd299-271">En este caso, el almacén local de hello era una base de datos de bases de datos principal.</span><span class="sxs-lookup"><span data-stu-id="cd299-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="cd299-272">Cuando se utiliza un almacén local de datos principal, debe definir varias tablas con hello [corregir las propiedades del sistema](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="cd299-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="cd299-273">Hola normal crear, leer, actualizar y eliminar operaciones (CRUD) para aplicaciones móviles de trabajo como si la aplicación hello aún está conectado, pero todas las operaciones de Hola se producen en el almacén local de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd299-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="cd299-274">Cuando se sincroniza almacén local de hello con servidor hello, hemos usado hello **MSSyncTable.pullWithQuery** método.</span><span class="sxs-lookup"><span data-stu-id="cd299-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd299-275">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cd299-275">Additional resources</span></span>
* <span data-ttu-id="cd299-276">[sincronización de datos sin conexión en aplicaciones móviles]</span><span class="sxs-lookup"><span data-stu-id="cd299-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="cd299-277">[Portada en la nube: Sincronización sin conexión en servicios móviles de Azure] \(Hola vídeo está acerca de servicios móviles y funcionamiento de la sincronización de aplicaciones móviles sin conexión de una manera similar.\)</span><span class="sxs-lookup"><span data-stu-id="cd299-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[crear una aplicación iOS]: app-service-mobile-ios-get-started.md
[sincronización de datos sin conexión en aplicaciones móviles]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Portada en la nube: Sincronización sin conexión en servicios móviles de Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
