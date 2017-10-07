---
title: "aaaHow distribuidas funciona de datos en el almacén de datos de SQL de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se distribuyen los datos para opciones de hello y masivo paralelas de procesamiento (MPP) para la distribución de tablas de almacenamiento de datos de SQL Azure y almacenamiento de datos paralelos."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>Datos distribuidos y tablas distribuidas para el procesamiento paralelo masivo (MPP)
Obtenga información sobre cómo se distribuyen los datos de usuario en SQL Data Warehouse y Almacenamiento de datos paralelos de Azure, que son sistemas de procesamiento paralelo masivo (MPP) de Microsoft. Diseñar la toouse de almacenamiento de datos datos distribuidos eficazmente le ayuda a tooachieve Hola de procesamiento de consultas ventajas de hello arquitectura MPP. Algunas opciones de diseño de bases de datos pueden mejorar de manera significativa el rendimiento de las consultas.  

> [!NOTE]
> Almacenamiento de datos de SQL Azure y Hola de uso de almacenamiento de datos paralelos de diseño un procesamiento paralelo masivo mismo (MPP), pero tienen algunas diferencias debido a Hola subyacente de la plataforma. SQL Data Warehouse es una plataforma como servicio (PaaS) que se ejecuta en Azure. Almacenamiento de datos paralelos se ejecuta en Analytics Platform System (APS), que es una aplicación local que se ejecuta en Windows Server.
> 
> 

## <a name="what-is-distributed-data"></a>¿Qué son los datos distribuidos?
En almacenamiento de datos SQL y almacenamiento de datos paralelos, datos distribuidos hace referencia a datos de toouser que están almacenados en varias ubicaciones en hello sistema MPP. Cada una de esas ubicaciones funciona como una unidad de procesamiento que se ejecuta consultas en la parte de datos de Hola y de almacenamiento independiente. Datos distribuido están fundamental toorunning consultas en el rendimiento de las consultas alta tooachieve paralelas.

datos de toodistribute, almacenamiento de datos de hello asigna cada fila de una ubicación de tooone distribuida de la tabla de usuario.  También pueden distribuirse las tablas con un método de distribución basado en una función hash o con un método round robin. Especifica el método de distribución de Hola Hola instrucción CREATE TABLE. 

## <a name="hash-distributed-tables"></a>Tablas distribuidas mediante una función hash
Hola siguiente diagrama ilustra cómo una completa (tabla no distribuido) se almacena como una tabla hash está distribuido. Una función determinista asigna cada distribución de tooone toobelong de fila. En la definición de la tabla de hello, una de las columnas de Hola se designa como columna de distribución de Hola. función de hash de Hello usa valor hello en hello distribución columna tooassign cada distribución de tooa de fila.

Existen consideraciones de rendimiento para la selección de Hola de una columna de distribución, como diferenciación y sesgo de datos, tipos de Hola de consultas ejecutadas en el sistema de Hola.

![Tabla distribuida](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "Tabla distribuida")  

* Cada fila pertenece tooone distribución.  
* Un algoritmo hash determinista asigna cada distribución tooone de fila.  
* número de Hola de filas de la tabla por distribución varía como se muestra en distintos tamaños de Hola de tablas.

## <a name="round-robin-distributed-tables"></a>Tablas distribuidas con el método round robin
Una tabla distribuida round robin distribuye filas hello mediante la asignación de cada distribución de tooa de filas de forma secuencial. Está formado por datos en una tabla de round robin tooload rápido, pero el rendimiento de las consultas puede ser más lento.  Combinar una tabla de round robin normalmente requiere reconstruyen Hola filas tooenable Hola consulta tooproduce un resultado exacto, lo que lleva tiempo.

## <a name="distributed-storage-locations-are-called-distributions"></a>Las ubicaciones de almacenamiento distribuidas se denominan distribuciones
Cada ubicación distribuida se denomina distribución. Cuando se ejecuta una consulta en paralelo, cada distribución realiza una consulta SQL en la parte de datos de Hola. Almacenamiento de datos de SQL usa la consulta de base de datos SQL toorun Hola. Almacenamiento de datos paralelos utiliza la consulta de SQL Server toorun Hola. Este diseño de arquitectura compartir nada es fundamental tooachieving escalabilidad informática en paralelo.

