---
title: 'Azure Cosmos DB: unidades de solicitud por minuto (RU/m) | Microsoft Docs'
description: "Obtenga información acerca de cómo tooreduce costo, gracias a la solicitud de unidades por minuto."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Unidades de solicitud por minuto en Azure Cosmos DB

Base de datos de Azure Cosmos es diseñada toohelp lograr un rendimiento rápido y predecible y escala perfectamente junto con el crecimiento de la aplicación. Puede aprovisionar el rendimiento de un contenedor de Cosmos DB en granularidades de unidades de solicitud por segundo y por minuto (RU/m). Hola rendimiento aprovisionado en una granularidad por minuto es toomanage usado inesperados picos de carga de trabajo de Hola que se producen en una granularidad por segundo. 

Este artículo proporciona información general sobre cómo funciona el aprovisionamiento de saludo de solicitud unidad por minuto (RU/m). objetivo de Hello en cuenta con el aprovisionamiento del RU/m es tooprovide un rendimiento predecible alrededor de las necesidades imprevisibles (especialmente si necesita toorun análisis sobre los datos operativos) y las cargas de trabajo picos. Queremos toohave que nuestros clientes consumen más rendimiento Hola aprovisionan por lo que puede escalar rápidamente con la tranquilidad de saber.

Después de leer este artículo, será hello tooanswer pueda siguientes preguntas:

* ¿Cómo funciona una unidad de solicitud por minuto?
* ¿Cuál es la diferencia de hello entre solicitar unidad por minuto y unidad de solicitud por segundo?
* ¿Cómo tooprovision RU/m?
* ¿En qué escenario consideraré la posibilidad de aprovisionar la unidad de solicitud por minuto?
* ¿Cómo toouse Hola métricas portal toooptimize el costo y el rendimiento?
* Defina qué tipo de solicitud puede consumir el presupuesto de RU/m.

## <a name="provisioning-request-units-per-minute-rum"></a>Aprovisionamiento de unidades de solicitud por minuto (RU/m)

Al aprovisionar la base de datos de Azure Cosmos con granularidad de hello segundo (RU/s), obtendrá garantía de Hola que la solicitud es correcta en una latencia baja si el rendimiento no superó la capacidad de hello aprovisionado en ese segundo. Con RU/m, la granularidad de Hola se encuentra en minuto Hola con garantía de Hola que la solicitud se realiza correctamente en ese minuto. En comparación con los sistemas toobursting, nos aseguramos de que obtendrá de rendimiento de hello es predecible y piensa en ella.

Hola por minuto aprovisionamiento funciona de forma sencilla:

* RU/m se factura cada hora y en suma tooRU/s. Para obtener más información, visite la [página de precios](https://aka.ms/acdbpricing) de Azure Cosmos DB.
* RU/m se puede habilitar en el nivel de colección. Esto puede realizarse a través de hello SDK (Node.js, Java o. NET) o a través del portal de hello (que también se incluyen las cargas de trabajo de la API de MongoDB)
* Cuando se habilita RU/m, para cada 100 RU/s aprovisionado, también obtendrá 1.000 RU/m aprovisionado (relación de hello es x 10)
* En un segundo determinado, una unidad de solicitud consume su aprovisionamiento de RU/m solo si ha superado su aprovisionamiento por segundo durante ese segundo
* Una vez Hola finaliza el período de 60 segundos (UTC), se ha rellenado Hola por minuto de aprovisionamiento
* RU/m se puede habilitar solo para colecciones con un aprovisionamiento máximo de 5000 RU/s por partición. Si escala sus necesidades de rendimiento y tiene ese alto nivel de aprovisionamiento por partición, recibirá un mensaje de advertencia

A continuación vemos un ejemplo concreto, en el cual un cliente puede aprovisionar 10 000 RU/s con 100 000 RU/m, ahorrando un 73 % del costo frente al aprovisionamiento por pico (en 50 000 RU/seg.) a través de un período de 90 segundos de una colección que tiene 10 000 RU/s y 100 000 RU/m aprovisionados:

* 1 segundo: asignación de hello RU/m se establece en 100 000
* 3er segundo: durante esa segunda aparición de Hola el consumo de unidad de la solicitud era 11,010 RUs, 1,010 RUs anteriormente Hola RU/s aprovisionamiento. Por lo tanto, 1,010 RUs se deducen del presupuesto RU/m de Hola. Están disponibles para hello 98,990 RUs siguientes 57 segundos en presupuesto de hello RU/m
* segundo 29: durante ese segundo, se produjo un pico grande (> 4 x superior aprovisionamiento por segundo) y el consumo de Hola de unidad de la solicitud era 46,920 RUs. 36,920 RUs se deducen del presupuesto RU/m de Hola que quita de 92,323 too55 RUs (segundo 28), 403 RUs (29 segundos)
* segundo 61st: presupuesto RU/m se vuelve a establecer too100, 000 RUs.
 
![Gráfico que muestra el consumo de Hola y el aprovisionamiento de la base de datos de Azure Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>Especificación de la capacidad de unidad de solicitud con RU/m

Al crear una colección de base de datos de Azure Cosmos, especifique el número de Hola de unidades de solicitud por segundo (RU por segundo) desea reservar para la recopilación de Hola. También puede decidir si desea tooadd RU por minuto. Esto puede realizarse a través de hello Portal o hello SDK. 

### <a name="through-hello-portal"></a>A través de hello Portal

Para habilitar o deshabilitar RU por minuto, basta con hacer un solo clic al aprovisionar una colección. 

 ![Captura de pantalla que se muestra cómo tooset RU/m Hola portal de Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>A través de hello SDK
En primer lugar, se trata de toonote importante que RU/m solo está disponible para hello siguientes SDK:

* .NET 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

Este es un fragmento de código para crear una colección con 3.000 unidades de solicitud por unidades de solicitud de segundo y 30.000 por minuto con hello .NET SDK:

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

Este es un fragmento de código para cambiar el rendimiento de una colección too5 Hola, 000 unidades de solicitud por segundo sin aprovisionamiento RU por minuto utilizando Hola .NET SDK:

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>Escenarios de buen ajuste

En esta sección, proporcionamos información general de escenarios de buen ajuste para habilitar unidades de solicitud por minuto.

**Entorno de desarrollo y pruebas:** buen ajuste. Durante la fase de desarrollo de hello, si va a probar la aplicación con distintas cargas de trabajo, RU/m puede proporcionar flexibilidad de hello en esta fase. Mientras hello [emulador](local-emulator.md) es una base de datos de Azure Cosmos tootest de excelente herramienta gratuita. Sin embargo si desea toostart en un entorno de nube, tendrá una gran flexibilidad con RU/m para sus necesidades de rendimiento "ad hoc". Pasará más tiempo desarrollando que preocupándose de las necesidades de rendimiento al principio. Se recomienda empezar con el aprovisionamiento de hello mínimo RU/s y habilitar RU/m.

**Necesidades de granularidad de minuto con picos impredecibles:** buen ajuste. Ahorro: 25-75 %. Hemos observado una gran mejora con respecto a RU/m, estando en dicho grupo la mayoría de los escenarios de producción. Si tiene una carga de trabajo de IoT tiene pico varias veces en un minuto, si dispone de las consultas se ejecutan cuando el sistema realiza insertar masivamente en hello mismo tiempo, necesitará capacidad adicional para necesidades de handeling picos. Recomendamos optimizar sus necesidades de recursos aplicando nuestro enfoque paso a paso a continuación.

 ![Gráfico donde se muestra el consumo de la solicitud en una granularidad de cinco minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Ilustración: prueba comparativa de consumo de RU*

**Tranquilidad:** buen ajuste. Ahorro: 10-20 %. A veces, simplemente desea toohave tranquilidad y no preocuparse sobre los posibles picos de actividad y la limitación. Esta característica es Hola right uno automáticamente. En ese caso, recomendamos habilitar RU/m y, de un modo ligeramente menos intenso, su aprovisionamiento por segundo. En este caso es diferente de hello anteriormente como no intentará hacerlo toooptimize activamente el aprovisionamiento. Esto es más como una mentalidad de “limitación cero” que adopta.

Las operaciones críticas con necesidades de "ad hoc": en ocasiones, se recomienda tooonly permiten operaciones críticas acceso RU/m presupuesto para no obtener presupuesto Hola consumir por "ad hoc" o menos importantes operaciones. Que se pueden definir fácilmente en la siguiente sección de Hola.

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>Uso de hello métricas portal toooptimize costo y el rendimiento

**En las próximas semanas hello, se desarrollará más contenido de hello alrededor RUs consumo minuto toooptimize que las necesidades de rendimiento de supervisión.**

A través de las métricas de portal de hello, puede ver la cantidad de segundos de RU regulares utilizas frente a RU minutos. La supervisión de estas métricas debe ayudarle a optimizar su aprovisionamiento. 

Se recomienda un enfoque de paso a paso acerca de cómo toouse RU/m tooyour ventaja. Para cada paso, debe tener una visión general del consumo de hello RU que representa un ciclo completo de la carga de trabajo (podría ser horas, días, o incluso semanas), obtendrá información sobre la utilización de Hola de lo que se aprovisiona.

principio de Hello detrás de este enfoque es toomake el aprovisionamiento de rendimiento como cerrar como posibles tooa aprovisionamiento punto que coincida con los rendimiento de los siguientes criterios. 

![Gráfico donde se muestra el consumo de la solicitud en una granularidad de cinco minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand Hola aprovisionamiento punto óptimo para la carga de trabajo, debe toounderstand:

* Patrones de consumo: ¿picos inexistentes, poco frecuentes o sostenidos? ¿Picos pequeños (doble de media), medios o grandes (más de 10 veces de media)?
* Porcentaje de solicitudes limitadas: ¿se siente cómodo en caso de tener un poco de limitación? Si es así, ¿en qué medida? 

Cuando haya identificado ¿cuáles son los objetivos, es posible que pueda tooget cuanto más se acerque toohello óptimo de aprovisionamiento.

tooassist, queremos tooprovide una orientación general sobre cómo toooptimize su aprovisionamiento según su consumo RU/m. Esta guía no aplica tooall tipo de cargas de trabajo, pero se basa en el conocimiento de la vista previa privada de Hola. Puede que cambiemos estas líneas base a medida que obtenemos más información:

|RU/m % uso|Grado de uso de RU/m|Medidas recomendadas para el aprovisionamiento|
|---|---|---|
|0-1%|En uso|Reducir RU/s tooconsume más RU/m|
|1-10%|Uso correcto|Mantener hello mismo aprovisionamiento nivel|
|Por encima del 10%|Uso excesivo|Aumentar RU/s toorely menos en RU/m.|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>Seleccione qué operaciones pueden consumir el presupuesto de hello RU/m

En el nivel de solicitud, puede también habilitar o deshabilitar la solicitud de RU/m presupuesto tooserve Hola independientemente del tipo de operación. Si se consume regular aprovisionado presupuesto de RUs/seg. y solicitud de hello no puede usar el presupuesto de hello RU/m, se limitarán esta solicitud. De forma predeterminada, el presupuesto de RU/m atiende todas las solicitudes si se activa el presupuesto de rendimiento de RU/m. 

Este es un fragmento de código para deshabilitar la asignación de RU/m con hello API de documentos para las operaciones CRUD y consulta.

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>Pasos siguientes

En este artículo hemos descrito el funcionamiento de las particiones en Azure Cosmos DB, cómo crear colecciones particionadas y cómo elegir una buena clave de partición para la aplicación.

* Realice pruebas de escala y de rendimiento con Azure Cosmos DB. Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md) para ver ejemplos.
* Comenzar a codificar con hello [SDK](documentdb-sdk-dotnet.md) o hello [API de REST](/rest/api/documentdb/).
* Información sobre el [procesamiento aprovisionado](request-units.md) en Azure Cosmos DB 

