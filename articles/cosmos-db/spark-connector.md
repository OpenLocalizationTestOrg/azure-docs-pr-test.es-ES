---
title: "Conexión de Apache Spark a Azure Cosmos DB | Microsoft Docs"
description: "Use este tutorial para aprender sobre el conector de Azure Cosmos DB Spark que le permite conectar Apache Spark a Azure Cosmos DB para realizar agregaciones distribuidas y ciencias de datos en el sistema de base de datos distribuido globalmente multiinquilino de Microsoft diseñado para la nube."
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
ms.openlocfilehash: 8ecbb478c81cde25bbd0d1c9ee07ae02b07f8cc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="d5d86-104">Aceleración de análisis de macrodatos en tiempo real con el conector de Spark a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d5d86-104">Accelerate real-time big-data analytics with the Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="d5d86-105">El conector de Spark a Azure Cosmos DB permite que Azure Cosmos DB actúe como un origen de entrada o un receptor de salida para trabajos de Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-105">The Spark to Azure Cosmos DB connector enables Azure Cosmos DB to act as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="d5d86-106">La conexión de [Spark](http://spark.apache.org/) a [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) acelera la capacidad de resolver problemas de ciencia de datos de avance rápido, donde puede usar Azure Cosmos DB para guardar los datos y consultarlos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="d5d86-106">Connecting [Spark](http://spark.apache.org/) to [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability to solve fast-moving data science problems where you can use Azure Cosmos DB to quickly persist and query data.</span></span> <span data-ttu-id="d5d86-107">El conector de Spark a Azure Cosmos DB usa de manera eficiente los índices administrados de forma nativa por Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-107">The Spark to Azure Cosmos DB connector efficiently utilizes the native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="d5d86-108">Los índices permiten columnas actualizables al realizar análisis y aplicar el filtrado de predicados en los datos distribuidos globalmente en rápida evolución, que abarcan Internet de las cosas (IoT), ciencia de datos y escenarios de análisis.</span><span class="sxs-lookup"><span data-stu-id="d5d86-108">The indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) to data science and analytics scenarios.</span></span>

<span data-ttu-id="d5d86-109">Para trabajar con Spark GraphX y las API Graph de Gremlin de Azure Cosmos DB, consulte [Análisis de gráficos mediante Spark y Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="d5d86-109">For working with Spark GraphX and the Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="d5d86-110">Descargar</span><span class="sxs-lookup"><span data-stu-id="d5d86-110">Download</span></span>

<span data-ttu-id="d5d86-111">Para comenzar, descargue el conector de Spark a Azure Cosmos DB (versión preliminar) del repositorio [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="d5d86-111">To get started, download the Spark to Azure Cosmos DB connector (preview) from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="d5d86-112">Componentes del conector</span><span class="sxs-lookup"><span data-stu-id="d5d86-112">Connector components</span></span>

<span data-ttu-id="d5d86-113">El conector utiliza los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="d5d86-113">The connector utilizes the following components:</span></span>

* <span data-ttu-id="d5d86-114">[Azure Cosmos DB](http://documentdb.com) permite a los clientes aprovisionar y escalar el rendimiento y el almacenamiento de forma elástica a través de cualquier número de regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="d5d86-114">[Azure Cosmos DB](http://documentdb.com) enables customers to provision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="d5d86-115">Las ofertas de servicio:</span><span class="sxs-lookup"><span data-stu-id="d5d86-115">The service offers:</span></span>
   * <span data-ttu-id="d5d86-116">[Distribución global](distribute-data-globally.md) llave en mano y escala horizontal</span><span class="sxs-lookup"><span data-stu-id="d5d86-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="d5d86-117">Garantía de latencias de un solo dígito en el percentil 99</span><span class="sxs-lookup"><span data-stu-id="d5d86-117">Guaranteed single digit latencies at the 99th percentile</span></span>
   * [<span data-ttu-id="d5d86-118">Varios modelos de coherencia bien definida</span><span class="sxs-lookup"><span data-stu-id="d5d86-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="d5d86-119">Garantía de alta disponibilidad con funcionalidades de hospedaje múltiple</span><span class="sxs-lookup"><span data-stu-id="d5d86-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="d5d86-120">Todas las características están respaldadas por [Acuerdos de Nivel de Servicio](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA) completos líderes del sector.</span><span class="sxs-lookup"><span data-stu-id="d5d86-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="d5d86-121">[Apache Spark](http://spark.apache.org/) es un motor de procesamiento de código abierto eficaz diseñado para ofrecer velocidad, facilidad de uso y análisis sofisticados.</span><span class="sxs-lookup"><span data-stu-id="d5d86-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="d5d86-122">Consulte [Apache Spark en Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) para implementar Apache Spark en la nube para implementaciones críticas mediante [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="d5d86-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in the cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="d5d86-123">Versiones oficialmente compatibles:</span><span class="sxs-lookup"><span data-stu-id="d5d86-123">Officially supported versions:</span></span>

| <span data-ttu-id="d5d86-124">Componente</span><span class="sxs-lookup"><span data-stu-id="d5d86-124">Component</span></span> | <span data-ttu-id="d5d86-125">Versión</span><span class="sxs-lookup"><span data-stu-id="d5d86-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="d5d86-126">Spark de Apache</span><span class="sxs-lookup"><span data-stu-id="d5d86-126">Apache Spark</span></span>|<span data-ttu-id="d5d86-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="d5d86-127">2.0+</span></span>|
| <span data-ttu-id="d5d86-128">Scala</span><span class="sxs-lookup"><span data-stu-id="d5d86-128">Scala</span></span>| <span data-ttu-id="d5d86-129">2.11</span><span class="sxs-lookup"><span data-stu-id="d5d86-129">2.11</span></span>|
| <span data-ttu-id="d5d86-130">SDK de Java de Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d5d86-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="d5d86-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="d5d86-131">1.10.0</span></span> |

<span data-ttu-id="d5d86-132">Este artículo le ayuda a ejecutar algunos ejemplos sencillos con Python (a través de pyDocumentDB) y las interfaces de Scala.</span><span class="sxs-lookup"><span data-stu-id="d5d86-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and the Scala interfaces.</span></span>

<span data-ttu-id="d5d86-133">Existen dos enfoques para conectar Apache Spark y Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="d5d86-133">There are two approaches to connect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="d5d86-134">Usar pyDocumentDB a través del [SDK de Python para Azure DocumentDB](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="d5d86-134">Use pyDocumentDB via the [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="d5d86-135">Crear un conector de Spark a Cosmos DB basado en Java mediante el [SDK para Java de Azure DocumentDB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="d5d86-135">Create a Java-based Spark to Azure Cosmos DB connector by utilizing the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="d5d86-136">Implementación de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d5d86-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="d5d86-137">El [SDK pyDocumentDB](https://github.com/Azure/azure-documentdb-python) actual le permite conectar Spark a Azure Cosmos DB como se muestra en el siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="d5d86-137">The current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you to connect Spark to Azure Cosmos DB as shown in the following diagram:</span></span>

![Flujo de datos de Spark a Azure Cosmos DB a través de pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-the-pydocumentdb-implementation"></a><span data-ttu-id="d5d86-139">Flujo de datos de la implementación de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d5d86-139">Data flow of the pyDocumentDB implementation</span></span>

<span data-ttu-id="d5d86-140">El flujo de datos es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5d86-140">The data flow is as follows:</span></span>

1. <span data-ttu-id="d5d86-141">El nodo maestro de Spark se conecta al nodo de puerta de enlace de Azure Cosmos DB a través de pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-141">The Spark master node connects to the Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="d5d86-142">Un usuario especifica solo las conexiones de Spark y Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-142">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="d5d86-143">Las conexiones a los respectivos nodos maestro y de puerta de enlace son transparentes para el usuario.</span><span class="sxs-lookup"><span data-stu-id="d5d86-143">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="d5d86-144">El nodo de puerta de enlace realiza la consulta en Azure Cosmos DB donde posteriormente se ejecuta la consulta en las particiones de la colección de los nodos de datos.</span><span class="sxs-lookup"><span data-stu-id="d5d86-144">The gateway node makes the query against Azure Cosmos DB where the query subsequently runs against the collection's partitions in the data nodes.</span></span> <span data-ttu-id="d5d86-145">La respuesta a esas consultas se reenvía al nodo de puerta de enlace y ese conjunto de resultados se devuelve al nodo maestro de Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-145">The response for those queries is sent back to the gateway node, and that result set is returned to the Spark master node.</span></span>
3. <span data-ttu-id="d5d86-146">Las consultas posteriores (por ejemplo, en un DataFrame de Spark) se envían a los nodos de trabajo de Spark para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="d5d86-146">Subsequent queries (for example, against a Spark DataFrame) are sent to the Spark worker nodes for processing.</span></span>

<span data-ttu-id="d5d86-147">La comunicación entre Spark y Azure Cosmos DB se limita al nodo maestro de Spark y a los nodos de puerta de enlace de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-147">Communication between Spark and Azure Cosmos DB is limited to the Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="d5d86-148">Las consultas van tan rápido como permite la capa de transporte entre estos dos nodos.</span><span class="sxs-lookup"><span data-stu-id="d5d86-148">The queries go as fast as the transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="d5d86-149">Instalación de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d5d86-149">Install pyDocumentDB</span></span>
<span data-ttu-id="d5d86-150">Puede instalar pyDocumentDB en el nodo de controlador mediante **pip**, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d5d86-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-to-azure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="d5d86-151">Conexión de Spark a Azure Cosmos DB mediante pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d5d86-151">Connect Spark to Azure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="d5d86-152">La simplicidad del transporte de comunicación permite que la ejecución de una consulta de Spark a Azure Cosmos DB mediante pyDocumentDB sea relativamente sencilla.</span><span class="sxs-lookup"><span data-stu-id="d5d86-152">The simplicity of the communication transport makes execution of a query from Spark to Azure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="d5d86-153">El fragmento de código siguiente muestra cómo usar pyDocumentDB en un contexto de Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-153">The following code snippet shows how to use pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring the connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys to connect to Azure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="d5d86-154">Como se indica en el fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="d5d86-154">As noted in the code snippet:</span></span>

* <span data-ttu-id="d5d86-155">El SDK de Python para Azure Cosmos DB (`pyDocumentDB`) contiene todos los parámetros de conexión necesarios.</span><span class="sxs-lookup"><span data-stu-id="d5d86-155">The Azure Cosmos DB Python SDK (`pyDocumentDB`) contains the all the necessary connection parameters.</span></span> <span data-ttu-id="d5d86-156">Por ejemplo, el parámetro de ubicaciones preferidas elige la réplica de lectura y el orden de prioridad.</span><span class="sxs-lookup"><span data-stu-id="d5d86-156">For example, the preferred locations parameter chooses the read replica and priority order.</span></span>
*  <span data-ttu-id="d5d86-157">Importe las bibliotecas necesarias y configure su **masterKey** y **host** para crear el *cliente* de Azure Cosmos DB (**pydocumentdb.document_client**).</span><span class="sxs-lookup"><span data-stu-id="d5d86-157">Import the necessary libraries and configure your **masterKey** and **host** to create the Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="d5d86-158">Ejecución de consultas de Spark mediante pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d5d86-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="d5d86-159">En los ejemplos siguientes se usa la instancia de Azure Cosmos DB creada en el fragmento de código anterior con las claves de solo lectura especificadas.</span><span class="sxs-lookup"><span data-stu-id="d5d86-159">The following examples use the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="d5d86-160">El siguiente fragmento de código se conecta a la colección **airports.codes** (en la cuenta de DoctorWho, como se ha especificado anteriormente), y ejecuta una consulta para extraer las ciudades con aeropuerto del Estado de Washington.</span><span class="sxs-lookup"><span data-stu-id="d5d86-160">The following code snippet connects to the **airports.codes** collection in the DoctorWho account as specified earlier and runs a query to extract the airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations the Azure Cosmos DB client will use to connect to the database and collection
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

<span data-ttu-id="d5d86-161">Después de haber ejecutado la consulta mediante **query**, el resultado es **query_iterable.QueryIterable**, que se convierte en una lista Python.</span><span class="sxs-lookup"><span data-stu-id="d5d86-161">After the query has been executed via **query**, the result is a **query_iterable.QueryIterable** that is converted to a Python list.</span></span> <span data-ttu-id="d5d86-162">Una lista Python puede convertirse con facilidad en un dataframe de Spark con el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="d5d86-162">A Python list can be easily converted to a Spark DataFrame by using the following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-the-pydocumentdb-to-connect-spark-to-azure-cosmos-db"></a><span data-ttu-id="d5d86-163">¿Por qué usar pyDocumentDB para conectar Spark a Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="d5d86-163">Why use the pyDocumentDB to connect Spark to Azure Cosmos DB?</span></span>
<span data-ttu-id="d5d86-164">La conexión de Spark a Azure Cosmos DB con pyDocumentDB suele utilizarse en escenarios donde:</span><span class="sxs-lookup"><span data-stu-id="d5d86-164">Connecting Spark to Azure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="d5d86-165">Quiera usar Python.</span><span class="sxs-lookup"><span data-stu-id="d5d86-165">You want to use Python.</span></span>
* <span data-ttu-id="d5d86-166">Desea devolver un conjunto de resultados relativamente pequeño desde Azure Cosmos DB a Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-166">You are returning a relatively small result set from Azure Cosmos DB to Spark.</span></span> <span data-ttu-id="d5d86-167">Tenga en cuenta que el conjunto de datos subyacente en Azure Cosmos DB puede ser bastante grande.</span><span class="sxs-lookup"><span data-stu-id="d5d86-167">Note that the underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="d5d86-168">Vaya a aplicar filtros, es decir, ejecutar filtros de predicado, en el origen de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="d5d86-169">Conector de Spark a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d5d86-169">Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="d5d86-170">El conector de Spark a Azure Cosmos DB usa el [SDK de Java para Azure DocumentDB](https://github.com/Azure/azure-documentdb-java) y transfiere los datos entre los nodos de trabajo de Spark y Azure Cosmos DB, tal y como se muestra en el diagrama siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5d86-170">The Spark to Azure Cosmos DB connector utilizes the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between the Spark worker nodes and Azure Cosmos DB as shown in the following diagram:</span></span>

![Flujo de datos del conector de Spark a Azure Cosmos DB](./media/spark-connector/spark-connector.png)

<span data-ttu-id="d5d86-172">El flujo de datos es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5d86-172">The data flow is as follows:</span></span>

1. <span data-ttu-id="d5d86-173">El nodo maestro de Spark se conecta al nodo de puerta de enlace de Azure Cosmos DB para obtener el mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="d5d86-173">The Spark master node connects to the Azure Cosmos DB gateway node to obtain the partition map.</span></span> <span data-ttu-id="d5d86-174">Un usuario especifica solo las conexiones de Spark y Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-174">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="d5d86-175">Las conexiones a los respectivos nodos maestro y de puerta de enlace son transparentes para el usuario.</span><span class="sxs-lookup"><span data-stu-id="d5d86-175">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="d5d86-176">Esta información se proporciona en el nodo principal de Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-176">This information is provided back to the Spark master node.</span></span>  <span data-ttu-id="d5d86-177">En este momento, debe poder analizar la consulta para determinar las particiones (y sus ubicaciones) dentro de Azure Cosmos DB a las que debe acceder.</span><span class="sxs-lookup"><span data-stu-id="d5d86-177">At this point, you should be able to parse the query to determine the partitions and their locations in Azure Cosmos DB that you need to access.</span></span>
3. <span data-ttu-id="d5d86-178">Esta información se transmite a los nodos de trabajo de Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-178">This information is transmitted to the Spark worker nodes.</span></span>
4. <span data-ttu-id="d5d86-179">Los nodos de trabajo de Spark se conectan directamente a las particiones de Azure Cosmos DB para extraer los datos y devolverlos a las particiones de Spark de los nodos de trabajo de Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-179">The Spark worker nodes connect to the Azure Cosmos DB partitions directly to extract the data and return the data to the Spark partitions in the Spark worker nodes.</span></span>

<span data-ttu-id="d5d86-180">La comunicación entre Spark y Azure Cosmos DB es mucho más rápida porque la transferencia de datos se realiza entre los nodos de trabajo de Spark y los nodos de datos de Azure Cosmos DB (particiones).</span><span class="sxs-lookup"><span data-stu-id="d5d86-180">Communication between Spark and Azure Cosmos DB is significantly faster because the data movement is between the Spark worker nodes and the Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="d5d86-181">Creación del conector de Spark a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d5d86-181">Build the Spark to Azure Cosmos DB connector</span></span>
<span data-ttu-id="d5d86-182">Actualmente, el proyecto del conector usa Maven.</span><span class="sxs-lookup"><span data-stu-id="d5d86-182">Currently, the connector project uses maven.</span></span> <span data-ttu-id="d5d86-183">Para crear el conector sin dependencias, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="d5d86-183">To build the connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="d5d86-184">También puede descargar las últimas versiones del archivo JAR de la carpeta de *versiones*.</span><span class="sxs-lookup"><span data-stu-id="d5d86-184">You can also download the latest versions of the JAR from the *releases* folder.</span></span>

### <a name="include-the-azure-cosmos-db-spark-jar"></a><span data-ttu-id="d5d86-185">Inclusión del archivo JAR de Azure Cosmos DB Spark</span><span class="sxs-lookup"><span data-stu-id="d5d86-185">Include the Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="d5d86-186">Antes de ejecutar ningún código, deberá incluir el archivo JAR de Azure Cosmos DB Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-186">Before you execute any code, you need to include the Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="d5d86-187">Si va a usar **spark-shell**, puede incluirlo mediante la opción **--jars**.</span><span class="sxs-lookup"><span data-stu-id="d5d86-187">If you are using the **spark-shell**, then you can include the JAR by using the **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="d5d86-188">Si desea ejecutar el archivo JAR sin dependencias, use el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="d5d86-188">If you want to execute the JAR without dependencies, use the following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="d5d86-189">Si usa un servicio de cuaderno como Azure HDInsight Jupyter Notebook en Azure HDInsight, puede usar los comandos **spark magic**:</span><span class="sxs-lookup"><span data-stu-id="d5d86-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use the **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="d5d86-190">El comando **jars** permite incluir los dos archivos JAR necesarios para **azure-cosmosdb-spark** (el propio y el SDK de Java para Azure DocumentDB) y excluir **scala-reflect**, a fin de que no interfiera con las llamadas Livy realizadas (Jupyter Notebook > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="d5d86-190">The **jars** command enables you to include the two JARs that are needed for **azure-cosmosdb-spark** (itself and the Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with the Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-to-azure-cosmos-db-using-the-connector"></a><span data-ttu-id="d5d86-191">Conexión de Spark a Azure Cosmos DB mediante el conector</span><span class="sxs-lookup"><span data-stu-id="d5d86-191">Connect Spark to Azure Cosmos DB using the connector</span></span>
<span data-ttu-id="d5d86-192">Aunque el transporte de comunicación es un poco más complicado, ejecutar una consulta de Spark en Azure Cosmos DB mediante el conector es mucho más rápido.</span><span class="sxs-lookup"><span data-stu-id="d5d86-192">Although the communication transport is a little more complicated, executing a query from Spark to Azure Cosmos DB by using the connector is significantly faster.</span></span>

<span data-ttu-id="d5d86-193">El fragmento de código siguiente muestra cómo usar el conector dentro de un contexto de Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-193">The following code snippet shows how to use the connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection to your collection
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

<span data-ttu-id="d5d86-194">Como se indica en el fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="d5d86-194">As noted in the code snippet:</span></span>

- <span data-ttu-id="d5d86-195">**azure-cosmosdb-spark** contiene todos los parámetros de conexión necesarios, que incluyen las ubicaciones preferidas.</span><span class="sxs-lookup"><span data-stu-id="d5d86-195">**azure-cosmosdb-spark** contains the all the necessary connection parameters, which include the preferred locations.</span></span> <span data-ttu-id="d5d86-196">Por ejemplo, puede elegir el orden de prioridad y la réplica de lectura.</span><span class="sxs-lookup"><span data-stu-id="d5d86-196">For example, you can choose the read replica and priority order.</span></span>
- <span data-ttu-id="d5d86-197">Solo tiene que importar las bibliotecas necesarias y configurar la clave principal y el host para crear el cliente de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-197">Just import the necessary libraries and configure your masterKey and host to create the Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-the-connector"></a><span data-ttu-id="d5d86-198">Ejecución de consultas de Spark mediante el conector</span><span class="sxs-lookup"><span data-stu-id="d5d86-198">Execute Spark queries via the connector</span></span>

<span data-ttu-id="d5d86-199">En el ejemplo siguiente se usa la instancia de Azure Cosmos DB creada en el fragmento de código anterior con las claves de solo lectura especificadas.</span><span class="sxs-lookup"><span data-stu-id="d5d86-199">The following example uses the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="d5d86-200">El siguiente fragmento de código se conecta a la colección DepartureDelays.flights_pcoll (en la cuenta de DoctorWho, como se especificó anteriormente) mediante la ejecución de una consulta para extraer la información sobre los retrasos de los vuelos que salen de Seattle.</span><span class="sxs-lookup"><span data-stu-id="d5d86-200">The following code snippet connects to the DepartureDelays.flights_pcoll collection (in the DoctorWho account as specified earlier) and runs a query to extract the flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-the-spark-to-azure-cosmos-db-connector-implementation"></a><span data-ttu-id="d5d86-201">¿Por qué usar la implementación del conector de Spark a Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="d5d86-201">Why use the Spark to Azure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="d5d86-202">La conexión de Spark a Azure Cosmos DB con el conector suele usarse en escenarios en que:</span><span class="sxs-lookup"><span data-stu-id="d5d86-202">Connecting Spark to Azure Cosmos DB by using the connector is typically for scenarios where:</span></span>

* <span data-ttu-id="d5d86-203">Quiere usar Scala y actualizarlo para incluir un contenedor de Python, tal y como se indicó en [Problema 3: Agregar contenedor de Python y ejemplos](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="d5d86-203">You want to use Scala and update it to include a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="d5d86-204">Tiene una gran cantidad de datos que se van a transferir entre Apache Spark y Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-204">You have a large amount of data to transfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="d5d86-205">Para darle una idea de la diferencia de rendimiento de consultas, vea la [wiki de ejecuciones de pruebas de consulta](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="d5d86-205">To give you an idea of the query performance difference, see the [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="d5d86-206">Ejemplo de agregación distribuida</span><span class="sxs-lookup"><span data-stu-id="d5d86-206">Distributed aggregation example</span></span>
<span data-ttu-id="d5d86-207">En esta sección se proporcionan algunos ejemplos de cómo se pueden realizar agregaciones distribuidas y análisis de forma conjunta con la utilización de Apache Spark y Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="d5d86-208">Azure Cosmos DB ya admite agregaciones, que se describen en el [blog Planet scale aggregates with Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="d5d86-208">Azure Cosmos DB already supports aggregations, which is discussed in the [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="d5d86-209">A continuación se indica cómo puede llevarlo al siguiente nivel con Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="d5d86-209">Here is how you can take it to the next level with Apache Spark.</span></span>

<span data-ttu-id="d5d86-210">Tenga en cuenta que estas agregaciones guardan relación con el [cuaderno del conector de Spark a Cosmos DB](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="d5d86-210">Note that these aggregations are in reference to the [Spark to Azure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-to-flights-sample-data"></a><span data-ttu-id="d5d86-211">Conexión a los datos de ejemplo sobre vuelos</span><span class="sxs-lookup"><span data-stu-id="d5d86-211">Connect to flights sample data</span></span>
<span data-ttu-id="d5d86-212">En estos ejemplos de agregaciones, se accede a algunos datos de rendimiento sobre vuelos almacenados en la base de datos **DoctorWho** de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5d86-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="d5d86-213">Para conectarse a ella, debe utilizar el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="d5d86-213">To connect to it, you need to utilize the following code snippet:</span></span>

```
// Import Spark to Azure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect to Azure Cosmos DB Database
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

<span data-ttu-id="d5d86-214">Con este fragmento de código, también se va a ejecutar una consulta base que transfiere el conjunto filtrado de datos deseado de Azure Cosmos DB a Spark (donde el último puede realizar agregaciones distribuidas).</span><span class="sxs-lookup"><span data-stu-id="d5d86-214">With this snippet, we are also going to run a base query that transfers the filtered set of data from Azure Cosmos DB to Spark where the latter can perform distributed aggregates.</span></span> <span data-ttu-id="d5d86-215">En este caso, se pregunta por los vuelos que salen de Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="d5d86-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="d5d86-216">Los resultados siguientes se generaron mediante la ejecución de las consultas del servicio de Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="d5d86-216">The following results were generated by running the queries from the Jupyter notebook service.</span></span>  <span data-ttu-id="d5d86-217">Tenga en cuenta que todos los fragmentos de código son genéricos y no específicos a cualquier servicio.</span><span class="sxs-lookup"><span data-stu-id="d5d86-217">Note that all the code snippets are generic and not specific to any service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="d5d86-218">Ejecución de consultas LIMIT y COUNT</span><span class="sxs-lookup"><span data-stu-id="d5d86-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="d5d86-219">Del mismo modo que está familiarizado con SQL y Spark SQL, se va a comenzar con una consulta **LIMIT**:</span><span class="sxs-lookup"><span data-stu-id="d5d86-219">Just like you're used to in SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Consulta LIMIT de Spark](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="d5d86-221">La siguiente consulta es una consulta **COUNT** sencilla y rápida:</span><span class="sxs-lookup"><span data-stu-id="d5d86-221">The next query is a simple and fast **COUNT** query:</span></span>

![Consulta COUNT de Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="d5d86-223">Consulta GROUP BY</span><span class="sxs-lookup"><span data-stu-id="d5d86-223">GROUP BY query</span></span>
<span data-ttu-id="d5d86-224">En el conjunto siguiente, se van a ejecutar consultas **GROUP BY** con facilidad en la base de datos de Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="d5d86-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Gráfico de consultas GROUP BY de Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="d5d86-226">Consulta DISTINCT, ORDER BY</span><span class="sxs-lookup"><span data-stu-id="d5d86-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="d5d86-227">Esta es una consulta **DISTINCT, ORDER BY**:</span><span class="sxs-lookup"><span data-stu-id="d5d86-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Gráfico de consultas GROUP BY de Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-the-flight-data-analysis"></a><span data-ttu-id="d5d86-229">Continuación del análisis de datos sobre vuelos</span><span class="sxs-lookup"><span data-stu-id="d5d86-229">Continue the flight data analysis</span></span>
<span data-ttu-id="d5d86-230">Puede usar las consultas de ejemplo siguientes para continuar el análisis de datos sobre vuelos:</span><span class="sxs-lookup"><span data-stu-id="d5d86-230">You can use the following example queries to continue analysis of the flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="d5d86-231">Los 5 destinos (ciudades) principales con vuelos retrasados que salen de Seattle</span><span class="sxs-lookup"><span data-stu-id="d5d86-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Gráfico de los principales retrasos de Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="d5d86-233">Cálculo del valor medio de los retrasos según las ciudades de destino cuyos vuelos salen de Seattle</span><span class="sxs-lookup"><span data-stu-id="d5d86-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Gráfico de valores medios de retrasos de Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="d5d86-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5d86-235">Next steps</span></span>

<span data-ttu-id="d5d86-236">Si aún no lo ha hecho, descargue el conector de Spark a Azure Cosmos DB del repositorio de GitHub [azure-documentdb-spark](https://github.com/Azure/azure-cosmosdb-spark) y explore los recursos adicionales del repositorio:</span><span class="sxs-lookup"><span data-stu-id="d5d86-236">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore the additional resources in the repo:</span></span>

* [<span data-ttu-id="d5d86-237">Ejemplos de agregaciones distribuidas</span><span class="sxs-lookup"><span data-stu-id="d5d86-237">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="d5d86-238">Cuadernos y script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d5d86-238">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="d5d86-239">Es posible que también quiera consultar la [guía de Apache Spark SQL, DataFrames y conjuntos de datos](http://spark.apache.org/docs/latest/sql-programming-guide.html) y el artículo [Apache Spark en Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d5d86-239">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
