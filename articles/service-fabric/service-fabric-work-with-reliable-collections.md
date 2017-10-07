---
title: aaaWorking con colecciones confiable | Documentos de Microsoft
description: "Obtenga información acerca de prácticas recomendadas de Hola para trabajar con colecciones de confianza."
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
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a><span data-ttu-id="157c9-103">Trabajo con Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="157c9-103">Working with Reliable Collections</span></span>
<span data-ttu-id="157c9-104">Service Fabric ofrece un con estado a los desarrolladores de modelo too.NET disponible a través de colecciones confiable de programación.</span><span class="sxs-lookup"><span data-stu-id="157c9-104">Service Fabric offers a stateful programming model available too.NET developers via Reliable Collections.</span></span> <span data-ttu-id="157c9-105">En concreto, Service Fabric proporciona un diccionario confiable y clases de cola confiables.</span><span class="sxs-lookup"><span data-stu-id="157c9-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="157c9-106">Al utilizar estas clases, se crean particiones en el estado (para escalabilidad) y este se replica (para disponibilidad) y se tramita dentro de una partición (para semántica ACID).</span><span class="sxs-lookup"><span data-stu-id="157c9-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="157c9-107">Veamos un uso típico de un objeto de diccionario confiable y vea lo que está haciendo realmente.</span><span class="sxs-lookup"><span data-stu-id="157c9-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

