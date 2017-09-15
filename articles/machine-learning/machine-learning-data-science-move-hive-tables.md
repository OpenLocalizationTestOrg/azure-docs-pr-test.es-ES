---
title: "Creación de tablas de Hive y carga de datos desde Azure Blob Storage | Microsoft Docs"
description: "Crear tablas de subárbol y cargar datos de blob en tablas de subárbol"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: eca4ecd8f639bb9816903f4b1d1f999755da819c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="08407-103">Creación de tablas de Hive y carga de datos desde Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="08407-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="08407-104">En este tema se presentan consultas genéricas de Hive que crean tablas de Hive y cargan datos desde Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="08407-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="08407-105">También se ofrecen algunas instrucciones acerca de las particiones de tablas de subárbol y de cómo utilizar el formato ORC para mejorar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="08407-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="08407-106">Este **menú** siguiente redirige a temas en los que se describe cómo introducir datos en entornos de destino en que se pueden almacenar y procesar datos durante el proceso de ciencia de datos en equipos (TDSP).</span><span class="sxs-lookup"><span data-stu-id="08407-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="08407-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="08407-107">Prerequisites</span></span>
<span data-ttu-id="08407-108">En este artículo se supone que ha:</span><span class="sxs-lookup"><span data-stu-id="08407-108">This article assumes that you have:</span></span>

