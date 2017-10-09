---
title: aaaLearn acerca de las operaciones de almacenamiento de datos de SQL de Azure | Documentos de Microsoft
description: "La elasticidad del servicio Almacenamiento de datos SQL permite aumentar, reducir o pausar la capacidad de proceso mediante el uso de una escala móvil de unidades de almacenamiento de datos (DWU). Este artículo explica las métricas de almacenamiento de datos de Hola y cómo se relacionan con tooDWUs. "
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: cadffa9c-589d-4db7-888a-1f202a753bc5
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 8be5ff6b14ab907e2b0a7eb55e0e2f4139aca8b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-workload"></a>Carga de trabajo del almacenamiento de datos
Una carga de trabajo de almacenamiento de datos hace referencia tooall de operaciones de Hola que ocurren en un almacenamiento de datos. carga de trabajo de almacenamiento de datos de Hello abarca Hola todo el proceso de cargar datos en almacenamiento de hello, realización de análisis y reporting en almacenamiento de datos de hello, administración de datos en almacenamiento de datos de Hola y exportar datos desde almacenamiento de datos de Hola. Hello profundidad y amplitud de estos componentes suelen ser acorde con el nivel de madurez Hola Hola del almacén de datos.

## <a name="new-toodata-warehousing"></a>¿Nueva toodata almacenamiento?
Un almacén de datos es una colección de datos que se cargan desde uno o más datos orígenes y tooperform usado tareas de business intelligence, como el análisis de datos e informes.

Almacenes de datos se caracterizan por las consultas que examinan más grandes cantidades de filas, intervalos grandes de datos y pueden devolver resultados relativamente grandes para fines de Hola de análisis e informes. Los almacenamientos de datos también se caracterizan por cargas de datos relativamente grandes frente a pequeñas inserciones, actualizaciones y eliminaciones en el nivel de transacción.

* Un almacén de datos funciona mejor cuando los datos de Hola se almacenan de forma que optimiza las consultas que requieran tooscan grandes cantidades de filas o intervalos grandes de datos. Este tipo de recorrido funciona mejor cuando se almacenan datos de Hola y se realiza la búsqueda por columnas, en lugar de filas.

> [!NOTE]
> índice columnstore en memoria de Hello, que usa almacenamiento de columnas, permite hasta too10x compresión mejoras y 100 x mejoras de rendimiento de consultas sobre árboles binarios tradicionales para las consultas de informes y análisis. Consideramos índices de almacén de columnas como Hola estándar para almacenar y análisis de datos de gran tamaño en un almacén de datos.
> 
> 

* Un almacenamiento de datos tiene requisitos diferentes de un sistema que se optimiza para el procesamiento de transacciones en línea (OLTP). Hola sistema OLTP tiene muchas inserciones, actualizaciones y las operaciones de eliminación. Estas operaciones de búsqueda toospecific filas en la tabla de Hola. Búsquedas de tabla demostrar un mejor comportamiento cuando los datos de Hola se almacenan en forma de fila por fila. datos Hola se pueden ordenar y buscan con una división y rápidamente vencerás método denominado una búsqueda binaria de árbol b o montículo.

## <a name="data-loading"></a>Carga de datos
Carga de datos es una parte importante de la carga de trabajo de almacenamiento de datos de Hola. Las empresas tienen normalmente un sistema OLTP ocupado que realiza el seguimiento de cambios a lo largo del día de hello cuando los clientes están generando las transacciones comerciales. Periódicamente, con frecuencia durante la noche durante una ventana de mantenimiento, las transacciones de Hola se mueven o copian toohello almacenamiento de datos. Una vez en el almacén de datos de hello datos hello, los analistas pueden realizar análisis y tomar decisiones empresariales en datos de Hola.

* Tradicionalmente, proceso de Hola de carga se denomina ETL de extracción, transformación y carga. Normalmente, los datos tienen toobe transformado por lo que resulta coherente con otros datos de almacenamiento de datos de Hola. Anteriormente, las empresas usan transformaciones de Hola de tooperform de servidores ETL dedicadas. Ahora, con tal procesamiento paralelo masivo rápido puede cargar datos en almacenamiento de datos SQL en primer lugar y, a continuación, realizar transformaciones de Hola. Este proceso se conoce como de extracción, carga y transformar (ETL); se está convirtiendo en un nuevo estándar para la carga de trabajo de almacenamiento de datos de Hola.