<span data-ttu-id="157c9-108">Todas las operaciones en objetos de diccionario confiables (excepto ClearAsync, que no se puede deshacer), requieren un objeto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="157c9-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="157c9-109">Este objeto tiene asociado ningún y todos los cambios que está intentando toomake tooany confiable diccionario u objetos de cola confiable dentro de una sola partición.</span><span class="sxs-lookup"><span data-stu-id="157c9-109">This object has associated with it any and all changes you’re attempting toomake tooany reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="157c9-110">Adquirir un ITransaction objeto mediante una llamada a la partición de hello del método de CreateTransaction del StateManager.</span><span class="sxs-lookup"><span data-stu-id="157c9-110">You acquire an ITransaction object by calling hello partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="157c9-111">En el código de hello anterior, el objeto de ITransaction de Hola se pasa método de AddAsync del diccionario de tooa confiable.</span><span class="sxs-lookup"><span data-stu-id="157c9-111">In hello code above, hello ITransaction object is passed tooa reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="157c9-112">Internamente, los métodos de diccionario que acepta una clave toman un bloqueo de lector/escritor asociado con la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="157c9-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with hello key.</span></span> <span data-ttu-id="157c9-113">Si el método hello modifica el valor de la clave de hello, método hello toma un bloqueo de escritura en la clave de Hola y si método hello solo lee desde el valor de la clave de hello, a continuación, se realiza un bloqueo de lectura en clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="157c9-113">If hello method modifies hello key’s value, hello method takes a write lock on hello key and if hello method only reads from hello key’s value, then a read lock is taken on hello key.</span></span> <span data-ttu-id="157c9-114">Puesto que AddAsync modifica toohello del valor de la clave de hello nueva, se toma valor pasado como parámetro, bloqueo de escritura de la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="157c9-114">Since AddAsync modifies hello key’s value toohello new, passed-in value, hello key’s write lock is taken.</span></span> <span data-ttu-id="157c9-115">Por lo tanto, si los subprocesos de 2 (o más) intentan tooadd valores con hello misma clave en hello mismo tiempo, un subproceso adquirirá el bloqueo de escritura de Hola y Hola otros subprocesos se bloquean.</span><span class="sxs-lookup"><span data-stu-id="157c9-115">So, if 2 (or more) threads attempt tooadd values with hello same key at hello same time, one thread will acquire hello write lock and hello other threads will block.</span></span> <span data-ttu-id="157c9-116">De forma predeterminada, un bloque de métodos para el bloqueo de too4 segundos tooacquire Hola; Después de 4 segundos, métodos de hello lanzan una excepción TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="157c9-116">By default, methods block for up too4 seconds tooacquire hello lock; after 4 seconds, hello methods throw a TimeoutException.</span></span> <span data-ttu-id="157c9-117">Sobrecargas de método existen permitiendo toopass un valor de tiempo de espera explícito si prefiere.</span><span class="sxs-lookup"><span data-stu-id="157c9-117">Method overloads exist allowing you toopass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="157c9-118">Por lo general, se escribe los tooa de tooreact código TimeoutException capturarla y volver a intentar la operación completa de hello (como se muestra en el código de hello anterior).</span><span class="sxs-lookup"><span data-stu-id="157c9-118">Usually, you write your code tooreact tooa TimeoutException by catching it and retrying hello entire operation (as shown in hello code above).</span></span> <span data-ttu-id="157c9-119">En mi sencillo código, simplemente llamo a Task.Delay pasando 100 milisegundos cada vez.</span><span class="sxs-lookup"><span data-stu-id="157c9-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="157c9-120">Sin embargo, en realidad, podría ser mejor usar algún tipo de retraso de interrupción exponencial en su lugar.</span><span class="sxs-lookup"><span data-stu-id="157c9-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="157c9-121">Una vez que se adquiere el bloqueo de hello, AddAsync agrega la clave de Hola y tooan diccionario temporal interno asociado Hola ITransaction objeto hace referencia a objeto de valor.</span><span class="sxs-lookup"><span data-stu-id="157c9-121">Once hello lock is acquired, AddAsync adds hello key and value object references tooan internal temporary dictionary associated with hello ITransaction object.</span></span> <span data-ttu-id="157c9-122">Esto se hace tooprovide con semántica de lectura your-posee-escrituras.</span><span class="sxs-lookup"><span data-stu-id="157c9-122">This is done tooprovide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="157c9-123">Es decir, después de llamar a AddAsync, un tooTryGetValueAsync llamada posterior (usando Hola el mismo objeto ITransaction) devolverá el valor de hello incluso si aún no hayan confirmado la transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="157c9-123">That is, after you call AddAsync, a later call tooTryGetValueAsync (using hello same ITransaction object) will return hello value even if you have not yet committed hello transaction.</span></span> <span data-ttu-id="157c9-124">A continuación, AddAsync serializa su clave y valor toobyte matrices de objetos y anexa estos archivo de registro de tooa de matrices de bytes en el nodo local Hola.</span><span class="sxs-lookup"><span data-stu-id="157c9-124">Next, AddAsync serializes your key and value objects toobyte arrays and appends these byte arrays tooa log file on hello local node.</span></span> <span data-ttu-id="157c9-125">Por último, AddAsync envía Hola bytes matrices tooall Hola réplicas secundarias para que haya Hola misma información de clave/valor.</span><span class="sxs-lookup"><span data-stu-id="157c9-125">Finally, AddAsync sends hello byte arrays tooall hello secondary replicas so they have hello same key/value information.</span></span> <span data-ttu-id="157c9-126">Aunque la información de clave/valor Hola se ha escrito el archivo de registro tooa, información de hello no se considera parte del diccionario de hello hasta que la transacción de Hola que están asociadas se ha confirmado.</span><span class="sxs-lookup"><span data-stu-id="157c9-126">Even though hello key/value information has been written tooa log file, hello information is not considered part of hello dictionary until hello transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="157c9-127">En el código de hello anterior, Hola llamada tooCommitAsync confirma todas las operaciones de la transacción de Hola de.</span><span class="sxs-lookup"><span data-stu-id="157c9-127">In hello code above, hello call tooCommitAsync commits all of hello transaction’s operations.</span></span> <span data-ttu-id="157c9-128">En concreto, anexa el archivo de registro de toohello de información de confirmación en el nodo local hello y también envía Hola réplicas secundarias de confirmación tooall registro Hola.</span><span class="sxs-lookup"><span data-stu-id="157c9-128">Specifically, it appends commit information toohello log file on hello local node and also sends hello commit record tooall hello secondary replicas.</span></span> <span data-ttu-id="157c9-129">Una vez que ha respondido un quórum (mayoría) de réplicas de hello, todos los datos se consideran cambios permanentes y los bloqueos asociados con las claves que se manipulación a través del objeto de ITransaction Hola se liberan para otras transacciones de subprocesos puede manipular Hola mismas claves y sus valores.</span><span class="sxs-lookup"><span data-stu-id="157c9-129">Once a quorum (majority) of hello replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via hello ITransaction object are released so other threads/transactions can manipulate hello same keys and their values.</span></span>

