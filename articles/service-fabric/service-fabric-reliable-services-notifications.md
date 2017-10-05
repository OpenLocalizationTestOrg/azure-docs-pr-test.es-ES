---
title: Notificaciones de Reliable Services | Microsoft Docs
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
ms.openlocfilehash: c6a53d851510ed5e6eec1f3ac0f636ad034a6d4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="e2c3e-103">Notificaciones de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e2c3e-103">Reliable Services notifications</span></span>
<span data-ttu-id="e2c3e-104">Las notificaciones permiten que los clientes sigan los cambios que se están realizando en un objeto que les interesa.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span></span> <span data-ttu-id="e2c3e-105">Existen dos tipos de objeto que admiten notificaciones: *Reliable State Manager* y *Reliable Dictionary*.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="e2c3e-106">Algunas causas habituales del uso de notificaciones son:</span><span class="sxs-lookup"><span data-stu-id="e2c3e-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="e2c3e-107">Creación de vistas materializadas, como índices secundarios o vistas filtradas agregadas del estado de la réplica.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span></span> <span data-ttu-id="e2c3e-108">Un ejemplo es un índice ordenado de todas las claves en un diccionario Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="e2c3e-109">Envío de datos de supervisión, como el número de usuarios agregados en la última hora.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-109">Sending monitoring data, such as the number of users added in the last hour.</span></span>

<span data-ttu-id="e2c3e-110">Las notificaciones se desencadenan como parte de la aplicación de operaciones.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="e2c3e-111">Por ese motivo, se deben controlar las notificaciones lo más rápido posible y los eventos sincrónicos no deben incluir operaciones costosas.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="e2c3e-112">Notificaciones de Reliable State Manager</span><span class="sxs-lookup"><span data-stu-id="e2c3e-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="e2c3e-113">Reliable State Manager proporciona notificaciones para los siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="e2c3e-113">Reliable State Manager provides notifications for the following events:</span></span>

* <span data-ttu-id="e2c3e-114">Transacción</span><span class="sxs-lookup"><span data-stu-id="e2c3e-114">Transaction</span></span>
  * <span data-ttu-id="e2c3e-115">Confirmación</span><span class="sxs-lookup"><span data-stu-id="e2c3e-115">Commit</span></span>
* <span data-ttu-id="e2c3e-116">Administrador de estado</span><span class="sxs-lookup"><span data-stu-id="e2c3e-116">State manager</span></span>
  * <span data-ttu-id="e2c3e-117">Recompilación</span><span class="sxs-lookup"><span data-stu-id="e2c3e-117">Rebuild</span></span>
  * <span data-ttu-id="e2c3e-118">Adición de un estado Reliable State</span><span class="sxs-lookup"><span data-stu-id="e2c3e-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="e2c3e-119">Eliminación de un estado Reliable State</span><span class="sxs-lookup"><span data-stu-id="e2c3e-119">Removal of a reliable state</span></span>

<span data-ttu-id="e2c3e-120">Reliable State Manager realiza un seguimiento de las transacciones en proceso actuales.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-120">Reliable State Manager tracks the current inflight transactions.</span></span> <span data-ttu-id="e2c3e-121">El único cambio en el estado de transacción que hace que se desencadene una notificación es la confirmación de una transacción.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span></span>

<span data-ttu-id="e2c3e-122">Reliable State Manager mantiene una colección de estados Reliable State, como Reliable Dictionary y Reliable Queue.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="e2c3e-123">Reliable State Manager desencadena notificaciones cuando esta colección cambia: se agrega o quita un estado Reliable State o se recompila la colección completa.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span></span>
<span data-ttu-id="e2c3e-124">La colección de Reliable State Manager se recompila en tres situaciones:</span><span class="sxs-lookup"><span data-stu-id="e2c3e-124">The Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="e2c3e-125">Recuperación: cuando se inicia una réplica, recupera su estado anterior del disco.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span></span> <span data-ttu-id="e2c3e-126">Al final de la recuperación, usa **NotifyStateManagerChangedEventArgs** para desencadenar un evento que contiene el conjunto de estados Reliable State recuperados.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span></span>
* <span data-ttu-id="e2c3e-127">Copia completa: para que una réplica pueda unirse al conjunto de configuración, tiene que compilarse.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-127">Full copy: Before a replica can join the configuration set, it has to be built.</span></span> <span data-ttu-id="e2c3e-128">En ocasiones, se requiere que se aplique una copia completa del estado de Reliable State Manager en la réplica principal a la réplica secundaria inactiva.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span></span> <span data-ttu-id="e2c3e-129">En la réplica secundaria, Reliable State Manager usa **NotifyStateManagerChangedEventArgs** para desencadenar un evento que contiene el conjunto de estados Reliable State que adquirió de la réplica principal.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span></span>
* <span data-ttu-id="e2c3e-130">Restauración: en escenarios de recuperación ante desastres, se puede restaurar el estado de la réplica desde una copia de seguridad con **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="e2c3e-131">En estos casos, en la réplica principal, Reliable State Manager usa **NotifyStateManagerChangedEventArgs** para desencadenar un evento que contiene el conjunto de estados Reliable State que restauró de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span></span>

