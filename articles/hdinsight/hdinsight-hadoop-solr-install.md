---
title: "Uso de la acción de script para instalar Solr en un clúster de Hadoop - Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo personalizar un clúster de HDInsight con Solr mediante la acción de script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 6efb7ea26c3cdf7748fff4b02b5810c85cc41e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="39b57-103">Instalación y uso de Solr en clústeres de HDInsight basados en Windows</span><span class="sxs-lookup"><span data-stu-id="39b57-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="39b57-104">Aprenda a personalizar un clúster de HDInsight basado en Windows con Solr mediante la acción de script, y cómo usar Solr para buscar datos.</span><span class="sxs-lookup"><span data-stu-id="39b57-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39b57-105">Los pasos de este tutorial solo se aplican a los clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="39b57-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="39b57-106">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="39b57-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="39b57-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="39b57-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="39b57-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="39b57-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="39b57-109">Para obtener información sobre el uso de Solr con un clúster basado en Linux, consulte [Instalación y uso de Solr en clústeres de Hadoop para HDinsight (Linux)](hdinsight-hadoop-solr-install-linux.md)</span><span class="sxs-lookup"><span data-stu-id="39b57-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="39b57-110">Puede instalar R en cualquier tipo de clúster (Hadoop, Storm, HBase, Spark) en HDInsight de Azure mediante la *acción de script*.</span><span class="sxs-lookup"><span data-stu-id="39b57-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="39b57-111">Hay un script de ejemplo para instalar Solr en un clúster de HDInsight disponible desde un blob de almacenamiento de Azure de solo lectura en [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="39b57-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="39b57-112">El script de ejemplo solo funciona con el clúster de HDInsight versión 3.1.</span><span class="sxs-lookup"><span data-stu-id="39b57-112">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="39b57-113">Para obtener más información acerca de las versiones de clústeres de HDInsight, consulte las [versiones de clústeres de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="39b57-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="39b57-114">El script de ejemplo que se usa en este tema crea un clúster de Solr con una configuración concreta.</span><span class="sxs-lookup"><span data-stu-id="39b57-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="39b57-115">Si desea configurar el clúster de Solr con distintas colecciones, particiones, esquemas o réplicas, entre otras, debe modificar el script y los archivos binarios de Solr en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="39b57-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span></span>

<span data-ttu-id="39b57-116">**Artículos relacionados**</span><span class="sxs-lookup"><span data-stu-id="39b57-116">**Related articles**</span></span>

* [<span data-ttu-id="39b57-117">Instalación y uso de Solr en clústeres de Hadoop para HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="39b57-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="39b57-118">[Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="39b57-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="39b57-119">[Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.</span><span class="sxs-lookup"><span data-stu-id="39b57-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="39b57-120">[Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="39b57-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="39b57-121">¿Qué es Solr?</span><span class="sxs-lookup"><span data-stu-id="39b57-121">What is Solr?</span></span>
<span data-ttu-id="39b57-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> es una plataforma de búsqueda empresarial que permite una eficaz búsqueda de texto completo en los datos.</span><span class="sxs-lookup"><span data-stu-id="39b57-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="39b57-123">Si bien Hadoop permite almacenar y administrar grandes cantidades de datos, Apache Solr proporciona las capacidades de búsqueda para recuperar rápidamente los datos.</span><span class="sxs-lookup"><span data-stu-id="39b57-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="39b57-124">Instalación de Solr mediante el portal</span><span class="sxs-lookup"><span data-stu-id="39b57-124">Install Solr using portal</span></span>
1. <span data-ttu-id="39b57-125">Comience a crear un clúster mediante la opción **CREACIÓN PERSONALIZADA**, como se describe en [Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="39b57-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="39b57-126">En la página **Acciones de script** del asistente, haga clic en **Agregar acción de script** para proporcionar detalles acerca de la acción de script, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="39b57-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="39b57-127">![Uso de la acción de script para personalizar un clúster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Uso de la acción de script para personalizar un clúster")</span><span class="sxs-lookup"><span data-stu-id="39b57-127">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="39b57-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="39b57-128">Property</span></span></th><th><span data-ttu-id="39b57-129">Valor</span><span class="sxs-lookup"><span data-stu-id="39b57-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="39b57-130">Nombre</span><span class="sxs-lookup"><span data-stu-id="39b57-130">Name</span></span></td>
            <td><span data-ttu-id="39b57-131">Especifique un nombre para la acción de script.</span><span class="sxs-lookup"><span data-stu-id="39b57-131">Specify a name for the script action.</span></span> <span data-ttu-id="39b57-132">Por ejemplo, <b>Instalar Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="39b57-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="39b57-133">Identificador URI de script</span><span class="sxs-lookup"><span data-stu-id="39b57-133">Script URI</span></span></td>
            <td><span data-ttu-id="39b57-134">Especifique el Identificador uniforme de recursos (URI) al script que se ha invocado para personalizar el clúster.</span><span class="sxs-lookup"><span data-stu-id="39b57-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="39b57-135">Por ejemplo, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i>.</span><span class="sxs-lookup"><span data-stu-id="39b57-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="39b57-136">Tipo de nodo</span><span class="sxs-lookup"><span data-stu-id="39b57-136">Node Type</span></span></td>
            <td><span data-ttu-id="39b57-137">Especifique los nodos en los que se ejecuta el script de personalización.</span><span class="sxs-lookup"><span data-stu-id="39b57-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="39b57-138">Puede elegir <b>Todos los nodos</b>, <b>Solo nodos principales</b> o <b>Solo nodos de trabajo</b>.</span><span class="sxs-lookup"><span data-stu-id="39b57-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="39b57-139">Parámetros</span><span class="sxs-lookup"><span data-stu-id="39b57-139">Parameters</span></span></td>
            <td><span data-ttu-id="39b57-140">Especifique los parámetros, si lo requiere el script.</span><span class="sxs-lookup"><span data-stu-id="39b57-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="39b57-141">El script para instalar Solr no requiere ningún parámetro, por lo que puede dejarlo en blanco.</span><span class="sxs-lookup"><span data-stu-id="39b57-141">The script to install Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="39b57-142">Puede agregar más de una acción de script para instalar varios componentes en el clúster.</span><span class="sxs-lookup"><span data-stu-id="39b57-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="39b57-143">Después de haber agregado los scripts, haga clic en la marca de verificación para comenzar a crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="39b57-143">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="39b57-144">Uso de Solr</span><span class="sxs-lookup"><span data-stu-id="39b57-144">Use Solr</span></span>
<span data-ttu-id="39b57-145">Debe comenzar con la indización de Solr con algunos archivos de datos.</span><span class="sxs-lookup"><span data-stu-id="39b57-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="39b57-146">A continuación, puede utilizar Solr para ejecutar consultas de búsqueda en los datos indizados.</span><span class="sxs-lookup"><span data-stu-id="39b57-146">You can then use Solr to run search queries on the indexed data.</span></span> <span data-ttu-id="39b57-147">Realice los pasos siguientes para utilizar Solr en un clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="39b57-147">Perform the following steps to use Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="39b57-148">**Use el protocolo de Escritorio remoto (RDP) para conectarse de manera remota con el clúster de HDInsight con Solr instalado**.</span><span class="sxs-lookup"><span data-stu-id="39b57-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="39b57-149">En el portal de Azure, habilite el Escritorio remoto para el clúster que ha creado con Solr instalado y, a continuación, conéctese de manera remota con el clúster.</span><span class="sxs-lookup"><span data-stu-id="39b57-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span></span> <span data-ttu-id="39b57-150">Para obtener instrucciones, vea [Conexión a los clústeres de HDInsight con RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="39b57-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="39b57-151">**Indexe Solr mediante la carga de archivos de datos**.</span><span class="sxs-lookup"><span data-stu-id="39b57-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="39b57-152">Al indizar Solr, colocar en él aquellos documentos que tenga que buscar.</span><span class="sxs-lookup"><span data-stu-id="39b57-152">When you index Solr, you put documents in it that you may need to search on.</span></span> <span data-ttu-id="39b57-153">Para indexar Solr, use RDP para conectarse de manera remota al clúster, vaya al escritorio, abra la línea de comandos de Hadoop y vaya a **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="39b57-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="39b57-154">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="39b57-154">Run the following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="39b57-155">Debería ver estos resultados en la consola:</span><span class="sxs-lookup"><span data-stu-id="39b57-155">You'll see the following output on the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="39b57-156">La utilidad post.jar indexa Solr con dos documentos de muestra, **solr.xml** y **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="39b57-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="39b57-157">La utilidad post.jar y los documentos de muestra están disponibles con la instalación de Solr.</span><span class="sxs-lookup"><span data-stu-id="39b57-157">The post.jar utility and the sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="39b57-158">**Utilice el panel de Solr para buscan dentro de los documentos indexados**.</span><span class="sxs-lookup"><span data-stu-id="39b57-158">**Use the Solr dashboard to search within the indexed documents**.</span></span> <span data-ttu-id="39b57-159">En la sesión RDP con el clúster de HDInsight, abra Internet Explorer e inicie el panel de Solr en **http://headnodehost:8983/solr/#/**.</span><span class="sxs-lookup"><span data-stu-id="39b57-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="39b57-160">En el panel izquierdo, en la lista desplegable **Core Selector** (Selector principal), seleccione **collection1** y, dentro de ella, haga clic en **Query** (Consulta).</span><span class="sxs-lookup"><span data-stu-id="39b57-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="39b57-161">Por ejemplo, para seleccionar y devolver a todos los documentos de Solr, indique los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="39b57-161">As an example, to select and return all the docs in Solr, provide the following values:</span></span>

   * <span data-ttu-id="39b57-162">En el cuadro de texto **q**, escriba **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="39b57-162">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="39b57-163">Se devolverán todos los documentos indizados en Solr.</span><span class="sxs-lookup"><span data-stu-id="39b57-163">This will return all the documents that are indexed in Solr.</span></span> <span data-ttu-id="39b57-164">Si desea buscar una cadena específica dentro de los documentos, puede especificar esa cadena aquí.</span><span class="sxs-lookup"><span data-stu-id="39b57-164">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="39b57-165">En el cuadro de texto **wt** , seleccione el formato de salida.</span><span class="sxs-lookup"><span data-stu-id="39b57-165">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="39b57-166">El valor predeterminado es **json**.</span><span class="sxs-lookup"><span data-stu-id="39b57-166">Default is **json**.</span></span> <span data-ttu-id="39b57-167">Haga clic en **Ejecutar consulta**.</span><span class="sxs-lookup"><span data-stu-id="39b57-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="39b57-168">![Uso de la acción de script para personalizar un clúster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Ejecución de una consulta en el panel de Solr")</span><span class="sxs-lookup"><span data-stu-id="39b57-168">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="39b57-169">La salida devuelve los dos documentos utilizados para indizar el Solr.</span><span class="sxs-lookup"><span data-stu-id="39b57-169">The output returns the two docs that we used for indexing Solr.</span></span> <span data-ttu-id="39b57-170">La salida debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="39b57-170">The output resembles the following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. <span data-ttu-id="39b57-171">**Recomendación: cree una copia de seguridad de los datos indexados desde Solr en el almacenamiento de blobs de Azure asociados con el clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="39b57-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span></span> <span data-ttu-id="39b57-172">Se recomienda que cree una copia de seguridad de los datos indexados desde los nodos del clúster de Solr en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="39b57-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="39b57-173">Realice los pasos siguientes para ello:</span><span class="sxs-lookup"><span data-stu-id="39b57-173">Perform the following steps to do so:</span></span>

   1. <span data-ttu-id="39b57-174">Desde la sesión RDP, abra Internet Explorer y apunte a la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="39b57-174">From the RDP session, open Internet Explorer, and point to the following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="39b57-175">Debería obtener una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="39b57-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="39b57-176">En la sesión remota, vaya a {SOLR_HOME}\{Collection}\data.</span><span class="sxs-lookup"><span data-stu-id="39b57-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="39b57-177">Para el clúster creado con el script de ejemplo, debiera ser **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="39b57-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="39b57-178">En esta ubicación, verá una carpeta de instantáneas creada con un nombre similar a **snapshot.*timestamp***.</span><span class="sxs-lookup"><span data-stu-id="39b57-178">At this location, you should see a snapshot folder created with a name similar to **snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="39b57-179">Comprima la carpeta de instantáneas y cárguela al almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="39b57-179">Zip the snapshot folder and upload it to Azure Blob storage.</span></span> <span data-ttu-id="39b57-180">En la línea de comandos de Hadoop, use el comando siguiente para ir a la ubicación de la carpeta de instantáneas:</span><span class="sxs-lookup"><span data-stu-id="39b57-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="39b57-181">Este comando copia la instantánea en /example/data/ en el contenedor dentro de la cuenta de almacenamiento predeterminada asociada con el clúster.</span><span class="sxs-lookup"><span data-stu-id="39b57-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="39b57-182">Instalación de Solr mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="39b57-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="39b57-183">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="39b57-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="39b57-184">El ejemplo muestra cómo instalar Spark con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39b57-184">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="39b57-185">Deberá personalizar el script para usar [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="39b57-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="39b57-186">Instalación de Solr con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="39b57-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="39b57-187">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="39b57-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="39b57-188">El ejemplo muestra cómo instalar Spark con .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="39b57-188">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="39b57-189">Deberá personalizar el script para usar [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="39b57-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="39b57-190">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="39b57-190">See also</span></span>
* [<span data-ttu-id="39b57-191">Instalación y uso de Solr en clústeres de Hadoop para HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="39b57-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="39b57-192">[Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="39b57-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="39b57-193">[Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.</span><span class="sxs-lookup"><span data-stu-id="39b57-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="39b57-194">[Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="39b57-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="39b57-195">[Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]: ejemplo de acción de script sobre la instalación de Spark.</span><span class="sxs-lookup"><span data-stu-id="39b57-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="39b57-196">[Instalación de R en clústeres de HDInsight][hdinsight-install-r]: ejemplo de acción de script sobre la instalación de R.</span><span class="sxs-lookup"><span data-stu-id="39b57-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="39b57-197">[Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md): ejemplo de acción de script sobre la instalación de Giraph.</span><span class="sxs-lookup"><span data-stu-id="39b57-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
