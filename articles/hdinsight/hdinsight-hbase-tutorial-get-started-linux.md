---
title: "Introducción a un ejemplo de HBase en HDInsight - Azure | Microsoft Docs"
description: "Siga este ejemplo de Apache HBase para empezar a usar Hadoop en HDInsight. Cree tablas desde el shell de HBase y consúltelas mediante Hive."
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
ms.openlocfilehash: bbd8a838062795ee03ae02dc5e3fd45d841a6e17
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="18478-105">Introducción a un ejemplo de Apache HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="18478-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="18478-106">Aprenda a crear un clúster de HBase en HDInsight, a crear tablas de HBase y a consultar tablas mediante Hive.</span><span class="sxs-lookup"><span data-stu-id="18478-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="18478-107">Para obtener información general de HBase, consulte [Información general de HBase de HDInsight][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="18478-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="18478-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18478-108">Prerequisites</span></span>
<span data-ttu-id="18478-109">Antes de empezar a probar este ejemplo de HBase, debe tener los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="18478-109">Before you begin trying this HBase example, you must have the following items:</span></span>

* <span data-ttu-id="18478-110">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="18478-110">**An Azure subscription**.</span></span> <span data-ttu-id="18478-111">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="18478-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="18478-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="18478-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="18478-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="18478-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="18478-114">Creación del clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="18478-114">Create HBase cluster</span></span>
<span data-ttu-id="18478-115">El siguiente procedimiento usa una plantilla de Azure Resource Manager para crear un clúster de HBase basado en Linux versión 3.4, y la cuenta de Azure Storage predeterminada dependiente.</span><span class="sxs-lookup"><span data-stu-id="18478-115">The following procedure uses an Azure Resource Manager template to create a version 3.4 Linux-based HBase cluster and the dependent default Azure Storage account.</span></span> <span data-ttu-id="18478-116">Para comprender los parámetros utilizados en el procedimiento y otros métodos de creación del clúster, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="18478-116">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="18478-117">Haga clic en la imagen siguiente para abrir la plantilla en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="18478-117">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="18478-118">La plantilla se encuentra en un contenedor de blobs público.</span><span class="sxs-lookup"><span data-stu-id="18478-118">The template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="18478-119">En la hoja **Implementación personalizada**, escriba los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="18478-119">From the **Custom deployment** blade, enter the following values:</span></span>
   
   * <span data-ttu-id="18478-120">**Suscripción**: seleccione la suscripción de Azure que usa para crear este clúster.</span><span class="sxs-lookup"><span data-stu-id="18478-120">**Subscription**: Select your Azure subscription that is used to create the cluster.</span></span>
   * <span data-ttu-id="18478-121">**Grupo de recursos**: cree un grupo de administración de recursos de Azure o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="18478-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="18478-122">**Ubicación**: especifique la ubicación del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="18478-122">**Location**: Specify the location of the resource group.</span></span> 
   * <span data-ttu-id="18478-123">**Nombre del clúster**: escriba el nombre del clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="18478-123">**ClusterName**: Enter a name for the HBase cluster.</span></span>
   * <span data-ttu-id="18478-124">**Nombre de inicio de sesión y contraseña de clúster**: el nombre de inicio de sesión predeterminado es **admin**.</span><span class="sxs-lookup"><span data-stu-id="18478-124">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="18478-125">**Nombre de usuario y contraseña de SSH**: el nombre de usuario predeterminado es **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="18478-125">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="18478-126">Puede cambiarlo.</span><span class="sxs-lookup"><span data-stu-id="18478-126">You can rename it.</span></span>
     
     <span data-ttu-id="18478-127">Otros parámetros son opcionales.</span><span class="sxs-lookup"><span data-stu-id="18478-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="18478-128">Cada clúster tiene una dependencia de cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="18478-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="18478-129">Después de eliminar un clúster, los datos permanecen en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18478-129">After you delete a cluster, the data retains in the storage account.</span></span> <span data-ttu-id="18478-130">El nombre de cuenta de almacenamiento de clúster predeterminado es el nombre del clúster con "store" anexado.</span><span class="sxs-lookup"><span data-stu-id="18478-130">The cluster default storage account name is the cluster name with "store" appended.</span></span> <span data-ttu-id="18478-131">Está codificado en la sección de variables de plantilla.</span><span class="sxs-lookup"><span data-stu-id="18478-131">It is hardcoded in the template variables section.</span></span>
3. <span data-ttu-id="18478-132">Seleccione **Acepto los términos y condiciones indicadas anteriormente** y, después, haga clic en **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="18478-132">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="18478-133">Se tarda aproximadamente 20 minutos en crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="18478-133">It takes about 20 minutes to create a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="18478-134">Después de que se elimine un clúster de HBase, puede crear otro clúster de HBase mediante el mismo contenedor de blobs predeterminado.</span><span class="sxs-lookup"><span data-stu-id="18478-134">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span></span> <span data-ttu-id="18478-135">El nuevo clúster selecciona las tablas de HBase que creó en el clúster original.</span><span class="sxs-lookup"><span data-stu-id="18478-135">The new cluster picks up the HBase tables you created in the original cluster.</span></span> <span data-ttu-id="18478-136">Para evitar incoherencias, recomendamos deshabilitar las tablas de HBase antes de eliminar el clúster.</span><span class="sxs-lookup"><span data-stu-id="18478-136">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="18478-137">Creación de tablas e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="18478-137">Create tables and insert data</span></span>
<span data-ttu-id="18478-138">Puede usar SSH para conectarse a los clústeres de HBase y, después, usar el shell de HBase para crear tablas de HBase e insertar y consultar datos.</span><span class="sxs-lookup"><span data-stu-id="18478-138">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data, and query data.</span></span> <span data-ttu-id="18478-139">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="18478-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="18478-140">Para la mayoría de las personas, los datos aparecen en formato tabular:</span><span class="sxs-lookup"><span data-stu-id="18478-140">For most people, data appears in the tabular format:</span></span>

![Datos tabulares de HBase de HDInsight][img-hbase-sample-data-tabular]

<span data-ttu-id="18478-142">En HBase (una implementación de BigTable), los mismos datos tienen un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="18478-142">In HBase (an implementation of BigTable), the same data looks like:</span></span>

![Datos de HDInsight HBase BigTable][img-hbase-sample-data-bigtable]


<span data-ttu-id="18478-144">**Para usar el shell de HBase, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="18478-144">**To use the HBase shell**</span></span>

1. <span data-ttu-id="18478-145">Desde SSH ejecute el siguiente comando de HBase:</span><span class="sxs-lookup"><span data-stu-id="18478-145">From SSH, run the following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="18478-146">Cree una tabla HBase con dos familias de columnas:</span><span class="sxs-lookup"><span data-stu-id="18478-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="18478-147">Inserte algunos datos:</span><span class="sxs-lookup"><span data-stu-id="18478-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Shell de HDInsight Hadoop HBase][img-hbase-shell]
4. <span data-ttu-id="18478-149">Obtenga una sola fila</span><span class="sxs-lookup"><span data-stu-id="18478-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="18478-150">Verá los mismos resultados que con el comando de examen porque solo hay una fila.</span><span class="sxs-lookup"><span data-stu-id="18478-150">You shall see the same results as using the scan command because there is only one row.</span></span>
   
    <span data-ttu-id="18478-151">Para más información acerca del esquema de tabla de Hbase, consulte [Introducción al diseño de esquema de HBase][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="18478-151">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="18478-152">Para ver más comandos de HBase, consulte [Guía de referencia de Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="18478-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="18478-153">Salga del shell</span><span class="sxs-lookup"><span data-stu-id="18478-153">Exit the shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="18478-154">**Para cargar datos de forma masiva en la tabla HBase de contactos**</span><span class="sxs-lookup"><span data-stu-id="18478-154">**To bulk load data into the contacts HBase table**</span></span>

<span data-ttu-id="18478-155">HBase incluye varios métodos de carga de datos en las tablas.</span><span class="sxs-lookup"><span data-stu-id="18478-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="18478-156">Para obtener más información, vea [Carga masiva](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="18478-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="18478-157">Se puede encontrar un archivo de datos de ejemplo en un contenedor de blobs público, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="18478-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="18478-158">El contenido del archivo de datos es:</span><span class="sxs-lookup"><span data-stu-id="18478-158">The content of the data file is:</span></span>

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

<span data-ttu-id="18478-159">Opcionalmente, puede crear un archivo de texto y cargarlo en su propia cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18478-159">You can optionally create a text file and upload the file to your own storage account.</span></span> <span data-ttu-id="18478-160">Para obtener instrucciones, consulte [Carga de datos para trabajos de Hadoop en HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="18478-160">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="18478-161">Este procedimiento usa la tabla HBase de contactos que ha creado en el último procedimiento.</span><span class="sxs-lookup"><span data-stu-id="18478-161">This procedure uses the Contacts HBase table you have created in the last procedure.</span></span>
> 

1. <span data-ttu-id="18478-162">Desde SSH ejecute el siguiente comando para transformar el archivo de datos en StoreFiles y almacene en una ruta de acceso relativa especificada por Dimporttsv.bulk.output.</span><span class="sxs-lookup"><span data-stu-id="18478-162">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="18478-163">Si está en el shell de HBase, utilice el comando de salida para salir.</span><span class="sxs-lookup"><span data-stu-id="18478-163">If you are in HBase Shell, use the exit command to exit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="18478-164">Ejecute el siguiente comando para cargar los datos desde /example/data/storeDataFileOutput en la tabla de HBase:</span><span class="sxs-lookup"><span data-stu-id="18478-164">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="18478-165">Puede abrir el shell de HBase y usar el comando de análisis para mostrar el contenido de la tabla.</span><span class="sxs-lookup"><span data-stu-id="18478-165">You can open the HBase shell, and use the scan command to list the table content.</span></span>

## <a name="use-hive-to-query-hbase"></a><span data-ttu-id="18478-166">Utilización de Hive para consultar HBase</span><span class="sxs-lookup"><span data-stu-id="18478-166">Use Hive to query HBase</span></span>

<span data-ttu-id="18478-167">Puede consultar datos en tablas de HBase mediante el uso de Hive.</span><span class="sxs-lookup"><span data-stu-id="18478-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="18478-168">En esta sección, creará una tabla de Hive que se asigna a la tabla de HBase y la usará para consultar los datos de la tabla de HBase.</span><span class="sxs-lookup"><span data-stu-id="18478-168">In this section, you create a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span></span>

1. <span data-ttu-id="18478-169">Abra **PuTTY**y conéctese al clúster.</span><span class="sxs-lookup"><span data-stu-id="18478-169">Open **PuTTY**, and connect to the cluster.</span></span>  <span data-ttu-id="18478-170">Consulte las instrucciones del procedimiento anterior.</span><span class="sxs-lookup"><span data-stu-id="18478-170">See the instructions in the previous procedure.</span></span>
2. <span data-ttu-id="18478-171">En la sesión SSH, use el siguiente comando para iniciar Beeline:</span><span class="sxs-lookup"><span data-stu-id="18478-171">From the SSH session, use the following command to start Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="18478-172">Para más información sobre Beeline, consulte [Uso de Hive con Hadoop en HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="18478-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="18478-173">Ejecute el siguiente script de HiveQL para crear una tabla de Hive que se asigne a la tabla de HBase.</span><span class="sxs-lookup"><span data-stu-id="18478-173">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span></span> <span data-ttu-id="18478-174">Antes de ejecutar esta instrucción, asegúrese de haber creado la tabla de ejemplo a la que se hace referencia aquí en HBase mediante el shell de HBase.</span><span class="sxs-lookup"><span data-stu-id="18478-174">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="18478-175">Ejecute el siguiente script de HiveQL para consultar los datos de la tabla de HBase:</span><span class="sxs-lookup"><span data-stu-id="18478-175">Run the following HiveQL script to query the data in the HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="18478-176">Usar las API de REST de HBase con Curl</span><span class="sxs-lookup"><span data-stu-id="18478-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="18478-177">La API de REST se protege con la [autenticación básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="18478-177">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="18478-178">Siempre debe crear solicitudes usando HTTP segura (HTTPS) para así garantizar que las credenciales se envían de manera segura al servidor.</span><span class="sxs-lookup"><span data-stu-id="18478-178">You shall always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>

2. <span data-ttu-id="18478-179">Use el siguiente comando para enumerar las tablas de HBase existentes:</span><span class="sxs-lookup"><span data-stu-id="18478-179">Use the following command to list the existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="18478-180">Use el siguiente comando para crear una nueva tabla de HBase con dos familias de columnas:</span><span class="sxs-lookup"><span data-stu-id="18478-180">Use the following command to create a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="18478-181">El esquema se ofrece con el formato JSon.</span><span class="sxs-lookup"><span data-stu-id="18478-181">The schema is provided in the JSon format.</span></span>
4. <span data-ttu-id="18478-182">Use el siguiente comando para instalar algunos datos:</span><span class="sxs-lookup"><span data-stu-id="18478-182">Use the following command to insert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="18478-183">Debe codificar en base64 los valores especificados en el modificador -d.</span><span class="sxs-lookup"><span data-stu-id="18478-183">You must base64 encode the values specified in the -d switch.</span></span> <span data-ttu-id="18478-184">En el ejemplo:</span><span class="sxs-lookup"><span data-stu-id="18478-184">In the example:</span></span>
   
   * <span data-ttu-id="18478-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="18478-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="18478-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="18478-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="18478-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="18478-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="18478-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) permite insertar varios valores (por lotes).</span><span class="sxs-lookup"><span data-stu-id="18478-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) values.</span></span>
5. <span data-ttu-id="18478-189">Use el siguiente comando para obtener una fila:</span><span class="sxs-lookup"><span data-stu-id="18478-189">Use the following command to get a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="18478-190">Para más información sobre Rest de HBase, consulte la [guía de referencia de Apache HBase](https://hbase.apache.org/book.html#_rest).</span><span class="sxs-lookup"><span data-stu-id="18478-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="18478-191">Thrift no es compatible con HBase en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18478-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="18478-192">Al usar Curl o cualquier otra comunicación REST con WebHCat, debe proporcionar el nombre de usuario y la contraseña del administrador del clúster de HDInsight para autenticar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="18478-192">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="18478-193">También debe usar el nombre del clúster como parte del identificador uniforme de recursos (URI) que se utiliza para enviar las solicitudes al servidor:</span><span class="sxs-lookup"><span data-stu-id="18478-193">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="18478-194">Recibirá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="18478-194">You should receive a response similar to the following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="18478-195">Comprobar el estado del clúster</span><span class="sxs-lookup"><span data-stu-id="18478-195">Check cluster status</span></span>
<span data-ttu-id="18478-196">HBase en HDInsight se incluye con una interfaz de usuario web para la supervisión de clústeres.</span><span class="sxs-lookup"><span data-stu-id="18478-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="18478-197">Mediante la interfaz de usuario web, puede solicitar estadísticas o información acerca de las regiones.</span><span class="sxs-lookup"><span data-stu-id="18478-197">Using the Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="18478-198">**Para acceder a la interfaz de usuario maestra de HBase**</span><span class="sxs-lookup"><span data-stu-id="18478-198">**To access the HBase Master UI**</span></span>

1. <span data-ttu-id="18478-199">Inicie sesión en la interfaz de usuario web de Ambari en https://&lt;nombre_de_cluster>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="18478-199">Sign into the the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="18478-200">Haga clic en **HBase** en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="18478-200">Click **HBase** from the left menu.</span></span>
3. <span data-ttu-id="18478-201">Haga clic en **Quick links** (Vínculos rápidos) en la parte superior de la página, seleccione el vínculo del nodo Zookeeper activo y, después, haga clic en **HBase Master UI** (Interfaz de usuario maestra de HBase).</span><span class="sxs-lookup"><span data-stu-id="18478-201">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="18478-202">La interfaz de usuario se abre en otra pestaña del explorador:</span><span class="sxs-lookup"><span data-stu-id="18478-202">The UI is opened in another browser tab:</span></span>

  ![Interfaz de usuario maestra de HBase de HDInsight](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="18478-204">La interfaz de usuario maestra de HBase contiene las siguientes secciones:</span><span class="sxs-lookup"><span data-stu-id="18478-204">The HBase Master UI contains the following sections:</span></span>

  - <span data-ttu-id="18478-205">servidores regionales</span><span class="sxs-lookup"><span data-stu-id="18478-205">region servers</span></span>
  - <span data-ttu-id="18478-206">maestros de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="18478-206">backup masters</span></span>
  - <span data-ttu-id="18478-207">tables</span><span class="sxs-lookup"><span data-stu-id="18478-207">tables</span></span>
  - <span data-ttu-id="18478-208">tareas</span><span class="sxs-lookup"><span data-stu-id="18478-208">tasks</span></span>
  - <span data-ttu-id="18478-209">atributos de software</span><span class="sxs-lookup"><span data-stu-id="18478-209">software attributes</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="18478-210">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="18478-210">Delete the cluster</span></span>
<span data-ttu-id="18478-211">Para evitar incoherencias, recomendamos deshabilitar las tablas de HBase antes de eliminar el clúster.</span><span class="sxs-lookup"><span data-stu-id="18478-211">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="18478-212">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="18478-212">Troubleshoot</span></span>

<span data-ttu-id="18478-213">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="18478-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18478-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18478-214">Next steps</span></span>
<span data-ttu-id="18478-215">En este tutorial, ha aprendido a crear un clúster de HBase, a crear tablas y a ver los datos de esas tablas en el shell de HBase.</span><span class="sxs-lookup"><span data-stu-id="18478-215">In this article, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span></span> <span data-ttu-id="18478-216">También ha aprendido a usar una consulta de datos de Hive en las tablas de HBase y a usar las API de REST de C# para HBase para crear una tabla de HBase y recuperar los datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="18478-216">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span></span>

<span data-ttu-id="18478-217">Para obtener más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="18478-217">To learn more, see:</span></span>

* <span data-ttu-id="18478-218">[Información general de HBase de HDInsight][hdinsight-hbase-overview]: HBase es una base de datos NoSQL de código abierto Apache basada en Hadoop que proporciona acceso aleatorio y una coherencia sólida para grandes cantidades de datos no estructurados y semiestructurados.</span><span class="sxs-lookup"><span data-stu-id="18478-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

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
