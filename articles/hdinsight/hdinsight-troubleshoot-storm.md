---
title: "Solución de problemas de Storm mediante Azure HDInsight | Microsoft Docs"
description: "Obtenga respuestas a las preguntas comunes sobre cómo usar con Apache Storm con Azure HDInsight."
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
ms.openlocfilehash: 70a3d762431d90acdd6ed2a432a569f34d0ce447
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="2f474-104">Solución de problemas de Storm mediante Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f474-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="2f474-105">Obtenga información sobre los principales problemas y sus soluciones al trabajar con cargas útiles de Apache Storm en Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="2f474-105">Learn about the top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-the-storm-ui-on-a-cluster"></a><span data-ttu-id="2f474-106">Acceso a la interfaz de usuario de Storm en un clúster</span><span class="sxs-lookup"><span data-stu-id="2f474-106">How do I access the Storm UI on a cluster</span></span>
<span data-ttu-id="2f474-107">Tiene dos opciones para acceder a la interfaz de usuario de Storm desde un explorador:</span><span class="sxs-lookup"><span data-stu-id="2f474-107">You have two options for accessing the Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="2f474-108">Interfaz de usuario de Ambari</span><span class="sxs-lookup"><span data-stu-id="2f474-108">Ambari UI</span></span>
1. <span data-ttu-id="2f474-109">Vaya al panel de Ambari.</span><span class="sxs-lookup"><span data-stu-id="2f474-109">Go to the Ambari dashboard.</span></span>
2. <span data-ttu-id="2f474-110">En la lista de servicios, seleccione **Storm**.</span><span class="sxs-lookup"><span data-stu-id="2f474-110">In the list of services, select **Storm**.</span></span>
3. <span data-ttu-id="2f474-111">En el menú **Vínculos rápidos**, seleccione **Interfaz de usuario de Storm**.</span><span class="sxs-lookup"><span data-stu-id="2f474-111">In the **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="2f474-112">Vínculo directo</span><span class="sxs-lookup"><span data-stu-id="2f474-112">Direct link</span></span>
<span data-ttu-id="2f474-113">Puede acceder a la interfaz de usuario de Storm en la siguiente URL:</span><span class="sxs-lookup"><span data-stu-id="2f474-113">You can access the Storm UI at the following URL:</span></span>

<span data-ttu-id="2f474-114">https://\<nombre DNS del clúster\>/stormui</span><span class="sxs-lookup"><span data-stu-id="2f474-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="2f474-115">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2f474-115">Example:</span></span>

 <span data-ttu-id="2f474-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="2f474-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another"></a><span data-ttu-id="2f474-117">Transferencia de información del punto de control del spout del centro de eventos de Storm de una topología a otra</span><span class="sxs-lookup"><span data-stu-id="2f474-117">How do I transfer Storm event hub spout checkpoint information from one topology to another</span></span>

