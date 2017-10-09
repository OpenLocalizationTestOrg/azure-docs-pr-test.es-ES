---
title: "Acción de secuencia de comandos de aaaUse tooinstall Solr en HDInsight basados en Linux - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar acciones de Script de clústeres de tooinstall Solr en Hadoop de HDInsight basados en Linux."
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
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="0262f-103">Instalación y uso de Solr en clústeres de Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="0262f-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="0262f-104">Obtenga información acerca de cómo tooinstall Solr en HDInsight de Azure mediante la acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="0262f-104">Learn how tooinstall Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="0262f-105">Solr es una eficaz plataforma de búsqueda eficaz y proporciona capacidades de búsqueda de nivel empresarial en datos administrados por Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0262f-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="0262f-106">pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="0262f-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="0262f-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="0262f-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0262f-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0262f-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0262f-109">script de ejemplo de Hola usado en este documento instala Solr 4.9 con una configuración concreta.</span><span class="sxs-lookup"><span data-stu-id="0262f-109">hello sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="0262f-110">Si desea que el clúster de Solr tooconfigure Hola con diferentes recopilaciones, particiones, esquemas, las réplicas, etc., debe modificar el script de Hola y archivos binarios de Solr.</span><span class="sxs-lookup"><span data-stu-id="0262f-110">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries.</span></span>

## <span data-ttu-id="0262f-111"><a name="whatis"></a>¿Qué es Solr?</span><span class="sxs-lookup"><span data-stu-id="0262f-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="0262f-112">[Apache Solr](http://lucene.apache.org/solr/features.html) es una plataforma de búsqueda empresarial que permite una eficaz búsqueda de texto completo en los datos.</span><span class="sxs-lookup"><span data-stu-id="0262f-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="0262f-113">Mientras Hadoop permite almacenar y administrar grandes cantidades de datos, Apache Solr proporciona capacidades de búsqueda de hello tooquickly recuperar datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0262f-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

> [!WARNING]
> <span data-ttu-id="0262f-114">Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0262f-114">Components provided with hello HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="0262f-115">Componentes personalizados, como Solr, reciban soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="0262f-115">Custom components, such as Solr, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="0262f-116">Soporte técnico de Microsoft puede no ser capaz de tooresolve problemas con componentes personalizados.</span><span class="sxs-lookup"><span data-stu-id="0262f-116">Microsoft support may not be able tooresolve problems with custom components.</span></span> <span data-ttu-id="0262f-117">Puede que tenga las Comunidades de código abierto de hello tooengage para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="0262f-117">You may need tooengage hello open source communities for assistance.</span></span> <span data-ttu-id="0262f-118">Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="0262f-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-hello-script-does"></a><span data-ttu-id="0262f-119">El script de Hola hace</span><span class="sxs-lookup"><span data-stu-id="0262f-119">What hello script does</span></span>

<span data-ttu-id="0262f-120">Este script realiza Hola después de clúster de HDInsight de toohello de cambios:</span><span class="sxs-lookup"><span data-stu-id="0262f-120">This script makes hello following changes toohello HDInsight cluster:</span></span>

