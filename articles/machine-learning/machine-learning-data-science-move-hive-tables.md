---
title: aaaCreate tablas de Hive y cargar datos desde almacenamiento de blobs de Azure | Documentos de Microsoft
description: Crear tablas de Hive y cargar datos en tablas de toohive de blob
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
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="b28d7-103">Creación de tablas de Hive y carga de datos desde Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="b28d7-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="b28d7-104">En este tema se presentan consultas genéricas de Hive que crean tablas de Hive y cargan datos desde Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b28d7-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="b28d7-105">También se proporciona alguna orientación acerca de las particiones de tablas de Hive y sobre cómo utilizar Hola optimizado fila columnas (ORC) formato tooimprove rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="b28d7-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="b28d7-106">Esto **menú** vincula tootopics que describen cómo tooingest datos en entornos de destino donde se pueden almacenar y procesar durante datos Hola Hola proceso de ciencia de datos de equipo (TDSP).</span><span class="sxs-lookup"><span data-stu-id="b28d7-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="b28d7-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b28d7-107">Prerequisites</span></span>
<span data-ttu-id="b28d7-108">En este artículo se supone que ha:</span><span class="sxs-lookup"><span data-stu-id="b28d7-108">This article assumes that you have:</span></span>

* <span data-ttu-id="b28d7-109">Creado una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b28d7-109">Created an Azure storage account.</span></span> <span data-ttu-id="b28d7-110">Para obtener instrucciones, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b28d7-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="b28d7-111">Aprovisionar un clúster de Hadoop personalizado con hello servicio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b28d7-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="b28d7-112">Si necesita instrucciones, consulte [Personalización de clústeres de Hadoop de HDInsight de Azure para análisis avanzado](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b28d7-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="b28d7-113">Clúster de toohello de acceso remoto habilitado, se registran en y abre la consola de línea de comandos de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="b28d7-114">Si necesita instrucciones, consulte [Hola de acceso principal del nodo de clúster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="b28d7-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="b28d7-115">Cargar el almacenamiento de blobs de datos tooAzure</span><span class="sxs-lookup"><span data-stu-id="b28d7-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="b28d7-116">Si ha creado una máquina virtual de Azure siguiendo las instrucciones de hello proporcionadas en [configurar una máquina virtual de Azure para análisis avanzado](machine-learning-data-science-setup-virtual-machine.md), el archivo de script debería haber sido descargado toohello *C:\\ Los usuarios\\\<nombre de usuario\>\\documentos\\secuencias de comandos de ciencia de datos* directorio en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="b28d7-117">Estas consultas de Hive solo requieren que conecte en su propio esquema de datos y la configuración de almacenamiento de blobs de Azure en hello campos correspondientes toobe listo para el envío.</span><span class="sxs-lookup"><span data-stu-id="b28d7-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="b28d7-118">Se supone que los datos de Hola para las tablas de subárbol están en un **sin comprimir** formato tabular, y que los datos de hello ha sido cargado predeterminado de toohello (o tooan adicional) contenedor de hello cuenta de almacenamiento utilizado por el clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="b28d7-119">Si desea que toopractice en hello **NYC Taxi recorridos datos**, necesita:</span><span class="sxs-lookup"><span data-stu-id="b28d7-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="b28d7-120">**descargar** Hola 24 [NYC Taxi recorridos datos](http://www.andresmh.com/nyctaxitrips) archivos (12 archivos de ida y vuelta y 12 archivos tarifa),</span><span class="sxs-lookup"><span data-stu-id="b28d7-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="b28d7-121">**Descomprima** todos los archivos en archivos .csv.</span><span class="sxs-lookup"><span data-stu-id="b28d7-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="b28d7-122">**cargar** ellos predeterminado toohello (o contenedor adecuado) de Hola cuenta de almacenamiento de Azure que se creó mediante el procedimiento de hello descrito en hello [para el proceso de análisis avanzado y la tecnología de clústeres de Hadoop de HDInsight de Azure de personalizar ](machine-learning-data-science-customize-hadoop-cluster.md) tema.</span><span class="sxs-lookup"><span data-stu-id="b28d7-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="b28d7-123">Hola proceso tooupload Hola .csv archivos toohello contenedor predeterminado en la cuenta de almacenamiento de hello puede encontrarse en el objeto [página](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="b28d7-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="b28d7-124"><a name="submit"></a>¿Cómo toosubmit consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="b28d7-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="b28d7-125">Las consultas de subárbol se pueden enviar mediante:</span><span class="sxs-lookup"><span data-stu-id="b28d7-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="b28d7-126">Enviar consultas de Hive a través de línea de comandos de Hadoop en el nodo principal del clúster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="b28d7-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="b28d7-127">Enviar consultas de Hive con hello Editor de Hive</span><span class="sxs-lookup"><span data-stu-id="b28d7-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="b28d7-128">Enviar consultas de Hive con los comandos de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b28d7-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="b28d7-129">Las consultas de Hive son similares a SQL.</span><span class="sxs-lookup"><span data-stu-id="b28d7-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="b28d7-130">Si está familiarizado con SQL, es posible hello [Hive para hoja de referencia rápida de los usuarios de SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) útil.</span><span class="sxs-lookup"><span data-stu-id="b28d7-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="b28d7-131">Al enviar una consulta de Hive, también puede controlar el destino de Hola de salida de hello de las consultas de Hive, ya sea en la pantalla o tooa archivo local de hello en el nodo principal de Hola o tooan blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="b28d7-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="b28d7-132"><a name="headnode"></a> 1. Enviar consultas de Hive a través de línea de comandos de Hadoop en el nodo principal del clúster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="b28d7-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="b28d7-133">Si Hola Hive consulta es compleja, enviar que directamente en el nodo principal de Hola de clúster de Hadoop de hello conduce normalmente a su vez toofaster alrededor de envío con un Editor de Hive o secuencias de comandos de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="b28d7-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="b28d7-134">Inicie sesión en toohello nodo principal del clúster de Hadoop de hello, abra Hola línea de comandos de Hadoop en el escritorio de hello del nodo principal de Hola y escriba el comando `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="b28d7-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="b28d7-135">Tiene consultas de Hive de tres maneras toosubmit Hola línea de comandos de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="b28d7-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="b28d7-136">Directamente</span><span class="sxs-lookup"><span data-stu-id="b28d7-136">directly</span></span>
* <span data-ttu-id="b28d7-137">usando archivos .hql</span><span class="sxs-lookup"><span data-stu-id="b28d7-137">using .hql files</span></span>
* <span data-ttu-id="b28d7-138">con hello Hive consola de comandos</span><span class="sxs-lookup"><span data-stu-id="b28d7-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="b28d7-139">Envíe consultas de subárbol directamente en la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b28d7-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="b28d7-140">Puede ejecutar el comando como `hive -e "<your hive query>;` toosubmit consultas sencillas de Hive directamente en Hadoop línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="b28d7-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="b28d7-141">Este es un ejemplo, donde hello rojo un contorno alrededor Hola comando que envía la consulta de Hive de Hola y Hola recuadro verde contornos Hola resultados de consulta de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="b28d7-143">Enviar consultas de subárbol en archivos .hql</span><span class="sxs-lookup"><span data-stu-id="b28d7-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="b28d7-144">Cuando la consulta de Hive hello es más complicado y tiene varias líneas, la modificación de consultas en la línea de comandos o la consola de comandos de Hive no resulta práctico.</span><span class="sxs-lookup"><span data-stu-id="b28d7-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="b28d7-145">Una alternativa es toouse un editor de texto en el nodo principal de Hola de consultas de Hive de hello toosave clúster de Hadoop hello en un archivo .hql en un directorio local del nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="b28d7-146">A continuación, la consulta de Hive hello en el archivo de hello .hql puede enviarse mediante hello `-f` argumento tal como sigue:</span><span class="sxs-lookup"><span data-stu-id="b28d7-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="b28d7-148">**Suprimir la impresión de pantalla del estado de progreso de las consultas de subárbol**</span><span class="sxs-lookup"><span data-stu-id="b28d7-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="b28d7-149">De forma predeterminada, una vez enviada en línea de comandos de Hadoop, en la consulta de Hive progreso de Hola de trabajo de asignación y reducción de Hola se imprime en pantalla.</span><span class="sxs-lookup"><span data-stu-id="b28d7-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="b28d7-150">toosuppress Hola imprimir pantalla de progreso del trabajo de asignación y reducción de hello, puede usar un argumento `-S` ("S" en mayúsculas) en hello línea de comandos como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b28d7-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="b28d7-151">.</span><span class="sxs-lookup"><span data-stu-id="b28d7-151">.</span></span>    <span data-ttu-id="b28d7-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="b28d7-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="b28d7-153">Envíe consultas de subárbol en la consola de comandos de subárbol.</span><span class="sxs-lookup"><span data-stu-id="b28d7-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="b28d7-154">En primer lugar también puede escribir consola de comandos del subárbol de hello mediante la ejecución de comando `hive` en línea de comandos de Hadoop y, a continuación, enviar consultas de Hive en la consola de comandos de Hive.</span><span class="sxs-lookup"><span data-stu-id="b28d7-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="b28d7-155">Aquí tiene un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b28d7-155">Here is an example.</span></span> <span data-ttu-id="b28d7-156">En este ejemplo, hello dos cuadros rojos resaltado Hola comandos usados tooenter Hola consola de comandos de Hive y Hola consulta de Hive enviada en la consola de comandos de Hive, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b28d7-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="b28d7-157">cuadro de Hello verde resalta la salida de hello de consulta de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-157">hello green box highlights hello output from hello Hive query.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="b28d7-159">en los ejemplos anteriores Hola directamente resultados Hola Hive consulta en pantalla.</span><span class="sxs-lookup"><span data-stu-id="b28d7-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="b28d7-160">También puede escribir tooa de archivo local en el nodo principal de Hola o tooan blobs de Azure para la salida Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="b28d7-161">A continuación, puede usar otras herramientas toofurther analizar la salida de hello de consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="b28d7-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="b28d7-162">**Salida de archivo local de tooa de resultados de consulta de Hive.**</span><span class="sxs-lookup"><span data-stu-id="b28d7-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="b28d7-163">toooutput Hive consultar resultados tooa local en el directorio en el nodo principal de hello, tiene consulta de Hive toosubmit Hola Hola línea de comandos de Hadoop como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b28d7-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="b28d7-164">En el siguiente ejemplo de Hola, se escribe la salida de hello de consulta de Hive en un archivo `hivequeryoutput.txt` en el directorio `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="b28d7-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="b28d7-166">**Salida tooan de resultados de consulta de Hive blobs de Azure**</span><span class="sxs-lookup"><span data-stu-id="b28d7-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="b28d7-167">También puede generar Hola Hive consulta resultados tooan blob de Azure, dentro de contenedor de hello predeterminado del clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="b28d7-168">consulta de Hive de Hola para esto es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="b28d7-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="b28d7-169">En el siguiente ejemplo de Hola, salida de hello de consulta de Hive se escribe el directorio de blob tooa `queryoutputdir` dentro de contenedor de hello predeterminado del clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="b28d7-170">En este caso, solo necesita tooprovide nombre del directorio hello, sin nombre de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="b28d7-171">Se produce un error si proporciona los nombres de directorio y de blob, como `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="b28d7-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="b28d7-173">Si abre el contenedor predeterminado de Hola de clúster de Hadoop de hello mediante el Explorador de almacenamiento de Azure, puede ver la salida de hello de consulta de Hive Hola tal y como se muestra en la figura siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="b28d7-174">Puede aplicar Hola filtro (resaltado mediante cuadro rojo) tooonly recuperar Hola blob con letras especificadas en los nombres.</span><span class="sxs-lookup"><span data-stu-id="b28d7-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="b28d7-176"><a name="hive-editor"></a> 2. Enviar consultas de Hive con hello Editor de Hive</span><span class="sxs-lookup"><span data-stu-id="b28d7-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="b28d7-177">También puede utilizar Hola consola de consultas (Editor de Hive) mediante la especificación de una dirección URL de formulario de hello *https://&#60; Nombre del clúster de Hadoop >.azurehdinsight.net/Home/HiveEditor* en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="b28d7-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="b28d7-178">Debe ser iniciado en hello, vea esta consola y por lo que necesita las credenciales de clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b28d7-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="b28d7-179"><a name="ps"></a> 3. Enviar consultas de Hive con los comandos de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b28d7-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="b28d7-180">También puede utilizar consultas de Hive toosubmit de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b28d7-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="b28d7-181">Para obtener instrucciones, consulte [Envío de trabajos de Hive mediante PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b28d7-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="b28d7-182"><a name="create-tables"></a>Creación de tablas y base de datos de Hive</span><span class="sxs-lookup"><span data-stu-id="b28d7-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="b28d7-183">Hello consultas de Hive compartidas hello [repositorio de GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) y puede descargarse desde allí.</span><span class="sxs-lookup"><span data-stu-id="b28d7-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="b28d7-184">Aquí es la consulta de Hive de Hola que crea una tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="b28d7-184">Here is hello Hive query that creates a Hive table.</span></span>

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

<span data-ttu-id="b28d7-185">Estas son las descripciones de Hola de campos de Hola que necesite tooplug en y otras configuraciones:</span><span class="sxs-lookup"><span data-stu-id="b28d7-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="b28d7-186">**&#60; nombre de base de datos >**: nombre de Hola de base de datos de Hola que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="b28d7-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="b28d7-187">Si su intención es base de datos predeterminada de toouse hello, Hola consulta *crear base de datos...*  puede omitirse.</span><span class="sxs-lookup"><span data-stu-id="b28d7-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="b28d7-188">**&#60; nombre de tabla >**: nombre de Hola de tabla de Hola que desea toocreate dentro de la base de datos especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="b28d7-189">Si desea que la base de datos predeterminada de toouse hello, tabla de hello puede hacer referencia directamente mediante *&#60; nombre de tabla >* sin &#60; nombre de base de datos >.</span><span class="sxs-lookup"><span data-stu-id="b28d7-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="b28d7-190">**&#60; separador de campos >**: separador de Hola que delimita los campos de toobe de archivo de datos de hello cargado toohello tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="b28d7-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="b28d7-191">**&#60; separador de línea >**: separador de Hola que delimita las líneas en el archivo de datos de hello.</span><span class="sxs-lookup"><span data-stu-id="b28d7-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="b28d7-192">**&#60; ubicación de almacenamiento >**: Hola datos de almacenamiento de Azure ubicación toosave Hola de tablas de Hive.</span><span class="sxs-lookup"><span data-stu-id="b28d7-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="b28d7-193">Si no se especifica *ubicación &#60; ubicación de almacenamiento >*, Hola base de datos y tablas hello se almacenan una en *hive/almacenamiento/* directorio en el contenedor de hello predeterminado del clúster de Hive Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b28d7-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="b28d7-194">Si desea que la ubicación de almacenamiento de toospecify hello, ubicación de almacenamiento de hello tiene toobe dentro de contenedor de hello predeterminado para la base de datos de Hola y tablas.</span><span class="sxs-lookup"><span data-stu-id="b28d7-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="b28d7-195">Esta ubicación tiene toobe hace referencia como contenedor de ubicación relativa toohello predeterminado del clúster de hello en formato de Hola de *' wasb: / / / &#60; directorio 1 > /'* o *' wasb: / / / &#60; directorio 1 > / &#60; directorio 2 > /'*, etcetera. Cuando se ejecuta la consulta de hello, directorios relativa Hola se crean dentro del contenedor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="b28d7-196">**TBLPROPERTIES("Skip.Header.Line.Count"="1")**: si el archivo de datos de hello tiene una línea de encabezado, tienen tooadd esta propiedad **final hello** de hello *crear tabla* consulta.</span><span class="sxs-lookup"><span data-stu-id="b28d7-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="b28d7-197">En caso contrario, se carga la línea de encabezado de hello como una tabla de registro toohello.</span><span class="sxs-lookup"><span data-stu-id="b28d7-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="b28d7-198">Si el archivo de datos de hello no tiene una línea de encabezado, se puede omitir esta configuración en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="b28d7-199"><a name="load-data"></a>Cargar datos tooHive tablas</span><span class="sxs-lookup"><span data-stu-id="b28d7-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="b28d7-200">Aquí es la consulta de Hive de Hola que carga datos en una tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="b28d7-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="b28d7-201">**&#60; datos de ruta de acceso tooblob >**: Hola si Hola blob archivo toobe cargado toohello Hive tabla está en el contenedor de predeterminado de Hola de hello clúster de Hadoop de HDInsight, *&#60; datos de ruta de acceso tooblob >* debe estar en formato de Hola *' wasb: / / / &#60; directorio de este contenedor > / &#60; nombre de archivo de blob >'*.</span><span class="sxs-lookup"><span data-stu-id="b28d7-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="b28d7-202">archivo de blob de Hello también puede estar en un contenedor adicional de hello clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b28d7-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="b28d7-203">En este caso, *&#60; datos de ruta de acceso tooblob >* debe estar en formato de hello *' wasb: / / &#60; nombre de contenedor > @&#60; nombre de la cuenta de almacenamiento >.blob.core.windows.net/ &#60; nombre de archivo de blob >'*.</span><span class="sxs-lookup"><span data-stu-id="b28d7-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b28d7-204">Hello toobe cargado tooHive tabla de datos de blob tiene toobe en predeterminado de Hola o contenedor adicional de la cuenta de almacenamiento de hello para el clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="b28d7-205">En caso contrario, Hola *carga datos* consulta produce un error que indica que el que no se puede tener acceso a datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="b28d7-206"><a name="partition-orc"></a>Temas avanzados: tabla con particiones y datos de Hive de almacén en formato ORC</span><span class="sxs-lookup"><span data-stu-id="b28d7-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="b28d7-207">Si hello es grande, creación de particiones de tabla de hello es beneficioso para las consultas que solo necesitan tooscan algunas particiones de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="b28d7-208">Por ejemplo, son datos de registro de hello toopartition razonable de un sitio web por fechas.</span><span class="sxs-lookup"><span data-stu-id="b28d7-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="b28d7-209">En suma toopartitioning Hive tablas, así como datos de Hive de hello toostore beneficioso en formato de optimizado fila columnas (ORC) de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="b28d7-210">Para obtener más información acerca de la aplicación de formato ORC, consulte <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">El uso de archivos ORC mejora el rendimiento cuando Hive está leyendo, escribiendo y procesando datos</a>.</span><span class="sxs-lookup"><span data-stu-id="b28d7-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="b28d7-211">Tabla con particiones</span><span class="sxs-lookup"><span data-stu-id="b28d7-211">Partitioned table</span></span>
<span data-ttu-id="b28d7-212">Aquí es la consulta de Hive de Hola que crea una tabla con particiones y carga datos en él.</span><span class="sxs-lookup"><span data-stu-id="b28d7-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="b28d7-213">Al consultar tablas con particiones, se recomienda tooadd condición de partición Hola Hola **principio** de hello `where` cláusula que esta mejora la eficacia de Hola de búsqueda de forma significativa.</span><span class="sxs-lookup"><span data-stu-id="b28d7-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="b28d7-214"><a name="orc"></a>Almacenamiento de datos de Hive en formato ORC</span><span class="sxs-lookup"><span data-stu-id="b28d7-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="b28d7-215">No se puede cargar directamente datos desde almacenamiento de blobs en tablas de subárbol que se almacena en formato de hello ORC.</span><span class="sxs-lookup"><span data-stu-id="b28d7-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="b28d7-216">Estos son los pasos de hello tablas tooHive almacenadas en formato ORC los blobs en ese Hola necesita tootake tooload datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b28d7-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="b28d7-217">Cree una tabla externa **almacenados archivo de texto de AS** y cargar datos de tabla de toohello de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="b28d7-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

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

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="b28d7-218">Crear una tabla interna con hello mismo esquema que la tabla externa de hello en el paso 1, con hello mismo el delimitador de campo y almacenar Hola datos de Hive en formato de hello ORC.</span><span class="sxs-lookup"><span data-stu-id="b28d7-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="b28d7-219">Seleccionar datos de la tabla externa de hello en el paso 1 e insertar en la tabla de hello ORC</span><span class="sxs-lookup"><span data-stu-id="b28d7-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="b28d7-220">Si tabla del archivo de texto hello *&#60; nombre de base de datos >. &#60; nombre de la tabla de archivo de texto externo >* tiene particiones, en el paso 3, hello `SELECT * FROM <database name>.<external textfile table name>` comando selecciona Hola variable de partición como un campo de hello devuelve el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="b28d7-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="b28d7-221">Insertándolo en hello *&#60; nombre de base de datos >. &#60; nombre de la tabla ORC >* se produce un error desde *&#60; nombre de base de datos >. &#60; nombre de la tabla ORC >* no tiene la variable de la partición de Hola como un campo de esquema de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b28d7-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="b28d7-222">En este caso, deberá toospecifically Hola seleccione campos toobe insertar demasiado*&#60; nombre de base de datos >. &#60; nombre de la tabla ORC >* como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b28d7-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="b28d7-223">Es seguro toodrop hello *&#60; nombre de la tabla de archivo de texto externo >* cuando Hola después de consulta después de todos los datos de uso se ha insertado en *&#60; nombre de base de datos >. &#60; nombre de la tabla ORC >*:</span><span class="sxs-lookup"><span data-stu-id="b28d7-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="b28d7-224">Después de seguir este procedimiento, debe tener una tabla con datos en hello ORC formato listo toouse.</span><span class="sxs-lookup"><span data-stu-id="b28d7-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  
