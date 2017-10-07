---
title: aaaTroubleshoot Storm mediante el uso de HDInsight de Azure | Documentos de Microsoft
description: Obtenga respuestas toocommon preguntas sobre el uso de Apache Storm con HDInsight de Azure.
keywords: "Azure HDInsight, Storm, preguntas más frecuentes, guía de solución de problemas, problemas comunes"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="7633d-104">Solución de problemas de Storm mediante Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7633d-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="7633d-105">Obtenga información acerca de los principales problemas de Hola y sus soluciones para trabajar con cargas de Apache Storm en Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="7633d-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="7633d-106">¿Cómo obtengo acceso Hola aluvión de interfaz de usuario en un clúster</span><span class="sxs-lookup"><span data-stu-id="7633d-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="7633d-107">Tiene dos opciones para tener acceso a Hola aluvión de interfaz de usuario desde un explorador:</span><span class="sxs-lookup"><span data-stu-id="7633d-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="7633d-108">Interfaz de usuario de Ambari</span><span class="sxs-lookup"><span data-stu-id="7633d-108">Ambari UI</span></span>
1. <span data-ttu-id="7633d-109">Vaya a Panel de Ambari toohello.</span><span class="sxs-lookup"><span data-stu-id="7633d-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="7633d-110">En la lista de hello de servicios, seleccione **Storm**.</span><span class="sxs-lookup"><span data-stu-id="7633d-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="7633d-111">Hola **vínculos rápidos** menú, seleccione **aluvión de interfaz de usuario**.</span><span class="sxs-lookup"><span data-stu-id="7633d-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="7633d-112">Vínculo directo</span><span class="sxs-lookup"><span data-stu-id="7633d-112">Direct link</span></span>
<span data-ttu-id="7633d-113">Puede tener acceso a Hola aluvión de interfaz de usuario en hello después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="7633d-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="7633d-114">https://\<nombre DNS del clúster\>/stormui</span><span class="sxs-lookup"><span data-stu-id="7633d-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="7633d-115">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7633d-115">Example:</span></span>

 <span data-ttu-id="7633d-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="7633d-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="7633d-117">Cómo transferir información de punto de comprobación de Storm eventos concentrador pitorro de una topología tooanother</span><span class="sxs-lookup"><span data-stu-id="7633d-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="7633d-118">Cuando se desarrollan las topologías que leen desde los centros de eventos de Azure mediante Hola archivo .jar de HDInsight Storm eventos concentrador pitorro, debe implementar una topología que tiene el mismo nombre en un nuevo clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="7633d-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="7633d-119">Sin embargo, debe conservar los datos de punto de comprobación de Hola que estaba confirmada tooApache ZooKeeper en el clúster antiguo Hola.</span><span class="sxs-lookup"><span data-stu-id="7633d-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="7633d-120">Dónde se almacenan los datos de punto de control</span><span class="sxs-lookup"><span data-stu-id="7633d-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="7633d-121">Datos de punto de control de los desplazamientos se almacenan por hello pitorro de concentrador de eventos en ZooKeeper en dos rutas de acceso raíz:</span><span class="sxs-lookup"><span data-stu-id="7633d-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="7633d-122">Los puntos de control de spout no transaccionales se almacenan en /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="7633d-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="7633d-123">Los datos de punto de control de spout de transacciones se almacenan en /transactional.</span><span class="sxs-lookup"><span data-stu-id="7633d-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="7633d-124">Cómo toorestore</span><span class="sxs-lookup"><span data-stu-id="7633d-124">How toorestore</span></span>