* <span data-ttu-id="0262f-121">Instala Solr 4.9 en `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="0262f-121">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="0262f-122">Crea un usuario, **solrusr**, que es usado toorun hello Solr servicio</span><span class="sxs-lookup"><span data-stu-id="0262f-122">Creates a user, **solrusr**, which is used toorun hello Solr service</span></span>
* <span data-ttu-id="0262f-123">Conjuntos de **solruser** como propietario de Hola de`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="0262f-123">Sets **solruser** as hello owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="0262f-124">Agrega una configuración [Upstart](http://upstart.ubuntu.com/) que inicia Solr automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0262f-124">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="0262f-125"><a name="install"></a>Instalación de Solr mediante acciones de script</span><span class="sxs-lookup"><span data-stu-id="0262f-125"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="0262f-126">Tooinstall de secuencia de comandos de ejemplo Solr en un clúster de HDInsight está disponible en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="0262f-126">A sample script tooinstall Solr on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="0262f-127">toocreate un clúster que tenga instalado el Solr, Hola de uso de los pasos de hello [HDInsight crear clústeres](hdinsight-hadoop-create-linux-clusters-portal.md) documento.</span><span class="sxs-lookup"><span data-stu-id="0262f-127">toocreate a cluster that has Solr installed, use hello steps in hello [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="0262f-128">Durante el proceso de creación de hello, utilice Hola siguiendo los pasos tooinstall Solr:</span><span class="sxs-lookup"><span data-stu-id="0262f-128">During hello creation process, use hello following steps tooinstall Solr:</span></span>

1. <span data-ttu-id="0262f-129">De hello __resumen de clúster__ hoja, settings__ select__Advanced, a continuación, __acciones de Script__.</span><span class="sxs-lookup"><span data-stu-id="0262f-129">From hello __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="0262f-130">Usar hello después de formulario de información de Hola toopopulate:</span><span class="sxs-lookup"><span data-stu-id="0262f-130">Use hello following information toopopulate hello form:</span></span>

   * <span data-ttu-id="0262f-131">**NOMBRE**: escriba un nombre descriptivo para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0262f-131">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="0262f-132">**URI DE SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="0262f-132">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="0262f-133">**PRINCIPAL**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="0262f-133">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="0262f-134">**TRABAJADOR**: active esta opción.</span><span class="sxs-lookup"><span data-stu-id="0262f-134">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="0262f-135">**ZOOKEEPER**: comprobar este tooinstall opción en el nodo de hello Zookeeper</span><span class="sxs-lookup"><span data-stu-id="0262f-135">**ZOOKEEPER**: Check this option tooinstall on hello Zookeeper node</span></span>
   * <span data-ttu-id="0262f-136">**PARÁMETROS**: deje este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="0262f-136">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="0262f-137">En parte inferior de Hola de hello **acciones de Script** hoja, use hello **seleccione** configuración del botón toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="0262f-137">At hello bottom of hello **Script actions** blade, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="0262f-138">Por último, utilice hello **siguiente** botón tooreturn toohello __resumen de clúster__</span><span class="sxs-lookup"><span data-stu-id="0262f-138">Finally, use hello **Next** button tooreturn toohello __Cluster summary__</span></span>

3. <span data-ttu-id="0262f-139">De hello __resumen de clúster__ página, seleccione __crear__ clúster de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0262f-139">From hello __Cluster summary__ page, select __Create__ toocreate hello cluster.</span></span>

## <span data-ttu-id="0262f-140"><a name="usesolr"></a>Cómo usar Solr en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0262f-140"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0262f-141">pasos de Hello en esta sección demuestran la funcionalidad básica de Solr.</span><span class="sxs-lookup"><span data-stu-id="0262f-141">hello steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="0262f-142">Para obtener más información sobre cómo usar Solr, vea hello [Solr Apache sitio](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="0262f-142">For more information on using Solr, see hello [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="0262f-143">Datos de índice</span><span class="sxs-lookup"><span data-stu-id="0262f-143">Index data</span></span>

<span data-ttu-id="0262f-144">Usar hello siguiendo los pasos tooadd ejemplo datos tooSolr y, a continuación, realizar consultas sobre él:</span><span class="sxs-lookup"><span data-stu-id="0262f-144">Use hello following steps tooadd example data tooSolr, and then query it:</span></span>

1. <span data-ttu-id="0262f-145">Conecte el clúster de HDInsight de toohello mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="0262f-145">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="0262f-146">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0262f-146">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="0262f-147">Pasos más adelante en este documento utiliza un SSL túnel tooconnect toohello Solr interfaz de usuario web.</span><span class="sxs-lookup"><span data-stu-id="0262f-147">Steps later in this document use an SSL tunnel tooconnect toohello Solr web UI.</span></span> <span data-ttu-id="0262f-148">toouse estos pasos, debe establecer una SSL de túnel y, a continuación, configurar su explorador toouse lo.</span><span class="sxs-lookup"><span data-stu-id="0262f-148">toouse these steps, you must establish an SSL tunnel and then configure your browser toouse it.</span></span>
     >
     > <span data-ttu-id="0262f-149">Para obtener más información, vea hello [uso SSH túnel con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="0262f-149">For more information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="0262f-150">Usar hello después de datos de ejemplo de comandos toohave Solr índice:</span><span class="sxs-lookup"><span data-stu-id="0262f-150">Use hello following commands toohave Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="0262f-151">Hello siguiente resultado se devuelve toohello consola:</span><span class="sxs-lookup"><span data-stu-id="0262f-151">hello following output is returned toohello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="0262f-152">Hola `post.jar` utilidad agrega hello **solr.xml** y **monitor.xml** índice toohello de documentos.</span><span class="sxs-lookup"><span data-stu-id="0262f-152">hello `post.jar` utility adds hello **solr.xml** and **monitor.xml** documents toohello index.</span></span>
  
3. <span data-ttu-id="0262f-153">Usar hello después comando tooquery hello Solr API de REST:</span><span class="sxs-lookup"><span data-stu-id="0262f-153">Use hello following command tooquery hello Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="0262f-154">Este comando busca **collection1** para los documentos que coinciden con  **\*:\***  (codificado como \*% 3A\* en la cadena de consulta de hello).</span><span class="sxs-lookup"><span data-stu-id="0262f-154">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in hello query string).</span></span> <span data-ttu-id="0262f-155">Hola siguiendo el documento JSON es un ejemplo de Hola respuesta:</span><span class="sxs-lookup"><span data-stu-id="0262f-155">hello following JSON document is an example of hello response:</span></span>

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

### <a name="using-hello-solr-dashboard"></a><span data-ttu-id="0262f-156">Con hello Solr panel</span><span class="sxs-lookup"><span data-stu-id="0262f-156">Using hello Solr dashboard</span></span>

<span data-ttu-id="0262f-157">panel de Hello Solr es una interfaz de usuario que le permite toowork con Solr a través del explorador web de web.</span><span class="sxs-lookup"><span data-stu-id="0262f-157">hello Solr dashboard is a web UI that allows you toowork with Solr through your web browser.</span></span> <span data-ttu-id="0262f-158">panel de Hello Solr no se expone directamente en hello Internet desde el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0262f-158">hello Solr dashboard is not exposed directly on hello Internet from your HDInsight cluster.</span></span> <span data-ttu-id="0262f-159">Puede usar un tooaccess de túnel SSH se.</span><span class="sxs-lookup"><span data-stu-id="0262f-159">You can use an SSH tunnel tooaccess it.</span></span> <span data-ttu-id="0262f-160">Para obtener más información sobre el uso de un túnel SSH, vea hello [uso SSH túnel con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="0262f-160">For more information on using an SSH tunnel, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="0262f-161">Una vez que haya establecido un túnel SSH, use Hola siguiente panel de pasos toouse Hola Solr:</span><span class="sxs-lookup"><span data-stu-id="0262f-161">Once you have established an SSH tunnel, use hello following steps toouse hello Solr dashboard:</span></span>

1. <span data-ttu-id="0262f-162">Determinar el nombre de host de hello para el nodo principal de hello principal:</span><span class="sxs-lookup"><span data-stu-id="0262f-162">Determine hello host name for hello primary headnode:</span></span>

   1. <span data-ttu-id="0262f-163">Utilice el nodo principal del clúster de toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="0262f-163">Use SSH tooconnect toohello cluster head node.</span></span> <span data-ttu-id="0262f-164">Por ejemplo: `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="0262f-164">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="0262f-165">Para obtener más información sobre el uso de SSH, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0262f-165">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="0262f-166">Usar hello siguiente comando tooget Hola nombre de host completo:</span><span class="sxs-lookup"><span data-stu-id="0262f-166">Use hello following command tooget hello fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="0262f-167">Este comando devuelve un toohello similar valor después de nombre de host:</span><span class="sxs-lookup"><span data-stu-id="0262f-167">This command returns a value similar toohello following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="0262f-168">Guardar valor Hola devuelve, tal como se utiliza más adelante.</span><span class="sxs-lookup"><span data-stu-id="0262f-168">Save hello value returned, as it is used later.</span></span>

2. <span data-ttu-id="0262f-169">En el explorador, conéctese demasiado**http://HOSTNAME:8983/solr / #/**, donde **HOSTNAME** es nombre hello que determinó en pasos anteriores Hola.</span><span class="sxs-lookup"><span data-stu-id="0262f-169">In your browser, connect too**http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is hello name you determined in hello previous steps.</span></span>

    <span data-ttu-id="0262f-170">solicitud de saludo se enruta a través de hello SSH túnel toohello Solr interfaz de usuario web en el clúster.</span><span class="sxs-lookup"><span data-stu-id="0262f-170">hello request is routed through hello SSH tunnel toohello Solr web UI on your cluster.</span></span> <span data-ttu-id="0262f-171">página de Hello aparece toohello similar después de imagen:</span><span class="sxs-lookup"><span data-stu-id="0262f-171">hello page appears similar toohello following image:</span></span>

    ![Imagen del panel de Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="0262f-173">Desde el panel izquierdo de hello, use hello **Core Selector** desplegable tooselect **collection1**.</span><span class="sxs-lookup"><span data-stu-id="0262f-173">From hello left pane, use hello **Core Selector** drop-down tooselect **collection1**.</span></span> <span data-ttu-id="0262f-174">Deberían aparecer varias entradas debajo de **collection1**.</span><span class="sxs-lookup"><span data-stu-id="0262f-174">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="0262f-175">En las entradas de hello debajo de **collection1**, seleccione **consulta**.</span><span class="sxs-lookup"><span data-stu-id="0262f-175">From hello entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="0262f-176">Usar hello después de la página de búsqueda de valores toopopulate hello:</span><span class="sxs-lookup"><span data-stu-id="0262f-176">Use hello following values toopopulate hello search page:</span></span>

   * <span data-ttu-id="0262f-177">Hola **preguntas** texto cuadro, escriba  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="0262f-177">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="0262f-178">Esta consulta devuelve todos los documentos de Hola que están indizados en Solr.</span><span class="sxs-lookup"><span data-stu-id="0262f-178">This query returns all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="0262f-179">Si desea toosearch una cadena específica dentro de los documentos de hello, puede especificar esa cadena aquí.</span><span class="sxs-lookup"><span data-stu-id="0262f-179">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="0262f-180">Hola **wt** cuadro de texto, formato de salida de hello select.</span><span class="sxs-lookup"><span data-stu-id="0262f-180">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="0262f-181">El valor predeterminado es **json**.</span><span class="sxs-lookup"><span data-stu-id="0262f-181">Default is **json**.</span></span>

     <span data-ttu-id="0262f-182">Por último, seleccione hello **Ejecutar consulta** situado en parte inferior de Hola de y patentes de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="0262f-182">Finally, select hello **Execute Query** button at hello bottom of hello search pate.</span></span>

     ![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="0262f-184">salida de Hello devuelve Hola dos documentos que ha agregado toohello índice anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0262f-184">hello output returns hello two documents that you added toohello index earlier.</span></span> <span data-ttu-id="0262f-185">Hola de salida es similar toohello posterior documento JSON:</span><span class="sxs-lookup"><span data-stu-id="0262f-185">hello output is similar toohello following JSON document:</span></span>

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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="0262f-186">Inicio y detención de Solr</span><span class="sxs-lookup"><span data-stu-id="0262f-186">Starting and stopping Solr</span></span>

<span data-ttu-id="0262f-187">Usar hello siga los comandos toomanually detener e iniciar Solr:</span><span class="sxs-lookup"><span data-stu-id="0262f-187">Use hello following commands toomanually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="0262f-188">Copia de seguridad de los datos indizados</span><span class="sxs-lookup"><span data-stu-id="0262f-188">Backup indexed data</span></span>

<span data-ttu-id="0262f-189">Usar hello siguiendo los pasos tooback el almacenamiento de Solr datos toohello predeterminado para el clúster:</span><span class="sxs-lookup"><span data-stu-id="0262f-189">Use hello following steps tooback up Solr data toohello default storage for your cluster:</span></span>

1. <span data-ttu-id="0262f-190">Conectar el clúster toohello mediante SSH, utilice Hola después de nombre de host de comando tooget hello para el nodo principal de hello:</span><span class="sxs-lookup"><span data-stu-id="0262f-190">Connect toohello cluster using SSH, then use hello following command tooget hello host name for hello head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="0262f-191">Usar hello después comando toocreate una instantánea de hello indizado datos.</span><span class="sxs-lookup"><span data-stu-id="0262f-191">Use hello following command toocreate a snapshot of hello indexed data.</span></span> <span data-ttu-id="0262f-192">Reemplace **HOSTNAME** con nombre hello devuelto por el comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="0262f-192">Replace **HOSTNAME** with hello name returned from hello previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="0262f-193">respuesta de Hello es similar toohello continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="0262f-193">hello response is similar toohello following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="0262f-194">Cambie los directorios demasiado`/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="0262f-194">Change directories too`/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="0262f-195">Hay un subdirectorio aquí para cada colección.</span><span class="sxs-lookup"><span data-stu-id="0262f-195">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="0262f-196">Cada directorio de la colección contiene un `data` directorio que contiene la instantánea de hello para la recopilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0262f-196">Each collection directory contains a `data` directory that contains hello snapshot for hello collection.</span></span>

4. <span data-ttu-id="0262f-197">toocreate un archivo comprimido de la carpeta de instantáneas Hola Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0262f-197">toocreate a compressed archive of hello snapshot folder, use hello following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="0262f-198">Reemplace hello `snapshot.20150806185338855` valores con el nombre de Hola de instantánea de hello para la colección.</span><span class="sxs-lookup"><span data-stu-id="0262f-198">Replace hello `snapshot.20150806185338855` values with hello name of hello snapshot for your collection.</span></span>

    <span data-ttu-id="0262f-199">Este comando crea un archivo denominado **snapshot.20150806185338855.tgz**, que contiene el contenido de Hola de hello **snapshot.20150806185338855** directory.</span><span class="sxs-lookup"><span data-stu-id="0262f-199">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains hello contents of hello **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="0262f-200">A continuación, puede almacenar almacenamiento principal del clúster de hello archivo toohello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0262f-200">You can then store hello archive toohello cluster's primary storage using hello following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="0262f-201">Para más información sobre cómo trabajar con copia de seguridad y restauraciones de Solr, vea [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="0262f-201">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0262f-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0262f-202">Next steps</span></span>

* <span data-ttu-id="0262f-203">[Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0262f-203">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="0262f-204">Utilice tooinstall de personalización de clúster de clústeres de Giraph en Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0262f-204">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="0262f-205">Giraph permite gráfico tooperform procesamiento por medio de Hadoop y puede utilizarse con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="0262f-205">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="0262f-206">[Instalación de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0262f-206">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="0262f-207">Utilice matiz de tooinstall de personalización de clúster en clústeres de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0262f-207">Use cluster customization tooinstall Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="0262f-208">El matiz es que un conjunto de aplicaciones Web utiliza toointeract con un clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0262f-208">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
