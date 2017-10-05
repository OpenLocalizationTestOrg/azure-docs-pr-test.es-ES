---
title: "Serialización de objetos de Reliable Collections en Azure Service Fabric | Microsoft Docs"
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
ms.openlocfilehash: c14794b71ce7340d9e90a56d781c712e247ded06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="dc669-103">Serialización de objetos de Reliable Collections en Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dc669-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="dc669-104">Reliable Collections replica y conserva sus elementos para garantizar su durabilidad en casos de errores de equipos e interrupciones del suministro eléctrico.</span><span class="sxs-lookup"><span data-stu-id="dc669-104">Reliable Collections' replicate and persist their items to make sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="dc669-105">Tanto para la replicación como para la persistencia de elementos, Reliable Collections debe serializarlos.</span><span class="sxs-lookup"><span data-stu-id="dc669-105">Both to replicate and to persist items, Reliable Collections' need to serialize them.</span></span>

<span data-ttu-id="dc669-106">Reliable Collections obtiene de Reliable State Manager el serializador apropiado para un tipo determinado.</span><span class="sxs-lookup"><span data-stu-id="dc669-106">Reliable Collections' get the appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="dc669-107">Reliable State Manager contiene serializadores integrados y permite registrar serializadores personalizados para un tipo determinado.</span><span class="sxs-lookup"><span data-stu-id="dc669-107">Reliable State Manager contains built-in serializers and allows custom serializers to be registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="dc669-108">Serializadores integrados</span><span class="sxs-lookup"><span data-stu-id="dc669-108">Built-in Serializers</span></span>

<span data-ttu-id="dc669-109">Reliable State Manager tiene serializadores integrados para algunos tipos comunes, a fin de poder serializarlos con eficacia de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="dc669-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="dc669-110">Para los demás tipos, Reliable State Manager recurre al uso de [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="dc669-110">For other types, Reliable State Manager falls back to use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="dc669-111">Los serializadores integrados resultan más eficaces, ya que saben que sus tipos no pueden cambiar y no necesitan incluir información sobre el tipo, como el nombre de tipo.</span><span class="sxs-lookup"><span data-stu-id="dc669-111">Built-in serializers are more efficient since they know their types cannot change and they do not need to include information about the type like its type name.</span></span>

<span data-ttu-id="dc669-112">Reliable State Manager tiene serializadores integrados para los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="dc669-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="dc669-113">Guid</span><span class="sxs-lookup"><span data-stu-id="dc669-113">Guid</span></span>
- <span data-ttu-id="dc669-114">booleano</span><span class="sxs-lookup"><span data-stu-id="dc669-114">bool</span></span>
- <span data-ttu-id="dc669-115">byte</span><span class="sxs-lookup"><span data-stu-id="dc669-115">byte</span></span>
- <span data-ttu-id="dc669-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="dc669-116">sbyte</span></span>
- <span data-ttu-id="dc669-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="dc669-117">byte[]</span></span>
- <span data-ttu-id="dc669-118">char</span><span class="sxs-lookup"><span data-stu-id="dc669-118">char</span></span>
- <span data-ttu-id="dc669-119">cadena</span><span class="sxs-lookup"><span data-stu-id="dc669-119">string</span></span>
- <span data-ttu-id="dc669-120">Decimal</span><span class="sxs-lookup"><span data-stu-id="dc669-120">decimal</span></span>
- <span data-ttu-id="dc669-121">double</span><span class="sxs-lookup"><span data-stu-id="dc669-121">double</span></span>
- <span data-ttu-id="dc669-122">float</span><span class="sxs-lookup"><span data-stu-id="dc669-122">float</span></span>
- <span data-ttu-id="dc669-123">int</span><span class="sxs-lookup"><span data-stu-id="dc669-123">int</span></span>
- <span data-ttu-id="dc669-124">uint</span><span class="sxs-lookup"><span data-stu-id="dc669-124">uint</span></span>
- <span data-ttu-id="dc669-125">long</span><span class="sxs-lookup"><span data-stu-id="dc669-125">long</span></span>
- <span data-ttu-id="dc669-126">ulong</span><span class="sxs-lookup"><span data-stu-id="dc669-126">ulong</span></span>
- <span data-ttu-id="dc669-127">short</span><span class="sxs-lookup"><span data-stu-id="dc669-127">short</span></span>
- <span data-ttu-id="dc669-128">ushort</span><span class="sxs-lookup"><span data-stu-id="dc669-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="dc669-129">Serialización personalizada</span><span class="sxs-lookup"><span data-stu-id="dc669-129">Custom Serialization</span></span>

