---
title: Trabajo con Reliable Collections | Microsoft Docs
description: Aprenda los procedimientos recomendados para trabajar con Reliable Collections.
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: f53f13e4fb83b1cd370ec673e86e5311cd93055f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-reliable-collections"></a><span data-ttu-id="ecab3-103">Trabajo con Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="ecab3-103">Working with Reliable Collections</span></span>
<span data-ttu-id="ecab3-104">Service Fabric ofrece un modelo de programación con estado a los desarrolladores de .NET a través de Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="ecab3-104">Service Fabric offers a stateful programming model available to .NET developers via Reliable Collections.</span></span> <span data-ttu-id="ecab3-105">En concreto, Service Fabric proporciona un diccionario confiable y clases de cola confiables.</span><span class="sxs-lookup"><span data-stu-id="ecab3-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="ecab3-106">Al utilizar estas clases, se crean particiones en el estado (para escalabilidad) y este se replica (para disponibilidad) y se tramita dentro de una partición (para semántica ACID).</span><span class="sxs-lookup"><span data-stu-id="ecab3-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="ecab3-107">Veamos un uso típico de un objeto de diccionario confiable y vea lo que está haciendo realmente.</span><span class="sxs-lookup"><span data-stu-id="ecab3-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record to log & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record to log & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

<span data-ttu-id="ecab3-108">Todas las operaciones en objetos de diccionario confiables (excepto ClearAsync, que no se puede deshacer), requieren un objeto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="ecab3-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="ecab3-109">Este objeto tiene asociados todos los cambios que está intentando realizar en cualquiera diccionario confiable y/u objeto de cola confiable dentro de una sola partición.</span><span class="sxs-lookup"><span data-stu-id="ecab3-109">This object has associated with it any and all changes you’re attempting to make to any reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="ecab3-110">Un objeto ITransaction se adquiere llamando al método CreateTransaction de StateManager de la partición.</span><span class="sxs-lookup"><span data-stu-id="ecab3-110">You acquire an ITransaction object by calling the partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="ecab3-111">En el código anterior, el objeto ITransaction se pasa al método AddAsync de un diccionario confiable.</span><span class="sxs-lookup"><span data-stu-id="ecab3-111">In the code above, the ITransaction object is passed to a reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="ecab3-112">Internamente, los métodos de diccionario que acepta una clave toman un bloqueo de lector o escritor asociado a dicha clave.</span><span class="sxs-lookup"><span data-stu-id="ecab3-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with the key.</span></span> <span data-ttu-id="ecab3-113">Si el método modifica el valor de la clave, dicho método toma un bloqueo de escritura en la clave; si el método solo lee el valor de la clave, se toma un bloqueo de lectura en la clave.</span><span class="sxs-lookup"><span data-stu-id="ecab3-113">If the method modifies the key’s value, the method takes a write lock on the key and if the method only reads from the key’s value, then a read lock is taken on the key.</span></span> <span data-ttu-id="ecab3-114">Puesto que AddAsync modifica el valor de la clave al nuevo valor pasado, se toma el bloqueo de escritura de la clave.</span><span class="sxs-lookup"><span data-stu-id="ecab3-114">Since AddAsync modifies the key’s value to the new, passed-in value, the key’s write lock is taken.</span></span> <span data-ttu-id="ecab3-115">Por tanto, si 2 (o más) subprocesos intentan agregar valores con la misma clave simultáneamente, un subproceso adquirirá el bloqueo de escritura y los otros subprocesos se bloquearán.</span><span class="sxs-lookup"><span data-stu-id="ecab3-115">So, if 2 (or more) threads attempt to add values with the same key at the same time, one thread will acquire the write lock and the other threads will block.</span></span> <span data-ttu-id="ecab3-116">De forma predeterminada, los métodos se bloquean hasta 4 segundos para adquirir el bloqueo; después de 4 segundos, los métodos inician una excepción TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="ecab3-116">By default, methods block for up to 4 seconds to acquire the lock; after 4 seconds, the methods throw a TimeoutException.</span></span> <span data-ttu-id="ecab3-117">Existen sobrecargas de método que le permiten pasar un valor de tiempo de espera explícito si lo prefiere.</span><span class="sxs-lookup"><span data-stu-id="ecab3-117">Method overloads exist allowing you to pass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="ecab3-118">Normalmente, el código se escribe para reaccionar ante una excepción TimeoutException capturándola y reintentando la operación completa (como se muestra en el código anterior).</span><span class="sxs-lookup"><span data-stu-id="ecab3-118">Usually, you write your code to react to a TimeoutException by catching it and retrying the entire operation (as shown in the code above).</span></span> <span data-ttu-id="ecab3-119">En mi sencillo código, simplemente llamo a Task.Delay pasando 100 milisegundos cada vez.</span><span class="sxs-lookup"><span data-stu-id="ecab3-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="ecab3-120">Sin embargo, en realidad, podría ser mejor usar algún tipo de retraso de interrupción exponencial en su lugar.</span><span class="sxs-lookup"><span data-stu-id="ecab3-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="ecab3-121">Una vez que se adquiere el bloqueo, AddAsync agrega las referencias de objeto de clave y valor a un diccionario temporal interno asociado al objeto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="ecab3-121">Once the lock is acquired, AddAsync adds the key and value object references to an internal temporary dictionary associated with the ITransaction object.</span></span> <span data-ttu-id="ecab3-122">Esto se hace para proporcionar una semántica de lectura de escrituras propias.</span><span class="sxs-lookup"><span data-stu-id="ecab3-122">This is done to provide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="ecab3-123">Es decir, después de llamar a AddAsync, una llamada posterior a TryGetValueAsync (con el mismo objeto ITransaction) devolverá el valor incluso si todavía no ha confirmado la transacción.</span><span class="sxs-lookup"><span data-stu-id="ecab3-123">That is, after you call AddAsync, a later call to TryGetValueAsync (using the same ITransaction object) will return the value even if you have not yet committed the transaction.</span></span> <span data-ttu-id="ecab3-124">A continuación, AddAsync serializa los objetos de clave y valor en matrices de bytes y anexa estas matrices de bytes a un archivo de registro en el nodo local.</span><span class="sxs-lookup"><span data-stu-id="ecab3-124">Next, AddAsync serializes your key and value objects to byte arrays and appends these byte arrays to a log file on the local node.</span></span> <span data-ttu-id="ecab3-125">Finalmente, AddAsync envía las matrices de bytes a todas las réplicas secundarias, por lo que tienen la misma información de clave y valor.</span><span class="sxs-lookup"><span data-stu-id="ecab3-125">Finally, AddAsync sends the byte arrays to all the secondary replicas so they have the same key/value information.</span></span> <span data-ttu-id="ecab3-126">Aunque la información de clave y valor se ha escrito en un archivo de registro, la información no se considera parte del diccionario hasta que se ha confirmado la transacción a la que están asociados.</span><span class="sxs-lookup"><span data-stu-id="ecab3-126">Even though the key/value information has been written to a log file, the information is not considered part of the dictionary until the transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="ecab3-127">En el código anterior, la llamada a CommitAsync confirma todas las operaciones de la transacción.</span><span class="sxs-lookup"><span data-stu-id="ecab3-127">In the code above, the call to CommitAsync commits all of the transaction’s operations.</span></span> <span data-ttu-id="ecab3-128">Específicamente, anexa información de confirmación al archivo de registro en el nodo local y también envía el registro de confirmación a todas las réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="ecab3-128">Specifically, it appends commit information to the log file on the local node and also sends the commit record to all the secondary replicas.</span></span> <span data-ttu-id="ecab3-129">Una vez que un cuórum (mayoría) de las réplicas ha respondido, todos los cambios de datos se consideran permanentes y se liberan todos los bloqueos asociados a las claves que se manipularon a través del objeto ITransaction de forma que otros subprocesos y transacciones puedan manipular las mismas claves y sus valores.</span><span class="sxs-lookup"><span data-stu-id="ecab3-129">Once a quorum (majority) of the replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via the ITransaction object are released so other threads/transactions can manipulate the same keys and their values.</span></span>