<span data-ttu-id="157c9-130">Si no se llama a CommitAsync (normalmente debido a que se produzca una excepción de tooan), objeto de ITransaction de hello obtiene eliminado.</span><span class="sxs-lookup"><span data-stu-id="157c9-130">If CommitAsync is not called (usually due tooan exception being thrown), then hello ITransaction object gets disposed.</span></span> <span data-ttu-id="157c9-131">Al desechar un objeto de ITransaction sin confirmar, Service Fabric anexa el archivo de registro de anulación información toohello del nodo local y es necesario toobe ninguna acción envían tooany de hello las réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="157c9-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information toohello local node’s log file and nothing needs toobe sent tooany of hello secondary replicas.</span></span> <span data-ttu-id="157c9-132">Y, a continuación, se liberan los bloqueos asociados con las claves que se manipulación a través de la transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="157c9-132">And then, any locks associated with keys that were manipulated via hello transaction are released.</span></span>

## <a name="common-pitfalls-and-how-tooavoid-them"></a><span data-ttu-id="157c9-133">Los errores comunes y cómo tooavoid ellos</span><span class="sxs-lookup"><span data-stu-id="157c9-133">Common pitfalls and how tooavoid them</span></span>
<span data-ttu-id="157c9-134">Ahora que sabe cómo funcionan internamente colecciones confiable hello, echemos un vistazo a algunas comunes hace un uso inadecuado de ellos.</span><span class="sxs-lookup"><span data-stu-id="157c9-134">Now that you understand how hello reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="157c9-135">Ver código de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="157c9-135">See hello code below:</span></span>

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

<span data-ttu-id="157c9-136">Cuando se trabaja con un diccionario de .NET normal, puede agregar un diccionario de toohello de clave/valor y a continuación, cambie el valor de Hola de una propiedad (por ejemplo, LastLogin).</span><span class="sxs-lookup"><span data-stu-id="157c9-136">When working with a regular .NET dictionary, you can add a key/value toohello dictionary and then change hello value of a property (such as LastLogin).</span></span> <span data-ttu-id="157c9-137">Sin embargo, este código no funcionará correctamente con un diccionario confiable.</span><span class="sxs-lookup"><span data-stu-id="157c9-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="157c9-138">Recuerde de hello discusión anterior, llamada hello tooAddAsync serializa Hola clave-valor objetos toobyte matrices y, a continuación, guarda hello las matrices tooa de archivos local y también envía las réplicas secundarias de toohello.</span><span class="sxs-lookup"><span data-stu-id="157c9-138">Remember from hello earlier discussion, hello call tooAddAsync serializes hello key/value objects toobyte arrays and then saves hello arrays tooa local file and also sends them toohello secondary replicas.</span></span> <span data-ttu-id="157c9-139">Si posteriormente se cambia una propiedad, esto cambia el valor de la propiedad de hello en memoria solo; no afecta el archivo local de Hola o datos de hello enviados toohello réplicas.</span><span class="sxs-lookup"><span data-stu-id="157c9-139">If you later change a property, this changes hello property’s value in memory only; it does not impact hello local file or hello data sent toohello replicas.</span></span> <span data-ttu-id="157c9-140">Si se bloquea el proceso de hello, lo que está en la memoria se produce inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="157c9-140">If hello process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="157c9-141">Cuando se inicia un nuevo proceso o si otra réplica, se convierte en principal y, a continuación, Hola antiguo valor de propiedad es lo que está disponible.</span><span class="sxs-lookup"><span data-stu-id="157c9-141">When a new process starts or if another replica becomes primary, then hello old property value is what is available.</span></span>

<span data-ttu-id="157c9-142">No se puede efectuar esfuerzo bastante sencillo es toomake Hola tipo de error mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="157c9-142">I cannot stress enough how easy it is toomake hello kind of mistake shown above.</span></span> <span data-ttu-id="157c9-143">Y sólo aprenderá error hello cuando el proceso de hello deja de funcionar.</span><span class="sxs-lookup"><span data-stu-id="157c9-143">And, you will only learn about hello mistake if/when hello process goes down.</span></span> <span data-ttu-id="157c9-144">código de hello de toowrite de forma correcta de Hello es simplemente tooreverse Hola dos líneas:</span><span class="sxs-lookup"><span data-stu-id="157c9-144">hello correct way toowrite hello code is simply tooreverse hello two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="157c9-145">Este es otro ejemplo que muestra un error común:</span><span class="sxs-lookup"><span data-stu-id="157c9-145">Here is another example showing a common mistake:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

