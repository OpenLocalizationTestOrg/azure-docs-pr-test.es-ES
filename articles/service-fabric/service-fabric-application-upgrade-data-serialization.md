---
title: "Actualización de la aplicación: serialización de datos| Microsoft Docs"
description: "Prácticas recomendadas para la serialización de datos y cómo afectan a las sucesivas actualizaciones de la aplicación."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>Información sobre cómo la serialización afecta a una actualización de aplicación
En un [aplicación actualización gradual](service-fabric-application-upgrade.md), actualización de hello es tooa aplicado subconjunto de nodos, un dominio de actualización a la vez. Durante este proceso, algunos dominios de actualización están en la versión más reciente de saludo de la aplicación y algunos dominios de actualización están en una versión anterior de la aplicación hello. Durante la implementación de hello, Hola nueva versión de la aplicación debe ser capaz de tooread Hola antiguo de los datos y Hola antigua versión de la aplicación debe ser capaz de tooread Hola nueva de los datos. Si el formato de datos de Hola no es hacia delante y hacia atrás actualización Hola compatible, pueden producirá un error o, incluso peor, datos podría estar perdido o dañado. En este artículo se analiza qué constituye su formato de datos y ofrece prácticas recomendadas para garantizar que sus datos sean compatibles con las versiones anteriores y nuevas.

## <a name="what-makes-up-your-data-format"></a>¿Qué conforma su formato de datos?
En Azure Service Fabric, datos de Hola que se guardan y se replican proceden de las clases de C#. Para las aplicaciones que utilizan [colecciones confiable](service-fabric-reliable-services-reliable-collections.md), que los datos son objetos de hello en diccionarios confiable de Hola y colas. Para las aplicaciones que utilizan [Reliable Actors](service-fabric-reliable-actors-introduction.md), es decir Hola realizar una copia de estado de actor Hola. Estas clases de C# deben ser serializables toobe conservarse y replicarse. Por lo tanto, el formato de datos de Hola se define mediante Hola campos y propiedades que se serializan, así como el modo en se serializan. Por ejemplo, en un `IReliableDictionary<int, MyClass>` datos hello están un número de serie `int` y un número de serie `MyClass`.

### <a name="code-changes-that-result-in-a-data-format-change"></a>Cambios de código que dan como resultado un cambio de formato de datos
Puesto que el formato de datos de hello viene determinado por las clases de C#, las clases de toohello de cambios pueden producir un cambio de formato de datos. Se debe tener cuidado tooensure que pueda controlar una actualización gradual cambio de formato de datos de Hola. Ejemplos que pueden provocar cambios del formato de datos:

* Adición o eliminación de campos o propiedades
* Cambio de nombre de campos o propiedades
* Cambiar los tipos de Hola de campos o propiedades
* Cambiar el nombre de clase de Hola o espacio de nombres

### <a name="data-contract-as-hello-default-serializer"></a>Contrato de datos como Hola serializador predeterminado
serializador de Hello es suele ser responsable de leer los datos de Hola y deserializar en la versión actual de hello, incluso si los datos de hello están en una anterior o *más reciente* versión. Hello serializador predeterminado es hello [serializador de contrato de datos](https://msdn.microsoft.com/library/ms733127.aspx), que tiene reglas de control de versiones bien definido. Colecciones confiables permiten Hola serializador toobe que se reemplaza, pero Reliable Actors actualmente no tienen que serlo. serializador de datos de Hello desempeña un papel importante en la habilitación de las actualizaciones sucesivas. serializador de contrato de datos de Hello es serializador Hola que se recomienda para las aplicaciones de Service Fabric.

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Cómo afecta el formato de datos de Hola a una actualización gradual
Durante una actualización gradual, hay dos escenarios principales donde serializador Hola puede encontrar un más antiguo o *más reciente* versión de los datos:

1. Después de que un nodo se actualiza y copia de seguridad se inicia, serializador nuevo Hola cargará los datos de Hola que estaba toodisk persistente por la versión anterior de Hola.
2. Durante la actualización gradual de hello, clúster de hello contienen una mezcla de versiones de hello antigua y nueva del código. Dado que las réplicas pueden colocarse en diferentes dominios de actualización y las réplicas envían datos tooeach otras hello nuevo o antiguo versión de los datos se puede encontrar por versión de Hola nuevo o antiguo del serializador.

> [!NOTE]
> Hola "nueva versión" y "versión antigua" aquí, consulte toohello versión del código que se está ejecutando. Hola "serializador nuevo" refiere toohello código de serializador que se está ejecutando en la nueva versión de hello de la aplicación. Hola "nuevos datos" hace referencia a clase C# toohello serializado de nueva versión de hello de la aplicación.
> 
> 

Hola dos versiones del código y el formato de datos debe ser hacia delante y hacia atrás compatible. Si no son compatibles, puede producir un error en la actualización gradual de Hola o se podrían perder datos. Hola actualización gradual puede producir un error debido a código de hello o serializador puede producir excepciones o un error cuando encuentra Hola otra versión. Si, por ejemplo, se ha agregado una nueva propiedad pero serializador antiguo Hola lo descarta durante la deserialización, podrían perderse datos.

Contrato de datos es hello recomendada soluciones para garantizar que los datos sean compatibles. Tiene reglas de versiones bien definidas para agregar, quitar y cambiar campos. También tiene compatibilidad para trabajar con campos desconocidos, enlazar con el proceso de serialización y deserialización de Hola y trabaja con herencia de clases. Para obtener más información, consulte [Uso de contrato de datos](https://msdn.microsoft.com/library/ms733127.aspx).

## <a name="next-steps"></a>Pasos siguientes
[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.

[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.

Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).

Obtenga información acerca de cómo toouse funcionalidad avanzada al actualizar la aplicación, se hace referencia demasiado[temas avanzados](service-fabric-application-upgrade-advanced.md).

Solucione problemas habituales en las actualizaciones de aplicaciones, se hace referencia a pasos toohello en [solución de problemas de las actualizaciones de aplicaciones ](service-fabric-application-upgrade-troubleshooting.md).

