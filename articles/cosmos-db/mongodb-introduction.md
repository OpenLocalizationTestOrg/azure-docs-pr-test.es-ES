---
title: "Introducción tooAzure DB Cosmos: API de MongoDB | Documentos de Microsoft"
description: "Obtenga información acerca de cómo puede utilizar la base de datos de Azure Cosmos toostore y grandes volúmenes de consulta de documentos JSON con el uso de baja latencia Hola populares OSS MongoDB APIs."
keywords: "Qué es MongoDB"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>Introducción tooAzure DB Cosmos: API de MongoDB

[Azure Cosmos DB](../cosmos-db/introduction.md) es un servicio de base de datos con varios modelos y distribución global de Microsoft para aplicaciones críticas. Proporciona la base de datos de Azure Cosmos [distribución global preparada](distribute-data-globally.md), [escalado flexible de rendimiento y almacenamiento](partition-data.md) latencias de milisegundo en todo el mundo, solo dígito se escriben en el percentil 99 de hello, [cinco niveles de coherencia bien definido](consistency-levels.md)y garantiza la alta disponibilidad, todo ello respaldado por [líderes en la industria SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de datos de Azure Cosmos [automáticamente los datos de índices](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sin necesidad de toodeal con administración de esquema y de índice. Sigue varios modelos y es compatible con los modelos de datos de documento, de clave-valor, de grafo y de columnas. 

![Azure Cosmos DB: API de MongoDB](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Las bases de datos de COSMOS DB se pueden usar como almacén de datos de Hola para aplicaciones escritas para [MongoDB](https://docs.mongodb.com/manual/introduction/). Esto significa que mediante [controladores](https://docs.mongodb.org/ecosystem/drivers/) existentes, la aplicación escrita para MongoDB se puede comunicar ahora con Cosmos DB y usar bases de datos de Cosmos DB en lugar de bases de datos de MongoDB. En muchos casos, puede cambiar del uso de MongoDB tooCosmos DB cambiando simplemente una cadena de conexión. Con esta funcionalidad, puede crear fácilmente y ejecutar aplicaciones de base de datos de MongoDB en hello Azure en la nube con la distribución global de Azure Cosmos DB y [líderes SLA completa de la industria](https://azure.microsoft.com/support/legal/sla/cosmos-db), mientras continúa toouse familiar conocimientos y herramientas para MongoDB.


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>¿Cuál es el beneficio de hello del uso de base de datos de Azure Cosmos para aplicaciones de MongoDB?

**Rendimiento escalables de manera flexible y almacenamiento:** escalar verticalmente o hacia abajo el toomeet de la base de datos de MongoDB necesita la aplicación. Los datos se almacenan en discos de estado sólido (SSD) para las bajas latencias predecibles. COSMOS DB admite colecciones de MongoDB que se pueden escalar toovirtually tamaños de almacenamiento ilimitado y rendimiento aprovisionado. Según vaya creciendo su aplicación, puede escalar Cosmos DB de manera flexible con un rendimiento predecible impecable. 

**Replicación de varias regiones:** Cosmos DB replica de forma transparente las áreas de tooall de datos que se ha asociado con su cuenta de MongoDB, lo que las aplicaciones de toodevelop que requieren acceso global toodata al proporcionar equilibrio entre la coherencia, disponibilidad y rendimiento, todos los datos con garantías correspondientes. COSMOS DB proporciona transparente conmutación por error regional con las API de hospedaje múltiple y el rendimiento de escala de tooelastically de capacidad de Hola y el almacenamiento en todo el mundo de Hola. Obtenga más información en [Distribución de datos global con DocumentDB](distribute-data-globally.md).

**Compatibilidad de MongoDB**: puede usar su experiencia, el código de la aplicación y las herramientas de MongoDB existentes. Puede desarrollar aplicaciones con MongoDB e implementarlas tooproduction mediante Hola totalmente administrado servicio de base de datos de Cosmos distribuido globalmente.

**Ninguna administración de servidor**: no tiene toomanage y escalar las bases de datos de MongoDB. COSMOS DB es un servicio completamente administrado, lo que significa que no tiene toomanage ninguna infraestructura o máquinas virtuales por sí mismo. Cosmos DB está disponible en más de 30 [regiones de Azure](https://azure.microsoft.com/regions/services/).

**Niveles de coherencia ajustables:** Select en cinco bien definida coherencia niveles tooachieve un equilibrio óptimo entre coherencia y rendimiento. Para las consultas y las operaciones de lectura, Cosmos DB ofrece cinco niveles de coherencia diferentes: segura, obsolescencia limitada, sesión, prefijo coherente y posible. Estos niveles de coherencia granular y bien definidos permiten toomake sonido ventajas y desventajas de coherencia, la disponibilidad y la latencia. Obtenga más información en [utilizando coherencia los niveles de rendimiento y la disponibilidad de toomaximize](consistency-levels.md).

**La indexación automática**: de forma predeterminada, Cosmos DB automáticamente indiza todas las propiedades de hello dentro de los documentos en la base de datos de MongoDB y no esperan o requieren cualquier esquema o la creación de índices secundarios.

**Nivel empresarial** -base de datos de Azure Cosmos admite varias réplicas locales toodeliver 99,99% disponibilidad y protección de datos en la cara de Hola de errores locales y regionales. Azure Cosmos DB presenta [certificaciones de conformidad](https://www.microsoft.com/trustcenter) y características de seguridad de nivel empresarial. 

Aprenda más en este vídeo de Azure Friday con Scott Hanselman y Kirill Gavrylyuk, Administrador de ingeniería principal de Azure Cosmos DB.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>Cómo iniciar tooget

Siga Hola MongoDB tutoriales toocreate una cuenta de base de datos de Cosmos y migrar su toouse de aplicación de Mongo DB Cosmos DB existente o crear uno nuevo:

* [Migrar una aplicación web MongoDB existente de Node.js](create-mongodb-nodejs.md)
* [Compilar una aplicación web de API de MongoDB con hello portal de Azure y .NET](create-mongodb-dotnet.md)
* [Compilar una aplicación de consola de API de MongoDB con hello portal de Azure y Java](create-mongodb-java.md)

## <a name="next-steps"></a>Pasos siguientes

Información sobre la API de Azure Cosmos base de datos MongoDB se integra en hello documentación general Azure Cosmos DB, pero hay algunos tooget de punteros que se inició:

* Siga hello [conectar tooa MongoDB cuenta](connect-mongodb-account.md) toolearn tutorial cómo tooget información de cadena de conexión de su cuenta.
* Siga hello [MongoChef de uso con la base de datos de Azure Cosmos](mongodb-mongochef.md) toolearn tutorial cómo toocreate una conexión entre la base de datos de base de datos de Azure Cosmos y aplicación de MongoDB en MongoChef.
* Siga hello [migrar datos tooAzure Cosmos DB con compatibilidad con el protocolo para MongoDB](mongodb-migrate.md) tutorial tooimport su tooan de datos API de base de datos de MongoDB.
* Conectar tooan API para el uso de la cuenta de MongoDB [Robomongo](mongodb-robomongo.md).
* Obtenga información acerca de cuántos RUs utilizan las operaciones con hello [GetLastRequestStatistics comando y Hola métricas portales Azure](request-units.md#GetLastRequestStatistics).
* Obtenga información acerca de cómo demasiado[configurar las preferencias de lectura para las aplicaciones distribuidas globalmente](../cosmos-db/tutorial-global-distribution-mongodb.md).
