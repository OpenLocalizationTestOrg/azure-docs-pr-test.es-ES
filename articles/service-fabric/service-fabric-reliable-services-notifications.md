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
# <a name="reliable-services-notifications"></a><span data-ttu-id="5bc91-103">Notificaciones de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="5bc91-103">Reliable Services notifications</span></span>
<span data-ttu-id="5bc91-104">Las notificaciones permiten a los clientes los cambios de hello tootrack que van a ser objeto de tooan que estén interesados en.</span><span class="sxs-lookup"><span data-stu-id="5bc91-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="5bc91-105">Existen dos tipos de objeto que admiten notificaciones: *Reliable State Manager* y *Reliable Dictionary*.</span><span class="sxs-lookup"><span data-stu-id="5bc91-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="5bc91-106">Algunas causas habituales del uso de notificaciones son:</span><span class="sxs-lookup"><span data-stu-id="5bc91-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="5bc91-107">Edificio materializa vistas, como los índices secundarios o agrega vistas filtradas de estado de la réplica de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="5bc91-108">Un ejemplo es un índice ordenado de todas las claves en un diccionario Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="5bc91-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="5bc91-109">Datos de supervisión envío, como el número de Hola de los usuarios agregados en hello última hora.</span><span class="sxs-lookup"><span data-stu-id="5bc91-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="5bc91-110">Las notificaciones se desencadenan como parte de la aplicación de operaciones.</span><span class="sxs-lookup"><span data-stu-id="5bc91-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="5bc91-111">Por ese motivo, se deben controlar las notificaciones lo más rápido posible y los eventos sincrónicos no deben incluir operaciones costosas.</span><span class="sxs-lookup"><span data-stu-id="5bc91-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="5bc91-112">Notificaciones de Reliable State Manager</span><span class="sxs-lookup"><span data-stu-id="5bc91-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="5bc91-113">Administrador de estado de confianza proporciona notificaciones para hello siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="5bc91-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="5bc91-114">Transacción</span><span class="sxs-lookup"><span data-stu-id="5bc91-114">Transaction</span></span>
  * <span data-ttu-id="5bc91-115">Confirmación</span><span class="sxs-lookup"><span data-stu-id="5bc91-115">Commit</span></span>
* <span data-ttu-id="5bc91-116">Administrador de estado</span><span class="sxs-lookup"><span data-stu-id="5bc91-116">State manager</span></span>
  * <span data-ttu-id="5bc91-117">Recompilación</span><span class="sxs-lookup"><span data-stu-id="5bc91-117">Rebuild</span></span>
  * <span data-ttu-id="5bc91-118">Adición de un estado Reliable State</span><span class="sxs-lookup"><span data-stu-id="5bc91-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="5bc91-119">Eliminación de un estado Reliable State</span><span class="sxs-lookup"><span data-stu-id="5bc91-119">Removal of a reliable state</span></span>