<span data-ttu-id="2f474-118">Cuando se desarrollan topologías que leen desde instancias de Azure Event Hubs mediante el archivo .jar del spout del centro de eventos Storm en HDInsight, debe implementar una topología que tenga el mismo nombre en un nuevo clúster.</span><span class="sxs-lookup"><span data-stu-id="2f474-118">When you develop topologies that read from Azure Event Hubs by using the HDInsight Storm event hub spout .jar file, you must deploy a topology that has the same name on a new cluster.</span></span> <span data-ttu-id="2f474-119">Sin embargo, debe conservar los datos del punto de control que se confirmaron en Apache ZooKeeper en el clúster antiguo.</span><span class="sxs-lookup"><span data-stu-id="2f474-119">However, you must retain the checkpoint data that was committed to Apache ZooKeeper on the old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="2f474-120">Dónde se almacenan los datos de punto de control</span><span class="sxs-lookup"><span data-stu-id="2f474-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="2f474-121">El spout del centro de eventos almacena los datos de punto de control para los desplazamientos en ZooKeeper en dos rutas de acceso raíz:</span><span class="sxs-lookup"><span data-stu-id="2f474-121">Checkpoint data for offsets is stored by the event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="2f474-122">Los puntos de control de spout no transaccionales se almacenan en /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="2f474-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="2f474-123">Los datos de punto de control de spout de transacciones se almacenan en /transactional.</span><span class="sxs-lookup"><span data-stu-id="2f474-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-to-restore"></a><span data-ttu-id="2f474-124">Cómo restaurar</span><span class="sxs-lookup"><span data-stu-id="2f474-124">How to restore</span></span>
<span data-ttu-id="2f474-125">Para obtener los scripts y las bibliotecas que se utilizan para exportar datos de ZooKeeper y, después, importar de nuevo los datos a ZooKeeper con un nuevo nombre, consulte [Ejemplos de Storm de HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="2f474-125">To get the scripts and libraries that you use to export data out of ZooKeeper and then import the data back to ZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="2f474-126">La carpeta lib tiene archivos .jar que contienen la implementación para la operación de exportación e importación.</span><span class="sxs-lookup"><span data-stu-id="2f474-126">The lib folder has .jar files that contain the implementation for the export/import operation.</span></span> <span data-ttu-id="2f474-127">La carpeta bash tiene un script de ejemplo que muestra como exportar datos desde el servidor de ZooKeeper en el clúster anterior y, después, volver a importarlos al servidor de ZooKeeper en el nuevo clúster.</span><span class="sxs-lookup"><span data-stu-id="2f474-127">The bash folder has an example script that demonstrates how to export data from the ZooKeeper server on the old cluster, and then import it back to the ZooKeeper server on the new cluster.</span></span>

<span data-ttu-id="2f474-128">Ejecuta el script [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) desde los nodos de ZooKeeper para importar y después exportar datos.</span><span class="sxs-lookup"><span data-stu-id="2f474-128">Run the [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from the ZooKeeper nodes to export and then import data.</span></span> <span data-ttu-id="2f474-129">Actualice el script a la versión correcta de Hortonworks Data Platform (HDP).</span><span class="sxs-lookup"><span data-stu-id="2f474-129">Update the script to the correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="2f474-130">(Estamos trabajando en que estos scripts sean genéricos en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2f474-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="2f474-131">Los scripts genéricos pueden ejecutarse desde cualquier nodo en el clúster sin modificaciones por el usuario).</span><span class="sxs-lookup"><span data-stu-id="2f474-131">Generic scripts can run from any node on the cluster without modifications by the user.)</span></span>

<span data-ttu-id="2f474-132">El comando export escribe los metadatos en una ruta de acceso del Sistema de archivos distribuido de Apache Hadoop (HDFS) (en un almacén de Azure Blob Storage o de Azure Data Lake Store) en la ubicación que haya establecido.</span><span class="sxs-lookup"><span data-stu-id="2f474-132">The export command writes the metadata to an Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="2f474-133">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f474-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="2f474-134">Exportación de los metadatos de desplazamiento</span><span class="sxs-lookup"><span data-stu-id="2f474-134">Export offset metadata</span></span>
1. <span data-ttu-id="2f474-135">Use SSH para ir al clúster de ZooKeeper en el clúster desde el que se debe exportar el desplazamiento de punto de control.</span><span class="sxs-lookup"><span data-stu-id="2f474-135">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="2f474-136">Ejecute el comando siguiente (después de actualizar la cadena de versión de HDP) para exportar los datos de desplazamiento de ZooKeeper a la ruta de acceso de HDFS /stormmetadta/zkdata:</span><span class="sxs-lookup"><span data-stu-id="2f474-136">Run the following command (after you update the HDP version string) to export ZooKeeper offset data to the /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="2f474-137">Importación de los metadatos de desplazamiento</span><span class="sxs-lookup"><span data-stu-id="2f474-137">Import offset metadata</span></span>
1. <span data-ttu-id="2f474-138">Use SSH para ir al clúster de ZooKeeper en el clúster desde el que se debe exportar el desplazamiento de punto de control.</span><span class="sxs-lookup"><span data-stu-id="2f474-138">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="2f474-139">Ejecute el comando siguiente (después de actualizar la cadena de versión de hdp) para importar los datos de desplazamiento de ZooKeeper desde la ruta de acceso de HDFS /stormmetadata/zkdata al servidor de ZooKeeper en el clúster de destino:</span><span class="sxs-lookup"><span data-stu-id="2f474-139">Run the following command (after you update the HDP version string) to import ZooKeeper offset data from the HDFS path /stormmetadata/zkdata to the ZooKeeper server on the target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-the-beginning-or-from-a-timestamp-that-the-user-chooses"></a><span data-ttu-id="2f474-140">Elimine los metadatos de desplazamiento para que las topologías puedan empezar a procesar los datos desde el principio o desde una marca de tiempo que elija el usuario.</span><span class="sxs-lookup"><span data-stu-id="2f474-140">Delete offset metadata so that topologies can start processing data from the beginning, or from a timestamp that the user chooses</span></span>
1. <span data-ttu-id="2f474-141">Use SSH para ir al clúster de ZooKeeper en el clúster desde el que se debe exportar el desplazamiento de punto de control.</span><span class="sxs-lookup"><span data-stu-id="2f474-141">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="2f474-142">Ejecute el comando siguiente (después de actualizar la cadena de versión de HDP) para eliminar todos los datos de desplazamiento de ZooKeeper del clúster actual:</span><span class="sxs-lookup"><span data-stu-id="2f474-142">Run the following command (after you update the HDP version string) to delete all ZooKeeper offset data in the current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="2f474-143">Cómo se buscan los archivos binarios de Storm en un clúster</span><span class="sxs-lookup"><span data-stu-id="2f474-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="2f474-144">Los archivos binarios de Storm para la pila de HDP actual se encuentran en: /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="2f474-144">Storm binaries for the current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="2f474-145">La ubicación es la misma para los nodos principales y para los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2f474-145">The location is the same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="2f474-146">Puede haber varios archivos binarios para versiones específicas de HDP en /usr/hdp (por ejemplo, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="2f474-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="2f474-147">La carpeta /usr/hdp/current/storm-client tiene un vínculo simbólico a la versión más reciente que se ejecuta en el clúster.</span><span class="sxs-lookup"><span data-stu-id="2f474-147">The /usr/hdp/current/storm-client folder is symlinked to the latest version that is running on the cluster.</span></span>

<span data-ttu-id="2f474-148">Para más información, consulte cómo [conectarse a un clúster de HDInsight a través de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) y [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="2f474-148">For more information, see [Connect to an HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-the-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="2f474-149">Cómo se puede determinar la topología de implementación de un clúster de Storm</span><span class="sxs-lookup"><span data-stu-id="2f474-149">How do I determine the deployment topology of a Storm cluster</span></span>
<span data-ttu-id="2f474-150">En primer lugar, identifique todos los componentes que se instalan con Storm de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2f474-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="2f474-151">Un clúster de Storm consta de cuatro categorías de nodo:</span><span class="sxs-lookup"><span data-stu-id="2f474-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="2f474-152">Nodos de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="2f474-152">Gateway nodes</span></span>
* <span data-ttu-id="2f474-153">Nodos principales</span><span class="sxs-lookup"><span data-stu-id="2f474-153">Head nodes</span></span>
* <span data-ttu-id="2f474-154">Nodos de ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="2f474-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="2f474-155">Nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="2f474-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="2f474-156">Nodos de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="2f474-156">Gateway nodes</span></span>
<span data-ttu-id="2f474-157">Un nodo de puerta de enlace es una puerta de enlace y un servicio de proxy inverso que permite el acceso público a un servicio de administración de Ambari activo.</span><span class="sxs-lookup"><span data-stu-id="2f474-157">A gateway node is a gateway and reverse proxy service that enables public access to an active Ambari management service.</span></span> <span data-ttu-id="2f474-158">También controla la elección del líder de Ambari.</span><span class="sxs-lookup"><span data-stu-id="2f474-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="2f474-159">Nodos principales</span><span class="sxs-lookup"><span data-stu-id="2f474-159">Head nodes</span></span>
<span data-ttu-id="2f474-160">Los nodos principales de Storm ejecutan los siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="2f474-160">Storm head nodes run the following services:</span></span>
* <span data-ttu-id="2f474-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="2f474-161">Nimbus</span></span>
* <span data-ttu-id="2f474-162">Servidor Ambari</span><span class="sxs-lookup"><span data-stu-id="2f474-162">Ambari server</span></span>
* <span data-ttu-id="2f474-163">Servidor de métricas de Ambari</span><span class="sxs-lookup"><span data-stu-id="2f474-163">Ambari Metrics server</span></span>
* <span data-ttu-id="2f474-164">Recopilador de métricas de Ambari</span><span class="sxs-lookup"><span data-stu-id="2f474-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="2f474-165">Nodos de ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="2f474-165">ZooKeeper nodes</span></span>
<span data-ttu-id="2f474-166">HDInsight incluye un cuórum de ZooKeeper de tres nodos.</span><span class="sxs-lookup"><span data-stu-id="2f474-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="2f474-167">El tamaño del cuórum es fijo y no se puede volver a configurar.</span><span class="sxs-lookup"><span data-stu-id="2f474-167">The quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="2f474-168">Los servicios de Storm en el clúster se configuran para usar automáticamente el cuórum de ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="2f474-168">Storm services in the cluster are configured to automatically use the ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="2f474-169">Nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="2f474-169">Worker nodes</span></span>
<span data-ttu-id="2f474-170">Los nodos de trabajo de Storm ejecutan los siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="2f474-170">Storm worker nodes run the following services:</span></span>
* <span data-ttu-id="2f474-171">Supervisor</span><span class="sxs-lookup"><span data-stu-id="2f474-171">Supervisor</span></span>
* <span data-ttu-id="2f474-172">Máquinas virtuales Java (JVM) de trabajo, para topologías en ejecución</span><span class="sxs-lookup"><span data-stu-id="2f474-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="2f474-173">Agente de Ambari</span><span class="sxs-lookup"><span data-stu-id="2f474-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="2f474-174">Localización de los archivos binarios del spout del centro de eventos de Storm para el desarrollo</span><span class="sxs-lookup"><span data-stu-id="2f474-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="2f474-175">Para más información sobre el uso de archivos .jar del centro de eventos de Storm con su topología, consulte los siguientes recursos.</span><span class="sxs-lookup"><span data-stu-id="2f474-175">For more information about using Storm event hub spout .jar files with your topology, see the following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="2f474-176">Topología basada en Java</span><span class="sxs-lookup"><span data-stu-id="2f474-176">Java-based topology</span></span>
[<span data-ttu-id="2f474-177">Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="2f474-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="2f474-178">Topología basada en C# (Mono en clústeres de Storm Linux HDInsight 3.4 o superior)</span><span class="sxs-lookup"><span data-stu-id="2f474-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="2f474-179">Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="2f474-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="2f474-180">Archivos binarios de spout del centro de eventos de Storm para clústeres de Storm Linux HDInsight 3.5 y superior</span><span class="sxs-lookup"><span data-stu-id="2f474-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="2f474-181">Para obtener información sobre cómo usar el spout del centro de eventos de Storm más reciente que funciona con los clústeres de Linux Storm de HDInsight 3.5 o superior, consulte el [archivo Léame](https://github.com/hdinsight/mvn-repo/blob/master/README.md) de mvn-repo.</span><span class="sxs-lookup"><span data-stu-id="2f474-181">To learn how to use the latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see the mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="2f474-182">Ejemplos de código fuente</span><span class="sxs-lookup"><span data-stu-id="2f474-182">Source code examples</span></span>
<span data-ttu-id="2f474-183">Consulte algunos [ejemplos](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) sobre cómo leer y escribir desde un centro de eventos de Azure Event Hubs mediante una topología de Apache Storm (escrita en Java) en un clúster de Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2f474-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how to read and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="2f474-184">Cómo se pueden encontrar los archivos de configuración Log4J de Storm en clústeres</span><span class="sxs-lookup"><span data-stu-id="2f474-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="2f474-185">Para identificar los archivos de configuración de Log4J de Apache para servicios de Storm.</span><span class="sxs-lookup"><span data-stu-id="2f474-185">To identify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="2f474-186">En nodos principales</span><span class="sxs-lookup"><span data-stu-id="2f474-186">On head nodes</span></span>
<span data-ttu-id="2f474-187">La configuración Log4J de Nimbus se lee de /usr/hdp/\<versión de HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="2f474-187">The Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="2f474-188">En nodos de trabajo</span><span class="sxs-lookup"><span data-stu-id="2f474-188">On worker nodes</span></span>
<span data-ttu-id="2f474-189">La configuración Log4J del supervisor se lee de /usr/hdp/\<versión de HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="2f474-189">The supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="2f474-190">El archivo de configuración Log4J de trabajo se lee de /usr/hdp/\<versión de HDP\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="2f474-190">The worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="2f474-191">Ejemplos: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="2f474-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