<span data-ttu-id="ecab3-130">Si no se llama a CommitAsync (normalmente debido a una excepción iniciada), se elimina el objeto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="ecab3-130">If CommitAsync is not called (usually due to an exception being thrown), then the ITransaction object gets disposed.</span></span> <span data-ttu-id="ecab3-131">Al desechar un objeto ITransaction sin confirmar, Service Fabric anexa información de anulación al archivo de registro del nodo local y no es necesario enviar nada a ninguna de las réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="ecab3-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information to the local node’s log file and nothing needs to be sent to any of the secondary replicas.</span></span> <span data-ttu-id="ecab3-132">Y después, se liberan los bloqueos asociados a las claves que se manipularon a través de la transacción.</span><span class="sxs-lookup"><span data-stu-id="ecab3-132">And then, any locks associated with keys that were manipulated via the transaction are released.</span></span>

## <a name="common-pitfalls-and-how-to-avoid-them"></a><span data-ttu-id="ecab3-133">Dificultades comunes y cómo evitarlas</span><span class="sxs-lookup"><span data-stu-id="ecab3-133">Common pitfalls and how to avoid them</span></span>
<span data-ttu-id="ecab3-134">Ahora que entiende cómo funcionan internamente las colecciones confiables, echemos un vistazo a algunos usos incorrectos comunes de ellas.</span><span class="sxs-lookup"><span data-stu-id="ecab3-134">Now that you understand how the reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="ecab3-135">Vea el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="ecab3-135">See the code below:</span></span>

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes the name/user, logs the bytes,
   // & sends the bytes to the secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // The line below updates the property’s value in memory only; the
   // new value is NOT serialized, logged, & sent to secondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