<span data-ttu-id="5bc91-120">Administrador de estado de confianza realiza un seguimiento de las transacciones en proceso actuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="5bc91-121">Hola único cambio en un estado de transacción que hace que un toobe notificación activada es una transacción se confirma.</span><span class="sxs-lookup"><span data-stu-id="5bc91-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="5bc91-122">Reliable State Manager mantiene una colección de estados Reliable State, como Reliable Dictionary y Reliable Queue.</span><span class="sxs-lookup"><span data-stu-id="5bc91-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="5bc91-123">Las notificaciones cuando cambia esta colección desencadena el Administrador de estado de confianza: se agrega o quita un estado confiable, o se vuelve a generar la colección completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="5bc91-124">Hola colección confiable Administrador de estado se vuelve a generar en tres casos:</span><span class="sxs-lookup"><span data-stu-id="5bc91-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="5bc91-125">Recuperación: Cuando se inicia una réplica, recupera su estado anterior desde el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="5bc91-126">Al final de Hola de recuperación, usa **NotifyStateManagerChangedEventArgs** toofire un evento que contiene el conjunto de Hola de Estados confiables recuperados.</span><span class="sxs-lookup"><span data-stu-id="5bc91-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="5bc91-127">Copia completa: antes de que una réplica puede unirse a conjunto de configuración de hello, tiene toobe integrada.</span><span class="sxs-lookup"><span data-stu-id="5bc91-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="5bc91-128">A veces, esto requiere una copia completa del estado del Administrador de confianza estado de hello réplica principal toobe toohello aplicado inactivo réplica secundaria.</span><span class="sxs-lookup"><span data-stu-id="5bc91-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="5bc91-129">El Administrador de estado de confianza en los usos de la réplica secundaria de hello **NotifyStateManagerChangedEventArgs** toofire un evento que contiene el conjunto de Hola de Estados confiables que adquirió de réplica principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="5bc91-130">Restore: En los escenarios de recuperación de desastres, estado de la réplica de Hola se puede restaurar desde una copia de seguridad a través de **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="5bc91-131">En tales casos, se utiliza el Administrador de estado confiable en la réplica principal de hello **NotifyStateManagerChangedEventArgs** toofire un evento que contiene el conjunto de Hola de Estados confiables que se restauran desde la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="5bc91-132">tooregister para las notificaciones de la transacción o las notificaciones del Administrador de estado, deberá tooregister con hello **TransactionChanged** o **StateManagerChanged** eventos en el Administrador de estado confiable.</span><span class="sxs-lookup"><span data-stu-id="5bc91-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="5bc91-133">Un lugar común tooregister con estos controladores de eventos es el constructor de Hola de su servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="5bc91-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="5bc91-134">Al registrar en el constructor de hello, no pierde cualquier notificación que se debe a un cambio durante la duración de Hola de **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="5bc91-135">Hola **TransactionChanged** utiliza el controlador de eventos **NotifyTransactionChangedEventArgs** tooprovide detalles acerca del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="5bc91-136">Contiene propiedad de acción de hello (por ejemplo, **NotifyTransactionChangedAction.Commit**) que especifica el tipo de saludo de cambio.</span><span class="sxs-lookup"><span data-stu-id="5bc91-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="5bc91-137">También contiene la propiedad de la transacción de Hola que proporciona una transacción de toohello de referencia que ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="5bc91-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="5bc91-138">En la actualidad, **TransactionChanged** se generan eventos solo si se confirma la transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="5bc91-139">Hello acción equivale a continuación, demasiado**NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="5bc91-140">Pero en hello futuras, se podrían producir eventos para otros tipos de cambios de estado de transacción.</span><span class="sxs-lookup"><span data-stu-id="5bc91-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="5bc91-141">Se recomienda comprobar acción de hello y procesar eventos de hello solo si es uno que se espera.</span><span class="sxs-lookup"><span data-stu-id="5bc91-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="5bc91-142">A continuación, se ofrece un ejemplo de controlador de eventos **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="5bc91-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="5bc91-143">Hola **StateManagerChanged** utiliza el controlador de eventos **NotifyStateManagerChangedEventArgs** tooprovide detalles acerca del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="5bc91-144">**NotifyStateManagerChangedEventArgs** tiene dos subclases: **NotifyStateManagerRebuildEventArgs** y **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="5bc91-145">Usar propiedades de acción de hello en **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** subclase correcta de toohello:</span><span class="sxs-lookup"><span data-stu-id="5bc91-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="5bc91-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="5bc91-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="5bc91-147">**NotifyStateManagerChangedAction.Add** y **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="5bc91-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="5bc91-148">A continuación, se ofrece un ejemplo de controlador de notificación **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="5bc91-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="5bc91-149">Notificaciones de Reliable Dictionary</span><span class="sxs-lookup"><span data-stu-id="5bc91-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="5bc91-150">Diccionario confiable proporciona notificaciones para hello siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="5bc91-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="5bc91-151">Rebuild: se llama cuando **ReliableDictionary** ha recuperado su estado de una copia de seguridad o un estado local copiado o recuperado.</span><span class="sxs-lookup"><span data-stu-id="5bc91-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="5bc91-152">Borrar: Se le llama cuando Hola estado de **ReliableDictionary** se ha borrado a través de hello **ClearAsync** método.</span><span class="sxs-lookup"><span data-stu-id="5bc91-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="5bc91-153">Agregar: se le llama cuando se ha agregado un elemento demasiado**ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="5bc91-154">Update: se llama cuando se ha actualizado un elemento de **IReliableDictionary** .</span><span class="sxs-lookup"><span data-stu-id="5bc91-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="5bc91-155">Remove: se llama cuando se ha eliminado un elemento de **IReliableDictionary** .</span><span class="sxs-lookup"><span data-stu-id="5bc91-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="5bc91-156">las notificaciones de diccionario confiable tooget, necesita tooregister con hello **DictionaryChanged** controlador de eventos en **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="5bc91-157">Un lugar común tooregister con estos controladores de eventos se encuentra en hello **ReliableStateManager.StateManagerChanged** agregar la notificación.</span><span class="sxs-lookup"><span data-stu-id="5bc91-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="5bc91-158">Registrar cuándo **IReliableDictionary** se agrega demasiado**IReliableStateManager** garantiza que no se pierda ninguna notificación.</span><span class="sxs-lookup"><span data-stu-id="5bc91-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="5bc91-159">**ProcessStateManagerSingleEntityNotification** es el método de ejemplo de Hola ese Hola anterior **OnStateManagerChangedHandler** llamadas de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5bc91-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="5bc91-160">código anterior Hello establece hello **IReliableNotificationAsyncCallback** interfaz, junto con **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="5bc91-161">Porque **NotifyDictionaryRebuildEventArgs** contiene un **IAsyncEnumerable** interfaz--toobe enumerar de forma asincrónica, es necesario que las notificaciones de regeneración se activan a través de  **RebuildNotificationAsyncCallback** en lugar de **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="5bc91-162">En hello anterior de código, como parte de la notificación de regeneración de procesamiento hello, primer Hola mantiene estado agregado está desactivada.</span><span class="sxs-lookup"><span data-stu-id="5bc91-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="5bc91-163">Dado que se vuelve a generar colección confiable Hola con un estado nuevo, todas las notificaciones anteriores son irrelevantes.</span><span class="sxs-lookup"><span data-stu-id="5bc91-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="5bc91-164">Hola **DictionaryChanged** utiliza el controlador de eventos **NotifyDictionaryChangedEventArgs** tooprovide detalles acerca del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="5bc91-165">**NotifyDictionaryChangedEventArgs** tiene cinco subclases.</span><span class="sxs-lookup"><span data-stu-id="5bc91-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="5bc91-166">Utilice la propiedad action de hello en **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** subclase correcta de toohello:</span><span class="sxs-lookup"><span data-stu-id="5bc91-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="5bc91-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="5bc91-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="5bc91-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="5bc91-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="5bc91-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="5bc91-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="5bc91-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="5bc91-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="5bc91-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="5bc91-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="5bc91-172">Recomendaciones</span><span class="sxs-lookup"><span data-stu-id="5bc91-172">Recommendations</span></span>
* <span data-ttu-id="5bc91-173">*Complete* los eventos de notificación tan rápido como sea posible.</span><span class="sxs-lookup"><span data-stu-id="5bc91-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="5bc91-174">*No ejecute* ninguna operación costosa (por ejemplo, operaciones de E/S) como parte de eventos sincrónicos.</span><span class="sxs-lookup"><span data-stu-id="5bc91-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="5bc91-175">*Hacer* comprobar el tipo de acción de hello antes de procesar los eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="5bc91-176">Hola futuro podrían agregar nuevos tipos de acción.</span><span class="sxs-lookup"><span data-stu-id="5bc91-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="5bc91-177">Estas son algunas cosas tookeep en cuenta:</span><span class="sxs-lookup"><span data-stu-id="5bc91-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="5bc91-178">Las notificaciones se activarán como parte de la ejecución de Hola de una operación.</span><span class="sxs-lookup"><span data-stu-id="5bc91-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="5bc91-179">Por ejemplo, se activa una notificación de restauración como último paso de Hola de una operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="5bc91-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="5bc91-180">Una restauración no finalizará hasta que se procesa el evento de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="5bc91-181">Dado que las notificaciones se activarán como parte del programa Hola a aplicar las operaciones, los clientes verán sólo las notificaciones para las operaciones confirmadas localmente.</span><span class="sxs-lookup"><span data-stu-id="5bc91-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="5bc91-182">Y dado que las operaciones se garantizan que solo toobe confirmado localmente (en otras palabras, iniciada), puede o no se puede deshacer en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="5bc91-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="5bc91-183">En la ruta de acceso de puesta al día de hello, se activa una notificación única para cada operación aplicada.</span><span class="sxs-lookup"><span data-stu-id="5bc91-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="5bc91-184">Esto significa que si la transacción T1 incluye Create(X), Delete(X) y Create(X), recibirá una notificación para la creación de hello de X, uno para la eliminación de Hola y uno para la creación de Hola de nuevo, en ese orden.</span><span class="sxs-lookup"><span data-stu-id="5bc91-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="5bc91-185">Para las transacciones que contienen varias operaciones, las operaciones se aplican en orden de hello en el que se recibieron en la réplica principal de Hola de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5bc91-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="5bc91-186">Como parte del procesamiento de progreso falso, es posible que algunas operaciones se deshagan.</span><span class="sxs-lookup"><span data-stu-id="5bc91-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="5bc91-187">Las notificaciones se generan para tales operaciones de deshacer, revertir el estado de Hola de hello réplica tooa atrás estable punto.</span><span class="sxs-lookup"><span data-stu-id="5bc91-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="5bc91-188">Una diferencia importante de las notificaciones de deshacer es que se agregan eventos con claves duplicadas.</span><span class="sxs-lookup"><span data-stu-id="5bc91-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="5bc91-189">Por ejemplo, si se deshaga la transacción T1, verá una notificación única tooDelete(X).</span><span class="sxs-lookup"><span data-stu-id="5bc91-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bc91-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5bc91-190">Next steps</span></span>
* [<span data-ttu-id="5bc91-191">Colecciones confiables</span><span class="sxs-lookup"><span data-stu-id="5bc91-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="5bc91-192">Introducción a Reliable Services de Service Fabric de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5bc91-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="5bc91-193">Copia de seguridad y restauración de Reliable Services (recuperación ante desastres)</span><span class="sxs-lookup"><span data-stu-id="5bc91-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="5bc91-194">Referencia para desarrolladores de colecciones confiables</span><span class="sxs-lookup"><span data-stu-id="5bc91-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

