---
title: "Activar la sincronización sin conexión para la aplicación móvil de Azure (Android)"
description: "Obtenga información sobre cómo usar las Aplicaciones móviles del Servicio de aplicaciones para almacenar en caché y sincronizar datos sin conexión en su aplicación de Android"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 304323c1816302e8c1f68f36a029aee55e02c54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="d18d5-103">Activar la sincronización sin conexión para la aplicación móvil de Android</span><span class="sxs-lookup"><span data-stu-id="d18d5-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="d18d5-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d18d5-104">Overview</span></span>
<span data-ttu-id="d18d5-105">En este tutorial se explica la característica de sincronización sin conexión de Aplicaciones móviles de Azure para Android.</span><span class="sxs-lookup"><span data-stu-id="d18d5-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="d18d5-106">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil &mdash;ver, agregar o modificar datos&mdash; aun cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="d18d5-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="d18d5-107">Los cambios se almacenan en una base de datos local.</span><span class="sxs-lookup"><span data-stu-id="d18d5-107">Changes are stored in a local database.</span></span> <span data-ttu-id="d18d5-108">Una vez que el dispositivo se vuelve a conectar, estos cambios se sincronizan con el back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="d18d5-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="d18d5-109">Si esta es la primera vez que usa Aplicaciones móviles de Azure, primero debería completar el tutorial [Creación de una aplicación de Android].</span><span class="sxs-lookup"><span data-stu-id="d18d5-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="d18d5-110">Si no usa el proyecto de servidor de inicio rápido descargado, debe agregar paquetes de extensión de acceso de datos al proyecto.</span><span class="sxs-lookup"><span data-stu-id="d18d5-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="d18d5-111">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [Trabajar con el SDK del servidor back-end de .NET para Aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d18d5-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="d18d5-112">Para obtener más información acerca de la característica de sincronización sin conexión, consulte el tema [Sincronización de datos sin conexión en Aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="d18d5-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="d18d5-113">Actualización de la aplicación para que admita la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="d18d5-113">Update the app to support offline sync</span></span>
<span data-ttu-id="d18d5-114">Con la sincronización sin conexión, se lee y se escribe desde una *tabla de sincronización* (usando la interfaz *IMobileServiceSyncTable*), que forma parte de una base de datos **SQLite** en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d18d5-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="d18d5-115">Para insertar y extraer los cambios entre el dispositivo y Azure Mobile Services, se usa un *contexto de sincronización* (*MobileServiceClient.SyncContext*), que se inicializa con la base de datos local usada para almacenar los datos localmente.</span><span class="sxs-lookup"><span data-stu-id="d18d5-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="d18d5-116">En `TodoActivity.java`, convierta en comentario la definición existente de `mToDoTable` y quite la marca de comentario de la versión de la tabla de sincronización:</span><span class="sxs-lookup"><span data-stu-id="d18d5-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="d18d5-117">En el método `onCreate`, convierta en comentario la inicialización existente de `mToDoTable` y quite la marca de comentario de esta definición:</span><span class="sxs-lookup"><span data-stu-id="d18d5-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="d18d5-118">En `refreshItemsFromTable`, convierta en comentario la definición de `results` y quite la marca de comentario de esta definición:</span><span class="sxs-lookup"><span data-stu-id="d18d5-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="d18d5-119">Convierta en comentario la definición de `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="d18d5-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="d18d5-120">Quite la marca de comentario de la definición de `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="d18d5-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="d18d5-121">Quite la marca de comentario de la definición de `sync`:</span><span class="sxs-lookup"><span data-stu-id="d18d5-121">Uncomment the definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-the-app"></a><span data-ttu-id="d18d5-122">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d18d5-122">Test the app</span></span>
<span data-ttu-id="d18d5-123">En esta sección, probará el comportamiento con la red inalámbrica activada y, después, desactivará la red inalámbrica para crear un escenario sin conexión.</span><span class="sxs-lookup"><span data-stu-id="d18d5-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="d18d5-124">Al agregar elementos de datos, se guardan en el almacén local de SQLite, pero no se sincronizarán con el servicio móvil hasta que presione el botón **Actualizar** .</span><span class="sxs-lookup"><span data-stu-id="d18d5-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="d18d5-125">Otras aplicaciones pueden tener requisitos diferentes con respecto a cuándo deben sincronizarse los datos, pero para los fines de demostración de este tutorial, haga que el usuario lo solicite expresamente.</span><span class="sxs-lookup"><span data-stu-id="d18d5-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="d18d5-126">Cuando presione ese botón, se iniciará una nueva tarea en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="d18d5-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="d18d5-127">En primer lugar, inserta todos los cambios realizados en el almacén local mediante el contexto de sincronización y, a continuación, extrae todos los datos cambiados de Azure a la tabla local.</span><span class="sxs-lookup"><span data-stu-id="d18d5-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="d18d5-128">Pruebas sin conexión</span><span class="sxs-lookup"><span data-stu-id="d18d5-128">Offline testing</span></span>
1. <span data-ttu-id="d18d5-129">Coloque el dispositivo o el simulador en *Modo avión*.</span><span class="sxs-lookup"><span data-stu-id="d18d5-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="d18d5-130">Esto crea un escenario sin conexión.</span><span class="sxs-lookup"><span data-stu-id="d18d5-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="d18d5-131">Agregue algunos elementos *ToDo* o marque algunos elementos como completados.</span><span class="sxs-lookup"><span data-stu-id="d18d5-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="d18d5-132">Salga del dispositivo o del simulador (o fuerce el cierre de la aplicación) y reinicie.</span><span class="sxs-lookup"><span data-stu-id="d18d5-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="d18d5-133">Compruebe que los cambios se conservan en el dispositivo porque se guardan en el almacén local de SQLite.</span><span class="sxs-lookup"><span data-stu-id="d18d5-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="d18d5-134">Visualice los contenidos de la tabla *TodoItem* de Azure con una herramienta SQL, como *SQL Server Management Studio* o con un cliente REST como *Fiddler* o *Postman*.</span><span class="sxs-lookup"><span data-stu-id="d18d5-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="d18d5-135">Compruebe que los nuevos elementos *no* se han sincronizado con el servidor:</span><span class="sxs-lookup"><span data-stu-id="d18d5-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="d18d5-136">En un back-end de Node.js, vaya a [Azure Portal](https://portal.azure.com/) y, en el back-end de Mobile App, haga clic en **Tablas fáciles** > **TodoItem** para ver el contenido de la tabla `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="d18d5-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="d18d5-137">En el back-end de .NET, vea el contenido de tabla con una herramienta SQL, como *SQL Server Management Studio*, o con un cliente REST como *Fiddler* o *Postman*.</span><span class="sxs-lookup"><span data-stu-id="d18d5-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="d18d5-138">Active la red inalámbrica en el dispositivo o el simulador.</span><span class="sxs-lookup"><span data-stu-id="d18d5-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="d18d5-139">Después, presione el botón **Actualizar** .</span><span class="sxs-lookup"><span data-stu-id="d18d5-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="d18d5-140">Vea los datos de TodoItem de nuevo en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d18d5-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="d18d5-141">Ahora deberían aparecer los elementos de TodoItems nuevos y modificados.</span><span class="sxs-lookup"><span data-stu-id="d18d5-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d18d5-142">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d18d5-142">Additional Resources</span></span>
* <span data-ttu-id="d18d5-143">[Sincronización de datos sin conexión en Aplicaciones móviles de Azure]</span><span class="sxs-lookup"><span data-stu-id="d18d5-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="d18d5-144">[Cloud Cover: sincronización sin conexión en Servicios móviles de Azure] \( (nota: el vídeo trata sobre Mobile Services, pero la sincronización sin conexión funciona de forma similar en Azure Mobile Apps)\)</span><span class="sxs-lookup"><span data-stu-id="d18d5-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

<span data-ttu-id="d18d5-145">[Sincronización de datos sin conexión en Aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="d18d5-145">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

<span data-ttu-id="d18d5-146">[Creación de una aplicación de Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="d18d5-146">[Create an Android App]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="d18d5-147">[Cloud Cover: sincronización sin conexión en Servicios móviles de Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="d18d5-147">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