<span data-ttu-id="dc669-130">Los serializadores personalizados se usan normalmente para aumentar el rendimiento o para cifrar los datos en la red y en disco.</span><span class="sxs-lookup"><span data-stu-id="dc669-130">Custom serializers are commonly used to increase performance or to encrypt the data over the wire and on disk.</span></span> <span data-ttu-id="dc669-131">Entre otras razones, los serializadores personalizados suelen ser más eficaces que el serializador genérico, ya que no necesitan serializar la información sobre el tipo.</span><span class="sxs-lookup"><span data-stu-id="dc669-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need to serialize information about the type.</span></span> 

<span data-ttu-id="dc669-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) se usa para registrar un serializador personalizado para un tipo determinado T. Este registro suele realizarse para la compilación de StatefulServiceBase, a fin de garantizar que, antes de que empiece la recuperación, todos los elementos de Reliable Collections puedan acceder al serializador pertinente para leer los datos persistentes.</span><span class="sxs-lookup"><span data-stu-id="dc669-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used to register a custom serializer for the given type T. This registration should happen in the construction of the StatefulServiceBase to ensure that before recovery starts, all Reliable Collections have access to the relevant serializer to read their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed to set OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="dc669-133">Los serializadores personalizados tienen prioridad sobre los serializadores integrados.</span><span class="sxs-lookup"><span data-stu-id="dc669-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="dc669-134">Por ejemplo, cuando se registra un serializador personalizado para int, este se usa para serializar enteros en lugar del serializador integrado para int.</span><span class="sxs-lookup"><span data-stu-id="dc669-134">For example, when a custom serializer for int is registered, it is used to serialize integers instead of the built-in serializer for int.</span></span>

### <a name="how-to-implement-a-custom-serializer"></a><span data-ttu-id="dc669-135">Cómo implementar un serializador personalizado</span><span class="sxs-lookup"><span data-stu-id="dc669-135">How to implement a custom serializer</span></span>

