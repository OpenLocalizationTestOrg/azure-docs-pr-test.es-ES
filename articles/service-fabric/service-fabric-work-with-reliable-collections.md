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
# <a name="working-with-reliable-collections"></a>Trabajo con Reliable Collections
Service Fabric ofrece un con estado a los desarrolladores de modelo too.NET disponible a través de colecciones confiable de programación. En concreto, Service Fabric proporciona un diccionario confiable y clases de cola confiables. Al utilizar estas clases, se crean particiones en el estado (para escalabilidad) y este se replica (para disponibilidad) y se tramita dentro de una partición (para semántica ACID). Veamos un uso típico de un objeto de diccionario confiable y vea lo que está haciendo realmente.

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

Todas las operaciones en objetos de diccionario confiables (excepto ClearAsync, que no se puede deshacer), requieren un objeto ITransaction. Este objeto tiene asociado ningún y todos los cambios que está intentando toomake tooany confiable diccionario u objetos de cola confiable dentro de una sola partición. Adquirir un ITransaction objeto mediante una llamada a la partición de hello del método de CreateTransaction del StateManager.

En el código de hello anterior, el objeto de ITransaction de Hola se pasa método de AddAsync del diccionario de tooa confiable. Internamente, los métodos de diccionario que acepta una clave toman un bloqueo de lector/escritor asociado con la clave de Hola. Si el método hello modifica el valor de la clave de hello, método hello toma un bloqueo de escritura en la clave de Hola y si método hello solo lee desde el valor de la clave de hello, a continuación, se realiza un bloqueo de lectura en clave de Hola. Puesto que AddAsync modifica toohello del valor de la clave de hello nueva, se toma valor pasado como parámetro, bloqueo de escritura de la clave de Hola. Por lo tanto, si los subprocesos de 2 (o más) intentan tooadd valores con hello misma clave en hello mismo tiempo, un subproceso adquirirá el bloqueo de escritura de Hola y Hola otros subprocesos se bloquean. De forma predeterminada, un bloque de métodos para el bloqueo de too4 segundos tooacquire Hola; Después de 4 segundos, métodos de hello lanzan una excepción TimeoutException. Sobrecargas de método existen permitiendo toopass un valor de tiempo de espera explícito si prefiere.

Por lo general, se escribe los tooa de tooreact código TimeoutException capturarla y volver a intentar la operación completa de hello (como se muestra en el código de hello anterior). En mi sencillo código, simplemente llamo a Task.Delay pasando 100 milisegundos cada vez. Sin embargo, en realidad, podría ser mejor usar algún tipo de retraso de interrupción exponencial en su lugar.

Una vez que se adquiere el bloqueo de hello, AddAsync agrega la clave de Hola y tooan diccionario temporal interno asociado Hola ITransaction objeto hace referencia a objeto de valor. Esto se hace tooprovide con semántica de lectura your-posee-escrituras. Es decir, después de llamar a AddAsync, un tooTryGetValueAsync llamada posterior (usando Hola el mismo objeto ITransaction) devolverá el valor de hello incluso si aún no hayan confirmado la transacción de Hola. A continuación, AddAsync serializa su clave y valor toobyte matrices de objetos y anexa estos archivo de registro de tooa de matrices de bytes en el nodo local Hola. Por último, AddAsync envía Hola bytes matrices tooall Hola réplicas secundarias para que haya Hola misma información de clave/valor. Aunque la información de clave/valor Hola se ha escrito el archivo de registro tooa, información de hello no se considera parte del diccionario de hello hasta que la transacción de Hola que están asociadas se ha confirmado.

En el código de hello anterior, Hola llamada tooCommitAsync confirma todas las operaciones de la transacción de Hola de. En concreto, anexa el archivo de registro de toohello de información de confirmación en el nodo local hello y también envía Hola réplicas secundarias de confirmación tooall registro Hola. Una vez que ha respondido un quórum (mayoría) de réplicas de hello, todos los datos se consideran cambios permanentes y los bloqueos asociados con las claves que se manipulación a través del objeto de ITransaction Hola se liberan para otras transacciones de subprocesos puede manipular Hola mismas claves y sus valores.