<span data-ttu-id="157c9-146">De nuevo, con los diccionarios de .NET normales, código de hello anterior funciona bien y es un patrón común: programador de hello usa una clave toolook un valor.</span><span class="sxs-lookup"><span data-stu-id="157c9-146">Again, with regular .NET dictionaries, hello code above works fine and is a common pattern: hello developer uses a key toolook up a value.</span></span> <span data-ttu-id="157c9-147">Si existe el valor de hello, desarrollador de hello cambia el valor de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="157c9-147">If hello value exists, hello developer changes a property’s value.</span></span> <span data-ttu-id="157c9-148">Sin embargo, con las colecciones de confianza, este código muestra hello como ya se describe el mismo problema: **no se debe modificar un objeto una vez que usted haya dado tooa confiable colección.**</span><span class="sxs-lookup"><span data-stu-id="157c9-148">However, with reliable collections, this code exhibits hello same problem as already discussed: **you MUST not modify an object once you have given it tooa reliable collection.**</span></span>

<span data-ttu-id="157c9-149">Hola correcta forma tooupdate un valor de una colección de confianza, está tooget un valor existente de referencia toohello y considere la posibilidad de referencia de objeto de hello tooby esta referencia inmutable.</span><span class="sxs-lookup"><span data-stu-id="157c9-149">hello correct way tooupdate a value in a reliable collection, is tooget a reference toohello existing value and consider hello object referred tooby this reference immutable.</span></span> <span data-ttu-id="157c9-150">A continuación, cree un nuevo objeto que es una copia exacta del objeto original Hola.</span><span class="sxs-lookup"><span data-stu-id="157c9-150">Then, create a new object which is an exact copy of hello original object.</span></span> <span data-ttu-id="157c9-151">Ahora, puede modificar el estado de Hola de este nuevo objeto y escribir nuevo objeto de hello en la colección de Hola para que se serializarán toobyte las matrices, archivo local toohello anexado y envían toohello réplicas.</span><span class="sxs-lookup"><span data-stu-id="157c9-151">Now, you can modify hello state of this new object and write hello new object into hello collection so that it gets serialized toobyte arrays, appended toohello local file and sent toohello replicas.</span></span> <span data-ttu-id="157c9-152">Después de confirmar Hola cambios, objetos en memoria caché hello, archivo local hello, y todas las réplicas de hello tienen Hola igual exacta de estado.</span><span class="sxs-lookup"><span data-stu-id="157c9-152">After committing hello change(s), hello in-memory objects, hello local file, and all hello replicas have hello same exact state.</span></span> <span data-ttu-id="157c9-153">¡Todo es correcto!</span><span class="sxs-lookup"><span data-stu-id="157c9-153">All is good!</span></span>

