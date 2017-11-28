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
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="9f6b4-103">Serialización de objetos de Reliable Collections en Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9f6b4-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="9f6b4-104">Las colecciones de confianza se replican y conservan su toomake de elementos que son duraderas a través de averías del equipo y las interrupciones del suministro eléctrico.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="9f6b4-105">Elementos tooreplicate y toopersist, tooserialize de las colecciones de confiable necesidad de ellos.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="9f6b4-106">Las colecciones de confiable obtener serializador adecuado de Hola para un tipo determinado desde el Administrador de estado confiable.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="9f6b4-107">Administrador de estado de confianza contiene los serializadores integrados y permite toobe serializadores personalizados registrados para un tipo determinado.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="9f6b4-108">Serializadores integrados</span><span class="sxs-lookup"><span data-stu-id="9f6b4-108">Built-in Serializers</span></span>

<span data-ttu-id="9f6b4-109">Reliable State Manager tiene serializadores integrados para algunos tipos comunes, a fin de poder serializarlos con eficacia de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="9f6b4-110">Para otros tipos, el Administrador de estado confiable vuelve ser hello toouse [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="9f6b4-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="9f6b4-111">Serializadores integrados son más eficaces, ya que saben que no se pueden cambiar sus tipos y no necesitan tooinclude información acerca de tipo hello como su nombre de tipo.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="9f6b4-112">Reliable State Manager tiene serializadores integrados para los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="9f6b4-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="9f6b4-113">Guid</span><span class="sxs-lookup"><span data-stu-id="9f6b4-113">Guid</span></span>
- <span data-ttu-id="9f6b4-114">booleano</span><span class="sxs-lookup"><span data-stu-id="9f6b4-114">bool</span></span>
- <span data-ttu-id="9f6b4-115">byte</span><span class="sxs-lookup"><span data-stu-id="9f6b4-115">byte</span></span>
- <span data-ttu-id="9f6b4-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="9f6b4-116">sbyte</span></span>
- <span data-ttu-id="9f6b4-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="9f6b4-117">byte[]</span></span>
- <span data-ttu-id="9f6b4-118">char</span><span class="sxs-lookup"><span data-stu-id="9f6b4-118">char</span></span>
- <span data-ttu-id="9f6b4-119">cadena</span><span class="sxs-lookup"><span data-stu-id="9f6b4-119">string</span></span>
- <span data-ttu-id="9f6b4-120">Decimal</span><span class="sxs-lookup"><span data-stu-id="9f6b4-120">decimal</span></span>
- <span data-ttu-id="9f6b4-121">double</span><span class="sxs-lookup"><span data-stu-id="9f6b4-121">double</span></span>
- <span data-ttu-id="9f6b4-122">float</span><span class="sxs-lookup"><span data-stu-id="9f6b4-122">float</span></span>
- <span data-ttu-id="9f6b4-123">int</span><span class="sxs-lookup"><span data-stu-id="9f6b4-123">int</span></span>
- <span data-ttu-id="9f6b4-124">uint</span><span class="sxs-lookup"><span data-stu-id="9f6b4-124">uint</span></span>
- <span data-ttu-id="9f6b4-125">long</span><span class="sxs-lookup"><span data-stu-id="9f6b4-125">long</span></span>
- <span data-ttu-id="9f6b4-126">ulong</span><span class="sxs-lookup"><span data-stu-id="9f6b4-126">ulong</span></span>
- <span data-ttu-id="9f6b4-127">short</span><span class="sxs-lookup"><span data-stu-id="9f6b4-127">short</span></span>
- <span data-ttu-id="9f6b4-128">ushort</span><span class="sxs-lookup"><span data-stu-id="9f6b4-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="9f6b4-129">Serialización personalizada</span><span class="sxs-lookup"><span data-stu-id="9f6b4-129">Custom Serialization</span></span>

<span data-ttu-id="9f6b4-130">Serializadores personalizados son datos de saludo de rendimiento o tooencrypt tooincrease usados a través de la conexión de Hola y en disco.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="9f6b4-131">Entre otras razones, serializadores personalizados son normalmente más eficaces que el serializador genérico, ya que no necesitan tooserialize información sobre el tipo de saludo.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="9f6b4-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) es tooregister usa un serializador personalizado para hello dado tipo T. Este registro debe realizarse en la construcción de Hola de hello StatefulServiceBase tooensure que antes de inicia la recuperación, todas las colecciones de confianza tienen acceso a toohello serializador relevante tooread sus datos persistentes.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

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
> <span data-ttu-id="9f6b4-133">Los serializadores personalizados tienen prioridad sobre los serializadores integrados.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="9f6b4-134">Por ejemplo, cuando se registra un serializador personalizado para int, es usado tooserialize enteros en lugar de serializador integrado de Hola para int.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="9f6b4-135">¿Cómo tooimplement un serializador personalizado</span><span class="sxs-lookup"><span data-stu-id="9f6b4-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="9f6b4-136">Un serializador personalizado necesita hello tooimplement [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interfaz.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="9f6b4-137">IStateSerializer<T> incluye una sobrecarga para escritura y lectura que usa un valor base adicional denominado T.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="9f6b4-138">Esta API se usa para la serialización diferencial.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-138">This API is for differential serialization.</span></span> <span data-ttu-id="9f6b4-139">Actualmente no se expone la característica de serialización diferencial.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="9f6b4-140">Por tanto, no se llama a estas dos sobrecargas hasta que se exponga y habilite la serialización diferencial.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="9f6b4-141">A continuación se expone un ejemplo de tipo personalizado denominado OrderKey que contiene cuatro propiedades.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="9f6b4-142">A continuación se muestra una implementación de ejemplo de IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="9f6b4-143">Tenga en cuenta que las sobrecargas de lectura y escritura que usan baseValue llaman a su sobrecarga correspondiente para compatibilidad con versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="9f6b4-144">Capacidad de actualización</span><span class="sxs-lookup"><span data-stu-id="9f6b4-144">Upgradability</span></span>
<span data-ttu-id="9f6b4-145">En un [aplicación actualización gradual](service-fabric-application-upgrade.md), actualización de hello es tooa aplicado subconjunto de nodos, un dominio de actualización a la vez.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="9f6b4-146">Durante este proceso, algunos dominios de actualización se incluirá en la versión más reciente de saludo de la aplicación y serán algunos dominios de actualización en una versión anterior de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="9f6b4-147">Durante la implementación de hello, Hola nueva versión de la aplicación debe ser capaz de tooread Hola antiguo de los datos y Hola antigua versión de la aplicación debe ser capaz de tooread Hola nueva de los datos.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="9f6b4-148">Si el formato de datos de Hola no es hacia delante y hacia atrás actualización Hola compatible, pueden producirá un error o, incluso peor, datos podría estar perdido o dañado.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="9f6b4-149">Si usas el serializador integrado, no es necesario tooworry sobre la compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="9f6b4-150">Sin embargo, si usas un serializador personalizado o hello DataContractSerializer, datos de hello toobe infinitamente hacia atrás y reenvía compatibles.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="9f6b4-151">En otras palabras, todas las versiones de serializador necesita toobe capaz de tooserialize y deserializar cualquier versión de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="9f6b4-152">Los usuarios de contrato de datos deben seguir las reglas de versiones bien definido de Hola para agregar, quitar y cambiar los campos.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="9f6b4-153">Contrato de datos también tiene compatibilidad para trabajar con campos desconocidos, enlazar con el proceso de serialización y deserialización de Hola y trabaja con herencia de clases.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="9f6b4-154">Para obtener más información, consulte [Uso de contrato de datos](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f6b4-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="9f6b4-155">Los usuarios de serializador personalizado deben respetar toohello directrices de serializador Hola usaran toomake seguro es hacia atrás y hacia delante compatible.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="9f6b4-156">Una manera común de admitir todas las versiones consiste en Agregar información de tamaño de principio de Hola y sólo agregar propiedades opcionales.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="9f6b4-157">Este modo puede leer cada versión tanta información pueda y moverse a través de la parte restante de Hola de secuencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f6b4-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f6b4-158">Next steps</span></span>
  * [<span data-ttu-id="9f6b4-159">Serialización y actualización</span><span class="sxs-lookup"><span data-stu-id="9f6b4-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="9f6b4-160">Referencia para desarrolladores de colecciones confiables</span><span class="sxs-lookup"><span data-stu-id="9f6b4-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="9f6b4-161">[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="9f6b4-162">[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f6b4-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="9f6b4-163">Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="9f6b4-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="9f6b4-164">Obtenga información acerca de cómo toouse funcionalidad avanzada al actualizar la aplicación, se hace referencia demasiado[temas avanzados](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="9f6b4-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="9f6b4-165">Solucione problemas habituales en las actualizaciones de aplicaciones, se hace referencia a pasos toohello en [solución de problemas de las actualizaciones de aplicaciones](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9f6b4-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
