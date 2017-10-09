---
title: "aaaService tejido de copia de seguridad y restauración | Documentos de Microsoft"
description: "Documentación conceptual para la copia de seguridad y la restauración de Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: subramar,jessebenson
ms.assetid: 91ea6ca4-cc2a-4155-9823-dcbd0b996349
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: mcoskun
ms.openlocfilehash: e502b59c84999c3fe825167383f00a5ebd70c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a>Copia de seguridad y restauración de Reliable Services y Reliable Actors
Azure Service Fabric es una plataforma de alta disponibilidad que se replica estado hello toomaintain de varios nodos esta alta disponibilidad.  Por lo tanto, incluso si se produce un error en un nodo del clúster de hello, servicios de hello continúan toobe disponible. Aunque esta redundancia integrada proporcionada por la plataforma de hello puede ser suficiente para algunos, en algunos casos es deseable para hello servicio tooback los datos (tooan almacén externo).

> [!NOTE]
> Es fundamental toobackup y restaure los datos (y la prueba que funciona según lo previsto) por lo que es posible recuperarse de los escenarios de pérdida de datos.
> 
> 

Por ejemplo, un servicio que desee tooback datos en orden tooprotect de hello los escenarios siguientes:

- En caso de hello de pérdida permanente de Hola de todo un clúster de Service Fabric.
- Pérdida permanente de una mayoría de las réplicas de Hola de una partición de servicio
- Errores administrativos mediante el cual Hola estado accidentalmente obtiene eliminado o dañado. Por ejemplo, esto puede ocurrir si un administrador con suficientes privilegios erróneamente elimina el servicio de Hola.
- Errores en el servicio de Hola que provocan daños en los datos. Por ejemplo, esto puede ocurrir cuando una actualización de código de servicio comienza a escribir datos defectuoso tooa colección confiable. En tal caso, ambos Hola código y datos de hello pueden tener toobe revertir tooan estado anterior.
- Procesamiento de datos sin conexión. Podría ser conveniente toohave procesamiento sin conexión de datos de business intelligence que se produce por separado del servicio de Hola que genera datos de Hola.

la característica de copia de seguridad y restauración de Hello permite servicios integrados en hello confiable API de servicios toocreate y restaurar las copias de seguridad. Hello las API de copia de seguridad proporcionadas por plataforma de hello permiten backup(s) del estado de la partición de servicio, sin bloqueo operaciones de lectura o escritura. Hola restauración que API permiten toobe de estado de la partición de servicio restaurado a partir de una copia de seguridad seleccionado.

## <a name="types-of-backup"></a>Tipos de copia de seguridad
Hay dos opciones de copia de seguridad: completa e incremental.
Una copia de seguridad completa es una copia de seguridad que contiene todos los Hola datos necesarios toorecreate Hola estado de réplica de hello: puntos de control y todos los registros.
Porque tiene puntos de control de Hola y de registro de hello, se puede restaurar una copia de seguridad completa por sí mismo.

problema de Hello con copias de seguridad completas se produce cuando los puntos de control de hello son grandes.
Por ejemplo, una réplica que tiene 16 GB de estado tendrá puntos de comprobación que suman aproximadamente too16 GB.
Si tiene un objetivo de punto de recuperación de cinco minutos, la réplica de hello necesita toobe copia de seguridad cada cinco minutos.
Cada vez que se hace la copia debe toocopy 16 GB de puntos de control además too50 MB (configurables usando `CheckpointThresholdInMB`) correspondientes a los registros.