<span data-ttu-id="157c9-154">código de Hello siguiente muestra un valor de hello tooupdate de forma correcta en una colección confiable:</span><span class="sxs-lookup"><span data-stu-id="157c9-154">hello code below shows hello correct way tooupdate a value in a reliable collection:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a><span data-ttu-id="157c9-155">Definir los errores de programador de tooprevent de tipos de datos inmutables</span><span class="sxs-lookup"><span data-stu-id="157c9-155">Define immutable data types tooprevent programmer error</span></span>
<span data-ttu-id="157c9-156">Idealmente, nos gustaría tooreport errores del compilador de saludo cuando accidentalmente generan código que transforma el estado de un objeto que se supone tooconsider inmutable.</span><span class="sxs-lookup"><span data-stu-id="157c9-156">Ideally, we’d like hello compiler tooreport errors when you accidentally produce code that mutates state of an object that you are supposed tooconsider immutable.</span></span> <span data-ttu-id="157c9-157">Pero, compilador de C# hello no tiene Hola capacidad toodo esto.</span><span class="sxs-lookup"><span data-stu-id="157c9-157">But, hello C# compiler does not have hello ability toodo this.</span></span> <span data-ttu-id="157c9-158">Por lo tanto, tooavoid programador errores, recomendamos encarecidamente que definen tipos de Hola que se usan con tipos de colecciones confiable toobe inmutable.</span><span class="sxs-lookup"><span data-stu-id="157c9-158">So, tooavoid potential programmer bugs, we highly recommend that you define hello types you use with reliable collections toobe immutable types.</span></span> <span data-ttu-id="157c9-159">En concreto, esto significa que pegar toocore los tipos de valor (por ejemplo, números [Int32, UInt64, etc.], DateTime, Guid, TimeSpan y hello como).</span><span class="sxs-lookup"><span data-stu-id="157c9-159">Specifically, this means that you stick toocore value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and hello like).</span></span> <span data-ttu-id="157c9-160">Y, por supuesto, también puede usar String.</span><span class="sxs-lookup"><span data-stu-id="157c9-160">And, of course, you can also use String.</span></span> <span data-ttu-id="157c9-161">Es mejor propiedades de la colección de tooavoid como serializar y deserializar ellos puede con frecuencia puede afectar al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="157c9-161">It is best tooavoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="157c9-162">Sin embargo, si desea que las propiedades de la colección de toouse, se recomienda usar Hola de. La biblioteca de colecciones inmutables de red ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="157c9-162">However, if you want toouse collection properties, we highly recommend hello use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="157c9-163">Esta biblioteca está disponible para descargarse desde http://nuget.org. También se recomienda sellar las clases y establecer los campos como solo lectura siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="157c9-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="157c9-164">Hola tipo de información de usuario a continuación muestra cómo toodefine una inmutable escriba sacar partido de las recomendaciones mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="157c9-164">hello UserInfo type below demonstrates how toodefine an immutable type taking advantage of aforementioned recommendations.</span></span>

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
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