> [!NOTE]
> Con SQL Server 2016, ahora es posible realizar análisis en tiempo real en una tabla OLTP. Esto no elimina la necesidad de Hola para un toostore de almacenamiento de datos y analizar los datos, pero proporcionan una manera tooperform de análisis en tiempo real.
> 
> 

### <a name="reporting-and-analysis-queries"></a>Consultas de informes y análisis
Las consultas de informes y análisis a menudo se clasifican como pequeñas, medianas y grandes en función de diversos criterios, pero normalmente están basadas en el tiempo. En la mayoría de los almacenamientos de datos, hay una carga de trabajo mixta de ejecución rápida frente a consultas de larga ejecución. En cada caso, es importante toodetermine esta combinación y toodetermine su frecuencia (cada hora, diariamente, fin de mes, trimestre final y así sucesivamente). Es importante toounderstand que Hola cargas de trabajo de consultas mixtas, junto con la simultaneidad, responsable de tooproper planear la capacidad de un almacén de datos.

* Planeamiento de capacidad puede ser una tarea compleja para una carga de trabajo de consultas mixtas, especialmente cuando se necesita un almacenamiento de datos de entrega a largo plazo tiempo tooadd capacidad toohello. Almacenamiento de datos SQL quita urgencia Hola de planeación de la capacidad ya que se puede aumentar y reducir la capacidad de proceso en cualquier momento y desde el almacenamiento y capacidad de proceso independientemente un tamaño.

### <a name="data-management"></a>Administración de datos
Administración de datos es importante, sobre todo cuando conozca que puede quedarse sin espacio en disco en hello futuro próximo. Almacenes de datos normalmente dividen datos de hello en rangos significativos, que se almacenan como particiones en una tabla. Todos los productos basados en SQL Server le permiten mover particiones dentro y fuera de la tabla de Hola. Esta partición cambio permite mover anterior almacenamiento costosas que no requiere herramientas de datos y mantiene los datos más recientes de hello disponibles en almacenamiento en línea.

* Los índices de almacén de columnas admiten tablas con particiones. Para los índices de almacén de columnas, las tablas con particiones se utilizan para la administración y el archivado de los datos. En las tablas almacenadas por filas, las particiones desempeñan una función mayor en el rendimiento de las consultas.  
* PolyBase desempeña un papel importante en la administración de datos. Con PolyBase, tiene opción hello tooarchive anterior tooHadoop de datos o almacenamiento de blobs de Azure.  Esto proporciona una gran cantidad de opciones, puesto que los datos de hello son estando en línea.  Es posible que tarde más tiempo datos tooretrieve desde Hadoop, pero contrapartida Hola de tiempo de recuperación podría ser mayor que el costo de almacenamiento de información de Hola.

### <a name="exporting-data"></a>Exportación de datos
Datos de una manera toomake disponibles para los informes y análisis son datos de toosend de tooservers de almacenamiento de datos de hello dedicado para ejecutar informes y análisis. Estos servidores se denominan puestos de datos. Por ejemplo, podría procesar previamente los datos de informe y, a continuación, expórtelo desde servidores de toomany de almacenamiento de datos de Hola mundo Hola, de toomake ampliamente estén disponibles para los clientes y los analistas.

* Para generar informes, todas las noches podría incluir servidores de informes de solo lectura con una instantánea de datos diarias de Hola. Esto proporciona mayor ancho de banda para los clientes al reducir las necesidades de recursos de proceso de hello en almacenamiento de datos de Hola. De un aspecto de la seguridad, los puestos de datos le permiten a tooreduce número de Hola de usuarios que tienen el almacenamiento de datos de access toohello.
* Para el análisis, puede generar un cubo de analysis en almacenamiento de datos de Hola y ejecutar análisis en almacenamiento de datos de hello, o procesar previamente los datos y exportar toohello el servidor de análisis para el análisis adicional.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ya conoce un poco acerca de almacenamiento de datos SQL, obtenga información acerca de cómo tooquickly [crear un almacén de datos de SQL] [ create a SQL Data Warehouse] y [cargar datos de ejemplo][load sample data].

<!--Image references-->

<!--Article references-->
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md

<!--MSDN references-->

<!--Other web references-->