![Ejemplo de copia de seguridad completa.](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

problema de Hello solución toothis es copias de seguridad incrementales, que copia de seguridad solo contiene entradas de registro de hello cambiado desde la última copia de seguridad de Hola.

![Ejemplo de copia de seguridad incremental.](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

Dado que copias de seguridad incrementales son los únicos cambios desde Hola última copia de seguridad (no se incluyen los puntos de control de hello), suelen toobe más rápido pero no se pueden restaurar por sí solas.
toorestore una copia de seguridad incremental, la cadena de copia de seguridad completa de hello es necesario.
Una cadena de copia de seguridad empieza por una copia de seguridad completa a la que sigue un número contiguo de copias de seguridad incrementales.

## <a name="backup-reliable-services"></a>Copias de seguridad de Reliable Services
autor del servicio Hello tenga control total sobre cuándo las copias de seguridad de toomake y donde se almacenarán las copias de seguridad.

toostart una copia de seguridad, el servicio de hello necesita tooinvoke Hola heredarse miembro función `BackupAsync`.  
Las copias de seguridad pueden realizarse únicamente desde las réplicas principales y requieren toobe de estado de escritura concedido.

Tal y como se muestra a continuación, `BackupAsync` toma una `BackupDescription` objeto, donde uno puede especificar una copia de seguridad completa o incremental, así como una función de devolución de llamada, `Func<< BackupInfo, CancellationToken, Task<bool>>>` que se invoca cuando la carpeta de copia de seguridad de Hola se ha creado localmente y está listo toobe ha sacado toosome almacenamiento externo.

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

Tootake de solicitud de una copia de seguridad incremental se puede producir un `FabricMissingFullBackupException`. Esta excepción indica que se está realizando uno de hello siguientes cosas:

- réplica de Hello nunca ha tomado una copia de seguridad completa porque se ha convertido en principal,
- algunos de hello las entradas de registro porque se ha truncado la última copia de seguridad de Hola o
- réplica pasado hello `MaxAccumulatedBackupLogSizeInMB` límite.

Los usuarios pueden aumentar la probabilidad de Hola de ser capaz de toodo copias de seguridad incrementales configurando `MinLogSizeInMB` o `TruncationThresholdFactor`.
Tenga en cuenta que estos valores si aumenta Hola por el uso del disco de réplica.
Para obtener más información, consulte el artículo de [configuración de Reliable Services](service-fabric-reliable-services-configuration.md).

`BackupInfo`Proporciona información relativa a la copia de seguridad de hello, incluida la ubicación de Hola de carpeta Hola donde hello en tiempo de ejecución guarda la copia de seguridad de hello (`BackupInfo.Directory`). función de devolución de llamada de Hello puede mover hello `BackupInfo.Directory` tooan almacén externo u otra ubicación.  Esta función también devuelve un valor booleano que indica si se trataba de ubicación de destino de tooits de toosuccessfully puede mover Hola carpeta de copia de seguridad.

Hello código siguiente se muestra cómo Hola `BackupCallbackAsync` método puede ser utilizado tooupload Hola copia de seguridad tooAzure almacenamiento:

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

En el ejemplo de Hola precedente, `ExternalBackupStore` es la clase de ejemplo de Hola es toointerface usado con el almacenamiento de blobs de Azure, y `UploadBackupFolderAsync` es método hello que comprime carpeta hello y lo coloca en el almacén de blobs de Azure Hola.

Observe lo siguiente:

  - Solo puede haber una operación de copia de seguridad en proceso por réplica en cualquier momento dado. Más de un `BackupAsync` llama a la vez, se producirá `FabricBackupInProgressException` tooone de copias de seguridad de toolimit en proceso.
  - Si una réplica conmuta por error mientras se realiza una copia de seguridad, copia de seguridad de hello puede no haberse completado. Por lo tanto, una vez finalizada la conmutación por error de hello, es copia de seguridad del servicio de hello responsabilidad toorestart Hola invocando `BackupAsync` según sea necesario.

## <a name="restore-reliable-services"></a>Restauración de Reliable Services
En general, los casos de Hola que tal vez tenga tooperform una operación de restauración se dividen en una de estas categorías:

  - servicio de Hello particionar datos perdidos. Por ejemplo, disco de Hola para dos de los tres réplicas de una partición (incluida la réplica principal de hello) obtiene dañado o se borre. nuevo elemento principal Hola necesite toorestore datos desde una copia de seguridad.
  - servicio completo de Hola se pierde. Por ejemplo, un administrador quita todo el servicio hello y, por tanto, el servicio de Hola y los datos de Hola necesitan toobe restaurar.
  - servicio de Hello replica datos de la aplicación está dañado (por ejemplo, debido a un error de la aplicación). En este caso, servicio de hello tiene toobe actualizado o revertida tooremove Hola causa de daños de Hola y datos de no dañar tiene toobe restaurar.

Aunque muchos enfoques son posibles, se ofrecen algunos ejemplos sobre el uso de `RestoreAsync` toorecover de Hola por encima de los escenarios.

## <a name="partition-data-loss-in-reliable-services"></a>Pérdida de datos de la partición en Reliable Services
En este caso, en tiempo de ejecución de hello automáticamente se detecta la pérdida de datos de hello e invocar hello `OnDataLossAsync` API.

el autor del servicio de Hello tiene hello tooperform después toorecover:

  - Invalide el método de clase base virtual hello `OnDataLossAsync`.
  - Buscar Hola copia de seguridad más reciente en la ubicación externa Hola que contiene copias de seguridad del servicio de Hola.
  - Descargar la última copia de seguridad de hello (y descomprimir copia de seguridad de hello en la carpeta de copia de seguridad de hello si estaba comprimido).
  - Hola `OnDataLossAsync` método proporciona un `RestoreContext`. Llamar a hello `RestoreAsync` API en hello proporciona `RestoreContext`.
  - Devuelve true si la restauración de hello tuvo éxito.

Aquí te mostramos un ejemplo de implementación de hello `OnDataLossAsync` método:

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

`RestoreDescription`pasa toohello `RestoreContext.RestoreAsync` llamada contiene un miembro denominado `BackupFolderPath`.
Al restaurar una copia de seguridad completa solo esto `BackupFolderPath` debe establecerse toohello ruta de acceso local de la carpeta de Hola que contiene la copia de seguridad completa.
Al restaurar una copia de seguridad completa y un número de copias de seguridad incrementales, `BackupFolderPath` debe establecerse toohello ruta de acceso local de carpeta de Hola que no solo contiene la copia de seguridad completa de hello, sino también todos los Hola copias de seguridad incrementales.
`RestoreAsync`puede iniciar la llamada `FabricMissingFullBackupException` si hello `BackupFolderPath` proporcionado no contiene una copia de seguridad completa.
También puede iniciar una excepción `ArgumentException` si `BackupFolderPath` tiene una cadena de copias de seguridad incrementales rota.
Por ejemplo, si contiene Hola copia de seguridad completa, en primer lugar Hola incremental y Hola tercera copia de seguridad incremental pero ninguna copia de seguridad incremental de segundo de Hola.

> [!NOTE]
> Hola RestorePolicy se establece tooSafe de forma predeterminada.  Esto significa que hello `RestoreAsync` API se producirá un error con ArgumentException si detecta esta carpeta de copia de seguridad de hello contiene un estado que está en estado toohello igual o anterior a contenidos en esta réplica.  `RestorePolicy.Force`puede ser usado tooskip esta comprobación de seguridad. Este objeto se especifica como parte de `RestoreDescription`.
> 

## <a name="deleted-or-lost-service"></a>Eliminación o pérdida del servicio
Si se quita un servicio, primero debe volver a crear el servicio de Hola antes de pueden restaurar datos de Hola.  Es importante toocreate Hola servicio con hello misma configuración, por ejemplo, partición de esquema, por lo que Hola datos puede restaurarse sin problemas.  Una vez que el servicio de hello está en funcionamiento, Hola datos toorestore de API (`OnDataLossAsync` anteriormente) tiene toobe invocar en cada partición de este servicio. Esta operación puede llevarse a cabo utilizando `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` en todas las particiones.  

Desde este punto de implementación es Hola igual que Hola por encima del escenario. Cada partición debe toorestore hello más reciente relevante copia de seguridad del almacén externo Hola. Una advertencia es esa partición Hola que identificador puede ahora cambiaron, puesto que en tiempo de ejecución de hello crea identificadores de partición dinámicamente. Por lo tanto, servicio de hello necesita información de partición apropiada de hello toostore y servicio nombre tooidentify Hola correcto última copia de seguridad toorestore de para cada partición.

> [!NOTE]
> No se recomienda toouse `FabricClient.ServiceManager.InvokeDataLossAsync` en cada partición toorestore Hola servicio completo, ya que puede dañar el estado del clúster.
> 

## <a name="replication-of-corrupt-application-data"></a>Replicación de datos de aplicación dañados
Si la actualización de la aplicación hello recién implementado tiene un error, que puede producir daños de datos. Por ejemplo, una actualización de la aplicación puede iniciar tooupdate cada registro del número de teléfono en un diccionario confiable con un código de área no válido.  En este caso, los números de teléfono no válido de Hola se replicarán desde Service Fabric no es consciente de la naturaleza de Hola de datos de Hola que se va a almacenar.

Hello lo primero toodo después de detectar tal un error notoria que provoca daños en los datos que es toofreeze Hola servicio Hola a nivel de aplicación y, si es posible, actualice versión toohello Hola del código de aplicación que no tiene errores de Hola.  Sin embargo, incluso después de corregir el código del servicio de hello, datos de hello todavía pueden estar dañados y, por tanto, los datos pueden necesitar que toobe restaurar.  En tales casos, no puede ser suficiente toorestore Hola última copia de seguridad, puesto que las copias de seguridad más recientes de hello también pueden estar dañados.  Por lo tanto, tienen toofind Hola última copia de seguridad realizada antes de que se ha dañado datos Hola.

Si no estás seguro de que las copias de seguridad están dañados, podría implementar un nuevo clúster de Service Fabric y restaurar copias de seguridad de Hola de las particiones afectadas como Hola anteriormente "Deleted o servicio pierde" escenario.  Para cada partición, iniciar Restaurar copias de seguridad de Hola de hello más reciente toohello menos. Una vez que encuentre una copia de seguridad no tiene daños de hello, mover o eliminar todas las copias de seguridad de esta partición que estaban más recientes (que esa copia de seguridad). Repita este proceso para cada partición. Ahora, cuando `OnDataLossAsync` se llama en partición de hello en el clúster de producción de hello, última copia de seguridad de hello encontradas en hello externo almacén será Hola uno seleccionado por Hola por encima del proceso.

Ahora, los pasos Hola Hola "Deleted o servicio pierde" sección puede ser usar estado de hello toorestore del estado de toohello del servicio de hello antes de código con errores de hello dañado estado Hola.

Observe lo siguiente:

  - Cuando se restaura, existe es probable que Hola copia de seguridad que se va a restaurar es anterior a estado de Hola de partición de Hola antes de que se han perdido datos Hola. Por este motivo, debe restaurar solo como una última toorecover recurso tantos datos como sea posible.
  - Hola de cadena que representa la ruta de acceso de carpeta de copia de seguridad de Hola y Hola rutas de acceso de archivos dentro de la carpeta de copia de seguridad de hello pueden ser mayores que 255 caracteres, dependiendo de la ruta de acceso de hello FabricDataRoot y longitud del nombre del tipo de aplicación. Esto puede causar algunos métodos. NET, como `Directory.Move`, toothrow hello `PathTooLongException` excepción. Una solución es toodirectly llamar a las API de kernel32, como `CopyFile`.

## <a name="backup-and-restore-reliable-actors"></a>Copia de seguridad y restauración de Reliable Actors


El marco de Reliable Actors está basado en Reliable Services. Hola ActorService que hospeda hello actor(s) es un servicio confiable con estado. Por lo tanto, todas las copias de seguridad de Hola y funcionalidad de restauración disponible en servicios de confianza también es actores tooReliable disponibles (excepto los comportamientos que son específicos de proveedor de estado). Puesto que las copias de seguridad se realizan por partición, se llevará a cabo una copia de seguridad de los estados para todos los actores de esa partición. La restauración es similar y se realizará por partición. tooperform copia de seguridad/restauración, el propietario del servicio Hola debe crear una clase de servicio de actor personalizada que deriva de la clase ActorService y, a continuación, backup/restore tooReliable similar servicios tal como se describió en las secciones anteriores.

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo)
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Cuando se crea una clase de servicio de actor personalizado, debe tooregister es así cuando se registra el actor Hola.

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

proveedor de estado predeterminado de Hola de Reliable Actors es `KvsActorStateProvider`. La copia de seguridad incremental no está habilitada de manera predeterminada para `KvsActorStateProvider`. Puede habilitar la copia de seguridad incremental mediante la creación de `KvsActorStateProvider` con hello adecuados en su constructor y, a continuación, pasándole tooActorService constructor como se muestra en el siguiente fragmento de código:

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo, null, null, new KvsActorStateProvider(true)) // Enable incremental backup
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Después de que se ha habilitado la copia de seguridad incremental, realizar una copia de seguridad incremental se puede producir un FabricMissingFullBackupException para uno de los siguientes motivos y deberá tootake una copia de seguridad completa antes de realizar backup(s) incremental:

  - réplica de Hello nunca ha tomado una copia de seguridad completa porque se convirtió en principal.
  - Algunas de las entradas del registro de hello se truncaron desde que se realizó la última copia de seguridad.

