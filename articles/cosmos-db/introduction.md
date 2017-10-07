---
title: aaaIntroduction tooAzure Cosmos DB | Documentos de Microsoft
description: "Información acerca de Azure Cosmos DB. Esta base de datos de varios modelos y distribución global se ha creado con latencia baja, escalabilidad elástica y alta disponibilidad."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a>Página principal tooAzure Cosmos DB

Azure Cosmos DB es la base de datos multimodelo de distribución global de Microsoft. Hola hacer clic en un botón, base de datos de Azure Cosmos permite tooelastically e independientemente de rendimiento de escala y almacenamiento en cualquier número de regiones geográficas de Azure. Ofrece garantía de rendimiento, latencia, disponibilidad y coherencia con [acuerdos de nivel de servicio](https://aka.ms/acdbsla) (SLA)  integrales, algo que no ofrece ningún otro servicio de base de datos.

![Azure Cosmos DB es el servicio de base de datos de distribución global de Microsoft con escalado elástico horizontal, baja latencia garantizada, cinco modelos de coherencia y SLA integrales garantizados.](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a>Soluciones que se benefician de Azure Cosmos DB

Cualquier [web, móviles, juegos y aplicaciones de IoT](use-cases.md) que necesita toohandle grandes cantidades de lecturas y escrituras en un [global](distribute-data-globally.md) escalar con tiempos de respuesta bajo para una variedad de datos se beneficiará de Azure Cosmos DB [garantiza](https://azure.microsoft.com/support/legal/sla/cosmos-db/) disponibilidad, alto rendimiento, latencia baja y coherencia ajustable.

## <a name="key-capabilities"></a>Principales capacidades
Como un servicio de base de datos distribuidos globalmente, base de datos de Azure Cosmos proporciona Hola después toohelp capacidades generar aplicaciones escalables de alta capacidad de respuesta:

* **Distribución global inmediata**
    * También puede [distribuir los datos](distribute-data-globally.md) tooany número de [regiones de Azure](https://azure.microsoft.com/regions/), con hello [haga clic en un botón](tutorial-global-distribution-documentdb.md). Esto permite tooput los datos donde los usuarios, asegurarse de latencia más baja posible de hello tooyour clientes. 
    * Utilizando Azure Cosmos DB API de hospedaje múltiple, siempre la aplicación hello sabe donde hello más cercano de la región es y enviará solicitudes toohello más cercano de centro de datos. Todo esto es posible sin realizar ningún cambio de configuración, establezca el área de escritura y porque muchas áreas de modo de lectura como desee y Hola rest se administra para usted.

* **Varios modelos de datos y API populares para acceder a los datos y consultarlos**
    * modelo de datos en función de secuencia de registro de atom (ARS) de Hola que base de datos de Azure Cosmos se basa en forma nativa es compatible con varios modelos de datos, incluyendo pero sin limitarse toodocument, gráfico, clave y valor, tabla y modelos de datos en columnas.
    * Se admiten las API de hello después de modelos de datos con los SDK disponible en varios idiomas:
        * [API de DocumentDB](documentdb-introduction.md)
        * [API de MongoDB](mongodb-introduction.md)
        * [Table API](table-introduction.md)
        * [API de Graph (Gremlin)](graph-introduction.md)
        * Modelos de datos adicionales disponibles próximamente 

* **Escalado elástico del rendimiento y el almacenamiento a petición en todo el mundo**
    * Escale fácilmente el rendimiento de la base de datos por [segundos](request-units.md) y cámbielo cuando quiera. 
    * Escalar el tamaño de almacenamiento [forma transparente y automática](partition-data.md) toohandle sus requisitos de tamaño ahora e indefinidamente.

* **Creación de aplicaciones muy adaptables y de misión crítica**
    * Base de datos de Azure Cosmos garantiza-to-end baja latencia en hello los clientes tooits de percentil 99 º. 
    * Para un artículo KB 1 típico, Cosmos DB garantiza la latencia de extremo a extremo de lecturas en 10 ms y escrituras indizadas en 15 ms en percentil 99 de hello, Hola dentro mismo región de Azure. las latencias de mediana de Hello son mucho menores (en ms 5).

* **Disponibilidad "siempre activa" garantizada**
    * Disponibilidad del 99,99 % en una única región.
    * Implementar el número de tooany de [regiones de Azure](https://azure.microsoft.com/regions) para una mayor disponibilidad.
    * [Simule un error](regional-failover.md) en una o más regiones sin pérdida de datos, garantizada. 

* **Escribir aplicaciones distribuidas globalmente, hello manera correcta**
    * Cinco [modelos de coherencia](consistency-levels.md) modelos proporcionan un espectro de homogeneidad similar a SQL todos Hola coherencia definitiva de forma similar a tooNoSQL y cada cosa en entre. 
  
* **Garantía de devolución del dinero**
    * Los datos llegarán rápidamente o le devolvemos el dinero. 
    * [Acuerdos de nivel de servicio](https://aka.ms/acdbsla) para la disponibilidad, la latencia, el rendimiento y la coherencia. 

* **Sin administración de esquema o índice de la base de datos**
    * Deje de preocuparse acerca de cómo mantener sus esquemas e índices de la base de datos e índices en sincronía con el esquema de la aplicación. No usamos esquemas. 
    * Motor de base de datos de Azure Cosmos base de datos es completamente independiente del esquema: automáticamente indiza todos los datos de Hola se introduce sin necesidad de ningún esquema ni índices y actúa increíblemente consultas rápidas. 

* **Costo de propiedad reducido**
    * Cinco veces tooten [más rentable](https://aka.ms/cosmos-db-tco-paper) que una solución no administrada.
    * Tres veces más económica que DynamoDB.

## <a name="capability-comparison"></a>Comparación de funcionalidades

Base de datos de Azure Cosmos proporciona mejores capacidades de Hola de bases de datos relacionales y no relacionales.

| Capacidades | Bases de datos relacionales   | Bases de datos no relacionales (NoSQL) |    Azure Cosmos DB |
| --- | --- | --- | --- |
| Distribución global | No | No | Sí, distribución inmediata en más de 30 regiones, con las API de hospedaje múltiple|
| Escalado horizontal | No | Sí | Sí, puede escalar de manera independiente el almacenamiento y el rendimiento | 
| Garantías de latencia | No | Sí | Sí, 99 % de lecturas en <10 ms y escrituras de <15 ms. | 
| Alta disponibilidad | No | Sí | Sí, Cosmos DB siempre está activo, ofrece compensaciones PACELC y proporciona opciones de conmutación por error automáticas y manuales|
| Modelo de datos + API | Relacional + SQL | Varios modelos + API de OSS | Varios modelos + SQL + API de OSS (más próximamente) |
| SLA | Sí | No | Sí, SLA integrales para la latencia, el rendimiento, la coherencia y la disponibilidad |


## <a name="next-steps"></a>Pasos siguientes
Comience a usar Azure Cosmos DB con una de nuestras guías rápidas:

* [Introducción a la API DocumentDB para Azure Cosmos DB](create-documentdb-dotnet.md)
* [Introducción a la API MongoDB para Azure Cosmos DB](create-mongodb-nodejs.md)
* [Introducción a la API Graph para Azure Cosmos DB](create-graph-dotnet.md)
* [Introducción a la API Table para Azure Cosmos DB](create-table-dotnet.md)
