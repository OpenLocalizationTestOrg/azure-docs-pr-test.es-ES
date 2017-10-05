---
title: "Uso de la acción de script para instalar Solr en HDInsight basado en Linux (Azure) | Microsoft Docs"
description: "Aprenda a instalar Solr en clústeres de Hadoop para HDInsight basados en Linux mediante acciones de script."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: ad930ca023a36fa5874483873c82fdba11d117c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="0570d-103">Instalación y uso de Solr en clústeres de Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="0570d-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="0570d-104">Aprenda a instalar Solr en Azure HDInsight con acción de script.</span><span class="sxs-lookup"><span data-stu-id="0570d-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="0570d-105">Solr es una eficaz plataforma de búsqueda eficaz y proporciona capacidades de búsqueda de nivel empresarial en datos administrados por Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0570d-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="0570d-106">Los pasos descritos en este documento requieren un clúster de HDInsight que use Linux.</span><span class="sxs-lookup"><span data-stu-id="0570d-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="0570d-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="0570d-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0570d-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0570d-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0570d-109">El script de ejemplo usado en este documento instala Solr 4.9 con una configuración concreta.</span><span class="sxs-lookup"><span data-stu-id="0570d-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="0570d-110">Si desea configurar el clúster de Solr con distintas colecciones, particiones, esquemas o réplicas, entre otras, debe modificar el script y los archivos binarios de Solr.</span><span class="sxs-lookup"><span data-stu-id="0570d-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span></span>

## <span data-ttu-id="0570d-111"><a name="whatis"></a>¿Qué es Solr?</span><span class="sxs-lookup"><span data-stu-id="0570d-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="0570d-112">[Apache Solr](http://lucene.apache.org/solr/features.html) es una plataforma de búsqueda empresarial que permite una eficaz búsqueda de texto completo en los datos.</span><span class="sxs-lookup"><span data-stu-id="0570d-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="0570d-113">Si bien Hadoop permite almacenar y administrar grandes cantidades de datos, Apache Solr proporciona las capacidades de búsqueda para recuperar rápidamente los datos.</span><span class="sxs-lookup"><span data-stu-id="0570d-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

> [!WARNING]
> <span data-ttu-id="0570d-114">Los componentes proporcionados con el clúster de HDInsight son totalmente compatibles con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0570d-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="0570d-115">Los componentes personalizados reciben soporte técnico comercialmente razonable para ayudarlo a solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="0570d-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="0570d-116">El soporte técnico de Microsoft puede no ser capaz de resolver problemas con componentes personalizados.</span><span class="sxs-lookup"><span data-stu-id="0570d-116">Microsoft support may not be able to resolve problems with custom components.</span></span> <span data-ttu-id="0570d-117">Debe ponerse en contacto con las comunidades de código abierto para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="0570d-117">You may need to engage the open source communities for assistance.</span></span> <span data-ttu-id="0570d-118">Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="0570d-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="0570d-119">Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="0570d-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-the-script-does"></a><span data-ttu-id="0570d-120">Funcionamiento del script</span><span class="sxs-lookup"><span data-stu-id="0570d-120">What the script does</span></span>

<span data-ttu-id="0570d-121">Este script realiza los siguientes cambios en el clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0570d-121">This script makes the following changes to the HDInsight cluster:</span></span>

* <span data-ttu-id="0570d-122">Instala Solr 4.9 en `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="0570d-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="0570d-123">Crea un usuario, **solruser**, que se usa para ejecutar el servicio Solr</span><span class="sxs-lookup"><span data-stu-id="0570d-123">Creates a user, **solrusr**, which is used to run the Solr service</span></span>
* <span data-ttu-id="0570d-124">Establece **solruser** como propietario de `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="0570d-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="0570d-125">Agrega una configuración [Upstart](http://upstart.ubuntu.com/) que inicia Solr automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0570d-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="0570d-126"><a name="install"></a>Instalación de Solr mediante acciones de script</span><span class="sxs-lookup"><span data-stu-id="0570d-126"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="0570d-127">En la siguiente ubicación se encuentra disponible un script de ejemplo para instalar Solr en un clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0570d-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="0570d-128">Para crear un clúster que tenga Solr instalado, siga los pasos del documento [Creación de clústeres de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0570d-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="0570d-129">Durante el proceso de creación, siga estos pasos para instalar Solr:</span><span class="sxs-lookup"><span data-stu-id="0570d-129">During the creation process, use the following steps to install Solr:</span></span>