Cuando se habilita la copia de seguridad incremental, `KvsActorStateProvider` no usa el búfer circular toomanage su registro registra y periódicamente lo trunca. Si no se realiza ninguna copia de seguridad por usuario durante un período de 45 minutos, el sistema de Hola trunca automáticamente entradas del registro de hello. Este intervalo se puede configurar mediante la especificación de `logTrunctationIntervalInMinutes` en `KvsActorStateProvider` constructor (habilitar la copia de seguridad incremental de toowhen similar). También pueden obtener truncados entradas del registro de Hello si la réplica principal necesita toobuild otra réplica mediante el envío de todos sus datos.

Al realizar la restauración a partir de una cadena de copia de seguridad, los servicios de tooReliable similares, hello BackupFolderPath debe contener subdirectorios con un subdirectorio que contiene copias de seguridad completa y otros subdirectorios que contienen backup(s) incremental. API de restauración de Hello producirá FabricException con mensaje de error adecuado si se produce un error de validación de la cadena de copia de seguridad de Hola. 

> [!NOTE]
> `KvsActorStateProvider`actualmente se omite la opción de hello RestorePolicy.Safe. La compatibilidad con esta característica está pensada para un próximo lanzamiento.
> 

## <a name="testing-backup-and-restore"></a>Prueba de la copia de seguridad y la restauración
Es importante tooensure que se hace copia datos críticos y se pueden restaurar desde. Esto puede hacerse mediante la invocación de hello `Start-ServiceFabricPartitionDataLoss` cmdlet de PowerShell que puede inducir la pérdida de datos en una partición determinada tootest si datos Hola de copia de seguridad y restauración la funcionalidad para su servicio está funcionando según lo previsto.  También es posible tooprogrammatically invocar la pérdida de datos y restaurar a partir de ese evento así.