<span data-ttu-id="7633d-125">secuencias de comandos de tooget hello y bibliotecas que se utilizan datos de tooexport fuera ZooKeeper y, a continuación, importa Hola datos atrás tooZooKeeper con un nombre nuevo, consulte [ejemplos aluvión de HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="7633d-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="7633d-126">carpeta de "lib" Hello tiene archivos .jar que contienen la implementación de hello para la operación de exportación/importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7633d-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="7633d-127">carpeta de bash Hello tiene un script de ejemplo que muestra cómo tooexport datos de Hola server ZooKeeper en el clúster antiguo hello y después importarlos a un servidor de ZooKeeper toohello atrás en el nuevo clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="7633d-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="7633d-128">Ejecute hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script de Hola ZooKeeper nodos tooexport y, a continuación, importar datos.</span><span class="sxs-lookup"><span data-stu-id="7633d-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="7633d-129">Hola script toohello correcta Hortonworks Data Platform (HDP) versión de actualización.</span><span class="sxs-lookup"><span data-stu-id="7633d-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="7633d-130">(Estamos trabajando en que estos scripts sean genéricos en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7633d-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="7633d-131">Scripts genéricos pueden ejecutar desde cualquier nodo en clúster de hello sin modificaciones por el usuario de Hola.)</span><span class="sxs-lookup"><span data-stu-id="7633d-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="7633d-132">comando de exportación de Hello escribe Hola metadatos tooan sistema de archivos distribuido de Apache Hadoop (HDFS) ruta de acceso (en un almacén de almacenamiento de blobs de Azure o almacén de Azure Data Lake) en una ubicación que se establece.</span><span class="sxs-lookup"><span data-stu-id="7633d-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="7633d-133">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7633d-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="7633d-134">Exportación de los metadatos de desplazamiento</span><span class="sxs-lookup"><span data-stu-id="7633d-134">Export offset metadata</span></span>
1. <span data-ttu-id="7633d-135">Usar clústeres SSH toogo toohello ZooKeeper en clúster de Hola desde qué punto de control de hello desplazamiento debe toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="7633d-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="7633d-136">Hola ejecución comando siguiente (después de actualizar la cadena de versión HDP hello) tooexport ZooKeeper desplazamiento datos toohello /stormmetadta/zkdata HDFS ruta de acceso:</span><span class="sxs-lookup"><span data-stu-id="7633d-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="7633d-137">Importación de los metadatos de desplazamiento</span><span class="sxs-lookup"><span data-stu-id="7633d-137">Import offset metadata</span></span>
1. <span data-ttu-id="7633d-138">Usar clústeres SSH toogo toohello ZooKeeper en clúster de Hola desde qué punto de control de hello desplazamiento debe toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="7633d-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="7633d-139">Ejecución hello después del comando (después de actualizar la cadena de versión de Hola HDP) tooimport ZooKeeper desplazamiento datos Hola HDFS ruta de acceso/stormmetadata/zkdata toohello ZooKeeper servidor en clúster de destino de hello:</span><span class="sxs-lookup"><span data-stu-id="7633d-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="7633d-140">Eliminar los metadatos de desplazamiento para que las topologías pueden comenzar a procesar datos desde el principio de Hola o de una marca de tiempo que el usuario Hola elige</span><span class="sxs-lookup"><span data-stu-id="7633d-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="7633d-141">Usar clústeres SSH toogo toohello ZooKeeper en clúster de Hola desde qué punto de control de hello desplazamiento debe toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="7633d-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="7633d-142">Ejecución hello después del comando (después de actualizar la cadena de versión de Hola HDP) toodelete todos los ZooKeeper desplazamiento datos en el clúster de hello actual:</span><span class="sxs-lookup"><span data-stu-id="7633d-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="7633d-143">Cómo se buscan los archivos binarios de Storm en un clúster</span><span class="sxs-lookup"><span data-stu-id="7633d-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="7633d-144">Los archivos binarios de aluvión de pila actual de HDP de hello están en /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="7633d-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="7633d-145">ubicación de Hello es Hola mismo para los nodos principales y para los nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="7633d-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="7633d-146">Puede haber varios archivos binarios para versiones específicas de HDP en /usr/hdp (por ejemplo, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="7633d-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="7633d-147">carpeta de Hello /usr/hdp/current/storm-client es symlinked toohello versión más reciente que se ejecuta en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="7633d-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="7633d-148">Para obtener más información, consulte [clúster de HDInsight de tooan de conectar a través de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) y [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="7633d-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="7633d-149">¿Cómo se puede determinar la topología de implementación de Hola de un clúster de Storm</span><span class="sxs-lookup"><span data-stu-id="7633d-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="7633d-150">En primer lugar, identifique todos los componentes que se instalan con Storm de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7633d-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="7633d-151">Un clúster de Storm consta de cuatro categorías de nodo:</span><span class="sxs-lookup"><span data-stu-id="7633d-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="7633d-152">Nodos de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="7633d-152">Gateway nodes</span></span>
* <span data-ttu-id="7633d-153">Nodos principales</span><span class="sxs-lookup"><span data-stu-id="7633d-153">Head nodes</span></span>
* <span data-ttu-id="7633d-154">Nodos de ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="7633d-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="7633d-155">Nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="7633d-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="7633d-156">Nodos de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="7633d-156">Gateway nodes</span></span>
<span data-ttu-id="7633d-157">Un nodo de puerta de enlace es una puerta de enlace y el servicio de proxy inverso que permite el servicio de administración de acceso público tooan active Ambari.</span><span class="sxs-lookup"><span data-stu-id="7633d-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="7633d-158">También controla la elección del líder de Ambari.</span><span class="sxs-lookup"><span data-stu-id="7633d-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="7633d-159">Nodos principales</span><span class="sxs-lookup"><span data-stu-id="7633d-159">Head nodes</span></span>
<span data-ttu-id="7633d-160">Nodos principales del aluvión ejecutan hello siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="7633d-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="7633d-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="7633d-161">Nimbus</span></span>
* <span data-ttu-id="7633d-162">Servidor Ambari</span><span class="sxs-lookup"><span data-stu-id="7633d-162">Ambari server</span></span>
* <span data-ttu-id="7633d-163">Servidor de métricas de Ambari</span><span class="sxs-lookup"><span data-stu-id="7633d-163">Ambari Metrics server</span></span>
* <span data-ttu-id="7633d-164">Recopilador de métricas de Ambari</span><span class="sxs-lookup"><span data-stu-id="7633d-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="7633d-165">Nodos de ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="7633d-165">ZooKeeper nodes</span></span>
<span data-ttu-id="7633d-166">HDInsight incluye un cuórum de ZooKeeper de tres nodos.</span><span class="sxs-lookup"><span data-stu-id="7633d-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="7633d-167">tamaño de quórum de Hello es fijo y no se puede reconfigurar.</span><span class="sxs-lookup"><span data-stu-id="7633d-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="7633d-168">Servicios de Storm en clúster de hello son quórum de tooautomatically configurado uso hello ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="7633d-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="7633d-169">Nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="7633d-169">Worker nodes</span></span>
<span data-ttu-id="7633d-170">Nodos de trabajador de Storm ejecutan hello siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="7633d-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="7633d-171">Supervisor</span><span class="sxs-lookup"><span data-stu-id="7633d-171">Supervisor</span></span>
* <span data-ttu-id="7633d-172">Máquinas virtuales Java (JVM) de trabajo, para topologías en ejecución</span><span class="sxs-lookup"><span data-stu-id="7633d-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="7633d-173">Agente de Ambari</span><span class="sxs-lookup"><span data-stu-id="7633d-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="7633d-174">Localización de los archivos binarios del spout del centro de eventos de Storm para el desarrollo</span><span class="sxs-lookup"><span data-stu-id="7633d-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="7633d-175">Para obtener más información acerca del uso de archivos .jar de Storm eventos concentrador pitorro con la topología, consulte Hola recursos siguientes.</span><span class="sxs-lookup"><span data-stu-id="7633d-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="7633d-176">Topología basada en Java</span><span class="sxs-lookup"><span data-stu-id="7633d-176">Java-based topology</span></span>
[<span data-ttu-id="7633d-177">Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="7633d-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="7633d-178">Topología basada en C# (Mono en clústeres de Storm Linux HDInsight 3.4 o superior)</span><span class="sxs-lookup"><span data-stu-id="7633d-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="7633d-179">Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="7633d-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="7633d-180">Archivos binarios de spout del centro de eventos de Storm para clústeres de Storm Linux HDInsight 3.5 y superior</span><span class="sxs-lookup"><span data-stu-id="7633d-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="7633d-181">toolearn cómo toouse hello más reciente Storm eventos concentrador pitorro que funciona con HDInsight 3.5 + aluvión de Linux clústeres, vea hello mvn-repo [archivo Léame](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="7633d-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="7633d-182">Ejemplos de código fuente</span><span class="sxs-lookup"><span data-stu-id="7633d-182">Source code examples</span></span>
<span data-ttu-id="7633d-183">Vea [ejemplos](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) de cómo tooread y escribir desde el centro de eventos de Azure mediante una topología de Apache Storm (escrita en Java) en un clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="7633d-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="7633d-184">Cómo se pueden encontrar los archivos de configuración Log4J de Storm en clústeres</span><span class="sxs-lookup"><span data-stu-id="7633d-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="7633d-185">archivos de configuración de tooidentify Log4J Apache para servicios de Storm.</span><span class="sxs-lookup"><span data-stu-id="7633d-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="7633d-186">En nodos principales</span><span class="sxs-lookup"><span data-stu-id="7633d-186">On head nodes</span></span>
<span data-ttu-id="7633d-187">se lee la configuración de Hello Nimbus Log4J desde/usr/hdp/\<versión HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="7633d-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="7633d-188">En nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="7633d-188">On worker nodes</span></span>
<span data-ttu-id="7633d-189">configuración de supervisor Log4J Hola se lee desde/usr/hdp/\<versión HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="7633d-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="7633d-190">archivo de configuración de trabajo Log4J Hola se lee desde/usr/hdp/\<versión HDP\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="7633d-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="7633d-191">Ejemplos: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="7633d-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

