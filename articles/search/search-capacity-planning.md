---
title: "aaaCapacity planificación para la búsqueda de Azure | Documentos de Microsoft"
description: "Ajuste los recursos de proceso de réplica y partición en Azure Search, donde el precio de cada recurso se basa en unidades de búsqueda facturables."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>Escalado de niveles de recursos para cargas de trabajo de indexación y consulta en Búsqueda de Azure
Después de [elegir un nivel de precios](search-sku-tier.md) y [aprovisionar un servicio de búsqueda](search-create-service-portal.md), Hola siguiente paso es el número de hello toooptionally aumento de las réplicas o particiones utilizadas por el servicio. Cada nivel ofrece un número fijo de unidades de facturación. Este artículo se explica cómo tooallocate esos tooachieve unidades una configuración óptima que equilibra los requisitos para la ejecución de la consulta, indización y almacenamiento.

Configuración de recursos está disponible al configurar un servicio en hello [nivel básico](http://aka.ms/azuresearchbasic) o uno de hello [niveles estándares](search-limits-quotas-capacity.md). Para servicios facturables en estos niveles, la capacidad se adquiere en incrementos de *unidades de búsqueda* (SU), en las que cada partición y réplica cuentan como una SU. 

Uso de menos SU da lugar a una factura proporcionalmente menor. La facturación está en vigor para siempre y cuando se configura el servicio de Hola. Si no usa temporalmente un servicio, la única manera de hello tooavoid facturación está eliminando el servicio de hello y, a continuación, volver a crearlo cuando lo necesite.

> [!Note]
> La eliminación de un servicio supone la eliminación de todo su contenido. Azure Search no dispone de ningún recurso para realizar copias de seguridad de datos de búsqueda persistentes ni para restaurarlos. tooredeploy un índice existente en un nuevo servicio, debe ejecutar Hola programa utilizado toocreate y cargarlo originalmente. 

## <a name="terminology-partitions-and-replicas"></a>Terminología: particiones y réplicas
Particiones y réplicas son recursos principales Hola hacer copia de un servicio de búsqueda.

| Recurso | Definición |
|----------|------------|
|*Particiones* | Proporciona almacenamiento de índices y E/S para realizar operaciones de lectura y escritura (por ejemplo, volver a generar o actualizar un índice).|
|*Réplicas* | Las instancias de servicio de búsqueda de hello, utilizan principalmente tooload equilibrar las operaciones de consulta. Cada réplica siempre hospeda una copia de un índice. Si tiene 12 réplicas, tendrá 12 copias de todos los índices cargado en el servicio de Hola.|

> [!NOTE]
> No hay ninguna manera toodirectly manipular o administrar los índices que se ejecutan en una réplica. Una copia de cada índice en cada réplica forma parte de la arquitectura de servicio de Hola.
>

## <a name="how-tooallocate-partitions-and-replicas"></a>¿Cómo tooallocate particiones y réplicas
En Búsqueda de Azure, un servicio se asigna inicialmente a un nivel mínimo de recursos que consta de una partición y una réplica. En los niveles donde se admita, puede ajustar de forma incremental los recursos informáticos aumentando las particiones si necesita más almacenamiento y E/S, o bien agregue réplicas para mejorar el rendimiento y aumentar los volúmenes de las consultas. Un único servicio debe tener suficientes toohandle recursos todas las cargas de trabajo (indización y las búsquedas). No se pueden subdividir las cargas de trabajo entre varios servicios.

tooincrease o cambiar la asignación de Hola de réplicas y particiones, se recomienda utilizar Hola portal de Azure. portal de Hello impone límites en combinaciones permitidas que permanecen por debajo de los límites máximos:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) y seleccione el servicio de búsqueda de Hola.
2. En **configuración**, abra hello **escala** hoja y uso Hola tooincrease controles deslizantes o reducir el número de Hola de particiones y réplicas.

