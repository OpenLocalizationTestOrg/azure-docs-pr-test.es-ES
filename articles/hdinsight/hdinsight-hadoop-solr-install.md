---
title: "Acción de secuencia de comandos tooinstall Solr de aaaUse en clúster de Hadoop - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar toocustomize HDInsight con Solr mediante la acción de secuencia de comandos."
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
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="d7d36-103">Instalación y uso de Solr en clústeres de HDInsight basados en Windows</span><span class="sxs-lookup"><span data-stu-id="d7d36-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="d7d36-104">Obtenga información acerca de cómo toocustomize HDInsight basados en Windows de clúster con Solr mediante la acción de secuencia de comandos y cómo toouse Solr toosearch datos.</span><span class="sxs-lookup"><span data-stu-id="d7d36-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7d36-105">Hola pasos de este trabajo único documento con clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="d7d36-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d7d36-106">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="d7d36-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="d7d36-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="d7d36-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d7d36-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d7d36-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="d7d36-109">Para obtener información sobre el uso de Solr con un clúster basado en Linux, consulte [Instalación y uso de Solr en clústeres de Hadoop para HDinsight (Linux)](hdinsight-hadoop-solr-install-linux.md)</span><span class="sxs-lookup"><span data-stu-id="d7d36-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="d7d36-110">Puede instalar R en cualquier tipo de clúster (Hadoop, Storm, HBase, Spark) en HDInsight de Azure mediante la *acción de script*.</span><span class="sxs-lookup"><span data-stu-id="d7d36-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="d7d36-111">Tooinstall de secuencia de comandos de ejemplo Solr en un clúster de HDInsight está disponible en un blob de almacenamiento de Azure de solo lectura en [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="d7d36-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="d7d36-112">script de ejemplo de Hola solo funciona con la versión de clúster de HDInsight 3.1.</span><span class="sxs-lookup"><span data-stu-id="d7d36-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="d7d36-113">Para obtener más información acerca de las versiones de clústeres de HDInsight, consulte las [versiones de clústeres de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d7d36-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="d7d36-114">script de ejemplo de Hola utilizado en este tema crea un clúster basado en Windows Solr con una configuración concreta.</span><span class="sxs-lookup"><span data-stu-id="d7d36-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="d7d36-115">Si desea que el clúster de Solr tooconfigure Hola con diferentes recopilaciones, particiones, esquemas, las réplicas, etc., debe modificar el script de Hola y archivos binarios de Solr en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="d7d36-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="d7d36-116">**Artículos relacionados**</span><span class="sxs-lookup"><span data-stu-id="d7d36-116">**Related articles**</span></span>

* [<span data-ttu-id="d7d36-117">Instalación y uso de Solr en clústeres de Hadoop para HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="d7d36-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="d7d36-118">[Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d7d36-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="d7d36-119">[Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.</span><span class="sxs-lookup"><span data-stu-id="d7d36-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="d7d36-120">[Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="d7d36-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="d7d36-121">¿Qué es Solr?</span><span class="sxs-lookup"><span data-stu-id="d7d36-121">What is Solr?</span></span>
<span data-ttu-id="d7d36-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> es una plataforma de búsqueda empresarial que permite una eficaz búsqueda de texto completo en los datos.</span><span class="sxs-lookup"><span data-stu-id="d7d36-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="d7d36-123">Mientras Hadoop permite almacenar y administrar grandes cantidades de datos, Apache Solr proporciona capacidades de búsqueda de hello tooquickly recuperar datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7d36-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="d7d36-124">Instalación de Solr mediante el portal</span><span class="sxs-lookup"><span data-stu-id="d7d36-124">Install Solr using portal</span></span>
1. <span data-ttu-id="d7d36-125">Empezar a crear un clúster mediante el uso de hello **creación personalizada** opción, como se describe en [Hadoop crear clústeres de HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d7d36-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="d7d36-126">En hello **acciones de Script** página del Asistente de hello, haga clic en **Agregar acción de secuencia de comandos** tooprovide detalles sobre la acción de secuencia de comandos de hello, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="d7d36-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="d7d36-127">![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize de acción de secuencia de comandos de uso un clúster")</span><span class="sxs-lookup"><span data-stu-id="d7d36-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="d7d36-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d7d36-128">Property</span></span></th><th><span data-ttu-id="d7d36-129">Valor</span><span class="sxs-lookup"><span data-stu-id="d7d36-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="d7d36-130">Nombre</span><span class="sxs-lookup"><span data-stu-id="d7d36-130">Name</span></span></td>
            <td><span data-ttu-id="d7d36-131">Especifique un nombre para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7d36-131">Specify a name for hello script action.</span></span> <span data-ttu-id="d7d36-132">Por ejemplo, <b>Instalar Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="d7d36-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="d7d36-133">Identificador URI de script</span><span class="sxs-lookup"><span data-stu-id="d7d36-133">Script URI</span></span></td>
            <td><span data-ttu-id="d7d36-134">Especificar una secuencia toohello de hello identificador uniforme de recursos (URI) que es invocado toocustomize Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="d7d36-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="d7d36-135">Por ejemplo, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i>.</span><span class="sxs-lookup"><span data-stu-id="d7d36-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="d7d36-136">Tipo de nodo</span><span class="sxs-lookup"><span data-stu-id="d7d36-136">Node Type</span></span></td>
            <td><span data-ttu-id="d7d36-137">Especifique los nodos de hello en el que se ejecuta el script de personalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7d36-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="d7d36-138">Puede elegir <b>Todos los nodos</b>, <b>Solo nodos principales</b> o <b>Solo nodos de trabajo</b>.</span><span class="sxs-lookup"><span data-stu-id="d7d36-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="d7d36-139">parameters</span><span class="sxs-lookup"><span data-stu-id="d7d36-139">Parameters</span></span></td>
            <td><span data-ttu-id="d7d36-140">Especificar parámetros de hello, si así lo requiere el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7d36-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="d7d36-141">Hola script tooinstall Solr no requiere ningún parámetro, por lo que puede dejar en blanco.</span><span class="sxs-lookup"><span data-stu-id="d7d36-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="d7d36-142">Puede agregar más de una secuencia de comandos acción tooinstall varios componentes en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7d36-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="d7d36-143">Después de haber agregado las secuencias de comandos de hello, haga clic en toostart de marca de verificación de hello crear clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="d7d36-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="d7d36-144">Uso de Solr</span><span class="sxs-lookup"><span data-stu-id="d7d36-144">Use Solr</span></span>
<span data-ttu-id="d7d36-145">Debe comenzar con la indización de Solr con algunos archivos de datos.</span><span class="sxs-lookup"><span data-stu-id="d7d36-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="d7d36-146">A continuación, puede usar consultas de búsqueda de Solr toorun en hello indizado datos.</span><span class="sxs-lookup"><span data-stu-id="d7d36-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="d7d36-147">Lleve a cabo Hola siguiendo los pasos toouse Solr en un clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d7d36-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="d7d36-148">**Usar tooremote de protocolo de escritorio remoto (RDP) en clúster de HDInsight de hello con Solr instalado**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="d7d36-149">Desde el portal de Azure hello, habilitar Escritorio remoto para clúster Hola creadas con clúster de hello instalado y, a continuación, remoto en Solr.</span><span class="sxs-lookup"><span data-stu-id="d7d36-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="d7d36-150">Para obtener instrucciones, consulte [conectarse mediante RDP de clústeres de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="d7d36-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="d7d36-151">**Indexe Solr mediante la carga de archivos de datos**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="d7d36-152">Al indizar Solr, coloque documentos en el que puede que necesite toosearch.</span><span class="sxs-lookup"><span data-stu-id="d7d36-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="d7d36-153">tooindex Solr, utilice RDP tooremote en clúster de hello, navegue toohello escritorio, abra la línea de comandos de Hadoop de Hola y navegar demasiado**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="d7d36-154">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="d7d36-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="d7d36-155">Verá Hola siguiente salida de consola hello:</span><span class="sxs-lookup"><span data-stu-id="d7d36-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="d7d36-156">utilidad de Hello post.jar indiza Solr con dos documentos de ejemplo, **solr.xml** y **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="d7d36-157">utilidad de post.jar Hello y documentos de ejemplo de Hola están disponibles con la instalación de Solr.</span><span class="sxs-lookup"><span data-stu-id="d7d36-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="d7d36-158">**Use hello Solr panel toosearch dentro de hello indizar documentos**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="d7d36-159">Hola RDP sesión toohello HDInsight clúster, abra Internet Explorer e iniciar panel de Solr hello en **http://headnodehost:8983/solr / #/**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="d7d36-160">En panel izquierdo de Hola y de hello **Core Selector** lista desplegable, seleccione **collection1**y dentro de ella, haga clic en **consulta**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="d7d36-161">Como un ejemplo, tooselect y se devuelven todos los documentos de hello en Solr, proporcionar Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="d7d36-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="d7d36-162">Hola **preguntas** texto cuadro, escriba  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="d7d36-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="d7d36-163">Esto devolverá todos los documentos de Hola que están indizados en Solr.</span><span class="sxs-lookup"><span data-stu-id="d7d36-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="d7d36-164">Si desea toosearch una cadena específica dentro de los documentos de hello, puede especificar esa cadena aquí.</span><span class="sxs-lookup"><span data-stu-id="d7d36-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="d7d36-165">Hola **wt** cuadro de texto, formato de salida de hello select.</span><span class="sxs-lookup"><span data-stu-id="d7d36-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="d7d36-166">El valor predeterminado es **json**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-166">Default is **json**.</span></span> <span data-ttu-id="d7d36-167">Haga clic en **Ejecutar consulta**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="d7d36-168">![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "ejecutar una consulta en el panel de Solr")</span><span class="sxs-lookup"><span data-stu-id="d7d36-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="d7d36-169">salida de Hello devuelve Hola dos documentos que hemos usado para indización Solr.</span><span class="sxs-lookup"><span data-stu-id="d7d36-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="d7d36-170">salida de Hello es similar a la siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="d7d36-170">hello output resembles hello following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
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
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
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
4. <span data-ttu-id="d7d36-171">**Recomendado: Copia de seguridad Hola indizar los datos de Solr tooAzure almacenamiento de blobs asociado con clúster de HDInsight de Hola**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="d7d36-172">Como una buena práctica, debe realizar una copia Hola indizado datos desde los nodos del clúster de Solr hello en almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d36-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="d7d36-173">Lleve a cabo Hola siguiendo los pasos toodo así:</span><span class="sxs-lookup"><span data-stu-id="d7d36-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="d7d36-174">Desde la sesión RDP de hello, abra Internet Explorer y toohello punto después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="d7d36-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="d7d36-175">Debería obtener una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7d36-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="d7d36-176">En la sesión remota de hello, navegue demasiado {SOLR_HOME}\{colección} \data.</span><span class="sxs-lookup"><span data-stu-id="d7d36-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="d7d36-177">Para el clúster de hello creado mediante un script de ejemplo de Hola, debe ser **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="d7d36-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="d7d36-178">En esta ubicación, verá una carpeta de instantáneas que se crea con un nombre similar demasiado**instantánea.* marca de tiempo***.</span><span class="sxs-lookup"><span data-stu-id="d7d36-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="d7d36-179">Comprima la carpeta de instantáneas de Hola y cargarlo en el almacenamiento de blobs de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d7d36-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="d7d36-180">Desde la línea de comandos de Hadoop de hello, navegar toohello ubicación de carpeta de instantáneas de hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d7d36-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="d7d36-181">Este comando copias instantáneas demasiado / / datos de ejemplo de Hola/contenedor hello en predeterminado Hola almacenamiento cuenta asociada con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7d36-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="d7d36-182">Instalación de Solr mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7d36-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="d7d36-183">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="d7d36-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="d7d36-184">ejemplo de Hola se muestra cómo tooinstall Spark con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7d36-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="d7d36-185">Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="d7d36-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="d7d36-186">Instalación de Solr con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="d7d36-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="d7d36-187">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="d7d36-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="d7d36-188">ejemplo de Hola se muestra cómo tooinstall Spark utilizando Hola .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d7d36-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="d7d36-189">Necesita toocustomize Hola script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="d7d36-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="d7d36-190">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d7d36-190">See also</span></span>
* [<span data-ttu-id="d7d36-191">Instalación y uso de Solr en clústeres de Hadoop para HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="d7d36-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="d7d36-192">[Creación de clústeres de Hadoop en HDInsight](hdinsight-provision-clusters.md): información general sobre la creación de clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d7d36-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="d7d36-193">[Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize]: información general sobre la personalización de clústeres de HDInsight mediante la acción de script.</span><span class="sxs-lookup"><span data-stu-id="d7d36-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="d7d36-194">[Desarrollo de acciones de script con HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="d7d36-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="d7d36-195">[Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]: ejemplo de acción de script sobre la instalación de Spark.</span><span class="sxs-lookup"><span data-stu-id="d7d36-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="d7d36-196">[Instalación de R en clústeres de HDInsight][hdinsight-install-r]: ejemplo de acción de script sobre la instalación de R.</span><span class="sxs-lookup"><span data-stu-id="d7d36-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="d7d36-197">[Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md): ejemplo de acción de script sobre la instalación de Giraph.</span><span class="sxs-lookup"><span data-stu-id="d7d36-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