> [!NOTE]
> Puede encontrar una implementación de ejemplo de copia de seguridad y restaurar la funcionalidad en hello aplicación de referencia Web en GitHub. Mire hello `Inventory.Service` service para obtener más detalles.
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a>Bajo el paraguas de hello: más detalles sobre copia de seguridad y restauración
A continuación se proporcionan más detalles sobre la copia de seguridad y la restauración.

### <a name="backup"></a>Backup
Hola, Administrador de estado confiable proporciona Hola capacidad toocreate copias de seguridad coherentes sin bloquear cualquiera leen o las operaciones de escritura. toodo por lo tanto, utiliza un mecanismo de persistencia de punto de comprobación y de registro.  Hola, Administrador de estado confiable toma los puntos de control (ligeras) aproximadas en determinadas presión de toorelieve puntos de registro de transacciones de Hola y mejorar los tiempos de recuperación.  Cuando `BackupAsync` se denomina hello confiable Administrador de estado indica toocopy de todos los objetos confiable su últimas checkpoint archivos tooa copia de seguridad carpeta local.  A continuación, Hola el Administrador de estado confiable copia todas las entradas del registro, a partir de Hola "start puntero" toohello última entrada de registro en carpeta de copia de seguridad de Hola.  Dado que todas las entradas de registro de hello una entrada de registro más reciente de toohello se incluyen en la copia de seguridad de Hola y Hola el Administrador de estado confiable conserva el registro de escritura anticipada, Hola el Administrador de estado confiable garantiza que todas las transacciones que se confirman (`CommitAsync` ha devuelto correctamente) se incluyen en la copia de seguridad de Hola.