Si necesita un sistema de aprovisionamiento basado en código o script, Hola [API de REST de administración](https://msdn.microsoft.com/library/azure/dn832687.aspx) es un portal toohello alternativo.

Por lo general, las aplicaciones de búsqueda necesitan más réplicas que particiones, sobre todo cuando las operaciones de servicio de Hola se inclina hacia las cargas de trabajo de la consulta. Hola sección en [alta disponibilidad](#HA) explica por qué.

> [!NOTE]
> Después de aprovisionar un servicio, no puede ser actualizada tooa SKU superior. Necesitará toocreate un servicio de búsqueda en el nuevo nivel de Hola y volver a cargar los índices. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda con el aprovisionamiento del servicio.
>
>

<a id="HA"></a>

## <a name="high-availability"></a>Alta disponibilidad
Dado que es fácil y relativamente rápido tooscale seguridad, general, se recomienda que comience con una partición y uno o dos réplicas y, a continuación, ampliación vertical como volúmenes de consultas de compilación. Para muchos servicios en niveles de Basic o S1 hello, una partición proporciona almacenamiento y E/S suficientes (en documentos de 15 millones por partición).

Las cargas de trabajo de consulta se ejecutan principalmente en réplicas. Es probable que necesite más réplicas si requiere más rendimiento o alta disponibilidad.

Las recomendaciones generales para alta disponibilidad son:

* Dos réplicas para alta disponibilidad de cargas de trabajo de solo lectura (consultas)
* Tres o más réplicas para lograr una alta disponibilidad en las cargas de trabajo de lectura y escritura (se agregan, actualizan o eliminan consultas e indexación como documentos individuales).

Los Acuerdos de Nivel de Servicio (SLA) de Azure Search están destinados a las operaciones de consulta y actualizaciones de índices que constan de procesos de incorporación, actualización o eliminación de documentos.

### <a name="index-availability-during-a-rebuild"></a>Disponibilidad de los índices durante un proceso de regeneración

Alta disponibilidad para la búsqueda de Azure pertenece tooqueries e índice actualizaciones que no implican volver a generar un índice. Si elimina un campo, cambiar un tipo de datos o cambiar el nombre de un campo, será necesario índice de hello toorebuild. índice de hello toorebuild, debe eliminar Hola indizar, volver a crear el índice de Hola y volver a cargar los datos de Hola.

> [!NOTE]
> Puede agregar nuevo índice de búsqueda de Azure de tooan campos sin volver a generar índice Hola. valor de Hola de nuevo campo de hello será null para todos los documentos ya está en el índice de Hola.

toomaintain la disponibilidad de índice durante una recompilación, debe tener una copia del índice de hello con un nombre diferente en hello mismo servicio, o una copia del programa Hola de índice con el mismo nombre en un servicio diferente y, a continuación, proporcionar lógica de redirección o la conmutación por error en el código de hello.

## <a name="disaster-recovery"></a>Recuperación ante desastres
En la actualidad no hay ningún mecanismo integrado para la recuperación ante desastres. Agregar particiones o réplicas sería una estrategia equivocada Hola para cumplir los objetivos de recuperación ante desastres. enfoque más común de Hello es tooadd de redundancia en el nivel del servicio de Hola mediante la configuración de un segundo servicio de búsqueda en otra región. Al igual que con la disponibilidad durante una regeneración de índice, redirección de Hola o lógica de conmutación por error debe proceder desde el código.

## <a name="increase-query-performance-with-replicas"></a>Aumento del rendimiento de las consultas con réplicas
La latencia de consultas es un indicador de que se necesitan más réplicas. Por lo general, un primer paso para mejorar el rendimiento de las consultas es tooadd más de este recurso. Si agrega réplicas, copias adicionales del índice de Hola se ponen en línea toosupport cargas de trabajo de consulta más grandes y Hola de saldo tooload solicita sobre Hola varias réplicas.

No podemos proporcionarle las estimaciones de disco duras en consultas por segundo (QPS): consulta rendimiento depende de la complejidad de Hola de hello consulta y competencia de cargas de trabajo. De media, una réplica de las SKU de los niveles Básico o S1 puede dar servicio a unas 15 QPS, pero el rendimiento será mayor o menor en función de la complejidad de la consulta (las consultas por facetas son más complejas) y la latencia de red. Además, es importante toorecognize que aunque incorporar réplicas definitivamente agregará escala y rendimiento, Hola resultado no es estrictamente lineal: agregar tres réplicas no garantiza el triple de rendimiento.

toolearn sobre QPS, incluidos los métodos para calcular el segundo para las cargas de trabajo, consulte [administrar el servicio de búsqueda](search-manage.md).

## <a name="increase-indexing-performance-with-partitions"></a>Aumento del rendimiento de la indexación con particiones
Las aplicaciones de búsqueda que requieren una actualización de datos casi en tiempo real necesitan una proporción mayor de particiones que de réplicas. Al agregarse particiones, se distribuyen las operaciones de lectura y escritura entre un número mayor de recursos de proceso. Además, se cuenta con más espacio en disco para almacenar documentos e índices adicionales.

Índices más grandes tienen más tooquery. Por lo tanto, es posible que con cada aumento incremental de las particiones sea necesario también un aumento menor, pero proporcional, de las réplicas. complejidad de Hola de las consultas y los volúmenes de consulta repercutirán en ¿con qué rapidez se invierte la ejecución de la consulta.

## <a name="basic-tier-partition-and-replica-combinations"></a>Nivel básico: combinaciones de particiones y réplicas
Un servicio básico puede tener exactamente una partición y una copia de seguridad toothree réplicas, para un límite máximo de tres SUs. recurso solo ajustable Hello es réplicas. Se necesita un mínimo de 2 réplicas para lograr una alta disponibilidad en las consultas.

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>Niveles Estándar: combinaciones de particiones y réplicas
Esta tabla muestra hello SUs toosupport requiere combinaciones de réplicas y particiones, el límite de 36 SU toohello asunto, para todos los niveles estándares.

|   | **1 partición** | **2 particiones** | **3 particiones** | **4 particiones** | **6 particiones** | **12 particiones** |
| --- | --- | --- | --- | --- | --- | --- |
| **1 réplica** |1 unidad de búsqueda |2 unidades de búsqueda |3 unidades de búsqueda |4 unidades de búsqueda |6 unidades de búsqueda |12 unidades de búsqueda |
| **2 réplicas** |2 unidades de búsqueda |4 unidades de búsqueda |6 unidades de búsqueda |8 unidades de búsqueda |12 unidades de búsqueda |24 unidades de búsqueda |
| **3 réplicas** |3 unidades de búsqueda |6 unidades de búsqueda |9 unidades de búsqueda |12 unidades de búsqueda |18 unidades de búsqueda |36 unidades de búsqueda |
| **4 réplicas** |4 unidades de búsqueda |8 unidades de búsqueda |12 unidades de búsqueda |16 unidades de búsqueda |24 unidades de búsqueda |N/D |
| **5 réplicas** |5 unidades de búsqueda |10 unidades de búsqueda |15 unidades de búsqueda |20 unidades de búsqueda |30 unidades de búsqueda |N/D |
| **6 réplicas** |6 unidades de búsqueda |12 unidades de búsqueda |18 unidades de búsqueda |24 unidades de búsqueda |36 unidades de búsqueda |N/D |
| **12 réplicas** |12 unidades de búsqueda |24 unidades de búsqueda |36 unidades de búsqueda |N/D |N/D |N/D |

SUs, precios y la capacidad se explican con detalle en hello sitio Web de Azure. Para obtener más información, consulte [Detalles de precios](https://azure.microsoft.com/pricing/details/search/).

> [!NOTE]
> número de Hola de réplicas y particiones divide uniformemente en 12 (específicamente, 1, 2, 3, 4, 6, 12). Esto se debe a que Búsqueda de Azure divide previamente cada índice en 12 particiones para que se pueda repartir en porciones iguales entre todas las particiones. Por ejemplo, si su servicio tiene tres particiones y crear un índice, cada partición contendrá cuatro particiones del índice de Hola. El modo en búsqueda de Azure particiona un índice es un detalle de implementación, sujeto toochange en versiones futuras. Aunque el número de hello es 12 hoy en día, no debe esperar que número tooalways ser 12 Hola futuras.
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>Fórmula de facturación para los recursos de réplica y partición
fórmula de Hola para calcular SUs cuántas se utilizan para combinaciones específicas es producto Hola de réplicas y particiones, o (R X P = SU). Por ejemplo, 3 réplicas multiplicadas por 3 particiones se facturan como 9 SU.

Costo por SU viene determinado por el nivel de hello, con una tasa de facturación por unidad menor de Basic a estándar. Las tarifas de cada nivel pueden consultarse en [Buscar Precios](https://azure.microsoft.com/pricing/details/search/).