<span data-ttu-id="157c9-165">Hola ItemId tipo también es un tipo inmutable, tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="157c9-165">hello ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="157c9-166">Control de versiones de esquema (actualizaciones)</span><span class="sxs-lookup"><span data-stu-id="157c9-166">Schema versioning (upgrades)</span></span>
<span data-ttu-id="157c9-167">Internamente, Reliable Collections serializa los objetos mediante DataContractSerializer de NET.</span><span class="sxs-lookup"><span data-stu-id="157c9-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="157c9-168">Hola serializar objetos son disco local de la réplica principal de toohello persistente y también toohello transmitido réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="157c9-168">hello serialized objects are persisted toohello primary replica’s local disk and are also transmitted toohello secondary replicas.</span></span> <span data-ttu-id="157c9-169">Ya que el servicio ha evolucionado, es probable que debe tener tipo de hello toochange de datos (esquema), que el servicio requiere.</span><span class="sxs-lookup"><span data-stu-id="157c9-169">As your service matures, it’s likely you’ll want toochange hello kind of data (schema) your service requires.</span></span> <span data-ttu-id="157c9-170">Debe abordar el control de versiones de los datos con mucho cuidado.</span><span class="sxs-lookup"><span data-stu-id="157c9-170">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="157c9-171">En primer lugar y ante todo, siempre debe ser capaz de toodeserialize los datos antiguos.</span><span class="sxs-lookup"><span data-stu-id="157c9-171">First and foremost, you must always be able toodeserialize old data.</span></span> <span data-ttu-id="157c9-172">En concreto, esto significa que el código de deserialización debe ser compatible con versiones anteriores infinitamente: 333 de versión de su código de servicio debe ser capaz de toooperate en datos colocados en una colección de confianza mediante la versión 1 de su código de servicio 5 años.</span><span class="sxs-lookup"><span data-stu-id="157c9-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able toooperate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="157c9-173">Además, el código de servicio se actualiza con un dominio de actualización en cada momento.</span><span class="sxs-lookup"><span data-stu-id="157c9-173">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="157c9-174">Por lo tanto, durante una actualización, tiene dos versiones diferentes del código de servicio ejecutándose simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="157c9-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="157c9-175">Se debe evita nueva versión de hello de su código de servicio utilizan Hola nuevo esquema tal y como las versiones anteriores de su código de servicio podrían no ser el nuevo esquema de toohandle capaz de Hola.</span><span class="sxs-lookup"><span data-stu-id="157c9-175">You must avoid having hello new version of your service code use hello new schema as old versions of your service code might not be able toohandle hello new schema.</span></span> <span data-ttu-id="157c9-176">Cuando sea posible, debe diseñar cada versión de su servicio toobe compatibles con la 1 versión.</span><span class="sxs-lookup"><span data-stu-id="157c9-176">When possible, you should design each version of your service toobe forward compatible by 1 version.</span></span> <span data-ttu-id="157c9-177">En concreto, esto significa que debería poder V1 de su código de servicio toosimply omitir los elementos de esquema no controlar explícitamente.</span><span class="sxs-lookup"><span data-stu-id="157c9-177">Specifically, this means that V1 of your service code should be able toosimply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="157c9-178">Sin embargo, debe ser capaz de toosave cualquier dato no saber explícitamente y simplemente escribirlo revertir al actualizar una clave de diccionario o valor.</span><span class="sxs-lookup"><span data-stu-id="157c9-178">However, it must be able toosave any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="157c9-179">Aunque puede modificar el esquema de Hola de una clave, debe asegurarse de que el código hash de la clave y algoritmos de equals sean estables.</span><span class="sxs-lookup"><span data-stu-id="157c9-179">While you can modify hello schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="157c9-180">Si cambia cualquiera de estos algoritmos de funcionamiento, no será capaz de toolook clave Hola dentro de diccionario confiable Hola nunca más.</span><span class="sxs-lookup"><span data-stu-id="157c9-180">If you change how either of these algorithms operate, you will not be able toolook up hello key within hello reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="157c9-181">Como alternativa, puede realizar lo que se actualice el tooas que normalmente se conoce una fase 2.</span><span class="sxs-lookup"><span data-stu-id="157c9-181">Alternatively, you can perform what is typically referred tooas a 2-phase upgrade.</span></span> <span data-ttu-id="157c9-182">Con una actualización de la fase 2, actualice su servicio de V1 tooV2: V2 contiene código de hello que sabe cómo toodeal con hello nuevo cambio de esquema, pero este código no se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="157c9-182">With a 2-phase upgrade, you upgrade your service from V1 tooV2: V2 contains hello code that knows how toodeal with hello new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="157c9-183">Cuando Hola V2 código lee datos V1, funciona en él y escribe datos V1.</span><span class="sxs-lookup"><span data-stu-id="157c9-183">When hello V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="157c9-184">A continuación, una vez Hola actualización completa en todos los dominios de actualización, es posible algún modo indicar instancias en ejecución V2 toohello que Hola la actualización es completa.</span><span class="sxs-lookup"><span data-stu-id="157c9-184">Then, after hello upgrade is complete across all upgrade domains, you can somehow signal toohello running V2 instances that hello upgrade is complete.</span></span> <span data-ttu-id="157c9-185">(Una manera de toosignal es tooroll espera una actualización de la configuración; esto es lo que hace esto una actualización de la fase 2.) Ahora, instancias de hello V2 pueden leer datos de V1, convertir tooV2 datos, trabajar con ella y escribirlo como datos V2.</span><span class="sxs-lookup"><span data-stu-id="157c9-185">(One way toosignal this is tooroll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, hello V2 instances can read V1 data, convert it tooV2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="157c9-186">Si otras instancias leen datos V2, no es necesario tooconvert, que simplemente trabajar con él y escribir datos V2.</span><span class="sxs-lookup"><span data-stu-id="157c9-186">When other instances read V2 data, they do not need tooconvert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="157c9-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="157c9-187">Next Steps</span></span>
<span data-ttu-id="157c9-188">toolearn sobre la creación de contratos de datos compatible hacia delante, vea [contratos de datos compatibles con el reenvío](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="157c9-188">toolearn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="157c9-189">prácticas recomendadas de toolearn en contratos de datos de control de versiones, vea [versiones de contratos de datos](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="157c9-189">toolearn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="157c9-190">toolearn cómo los contratos de datos con tolerancia a errores de la versión de tooimplement, consulte [devoluciones de llamada de serialización tolerante a versiones](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="157c9-190">toolearn how tooimplement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="157c9-191">toolearn tooprovide una estructura de datos que puede interoperar entre varias versiones, vea [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="157c9-191">toolearn how tooprovide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