### <a name="can-i-view-hello-distributions"></a>¿Puedo ver las distribuciones de hello?
Cada distribución tiene un Id. de distribución y es visible en vistas del sistema que pertenecen tooSQL almacenamiento de datos y almacenamiento de datos paralelos. Puede usar el rendimiento de la consulta de tootroubleshoot de identificador hello distribución y otros problemas. Para obtener una lista de vistas del sistema hello, vea hello [vista del sistema MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="difference-between-a-distribution-and-a-compute-node"></a>Diferencia entre una distribución y un nodo de ejecución
Una distribución es la unidad básica de Hola para almacenar datos distribuidos y procesar las consultas en paralelo. Las distribuciones se agrupan en nodos de ejecución. Cada nodo de ejecución realiza el seguimiento de una o varias distribuciones.  

* Sistema de la plataforma de análisis utiliza nodos de proceso como un componente central de hello arquitectura y escalabilidad horizontal las capacidades de hardware. Siempre utiliza ocho distribuciones por nodo de proceso, como se muestra en el diagrama de Hola para las tablas hash distribuido. Hola número de nodos de proceso y Hola, por tanto, el número de distribuciones, viene determinado por el número de Hola de nodos de proceso que adquiere de dispositivo de Hola. Por ejemplo, si adquiere ocho nodos de ejecución, obtendrá 64 distribuciones (8 nodos de ejecución x 8 distribuciones/nodo). 
* SQL Data Warehouse tiene una cantidad de distribuciones (60) y un número flexible de nodos de ejecución. nodos de proceso de Hola se implementan con recursos de proceso y almacenamiento de Azure. número de Hola de nodos de proceso puede cambiar cargas de trabajo del servicio de back-end toohello correspondiente y capacidad informática de hello (a Dwu) que especifique para el almacenamiento de datos de Hola. Cuando se cambia el número de Hola de nodos de proceso, número de Hola de distribuciones por nodo de proceso también cambia. 

### <a name="can-i-view-hello-compute-nodes"></a>¿Puedo ver los nodos de proceso de hello?
Cada nodo de cálculo tiene un identificador de nodo y es visible en vistas del sistema que pertenecen tooSQL almacenamiento de datos y almacenamiento de datos paralelos.  Puede ver el nodo de proceso de hello buscando columna node_id de hello en las vistas de sistema cuyos nombres comienzan por sys.pdw_nodes. Para obtener una lista de vistas del sistema hello, vea hello [vista del sistema MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="Replicated"></a>Tablas replicadas
Tiene una tabla que se replica una totalmente almacena la copia de la tabla de hello en cada nodo de ejecución. Replicación de una tabla quita los datos de tootransfer de necesidad de hello entre los nodos de proceso antes de una combinación o una agregación. Las tablas replicadas sólo son viables con tablas pequeñas debido a Hola tabla completa Hola de almacenamiento adicional toostore necesarios en cada nodo de ejecución.  

Hello siguiente diagrama muestra una tabla replicada se almacena en cada nodo de proceso. Para almacenamiento de datos de SQL, tabla replicada hello es tooa copiado totalmente la base de datos de distribución en cada nodo de ejecución. Para almacenamiento de datos paralelos, tabla replicada Hola se almacena en todos los discos asignados toohello de nodos de proceso.  Esta estrategia de disco se implementa mediante el uso de grupos de archivos de SQL Server.  

![Tabla replicada](media/sql-data-warehouse-distributed-data/replicated-table.png "Tabla replicada") 

## <a name="next-steps"></a>Pasos siguientes
tablas toouse distribuida de forma eficaz, consulte [distribuir tablas en el almacén de datos de SQL](sql-data-warehouse-tables-distribute.md)  

