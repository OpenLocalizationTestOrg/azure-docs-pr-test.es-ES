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
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="97442-104">Acelerar el análisis de grandes cantidades de datos en tiempo real con el conector de base de datos de Cosmos de hello Spark tooAzure</span><span class="sxs-lookup"><span data-stu-id="97442-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="97442-105">Conector de base de datos de Cosmos de Hello Spark tooAzure permite tooact de base de datos de Azure Cosmos como un origen de entrada o el receptor de salida para los trabajos de Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="97442-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="97442-106">Conexión [Spark](http://spark.apache.org/) demasiado[base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) acelera la capacidad toosolve mover fast ciencia de datos problemas que puede usar base de datos de Azure Cosmos tooquickly persisten y consultar datos.</span><span class="sxs-lookup"><span data-stu-id="97442-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="97442-107">Conector de base de datos de Cosmos de Hello Spark tooAzure eficazmente utiliza índices de base de datos de Azure Cosmos administrado nativo Hola.</span><span class="sxs-lookup"><span data-stu-id="97442-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="97442-108">índices de Hello habilitar columnas actualizables cuando realice análisis y filtrado cambiante global de predicado de inserción distribuidas, datos, que abarcan desde toodata ciencia y análisis de escenarios de Internet de las cosas (IoT).</span><span class="sxs-lookup"><span data-stu-id="97442-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="97442-109">Para trabajar con Spark GraphX y gráfico de Gremlin Hola DB Cosmos API de Azure, consulte [realizar análisis de gráfico usando Spark y Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="97442-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="97442-110">Descargar</span><span class="sxs-lookup"><span data-stu-id="97442-110">Download</span></span>

<span data-ttu-id="97442-111">tooget iniciado, descargue tooAzure Cosmos DB connector (vista previa) de hello Spark de hello [cosmosdb de azure de spark](https://github.com/Azure/azure-cosmosdb-spark/) repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="97442-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="97442-112">Componentes del conector</span><span class="sxs-lookup"><span data-stu-id="97442-112">Connector components</span></span>

<span data-ttu-id="97442-113">Conector de Hello utiliza Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="97442-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="97442-114">[Base de datos de Azure Cosmos](http://documentdb.com) permite que los clientes tooprovision y escalar de forma elástica rendimiento y almacenamiento a través de cualquier número de regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="97442-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="97442-115">Hola ofertas de servicio:</span><span class="sxs-lookup"><span data-stu-id="97442-115">hello service offers:</span></span>
   * <span data-ttu-id="97442-116">[Distribución global](distribute-data-globally.md) llave en mano y escala horizontal</span><span class="sxs-lookup"><span data-stu-id="97442-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="97442-117">Garantiza que las latencias de un dígito en percentil 99 Hola</span><span class="sxs-lookup"><span data-stu-id="97442-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * [<span data-ttu-id="97442-118">Varios modelos de coherencia bien definida</span><span class="sxs-lookup"><span data-stu-id="97442-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="97442-119">Garantía de alta disponibilidad con funcionalidades de hospedaje múltiple</span><span class="sxs-lookup"><span data-stu-id="97442-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="97442-120">Todas las características están respaldadas por [Acuerdos de Nivel de Servicio](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA) completos líderes del sector.</span><span class="sxs-lookup"><span data-stu-id="97442-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="97442-121">[Apache Spark](http://spark.apache.org/) es un motor de procesamiento de código abierto eficaz diseñado para ofrecer velocidad, facilidad de uso y análisis sofisticados.</span><span class="sxs-lookup"><span data-stu-id="97442-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="97442-122">[Apache Spark en HDInsight de Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) para que pueda implementar Apache Spark en nube de Hola para implementaciones críticas mediante el uso de [HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="97442-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="97442-123">Versiones oficialmente compatibles:</span><span class="sxs-lookup"><span data-stu-id="97442-123">Officially supported versions:</span></span>

| <span data-ttu-id="97442-124">Componente</span><span class="sxs-lookup"><span data-stu-id="97442-124">Component</span></span> | <span data-ttu-id="97442-125">Versión</span><span class="sxs-lookup"><span data-stu-id="97442-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="97442-126">Spark de Apache</span><span class="sxs-lookup"><span data-stu-id="97442-126">Apache Spark</span></span>|<span data-ttu-id="97442-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="97442-127">2.0+</span></span>|
| <span data-ttu-id="97442-128">Scala</span><span class="sxs-lookup"><span data-stu-id="97442-128">Scala</span></span>| <span data-ttu-id="97442-129">2.11</span><span class="sxs-lookup"><span data-stu-id="97442-129">2.11</span></span>|
| <span data-ttu-id="97442-130">SDK de Java de Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="97442-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="97442-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="97442-131">1.10.0</span></span> |

<span data-ttu-id="97442-132">En este artículo le ayuda a ejecutar algunos ejemplos simples mediante Python (a través de pyDocumentDB) y Hola Scala interfaces.</span><span class="sxs-lookup"><span data-stu-id="97442-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="97442-133">Hay dos enfoques tooconnect Apache Spark y base de datos de Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="97442-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="97442-134">Usar pyDocumentDB a través de hello [SDK de Azure DocumentDB Python](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="97442-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="97442-135">Crear un conector de base de datos de Cosmos tooAzure Spark basados en Java mediante el uso de hello [SDK de Java de Azure DocumentDB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="97442-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="97442-136">Implementación de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="97442-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="97442-137">Hola actual [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) permite tooconnect Spark tooAzure DB Cosmos como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="97442-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Spark tooAzure Cosmos DB el flujo de datos a través de pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="97442-139">Flujo de datos de implementación de hello pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="97442-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="97442-140">flujo de datos de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="97442-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="97442-141">nodo maestro de Hello Spark conecta el nodo de puerta de enlace de base de datos de Azure Cosmos toohello mediante pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="97442-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="97442-142">Un usuario especifica solo Hola Spark y base de datos de Azure Cosmos conexiones.</span><span class="sxs-lookup"><span data-stu-id="97442-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="97442-143">Las conexiones toohello respectivos maestra y puerta de enlace de nodos son usuario toohello transparente.</span><span class="sxs-lookup"><span data-stu-id="97442-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="97442-144">nodo de puerta de enlace de Hello hace consulta de hello en la base de datos de Azure Cosmos donde consulta Hola ejecuta posteriormente en particiones de la colección de hello en nodos de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="97442-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="97442-145">respuesta de Hola para esas consultas se le envía toohello nodo de puerta de enlace y ese conjunto de resultados se devuelve el nodo principal de toohello Spark.</span><span class="sxs-lookup"><span data-stu-id="97442-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="97442-146">Las consultas posteriores (por ejemplo, en una trama de datos de Spark) se envían los nodos de trabajador de Spark toohello para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="97442-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="97442-147">Comunicación entre Spark y base de datos de Azure Cosmos es limitado toohello nodo maestro Spark y nodos de puerta de enlace de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="97442-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="97442-148">las consultas de Hello van tan rápido como el nivel de transporte de hello entre estos dos nodos permite.</span><span class="sxs-lookup"><span data-stu-id="97442-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="97442-149">Instalación de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="97442-149">Install pyDocumentDB</span></span>
<span data-ttu-id="97442-150">Puede instalar pyDocumentDB en el nodo de controlador mediante **pip**, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="97442-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="97442-151">Conectar Spark tooAzure Cosmos DB a través de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="97442-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="97442-152">simplicidad de Hola de transporte de comunicación de hello hace la ejecución de una consulta de Spark tooAzure DB Cosmos mediante pyDocumentDB relativamente sencilla.</span><span class="sxs-lookup"><span data-stu-id="97442-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="97442-153">Hola código fragmento siguiente muestra cómo toouse pyDocumentDB en un contexto de Spark.</span><span class="sxs-lookup"><span data-stu-id="97442-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

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

<span data-ttu-id="97442-154">Como se indica en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="97442-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="97442-155">Hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contiene Hola Hola a todos los parámetros de conexión necesaria.</span><span class="sxs-lookup"><span data-stu-id="97442-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="97442-156">Por ejemplo, hello preferido parámetro ubicaciones elige Hola lee el orden de prioridad y la réplica.</span><span class="sxs-lookup"><span data-stu-id="97442-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="97442-157">Hola necesarios bibliotecas de importación y configurar su **masterKey** y **host** toocreate Hola base de datos de Azure Cosmos *cliente* (**pydocumentdb.document_ cliente**).</span><span class="sxs-lookup"><span data-stu-id="97442-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="97442-158">Ejecución de consultas de Spark mediante pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="97442-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="97442-159">Hola siguientes ejemplos use Hola base de datos de Azure Cosmos la instancia que se creó en el fragmento de código anterior hello mediante Hola especifica claves de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="97442-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="97442-160">Hello fragmento de código siguiente conecta toohello **airports.codes** colección hello DoctorWho como en cuenta especificada anteriormente y se ejecuta un aeropuerto de consulta tooextract Hola ciudades en el estado de Washington.</span><span class="sxs-lookup"><span data-stu-id="97442-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

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

<span data-ttu-id="97442-161">Una vez ejecutada la consulta de Hola a través de **consulta**, resultado de hello es un **query_iterable. QueryIterable** que es la lista de Python tooa convertido.</span><span class="sxs-lookup"><span data-stu-id="97442-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="97442-162">Una lista de Python puede convertir fácilmente tooa trama de datos de Spark mediante Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="97442-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="97442-163">¿Por qué usar hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="97442-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="97442-164">Conexión tooAzure Spark Cosmos DB mediante el uso de pyDocumentDB es normalmente en escenarios donde:</span><span class="sxs-lookup"><span data-stu-id="97442-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="97442-165">Desea toouse Python.</span><span class="sxs-lookup"><span data-stu-id="97442-165">You want toouse Python.</span></span>
* <span data-ttu-id="97442-166">Devuelve un conjunto de base de datos de Azure Cosmos tooSpark de resultados relativamente pequeño.</span><span class="sxs-lookup"><span data-stu-id="97442-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="97442-167">Tenga en cuenta que Hola conjunto de datos subyacente en la base de datos de Azure Cosmos puede ser bastante grande.</span><span class="sxs-lookup"><span data-stu-id="97442-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="97442-168">Vaya a aplicar filtros, es decir, ejecutar filtros de predicado, en el origen de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="97442-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="97442-169">Spark tooAzure conector de base de datos de Cosmos</span><span class="sxs-lookup"><span data-stu-id="97442-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="97442-170">Conector de Hello Spark tooAzure Cosmos DB utiliza hello [SDK de Java de Azure DocumentDB](https://github.com/Azure/azure-documentdb-java) y mueve datos entre nodos de trabajador de Spark hello y base de datos de Azure Cosmos como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="97442-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Flujo de datos en el conector de base de datos de Cosmos de hello Spark tooAzure](./media/spark-connector/spark-connector.png)

<span data-ttu-id="97442-172">flujo de datos de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="97442-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="97442-173">nodo maestro de Hello Spark conecta mapa de partición del nodo tooobtain Hola de toohello base de datos de Azure Cosmos puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="97442-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="97442-174">Un usuario especifica solo Hola Spark y base de datos de Azure Cosmos conexiones.</span><span class="sxs-lookup"><span data-stu-id="97442-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="97442-175">Las conexiones toohello respectivos maestra y puerta de enlace de nodos son usuario toohello transparente.</span><span class="sxs-lookup"><span data-stu-id="97442-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="97442-176">Esta información se proporciona el nodo principal de toohello atrás Spark.</span><span class="sxs-lookup"><span data-stu-id="97442-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="97442-177">En este punto, debe ser particiones de tooparse capaz de hello consulta toodetermine hello y sus ubicaciones en la base de datos de Azure Cosmos que necesita tooaccess.</span><span class="sxs-lookup"><span data-stu-id="97442-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="97442-178">Esta información es nodos de trabajador de la información transmitida toohello Spark.</span><span class="sxs-lookup"><span data-stu-id="97442-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="97442-179">nodos de trabajador de Hello Spark conectan particiones de base de datos de Azure Cosmos toohello directamente tooextract Hola datos y devolver Hola datos toohello particiones Spark en nodos de trabajador de hello Spark.</span><span class="sxs-lookup"><span data-stu-id="97442-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="97442-180">Comunicación entre Spark y base de datos de Azure Cosmos es mucho más rápido porque el movimiento de datos de hello es entre nodos de trabajador de Spark hello y nodos de datos de base de datos de Azure Cosmos hello (particiones).</span><span class="sxs-lookup"><span data-stu-id="97442-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="97442-181">Compilar el conector de base de datos de Cosmos de hello Spark tooAzure</span><span class="sxs-lookup"><span data-stu-id="97442-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="97442-182">Actualmente, el proyecto de conector de hello utiliza a maven.</span><span class="sxs-lookup"><span data-stu-id="97442-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="97442-183">Conector de hello toobuild sin dependencias, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="97442-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="97442-184">También puede descargar versiones más recientes de Hola de hello JAR de hello *libera* carpeta.</span><span class="sxs-lookup"><span data-stu-id="97442-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="97442-185">Incluir hello Azure Cosmos DB Spark JAR</span><span class="sxs-lookup"><span data-stu-id="97442-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="97442-186">Antes de ejecutar cualquier código, debe hello tooinclude Azure Cosmos DB Spark JAR.</span><span class="sxs-lookup"><span data-stu-id="97442-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="97442-187">Si usas hello **spark shell**, a continuación, puede incluir Hola JAR mediante hello **--archivos JAR** opción.</span><span class="sxs-lookup"><span data-stu-id="97442-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="97442-188">Si desea tooexecute Hola JAR sin dependencias, utilice Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="97442-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="97442-189">Si usas un servicio de Bloc de notas como servicio de Bloc de notas de HDInsight Jupyter de Azure, puede usar hello **inspirará magia** comandos:</span><span class="sxs-lookup"><span data-stu-id="97442-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="97442-190">Hola **archivos JAR** comando permite tooinclude Hola dos archivos JAR que se necesitan para **cosmosdb de azure de spark** (propio hello y SDK de Java de documentos de Azure) y excluir **scala-reflejar** para que no interfiera con hello llama Livio (Jupyter notebook > Livio > Spark).</span><span class="sxs-lookup"><span data-stu-id="97442-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="97442-191">Conectar Spark tooAzure DB de Cosmos con Hola conector</span><span class="sxs-lookup"><span data-stu-id="97442-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="97442-192">Aunque el transporte de comunicación de hello es un poco más complicada, ejecutar una consulta de Spark tooAzure Cosmos DB mediante el conector de hello es significativamente más rápida.</span><span class="sxs-lookup"><span data-stu-id="97442-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="97442-193">Hola siguiente fragmento de código muestra cómo toouse Hola conector en un contexto de Spark.</span><span class="sxs-lookup"><span data-stu-id="97442-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

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

<span data-ttu-id="97442-194">Como se indica en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="97442-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="97442-195">**Azure-cosmosdb-spark** contiene Hola todos Hola parámetros de conexión necesarios, que incluyen ubicaciones Hola preferido.</span><span class="sxs-lookup"><span data-stu-id="97442-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="97442-196">Por ejemplo, puede elegir Hola lee el orden de prioridad y la réplica.</span><span class="sxs-lookup"><span data-stu-id="97442-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="97442-197">Simplemente Hola necesarios bibliotecas de importación y configurar al cliente de base de datos de Azure Cosmos Hola de toocreate masterKey y el host.</span><span class="sxs-lookup"><span data-stu-id="97442-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="97442-198">Ejecutar consultas de Spark mediante el conector de Hola</span><span class="sxs-lookup"><span data-stu-id="97442-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="97442-199">Hola después de la instancia de base de datos de Azure Cosmos de Hola de usos de ejemplo que se creó en el fragmento de código anterior hello mediante Hola especifica claves de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="97442-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="97442-200">Hello fragmento de código siguiente conecta toohello DepartureDelays.flights_pcoll colección (en Hola DoctorWho cuenta como se especificó anteriormente) y ejecuta una consulta tooextract Hola retraso la información de vuelo de vuelos que salen de Seattle.</span><span class="sxs-lookup"><span data-stu-id="97442-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="97442-201">¿Por qué usar la implementación del conector de BD de Cosmos de hello Spark tooAzure?</span><span class="sxs-lookup"><span data-stu-id="97442-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="97442-202">Conexión tooAzure Spark Cosmos DB mediante el conector de hello es normalmente en escenarios donde:</span><span class="sxs-lookup"><span data-stu-id="97442-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="97442-203">Desea toouse Scala y actualizarlo tooinclude un contenedor de Python, tal y como se indicó en [problema 3: contenedor agregar Python y ejemplos](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="97442-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="97442-204">Tiene una gran cantidad de datos tootransfer entre Apache Spark y base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="97442-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="97442-205">toogive una idea de diferencia de rendimiento de la consulta de hello, verá hello [wiki de ejecuciones de pruebas de consulta](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="97442-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="97442-206">Ejemplo de agregación distribuida</span><span class="sxs-lookup"><span data-stu-id="97442-206">Distributed aggregation example</span></span>
<span data-ttu-id="97442-207">En esta sección se proporcionan algunos ejemplos de cómo se pueden realizar agregaciones distribuidas y análisis de forma conjunta con la utilización de Apache Spark y Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="97442-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="97442-208">Base de datos de Azure Cosmos ya admite agregaciones, que se describe en hello [agregados de escala de planeta con base de datos de Azure Cosmos blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="97442-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="97442-209">Le mostramos cómo puede llevarlos toohello junto con Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="97442-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="97442-210">Tenga en cuenta que estas agrupaciones están en referencia toohello [Bloc de notas de Spark tooAzure Cosmos DB Connector](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="97442-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="97442-211">Conexión de datos de ejemplo de tooflights</span><span class="sxs-lookup"><span data-stu-id="97442-211">Connect tooflights sample data</span></span>
<span data-ttu-id="97442-212">En estos ejemplos de agregaciones, se accede a algunos datos de rendimiento sobre vuelos almacenados en la base de datos **DoctorWho** de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="97442-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="97442-213">tooconnect tooit, necesita hello tooutilize siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="97442-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

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

<span data-ttu-id="97442-214">Con este fragmento de código, estamos también continuo toorun una consulta básica que las transferencias de Hola conjunto filtrado de datos de la base de datos de Azure Cosmos tooSpark donde hello este último puede realizar agregados distribuidos.</span><span class="sxs-lookup"><span data-stu-id="97442-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="97442-215">En este caso, se pregunta por los vuelos que salen de Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="97442-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="97442-216">Hola se generaron resultados siguientes mediante la ejecución de consultas de Hola de hello Jupyter servicio de Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="97442-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="97442-217">Tenga en cuenta que todos los fragmentos de código de hello tooany genérico y no específicos del servicio.</span><span class="sxs-lookup"><span data-stu-id="97442-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="97442-218">Ejecución de consultas LIMIT y COUNT</span><span class="sxs-lookup"><span data-stu-id="97442-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="97442-219">Simplemente como le usa tooin SQL/Spark SQL, vamos a empezar con una **límite** consulta:</span><span class="sxs-lookup"><span data-stu-id="97442-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Consulta LIMIT de Spark](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="97442-221">Hello consulta siguiente es una sencilla y rápida **recuento** consulta:</span><span class="sxs-lookup"><span data-stu-id="97442-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Consulta COUNT de Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="97442-223">Consulta GROUP BY</span><span class="sxs-lookup"><span data-stu-id="97442-223">GROUP BY query</span></span>
<span data-ttu-id="97442-224">En el conjunto siguiente, se van a ejecutar consultas **GROUP BY** con facilidad en la base de datos de Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="97442-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Gráfico de consultas GROUP BY de Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="97442-226">Consulta DISTINCT, ORDER BY</span><span class="sxs-lookup"><span data-stu-id="97442-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="97442-227">Esta es una consulta **DISTINCT, ORDER BY**:</span><span class="sxs-lookup"><span data-stu-id="97442-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Gráfico de consultas GROUP BY de Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="97442-229">Continuar el análisis de datos del vuelo de Hola</span><span class="sxs-lookup"><span data-stu-id="97442-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="97442-230">Puede usar Hola después de análisis de toocontinue de las consultas de ejemplo de datos de vuelo hello:</span><span class="sxs-lookup"><span data-stu-id="97442-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="97442-231">Los 5 destinos (ciudades) principales con vuelos retrasados que salen de Seattle</span><span class="sxs-lookup"><span data-stu-id="97442-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Gráfico de los principales retrasos de Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="97442-233">Cálculo del valor medio de los retrasos según las ciudades de destino cuyos vuelos salen de Seattle</span><span class="sxs-lookup"><span data-stu-id="97442-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Gráfico de valores medios de retrasos de Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="97442-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97442-235">Next steps</span></span>

<span data-ttu-id="97442-236">Si no lo ha hecho ya, descargar conector de base de datos de Cosmos de hello Spark tooAzure de hello [cosmosdb de azure de spark](https://github.com/Azure/azure-cosmosdb-spark) repositorio de GitHub y explorar recursos adicionales de hello en el repositorio de hello:</span><span class="sxs-lookup"><span data-stu-id="97442-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* [<span data-ttu-id="97442-237">Ejemplos de agregaciones distribuidas</span><span class="sxs-lookup"><span data-stu-id="97442-237">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="97442-238">Cuadernos y script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="97442-238">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="97442-239">También podría interesarle hello tooreview [Apache Spark SQL, tramas de datos y conjuntos de datos guía](http://spark.apache.org/docs/latest/sql-programming-guide.html) hello y [Apache Spark en HDInsight de Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="97442-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