Cualquier transacción que confirma después de `BackupAsync` se ha llamado puede o no puede estar en la copia de seguridad de Hola.  Una vez que se ha rellenado la carpeta de copia de seguridad local de Hola por plataforma de hello (es decir, copia de seguridad local se completa en tiempo de ejecución de hello), se invoca la devolución de llamada copia de seguridad del servicio de Hola.  Esta devolución de llamada es responsable de transferir tooan de ubicación externa como almacenamiento de Azure para la carpeta de copia de seguridad Hola.

### <a name="restore"></a>Restauración
Hola, Administrador de estado confiable proporciona Hola capacidad toorestore desde una copia de seguridad mediante hello `RestoreAsync` API.  
Hola `RestoreAsync` método `RestoreContext` puede llamar solo dentro de hello `OnDataLossAsync` método.
Hola bool devuelto por `OnDataLossAsync` indica si el servicio de hello restaura su estado desde un origen externo.
Si hello `OnDataLossAsync` devuelve true, Service Fabric se volverá a generar todas las demás réplicas del servidor principal. Service Fabric garantiza que las réplicas que van a recibir `OnDataLossAsync` llame al primer rol principal de transición toohello pero no tienen permisos de lectura estado o estado de escritura.
Esto supone que, en el caso de los implementadores de StatefulService, no se va a llamar a `RunAsync` hasta que `OnDataLossAsync` se complete correctamente.
A continuación, `OnDataLossAsync` se invocará en la nueva réplica principal de Hola.
Hasta que un servicio de esta API completa correctamente (devolviendo true o false) y finaliza la reconfiguración de hello relevante, Hola API mantener que se llamará a uno en uno.

