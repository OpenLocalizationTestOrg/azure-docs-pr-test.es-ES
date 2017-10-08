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
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a>Activación de la sincronización sin conexión para una aplicación móvil Cordova
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

Este tutorial presenta la característica de sincronización sin conexión de Hola de aplicaciones móviles de Azure para Cordova. Sincronización sin conexión permite toointeract de los usuarios finales con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red. Los cambios se almacenan en una base de datos local.  Una vez que el dispositivo de hello vuelve a estar conectado, estos cambios se sincronizan con el servicio remoto hello.

Este tutorial se basa en hello solución de inicio rápido de Cordova para aplicaciones móviles que crea al completar Hola tutorial [inicio rápido de Apache Cordova]. En este tutorial, va a actualizar Hola quickstart solución tooadd características sin conexión de las aplicaciones móviles de Azure.  También se resalte código de sin conexión específicas de hello en la aplicación hello.

toolearn más información acerca de la característica de sincronización sin conexión de hello, vea el tema de hello [sincronización de datos sin conexión en aplicaciones móviles de Azure]. Para obtener detalles de uso de la API, vea hello [documentación de la API](https://azure.github.io/azure-mobile-apps-js-client).

## <a name="add-offline-sync-toohello-quickstart-solution"></a>Agregar la solución de inicio rápido de toohello de sincronización sin conexión
se debe agregar código de sincronización sin conexión de Hello toohello aplicación. Sincronización sin conexión requiere el complemento de almacenamiento de sqlite cordova hello, que automáticamente se agrega tooyour aplicación al complemento de aplicaciones móviles de Azure Hola se incluye en el proyecto de Hola. proyecto de inicio rápido de Hello incluye los dos de estos complementos.

1. En el Explorador de soluciones de Visual Studio, abra index.js y reemplace Hola después de código

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    por este otro:

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. A continuación, reemplace Hola siguiente código:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    por este otro:

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

    inicializar el almacén local de Hola Hola adiciones de código anterior y definir una tabla local que coincida con los valores de columna de hello utilizados en Azure back-end. (No es necesario tooinclude todos los valores de columna en este código.)  Hola `version` campo se mantiene Hola móviles servidor back-end y se utiliza para la resolución de conflictos.

    Obtiene un contexto de sincronización de toohello de referencia mediante una llamada a **getSyncContext**. Hello contexto de sincronización le ayuda a mantener las relaciones entre tablas de seguimiento e insertar los cambios en todas las tablas de una aplicación cliente modifica cuando `.push()` se llama.

3. Actualice la URL de aplicación de la aplicación móvil de tooyour de hello aplicación dirección URL.

4. Ahora, reemplace este código:

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    por este otro:

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

    Hello anterior código inicializa el contexto de sincronización de hello y, a continuación, llama tooget getSyncTable (en lugar de getTable) una tabla de referencia toohello local.

    Este código usa Hola base de datos local para todos los crear, leer, actualizar y eliminar operaciones (CRUD) de la tabla.

    En este ejemplo se realiza un control de errores simple en los conflictos de sincronización. Una aplicación real controlaría Hola varios errores como las condiciones de red, servidor entra en conflicto y otros. Para obtener ejemplos de código, vea hello [ejemplo de sincronización sin conexión].

5. A continuación, agregue esta sincronización real de función tooperform Hola.

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    Decidir cuándo toopush cambia back-end de aplicación móvil de toohello mediante una llamada a **syncContext.push()**. Por ejemplo, podría llamar a **syncBackend** en un botón de sincronización de tooa relacionados del controlador de eventos de botón.

## <a name="offline-sync-considerations"></a>Consideraciones sobre la sincronización sin conexión

En el ejemplo de Hola Hola **inserción** método **syncContext** solo se llama en el inicio de la aplicación en función de devolución de llamada de hello para el inicio de sesión.  En una aplicación del mundo real, también puede realizar esta funcionalidad de sincronización de forma manual o cuando cambia el estado de la red de Hola.

Cuando se ejecuta una extracción en una tabla que tiene pendiente actualizaciones locales realiza un seguimiento mediante el contexto de hello, que extraen operación automáticamente desencadenadores una inserción. Al actualizar, agregar y completar los elementos en este ejemplo, puede omitir Hola explícita **inserción** llamar, dado que puede ser redundante.

En el código de hello proporcionada, se consultan todos los registros de la tabla todoItem remoto de hello, pero también es posible toofilter registros pasando un identificador de la consulta y una consulta demasiado**inserción**. Para obtener más información, vea la sección de hello *sincronización Incremental* en [sincronización de datos sin conexión en aplicaciones móviles de Azure].

## <a name="optional-disable-authentication"></a>(Opcional) Deshabilitación de la autenticación

Si no desea tooset la autenticación antes de probar la sincronización sin conexión, comente la función de devolución de llamada de hello para el inicio de sesión, pero deje el código de hello dentro de la función de devolución de llamada de hello sin comentarios.  Después de la creación de comentarios de las líneas de inicio de sesión de hello, código de hello sigue:

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

Ahora, Hola aplicación se sincronice con hello Azure back-end cuando se ejecuta la aplicación hello.

## <a name="run-hello-client-app"></a>Ejecutar la aplicación de cliente hello
Con ahora habilitada la sincronización sin conexión, puede ejecutar aplicaciones de cliente de Hola de al menos una vez en cada plataforma para rellenar la base de datos de almacén local de Hola. Más adelante, simular un escenario sin conexión y modificar datos de hello en el almacén local de hello mientras está sin conexión la aplicación hello.

## <a name="optional-test-hello-sync-behavior"></a>(Opcional) Probar el comportamiento de sincronización de Hola
En esta sección, se modifique Hola cliente proyecto toosimulate un escenario sin conexión mediante el uso de una dirección URL de aplicación no válido para el back-end. Al agregar o cambiar los elementos de datos, estos cambios se mantienen en el almacén local, pero no están sincronizados toohello almacén de datos de back-end hasta que se haya restablecido la conexión de Hola.

1. Hola el Explorador de soluciones, abrir archivo de proyecto de hello index.js y cambie toopoint de dirección URL de aplicación Hola a una dirección URL no válida, como el siguiente código de hello:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. En index.html, actualizar Hola CSP `<meta>` elemento con Hola la misma dirección URL no válido.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. Crear y ejecutar la aplicación de cliente de hello y observe que una excepción se registra en la consola de hello cuando la aplicación hello intenta sincronizar con back-end de hello después de iniciar sesión. Los elementos nuevos que agregue solo existen en almacén local de hello hasta que se insertan back-end de toohello móvil. aplicación de cliente de Hello se comporta como si estuviera conectada toohello back-end.

4. Cierre la aplicación hello y reiníciela tooverify que elementos nuevos de Hola que creó están almacén local toohello persistente.

5. (Opcional) Use Visual Studio tooview su toosee de tabla de base de datos de SQL Azure Hola datos en la base de datos de back-end de hello no han cambiado.

    En Visual Studio, abra el **Explorador de servidores**. Navegar por la base de datos de tooyour en **Azure**->**bases de datos SQL**. Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**. Ahora puede examinar la tabla de base de datos SQL tooyour y su contenido.

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a>(Opcional) Prueba Hola reconexión tooyour móviles back-end

En esta sección, se vuelve a conectar hello toohello móviles backend de la aplicación, que simula la aplicación hello que vuelve al estado en línea. Cuando inicie sesión, los datos son móviles tooyour sincronizados back-end.

1. Vuelva a abrir index.js y restaurar la dirección URL de la aplicación hello.
2. Vuelva a abrir index.html y corrija la dirección URL de la aplicación Hola Hola CSP `<meta>` elemento.
3. Volver a generar y ejecutar la aplicación de cliente de hello. aplicación Hello intenta toosync con back-end de aplicación móvil de hello después de iniciar sesión. Compruebe que ninguna excepción se registra en la consola de depuración de Hola.
4. (Opcional) Hola de vista actualiza datos mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler. Se ha sincronizado aviso Hola datos entre la base de datos de back-end de Hola y el almacén local de Hola.

    Tenga en cuenta datos Hola se ha sincronizado entre la base de datos de Hola y el almacén local de Hola y contiene elementos de hello que agregó mientras la aplicación se desconectó.

## <a name="additional-resources"></a>Recursos adicionales
* [sincronización de datos sin conexión en aplicaciones móviles de Azure]
* [Visual Studio Tools para Apache Cordova]

## <a name="next-steps"></a>Pasos siguientes
* Revisión de características de sincronización sin conexión, como la resolución de conflictos en hello más avanzadas [ejemplo de sincronización sin conexión]
* Revise la sincronización sin conexión de hello referencia de API en hello [documentación de la API](https://azure.github.io/azure-mobile-apps-js-client).

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
