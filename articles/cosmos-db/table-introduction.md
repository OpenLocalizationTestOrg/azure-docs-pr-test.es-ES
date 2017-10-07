---
title: API de tabla de DB aaaIntroduction tooAzure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo puede utilizar la base de datos de Azure Cosmos toostore y populares OSS MongoDB APIs de Hola de grandes volúmenes de datos de clave y valor con el uso de baja latencia de consulta."
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a>Introducción tooAzure DB Cosmos: API de tabla

[Azure Cosmos DB](introduction.md) es un servicio de base de datos con varios modelos y distribución global de Microsoft para aplicaciones críticas. Proporciona la base de datos de Azure Cosmos [distribución global preparada](distribute-data-globally.md), [escalado flexible de rendimiento y almacenamiento](partition-data.md) latencias de milisegundo en todo el mundo, solo dígito se escriben en el percentil 99 de hello, [cinco niveles de coherencia bien definido](consistency-levels.md)y garantiza la alta disponibilidad, todo ello respaldado por [líderes en la industria SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de datos de Azure Cosmos [automáticamente los datos de índices](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sin necesidad de toodeal con administración de esquema y de índice. Sigue varios modelos y es compatible con los modelos de datos de documento, de clave-valor, de grafo y de columnas. 

![API Table Storage de Azure y Azure Cosmos DB](./media/table-introduction/premium-tables.png) 

Base de datos de Azure Cosmos proporciona Hola API (vista previa) de la tabla para las aplicaciones que necesitan un almacén de clave y valor con esquema flexible, un rendimiento predecible, distribución global y un alto rendimiento. Hola API de tabla proporciona Hola misma funcionalidad que el almacenamiento de tabla de Azure, pero aprovecha todos los beneficios de Hola de motor de base de datos de Azure Cosmos Hola. 

Puede continuar toouse almacenamiento de tabla de Azure para las tablas con almacenamiento alta y requisitos de rendimiento inferior. Azure DB Cosmos incorporará la compatibilidad con tablas con optimización para el almacenamiento en una futura actualización y se actualiza la tabla de Azure nuevas y existentes serán las cuentas de almacenamiento tooAzure Cosmos DB.

## <a name="premium-and-standard-table-apis"></a>API Table premium y estándar
Si actualmente usa almacenamiento de tabla de Azure, obtendrá Hola después ventajas moviendo "premium" vista previa de DB tooAzure Cosmos:

|  | Azure Table Storage | Table Storage de Azure Cosmos DB (versión preliminar) |
| --- | --- | --- |
| Latency | Rápido, pero no hay límites máximos en la latencia. | Con el respaldo de latencia de milisegundos de un solo dígito para lecturas y escrituras, < 10 ms de latencia lee y < 15 ms de latencia se escribe en el percentil 99 de hello, en cualquiera de ellas, en cualquier lugar de Hola a todos |
| Rendimiento | Altamente escalable, pero sin un modelo de rendimiento dedicado. Las tablas tienen un límite de escalabilidad de 20 000 operaciones por segundo. | Altamente escalable con [rendimiento reservado dedicado por tabla](request-units.md), respaldado por el SLA. Las cuentas no tienen límite máximo en el rendimiento y admiten más de 10 millones de operaciones por segundo por tabla. |
| Distribución global | Una sola región, con una región de lectura secundaria legible opcional para alta disponibilidad. No se puede iniciar la conmutación por error. | [Distribución global preparada](distribute-data-globally.md) desde una too30 + regiones, soporte para [conmutaciones por error automática y manual](regional-failover.md) en cualquier momento, en cualquier lugar de Hola a todos |
| Indización | Índice principal solo en PartitionKey y RowKey. No hay índices secundarios. | Indexación automática y completa en todas las propiedades, sin administración de índices. |
| Consultar | La ejecución de consultas usa el índice de la clave principal y, en caso contrario, examina. | Las consultas pueden aprovechar la indexación automática en las propiedades para reducir el tiempo de consulta. El motor de base de datos de Azure Cosmos DB puede admitir agregados, funciones geoespaciales y ordenación. |
| Coherencia | Fuerte en la región primaria, Final en la región secundaria. | [Cinco niveles de coherencia bien definido](consistency-levels.md) tootrade desactivar disponibilidad, latencia, el rendimiento y coherencia según sus necesidades de aplicación |
| Precios | Optimizado para el almacenamiento.  | Optimizado para el rendimiento. |
| SLA | Disponibilidad del 99,9 %. | disponibilidad del 99,99% dentro de una única región y capacidad tooadd más regiones para una mayor disponibilidad. [SLA completos líderes en el sector](https://azure.microsoft.com/support/legal/sla/cosmos-db/) en disponibilidad general. |

## <a name="how-tooget-started"></a>Cómo iniciar tooget

Crear una cuenta de base de datos de Azure Cosmos en hello [portal de Azure](https://portal.azure.com)y empezar a trabajar con nuestro [inicio rápido para API de tabla mediante .NET](create-table-dotnet.md). 

## <a name="next-steps"></a>Pasos siguientes

A continuación, presentamos unos tooget punteros se inició:
* [Compilar una aplicación de .NET mediante Hola API de tabla](create-table-dotnet.md)
* [Desarrollar con hello API de tabla en .NET](tutorial-develop-table-dotnet.md)
* [Datos de la tabla de consulta mediante el uso de hello API de tabla](tutorial-query-table.md)
* [Cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de tabla](tutorial-global-distribution-table.md)
* [Table API .NET de Azure Cosmos DB: descarga y notas de la versión](table-sdk-dotnet.md)