`RestoreAsync`en primer lugar se quita todo el estado existente en la réplica principal de Hola que se llamó en.  
A continuación, Hola confiable Administrador de Estados crea todos los objetos confiable Hola que existen en la carpeta de copia de seguridad de Hola.  
A continuación, objetos de confianza de hello son toorestore siguiendo las instrucciones de sus puntos de control en la carpeta de copia de seguridad de Hola.  
Por último, Hola confiable State Manager recupera su propio estado de los registros de hello en la carpeta de copia de seguridad de Hola y realiza la recuperación.  
Como parte del proceso de recuperación de hello, las operaciones desde Hola "punto de partida" que tienen entradas de registro de confirmación en la carpeta de copia de seguridad de hello son objetos confiable de toohello reproducido.  
Este paso garantiza que Hola recuperada del estado es coherente.

## <a name="next-steps"></a>Pasos siguientes
  - [Colecciones confiables](service-fabric-work-with-reliable-collections.md)
  - [Introducción a Reliable Services de Service Fabric de Microsoft Azure](service-fabric-reliable-services-quick-start.md)
  - [Notificaciones de Reliable Services](service-fabric-reliable-services-notifications.md)
  - [Configuración de Reliable Services](service-fabric-reliable-services-configuration.md)
  - [Referencia para desarrolladores de colecciones confiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