<span data-ttu-id="ecab3-136">Cuando se trabaja con un diccionario .NET común, puede agregar una clave y un valor al diccionario y, luego, cambiar el valor de una propiedad (por ejemplo, LastLogin).</span><span class="sxs-lookup"><span data-stu-id="ecab3-136">When working with a regular .NET dictionary, you can add a key/value to the dictionary and then change the value of a property (such as LastLogin).</span></span> <span data-ttu-id="ecab3-137">Sin embargo, este código no funcionará correctamente con un diccionario confiable.</span><span class="sxs-lookup"><span data-stu-id="ecab3-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="ecab3-138">Según la explicación anterior, recuerde que la llamada a AddAsync serializa los objetos de clave y valor en matrices de bytes y, luego, guarda las matrices en un archivo local y también las envía a las réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="ecab3-138">Remember from the earlier discussion, the call to AddAsync serializes the key/value objects to byte arrays and then saves the arrays to a local file and also sends them to the secondary replicas.</span></span> <span data-ttu-id="ecab3-139">Si posteriormente cambia una propiedad, esto cambia el valor de la propiedad solo en la memoria; no afecta al archivo local o a los datos que se enviarán a las réplicas.</span><span class="sxs-lookup"><span data-stu-id="ecab3-139">If you later change a property, this changes the property’s value in memory only; it does not impact the local file or the data sent to the replicas.</span></span> <span data-ttu-id="ecab3-140">Si el proceso se bloquea, lo que está en memoria se desecha.</span><span class="sxs-lookup"><span data-stu-id="ecab3-140">If the process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="ecab3-141">Cuando se inicia un nuevo proceso u otra réplica se convierte en principal, el valor de propiedad anterior es lo que está disponible.</span><span class="sxs-lookup"><span data-stu-id="ecab3-141">When a new process starts or if another replica becomes primary, then the old property value is what is available.</span></span>

<span data-ttu-id="ecab3-142">Es fundamental recalcar lo fácil que es cometer el tipo de error mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ecab3-142">I cannot stress enough how easy it is to make the kind of mistake shown above.</span></span> <span data-ttu-id="ecab3-143">Y solo aprenderá del error cuando el proceso termine.</span><span class="sxs-lookup"><span data-stu-id="ecab3-143">And, you will only learn about the mistake if/when the process goes down.</span></span> <span data-ttu-id="ecab3-144">La manera correcta de escribir el código es simplemente invertir las dos líneas:</span><span class="sxs-lookup"><span data-stu-id="ecab3-144">The correct way to write the code is simply to reverse the two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="ecab3-145">Este es otro ejemplo que muestra un error común:</span><span class="sxs-lookup"><span data-stu-id="ecab3-145">Here is another example showing a common mistake:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (user.HasValue) {
      // The line below updates the property’s value in memory only; the
      // new value is NOT serialized, logged, & sent to secondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

