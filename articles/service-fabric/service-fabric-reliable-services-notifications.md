---
title: notificaciones de servicios de aaaReliable | Documentos de Microsoft
description: "Documentación conceptual sobre las notificaciones de servicio de Reliable Services de Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a>Notificaciones de Reliable Services
Las notificaciones permiten a los clientes los cambios de hello tootrack que van a ser objeto de tooan que estén interesados en. Existen dos tipos de objeto que admiten notificaciones: *Reliable State Manager* y *Reliable Dictionary*.

Algunas causas habituales del uso de notificaciones son:

* Edificio materializa vistas, como los índices secundarios o agrega vistas filtradas de estado de la réplica de Hola. Un ejemplo es un índice ordenado de todas las claves en un diccionario Reliable Dictionary.
* Datos de supervisión envío, como el número de Hola de los usuarios agregados en hello última hora.

Las notificaciones se desencadenan como parte de la aplicación de operaciones. Por ese motivo, se deben controlar las notificaciones lo más rápido posible y los eventos sincrónicos no deben incluir operaciones costosas.

## <a name="reliable-state-manager-notifications"></a>Notificaciones de Reliable State Manager
Administrador de estado de confianza proporciona notificaciones para hello siguientes eventos:

* Transacción
  * Confirmación
* Administrador de estado
  * Recompilación
  * Adición de un estado Reliable State
  * Eliminación de un estado Reliable State

Administrador de estado de confianza realiza un seguimiento de las transacciones en proceso actuales de Hola. Hola único cambio en un estado de transacción que hace que un toobe notificación activada es una transacción se confirma.

Reliable State Manager mantiene una colección de estados Reliable State, como Reliable Dictionary y Reliable Queue. Las notificaciones cuando cambia esta colección desencadena el Administrador de estado de confianza: se agrega o quita un estado confiable, o se vuelve a generar la colección completa de Hola.
Hola colección confiable Administrador de estado se vuelve a generar en tres casos:

* Recuperación: Cuando se inicia una réplica, recupera su estado anterior desde el disco de Hola. Al final de Hola de recuperación, usa **NotifyStateManagerChangedEventArgs** toofire un evento que contiene el conjunto de Hola de Estados confiables recuperados.
* Copia completa: antes de que una réplica puede unirse a conjunto de configuración de hello, tiene toobe integrada. A veces, esto requiere una copia completa del estado del Administrador de confianza estado de hello réplica principal toobe toohello aplicado inactivo réplica secundaria. El Administrador de estado de confianza en los usos de la réplica secundaria de hello **NotifyStateManagerChangedEventArgs** toofire un evento que contiene el conjunto de Hola de Estados confiables que adquirió de réplica principal de Hola.
* Restore: En los escenarios de recuperación de desastres, estado de la réplica de Hola se puede restaurar desde una copia de seguridad a través de **RestoreAsync**. En tales casos, se utiliza el Administrador de estado confiable en la réplica principal de hello **NotifyStateManagerChangedEventArgs** toofire un evento que contiene el conjunto de Hola de Estados confiables que se restauran desde la copia de seguridad de Hola.

tooregister para las notificaciones de la transacción o las notificaciones del Administrador de estado, deberá tooregister con hello **TransactionChanged** o **StateManagerChanged** eventos en el Administrador de estado confiable. Un lugar común tooregister con estos controladores de eventos es el constructor de Hola de su servicio con estado. Al registrar en el constructor de hello, no pierde cualquier notificación que se debe a un cambio durante la duración de Hola de **IReliableStateManager**.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

Hola **TransactionChanged** utiliza el controlador de eventos **NotifyTransactionChangedEventArgs** tooprovide detalles acerca del evento Hola. Contiene propiedad de acción de hello (por ejemplo, **NotifyTransactionChangedAction.Commit**) que especifica el tipo de saludo de cambio. También contiene la propiedad de la transacción de Hola que proporciona una transacción de toohello de referencia que ha cambiado.

> [!NOTE]
> En la actualidad, **TransactionChanged** se generan eventos solo si se confirma la transacción de Hola. Hello acción equivale a continuación, demasiado**NotifyTransactionChangedAction.Commit**. Pero en hello futuras, se podrían producir eventos para otros tipos de cambios de estado de transacción. Se recomienda comprobar acción de hello y procesar eventos de hello solo si es uno que se espera.
> 
> 

A continuación, se ofrece un ejemplo de controlador de eventos **TransactionChanged** .

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

Hola **StateManagerChanged** utiliza el controlador de eventos **NotifyStateManagerChangedEventArgs** tooprovide detalles acerca del evento Hola.
**NotifyStateManagerChangedEventArgs** tiene dos subclases: **NotifyStateManagerRebuildEventArgs** y **NotifyStateManagerSingleEntityChangedEventArgs**.
Usar propiedades de acción de hello en **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** subclase correcta de toohello:

* **NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** y **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**

A continuación, se ofrece un ejemplo de controlador de notificación **StateManagerChanged** .

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a>Notificaciones de Reliable Dictionary
Diccionario confiable proporciona notificaciones para hello siguientes eventos:

* Rebuild: se llama cuando **ReliableDictionary** ha recuperado su estado de una copia de seguridad o un estado local copiado o recuperado.
* Borrar: Se le llama cuando Hola estado de **ReliableDictionary** se ha borrado a través de hello **ClearAsync** método.
* Agregar: se le llama cuando se ha agregado un elemento demasiado**ReliableDictionary**.
* Update: se llama cuando se ha actualizado un elemento de **IReliableDictionary** .
* Remove: se llama cuando se ha eliminado un elemento de **IReliableDictionary** .

las notificaciones de diccionario confiable tooget, necesita tooregister con hello **DictionaryChanged** controlador de eventos en **IReliableDictionary**. Un lugar común tooregister con estos controladores de eventos se encuentra en hello **ReliableStateManager.StateManagerChanged** agregar la notificación.
Registrar cuándo **IReliableDictionary** se agrega demasiado**IReliableStateManager** garantiza que no se pierda ninguna notificación.

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> **ProcessStateManagerSingleEntityNotification** es el método de ejemplo de Hola ese Hola anterior **OnStateManagerChangedHandler** llamadas de ejemplo.
> 
> 

código anterior Hello establece hello **IReliableNotificationAsyncCallback** interfaz, junto con **DictionaryChanged**. Porque **NotifyDictionaryRebuildEventArgs** contiene un **IAsyncEnumerable** interfaz--toobe enumerar de forma asincrónica, es necesario que las notificaciones de regeneración se activan a través de  **RebuildNotificationAsyncCallback** en lugar de **OnDictionaryChangedHandler**.

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> En hello anterior de código, como parte de la notificación de regeneración de procesamiento hello, primer Hola mantiene estado agregado está desactivada. Dado que se vuelve a generar colección confiable Hola con un estado nuevo, todas las notificaciones anteriores son irrelevantes.
> 
> 

Hola **DictionaryChanged** utiliza el controlador de eventos **NotifyDictionaryChangedEventArgs** tooprovide detalles acerca del evento Hola.
**NotifyDictionaryChangedEventArgs** tiene cinco subclases. Utilice la propiedad action de hello en **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** subclase correcta de toohello:

* **NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a>Recomendaciones
* *Complete* los eventos de notificación tan rápido como sea posible.
* *No ejecute* ninguna operación costosa (por ejemplo, operaciones de E/S) como parte de eventos sincrónicos.
* *Hacer* comprobar el tipo de acción de hello antes de procesar los eventos de Hola. Hola futuro podrían agregar nuevos tipos de acción.

Estas son algunas cosas tookeep en cuenta:

* Las notificaciones se activarán como parte de la ejecución de Hola de una operación. Por ejemplo, se activa una notificación de restauración como último paso de Hola de una operación de restauración. Una restauración no finalizará hasta que se procesa el evento de notificación de Hola.
* Dado que las notificaciones se activarán como parte del programa Hola a aplicar las operaciones, los clientes verán sólo las notificaciones para las operaciones confirmadas localmente. Y dado que las operaciones se garantizan que solo toobe confirmado localmente (en otras palabras, iniciada), puede o no se puede deshacer en hello futuras.
* En la ruta de acceso de puesta al día de hello, se activa una notificación única para cada operación aplicada. Esto significa que si la transacción T1 incluye Create(X), Delete(X) y Create(X), recibirá una notificación para la creación de hello de X, uno para la eliminación de Hola y uno para la creación de Hola de nuevo, en ese orden.
* Para las transacciones que contienen varias operaciones, las operaciones se aplican en orden de hello en el que se recibieron en la réplica principal de Hola de usuario de Hola.
* Como parte del procesamiento de progreso falso, es posible que algunas operaciones se deshagan. Las notificaciones se generan para tales operaciones de deshacer, revertir el estado de Hola de hello réplica tooa atrás estable punto. Una diferencia importante de las notificaciones de deshacer es que se agregan eventos con claves duplicadas. Por ejemplo, si se deshaga la transacción T1, verá una notificación única tooDelete(X).

## <a name="next-steps"></a>Pasos siguientes
* [Colecciones confiables](service-fabric-work-with-reliable-collections.md)
* [Introducción a Reliable Services de Service Fabric de Microsoft Azure](service-fabric-reliable-services-quick-start.md)
* [Copia de seguridad y restauración de Reliable Services (recuperación ante desastres)](service-fabric-reliable-services-backup-restore.md)
* [Referencia para desarrolladores de colecciones confiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