<span data-ttu-id="dc669-136">Un serializador personalizado debe implementar la interfaz [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1).</span><span class="sxs-lookup"><span data-stu-id="dc669-136">A custom serializer needs to implement the [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="dc669-137">IStateSerializer<T> incluye una sobrecarga para escritura y lectura que usa un valor base adicional denominado T.</span><span class="sxs-lookup"><span data-stu-id="dc669-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="dc669-138">Esta API se usa para la serialización diferencial.</span><span class="sxs-lookup"><span data-stu-id="dc669-138">This API is for differential serialization.</span></span> <span data-ttu-id="dc669-139">Actualmente no se expone la característica de serialización diferencial.</span><span class="sxs-lookup"><span data-stu-id="dc669-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="dc669-140">Por tanto, no se llama a estas dos sobrecargas hasta que se exponga y habilite la serialización diferencial.</span><span class="sxs-lookup"><span data-stu-id="dc669-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="dc669-141">A continuación se expone un ejemplo de tipo personalizado denominado OrderKey que contiene cuatro propiedades.</span><span class="sxs-lookup"><span data-stu-id="dc669-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="dc669-142">A continuación se muestra una implementación de ejemplo de IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="dc669-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="dc669-143">Tenga en cuenta que las sobrecargas de lectura y escritura que usan baseValue llaman a su sobrecarga correspondiente para compatibilidad con versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="dc669-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="dc669-144">Capacidad de actualización</span><span class="sxs-lookup"><span data-stu-id="dc669-144">Upgradability</span></span>
<span data-ttu-id="dc669-145">En una [actualización de la aplicación gradual](service-fabric-application-upgrade.md), la actualización se aplica a un subconjunto de nodos, un dominio de actualización a la vez.</span><span class="sxs-lookup"><span data-stu-id="dc669-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), the upgrade is applied to a subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="dc669-146">Durante este proceso, algunos dominios de actualización se incluirán en la versión más reciente de su aplicación, mientras que otros estarán en la versión anterior.</span><span class="sxs-lookup"><span data-stu-id="dc669-146">During this process, some upgrade domains will be on the newer version of your application, and some upgrade domains will be on the older version of your application.</span></span> <span data-ttu-id="dc669-147">Durante el lanzamiento, la nueva versión de la aplicación debe poder leer la versión anterior de sus datos, mientras que la versión anterior debe poder leer la nueva versión.</span><span class="sxs-lookup"><span data-stu-id="dc669-147">During the rollout, the new version of your application must be able to read the old version of your data, and the old version of your application must be able to read the new version of your data.</span></span> <span data-ttu-id="dc669-148">Si el formato de datos no es compatible con las versiones anteriores y nuevas, es posible que se produzca un error en la actualización, o lo que es peor, que se pierdan o dañen datos.</span><span class="sxs-lookup"><span data-stu-id="dc669-148">If the data format is not forward and backward compatible, the upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="dc669-149">Si usa el serializador integrado, no tiene que preocuparse por la cuestión de la compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="dc669-149">If you are using  built-in serializer, you do not have to worry about compatibility.</span></span>
<span data-ttu-id="dc669-150">No obstante, si usa un serializador personalizado o DataContractSerializer, los datos deben ser siempre compatibles con versiones anteriores y posteriores.</span><span class="sxs-lookup"><span data-stu-id="dc669-150">However, if you are using a custom serializer or the DataContractSerializer, the data have to be infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="dc669-151">En otras palabras, todas las versiones del serializador deben tener la capacidad de serializar y deserializar cualquier versión del tipo.</span><span class="sxs-lookup"><span data-stu-id="dc669-151">In other words, each version of serializer needs to be able to serialize and de-serialize any version of the type.</span></span>

<span data-ttu-id="dc669-152">Los usuarios con contrato de datos deben seguir reglas de versiones bien definidas para agregar, quitar y cambiar campos.</span><span class="sxs-lookup"><span data-stu-id="dc669-152">Data Contract users should follow the well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="dc669-153">El contrato de datos también tiene compatibilidad para tratar con campos desconocidos, enlazar con el proceso de serialización y deserialización, y para tratar con la herencia de clases.</span><span class="sxs-lookup"><span data-stu-id="dc669-153">Data Contract also has support for dealing with unknown fields, hooking into the serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="dc669-154">Para obtener más información, consulte [Uso de contrato de datos](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc669-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="dc669-155">Los usuarios de serializadores personalizados deben atenerse a los criterios del serializador que usan, a fin de garantizar la compatibilidad con versiones anteriores y posteriores.</span><span class="sxs-lookup"><span data-stu-id="dc669-155">Custom serializer users should adhere to the guidelines of the serializer they are using to make sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="dc669-156">Una manera común de admitir todas las versiones es agregar información sobre el tamaño al principio y solo agregar propiedades opcionales.</span><span class="sxs-lookup"><span data-stu-id="dc669-156">Common way of supporting all versions is adding size information at the beginning and only adding optional properties.</span></span>
<span data-ttu-id="dc669-157">De esta forma, cada versión puede leer todo lo posible y saltar por la parte restante de la secuencia.</span><span class="sxs-lookup"><span data-stu-id="dc669-157">This way each version can read as much it can and jump over the remaining part of the stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc669-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc669-158">Next steps</span></span>
  * [<span data-ttu-id="dc669-159">Serialización y actualización</span><span class="sxs-lookup"><span data-stu-id="dc669-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="dc669-160">Referencia para desarrolladores de colecciones confiables</span><span class="sxs-lookup"><span data-stu-id="dc669-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="dc669-161">[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc669-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="dc669-162">[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc669-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="dc669-163">Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="dc669-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="dc669-164">Aprenda a usar funcionalidades avanzadas para actualizar una aplicación. Para ello, consulte los [temas avanzados](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="dc669-164">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="dc669-165">Solucione problemas habituales en las actualizaciones de aplicaciones consultando los pasos que figuran en [Solución de problemas de las actualizaciones de aplicaciones](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="dc669-165">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
