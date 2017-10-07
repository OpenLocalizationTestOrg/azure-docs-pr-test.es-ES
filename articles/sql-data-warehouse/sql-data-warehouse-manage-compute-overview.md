---
title: "capacidad de almacenamiento de datos de SQL Azure (Introducción) de cálculo aaaManage | Documentos de Microsoft"
description: Funcionalidades de escalado horizontal del rendimiento en Almacenamiento de datos SQL de Azure. Escalar horizontalmente mediante el ajuste a Dwu o pausar y reanudar los costos de toosave de recursos de proceso.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (información general)
> [!div class="op_single_selector"]
> * [Información general](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

arquitectura de Hola de almacenamiento de datos SQL separa almacenamiento y proceso, lo que permite cada tooscale de forma independiente. Como resultado, compute puede ser demandas de rendimiento escalado toomeet independiente de la cantidad de Hola de datos. Una consecuencia natural de esta arquitectura es que la [facturación][billed] para el proceso y almacenamiento es independiente. 

Esta introducción se describe cómo escalar horizontalmente funciona con almacenamiento de datos SQL y cómo tooutilize Hola pausar, reanudar y capacidades de escala de almacenamiento de datos SQL. Consulte hello [unidades (a Dwu) del almacenamiento de datos] [ data warehouse units (DWUs)] toolearn página cómo se relacionan a Dwu y rendimiento. 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>Funcionamiento de las operaciones de administración de proceso en SQL Data Warehouse
arquitectura de Hola para almacenamiento de datos de SQL está formada por un nodo del control, nodos de proceso y Hola repartidos 60 distribuciones de capa de almacenamiento. 

Durante una sesión activa normal en el almacén de datos de SQL, nodo principal del sistema administra los metadatos de Hola y contiene el optimizador de consultas distribuida de Hola. Debajo de este nodo principal se encuentran los nodos de proceso y el nivel de almacenamiento. Para un 400 DWU, el sistema tiene un nodo principal, cuatro nodos de proceso y capa de almacenamiento de hello, que consta de 60 distribuciones. 

Cuando se someten a una escala o pausa la operación, el sistema de hello primero elimina todas las consultas entrantes y, a continuación, revierte las transacciones tooensure un estado coherente. Para las operaciones de escala, el escalado solo se producirá una vez completada esta reversión transaccional. Para una operación de escalado vertical, disposiciones de sistema de Hola Hola extra deseado número de nodos de proceso y comienza a continuación, volver a adjuntar la capa de almacenamiento de toohello de nodos de proceso de Hola. Para una operación de reducción, hello nodos innecesarios se liberan y nodos de proceso restantes Hola volver a adjuntar por sí mismos toohello número adecuado de las distribuciones. Para una operación de pausa, todos los de proceso se liberan los nodos y el sistema sufrirá una variedad de metadatos operaciones tooleave el sistema final en un estado estable.

| DWU  | \# de nodos de ejecución | \# de distribuciones por nodo |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20 |                           |
| 400  | 4                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1000 | 10                 | 6                            |
| 1200 | 12                 | 5                            |
| 1.500 | 15                 | 4                            |
| 2000 | 20 |                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

Hola tres funciones principales para administrar el proceso son:

1. Pausar
2. Reanudación
3. Escala

Cada una de estas operaciones puede tardar varios toocomplete minutos. Si estás escalado, pausar o reanudar automáticamente, puede que desee tooimplement de lógica tooensure que algunas de las operaciones se hayan completado antes de realizar otra acción. 

Comprobando el estado de la base de datos de Hola a través de varios extremos le permitirá toocorrectly implementar automatización de tales operaciones. portal de Hola proporcionará la notificación tras la finalización de un estado actual de las bases de datos hello y operación pero no permite la programación de comprobación del estado. 

>  [!NOTE]
>
>  La funcionalidad de administración del proceso no existe en todos los puntos de conexión.
>
>  

|              | Pausar y reanudar | Escala | Comprobar el estado de la base de datos |
| ------------ | ------------ | ----- | -------------------- |
| Portal de Azure | Sí          | Sí   | **No**               |
| PowerShell   | Sí          | Sí   | Sí                  |
| API de REST     | Sí          | Sí   | Sí                  |
| T-SQL        | **No**       | Sí   | Sí                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Escalado de proceso

El rendimiento en SQL Data Warehouse se mide en [unidades de almacenamiento de datos (DWU)][data warehouse units (DWUs)], que es una medida de recursos de proceso abstracta, como la CPU, la memoria y el ancho de banda de E/S. Un usuario que desea tooscale el rendimiento de su sistema puede hacerlo a través de varios medios, como a través del portal de hello, T-SQL y API de REST. 

### <a name="how-do-i-scale-compute"></a>¿Cómo se puede escalar el proceso?
Cambiar la configuración de la unidad de hello administra capacidad de proceso para su almacenamiento de datos de SQL. El rendimiento aumenta [linealmente][linearly] a medida que agrega más DWU para determinadas operaciones.  Proporcionamos ofertas de DWU que garantizan que el rendimiento cambiará considerablemente al escalar o reducir el sistema verticalmente. 

tooadjust a Dwu, puede usar cualquiera de estos métodos individuales.

* [Escalado de la potencia de proceso con Azure Portal][Scale compute power with Azure portal]
* [Escalado de la potencia de proceso con PowerShell][Scale compute power with PowerShell]
* [Escalado de la potencia de proceso con API de REST][Scale compute power with REST APIs]
* [Escalado de la potencia de proceso con TSQL][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>¿Cuántas DWU debería usar?

toounderstand qué el valor DWU ideal es, intente escalado vertical y horizontalmente y ejecute algunas consultas después de cargar los datos. Dado que el escalado se realiza rápidamente, puede probar varios niveles de rendimiento en una hora o menos. 

> [!Note] 
> Almacenamiento de datos de SQL está diseñado tooprocess grandes cantidades de datos. toosee sus capacidades true para ajustar la escala, especialmente en a mayor Dwu, desea toouse un gran conjunto de datos que se aproxima o supera 1 TB.

Recomendaciones para buscar Hola DWU recomendada para la carga de trabajo:

1. Para un almacenamiento de datos en desarrollo, comience seleccionando un número pequeño de DWU.  Un buen punto de partida es DW400 o DW200.
2. Supervisar el rendimiento de la aplicación, observar el número de Hola de a Dwu seleccionado compara el rendimiento toohello que observa.
3. Determinar cuánto rendimiento más rápido o más lento que debería ser para tooreach Hola nivel de rendimiento adecuado para sus requisitos, suponiendo la escala lineal.
4. Aumentar o reducir el número de Hola de a Dwu en proporción toohow mucho más rápida o más lentamente que desea que su tooperform de carga de trabajo. 
5. Continúe realizando ajustes hasta llegar a un nivel de rendimiento adecuado para sus requerimientos empresariales.

> [!NOTE]
>
> Rendimiento de las consultas solo aumenta con la ejecución en paralelo más si se puede dividir el trabajo de hello entre nodos de proceso. Si encuentra que el ajuste de escala no cambia su rendimiento, desproteja nuestro artículos toocheck si los datos no se distribuyen o si va a presentar una gran cantidad de movimiento de datos de optimización del rendimiento. 

### <a name="when-should-i-scale-dwus"></a>¿Cuándo debo realizar un escalado de DWU?
Ajuste de escala a Dwu modifica Hola escenarios importantes siguientes:

1. Cambiar linealmente el rendimiento del sistema de Hola para exámenes, agregaciones y las instrucciones de CTAS
2. Aumentar el número de Hola de lectores y escritores cuando se carga con PolyBase
3. Número máximo de consultas simultáneas y ranuras de simultaneidad

Recomendaciones para saber cuándo tooscale a Dwu:

1. Para realizar una operación de transformación o carga de una gran cantidad de datos, realice el escalado vertical de DWU para que los datos estén disponibles con mayor rapidez.
2. Durante las horas punta, escalar tooaccommodate un mayor número de consultas simultáneas. 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Pausa del proceso
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause una base de datos, use cualquiera de estos métodos individuales.

* [Pausa del proceso con Azure Portal][Pause compute with Azure portal]
* [Pausa del proceso con PowerShell][Pause compute with PowerShell]
* [Pausa del proceso con las API de REST][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Reanudación del proceso
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume una base de datos, use cualquiera de estos métodos individuales.

* [Reanudación del proceso con Azure Portal][Resume compute with Azure portal]
* [Reanudación del proceso con PowerShell][Resume compute with PowerShell]
* [Reanudación del proceso con las API de REST][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>Comprobar el estado de la base de datos 

tooresume una base de datos, use cualquiera de estos métodos individuales.

- [Comprobar el estado de la base de datos con T-SQL][Check database state with T-SQL]
- [Comprobar el estado de la base de datos con PowerShell][Check database state with PowerShell]
- [Comprobar el estado de la base de datos con API de REST][Check database state with REST APIs]

## <a name="permissions"></a>Permisos

Base de datos de hello escala requiere permisos de hello descritos en [ALTER DATABASE][ALTER DATABASE].  Pausar y reanudar requieren hello [colaborador de la base de datos de SQL] [ SQL DB Contributor] permiso, Microsoft.Sql/servers/databases/action específicamente.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Pasos siguientes
Consulte toohello después toohelp artículos entender algunos conceptos clave de rendimiento adicionales:

* [Administración de cargas de trabajo y simultaneidad][Workload and concurrency management]
* [Introducción al diseño de tablas][Table design overview]
* [Distribución de tablas][Table distribution]
* [Indexación de tablas][Table indexing]
* [Partición de tabla][Table partitioning]
* [Estadísticas de tabla][Table statistics]
* [Prácticas recomendadas][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
