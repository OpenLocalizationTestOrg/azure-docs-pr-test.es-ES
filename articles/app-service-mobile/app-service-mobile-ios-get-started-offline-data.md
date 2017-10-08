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
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>Habilitación de la sincronización sin conexión con aplicaciones móviles iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Información general
Este tutorial trata la sincronización sin conexión con la característica de aplicaciones móviles Hola de servicio de aplicaciones de Azure para iOS. Con los usuarios finales de sincronización sin conexión pueden interactuar con una aplicación móvil tooview, agregar o modificar los datos, incluso cuando no haya ninguna conexión de red. Los cambios se almacenan en una base de datos local. Cuando el dispositivo de hello vuelve a estar conectado, los cambios de Hola se sincronizan con remoto back-end Hola.

Si se trata de la primera experiencia con aplicaciones móviles, primero debe completar el tutorial Hola [crear una aplicación iOS]. Si no utiliza Hola Descargar proyecto de inicio rápido de servidor, debe agregar proyecto de tooyour de paquetes de extensión de acceso a datos de Hola. Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn más información acerca de la característica de sincronización sin conexión de hello, consulte [sincronización de datos sin conexión en aplicaciones móviles].

## <a name="review-sync"></a>Revise el código de sincronización de cliente hello
proyecto de cliente de Hola que has descargado para hello [crear una aplicación iOS] tutorial ya contiene código que admite la sincronización sin conexión con una base de datos local de bases de datos principal. Esta sección resume lo que ya está incluido en el código del tutorial Hola. Para obtener información conceptual de característica de hello, consulte [sincronización de datos sin conexión en aplicaciones móviles].

Característica de sincronización de datos sin conexión de Hola de aplicaciones móviles, los usuarios finales pueden interactuar con una base de datos local incluso cuando la red de hello es inaccesible. toouse estas características en la aplicación, inicializa el contexto de sincronización de Hola de `MSClient` y hacer referencia a un almacén local. A continuación, hace referencia a la tabla a través de hello **MSSyncTable** interfaz.

En **QSTodoService.m** (Objective-C) o **ToDoTableViewController.swift** (Swift), tenga en cuenta que Hola tipo de miembro de hello **syncTable** es  **MSSyncTable**. La sincronización sin conexión usa esta interfaz de tabla de sincronización en lugar de **MSTable**. Cuando se utiliza una tabla de sincronización, todas las operaciones va almacén local de toohello y se sincronizan sólo con hello remoto back-end con inserción explícita y las operaciones de extracción.

 tooget una tabla de sincronización de tooa de referencia, utilice hello **syncTableWithName** método en `MSClient`. la funcionalidad de sincronización sin conexión tooremove, use **tableWithName** en su lugar.

Para poder realizar cualquier operación de tabla, se debe inicializar el almacén local de Hola. Este es el código relevante hello:

* **Objective-C**. Hola **QSTodoService.init** método:

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **Swift**. Hola **ToDoTableViewController.viewDidLoad** método:

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   Este método crea un almacén local mediante el uso de hello `MSCoreDataStore` proporciona la interfaz que Hola SDK de aplicaciones móviles. Como alternativa, puede proporcionar un almacén local diferente mediante la implementación de hello `MSSyncContextDataSource` protocolo. Además, Hola primer parámetro de **MSSyncContext** es toospecify usa un controlador de conflictos. Porque nos hemos pasado `nil`, obtenemos un controlador de conflictos predeterminado hello, que se produce un error en cualquier conflicto.

Ahora, vamos a realizar la operación de sincronización real de Hola y obtener datos de back-end remoto hello:

* **Objective-C**. `syncData`primero inserta nuevos cambios y, a continuación, se llama **pullData** tooget datos de back-end remoto Hola. A su vez, Hola **pullData** método obtiene datos nuevos que coincide con una consulta:

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
* **SWIFT**:
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

En la versión de Hola Objective-C, en `syncData`, llamamos primero **pushWithCompletion** en el contexto de sincronización de Hola. Este método es un miembro de `MSSyncContext` (y no Hola sincronización propia tabla) porque aplica los cambios realizados en todas las tablas. Solo los registros que se han modificado de alguna manera localmente (a través de operaciones CUD) se envían toohello server. Hola, a continuación, la aplicación auxiliar **pullData** se llama, que llama **MSSyncTable.pullWithQuery** tooretrieve de datos remotos y almacenarlos en la base de datos local de Hola.

