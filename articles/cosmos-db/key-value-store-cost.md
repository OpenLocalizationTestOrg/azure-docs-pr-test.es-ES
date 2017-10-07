---
title: "aaaAzure DB Cosmos como un almacén de valor de clave: información general de costo | Documentos de Microsoft"
description: "Obtenga información acerca de bajo costo de usar base de datos de Azure Cosmos como un almacén de claves de valores de hello."
keywords: "almacén de pares valor-clave"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a>Azure Cosmos DB como almacén de pares valor-clave: Información general de costos

Azure Cosmos DB es un servicio de base de datos multimodelo globalmente distribuido para crear aplicaciones de alta disponibilidad y a gran escala fácilmente. De forma predeterminada, base de datos de Azure Cosmos automáticamente indiza todos los datos de hello eficazmente introduce. Esto permite consultas [SQL](documentdb-sql-query.md) (y [JavaScript](programming.md)) rápidas y coherentes en todos los tipos de datos. 

Este artículo describe el costo de Hola de base de datos de Azure Cosmos para escritura simple y operaciones de lectura cuando se utiliza como un almacén de clave/valor. Las operaciones de escritura incluyen inserciones, reemplazos, eliminaciones y upserts de documentos. Además de para garantizar la alta disponibilidad del 99,99%, garantiza que las ofertas de base de datos de Azure Cosmos < 10 ms de latencia para las lecturas y < 15 ms de latencia para hello (indizado) respectivamente, escribe en el percentil 99 Hola. 

## <a name="why-we-use-request-units-rus"></a>¿Por qué usamos unidades de solicitud (RU)?

Rendimiento de base de datos de Cosmos Azure se basa en la cantidad de Hola de aprovisionamiento [unidades de solicitud](request-units.md) (RU) para la partición de Hola. Hola de aprovisionamiento está en una granularidad de segundo y se adquiere en RUs/seg. y RUs por minuto ([no toobe confundirse con hello facturación horaria](https://azure.microsoft.com/pricing/details/cosmos-db/)). RUs deben considerarse como una moneda que simplifica el aprovisionamiento de Hola de rendimiento necesario para la aplicación hello. Los clientes no tiene toothink de diferenciar entre lectura y escritura de unidades de capacidad. modelo de moneda única Hola de RUs crea las eficiencias de capacidad de hello aprovisionado tooshare entre las lecturas y escrituras. Este modelo de capacidad aprovisionada permite Hola servicio tooprovide un rendimiento coherente y predecible, garantizada la baja latencia y alta disponibilidad. Por último, usamos el rendimiento toomodel RU pero cada RU aprovisionado también tiene una cantidad definida de recursos (memoria, núcleos). RU/s no es solo E/S por segundo.

Como un sistema de base de datos distribuidos globalmente, Cosmos DB es Hola solo servicio de Azure que proporciona un SLA de latencia, el rendimiento y la coherencia en la disponibilidad de toohigh de adición. rendimiento de Hello que aprovisionar es tooeach aplicada de regiones de hello asociadas a su cuenta de base de datos de base de datos de Cosmos. Para lecturas, Cosmos DB ofrece varios, bien definido [niveles de coherencia](consistency-levels.md) para toochoose de. 

Hola siguiente tabla se muestra Hola número de RUs tooperform necesario leer y escribe las transacciones según el tamaño del documento de 1KB y 100KBs.

|Tamaño del elemento|1 lectura|1 escritura|
|-------------|------|-------|
|1 KB|1 RU|5 RU|
|100 KB|10 RU|50 RU|

## <a name="cost-of-reads-and-writes"></a>Costo de lecturas y escrituras

Si se aprovisiona 1.000 RU/seg., esto cantidades too3.6m RU/hora y costará $0,08 hora hello (en hello Estados Unidos y Europa). Para un documento de 1 KB de tamaño, esto significa que puede consumir 3,6 millones de lecturas o 0,72 millones de escrituras (3,6 millones de RU/5) con el rendimiento aprovisionado. Toomillion normalizado las lecturas y escrituras, costo de hello sería $0,022 /m lecturas (0,08 $ / 3,6) y escribe $0.111/ m (0,08 $ / 0,72). Hola costo por millones pasa a ser mínimo tal y como se muestra en la siguiente tabla se Hola.

|Tamaño del elemento|1 millón de lecturas|1 millón de escrituras|
|-------------|-------|--------|
|1 KB|0,022 USD|0,111 USD|
|100 KB|0,222 USD|1,111 USD|


Mayoría de los blob básica de Hola o el cargo de servicios de almacenes de objeto 0,40 $ por cada millón de transacción de lectura y 5 dólares por transacción de escritura millones. Si usa un rendimiento óptimo, puede ser Cosmos DB too98% más económico que estas otras soluciones (para las transacciones de 1KB).

## <a name="next-steps"></a>Pasos siguientes

Permanezca atento para buscar nuevos artículos sobre la optimización del aprovisionamiento de recursos de Azure Cosmos DB. En Hola mientras tanto, sentirse toouse libre nuestro [calculadora RU](https://www.documentdb.com/capacityplanner).

