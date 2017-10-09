---
title: aaaGet a trabajar con un ejemplo de HBase en HDInsight - Azure | Documentos de Microsoft
description: Siga este toostart de ejemplo de Apache HBase con hadoop en HDInsight. Crear tablas de hello shell de HBase y consultarlos con Hive.
keywords: hbasecommand, ejemplo de hbase
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="aea5b-105">Introducción a un ejemplo de Apache HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="aea5b-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="aea5b-106">Obtenga información acerca de cómo crear tablas de HBase toocreate un clúster de HBase en HDInsight y consultar tablas mediante el uso de Hive.</span><span class="sxs-lookup"><span data-stu-id="aea5b-106">Learn how toocreate an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="aea5b-107">Para obtener información general de HBase, consulte [Información general de HBase de HDInsight][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="aea5b-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="aea5b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aea5b-108">Prerequisites</span></span>
<span data-ttu-id="aea5b-109">Antes de intentar este ejemplo de HBase, debe tener Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="aea5b-109">Before you begin trying this HBase example, you must have hello following items:</span></span>

* <span data-ttu-id="aea5b-110">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="aea5b-110">**An Azure subscription**.</span></span> <span data-ttu-id="aea5b-111">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="aea5b-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="aea5b-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aea5b-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="aea5b-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="aea5b-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="aea5b-114">Creación del clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="aea5b-114">Create HBase cluster</span></span>
<span data-ttu-id="aea5b-115">Hello siguiente procedimiento usa un toocreate de plantilla de Azure Resource Manager un versión 3.4 basados en Linux HBase hello y clúster dependientes almacenamiento de Azure cuenta predeterminada.</span><span class="sxs-lookup"><span data-stu-id="aea5b-115">hello following procedure uses an Azure Resource Manager template toocreate a version 3.4 Linux-based HBase cluster and hello dependent default Azure Storage account.</span></span> <span data-ttu-id="aea5b-116">parámetros de hello toounderstand utilizados en el procedimiento de Hola y otros métodos de creación del clúster, consulte [clústeres basados en Linux crear Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="aea5b-116">toounderstand hello parameters used in hello procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="aea5b-117">Haga clic en hello después de la plantilla de imagen tooopen Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="aea5b-117">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="aea5b-118">plantilla de Hola se encuentra en un contenedor de blobs públicos.</span><span class="sxs-lookup"><span data-stu-id="aea5b-118">hello template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="aea5b-119">De hello **implementación personalizada** hoja, escriba Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="aea5b-119">From hello **Custom deployment** blade, enter hello following values:</span></span>
   
   * <span data-ttu-id="aea5b-120">**Suscripción**: seleccione la suscripción de Azure que es usado toocreate Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="aea5b-120">**Subscription**: Select your Azure subscription that is used toocreate hello cluster.</span></span>
   * <span data-ttu-id="aea5b-121">**Grupo de recursos**: cree un grupo de administración de recursos de Azure o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="aea5b-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="aea5b-122">**Ubicación**: especificar ubicación de Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aea5b-122">**Location**: Specify hello location of hello resource group.</span></span> 
   * <span data-ttu-id="aea5b-123">**ClusterName**: escriba un nombre para el clúster de HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-123">**ClusterName**: Enter a name for hello HBase cluster.</span></span>
   * <span data-ttu-id="aea5b-124">**Nombre de inicio de sesión y la contraseña del clúster**: nombre de inicio de sesión predeterminado de hello es **administración**.</span><span class="sxs-lookup"><span data-stu-id="aea5b-124">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="aea5b-125">**SSH username y password**: nombre de usuario de hello predeterminada es **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="aea5b-125">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="aea5b-126">Puede cambiarlo.</span><span class="sxs-lookup"><span data-stu-id="aea5b-126">You can rename it.</span></span>
     
     <span data-ttu-id="aea5b-127">Otros parámetros son opcionales.</span><span class="sxs-lookup"><span data-stu-id="aea5b-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="aea5b-128">Cada clúster tiene una dependencia de cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="aea5b-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="aea5b-129">Después de eliminar un clúster, datos de Hola se conservan en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-129">After you delete a cluster, hello data retains in hello storage account.</span></span> <span data-ttu-id="aea5b-130">nombre de cuenta de almacenamiento de Hello clúster predeterminado es el nombre de clúster de hello con "almacén" anexado.</span><span class="sxs-lookup"><span data-stu-id="aea5b-130">hello cluster default storage account name is hello cluster name with "store" appended.</span></span> <span data-ttu-id="aea5b-131">Está codificada en la sección de las variables de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-131">It is hardcoded in hello template variables section.</span></span>
3. <span data-ttu-id="aea5b-132">Seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**y, a continuación, haga clic en **compra**.</span><span class="sxs-lookup"><span data-stu-id="aea5b-132">Select **I agree toohello terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="aea5b-133">Tarda aproximadamente 20 minutos toocreate un clúster.</span><span class="sxs-lookup"><span data-stu-id="aea5b-133">It takes about 20 minutes toocreate a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="aea5b-134">Después de elimina un clúster de HBase, puede crear otro clúster de HBase mediante Hola mismo contenedor de blob de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="aea5b-134">After an HBase cluster is deleted, you can create another HBase cluster by using hello same default blob container.</span></span> <span data-ttu-id="aea5b-135">nuevo clúster de Hello recoge las tablas de HBase Hola que creó en el clúster de hello original.</span><span class="sxs-lookup"><span data-stu-id="aea5b-135">hello new cluster picks up hello HBase tables you created in hello original cluster.</span></span> <span data-ttu-id="aea5b-136">tooavoid incoherencias, se recomienda deshabilitar las tablas de hello HBase antes de eliminar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-136">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="aea5b-137">Creación de tablas e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="aea5b-137">Create tables and insert data</span></span>
<span data-ttu-id="aea5b-138">Puede utilizar SSH tooconnect tooHBase clústeres y, a continuación, usar las tablas de Shell de HBase toocreate HBase, insertar datos y consultar datos.</span><span class="sxs-lookup"><span data-stu-id="aea5b-138">You can use SSH tooconnect tooHBase clusters and then use HBase Shell toocreate HBase tables, insert data, and query data.</span></span> <span data-ttu-id="aea5b-139">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aea5b-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="aea5b-140">Para la mayoría de los usuarios, los datos aparecen en formato tabular hello:</span><span class="sxs-lookup"><span data-stu-id="aea5b-140">For most people, data appears in hello tabular format:</span></span>

![Datos tabulares de HBase de HDInsight][img-hbase-sample-data-tabular]

<span data-ttu-id="aea5b-142">En HBase (una implementación de BigTable), hello mismo datos aspecto:</span><span class="sxs-lookup"><span data-stu-id="aea5b-142">In HBase (an implementation of BigTable), hello same data looks like:</span></span>

![Datos de HDInsight HBase BigTable][img-hbase-sample-data-bigtable]


<span data-ttu-id="aea5b-144">**Hola toouse shell de HBase**</span><span class="sxs-lookup"><span data-stu-id="aea5b-144">**toouse hello HBase shell**</span></span>

1. <span data-ttu-id="aea5b-145">De SSH, ejecute hello siguiente comando de HBase:</span><span class="sxs-lookup"><span data-stu-id="aea5b-145">From SSH, run hello following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="aea5b-146">Cree una tabla HBase con dos familias de columnas:</span><span class="sxs-lookup"><span data-stu-id="aea5b-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="aea5b-147">Inserte algunos datos:</span><span class="sxs-lookup"><span data-stu-id="aea5b-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Shell de HDInsight Hadoop HBase][img-hbase-shell]
4. <span data-ttu-id="aea5b-149">Obtenga una sola fila</span><span class="sxs-lookup"><span data-stu-id="aea5b-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="aea5b-150">Verá Hola mismo da como resultado como mediante el comando de examen de hello porque no hay una sola fila.</span><span class="sxs-lookup"><span data-stu-id="aea5b-150">You shall see hello same results as using hello scan command because there is only one row.</span></span>
   
    <span data-ttu-id="aea5b-151">Para obtener más información acerca del esquema de tabla HBase hello, consulte [Introducción tooHBase diseño de esquema][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="aea5b-151">For more information about hello HBase table schema, see [Introduction tooHBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="aea5b-152">Para ver más comandos de HBase, consulte [Guía de referencia de Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="aea5b-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="aea5b-153">Shell de Hola de salida</span><span class="sxs-lookup"><span data-stu-id="aea5b-153">Exit hello shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="aea5b-154">**toobulk carga datos en la tabla de hello contactos HBase**</span><span class="sxs-lookup"><span data-stu-id="aea5b-154">**toobulk load data into hello contacts HBase table**</span></span>

<span data-ttu-id="aea5b-155">HBase incluye varios métodos de carga de datos en las tablas.</span><span class="sxs-lookup"><span data-stu-id="aea5b-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="aea5b-156">Para obtener más información, vea [Carga masiva](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="aea5b-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="aea5b-157">Se puede encontrar un archivo de datos de ejemplo en un contenedor de blobs público, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="aea5b-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="aea5b-158">contenido de Hola Hola del archivo de datos es:</span><span class="sxs-lookup"><span data-stu-id="aea5b-158">hello content of hello data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="aea5b-159">Si lo desea puede crear un archivo de texto y cargar la cuenta de almacenamiento propios de hello archivos tooyour.</span><span class="sxs-lookup"><span data-stu-id="aea5b-159">You can optionally create a text file and upload hello file tooyour own storage account.</span></span> <span data-ttu-id="aea5b-160">Para obtener instrucciones de hello, consulte [cargar datos para los trabajos de Hadoop en HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="aea5b-160">For hello instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="aea5b-161">Este procedimiento utiliza la tabla de HBase contactos de Hola que ha creado en el último procedimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-161">This procedure uses hello Contacts HBase table you have created in hello last procedure.</span></span>
> 

1. <span data-ttu-id="aea5b-162">Desde SSH, ejecute hello después comando tootransform hello tooStoreFiles de archivos de datos y almacenar en una ruta de acceso relativa especificado por Dimporttsv.bulk.output.</span><span class="sxs-lookup"><span data-stu-id="aea5b-162">From SSH, run hello following command tootransform hello data file tooStoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="aea5b-163">Si está en el Shell de HBase, utilice tooexit de comandos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="aea5b-163">If you are in HBase Shell, use hello exit command tooexit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="aea5b-164">Ejecute hello siguientes datos de saludo de comando tooupload de /example/data/storeDataFileOutput toohello HBase tabla:</span><span class="sxs-lookup"><span data-stu-id="aea5b-164">Run hello following command tooupload hello data from  /example/data/storeDataFileOutput toohello HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="aea5b-165">Puede abrir Hola shell de HBase y utilizar contenido de la tabla de hello examen comando toolist Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-165">You can open hello HBase shell, and use hello scan command toolist hello table content.</span></span>

## <a name="use-hive-tooquery-hbase"></a><span data-ttu-id="aea5b-166">Usar Hive tooquery HBase</span><span class="sxs-lookup"><span data-stu-id="aea5b-166">Use Hive tooquery HBase</span></span>

<span data-ttu-id="aea5b-167">Puede consultar datos en tablas de HBase mediante el uso de Hive.</span><span class="sxs-lookup"><span data-stu-id="aea5b-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="aea5b-168">En esta sección, se crea una tabla de Hive que asigna la tabla de HBase toohello y utiliza datos de hello tooquery en la tabla HBase.</span><span class="sxs-lookup"><span data-stu-id="aea5b-168">In this section, you create a Hive table that maps toohello HBase table and uses it tooquery hello data in your HBase table.</span></span>

1. <span data-ttu-id="aea5b-169">Abra **PuTTY**y conecta el clúster de toohello.</span><span class="sxs-lookup"><span data-stu-id="aea5b-169">Open **PuTTY**, and connect toohello cluster.</span></span>  <span data-ttu-id="aea5b-170">Consulte las instrucciones de hello en el procedimiento anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-170">See hello instructions in hello previous procedure.</span></span>
2. <span data-ttu-id="aea5b-171">Desde la sesión de SSH de hello, utilice Hola después comando toostart Beeline:</span><span class="sxs-lookup"><span data-stu-id="aea5b-171">From hello SSH session, use hello following command toostart Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="aea5b-172">Para más información sobre Beeline, consulte [Uso de Hive con Hadoop en HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="aea5b-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="aea5b-173">Ejecute hello después toocreate de script de HiveQL una tabla de Hive que se asigna la tabla de HBase toohello.</span><span class="sxs-lookup"><span data-stu-id="aea5b-173">Run hello following HiveQL script  toocreate a Hive table that maps toohello HBase table.</span></span> <span data-ttu-id="aea5b-174">Asegúrese de que ha creado la tabla de ejemplo de Hola mencionada anteriormente en este tutorial mediante shell de HBase de hello antes de ejecutar esta instrucción.</span><span class="sxs-lookup"><span data-stu-id="aea5b-174">Make sure that you have created hello sample table referenced earlier in this tutorial by using hello HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="aea5b-175">Ejecute hello HiveQL script tooquery Hola datos en la tabla de HBase Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="aea5b-175">Run hello following HiveQL script tooquery hello data in hello HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="aea5b-176">Usar las API de REST de HBase con Curl</span><span class="sxs-lookup"><span data-stu-id="aea5b-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="aea5b-177">API de REST de Hello se protege una a través de [la autenticación básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="aea5b-177">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="aea5b-178">Siempre deben realizar solicitudes mediante el uso de HTTP seguro (HTTPS) toohelp Asegúrese de que sus credenciales se envían de forma segura toohello server.</span><span class="sxs-lookup"><span data-stu-id="aea5b-178">You shall always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>

2. <span data-ttu-id="aea5b-179">Usar hello las tablas existentes de HBase de comando toolist Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="aea5b-179">Use hello following command toolist hello existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="aea5b-180">Usar hello después comando toocreate una nueva tabla de HBase con las familias de dos columnas:</span><span class="sxs-lookup"><span data-stu-id="aea5b-180">Use hello following command toocreate a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="aea5b-181">esquema de Hola se proporciona en formato JSon de Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-181">hello schema is provided in hello JSon format.</span></span>
4. <span data-ttu-id="aea5b-182">Usar hello después comando tooinsert algunos datos:</span><span class="sxs-lookup"><span data-stu-id="aea5b-182">Use hello following command tooinsert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="aea5b-183">Debe base64 codificar valores de hello especificados en la instrucción switch -d de Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-183">You must base64 encode hello values specified in hello -d switch.</span></span> <span data-ttu-id="aea5b-184">En el ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="aea5b-184">In hello example:</span></span>
   
   * <span data-ttu-id="aea5b-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="aea5b-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="aea5b-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="aea5b-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="aea5b-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="aea5b-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="aea5b-188">[clave de fila false](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) permite tooinsert varios valores (por lotes).</span><span class="sxs-lookup"><span data-stu-id="aea5b-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you tooinsert multiple (batched) values.</span></span>
5. <span data-ttu-id="aea5b-189">Usar hello después de una fila del comando tooget:</span><span class="sxs-lookup"><span data-stu-id="aea5b-189">Use hello following command tooget a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="aea5b-190">Para más información sobre Rest de HBase, consulte la [guía de referencia de Apache HBase](https://hbase.apache.org/book.html#_rest).</span><span class="sxs-lookup"><span data-stu-id="aea5b-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="aea5b-191">Thrift no es compatible con HBase en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aea5b-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="aea5b-192">Al usar Curl o cualquier otro tipo de comunicación REST con WebHCat, debe autenticar solicitudes de hello proporcionando el nombre de usuario de Hola y la contraseña de administrador de clústeres de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-192">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="aea5b-193">También debe utilizar el nombre del clúster de hello como parte del identificador uniforme de recursos (URI) de Hola utiliza servidor toohello de toosend Hola solicitudes:</span><span class="sxs-lookup"><span data-stu-id="aea5b-193">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="aea5b-194">Debería recibir un toohello similar de respuesta después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="aea5b-194">You should receive a response similar toohello following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="aea5b-195">Comprobar el estado del clúster</span><span class="sxs-lookup"><span data-stu-id="aea5b-195">Check cluster status</span></span>
<span data-ttu-id="aea5b-196">HBase en HDInsight se incluye con una interfaz de usuario web para la supervisión de clústeres.</span><span class="sxs-lookup"><span data-stu-id="aea5b-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="aea5b-197">Hola UI Web puede solicitar las estadísticas o información acerca de las regiones.</span><span class="sxs-lookup"><span data-stu-id="aea5b-197">Using hello Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="aea5b-198">**Hola tooaccess UI Master HBase**</span><span class="sxs-lookup"><span data-stu-id="aea5b-198">**tooaccess hello HBase Master UI**</span></span>

1. <span data-ttu-id="aea5b-199">Inicio de sesión en Hola Hola Ambari Web UI en https://&lt;Clustername >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="aea5b-199">Sign into hello hello Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="aea5b-200">Haga clic en **HBase** desde el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-200">Click **HBase** from hello left menu.</span></span>
3. <span data-ttu-id="aea5b-201">Haga clic en **vínculos rápidos** Hola parte superior de la página hello, vínculo de nodo de Zookeeper activo toohello de punto y, a continuación, haga clic en **HBase Master UI**.</span><span class="sxs-lookup"><span data-stu-id="aea5b-201">Click **Quick links** on hello top of hello page, point toohello active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="aea5b-202">Hola interfaz de usuario se abre en otra ficha del explorador:</span><span class="sxs-lookup"><span data-stu-id="aea5b-202">hello UI is opened in another browser tab:</span></span>

  ![Interfaz de usuario maestra de HBase de HDInsight](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="aea5b-204">Hola HBase Master UI contiene Hola siguientes secciones:</span><span class="sxs-lookup"><span data-stu-id="aea5b-204">hello HBase Master UI contains hello following sections:</span></span>

  - <span data-ttu-id="aea5b-205">servidores regionales</span><span class="sxs-lookup"><span data-stu-id="aea5b-205">region servers</span></span>
  - <span data-ttu-id="aea5b-206">maestros de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="aea5b-206">backup masters</span></span>
  - <span data-ttu-id="aea5b-207">tables</span><span class="sxs-lookup"><span data-stu-id="aea5b-207">tables</span></span>
  - <span data-ttu-id="aea5b-208">tareas</span><span class="sxs-lookup"><span data-stu-id="aea5b-208">tasks</span></span>
  - <span data-ttu-id="aea5b-209">atributos de software</span><span class="sxs-lookup"><span data-stu-id="aea5b-209">software attributes</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="aea5b-210">Eliminar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="aea5b-210">Delete hello cluster</span></span>
<span data-ttu-id="aea5b-211">tooavoid incoherencias, se recomienda deshabilitar las tablas de hello HBase antes de eliminar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-211">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="aea5b-212">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="aea5b-212">Troubleshoot</span></span>

<span data-ttu-id="aea5b-213">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="aea5b-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aea5b-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aea5b-214">Next steps</span></span>
<span data-ttu-id="aea5b-215">En este artículo, ha aprendido cómo toocreate un clúster de HBase y cómo ver y tablas toocreate Hola datos en las tablas de Hola shell de HBase.</span><span class="sxs-lookup"><span data-stu-id="aea5b-215">In this article, you learned how toocreate an HBase cluster and how toocreate tables and view hello data in those tables from hello HBase shell.</span></span> <span data-ttu-id="aea5b-216">También ha aprendido cómo toouse un subárbol consultas sobre los datos en las tablas de HBase y cómo toouse Hola toocreate de API de REST de HBase C# en una tabla HBase y recuperar datos de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="aea5b-216">You also learned how toouse a Hive query on data in HBase tables and how toouse hello HBase C# REST APIs toocreate an HBase table and retrieve data from hello table.</span></span>

<span data-ttu-id="aea5b-217">toolearn más información, vea:</span><span class="sxs-lookup"><span data-stu-id="aea5b-217">toolearn more, see:</span></span>

* <span data-ttu-id="aea5b-218">[Información general de HBase de HDInsight][hdinsight-hbase-overview]: HBase es una base de datos NoSQL de código abierto Apache basada en Hadoop que proporciona acceso aleatorio y una coherencia sólida para grandes cantidades de datos no estructurados y semiestructurados.</span><span class="sxs-lookup"><span data-stu-id="aea5b-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