En la versión de Swift hello, porque no estaba estrictamente necesaria, la operación de inserción de hello hay ninguna llamada demasiado**pushWithCompletion**. Si hay cambios pendientes en el contexto de sincronización de hello para la tabla de Hola que está realizando una operación de inserción, extracción siempre realiza una inserción en primer lugar. Sin embargo, si tiene más de una tabla de sincronización, es mejor tooensure de inserción de llamada tooexplicitly que todo lo que sea coherente en las tablas relacionadas.

En hello Objective-C y versiones Swift, puede usar hello **pullWithQuery** método toospecify un toofilter consulta Hola registros que desean tooretrieve. En este ejemplo, consulta Hola recupera todos los registros de hello remoto `TodoItem` tabla.

Hola segundo parámetro de **pullWithQuery** es un identificador de la consulta que se usa para *sincronización incremental*. Sincronización incremental recupera únicamente los registros que se han modificado desde la última sincronización hello, uso del registro de hello `UpdatedAt` marca de tiempo (llamado `updatedAt` en hello el almacén local.) Hola identificador de la consulta debe ser una cadena descriptiva que es única para cada consulta lógica en la aplicación. tooopt dejen de estar sincronizados incremental, pasar `nil` como Hola Id. de consulta. Es posible que este enfoque resulte ineficaz, ya que recupera todos los registros en cada operación de extracción.

aplicación de Hello Objective-C se sincroniza al modificar o agregar datos, cuando un usuario realiza gestos de actualización de Hola y de inicio.

aplicación de Swift Hello se sincroniza cuando el usuario de hello realiza gestos de actualización de Hola y al iniciar.

Porque las sincronizaciones siempre que hay datos de aplicación hello modificación (Objective-C) o cada vez que inicia de aplicación hello (Objective-C y Swift), aplicación hello se da por supuesto que el usuario Hola está en línea. En una sección posterior, se actualizará la aplicación hello para que los usuarios pueden editar incluso cuando están sin conexión.

## <a name="review-core-data"></a>Modelo de datos de núcleo de Hola de revisión
Cuando se usa el almacén sin conexión de datos principal de hello, debe definir tablas y campos en el modelo de datos. aplicación de ejemplo de Hola ya incluye un modelo de datos con formato correcto de saludo. En esta sección, se guiará a través de estas tablas tooshow cómo se utilizan.

Abra **QSDataModel.xcdatamodeld**. Cuatro tablas son definidos: Hola tres que usan SDK y uno que se utiliza para tareas de hello elementos propios:
  * MS_TableOperations: Pistas Hola elementos que se deben toobe sincronizado con el servidor de Hola.
  * MS_TableOperationErrors: realiza el seguimiento de los errores que se producen durante la sincronización sin conexión.
  * MS_TableConfig: Pistas Hola la última vez que se actualizó para la última operación de sincronización Hola para todas las operaciones de extracción.
  * TodoItem: Almacena elementos de hello pendientes. las columnas del sistema de Hola **registroen**, **updatedAt**, y **versión** son propiedades del sistema opcional.

> [!NOTE]
> Hola SDK de aplicaciones móviles reserva los nombres de columna que comienzan por "**``**". Utilice este prefijo exclusivamente para las columnas del sistema. En caso contrario, se modifican los nombres de columna cuando se usa remoto back-end Hola.
>
>

Cuando se usa la característica de sincronización sin conexión de hello, definir tres tablas del sistema hello y una tabla de datos de Hola.

### <a name="system-tables"></a>Tablas del sistema

**MS_TableOperations**  

![Atributos de la tabla MS_TableOperations][defining-core-data-tableoperations-entity]

| Atributo | Tipo |
| --- | --- |
| id | Integer 64 |
| itemId | Cadena |
| propiedades | Binary Data |
| table | Cadena |
| tableKind | Integer 16 |