* <span data-ttu-id="08407-109">Creado una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="08407-109">Created an Azure storage account.</span></span> <span data-ttu-id="08407-110">Para obtener instrucciones, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="08407-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="08407-111">Aprovisionado un clúster de Hadoop personalizado con el servicio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="08407-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="08407-112">Si necesita instrucciones, consulte [Personalización de clústeres de Hadoop de HDInsight de Azure para análisis avanzado](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="08407-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="08407-113">Habilitado el acceso remoto para el clúster, iniciado sesión y abierto la consola de la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="08407-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="08407-114">Si necesita instrucciones, consulte [Acceso al nodo principal del clúster Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="08407-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="08407-115">Carga de datos en el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="08407-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="08407-116">Si creó una máquina virtual de Azure siguiendo las instrucciones dadas en [Configuración de una máquina virtual de Azure para análisis avanzado](machine-learning-data-science-setup-virtual-machine.md), este archivo de script debió descargarse en el directorio *C:\\Users\\\<nombre de usuario\>\\Documents\\Data Science Scripts* de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="08407-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="08407-117">Estas consultas de subárbol solo requieren que conecte sus propios esquemas de datos y la configuración de almacenamiento de blobs de Azure en los campos adecuados para estar preparado para su envío.</span><span class="sxs-lookup"><span data-stu-id="08407-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="08407-118">Se supone que los datos de las tablas de Hive están en un formato tabular **sin comprimir** y que se han cargado los datos en el contenedor predeterminado (o en otro adicional) de la cuenta de almacenamiento que usa el clúster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="08407-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="08407-119">Si desea practicar con el grupo **NYC Taxi Trip Data**, necesita hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="08407-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="08407-120">**Descargue** los 24 archivos de [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) (12 archivos de carreras y 12 archivos de tarifas).</span><span class="sxs-lookup"><span data-stu-id="08407-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="08407-121">**Descomprima** todos los archivos en archivos .csv.</span><span class="sxs-lookup"><span data-stu-id="08407-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="08407-122">**cargue** los archivos en el contenedor predeterminado (o el contenedor pertinente) de la cuenta de Azure Storage que se creó mediante el procedimiento descrito en el tema [Personalización de los clústeres de Hadoop de HDInsight de Azure para el proceso de ciencia de datos en equipos](machine-learning-data-science-customize-hadoop-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="08407-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="08407-123">En esta [página](machine-learning-data-science-process-hive-walkthrough.md#upload)encontrará el proceso de cargar los archivos .csv en el contenedor predeterminado de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="08407-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="08407-124"><a name="submit"></a>Envío de consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="08407-124"><a name="submit"></a>How to submit Hive queries</span></span>
<span data-ttu-id="08407-125">Las consultas de subárbol se pueden enviar mediante:</span><span class="sxs-lookup"><span data-stu-id="08407-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="08407-126">Enviar consultas de Hive a través de línea de comandos de Hadoop en el nodo principal del clúster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="08407-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="08407-127">Enviar consultas de Hive con el Editor de Hive</span><span class="sxs-lookup"><span data-stu-id="08407-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="08407-128">Enviar consultas de Hive con los comandos de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="08407-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="08407-129">Las consultas de Hive son similares a SQL.</span><span class="sxs-lookup"><span data-stu-id="08407-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="08407-130">Los usuarios familiarizados con SQL pueden encontrar la [hoja de referencia rápida Hive para usuarios de SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) de gran utilidad.</span><span class="sxs-lookup"><span data-stu-id="08407-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="08407-131">Al enviar una consulta de subárbol, también puede controlar el destino del resultado de las consultas de subárbol, ya sea en la pantalla o en un archivo local del nodo principal o en un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="08407-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <span data-ttu-id="08407-132"><a name="headnode"></a> 1. Enviar consultas de Hive a través de línea de comandos de Hadoop en el nodo principal del clúster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="08407-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="08407-133">Si la consulta es compleja, enviar consultas de Hive directamente en el nodo principal del clúster de Hadoop normalmente permite obtener respuestas más rápidas que si se efectúa el envío mediante un editor de Hive o scripts de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08407-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="08407-134">Inicie sesión en el nodo principal del clúster de Hadoop, abra la línea de comandos de Hadoop en el escritorio del nodo principal y escriba el comando `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="08407-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="08407-135">Los usuarios disponen de tres maneras de enviar consultas de Hive en la línea de comandos de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="08407-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="08407-136">Directamente</span><span class="sxs-lookup"><span data-stu-id="08407-136">directly</span></span>
* <span data-ttu-id="08407-137">usando archivos .hql</span><span class="sxs-lookup"><span data-stu-id="08407-137">using .hql files</span></span>
* <span data-ttu-id="08407-138">Con la consola de comandos de Hive</span><span class="sxs-lookup"><span data-stu-id="08407-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="08407-139">Envíe consultas de subárbol directamente en la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="08407-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="08407-140">Los usuarios pueden ejecutar el comando como `hive -e "<your hive query>;` para enviar consultas de Hive sencillas directamente en la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="08407-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="08407-141">Este es un ejemplo, donde el cuadro rojo muestra el comando que envía la consulta de subárbol y el cuadro verde muestra el resultado de la consulta de subárbol.</span><span class="sxs-lookup"><span data-stu-id="08407-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="08407-143">Enviar consultas de subárbol en archivos .hql</span><span class="sxs-lookup"><span data-stu-id="08407-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="08407-144">Cuando la consulta de subárbol es más complicada y tiene varias líneas, no resulta práctico modificar consultas en la línea de comandos o la consola de comandos de subárbol.</span><span class="sxs-lookup"><span data-stu-id="08407-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="08407-145">Una alternativa es usar un editor de texto en el nodo principal del clúster de Hadoop y guardar las consultas de subárbol en un archivo .hql de un directorio local del nodo principal.</span><span class="sxs-lookup"><span data-stu-id="08407-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="08407-146">A continuación, la consulta de Hive del archivo .hql puede enviarse mediante el argumento `-f` del modo indicado a continuación:</span><span class="sxs-lookup"><span data-stu-id="08407-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="08407-148">**Suprimir la impresión de pantalla del estado de progreso de las consultas de subárbol**</span><span class="sxs-lookup"><span data-stu-id="08407-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="08407-149">De forma predeterminada, después de enviar la consulta de Hive en la línea de comandos de Hadoop, el progreso del trabajo de asignación/reducción se imprimirá en pantalla.</span><span class="sxs-lookup"><span data-stu-id="08407-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="08407-150">Para suprimir la impresión de la pantalla del progreso del trabajo de asignación/reducción, puede usar un argumento `-S` ("S" en mayúsculas) en la línea de comandos del modo indicado a continuación:</span><span class="sxs-lookup"><span data-stu-id="08407-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
<span data-ttu-id="08407-151">.</span><span class="sxs-lookup"><span data-stu-id="08407-151">.</span></span>    <span data-ttu-id="08407-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="08407-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="08407-153">Envíe consultas de subárbol en la consola de comandos de subárbol.</span><span class="sxs-lookup"><span data-stu-id="08407-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="08407-154">Los usuarios también pueden especificar en primer lugar la consola de comandos de Hive al ejecutar el comando `hive` en la línea de comandos de Hadoop y, a continuación, enviar consultas de Hive en la consola de comandos de Hive.</span><span class="sxs-lookup"><span data-stu-id="08407-154">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="08407-155">Aquí tiene un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="08407-155">Here is an example.</span></span> <span data-ttu-id="08407-156">En este ejemplo, los dos cuadros de color rojo resaltan los comandos que se utilizan para escribir en la consola de comandos de subárbol y la consulta de subárbol enviada en la consola de comandos de subárbol, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="08407-156">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="08407-157">El cuadro verde resalta el resultado de la consulta de subárbol.</span><span class="sxs-lookup"><span data-stu-id="08407-157">The green box highlights the output from the Hive query.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="08407-159">Los ejemplos anteriores generan directamente los resultados de la consulta de subárbol en pantalla.</span><span class="sxs-lookup"><span data-stu-id="08407-159">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="08407-160">Los usuarios también pueden escribir la salida en un archivo local del nodo principal o en un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="08407-160">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="08407-161">A continuación, los usuarios pueden utilizar otras herramientas para analizar más el resultado de las consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="08407-161">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="08407-162">**Genere los resultados de consulta de subárbol en un archivo local.**</span><span class="sxs-lookup"><span data-stu-id="08407-162">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="08407-163">Para generar los resultados de consultas de Hive en un directorio local del nodo principal, los usuarios tienen que enviar la consulta de Hive de la línea de comandos de Hadoop de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="08407-163">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="08407-164">En el ejemplo siguiente, el resultado de la consulta de Hive se escribe en un archivo `hivequeryoutput.txt` del directorio `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="08407-164">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="08407-166">**Generar los resultados de consulta de subárbol en un blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="08407-166">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="08407-167">Los usuarios también pueden generar resultados de consulta de Hive en un blob de Azure, dentro del contenedor predeterminado del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="08407-167">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="08407-168">La consulta de Hive para esto es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="08407-168">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="08407-169">En el ejemplo siguiente, el resultado de la consulta de Hive se escribe en un directorio de blob `queryoutputdir` dentro del contenedor predeterminado del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="08407-169">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="08407-170">En este caso, solo necesita proporcionar el nombre del directorio, sin el nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="08407-170">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="08407-171">Se produce un error si proporciona los nombres de directorio y de blob, como `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="08407-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="08407-173">Si abre el contenedor predeterminado del clúster de Hadoop mediante herramientas como el Explorador de Azure Storage, verá el resultado de la consulta de Hive como se muestra en la ilustración siguiente.</span><span class="sxs-lookup"><span data-stu-id="08407-173">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="08407-174">Puede aplicar el filtro (resaltado mediante un cuadro rojo) para recuperar solo el blob con letras especificadas en los nombres.</span><span class="sxs-lookup"><span data-stu-id="08407-174">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="08407-176"><a name="hive-editor"></a> 2. Enviar consultas de Hive con el Editor de Hive</span><span class="sxs-lookup"><span data-stu-id="08407-176"><a name="hive-editor"></a> 2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="08407-177">También puede utilizar la consola de consultas (Editor de Hive) escribiendo una dirección URL del formulario *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="08407-177">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="08407-178">Debe haber iniciado sesión para ver esta consola; así pues, tiene que escribir sus credenciales de Hadoop aquí.</span><span class="sxs-lookup"><span data-stu-id="08407-178">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="08407-179"><a name="ps"></a> 3. Enviar consultas de Hive con los comandos de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="08407-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="08407-180">Los usuarios pueden también usar PowerShell para enviar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="08407-180">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="08407-181">Para obtener instrucciones, consulte [Envío de trabajos de Hive mediante PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="08407-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="08407-182"><a name="create-tables"></a>Creación de tablas y base de datos de Hive</span><span class="sxs-lookup"><span data-stu-id="08407-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="08407-183">Las consultas de Hive se comparten en el [repositorio de GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) y se pueden descargar desde allí.</span><span class="sxs-lookup"><span data-stu-id="08407-183">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="08407-184">Esta es la consulta de subárbol que crea una tabla de subárbol.</span><span class="sxs-lookup"><span data-stu-id="08407-184">Here is the Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="08407-185">Estas son las descripciones de los campos que los usuarios necesitan para conectar y otras configuraciones:</span><span class="sxs-lookup"><span data-stu-id="08407-185">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="08407-186">**&#60;nombre de base de datos>**: nombre de la base de datos que los usuarios desean crear.</span><span class="sxs-lookup"><span data-stu-id="08407-186">**&#60;database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="08407-187">Si los usuarios solo desean usar la base de datos predeterminada, se puede omitir la consulta *crear base de datos...*</span><span class="sxs-lookup"><span data-stu-id="08407-187">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="08407-188">**&#60;nombre de tabla>**: nombre de la tabla que los usuarios quieren crear en la base de datos especificada.</span><span class="sxs-lookup"><span data-stu-id="08407-188">**&#60;table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="08407-189">Si los usuarios desean usar la base de datos predeterminada, puede hacer referencia directamente a la tabla *&#60;nombre de tabla>* sin &#60;nombre de base de datos>.</span><span class="sxs-lookup"><span data-stu-id="08407-189">If you want to use the default database, the table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="08407-190">**&#60;separador de campos>**: separador que delimita los campos del archivo de datos que se cargará en la tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="08407-190">**&#60;field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="08407-191">**&#60;line separator>**: separador que delimita las líneas del archivo de datos.</span><span class="sxs-lookup"><span data-stu-id="08407-191">**&#60;line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="08407-192">**&#60;storage location>**: la ubicación de Azure Storage para guardar los datos de tablas de Hive.</span><span class="sxs-lookup"><span data-stu-id="08407-192">**&#60;storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="08407-193">Si los usuarios no especifican *LOCATION &#60;ubicación de almacenamiento>*, la base de datos y las tablas se almacenan de forma predeterminada en el directorio *hive/warehouse/* del contenedor predeterminado del clúster Hive.</span><span class="sxs-lookup"><span data-stu-id="08407-193">If you do not specify *LOCATION &#60;storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="08407-194">Si un usuario desea especificar la ubicación de almacenamiento, esta debe estar dentro del contenedor predeterminado para la base de datos y las tablas.</span><span class="sxs-lookup"><span data-stu-id="08407-194">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="08407-195">A esta ubicación tiene que hacerse referencia como ubicación relativa al contenedor predeterminado del clúster con el formato *'wasb:///&#60;directory 1>/'* o *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. Después de ejecutar la consulta, se crean los directorios relativos dentro del contenedor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="08407-195">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="08407-196">**TBLPROPERTIES("skip.header.line.count"="1")**: si el archivo de datos tiene una línea de encabezado, los usuarios deben agregar esta propiedad **al final** de la consulta *create table*.</span><span class="sxs-lookup"><span data-stu-id="08407-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="08407-197">De lo contrario, se carga la línea de encabezado como registro en la tabla.</span><span class="sxs-lookup"><span data-stu-id="08407-197">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="08407-198">Si el archivo de datos no tiene una línea de encabezado, se puede omitir esta configuración en la consulta.</span><span class="sxs-lookup"><span data-stu-id="08407-198">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <span data-ttu-id="08407-199"><a name="load-data"></a>Carga de datos en tablas de Hive</span><span class="sxs-lookup"><span data-stu-id="08407-199"><a name="load-data"></a>Load data to Hive tables</span></span>
<span data-ttu-id="08407-200">Esta es la consulta de subárbol que carga datos en una tabla de subárbol.</span><span class="sxs-lookup"><span data-stu-id="08407-200">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="08407-201">**&#60;ruta de acceso a datos de blob>**: si el archivo de blob que se va a cargar en la tabla de Hive se encuentra en el contenedor predeterminado del clúster Hadoop de HDInsight, *&#60;ruta de acceso a datos de blob>* debe tener el formato "*wasb:///&#60;directorio de este contenedor>/&#60;nombre del archivo de blob>"*.</span><span class="sxs-lookup"><span data-stu-id="08407-201">**&#60;path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *&#60;path to blob data>* should be in the format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="08407-202">El archivo blob también puede estar en un contenedor adicional del clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="08407-202">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="08407-203">En este caso, *&#60;ruta de acceso a datos de blob>* debería tener el formato *"wasb://&#60;nombre del contenedor>@&#60;nombre de cuenta de almacenamiento>.blob.core.windows.net/&#60;nombre de archivo de blob>"*.</span><span class="sxs-lookup"><span data-stu-id="08407-203">In this case, *&#60;path to blob data>* should be in the format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="08407-204">Los datos blob que se van a cargar en la tabla de subárbol tienen que estar en el contenedor adicional o predeterminado de la cuenta de almacenamiento para el clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="08407-204">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="08407-205">De lo contrario, la consulta *LOAD DATA* genera un error indicando que no puede obtener acceso a los datos.</span><span class="sxs-lookup"><span data-stu-id="08407-205">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <span data-ttu-id="08407-206"><a name="partition-orc"></a>Temas avanzados: tabla con particiones y datos de Hive de almacén en formato ORC</span><span class="sxs-lookup"><span data-stu-id="08407-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="08407-207">Si los datos son grandes, crear particiones de la tabla será beneficioso para las consultas que solo necesitan examinar algunas particiones de la tabla.</span><span class="sxs-lookup"><span data-stu-id="08407-207">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="08407-208">Por ejemplo, es razonable crear particiones de los datos de registro de un sitio web por fechas.</span><span class="sxs-lookup"><span data-stu-id="08407-208">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="08407-209">Además de crear particiones de tablas de subárbol, también es beneficioso almacenar los datos de subárbol en el formato ORC.</span><span class="sxs-lookup"><span data-stu-id="08407-209">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="08407-210">Para obtener más información acerca de la aplicación de formato ORC, consulte <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">El uso de archivos ORC mejora el rendimiento cuando Hive está leyendo, escribiendo y procesando datos</a>.</span><span class="sxs-lookup"><span data-stu-id="08407-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="08407-211">Tabla con particiones</span><span class="sxs-lookup"><span data-stu-id="08407-211">Partitioned table</span></span>
<span data-ttu-id="08407-212">Esta es la consulta de subárbol que crea una tabla con particiones y carga datos en ella.</span><span class="sxs-lookup"><span data-stu-id="08407-212">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="08407-213">Al consultar tablas con particiones, se recomienda agregar la condición de partición al **comienzo** de la cláusula `where`, ya que esto mejora la eficacia de la búsqueda de manera significativa.</span><span class="sxs-lookup"><span data-stu-id="08407-213">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="08407-214"><a name="orc"></a>Almacenamiento de datos de Hive en formato ORC</span><span class="sxs-lookup"><span data-stu-id="08407-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="08407-215">Los usuarios no pueden cargar datos directamente desde Blob Storage en tablas de Hive que se almacenan en el formato ORC.</span><span class="sxs-lookup"><span data-stu-id="08407-215">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="08407-216">Estos son los pasos que los usuarios deben seguir para cargar datos desde blobs de Azure a tablas de Hive almacenadas en formato ORC.</span><span class="sxs-lookup"><span data-stu-id="08407-216">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="08407-217">Cree una tabla externa **STORED AS TEXTFILE** y cargue datos del almacenamiento de blobs en la tabla.</span><span class="sxs-lookup"><span data-stu-id="08407-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="08407-218">Cree una tabla interna con el mismo esquema que la tabla externa del paso 1, con el mismo delimitador de campo, y almacene los datos de subárbol en el formato ORC.</span><span class="sxs-lookup"><span data-stu-id="08407-218">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="08407-219">Seleccionar datos desde la tabla externa del paso 1 e insertarlos en la tabla de ORC</span><span class="sxs-lookup"><span data-stu-id="08407-219">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="08407-220">Si la tabla TEXTFILE *&amp;#60;nombre de base de datos&gt;.&amp;#60;nombre de la tabla de archivo de texto externo&gt;`SELECT * FROM <database name>.<external textfile table name>` tiene particiones, en el PASO 3, el comando* selecciona la variable de partición como un campo en el conjunto de datos devuelto.</span><span class="sxs-lookup"><span data-stu-id="08407-220">If the TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="08407-221">Si se inserta en *&#60;nombre de base de datos>.&#60;nombre de la tabla ORC>* se producirá un error, ya que *&#60;nombre de base de datos>.&#60;nombre de la tabla ORC>* no tiene la variable de partición como un campo en el esquema de tabla.</span><span class="sxs-lookup"><span data-stu-id="08407-221">Inserting it into the *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="08407-222">En este caso, los usuarios deben seleccionar específicamente los campos que se van a insertar en *&#60;nombre de base de datos>.&#60;nombre de la tabla ORC>* de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="08407-222">In this case, you need to specifically select the fields to be inserted to *&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="08407-223">Es seguro quitar *&#60;nombre de la tabla de archivo de texto externo>* cuando use la consulta siguiente una vez insertados todos los datos en *&#60;nombre de base de datos>.&#60;nombre de la tabla ORC>*:</span><span class="sxs-lookup"><span data-stu-id="08407-223">It is safe to drop the *&#60;external textfile table name>* when using the following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="08407-224">Después de seguir este procedimiento, debe tener una tabla con datos en el formato ORC lista para su uso.</span><span class="sxs-lookup"><span data-stu-id="08407-224">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  