<span data-ttu-id="e2c3e-132">Para registrarse para las notificaciones de transacciones o notificaciones del administrador de estado, se debe registrar con los eventos **TransactionChanged** o **StateManagerChanged** en Reliable State Manager.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="e2c3e-133">Un lugar habitual donde registrarse con estos controladores de eventos es el constructor de su servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-133">A common place to register with these event handlers is the constructor of your stateful service.</span></span> <span data-ttu-id="e2c3e-134">Cuando se registre en el constructor, no perderá ninguna notificación causada por un cambio mientras dure **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="e2c3e-135">El controlador de eventos **TransactionChanged** usa **NotifyTransactionChangedEventArgs** para proporcionar detalles sobre el evento.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span></span> <span data-ttu-id="e2c3e-136">Contiene la propiedad de acción (por ejemplo, **NotifyTransactionChangedAction.Commit**) que especifica el tipo de cambio.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span></span> <span data-ttu-id="e2c3e-137">También contiene la propiedad de transacción que proporciona una referencia a la transacción que ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-137">It also contains the transaction property that provides a reference to the transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="e2c3e-138">En la actualidad, los eventos **TransactionChanged** solo se generan si se confirma la transacción.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span></span> <span data-ttu-id="e2c3e-139">Entonces, la acción equivale a **NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="e2c3e-140">Sin embargo, es posible que en el futuro se generen eventos para otros tipos de cambios en el estado de la transacción.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-140">But in the future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="e2c3e-141">Se recomienda comprobar la acción y solo procesar el evento si es el que espera.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-141">We recommend checking the action and processing the event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="e2c3e-142">A continuación, se ofrece un ejemplo de controlador de eventos **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="e2c3e-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="e2c3e-143">El controlador de eventos **StateManagerChanged** usa **NotifyStateManagerChangedEventArgs** para proporcionar detalles sobre el evento.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="e2c3e-144">**NotifyStateManagerChangedEventArgs** tiene dos subclases: **NotifyStateManagerRebuildEventArgs** y **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="e2c3e-145">Use la propiedad de acción en **NotifyStateManagerChangedEventArgs** para convertir la subclase **NotifyStateManagerChangedEventArgs** en la correcta:</span><span class="sxs-lookup"><span data-stu-id="e2c3e-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="e2c3e-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e2c3e-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="e2c3e-147">**NotifyStateManagerChangedAction.Add** y **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e2c3e-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="e2c3e-148">A continuación, se ofrece un ejemplo de controlador de notificación **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="e2c3e-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="e2c3e-149">Notificaciones de Reliable Dictionary</span><span class="sxs-lookup"><span data-stu-id="e2c3e-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="e2c3e-150">Reliable Dictionary proporciona notificaciones para los siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="e2c3e-150">Reliable Dictionary provides notifications for the following events:</span></span>