<span data-ttu-id="ecab3-146">De nuevo, con los diccionarios .NET convencionales, el código anterior funciona bien y es un patrón común: el desarrollador usa una clave para buscar un valor.</span><span class="sxs-lookup"><span data-stu-id="ecab3-146">Again, with regular .NET dictionaries, the code above works fine and is a common pattern: the developer uses a key to look up a value.</span></span> <span data-ttu-id="ecab3-147">Si el valor existe, el desarrollador cambia el valor de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="ecab3-147">If the value exists, the developer changes a property’s value.</span></span> <span data-ttu-id="ecab3-148">Sin embargo, con colecciones confiables, este código tiene el mismo problema que se comentó anteriormente: **no DEBE modificar un objeto una vez que lo haya entregado a una colección confiable.**</span><span class="sxs-lookup"><span data-stu-id="ecab3-148">However, with reliable collections, this code exhibits the same problem as already discussed: **you MUST not modify an object once you have given it to a reliable collection.**</span></span>

<span data-ttu-id="ecab3-149">La forma correcta de actualizar un valor en una colección confiable es obtener una referencia al valor existente y considerar el objeto al que se refiere esta referencia como inmutable.</span><span class="sxs-lookup"><span data-stu-id="ecab3-149">The correct way to update a value in a reliable collection, is to get a reference to the existing value and consider the object referred to by this reference immutable.</span></span> <span data-ttu-id="ecab3-150">Después, cree un nuevo objeto que es una copia exacta del objeto original.</span><span class="sxs-lookup"><span data-stu-id="ecab3-150">Then, create a new object which is an exact copy of the original object.</span></span> <span data-ttu-id="ecab3-151">Ahora, puede modificar el estado de este nuevo objeto y escribir este en la colección para que se serialice en matrices de bytes, se anexe al archivo local y se envíe a las réplicas.</span><span class="sxs-lookup"><span data-stu-id="ecab3-151">Now, you can modify the state of this new object and write the new object into the collection so that it gets serialized to byte arrays, appended to the local file and sent to the replicas.</span></span> <span data-ttu-id="ecab3-152">Después de confirmar los cambios, los objetos en memoria, el archivo local y todas las réplicas tienen exactamente el mismo estado.</span><span class="sxs-lookup"><span data-stu-id="ecab3-152">After committing the change(s), the in-memory objects, the local file, and all the replicas have the same exact state.</span></span> <span data-ttu-id="ecab3-153">¡Todo es correcto!</span><span class="sxs-lookup"><span data-stu-id="ecab3-153">All is good!</span></span>

<span data-ttu-id="ecab3-154">El código siguiente muestra la manera adecuada de actualizar un valor en una colección confiable:</span><span class="sxs-lookup"><span data-stu-id="ecab3-154">The code below shows the correct way to update a value in a reliable collection:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with the same state as the current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In the new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update the key’s value to the updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-to-prevent-programmer-error"></a><span data-ttu-id="ecab3-155">Definición de tipos de datos inmutables para evitar errores de programador</span><span class="sxs-lookup"><span data-stu-id="ecab3-155">Define immutable data types to prevent programmer error</span></span>
<span data-ttu-id="ecab3-156">Idealmente, nos gustaría que el compilador informara de errores cuando se crea accidentalmente código que transforma el estado de un objeto que se supone que se considera inmutable.</span><span class="sxs-lookup"><span data-stu-id="ecab3-156">Ideally, we’d like the compiler to report errors when you accidentally produce code that mutates state of an object that you are supposed to consider immutable.</span></span> <span data-ttu-id="ecab3-157">Sin embargo, el compilador de C# no tiene la posibilidad de hacer esto.</span><span class="sxs-lookup"><span data-stu-id="ecab3-157">But, the C# compiler does not have the ability to do this.</span></span> <span data-ttu-id="ecab3-158">Por lo tanto, para evitar posibles errores de programador, es muy recomendable que defina los tipos que usa con colecciones confiables para que sean tipos inmutables.</span><span class="sxs-lookup"><span data-stu-id="ecab3-158">So, to avoid potential programmer bugs, we highly recommend that you define the types you use with reliable collections to be immutable types.</span></span> <span data-ttu-id="ecab3-159">En concreto, esto significa que se debe ceñir a tipos de valor principales (como números [Int32, UInt64, etc.], DateTime, Guid, TimeSpan y similares).</span><span class="sxs-lookup"><span data-stu-id="ecab3-159">Specifically, this means that you stick to core value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and the like).</span></span> <span data-ttu-id="ecab3-160">Y, por supuesto, también puede usar String.</span><span class="sxs-lookup"><span data-stu-id="ecab3-160">And, of course, you can also use String.</span></span> <span data-ttu-id="ecab3-161">Es mejor evitar las propiedades de la colección ya que la serialización y deserialización de las mismas puede, con frecuencia, afectar negativamente al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="ecab3-161">It is best to avoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="ecab3-162">Sin embargo, si desea utilizar las propiedades de la colección, es muy recomendable el uso de la biblioteca de colecciones inmutables de .NET ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="ecab3-162">However, if you want to use collection properties, we highly recommend the use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="ecab3-163">Esta biblioteca está disponible para descargarse desde http://nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ecab3-163">This library is available for download from http://nuget.org.</span></span> <span data-ttu-id="ecab3-164">También se recomienda sellar las clases y establecer los campos como solo lectura siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="ecab3-164">We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="ecab3-165">El tipo UserInfo siguiente muestra cómo definir un tipo inmutable aprovechando las recomendaciones mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ecab3-165">The UserInfo type below demonstrates how to define an immutable type taking advantage of aforementioned recommendations.</span></span>

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert the deserialized collection to an immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has to set it. So instead, the getter is public and the setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId to the ItemsBidding
   // collection by creating a new immutable UserInfo object with the added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