**MS_TableOperationErrors**

 ![Atributos de la tabla MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| Atributo | Tipo |
| --- | --- |
| id |String |
| operationId |Integer 64 |
| propiedades |Binary Data |
| tableKind |Integer 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| Atributo | Tipo |
| --- | --- |
| id |String |
| key |Cadena |
| keyType |Integer 64 |
| table |Cadena |
| value |String |

### <a name="data-table"></a>Tabla de datos

**TodoItem**

| Atributo | Escriba | Nota: |
| --- | --- | --- |
| id | Cadena, marcado obligatorio |Clave principal en almacén remoto |
| complete | Booleano | Campo de tarea pendiente |
| text |string |Campo de tarea pendiente |
| createdAt | Date | (opcional) Se asigna demasiado**registroen** propiedad del sistema |
| updatedAt | Date | (opcional) Se asigna demasiado**updatedAt** propiedad del sistema |
| versión | String | (opcional) Conflictos de toodetect usado, tooversion de mapas |

## <a name="setup-sync"></a>Cambiar el comportamiento de sincronización de Hola de aplicación hello
En esta sección, modificar aplicación hello para que no se sincroniza en el inicio de aplicación o al insertar y actualizar los elementos. Se sincroniza cuando se realice el botón de gesto de hello actualizar.

**Objective-C**:

1. En **QSTodoListViewController.m**, cambiar hello **viewDidLoad** método tooremove Hola llamada demasiado`[self refresh]` final Hola del método hello. Ahora datos hello no se ha sincronizado con el servidor de hello en el inicio de aplicación. En su lugar, se se ha sincronizado con contenido de hello del almacén local de Hola.
2. En **QSTodoService.m**, modifique la definición de Hola de `addItem` para que lo no sincronizará después de que se inserta el elemento de Hola. Quitar hello `self syncData` bloquear y reemplazarlo por siguiente hello:

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. Modificar la definición de Hola de `completeItem` tal y como se mencionó anteriormente. Quite el bloque de Hola para `self syncData` y reemplazarlo por siguiente hello:
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**SWIFT**:

En `viewDidLoad`, en **ToDoTableViewController.swift**, comenta dos líneas de Hola se muestra aquí, toostop sincronización en el inicio de aplicación. En tiempo de Hola de redactar este artículo, aplicación de lista de tareas de Swift hello no actualizar el servicio de hello, cuando un usuario agrega o completa un elemento. Actualiza servicio Hola solo en el inicio de aplicación.

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>Probar la aplicación hello
En esta sección, se conectará toosimulate de dirección URL no válido de tooan un escenario sin conexión. Cuando se agregan elementos de datos, que están mantenían en hello almacenar datos locales de núcleos, pero no están sincronizados con back-end de aplicación móvil de Hola.

1. Cambiar dirección URL de la aplicación móvil de hello en **QSTodoService.m** tooan dirección URL no válida y vuelva a la aplicación hello ejecución:

   **Objective-C**. En QSTodoService.m:
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **Swift**. En ToDoTableViewController.swift:
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. Agregue algunas tareas pendientes. Salga de simulador de hello (o aplicación hello forzosamente cerrar) y, a continuación, reiniciarlo. Compruebe que los cambios se conserven.

3. Ver contenido de Hola de hello remoto **TodoItem** tabla:
   * Para un back-end de Node.js, visite toohello [portal de Azure](https://portal.azure.com/) y, en su aplicación móvil de back-end, haga clic en **tablas fácil** > **TodoItem**.  
   * En un back-end de .NET, use una herramienta SQL, como SQL Server Management Studio, o un cliente REST, como Fiddler o Postman.  

4. Compruebe que dispone de nuevos elementos de hello *no* está sincronizado con el servidor de Hola.

5. Cambio Hola URL atrás toohello corregir uno en **QSTodoService.m**y la aplicación hello vuelva a ejecutar.

6. Realizar gestos de actualización de hello desplazando hacia abajo de la lista de Hola de elementos.  
Se muestra un control giratorio de progreso.

7. Hola de vista **TodoItem** datos de nuevo. elementos de tareas nuevas y modificadas de Hello ahora deben aparecer.

## <a name="summary"></a>Resumen
característica de sincronización sin conexión de hello toosupport, hemos usado hello `MSSyncTable` de la interfaz y se inicializa `MSClient.syncContext` con un almacén local. En este caso, el almacén local de hello era una base de datos de bases de datos principal.

Cuando se utiliza un almacén local de datos principal, debe definir varias tablas con hello [corregir las propiedades del sistema](#review-core-data).

Hola normal crear, leer, actualizar y eliminar operaciones (CRUD) para aplicaciones móviles de trabajo como si la aplicación hello aún está conectado, pero todas las operaciones de Hola se producen en el almacén local de Hola.

Cuando se sincroniza almacén local de hello con servidor hello, hemos usado hello **MSSyncTable.pullWithQuery** método.

## <a name="additional-resources"></a>Recursos adicionales
* [sincronización de datos sin conexión en aplicaciones móviles]
* [Portada en la nube: Sincronización sin conexión en servicios móviles de Azure] \(Hola vídeo está acerca de servicios móviles y funcionamiento de la sincronización de aplicaciones móviles sin conexión de una manera similar.\)

<!-- URLs. -->


[crear una aplicación iOS]: app-service-mobile-ios-get-started.md
[sincronización de datos sin conexión en aplicaciones móviles]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Portada en la nube: Sincronización sin conexión en servicios móviles de Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