* <span data-ttu-id="e2c3e-151">Rebuild: se llama cuando **ReliableDictionary** ha recuperado su estado de una copia de seguridad o un estado local copiado o recuperado.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="e2c3e-152">Clear: se llama cuando se ha borrado el estado de **ReliableDictionary** mediante el método **ClearAsync**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span></span>
* <span data-ttu-id="e2c3e-153">Add: se llama cuando se ha agregado un elemento a **ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-153">Add: Called when an item has been added to **ReliableDictionary**.</span></span>
* <span data-ttu-id="e2c3e-154">Update: se llama cuando se ha actualizado un elemento de **IReliableDictionary** .</span><span class="sxs-lookup"><span data-stu-id="e2c3e-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="e2c3e-155">Remove: se llama cuando se ha eliminado un elemento de **IReliableDictionary** .</span><span class="sxs-lookup"><span data-stu-id="e2c3e-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="e2c3e-156">Para obtener notificaciones de Reliable Dictionary, se debe registrar con el controlador de eventos **DictionaryChanged** en **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="e2c3e-157">Un lugar habitual donde registrarse con estos controladores de eventos es en la notificación de adición de **ReliableStateManager.StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="e2c3e-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="e2c3e-158">Registrarse cuando se agrega **IReliableDictionary** a **IReliableStateManager** garantiza que no se pierda ninguna notificación.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="e2c3e-159">**ProcessStateManagerSingleEntityNotification** es el método de ejemplo al que se llama en el ejemplo anterior de **OnStateManagerChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="e2c3e-160">El código anterior establece la interfaz **IReliableNotificationAsyncCallback**, junto con **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="e2c3e-161">Dado que **NotifyDictionaryRebuildEventArgs** contiene una interfaz **IAsyncEnumerable**, que debe enumerarse de forma asincrónica, las notificaciones de recompilación se desencadenan mediante **RebuildNotificationAsyncCallback** en lugar de **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="e2c3e-162">En el código anterior, como parte del procesamiento de la notificación de recompilación, primero se borra el estado agregado mantenido.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span></span> <span data-ttu-id="e2c3e-163">Como se está recompilando la colección Reliable Collection con un estado nuevo, todas las notificaciones anteriores son irrelevantes.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="e2c3e-164">El controlador de eventos **DictionaryChanged** usa **NotifyDictionaryChangedEventArgs** para proporcionar detalles sobre el evento.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="e2c3e-165">**NotifyDictionaryChangedEventArgs** tiene cinco subclases.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="e2c3e-166">Use la propiedad de acción en **NotifyDictionaryChangedEventArgs** para convertir la subclase **NotifyDictionaryChangedEventArgs** en la correcta:</span><span class="sxs-lookup"><span data-stu-id="e2c3e-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="e2c3e-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e2c3e-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="e2c3e-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e2c3e-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="e2c3e-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e2c3e-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="e2c3e-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e2c3e-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="e2c3e-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e2c3e-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="e2c3e-172">Recomendaciones</span><span class="sxs-lookup"><span data-stu-id="e2c3e-172">Recommendations</span></span>
* <span data-ttu-id="e2c3e-173">*Complete* los eventos de notificación tan rápido como sea posible.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="e2c3e-174">*No ejecute* ninguna operación costosa (por ejemplo, operaciones de E/S) como parte de eventos sincrónicos.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="e2c3e-175">*Compruebe* el tipo de acción antes de procesar el evento.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-175">*Do* check the action type before you process the event.</span></span> <span data-ttu-id="e2c3e-176">Es posible que se agreguen nuevos tipos de acción en el futuro.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-176">New action types might be added in the future.</span></span>

<span data-ttu-id="e2c3e-177">Algunos aspectos que debe tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="e2c3e-177">Here are some things to keep in mind:</span></span>

* <span data-ttu-id="e2c3e-178">Las notificaciones se desencadenan como parte de la ejecución de una operación.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-178">Notifications are fired as part of the execution of an operation.</span></span> <span data-ttu-id="e2c3e-179">Por ejemplo, se desencadena una notificación de restauración como el último paso de una operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-179">For example, a restore notification is fired as the last step of a restore operation.</span></span> <span data-ttu-id="e2c3e-180">La restauración no finalizará hasta que se procese el evento de notificación.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-180">A restore will not finish until the notification event is processed.</span></span>
* <span data-ttu-id="e2c3e-181">Ya que las notificaciones se desencadenan como parte de la aplicación de operaciones, los clientes solo ven notificaciones para las operaciones confirmadas localmente.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="e2c3e-182">Y como solo se garantiza que las operaciones se confirmen localmente (es decir, se registren), es posible que en el futuro se deshagan o no.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span></span>
* <span data-ttu-id="e2c3e-183">En la ruta de acceso de puesta al día, se desencadena una única notificación para cada operación aplicada.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-183">On the redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="e2c3e-184">Esto significa que, si una transacción T1 incluye Create(X), Delete(X) y Create(X), recibirá una notificación para la creación de X, una para la eliminación y otra para la creación de nuevo, en ese orden.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span></span>
* <span data-ttu-id="e2c3e-185">Para las transacciones que contienen varias operaciones, se aplican las operaciones en el orden en que se recibieron en la réplica principal del usuario.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span></span>
* <span data-ttu-id="e2c3e-186">Como parte del procesamiento de progreso falso, es posible que algunas operaciones se deshagan.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="e2c3e-187">Se generan notificaciones para estas operaciones de deshacer y se revierte el estado de la réplica a un punto estable.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span></span> <span data-ttu-id="e2c3e-188">Una diferencia importante de las notificaciones de deshacer es que se agregan eventos con claves duplicadas.</span><span class="sxs-lookup"><span data-stu-id="e2c3e-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="e2c3e-189">Por ejemplo, si se está deshaciendo la transacción T1, el usuario verá una única notificación para Delete(X).</span><span class="sxs-lookup"><span data-stu-id="e2c3e-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2c3e-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2c3e-190">Next steps</span></span>
* [<span data-ttu-id="e2c3e-191">Colecciones confiables</span><span class="sxs-lookup"><span data-stu-id="e2c3e-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="e2c3e-192">Introducción a Reliable Services de Service Fabric de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e2c3e-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="e2c3e-193">Copia de seguridad y restauración de Reliable Services (recuperación ante desastres)</span><span class="sxs-lookup"><span data-stu-id="e2c3e-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="e2c3e-194">Referencia para desarrolladores de colecciones confiables</span><span class="sxs-lookup"><span data-stu-id="e2c3e-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