1. <span data-ttu-id="0570d-130">En la hoja __Resumen del clúster__, seleccione__Configuración avanzada__ y, después, __Acciones de script__.</span><span class="sxs-lookup"><span data-stu-id="0570d-130">From the __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="0570d-131">Use la siguiente información para rellenar el cuestionario:</span><span class="sxs-lookup"><span data-stu-id="0570d-131">Use the following information to populate the form:</span></span>

   * <span data-ttu-id="0570d-132">**NOMBRE**: escriba un nombre descriptivo para la acción de script.</span><span class="sxs-lookup"><span data-stu-id="0570d-132">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="0570d-133">**URI DE SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="0570d-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="0570d-134">**PRINCIPAL**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="0570d-134">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="0570d-135">**TRABAJADOR**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="0570d-135">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="0570d-136">**ZOOKEEPER**: active esta opción para instalar en el nodo Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="0570d-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span></span>
   * <span data-ttu-id="0570d-137">**PARÁMETROS**: deje este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="0570d-137">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="0570d-138">En la parte inferior de la hoja **Acciones de scripts**, use el botón **Seleccionar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="0570d-138">At the bottom of the **Script actions** blade, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="0570d-139">Por último, use el botón **Siguiente** para regresar a __Resumen del clúster__.</span><span class="sxs-lookup"><span data-stu-id="0570d-139">Finally, use the **Next** button to return to the __Cluster summary__</span></span>

3. <span data-ttu-id="0570d-140">En la página __Resumen del clúster__, seleccione __Crear__ para crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="0570d-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span></span>

## <span data-ttu-id="0570d-141"><a name="usesolr"></a>Cómo usar Solr en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0570d-141"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0570d-142">Los pasos descritos en esta sección muestran la funcionalidad básica de Solr.</span><span class="sxs-lookup"><span data-stu-id="0570d-142">The steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="0570d-143">Para obtener más información sobre el uso de Solr, consulte el sitio de [Solr Apache](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="0570d-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="0570d-144">Datos de índice</span><span class="sxs-lookup"><span data-stu-id="0570d-144">Index data</span></span>

<span data-ttu-id="0570d-145">Use los pasos siguientes para agregar datos de ejemplo a Solr y luego, consúltelo:</span><span class="sxs-lookup"><span data-stu-id="0570d-145">Use the following steps to add example data to Solr, and then query it:</span></span>

