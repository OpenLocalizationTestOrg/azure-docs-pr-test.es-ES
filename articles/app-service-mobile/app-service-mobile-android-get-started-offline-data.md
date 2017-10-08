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
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>Activar la sincronización sin conexión para la aplicación móvil de Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Información general
Este tutorial trata la característica de sincronización sin conexión de Hola de aplicaciones móviles de Azure para Android. Sincronización sin conexión permite toointeract de los usuarios finales con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red. Los cambios se almacenan en una base de datos local. Una vez que el dispositivo de hello vuelve a estar conectado, estos cambios se sincronizan con back-end de hello remoto.

Si se trata de la primera experiencia con aplicaciones móviles de Azure, primero debe completar el tutorial Hola [crear una aplicación Android]. Si no usa Hola descarga el proyecto de servidor de inicio rápido, debe agregar proyecto tooyour de paquetes de extensión de acceso de hello datos. Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn más información acerca de la característica de sincronización sin conexión de hello, vea el tema de hello [sincronización de datos sin conexión en aplicaciones móviles de Azure].

## <a name="update-hello-app-toosupport-offline-sync"></a>Actualizar la sincronización sin conexión de hello aplicaciones toosupport
Con la sincronización sin conexión, se lectura y escritura de tooand desde una *tabla sincronización* (con hello *IMobileServiceSyncTable* interfaz), que forma parte de un **SQLite** base de datos en el dispositivo.

cambios de toopush y extracción entre dispositivos de Hola y servicios móviles de Azure, use un *contexto de sincronización* (*MobileServiceClient.SyncContext*), que se inicializa con la base de datos local de Hola toostore datos localmente.

1. En `TodoActivity.java`, comentario Hola definición existente de `mToDoTable` y quite la versión de la tabla de hello sincronización:
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. Hola `onCreate` método, comenta inicialización existente de Hola de `mToDoTable` y quite el comentario de esta definición:
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. En `refreshItemsFromTable` comentario definición Hola de `results` y quite el comentario de esta definición:
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. Comenta la definición de Hola de `refreshItemsFromMobileServiceTable`.
5. Quite la definición de Hola de `refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. Quite la definición de Hola de `sync`:
   
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

## <a name="test-hello-app"></a>Probar la aplicación hello
En esta sección, probar el comportamiento de hello con Wi-Fi en y, a continuación, apague Wi-Fi toocreate un escenario sin conexión.

Cuando se agregan elementos de datos, se mantienen en el almacén local de SQLite de hello, pero el servicio móvil no sincronizados toohello, hasta que presione hello **actualizar** botón. Otras aplicaciones pueden tener requisitos diferentes con respecto a cuando datos necesita toobe sincronizado, pero con fines de demostración de este tutorial tiene usuario Hola solicita de forma explícita.

Cuando presione ese botón, se iniciará una nueva tarea en segundo plano. En primer lugar, inserta todos los cambios realizados toohello almacén local mediante el contexto de sincronización y, a continuación, extrae todos los cambiar datos de tabla de Azure toohello local.

### <a name="offline-testing"></a>Pruebas sin conexión
1. Dispositivo de Hola de contexto o el simulador en *modo de avión*. Esto crea un escenario sin conexión.
2. Agregue algunos elementos *ToDo* o marque algunos elementos como completados. Salga de dispositivo de Hola o simulador (o aplicación hello forzosamente cerrar) y reiniciar. Compruebe que se han guardado los cambios en el dispositivo de hello debido a se conservan en el almacén local de SQLite de Hola.
3. Ver contenido de Hola de hello Azure *TodoItem* tabla con una herramienta SQL como *SQL Server Management Studio*, o un cliente REST como *Fiddler* o  *Postman*. Compruebe que dispone de nuevos elementos de hello *no* se han sincronizado toohello server
   
       + Para un back-end de Node.js, visite toohello [portal de Azure](https://portal.azure.com/), y en su aplicación móvil de back-end, haga clic en **tablas fácil** > **TodoItem** tooview contenido de Hola de hello `TodoItem` tabla.
       + Para un back-end. NET, tabla de Hola de vista de contenido con una herramienta SQL como *SQL Server Management Studio*, o un cliente REST como *Fiddler* o *Postman*.
4. Activar Wi-Fi en dispositivos de Hola o el simulador. A continuación, presione hello **actualizar** botón.
5. Volver a ver datos de TodoItem Hola Hola portal de Azure. Hola que debería aparecer ahora TodoItems nuevas y modificadas.

## <a name="additional-resources"></a>Recursos adicionales
* [sincronización de datos sin conexión en aplicaciones móviles de Azure]
* [Portada en la nube: Sincronización sin conexión en servicios móviles de Azure] \(Nota: Hola vídeo se encuentra en servicios móviles, pero la sincronización sin conexión funciona de forma similar en aplicaciones móviles de Azure\)

<!-- URLs. -->

[sincronización de datos sin conexión en aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md

[crear una aplicación Android]: app-service-mobile-android-get-started.md

[Portada en la nube: Sincronización sin conexión en servicios móviles de Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