<span data-ttu-id="ecab3-166">El tipo ItemId es también un tipo inmutable, tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="ecab3-166">The ItemId type is also an immutable type as shown here:</span></span>

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="ecab3-167">Control de versiones de esquema (actualizaciones)</span><span class="sxs-lookup"><span data-stu-id="ecab3-167">Schema versioning (upgrades)</span></span>
<span data-ttu-id="ecab3-168">Internamente, Reliable Collections serializa los objetos mediante DataContractSerializer de NET.</span><span class="sxs-lookup"><span data-stu-id="ecab3-168">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="ecab3-169">Los objetos serializados se conservan en el disco local de la réplica principal y también se transmiten a las réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="ecab3-169">The serialized objects are persisted to the primary replica’s local disk and are also transmitted to the secondary replicas.</span></span> <span data-ttu-id="ecab3-170">A medida que se desarrolle el servicio, es probable que desee cambiar el tipo de datos (esquema) que el servicio requiere.</span><span class="sxs-lookup"><span data-stu-id="ecab3-170">As your service matures, it’s likely you’ll want to change the kind of data (schema) your service requires.</span></span> <span data-ttu-id="ecab3-171">Debe abordar el control de versiones de los datos con mucho cuidado.</span><span class="sxs-lookup"><span data-stu-id="ecab3-171">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="ecab3-172">En primer lugar y ante todo, siempre debe ser capaz de deserializar los datos antiguos.</span><span class="sxs-lookup"><span data-stu-id="ecab3-172">First and foremost, you must always be able to deserialize old data.</span></span> <span data-ttu-id="ecab3-173">En concreto, esto significa que el código de deserialización debe ser compatible con versiones anteriores de forma ilimitada: la versión 333 del código de servicio debe ser capaz de funcionar en los datos colocados en una colección confiable por la versión 1 del código de servicio de hace 5 años.</span><span class="sxs-lookup"><span data-stu-id="ecab3-173">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able to operate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="ecab3-174">Además, el código de servicio se actualiza con un dominio de actualización en cada momento.</span><span class="sxs-lookup"><span data-stu-id="ecab3-174">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="ecab3-175">Por lo tanto, durante una actualización, tiene dos versiones diferentes del código de servicio ejecutándose simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="ecab3-175">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="ecab3-176">Debe evitar que la nueva versión del código de servicio utilice el nuevo esquema, ya que las versiones anteriores de dicho código podrían no ser capaces de controlar el nuevo esquema.</span><span class="sxs-lookup"><span data-stu-id="ecab3-176">You must avoid having the new version of your service code use the new schema as old versions of your service code might not be able to handle the new schema.</span></span> <span data-ttu-id="ecab3-177">Cuando sea posible, debería diseñar cada versión del servicio para que sea compatible con versiones posteriores mediante la versión 1.</span><span class="sxs-lookup"><span data-stu-id="ecab3-177">When possible, you should design each version of your service to be forward compatible by 1 version.</span></span> <span data-ttu-id="ecab3-178">En concreto, esto significa que la versión 1 (V1) del código de servicio simplemente debe ser capaz de omitir cualquier elemento de esquema que no controla explícitamente.</span><span class="sxs-lookup"><span data-stu-id="ecab3-178">Specifically, this means that V1 of your service code should be able to simply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="ecab3-179">Sin embargo, debe ser capaz de guardar todos los datos que no conoce explícitamente y simplemente reescribirlos al actualizar un valor o una clave de diccionario.</span><span class="sxs-lookup"><span data-stu-id="ecab3-179">However, it must be able to save any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="ecab3-180">Aunque puede modificar el esquema de una clave, debe asegurarse de que el código hash de la clave y los algoritmos de igualdades son estables.</span><span class="sxs-lookup"><span data-stu-id="ecab3-180">While you can modify the schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="ecab3-181">Si cambia la forma en la que cualquiera de estos algoritmos opera, no podrá volver a buscar la clave del diccionario confiable nunca más.</span><span class="sxs-lookup"><span data-stu-id="ecab3-181">If you change how either of these algorithms operate, you will not be able to look up the key within the reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="ecab3-182">Como alternativa, puede realizar lo que se conoce normalmente como una actualización de 2 fases.</span><span class="sxs-lookup"><span data-stu-id="ecab3-182">Alternatively, you can perform what is typically referred to as a 2-phase upgrade.</span></span> <span data-ttu-id="ecab3-183">Con una actualización de 2 fases, usted actualiza el servicio de V1 a V2: V2 contiene el código que sabe cómo tratar con el nuevo cambio de esquema, pero este código no se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="ecab3-183">With a 2-phase upgrade, you upgrade your service from V1 to V2: V2 contains the code that knows how to deal with the new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="ecab3-184">Cuando el código de V2 lee datos de V1, opera en ellos y escribe datos de V1.</span><span class="sxs-lookup"><span data-stu-id="ecab3-184">When the V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="ecab3-185">Luego, después de que la actualización se complete en todos los dominios de actualización, puede indicar de algún modo a las instancias de V2 en ejecución que la actualización se ha completado.</span><span class="sxs-lookup"><span data-stu-id="ecab3-185">Then, after the upgrade is complete across all upgrade domains, you can somehow signal to the running V2 instances that the upgrade is complete.</span></span> <span data-ttu-id="ecab3-186">(Una forma de indicar esto es lanzar una actualización de la configuración; esta característica es la que convierte a esto en una actualización de 2 fases). Ahora, las instancias de V2 pueden leer datos de V1, convertirlos en datos de V2, operar en ellos y escribirlos como datos de V2.</span><span class="sxs-lookup"><span data-stu-id="ecab3-186">(One way to signal this is to roll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, the V2 instances can read V1 data, convert it to V2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="ecab3-187">Cuando otras instancias lean datos de V2, no necesitarán convertirlos; simplemente operarán en ellos y escribirán datos de V2.</span><span class="sxs-lookup"><span data-stu-id="ecab3-187">When other instances read V2 data, they do not need to convert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecab3-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ecab3-188">Next Steps</span></span>
<span data-ttu-id="ecab3-189">Para más información sobre la creación de contratos de datos compatibles con versiones posteriores, vea [Contratos de datos compatibles con versiones posteriores](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecab3-189">To learn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="ecab3-190">Para obtener procedimientos recomendados sobre el control de versiones de contratos de datos, consulte [Versiones de contratos de datos](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecab3-190">To learn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="ecab3-191">Para más información sobre cómo implementar contratos de datos tolerantes a versiones, consulte [Devoluciones de llamadas en la serialización tolerante a versiones](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecab3-191">To learn how to implement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="ecab3-192">Para más información sobre cómo proporcionar una estructura de datos que pueda interoperar entre varias versiones, consulte [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecab3-192">To learn how to provide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