Si no se llama a CommitAsync (normalmente debido a que se produzca una excepción de tooan), objeto de ITransaction de hello obtiene eliminado. Al desechar un objeto de ITransaction sin confirmar, Service Fabric anexa el archivo de registro de anulación información toohello del nodo local y es necesario toobe ninguna acción envían tooany de hello las réplicas secundarias. Y, a continuación, se liberan los bloqueos asociados con las claves que se manipulación a través de la transacción de Hola.

## <a name="common-pitfalls-and-how-tooavoid-them"></a>Los errores comunes y cómo tooavoid ellos
Ahora que sabe cómo funcionan internamente colecciones confiable hello, echemos un vistazo a algunas comunes hace un uso inadecuado de ellos. Ver código de hello siguiente:

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

Cuando se trabaja con un diccionario de .NET normal, puede agregar un diccionario de toohello de clave/valor y a continuación, cambie el valor de Hola de una propiedad (por ejemplo, LastLogin). Sin embargo, este código no funcionará correctamente con un diccionario confiable. Recuerde de hello discusión anterior, llamada hello tooAddAsync serializa Hola clave-valor objetos toobyte matrices y, a continuación, guarda hello las matrices tooa de archivos local y también envía las réplicas secundarias de toohello. Si posteriormente se cambia una propiedad, esto cambia el valor de la propiedad de hello en memoria solo; no afecta el archivo local de Hola o datos de hello enviados toohello réplicas. Si se bloquea el proceso de hello, lo que está en la memoria se produce inmediatamente. Cuando se inicia un nuevo proceso o si otra réplica, se convierte en principal y, a continuación, Hola antiguo valor de propiedad es lo que está disponible.

No se puede efectuar esfuerzo bastante sencillo es toomake Hola tipo de error mostrado anteriormente. Y sólo aprenderá error hello cuando el proceso de hello deja de funcionar. código de hello de toowrite de forma correcta de Hello es simplemente tooreverse Hola dos líneas:


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

Este es otro ejemplo que muestra un error común:

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

De nuevo, con los diccionarios de .NET normales, código de hello anterior funciona bien y es un patrón común: programador de hello usa una clave toolook un valor. Si existe el valor de hello, desarrollador de hello cambia el valor de la propiedad. Sin embargo, con las colecciones de confianza, este código muestra hello como ya se describe el mismo problema: **no se debe modificar un objeto una vez que usted haya dado tooa confiable colección.**

Hola correcta forma tooupdate un valor de una colección de confianza, está tooget un valor existente de referencia toohello y considere la posibilidad de referencia de objeto de hello tooby esta referencia inmutable. A continuación, cree un nuevo objeto que es una copia exacta del objeto original Hola. Ahora, puede modificar el estado de Hola de este nuevo objeto y escribir nuevo objeto de hello en la colección de Hola para que se serializarán toobyte las matrices, archivo local toohello anexado y envían toohello réplicas. Después de confirmar Hola cambios, objetos en memoria caché hello, archivo local hello, y todas las réplicas de hello tienen Hola igual exacta de estado. ¡Todo es correcto!

código de Hello siguiente muestra un valor de hello tooupdate de forma correcta en una colección confiable:

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

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>Definir los errores de programador de tooprevent de tipos de datos inmutables
Idealmente, nos gustaría tooreport errores del compilador de saludo cuando accidentalmente generan código que transforma el estado de un objeto que se supone tooconsider inmutable. Pero, compilador de C# hello no tiene Hola capacidad toodo esto. Por lo tanto, tooavoid programador errores, recomendamos encarecidamente que definen tipos de Hola que se usan con tipos de colecciones confiable toobe inmutable. En concreto, esto significa que pegar toocore los tipos de valor (por ejemplo, números [Int32, UInt64, etc.], DateTime, Guid, TimeSpan y hello como). Y, por supuesto, también puede usar String. Es mejor propiedades de la colección de tooavoid como serializar y deserializar ellos puede con frecuencia puede afectar al rendimiento. Sin embargo, si desea que las propiedades de la colección de toouse, se recomienda usar Hola de. La biblioteca de colecciones inmutables de red ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)). Esta biblioteca está disponible para descargarse desde http://nuget.org. También se recomienda sellar las clases y establecer los campos como solo lectura siempre que sea posible.