1. <span data-ttu-id="0570d-146">Conéctese al clúster de HDInsight con SSH:</span><span class="sxs-lookup"><span data-stu-id="0570d-146">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="0570d-147">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0570d-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="0570d-148">Unos pasos más adelante en este documento, use un túnel SSL para conectarse a la interfaz de usuario web Solr.</span><span class="sxs-lookup"><span data-stu-id="0570d-148">Steps later in this document use an SSL tunnel to connect to the Solr web UI.</span></span> <span data-ttu-id="0570d-149">Para poder seguir estos pasos, tiene que establecer un túnel SSL y, después, configurar el explorador para que lo utilice.</span><span class="sxs-lookup"><span data-stu-id="0570d-149">To use these steps, you must establish an SSL tunnel and then configure your browser to use it.</span></span>
     >
     > <span data-ttu-id="0570d-150">Para obtener más información, vea el documento [Uso de un túnel SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="0570d-150">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="0570d-151">Use los siguientes comandos para tener los datos de ejemplo del índice Solr:</span><span class="sxs-lookup"><span data-stu-id="0570d-151">Use the following commands to have Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="0570d-152">Se devuelve el siguiente resultado a la consola:</span><span class="sxs-lookup"><span data-stu-id="0570d-152">The following output is returned to the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="0570d-153">La utilidad `post.jar` agrega los documentos **solr.xml** y **monitor.xml** al índice.</span><span class="sxs-lookup"><span data-stu-id="0570d-153">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span></span>
  
3. <span data-ttu-id="0570d-154">Use el comando siguiente para consultar a la API de REST de Solr:</span><span class="sxs-lookup"><span data-stu-id="0570d-154">Use the following command to query the Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="0570d-155">Este comando busca en **collection1** los documentos que coinciden con **\*:\*** (codificado como \*%3A\* en la cadena de consulta).</span><span class="sxs-lookup"><span data-stu-id="0570d-155">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span></span> <span data-ttu-id="0570d-156">El documento JSON siguiente es un ejemplo de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="0570d-156">The following JSON document is an example of the response:</span></span>

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

### <a name="using-the-solr-dashboard"></a><span data-ttu-id="0570d-157">Mediante el panel de Solr</span><span class="sxs-lookup"><span data-stu-id="0570d-157">Using the Solr dashboard</span></span>

<span data-ttu-id="0570d-158">El panel de Solr es una interfaz de usuario web que le permite trabajar con Solr mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="0570d-158">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span></span> <span data-ttu-id="0570d-159">El panel de Solr no se expone directamente a Internet desde su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0570d-159">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span></span> <span data-ttu-id="0570d-160">Puede usar un túnel SSH para acceder a él.</span><span class="sxs-lookup"><span data-stu-id="0570d-160">You can use an SSH tunnel to access it.</span></span> <span data-ttu-id="0570d-161">Para obtener más información sobre el uso del túnel SSH, vea el documento [Uso de un túnel SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="0570d-161">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="0570d-162">Una vez establecido un túnel SSH, siga estos pasos para usar el panel de Solr:</span><span class="sxs-lookup"><span data-stu-id="0570d-162">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span></span>

1. <span data-ttu-id="0570d-163">Determine el nombre del host del nodo principal primario:</span><span class="sxs-lookup"><span data-stu-id="0570d-163">Determine the host name for the primary headnode:</span></span>

   1. <span data-ttu-id="0570d-164">Use SSH para conectarse al nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="0570d-164">Use SSH to connect to the cluster head node.</span></span> <span data-ttu-id="0570d-165">Por ejemplo: `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="0570d-165">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="0570d-166">Para obtener más información sobre cómo usar SSH, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0570d-166">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="0570d-167">Use el comando siguiente para obtener el nombre de host completo:</span><span class="sxs-lookup"><span data-stu-id="0570d-167">Use the following command to get the fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="0570d-168">Este comando devuelve un valor similar al nombre del host siguiente:</span><span class="sxs-lookup"><span data-stu-id="0570d-168">This command returns a value similar to the following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="0570d-169">Guarde el valor devuelto porque lo usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="0570d-169">Save the value returned, as it is used later.</span></span>

2. <span data-ttu-id="0570d-170">En el explorador, conéctese a **http://HOSTNAME:8983/solr/#/**, donde **HOSTNAME** es el nombre que determinó en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="0570d-170">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span></span>

    <span data-ttu-id="0570d-171">La solicitud se enruta a través del túnel SSH a la interfaz de usuario de web de Solr en el clúster.</span><span class="sxs-lookup"><span data-stu-id="0570d-171">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span></span> <span data-ttu-id="0570d-172">La página que se muestra es similar a la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="0570d-172">The page appears similar to the following image:</span></span>

    ![Imagen del panel de Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="0570d-174">En el panel izquierdo, use la lista desplegable **Core Selector** (Selector principal) para seleccionar **collection1**.</span><span class="sxs-lookup"><span data-stu-id="0570d-174">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span></span> <span data-ttu-id="0570d-175">Deberían aparecer varias entradas debajo de **collection1**.</span><span class="sxs-lookup"><span data-stu-id="0570d-175">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="0570d-176">Entre las entradas en **collection1**, seleccione **Query** (Consulta).</span><span class="sxs-lookup"><span data-stu-id="0570d-176">From the entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="0570d-177">Use los siguientes valores para rellenar la página de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="0570d-177">Use the following values to populate the search page:</span></span>

   * <span data-ttu-id="0570d-178">En el cuadro de texto **q**, escriba **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="0570d-178">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="0570d-179">Esta consulta devuelve todos los documentos indizados en Solr.</span><span class="sxs-lookup"><span data-stu-id="0570d-179">This query returns all the documents that are indexed in Solr.</span></span> <span data-ttu-id="0570d-180">Si desea buscar una cadena específica dentro de los documentos, puede especificar esa cadena aquí.</span><span class="sxs-lookup"><span data-stu-id="0570d-180">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="0570d-181">En el cuadro de texto **wt** , seleccione el formato de salida.</span><span class="sxs-lookup"><span data-stu-id="0570d-181">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="0570d-182">El valor predeterminado es **json**.</span><span class="sxs-lookup"><span data-stu-id="0570d-182">Default is **json**.</span></span>

     <span data-ttu-id="0570d-183">Por último, seleccione el botón **Ejecutar consulta** que aparece en la parte inferior de la página de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0570d-183">Finally, select the **Execute Query** button at the bottom of the search pate.</span></span>

     ![Uso de la acción de script para personalizar un clúster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="0570d-185">El resultado devuelve los dos documentos que agregó anteriormente al índice.</span><span class="sxs-lookup"><span data-stu-id="0570d-185">The output returns the two documents that you added to the index earlier.</span></span> <span data-ttu-id="0570d-186">El resultado es similar al siguiente documento JSON:</span><span class="sxs-lookup"><span data-stu-id="0570d-186">The output is similar to the following JSON document:</span></span>

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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="0570d-187">Inicio y detención de Solr</span><span class="sxs-lookup"><span data-stu-id="0570d-187">Starting and stopping Solr</span></span>

<span data-ttu-id="0570d-188">Si necesita detener o iniciar Solr manualmente, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="0570d-188">Use the following commands to manually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="0570d-189">Copia de seguridad de los datos indizados</span><span class="sxs-lookup"><span data-stu-id="0570d-189">Backup indexed data</span></span>

<span data-ttu-id="0570d-190">Use los pasos siguientes para realizar copias de seguridad de datos de Solr en el almacenamiento predeterminado del clúster:</span><span class="sxs-lookup"><span data-stu-id="0570d-190">Use the following steps to back up Solr data to the default storage for your cluster:</span></span>

1. <span data-ttu-id="0570d-191">Conéctese al clúster con SSH y, luego, use el comando siguiente para obtener el nombre del host para el nodo principal:</span><span class="sxs-lookup"><span data-stu-id="0570d-191">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="0570d-192">Use el siguiente comando para crear una instantánea de los datos indexados.</span><span class="sxs-lookup"><span data-stu-id="0570d-192">Use the following command to create a snapshot of the indexed data.</span></span> <span data-ttu-id="0570d-193">Reemplace **HOSTNAME** por el nombre que devolvió el comando anterior:</span><span class="sxs-lookup"><span data-stu-id="0570d-193">Replace **HOSTNAME** with the name returned from the previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="0570d-194">La respuesta es similar al siguiente XML:</span><span class="sxs-lookup"><span data-stu-id="0570d-194">The response is similar to the following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="0570d-195">Cambie los directorios a `/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="0570d-195">Change directories to `/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="0570d-196">Hay un subdirectorio aquí para cada colección.</span><span class="sxs-lookup"><span data-stu-id="0570d-196">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="0570d-197">Cada directorio de la colección contiene un directorio `data` que contiene a su vez la instantánea de la colección.</span><span class="sxs-lookup"><span data-stu-id="0570d-197">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span></span>

4. <span data-ttu-id="0570d-198">Para crear un archivo comprimido de la carpeta de instantáneas, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0570d-198">To create a compressed archive of the snapshot folder, use the following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="0570d-199">Sustituya los valores `snapshot.20150806185338855` con el nombre de la instantánea de su colección.</span><span class="sxs-lookup"><span data-stu-id="0570d-199">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span></span>

    <span data-ttu-id="0570d-200">Este comando crea un archivo denominado **snapshot.20150806185338855.tgz**, que incluye el contenido del directorio **snapshot.20150806185338855**.</span><span class="sxs-lookup"><span data-stu-id="0570d-200">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="0570d-201">A continuación, puede almacenar el archivo en el almacenamiento principal del clúster con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0570d-201">You can then store the archive to the cluster's primary storage using the following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="0570d-202">Para más información sobre cómo trabajar con copia de seguridad y restauraciones de Solr, vea [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="0570d-202">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0570d-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0570d-203">Next steps</span></span>

* <span data-ttu-id="0570d-204">[Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0570d-204">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="0570d-205">Use la personalización del clúster para instalar Giraph en clústeres de Hadoop para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0570d-205">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="0570d-206">Giraph permite realizar un procesamiento gráfico mediante Hadoop, y se puede usar con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="0570d-206">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="0570d-207">[Instalación de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0570d-207">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="0570d-208">Use la personalización del clúster para instalar Hue en clústeres de Hadoop para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0570d-208">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="0570d-209">Hue es un conjunto de aplicaciones web que usan para interactuar con un clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0570d-209">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
