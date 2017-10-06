---
title: aaaConnecting Apache Spark tooAzure Cosmos DB | Documentos de Microsoft
description: "Use este tutorial toolearn sobre el conector de Azure Cosmos DB Spark Hola que le permite tooconnect Apache Spark tooAzure Cosmos DB tooperform distribuida agregaciones y las ciencias de datos en el sistema de base de datos distribuidos globalmente multiempresa Hola de Microsoft que está diseñado para la nube de Hola."
keywords: apache spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a>Acelerar el análisis de grandes cantidades de datos en tiempo real con el conector de base de datos de Cosmos de hello Spark tooAzure

Conector de base de datos de Cosmos de Hello Spark tooAzure permite tooact de base de datos de Azure Cosmos como un origen de entrada o el receptor de salida para los trabajos de Apache Spark. Conexión [Spark](http://spark.apache.org/) demasiado[base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) acelera la capacidad toosolve mover fast ciencia de datos problemas que puede usar base de datos de Azure Cosmos tooquickly persisten y consultar datos. Conector de base de datos de Cosmos de Hello Spark tooAzure eficazmente utiliza índices de base de datos de Azure Cosmos administrado nativo Hola. índices de Hello habilitar columnas actualizables cuando realice análisis y filtrado cambiante global de predicado de inserción distribuidas, datos, que abarcan desde toodata ciencia y análisis de escenarios de Internet de las cosas (IoT).

Para trabajar con Spark GraphX y gráfico de Gremlin Hola DB Cosmos API de Azure, consulte [realizar análisis de gráfico usando Spark y Apache TinkerPop Gremlin](spark-connector-graph.md).

## <a name="download"></a>Descargar

tooget iniciado, descargue tooAzure Cosmos DB connector (vista previa) de hello Spark de hello [cosmosdb de azure de spark](https://github.com/Azure/azure-cosmosdb-spark/) repositorio en GitHub.

## <a name="connector-components"></a>Componentes del conector

Conector de Hello utiliza Hola de los componentes siguientes:

* [Base de datos de Azure Cosmos](http://documentdb.com) permite que los clientes tooprovision y escalar de forma elástica rendimiento y almacenamiento a través de cualquier número de regiones geográficas. Hola ofertas de servicio:
   * [Distribución global](distribute-data-globally.md) llave en mano y escala horizontal
   * Garantiza que las latencias de un dígito en percentil 99 Hola
   * [Varios modelos de coherencia bien definida](consistency-levels.md)
   * Garantía de alta disponibilidad con funcionalidades de hospedaje múltiple
   * Todas las características están respaldadas por [Acuerdos de Nivel de Servicio](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA) completos líderes del sector.

* [Apache Spark](http://spark.apache.org/) es un motor de procesamiento de código abierto eficaz diseñado para ofrecer velocidad, facilidad de uso y análisis sofisticados.

* [Apache Spark en HDInsight de Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) para que pueda implementar Apache Spark en nube de Hola para implementaciones críticas mediante el uso de [HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Versiones oficialmente compatibles:

| Componente | Versión |
|---------|-------|
|Spark de Apache|2.0+|
| Scala| 2.11|
| SDK de Java de Azure DocumentDB | 1.10.0 |

En este artículo le ayuda a ejecutar algunos ejemplos simples mediante Python (a través de pyDocumentDB) y Hola Scala interfaces.

Hay dos enfoques tooconnect Apache Spark y base de datos de Azure Cosmos:
- Usar pyDocumentDB a través de hello [SDK de Azure DocumentDB Python](https://github.com/Azure/azure-documentdb-python).
- Crear un conector de base de datos de Cosmos tooAzure Spark basados en Java mediante el uso de hello [SDK de Java de Azure DocumentDB](https://github.com/Azure/azure-documentdb-java).

## <a name="pydocumentdb-implementation"></a>Implementación de pyDocumentDB
Hola actual [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) permite tooconnect Spark tooAzure DB Cosmos como se muestra en hello siguiente diagrama:

![Spark tooAzure Cosmos DB el flujo de datos a través de pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a>Flujo de datos de implementación de hello pyDocumentDB

flujo de datos de Hello es como sigue:

1. nodo maestro de Hello Spark conecta el nodo de puerta de enlace de base de datos de Azure Cosmos toohello mediante pyDocumentDB. Un usuario especifica solo Hola Spark y base de datos de Azure Cosmos conexiones. Las conexiones toohello respectivos maestra y puerta de enlace de nodos son usuario toohello transparente.
2. nodo de puerta de enlace de Hello hace consulta de hello en la base de datos de Azure Cosmos donde consulta Hola ejecuta posteriormente en particiones de la colección de hello en nodos de datos de Hola. respuesta de Hola para esas consultas se le envía toohello nodo de puerta de enlace y ese conjunto de resultados se devuelve el nodo principal de toohello Spark.
3. Las consultas posteriores (por ejemplo, en una trama de datos de Spark) se envían los nodos de trabajador de Spark toohello para su procesamiento.

Comunicación entre Spark y base de datos de Azure Cosmos es limitado toohello nodo maestro Spark y nodos de puerta de enlace de base de datos de Azure Cosmos.  las consultas de Hello van tan rápido como el nivel de transporte de hello entre estos dos nodos permite.

### <a name="install-pydocumentdb"></a>Instalación de pyDocumentDB
Puede instalar pyDocumentDB en el nodo de controlador mediante **pip**, por ejemplo:

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a>Conectar Spark tooAzure Cosmos DB a través de pyDocumentDB
simplicidad de Hola de transporte de comunicación de hello hace la ejecución de una consulta de Spark tooAzure DB Cosmos mediante pyDocumentDB relativamente sencilla.

Hola código fragmento siguiente muestra cómo toouse pyDocumentDB en un contexto de Spark.

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

Como se indica en el fragmento de código de hello:

* Hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contiene Hola Hola a todos los parámetros de conexión necesaria. Por ejemplo, hello preferido parámetro ubicaciones elige Hola lee el orden de prioridad y la réplica.
*  Hola necesarios bibliotecas de importación y configurar su **masterKey** y **host** toocreate Hola base de datos de Azure Cosmos *cliente* (**pydocumentdb.document_ cliente**).


### <a name="execute-spark-queries-via-pydocumentdb"></a>Ejecución de consultas de Spark mediante pyDocumentDB
Hola siguientes ejemplos use Hola base de datos de Azure Cosmos la instancia que se creó en el fragmento de código anterior hello mediante Hola especifica claves de solo lectura. Hello fragmento de código siguiente conecta toohello **airports.codes** colección hello DoctorWho como en cuenta especificada anteriormente y se ejecuta un aeropuerto de consulta tooextract Hola ciudades en el estado de Washington.

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

Una vez ejecutada la consulta de Hola a través de **consulta**, resultado de hello es un **query_iterable. QueryIterable** que es la lista de Python tooa convertido. Una lista de Python puede convertir fácilmente tooa trama de datos de Spark mediante Hola siguiente código:

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a>¿Por qué usar hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?
Conexión tooAzure Spark Cosmos DB mediante el uso de pyDocumentDB es normalmente en escenarios donde:

* Desea toouse Python.
* Devuelve un conjunto de base de datos de Azure Cosmos tooSpark de resultados relativamente pequeño. Tenga en cuenta que Hola conjunto de datos subyacente en la base de datos de Azure Cosmos puede ser bastante grande. Vaya a aplicar filtros, es decir, ejecutar filtros de predicado, en el origen de Azure Cosmos DB.  

## <a name="spark-tooazure-cosmos-db-connector"></a>Spark tooAzure conector de base de datos de Cosmos

Conector de Hello Spark tooAzure Cosmos DB utiliza hello [SDK de Java de Azure DocumentDB](https://github.com/Azure/azure-documentdb-java) y mueve datos entre nodos de trabajador de Spark hello y base de datos de Azure Cosmos como se muestra en hello siguiente diagrama:

![Flujo de datos en el conector de base de datos de Cosmos de hello Spark tooAzure](./media/spark-connector/spark-connector.png)

flujo de datos de Hello es como sigue:

1. nodo maestro de Hello Spark conecta mapa de partición del nodo tooobtain Hola de toohello base de datos de Azure Cosmos puerta de enlace. Un usuario especifica solo Hola Spark y base de datos de Azure Cosmos conexiones. Las conexiones toohello respectivos maestra y puerta de enlace de nodos son usuario toohello transparente.
2. Esta información se proporciona el nodo principal de toohello atrás Spark.  En este punto, debe ser particiones de tooparse capaz de hello consulta toodetermine hello y sus ubicaciones en la base de datos de Azure Cosmos que necesita tooaccess.
3. Esta información es nodos de trabajador de la información transmitida toohello Spark.
4. nodos de trabajador de Hello Spark conectan particiones de base de datos de Azure Cosmos toohello directamente tooextract Hola datos y devolver Hola datos toohello particiones Spark en nodos de trabajador de hello Spark.

Comunicación entre Spark y base de datos de Azure Cosmos es mucho más rápido porque el movimiento de datos de hello es entre nodos de trabajador de Spark hello y nodos de datos de base de datos de Azure Cosmos hello (particiones).

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a>Compilar el conector de base de datos de Cosmos de hello Spark tooAzure
Actualmente, el proyecto de conector de hello utiliza a maven. Conector de hello toobuild sin dependencias, puede ejecutar:
```
mvn clean package
```
También puede descargar versiones más recientes de Hola de hello JAR de hello *libera* carpeta.

### <a name="include-hello-azure-cosmos-db-spark-jar"></a>Incluir hello Azure Cosmos DB Spark JAR
Antes de ejecutar cualquier código, debe hello tooinclude Azure Cosmos DB Spark JAR.  Si usas hello **spark shell**, a continuación, puede incluir Hola JAR mediante hello **--archivos JAR** opción.  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

Si desea tooexecute Hola JAR sin dependencias, utilice Hola siguiente código:

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

Si usas un servicio de Bloc de notas como servicio de Bloc de notas de HDInsight Jupyter de Azure, puede usar hello **inspirará magia** comandos:

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

Hola **archivos JAR** comando permite tooinclude Hola dos archivos JAR que se necesitan para **cosmosdb de azure de spark** (propio hello y SDK de Java de documentos de Azure) y excluir **scala-reflejar** para que no interfiera con hello llama Livio (Jupyter notebook > Livio > Spark).

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a>Conectar Spark tooAzure DB de Cosmos con Hola conector
Aunque el transporte de comunicación de hello es un poco más complicada, ejecutar una consulta de Spark tooAzure Cosmos DB mediante el conector de hello es significativamente más rápida.

Hola siguiente fragmento de código muestra cómo toouse Hola conector en un contexto de Spark.

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Como se indica en el fragmento de código de hello:

- **Azure-cosmosdb-spark** contiene Hola todos Hola parámetros de conexión necesarios, que incluyen ubicaciones Hola preferido. Por ejemplo, puede elegir Hola lee el orden de prioridad y la réplica.
- Simplemente Hola necesarios bibliotecas de importación y configurar al cliente de base de datos de Azure Cosmos Hola de toocreate masterKey y el host.

### <a name="execute-spark-queries-via-hello-connector"></a>Ejecutar consultas de Spark mediante el conector de Hola

Hola después de la instancia de base de datos de Azure Cosmos de Hola de usos de ejemplo que se creó en el fragmento de código anterior hello mediante Hola especifica claves de solo lectura. Hello fragmento de código siguiente conecta toohello DepartureDelays.flights_pcoll colección (en Hola DoctorWho cuenta como se especificó anteriormente) y ejecuta una consulta tooextract Hola retraso la información de vuelo de vuelos que salen de Seattle.

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a>¿Por qué usar la implementación del conector de BD de Cosmos de hello Spark tooAzure?

Conexión tooAzure Spark Cosmos DB mediante el conector de hello es normalmente en escenarios donde:

* Desea toouse Scala y actualizarlo tooinclude un contenedor de Python, tal y como se indicó en [problema 3: contenedor agregar Python y ejemplos](https://github.com/Azure/azure-cosmosdb-spark/issues/3).
* Tiene una gran cantidad de datos tootransfer entre Apache Spark y base de datos de Azure Cosmos.

toogive una idea de diferencia de rendimiento de la consulta de hello, verá hello [wiki de ejecuciones de pruebas de consulta](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).

## <a name="distributed-aggregation-example"></a>Ejemplo de agregación distribuida
En esta sección se proporcionan algunos ejemplos de cómo se pueden realizar agregaciones distribuidas y análisis de forma conjunta con la utilización de Apache Spark y Azure Cosmos DB. Base de datos de Azure Cosmos ya admite agregaciones, que se describe en hello [agregados de escala de planeta con base de datos de Azure Cosmos blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/). Le mostramos cómo puede llevarlos toohello junto con Apache Spark.

Tenga en cuenta que estas agrupaciones están en referencia toohello [Bloc de notas de Spark tooAzure Cosmos DB Connector](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).

### <a name="connect-tooflights-sample-data"></a>Conexión de datos de ejemplo de tooflights
En estos ejemplos de agregaciones, se accede a algunos datos de rendimiento sobre vuelos almacenados en la base de datos **DoctorWho** de Azure Cosmos DB. tooconnect tooit, necesita hello tooutilize siguiente fragmento de código:

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Con este fragmento de código, estamos también continuo toorun una consulta básica que las transferencias de Hola conjunto filtrado de datos de la base de datos de Azure Cosmos tooSpark donde hello este último puede realizar agregados distribuidos. En este caso, se pregunta por los vuelos que salen de Seattle (SEA).

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

Hola se generaron resultados siguientes mediante la ejecución de consultas de Hola de hello Jupyter servicio de Bloc de notas.  Tenga en cuenta que todos los fragmentos de código de hello tooany genérico y no específicos del servicio.

### <a name="running-limit-and-count-queries"></a>Ejecución de consultas LIMIT y COUNT
Simplemente como le usa tooin SQL/Spark SQL, vamos a empezar con una **límite** consulta:

![Consulta LIMIT de Spark](./media/spark-connector/spark-sql-query.png)

Hello consulta siguiente es una sencilla y rápida **recuento** consulta:

![Consulta COUNT de Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a>Consulta GROUP BY
En el conjunto siguiente, se van a ejecutar consultas **GROUP BY** con facilidad en la base de datos de Azure Cosmos DB:

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Gráfico de consultas GROUP BY de Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a>Consulta DISTINCT, ORDER BY
Esta es una consulta **DISTINCT, ORDER BY**:

![Gráfico de consultas GROUP BY de Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a>Continuar el análisis de datos del vuelo de Hola
Puede usar Hola después de análisis de toocontinue de las consultas de ejemplo de datos de vuelo hello:

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a>Los 5 destinos (ciudades) principales con vuelos retrasados que salen de Seattle
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Gráfico de los principales retrasos de Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a>Cálculo del valor medio de los retrasos según las ciudades de destino cuyos vuelos salen de Seattle
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Gráfico de valores medios de retrasos de Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a>Pasos siguientes

Si no lo ha hecho ya, descargar conector de base de datos de Cosmos de hello Spark tooAzure de hello [cosmosdb de azure de spark](https://github.com/Azure/azure-cosmosdb-spark) repositorio de GitHub y explorar recursos adicionales de hello en el repositorio de hello:

* [Ejemplos de agregaciones distribuidas](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [Cuadernos y script de ejemplo](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

También podría interesarle hello tooreview [Apache Spark SQL, tramas de datos y conjuntos de datos guía](http://spark.apache.org/docs/latest/sql-programming-guide.html) hello y [Apache Spark en HDInsight de Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) artículo.
