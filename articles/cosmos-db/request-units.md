---
title: aaaRequest unidades & calcular rendimiento - base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo especificar toounderstand y estimar los requisitos de la unidad de solicitud en la base de datos de Azure Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a>Unidades de solicitud en Azure Cosmos DB
Ya disponible: la [calculadora de unidades de solicitud](https://www.documentdb.com/capacityplanner) de Azure Cosmos DB. Obtenga más información en [Estimación de las necesidades de rendimiento](request-units.md#estimating-throughput-needs).

![Calculadora de rendimiento][5]

## <a name="introduction"></a>Introducción
[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Con la base de datos de Azure Cosmos, no tiene máquinas virtuales que toorent, implementar software o supervisar las bases de datos. Base de datos de Azure Cosmos se opera y continuamente supervisado por Microsoft ingenieros superior toodeliver world clase disponibilidad, rendimiento y protección de datos. Puede acceder a sus datos con las API de su preferencia, como [DocumentDB SQL](documentdb-sql-query.md) (documentos), MongoDB (documentos), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (clave-valor) y [Gremlin](https://tinkerpop.apache.org/gremlin.html) (grafos), que admite de forma nativa. moneda Hola de base de datos de Azure Cosmos es hello unidad de solicitud (RU). Con RUs, no es necesario tooreserve capacidades de lectura/escritura o aprovisionar CPU, memoria y e/s por segundo.

Base de datos de Azure Cosmos es compatible con una serie de interfaces API con diferentes operaciones comprendido entre lecturas simples y escribe toocomplex consultas de gráfico. Puesto que no todas las solicitudes son iguales, se asignan una cantidad normalizada de **unidades de solicitud** según la cantidad de Hola de solicitud de cálculo necesarios tooserve Hola. número de Hola de unidades de solicitud para una operación es determinista y puede realizar un seguimiento de número de Hola de unidades de solicitud consumidas por cualquier operación en la base de datos de Azure Cosmos a través de un encabezado de respuesta. 

tooprovide un rendimiento predecible, es necesario tooreserve rendimiento en unidades de 100 RU/segundo. 

Después de leer este artículo, podrá hello tooanswer pueda siguientes preguntas:  

* ¿Qué son las unidades de solicitud y los cargos de solicitud?
* ¿Cómo se puede especificar la capacidad de unidad de solicitud para una colección?
* ¿Cómo puedo estimar mis necesidades de unidad de solicitud de la aplicación?
* ¿Qué ocurre si supero la capacidad de la unidad de solicitud para una colección?

Base de datos de Azure Cosmos sea una base de datos de varios modelo, es importante toonote que nos referiremos tooa colección/documento de un documento de API, un nodo de gráfico/para una API de graph y una tabla o entidad para la API de la tabla. Rendimiento de este documento se generalizará toohello conceptos de contenedor de elementos.

## <a name="request-units-and-request-charges"></a>Unidades de solicitud y cargos de solicitud
Base de datos de Cosmos Azure ofrece un rendimiento rápido y predecible por *reservar* necesidades de rendimiento de la aplicación de recursos toosatisfy.  Como aplicación de carga y patrones de acceso cambian con el tiempo, base de datos de Azure Cosmos permite tooeasily aumentar o reducir Hola de aplicación tooyour disponible de rendimiento reservados.

Con Azure Cosmos DB, el rendimiento reservado se especifica en términos de procesamiento de unidades de solicitud por segundo. Se puede considerar de unidades de solicitud como moneda de rendimiento, mediante el cual se *reservar* garantiza que una cantidad de unidades de solicitud aplicación tooyour disponible en por segundo.  Cada operación de Azure Cosmos DB: escritura de un documento, realización de una consulta, actualización de un documento, consume CPU, memoria y E/S por segundo.  Es decir, cada operación implica un *cargo de solicitud*, que se expresa en *unidades de solicitud*.  Descripción de los factores de Hola que afectan a los cargos de unidad de solicitud, junto con los requisitos de rendimiento de su aplicación, permite que se toorun la aplicación como costo eficazmente como sea posible. Explorador de consulta de Hello es también una maravillosa herramienta tootest Hola de principales de una consulta.

Se recomienda introducción, inspeccionando Hola después de vídeo, donde se explica Aravind Ramachandran unidades de solicitud y un rendimiento predecible con la base de datos de Azure Cosmos.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>Especificación de la capacidad de unidad de solicitud en Azure Cosmos DB
Al iniciar una nueva colección, tabla o gráfico, especifique el número de Hola de unidades de solicitud por segundo (RU por segundo) que desea reservada. En función de rendimiento aprovisionado hello, base de datos de Azure Cosmos asigna toohost de particiones físicas en la colección y divisiones/rebalancea datos entre particiones cuando crece.

Base de datos de Azure Cosmos requiere que un toobe de clave de partición especificado cuando una colección está aprovisionado con 2.500 unidades de solicitud o superior. Una clave de partición también es necesario tooscale el rendimiento de la colección más allá de 2.500 unidades de solicitud en hello futuras. Por lo tanto, se recomienda encarecidamente tooconfigure una [clave de partición](partition-data.md) al crear un contenedor, independientemente de su rendimiento inicial. Dado que los datos podrían tener toobe dividir en varias particiones, es necesario toopick una clave de partición que tenga una cardinalidad alta (100 toomillions de valores distintos) para que la colección, tabla o gráfico y las solicitudes se pueden escalar uniformemente por base de datos de Azure Cosmos. 

> [!NOTE]
> Una clave de partición es un límite lógico, no uno físico. Por lo tanto, no es necesario el número de hello toolimit de valores de clave de partición distintos. De hecho es mejor toohave mayor que menor, los valores de clave de partición como base de datos de Azure Cosmos tiene más opciones de equilibrio de carga.

Este es un fragmento de código para crear una colección con 3.000 solicitud unidades por segundo mediante Hola .NET SDK:

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure Cosmos DB funciona con un modelo de reserva del rendimiento. Es decir, se le cobra según cantidad Hola de rendimiento *reservada*, independientemente de la cantidad de ese rendimiento está activamente *utiliza*. Como carga, datos y el uso cambien los patrones la aplicación puede escalar fácilmente arriba y abajo Hola cantidad de RUs reservadas mediante SDK o con hello [Portal de Azure](https://portal.azure.com).

Se asignan a cada colección, tabla o gráfico tooan `Offer` recursos en Azure Cosmos DB, que contiene los metadatos sobre el rendimiento aprovisionado Hola. Puede cambiar rendimiento Hola asignada, búsqueda de recurso de oferta correspondiente de Hola para un contenedor y actualizarla con el nuevo valor de rendimiento Hola. Este es un fragmento de código para cambiar el rendimiento de una colección too5 hello, 000 unidades de solicitud por segundo con Hola .NET SDK:

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

Cuando se cambia el rendimiento de hello, hay sin disponibilidad de toohello del impacto del contenedor. Rendimiento reservadas nuevas Hola suele ser eficaz en segundos en la aplicación de rendimiento nuevo Hola.

## <a name="request-unit-considerations"></a>Consideraciones de la unidad de solicitud
Al calcular el número de Hola de tooreserve de unidades de solicitud para el contenedor de la base de datos de Azure Cosmos, es hello tootake importante después de las variables en cuenta:

* **Tamaño del elemento**. Como tamaño aumenta Hola unidades consumidas tooread o escribir datos de hello también aumentará.
* **Recuento de propiedades del elemento**. Suponiendo que de forma predeterminada la indización de todas las propiedades, Hola unidades consumidas toowrite un documento, nodo/ntity aumentará como Hola propiedad recuento aumenta.
* **Coherencia de datos**. Cuando se usa niveles de coherencia de datos de Strong o Bounded Staleness, unidades adicionales será consumido tooread elementos.
* **Propiedades indexadas**. Una directiva de índice en cada contenedor determina qué propiedades se indexan de forma predeterminada. Puede reducir el consumo de unidades de solicitud limitando el número de Hola de las propiedades indizadas o habilitando la indexación diferida.
* **Indexación de documentos**. De forma predeterminada, que cada elemento se indiza automáticamente, consumirá menos unidades de solicitud si elige no tooindex algunos de los elementos.
* **Patrones de consultas**. complejidad de Hola de una consulta afecta a cuántas unidades de solicitud se usan para una operación. número de Hola de predicados, naturaleza de los predicados de hello, proyecciones, número de UDF y el tamaño de hello del conjunto de datos de origen de hello todos influyen en el costo de Hola de operaciones de consulta.
* **Uso de script**.  Al igual que con las consultas, procedimientos almacenados y desencadenadores consumen unidades de solicitud basándose en hello complejidad de las operaciones de Hola que se está realizando. Al desarrollar la aplicación, inspeccionar el cargo de la solicitud de hello toobetter encabezado entender cómo cada operación consume una capacidad de unidad de solicitud.

## <a name="estimating-throughput-needs"></a>Estimación de necesidades de rendimiento
Una unidad de solicitud es una medida normalizada del costo de procesamiento de solicitudes. Una unidad única solicitud representa Hola procesamiento capacidad requerida tooread (a través de vínculos propios o Id. de) un elemento que se compone de 10 valores de la propiedad unique (excepto las propiedades del sistema) de 1KB único. Un toocreate de solicitud (insert), reemplazar o eliminar Hola mismo elemento consumirá más capacidad de procesamiento del servicio de hello y, por tanto, más unidades de solicitud.   

> [!NOTE]
> línea de base de Hola de unidad 1 solicitud para un 1KB elemento corresponde tooa simple obtener por Id. de elemento de Hola o vínculo propio.
> 
> 

Por ejemplo, aquí es una tabla que muestra cuántos solicitar unidades tooprovision en tres tamaños de los distintos elementos (1KB, 4KB y 64KB) y en dos niveles de rendimiento diferentes (500 lecturas por segundo 100 escrituras por segundo y 500 lecturas por segundo + 500 escrituras por segundo). coherencia de los datos Hola se configuró en la sesión y Hola directiva de indexación se estableció tooNone.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Tamaño del elemento</strong></p></td>
            <td valign="top"><p><strong>Lecturas/segundo</strong></p></td>
            <td valign="top"><p><strong>Escrituras/segundo</strong></p></td>
            <td valign="top"><p><strong>Unidades de solicitud</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1,3) + (100 * 7) = 1350 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1,3) + (500 * 7) = 4150 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9800 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29 000 RU/s</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a>Usar la calculadora de unidades de solicitud de Hola
clientes toohelp bien optimizar sus estimaciones de rendimiento, no hay una basada en web [Calculadora de unidades de solicitud](https://www.documentdb.com/capacityplanner) toohelp estimación Hola solicitud requisitos de la unidad para las operaciones típicas, incluidos:

* Creaciones (escrituras) de elementos
* Lecturas de elementos
* Eliminaciones de elementos
* Actualizaciones de elementos

herramienta de Hello también incluye compatibilidad para calcular las necesidades de almacenamiento de datos basadas en los elementos de ejemplo de Hola que proporcione.

Uso de herramienta de hello es simple:

1. Cargue uno o más elementos representativos.
   
    ![Cargar la calculadora de unidades de solicitud de elementos toohello][2]
2. requisitos de almacenamiento de datos de tooestimate, escriba el número total de Hola de elementos esperados toostore.
3. Introducir número de Hola de elementos de crear, leer, actualizar y eliminar operaciones requieren (de forma por segundo). cargos de unidad de solicitud tooestimate Hola de operaciones de actualización del elemento, cargar una copia del elemento de ejemplo de Hola del paso 1 anterior que incluye actualizaciones de campo típico.  Por ejemplo, si las actualizaciones de elementos normalmente modificar dos propiedades denominadas lastLogin y userVisits y, a continuación, basta con copiar el elemento de ejemplo de Hola, actualice los valores de hello de esas dos propiedades y cargar Hola copiar elemento.
   
    ![Especificar los requisitos de rendimiento de la calculadora de unidad de solicitud de Hola][3]
4. Haga clic en calcular y examinar los resultados de Hola.
   
    ![Resultados de la calculadora de unidades de solicitud][4]

> [!NOTE]
> Si tiene tipos de elemento que variarán considerablemente en cuanto al número de hello y tamaño de las propiedades indizadas, a continuación, cargar una muestra de cada *tipo* de toohello elemento típico de herramientas y, a continuación, calcular los resultados de Hola.
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a>Usar el encabezado de respuesta de cargo de solicitud de base de datos de Azure Cosmos de Hola
Cada respuesta de servicio de base de datos de Azure Cosmos Hola incluye un encabezado personalizado (`x-ms-request-charge`) que contiene unidades de solicitud de hello utilizados para la solicitud de saludo. Este encabezado también es accesible a través de hello Azure Cosmos DB SDK. Hola .NET SDK, RequestCharge es una propiedad del objeto de ResourceResponse Hola.  Para las consultas, Hola Explorador de consulta de base de datos de Azure Cosmos Hola portal de Azure proporciona información acerca de cargos de solicitud para las consultas ejecutadas.

![Examen de cargos RU Hola Explorador de consulta][1]

Con esto en mente, un método para calcular la cantidad de Hola de rendimiento reservados requerido por la aplicación es cargo por unidad toorecord Hola solicitud asociado con la ejecución de las operaciones típicas con un elemento representativo utilizado por la aplicación y, a continuación, calcular el número de Hola de operaciones es posible anticipar realizar cada segundo.  Ser toomeasure seguro e incluyen las consultas habituales y uso de scripts de base de datos de Azure Cosmos así.

> [!NOTE]
> Si tiene tipos de elemento que variarán considerablemente en cuanto al número de hello y tamaño de las propiedades indizadas, a continuación, registre el cargo por unidad Hola operación aplicable solicitud asociada a cada uno *tipo* de elemento típico.
> 
> 

Por ejemplo:

1. Registrar Hola cargo de unidad de solicitud de creación (Insertar) un elemento típico. 
2. Cargos de unidad de solicitud de registro Hola de leer un elemento típico.
3. Cargos de unidad de registro Hola solicitud de actualización de un elemento típico.
4. Cargos de unidad de solicitud Hola registro de consultas de elemento típicas, comunes.
5. Cargo de unidad de solicitud de hello registros de los scripts personalizados (procedimientos almacenados, desencadenadores, funciones definidas por el usuario) usado por la aplicación hello
6. Calcular la solicitud requiere Hola que unidades dados Hola estimado número de operaciones prevé toorun cada segundo.

### <a id="GetLastRequestStatistics"></a>Uso del comando GetLastRequestStatistics de la API de MongoDB
API de MongoDB admite un comando personalizado, *getLastRequestStatistics*, para recuperar el cargo de la solicitud de Hola para operaciones específicas.

Por ejemplo, en hello Shell de Mongo; para ello, ejecute operación Hola deseada tooverify Hola solicitud gratuito.
```
> db.sample.find()
```

A continuación, ejecute el comando de hello *getLastRequestStatistics*.
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

Con esto en mente, un método para calcular la cantidad de Hola de rendimiento reservados requerido por la aplicación es cargo por unidad toorecord Hola solicitud asociado con la ejecución de las operaciones típicas con un elemento representativo utilizado por la aplicación y, a continuación, calcular el número de Hola de operaciones es posible anticipar realizar cada segundo.

> [!NOTE]
> Si tiene tipos de elemento que variarán considerablemente en cuanto al número de hello y tamaño de las propiedades indizadas, a continuación, registre el cargo por unidad Hola operación aplicable solicitud asociada a cada uno *tipo* de elemento típico.
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>Uso de las métricas del Portal de la API de MongoDB
Hola tooget de manera más sencilla cargos por una buena estimación de la unidad de solicitud de la API de base de datos de MongoDB es hello toouse [portal de Azure](https://portal.azure.com) métricas. Con hello *número de solicitudes* y *cargo de solicitud* gráficos, puede obtener una estimación de cuántas unidades de solicitud cada operación es el número de unidades de solicitud y utilizar consumen tooone relativa otro.

![Métricas del Portal de la API de MongoDB][6]

## <a name="a-request-unit-estimation-example"></a>Un ejemplo de estimación de la unidad de solicitud
Considere la posibilidad de hello siguiente documento ~ 1KB:

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> Documentos se reduce en la base de datos de Azure Cosmos, por lo que el sistema Hola calcula el tamaño del documento de hello anterior es un poco menos de 1KB.
> 
> 

Hello tabla siguiente muestran solicitud aproximado cargos de unidad para las operaciones típicas de este elemento (cargo de unidad de solicitud aproximado Hola se da por supuesto que el nivel de coherencia de cuenta de hello está establecido demasiado "Sesión" y que todos los elementos se indizan automáticamente):

| Operación | Cargo de la unidad de solicitud |
| --- | --- |
| Crear elemento |~15 RU |
| Lectura de elemento |~1 RU |
| Consulta de elemento por identificador |~2,5 RU |

Además, esta tabla muestra solicitud aproximado cargos de unidad para las consultas habituales que se usan en la aplicación hello:

| Consultar | Cargo de la unidad de solicitud | Número de elementos devueltos |
| --- | --- | --- |
| Selección de alimentos por Id. |~2,5 RU |1 |
| Selección de alimentos por fabricante |~7 RU |7 |
| Selección por grupo de alimentos y clasificación por peso |~70 RU |100 |
| Selección de los 10 alimentos más importantes en un grupo de alimentos |~10 RU |10 |

> [!NOTE]
> Cargos RU varían en función de número de Hola de elementos devueltos.
> 
> 

Con esta información, se pueden estimar los requisitos de RU de Hola para este número de Hola de aplicación dado de operaciones y las consultas que se espera por segundo:

| Operación o consulta | Número estimado por segundo | RU necesarias |
| --- | --- | --- |
| Crear elemento |10 |150 |
| Lectura de elemento |100 |100 |
| Selección de alimentos por fabricante |25 |175 |
| Selección por grupo de alimentos |10 |700 |
| Selección de los 10 principales |15 |150 en total |

En este caso, se espera un requisito de rendimiento medio de 1,275 RU/s.  Redondea hacia arriba toohello más cercano de 100, puede proporcionar 1.300 RU/s para la recopilación de esta aplicación.

## <a id="RequestRateTooLarge"></a> Superación de los límites de rendimiento reservados en Azure Cosmos DB
Recuerde que el consumo de unidad de solicitud se evalúa como una tasa por segundo si presupuesto Hola está vacía. Para las aplicaciones que superan Hola tasa de solicitud de aprovisionamiento de unidad para un contenedor, solicita toothat colección se limitarán hasta que la velocidad de hello cae por debajo del nivel de hello reservado. Cuando se produce una limitación, servidor hello forma preferente finalizará solicitud Hola con RequestRateTooLargeException (código de estado HTTP 429) y Hola devuelto x reintento ms después de ms de encabezado, indicando Hola período de tiempo, en milisegundos, que Hola usuario debe esperar antes de solicitud de hello intentando de nuevo.

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

Si usas las consultas LINQ y SDK de cliente de .NET de hello y, a continuación, la mayoría de los casos de hello nunca tienen toodeal a esta excepción, como la versión actual de Hola de hello SDK del cliente .NET implícitamente detecta esta respuesta, aspectos Hola especificado por el servidor encabezado retry-after, y solicitud de Hola de reintentos. A menos que su cuenta está obteniendo acceso al mismo tiempo varios clientes, el siguiente reintento de Hola se realizará correctamente.

Si tiene más de un cliente de manera acumulativa funcionando por encima de la tasa de solicitud de hello, hello comportamiento para reintentar la predeterminada puede no ser suficiente y cliente de hello producirá un DocumentClientException con 429 toohello aplicación de código de estado. En casos como éste, puede controlar el comportamiento de reintento y la lógica de error de la aplicación rutinas de control o un aumento de rendimiento reservados de hello para el contenedor de Hola.

## <a id="RequestRateTooLargeAPIforMongoDB"></a> Superación de los límites de rendimiento reservados en la API de MongoDB
Las aplicaciones que superan las unidades de solicitud de hello aprovisionado para una colección se limitarán hasta que la velocidad de hello cae por debajo del nivel de hello reservado. Cuando se produce una limitación, Hola back-end forma preferente finalizará solicitud Hola con un *16500* código de error - *demasiado muchas solicitudes*. De forma predeterminada, la API de MongoDB volverá a intentar automáticamente too10 horas antes de devolver un *demasiado muchas solicitudes* código de error. Si recibe muchos *demasiado muchas solicitudes* códigos de error, debe pensar en cualquier comportamiento para reintentar la adición de rutinas de control de errores de la aplicación o [aumenta el rendimiento reservado de hello para la recopilación de hello](set-throughput.md).

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de rendimiento reservados con bases de datos de la base de datos de Azure Cosmos, explorar estos recursos:

* [Precios de Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [Creación de particiones en Azure Cosmos DB](partition-data.md)

toolearn más información acerca de la base de datos de Cosmos de Azure, vea Hola base de datos de Azure Cosmos [documentación](https://azure.microsoft.com/documentation/services/cosmos-db/). 

tooget a trabajar con la escalabilidad y rendimiento de pruebas con la base de datos de Cosmos de Azure, consulte [pruebas de rendimiento y escala con base de datos de Azure Cosmos](performance-testing.md).

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
