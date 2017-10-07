---
title: "serialización de objetos de colección en Azure Service Fabric aaaReliable | Documentos de Microsoft"
description: "Serialización de objetos de Reliable Collections en Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Serialización de objetos de Reliable Collections en Azure Service Fabric
Las colecciones de confianza se replican y conservan su toomake de elementos que son duraderas a través de averías del equipo y las interrupciones del suministro eléctrico.
Elementos tooreplicate y toopersist, tooserialize de las colecciones de confiable necesidad de ellos.

Las colecciones de confiable obtener serializador adecuado de Hola para un tipo determinado desde el Administrador de estado confiable.
Administrador de estado de confianza contiene los serializadores integrados y permite toobe serializadores personalizados registrados para un tipo determinado.

## <a name="built-in-serializers"></a>Serializadores integrados

Reliable State Manager tiene serializadores integrados para algunos tipos comunes, a fin de poder serializarlos con eficacia de forma predeterminada. Para otros tipos, el Administrador de estado confiable vuelve ser hello toouse [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).
Serializadores integrados son más eficaces, ya que saben que no se pueden cambiar sus tipos y no necesitan tooinclude información acerca de tipo hello como su nombre de tipo.

Reliable State Manager tiene serializadores integrados para los siguientes tipos: 
- Guid
- booleano
- byte
- sbyte
- byte[]
- char
- cadena
- Decimal
- double
- float
- int
- uint
- long
- ulong
- short
- ushort

## <a name="custom-serialization"></a>Serialización personalizada

Serializadores personalizados son datos de saludo de rendimiento o tooencrypt tooincrease usados a través de la conexión de Hola y en disco. Entre otras razones, serializadores personalizados son normalmente más eficaces que el serializador genérico, ya que no necesitan tooserialize información sobre el tipo de saludo. 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) es tooregister usa un serializador personalizado para hello dado tipo T. Este registro debe realizarse en la construcción de Hola de hello StatefulServiceBase tooensure que antes de inicia la recuperación, todas las colecciones de confianza tienen acceso a toohello serializador relevante tooread sus datos persistentes.

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> Los serializadores personalizados tienen prioridad sobre los serializadores integrados. Por ejemplo, cuando se registra un serializador personalizado para int, es usado tooserialize enteros en lugar de serializador integrado de Hola para int.

### <a name="how-tooimplement-a-custom-serializer"></a>¿Cómo tooimplement un serializador personalizado

Un serializador personalizado necesita hello tooimplement [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interfaz.

> [!NOTE]
> IStateSerializer<T> incluye una sobrecarga para escritura y lectura que usa un valor base adicional denominado T. Esta API se usa para la serialización diferencial. Actualmente no se expone la característica de serialización diferencial. Por tanto, no se llama a estas dos sobrecargas hasta que se exponga y habilite la serialización diferencial.

A continuación se expone un ejemplo de tipo personalizado denominado OrderKey que contiene cuatro propiedades.

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

A continuación se muestra una implementación de ejemplo de IStateSerializer<OrderKey>.
Tenga en cuenta que las sobrecargas de lectura y escritura que usan baseValue llaman a su sobrecarga correspondiente para compatibilidad con versiones posteriores.

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a>Capacidad de actualización
En un [aplicación actualización gradual](service-fabric-application-upgrade.md), actualización de hello es tooa aplicado subconjunto de nodos, un dominio de actualización a la vez. Durante este proceso, algunos dominios de actualización se incluirá en la versión más reciente de saludo de la aplicación y serán algunos dominios de actualización en una versión anterior de la aplicación hello. Durante la implementación de hello, Hola nueva versión de la aplicación debe ser capaz de tooread Hola antiguo de los datos y Hola antigua versión de la aplicación debe ser capaz de tooread Hola nueva de los datos. Si el formato de datos de Hola no es hacia delante y hacia atrás actualización Hola compatible, pueden producirá un error o, incluso peor, datos podría estar perdido o dañado.

Si usas el serializador integrado, no es necesario tooworry sobre la compatibilidad.
Sin embargo, si usas un serializador personalizado o hello DataContractSerializer, datos de hello toobe infinitamente hacia atrás y reenvía compatibles.
En otras palabras, todas las versiones de serializador necesita toobe capaz de tooserialize y deserializar cualquier versión de tipo hello.

Los usuarios de contrato de datos deben seguir las reglas de versiones bien definido de Hola para agregar, quitar y cambiar los campos. Contrato de datos también tiene compatibilidad para trabajar con campos desconocidos, enlazar con el proceso de serialización y deserialización de Hola y trabaja con herencia de clases. Para obtener más información, consulte [Uso de contrato de datos](https://msdn.microsoft.com/library/ms733127.aspx).

Los usuarios de serializador personalizado deben respetar toohello directrices de serializador Hola usaran toomake seguro es hacia atrás y hacia delante compatible.
Una manera común de admitir todas las versiones consiste en Agregar información de tamaño de principio de Hola y sólo agregar propiedades opcionales.
Este modo puede leer cada versión tanta información pueda y moverse a través de la parte restante de Hola de secuencia de Hola.

## <a name="next-steps"></a>Pasos siguientes
  * [Serialización y actualización](service-fabric-application-upgrade-data-serialization.md)
  * [Referencia para desarrolladores de colecciones confiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.
  * [actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.
  * Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).
  * Obtenga información acerca de cómo toouse funcionalidad avanzada al actualizar la aplicación, se hace referencia demasiado[temas avanzados](service-fabric-application-upgrade-advanced.md).
  * Solucione problemas habituales en las actualizaciones de aplicaciones, se hace referencia a pasos toohello en [solución de problemas de las actualizaciones de aplicaciones](service-fabric-application-upgrade-troubleshooting.md).
