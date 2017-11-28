---
title: "aaaEnable la sincronización sin conexión de la aplicación móvil de Azure (Android)"
description: "Obtenga información acerca de cómo toouse la toocache y sincronización de datos sin conexión de aplicación del servicio de aplicaciones móviles en su aplicación Android"
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
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="2d8ed-103">Activar la sincronización sin conexión para la aplicación móvil de Android</span><span class="sxs-lookup"><span data-stu-id="2d8ed-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="2d8ed-104">Información general</span><span class="sxs-lookup"><span data-stu-id="2d8ed-104">Overview</span></span>
<span data-ttu-id="2d8ed-105">Este tutorial trata la característica de sincronización sin conexión de Hola de aplicaciones móviles de Azure para Android.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="2d8ed-106">Sincronización sin conexión permite toointeract de los usuarios finales con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="2d8ed-107">Los cambios se almacenan en una base de datos local.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-107">Changes are stored in a local database.</span></span> <span data-ttu-id="2d8ed-108">Una vez que el dispositivo de hello vuelve a estar conectado, estos cambios se sincronizan con back-end de hello remoto.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="2d8ed-109">Si se trata de la primera experiencia con aplicaciones móviles de Azure, primero debe completar el tutorial Hola [crear una aplicación Android].</span><span class="sxs-lookup"><span data-stu-id="2d8ed-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="2d8ed-110">Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto tooyour de paquetes de extensión de acceso de hello datos.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="2d8ed-111">Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="2d8ed-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="2d8ed-112">toolearn más información acerca de la característica de sincronización sin conexión de hello, vea el tema de hello [sincronización de datos sin conexión en aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="2d8ed-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="2d8ed-113">Actualizar la sincronización sin conexión de hello aplicaciones toosupport</span><span class="sxs-lookup"><span data-stu-id="2d8ed-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="2d8ed-114">Con la sincronización sin conexión, se lectura y escritura de tooand desde una *tabla sincronización* (con hello *IMobileServiceSyncTable* interfaz), que forma parte de un **SQLite** base de datos en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="2d8ed-115">cambios de toopush y extracción entre dispositivos de Hola y servicios móviles de Azure, use un *contexto de sincronización* (*MobileServiceClient.SyncContext*), que se inicializa con la base de datos local de Hola toostore datos localmente.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="2d8ed-116">En `TodoActivity.java`, comentario Hola definición existente de `mToDoTable` y quite la versión de la tabla de hello sincronización:</span><span class="sxs-lookup"><span data-stu-id="2d8ed-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="2d8ed-117">Hola `onCreate` método, comenta inicialización existente de Hola de `mToDoTable` y quite el comentario de esta definición:</span><span class="sxs-lookup"><span data-stu-id="2d8ed-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="2d8ed-118">En `refreshItemsFromTable` comentario definición Hola de `results` y quite el comentario de esta definición:</span><span class="sxs-lookup"><span data-stu-id="2d8ed-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="2d8ed-119">Comenta la definición de Hola de `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="2d8ed-120">Quite la definición de Hola de `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="2d8ed-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="2d8ed-121">Quite la definición de Hola de `sync`:</span><span class="sxs-lookup"><span data-stu-id="2d8ed-121">Uncomment hello definition of `sync`:</span></span>
   
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

## <a name="test-hello-app"></a><span data-ttu-id="2d8ed-122">Probar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="2d8ed-122">Test hello app</span></span>
<span data-ttu-id="2d8ed-123">En esta sección, probar el comportamiento de hello con Wi-Fi en y, a continuación, apague Wi-Fi toocreate un escenario sin conexión.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="2d8ed-124">Cuando se agregan elementos de datos, se mantienen en el almacén local de SQLite de hello, pero el servicio móvil no sincronizados toohello, hasta que presione hello **actualizar** botón.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="2d8ed-125">Otras aplicaciones pueden tener requisitos diferentes con respecto a cuando datos necesita toobe sincronizado, pero con fines de demostración de este tutorial tiene usuario Hola solicita de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="2d8ed-126">Cuando presione ese botón, se iniciará una nueva tarea en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="2d8ed-127">En primer lugar, inserta todos los cambios realizados toohello almacén local mediante el contexto de sincronización y, a continuación, extrae todos los cambiar datos de tabla de Azure toohello local.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="2d8ed-128">Pruebas sin conexión</span><span class="sxs-lookup"><span data-stu-id="2d8ed-128">Offline testing</span></span>
1. <span data-ttu-id="2d8ed-129">Dispositivo de Hola de contexto o el simulador en *modo de avión*.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="2d8ed-130">Esto crea un escenario sin conexión.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="2d8ed-131">Agregue algunos elementos *ToDo* o marque algunos elementos como completados.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="2d8ed-132">Salga de dispositivo de Hola o simulador (o aplicación hello forzosamente cerrar) y reiniciar.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="2d8ed-133">Compruebe que se han guardado los cambios en el dispositivo de hello debido a se conservan en el almacén local de SQLite de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="2d8ed-134">Ver contenido de Hola de hello Azure *TodoItem* tabla con una herramienta SQL como *SQL Server Management Studio*, o un cliente REST como *Fiddler* o  *Postman*.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="2d8ed-135">Compruebe que dispone de nuevos elementos de hello *no* se han sincronizado toohello server</span><span class="sxs-lookup"><span data-stu-id="2d8ed-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="2d8ed-136">Para un back-end de Node.js, visite toohello [portal de Azure](https://portal.azure.com/), y en su aplicación móvil de back-end, haga clic en **tablas fácil** > **TodoItem** tooview contenido de Hola de hello `TodoItem` tabla.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="2d8ed-137">Para un back-end. NET, tabla de Hola de vista de contenido con una herramienta SQL como *SQL Server Management Studio*, o un cliente REST como *Fiddler* o *Postman*.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="2d8ed-138">Activar Wi-Fi en dispositivos de Hola o el simulador.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="2d8ed-139">A continuación, presione hello **actualizar** botón.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="2d8ed-140">Volver a ver datos de TodoItem Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="2d8ed-141">Hola que debería aparecer ahora TodoItems nuevas y modificadas.</span><span class="sxs-lookup"><span data-stu-id="2d8ed-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d8ed-142">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2d8ed-142">Additional Resources</span></span>
* <span data-ttu-id="2d8ed-143">[sincronización de datos sin conexión en aplicaciones móviles de Azure]</span><span class="sxs-lookup"><span data-stu-id="2d8ed-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="2d8ed-144">[Portada en la nube: Sincronización sin conexión en servicios móviles de Azure] \(Nota: Hola vídeo se encuentra en servicios móviles, pero la sincronización sin conexión funciona de forma similar en aplicaciones móviles de Azure\)</span><span class="sxs-lookup"><span data-stu-id="2d8ed-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[sincronización de datos sin conexión en aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md

[crear una aplicación Android]: app-service-mobile-android-get-started.md

[Portada en la nube: Sincronización sin conexión en servicios móviles de Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