Hola tipo de información de usuario a continuación muestra cómo toodefine una inmutable escriba sacar partido de las recomendaciones mencionado anteriormente.

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

Hola ItemId tipo también es un tipo inmutable, tal y como se muestra aquí:

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

## <a name="schema-versioning-upgrades"></a>Control de versiones de esquema (actualizaciones)
Internamente, Reliable Collections serializa los objetos mediante DataContractSerializer de NET. Hola serializar objetos son disco local de la réplica principal de toohello persistente y también toohello transmitido réplicas secundarias. Ya que el servicio ha evolucionado, es probable que debe tener tipo de hello toochange de datos (esquema), que el servicio requiere. Debe abordar el control de versiones de los datos con mucho cuidado. En primer lugar y ante todo, siempre debe ser capaz de toodeserialize los datos antiguos. En concreto, esto significa que el código de deserialización debe ser compatible con versiones anteriores infinitamente: 333 de versión de su código de servicio debe ser capaz de toooperate en datos colocados en una colección de confianza mediante la versión 1 de su código de servicio 5 años.

Además, el código de servicio se actualiza con un dominio de actualización en cada momento. Por lo tanto, durante una actualización, tiene dos versiones diferentes del código de servicio ejecutándose simultáneamente. Se debe evita nueva versión de hello de su código de servicio utilizan Hola nuevo esquema tal y como las versiones anteriores de su código de servicio podrían no ser el nuevo esquema de toohandle capaz de Hola. Cuando sea posible, debe diseñar cada versión de su servicio toobe compatibles con la 1 versión. En concreto, esto significa que debería poder V1 de su código de servicio toosimply omitir los elementos de esquema no controlar explícitamente. Sin embargo, debe ser capaz de toosave cualquier dato no saber explícitamente y simplemente escribirlo revertir al actualizar una clave de diccionario o valor.

> [!WARNING]
> Aunque puede modificar el esquema de Hola de una clave, debe asegurarse de que el código hash de la clave y algoritmos de equals sean estables. Si cambia cualquiera de estos algoritmos de funcionamiento, no será capaz de toolook clave Hola dentro de diccionario confiable Hola nunca más.
>
>

Como alternativa, puede realizar lo que se actualice el tooas que normalmente se conoce una fase 2. Con una actualización de la fase 2, actualice su servicio de V1 tooV2: V2 contiene código de hello que sabe cómo toodeal con hello nuevo cambio de esquema, pero este código no se ejecuta. Cuando Hola V2 código lee datos V1, funciona en él y escribe datos V1. A continuación, una vez Hola actualización completa en todos los dominios de actualización, es posible algún modo indicar instancias en ejecución V2 toohello que Hola la actualización es completa. (Una manera de toosignal es tooroll espera una actualización de la configuración; esto es lo que hace esto una actualización de la fase 2.) Ahora, instancias de hello V2 pueden leer datos de V1, convertir tooV2 datos, trabajar con ella y escribirlo como datos V2. Si otras instancias leen datos V2, no es necesario tooconvert, que simplemente trabajar con él y escribir datos V2.

## <a name="next-steps"></a>Pasos siguientes
toolearn sobre la creación de contratos de datos compatible hacia delante, vea [contratos de datos compatibles con el reenvío](https://msdn.microsoft.com/library/ms731083.aspx).

prácticas recomendadas de toolearn en contratos de datos de control de versiones, vea [versiones de contratos de datos](https://msdn.microsoft.com/library/ms731138.aspx).

toolearn cómo los contratos de datos con tolerancia a errores de la versión de tooimplement, consulte [devoluciones de llamada de serialización tolerante a versiones](https://msdn.microsoft.com/library/ms733734.aspx).

toolearn tooprovide una estructura de datos que puede interoperar entre varias versiones, vea [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).
