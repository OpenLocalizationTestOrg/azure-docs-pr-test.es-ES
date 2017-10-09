---
title: datos de aaaUpload para trabajos de Hadoop en HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooupload y acceso a datos para los trabajos de Hadoop en HDInsight utilizando Hola CLI de Azure, el Explorador de almacenamiento de Azure, Azure PowerShell, línea de comandos de Hadoop de Hola o Sqoop."
keywords: "extracción, transformación y carga de datos de hadoop, obtención de datos en hadoop, carga de datos de hadoop"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="d700d-104">Carga de datos para trabajos de Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d700d-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="d700d-105">HDInsight de Azure ofrece un sistema de archivos distribuido de Hadoop (HDFS) completo a través del servicio de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="d700d-106">Está diseñado como un tooprovide de extensión HDFS una perfecta experiencia toocustomers.</span><span class="sxs-lookup"><span data-stu-id="d700d-106">It is designed as an HDFS extension tooprovide a seamless experience toocustomers.</span></span> <span data-ttu-id="d700d-107">Habilita Hola conjunto completo de componentes de hello Hadoop ecosistema toooperate directamente en los datos de Hola que administra.</span><span class="sxs-lookup"><span data-stu-id="d700d-107">It enables hello full set of components in hello Hadoop ecosystem toooperate directly on hello data it manages.</span></span> <span data-ttu-id="d700d-108">El almacenamiento de blobs de Azure y HDFS son sistemas de archivos diferentes que se han optimizado para el almacenamiento de datos y el cálculo en ellos.</span><span class="sxs-lookup"><span data-stu-id="d700d-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="d700d-109">Para obtener información acerca de las ventajas de hello del uso de almacenamiento de blobs de Azure, consulte [almacenamiento de blobs de Azure de uso con HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="d700d-109">For information about hello benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="d700d-110">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="d700d-110">**Prerequisites**</span></span>

<span data-ttu-id="d700d-111">Tenga en cuenta Hola siguiente requisito antes de empezar:</span><span class="sxs-lookup"><span data-stu-id="d700d-111">Note hello following requirement before you begin:</span></span>

* <span data-ttu-id="d700d-112">Un clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="d700d-113">Para obtener instrucciones, consulte [Introducción a HDInsight de Azure][hdinsight-get-started] o [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="d700d-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="d700d-114">Motivos para almacenar blobs</span><span class="sxs-lookup"><span data-stu-id="d700d-114">Why blob storage?</span></span>
<span data-ttu-id="d700d-115">Suelen ser clústeres de HDInsight de Azure implementa toorun trabajos de MapReduce y clústeres de Hola se quitan después de completan estos trabajos.</span><span class="sxs-lookup"><span data-stu-id="d700d-115">Azure HDInsight clusters are typically deployed toorun MapReduce jobs, and hello clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="d700d-116">Mantener datos de hello en clústeres HDFS hello cuando finalicen los cálculos sería un toostore forma costosa estos datos.</span><span class="sxs-lookup"><span data-stu-id="d700d-116">Keeping hello data in hello HDFS clusters after computations are complete would be an expensive way toostore this data.</span></span> <span data-ttu-id="d700d-117">Almacenamiento de blobs de Azure es una alta disponibilidad, altamente escalable y de alta capacidad, la opción de almacenamiento de bajo costo y pueden compartirse para datos que están toobe procesada con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d700d-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is toobe processed using HDInsight.</span></span> <span data-ttu-id="d700d-118">Almacenar datos en un blob permite clústeres de HDInsight de Hola que sirven para toobe cálculo publicado sin ningún riesgo sin pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="d700d-118">Storing data in a blob enables hello HDInsight clusters that are used for computation toobe safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="d700d-119">Directorios</span><span class="sxs-lookup"><span data-stu-id="d700d-119">Directories</span></span>
<span data-ttu-id="d700d-120">Los contenedores del almacenamiento de blobs de Azure almacenan los datos como pares de clave/valor y no hay jerarquía de directorios.</span><span class="sxs-lookup"><span data-stu-id="d700d-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="d700d-121">Sin embargo Hola "/" caracteres pueden usarse en toomake de nombre de clave de hello parece como si un archivo se almacena en una estructura de directorios.</span><span class="sxs-lookup"><span data-stu-id="d700d-121">However hello "/" character can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="d700d-122">HDInsight los ve como si fueran directorios reales.</span><span class="sxs-lookup"><span data-stu-id="d700d-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="d700d-123">Por ejemplo, la clave de un blob puede ser *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="d700d-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="d700d-124">No existe ningún directorio de "entrada" real, pero debido a toohello presencia de hello carácter "/" en el nombre de clave de hello, tiene el aspecto de Hola de una ruta de acceso de archivo.</span><span class="sxs-lookup"><span data-stu-id="d700d-124">No actual "input" directory exists, but due toohello presence of hello "/" character in hello key name, it has hello appearance of a file path.</span></span>

<span data-ttu-id="d700d-125">Por eso, si usa las herramientas de Azure Explorer, puede que vea algunos archivos de 0 bytes.</span><span class="sxs-lookup"><span data-stu-id="d700d-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="d700d-126">Estos archivos tienen dos propósitos:</span><span class="sxs-lookup"><span data-stu-id="d700d-126">These files serve two purposes:</span></span>

* <span data-ttu-id="d700d-127">Si hay carpetas vacías, marcadas de existencia de Hola de carpeta Hola.</span><span class="sxs-lookup"><span data-stu-id="d700d-127">If there are empty folders, they mark of hello existence of hello folder.</span></span> <span data-ttu-id="d700d-128">Almacenamiento de blobs de Azure es lo suficientemente inteligente tooknow que si existe un blob denominado foo/barra, hay una carpeta denominada **foo**.</span><span class="sxs-lookup"><span data-stu-id="d700d-128">Azure Blob storage is clever enough tooknow that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="d700d-129">Pero Hola toosignify de manera única una carpeta vacía denominada **foo** es tener este archivo especial 0 bytes en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d700d-129">But hello only way toosignify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="d700d-130">Contienen metadatos especial que es necesitan por hello Hadoop file systems, en particular los permisos de Hola y los propietarios de carpetas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d700d-130">They hold special metadata that is needed by hello Hadoop file system, notably hello permissions and owners for hello folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="d700d-131">Utilidades de la ea de comandos</span><span class="sxs-lookup"><span data-stu-id="d700d-131">Command-line utilities</span></span>
<span data-ttu-id="d700d-132">Microsoft proporciona Hola siguientes utilidades toowork con almacenamiento de blobs de Azure:</span><span class="sxs-lookup"><span data-stu-id="d700d-132">Microsoft provides hello following utilities toowork with Azure Blob storage:</span></span>

| <span data-ttu-id="d700d-133">Herramienta</span><span class="sxs-lookup"><span data-stu-id="d700d-133">Tool</span></span> | <span data-ttu-id="d700d-134">Linux</span><span class="sxs-lookup"><span data-stu-id="d700d-134">Linux</span></span> | <span data-ttu-id="d700d-135">OS X</span><span class="sxs-lookup"><span data-stu-id="d700d-135">OS X</span></span> | <span data-ttu-id="d700d-136">Windows</span><span class="sxs-lookup"><span data-stu-id="d700d-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="d700d-137">[Interfaz de la línea de comandos de Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="d700d-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="d700d-138">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-138">✔</span></span> |<span data-ttu-id="d700d-139">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-139">✔</span></span> |<span data-ttu-id="d700d-140">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-140">✔</span></span> |
| <span data-ttu-id="d700d-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="d700d-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="d700d-142">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-142">✔</span></span> |
| <span data-ttu-id="d700d-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="d700d-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="d700d-144">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-144">✔</span></span> |
| [<span data-ttu-id="d700d-145">Línea de comandos de Hadoop</span><span class="sxs-lookup"><span data-stu-id="d700d-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="d700d-146">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-146">✔</span></span> |<span data-ttu-id="d700d-147">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-147">✔</span></span> |<span data-ttu-id="d700d-148">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="d700d-149">Mientras Hola CLI de Azure y Azure PowerShell, AzCopy todos pueden usarse desde fuera de Azure, hello Hadoop comando solo está disponible en el clúster de HDInsight de Hola y solo permite cargar datos de sistema de archivos local de hello en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-149">While hello Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, hello Hadoop command is only available on hello HDInsight cluster and only allows loading data from hello local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="d700d-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d700d-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="d700d-151">Hola CLI de Azure es una herramienta de multiplataforma que le permite toomanage Azure servicios.</span><span class="sxs-lookup"><span data-stu-id="d700d-151">hello Azure CLI is a cross-platform tool that allows you toomanage Azure services.</span></span> <span data-ttu-id="d700d-152">Usar hello siguiendo el almacenamiento de blobs de pasos tooupload datos tooAzure:</span><span class="sxs-lookup"><span data-stu-id="d700d-152">Use hello following steps tooupload data tooAzure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="d700d-153">[Instalar y configurar Hola CLI de Azure para Mac, Linux y Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d700d-153">[Install and configure hello Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="d700d-154">Abra un símbolo del sistema, bash u otro shell y usar hello después tooauthenticate tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-154">Open a command prompt, bash, or other shell, and use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

    <span data-ttu-id="d700d-155">Cuando se le solicite, escriba Hola nombre de usuario y una contraseña para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="d700d-155">When prompted, enter hello user name and password for your subscription.</span></span>
3. <span data-ttu-id="d700d-156">Escriba Hola después cuentas de almacenamiento de comando toolist Hola para su suscripción:</span><span class="sxs-lookup"><span data-stu-id="d700d-156">Enter hello following command toolist hello storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="d700d-157">Seleccionar cuenta de almacenamiento de Hola que contiene datos de blob de Hola que desee toowork con y luego use Hola después la tecla de comando tooretrieve Hola para esta cuenta:</span><span class="sxs-lookup"><span data-stu-id="d700d-157">Select hello storage account that contains hello blob you want toowork with, then use hello following command tooretrieve hello key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="d700d-158">Esto debería devolver las claves **Principal** y **Secundaria**.</span><span class="sxs-lookup"><span data-stu-id="d700d-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="d700d-159">Hola copia **principal** valor de clave porque se usará en pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d700d-159">Copy hello **Primary** key value because it will be used in hello next steps.</span></span>
5. <span data-ttu-id="d700d-160">Usar hello después comando tooretrieve una lista de contenedores de blob dentro de la cuenta de almacenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="d700d-160">Use hello following command tooretrieve a list of blob containers within hello storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="d700d-161">Usar hello después tooupload de comandos y descargar archivos toohello blob:</span><span class="sxs-lookup"><span data-stu-id="d700d-161">Use hello following commands tooupload and download files toohello blob:</span></span>

   * <span data-ttu-id="d700d-162">tooupload un archivo:</span><span class="sxs-lookup"><span data-stu-id="d700d-162">tooupload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="d700d-163">toodownload un archivo:</span><span class="sxs-lookup"><span data-stu-id="d700d-163">toodownload a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="d700d-164">Si siempre trabajará con hello misma cuenta de almacenamiento, puede establecer Hola después de las variables de entorno en lugar de especificar la cuenta de Hola y de clave para cada comando:</span><span class="sxs-lookup"><span data-stu-id="d700d-164">If you will always be working with hello same storage account, you can set hello following environment variables instead of specifying hello account and key for every command:</span></span>
>
> * <span data-ttu-id="d700d-165">**AZURE\_almacenamiento\_cuenta**: nombre de cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="d700d-165">**AZURE\_STORAGE\_ACCOUNT**: hello storage account name</span></span>
> * <span data-ttu-id="d700d-166">**AZURE\_almacenamiento\_acceso\_clave**: clave de cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="d700d-166">**AZURE\_STORAGE\_ACCESS\_KEY**: hello storage account key</span></span>
>
>

### <span data-ttu-id="d700d-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d700d-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="d700d-168">Azure PowerShell es un entorno de scripting que puede usar toocontrol y automatizar la implementación de Hola y administración de las cargas de trabajo en Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-168">Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="d700d-169">Para obtener información acerca de cómo configurar su toorun de estación de trabajo Azure PowerShell, consulte [instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d700d-169">For information about configuring your workstation toorun Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="d700d-170">**tooupload un almacenamiento de blobs de tooAzure de archivos local**</span><span class="sxs-lookup"><span data-stu-id="d700d-170">**tooupload a local file tooAzure Blob storage**</span></span>

1. <span data-ttu-id="d700d-171">Consola de Azure PowerShell Hola abiertos como se indica en [instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d700d-171">Open hello Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="d700d-172">Establecer valores de hello de hello cinco primeras variables en hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="d700d-172">Set hello values of hello first five variables in hello following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="d700d-173">Hola pegar en hello Azure PowerShell consola toorun se toocopy Hola los archivos de scripts.</span><span class="sxs-lookup"><span data-stu-id="d700d-173">Paste hello script into hello Azure PowerShell console toorun it toocopy hello file.</span></span>

<span data-ttu-id="d700d-174">Por ejemplo PowerShell toowork de scripts creados con HDInsight, vea [herramientas de HDInsight](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="d700d-174">For example PowerShell scripts created toowork with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="d700d-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="d700d-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="d700d-176">AzCopy es una herramienta de línea de comandos que se haya diseñado toosimplify Hola tarea de transferencia de datos dentro y fuera de una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-176">AzCopy is a command-line tool that is designed toosimplify hello task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="d700d-177">Puede usarla como una herramienta independiente o incorporarla a una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="d700d-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="d700d-178">[Descarga de AzCopy][azure-azcopy-download]</span><span class="sxs-lookup"><span data-stu-id="d700d-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="d700d-179">Hola AzCopy sintaxis es:</span><span class="sxs-lookup"><span data-stu-id="d700d-179">hello AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="d700d-180">Para obtener más información, consulte [AzCopy: carga y descarga de archivos para blobs de Azure][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="d700d-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="d700d-181"><a id="commandline"></a>Línea de comandos de Hadoop</span><span class="sxs-lookup"><span data-stu-id="d700d-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="d700d-182">línea de comandos de Hadoop de Hello sólo es útil para almacenar datos en el almacenamiento de blobs al datos Hola ya están presentes en el nodo principal del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="d700d-182">hello Hadoop command line is only useful for storing data into blob storage when hello data is already present on hello cluster head node.</span></span>

<span data-ttu-id="d700d-183">Hola de orden toouse Hadoop comando, debe conectarse primero nodo principal de toohello mediante uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="d700d-183">In order toouse hello Hadoop command, you must first connect toohello headnode using one of hello following methods:</span></span>

* <span data-ttu-id="d700d-184">**HDInsight para Windows**: [conectar mediante Escritorio remoto](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="d700d-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="d700d-185">**HDInsight basados en Linux**: conectarse a través de SSH ([Hola comando SSH](hdinsight-hadoop-linux-use-ssh-unix.md) o [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="d700d-185">**Linux-based HDInsight**: Connect using SSH ([hello SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="d700d-186">Una vez conectado, puede usar Hola después tooupload sintaxis toostorage de un archivo.</span><span class="sxs-lookup"><span data-stu-id="d700d-186">Once connected, you can use hello following syntax tooupload a file toostorage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="d700d-187">Por ejemplo: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="d700d-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="d700d-188">Como sistema de archivos predeterminado de Hola para HDInsight está en almacenamiento de blobs de Azure, /example/data.txt aparece realmente en almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-188">Because hello default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="d700d-189">También puede consultar el archivo toohello como:</span><span class="sxs-lookup"><span data-stu-id="d700d-189">You can also refer toohello file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="d700d-190">o</span><span class="sxs-lookup"><span data-stu-id="d700d-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="d700d-191">Para obtener una lista de otros comandos de Hadoop que funcionan con archivos, consulte [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="d700d-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="d700d-192">En los clústeres de HBase, tamaño de bloque predeterminado de hello usa al escribir los datos es de 256KB.</span><span class="sxs-lookup"><span data-stu-id="d700d-192">On HBase clusters, hello default block size used when writing data is 256KB.</span></span> <span data-ttu-id="d700d-193">Si bien esto funciona bien cuando se usa la API de REST o HBase APIs, utilizando hello `hadoop` o `hdfs dfs` datos de toowrite de comandos mayores de GB de ~ 12 genera un error.</span><span class="sxs-lookup"><span data-stu-id="d700d-193">While this works fine when using HBase APIs or REST APIs, using hello `hadoop` or `hdfs dfs` commands toowrite data larger than ~12GB results in an error.</span></span> <span data-ttu-id="d700d-194">Vea hello [excepción de almacenamiento para la operación de escritura en el blob](#storageexception) sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="d700d-194">See hello [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="d700d-195">Clientes gráficos</span><span class="sxs-lookup"><span data-stu-id="d700d-195">Graphical clients</span></span>
<span data-ttu-id="d700d-196">También hay varias aplicaciones que proporcionan una interfaz gráfica para trabajar con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="d700d-197">Hola te mostramos una lista de algunas de estas aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="d700d-197">hello following is a list of a few of these applications:</span></span>

| <span data-ttu-id="d700d-198">Cliente</span><span class="sxs-lookup"><span data-stu-id="d700d-198">Client</span></span> | <span data-ttu-id="d700d-199">Linux</span><span class="sxs-lookup"><span data-stu-id="d700d-199">Linux</span></span> | <span data-ttu-id="d700d-200">OS X</span><span class="sxs-lookup"><span data-stu-id="d700d-200">OS X</span></span> | <span data-ttu-id="d700d-201">Windows</span><span class="sxs-lookup"><span data-stu-id="d700d-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="d700d-202">Microsoft Visual Studio Tools para HDInsight</span><span class="sxs-lookup"><span data-stu-id="d700d-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="d700d-203">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-203">✔</span></span> |<span data-ttu-id="d700d-204">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-204">✔</span></span> |<span data-ttu-id="d700d-205">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-205">✔</span></span> |
| [<span data-ttu-id="d700d-206">Explorador de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d700d-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="d700d-207">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-207">✔</span></span> |<span data-ttu-id="d700d-208">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-208">✔</span></span> |<span data-ttu-id="d700d-209">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-209">✔</span></span> |
| [<span data-ttu-id="d700d-210">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="d700d-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="d700d-211">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-211">✔</span></span> |
| [<span data-ttu-id="d700d-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="d700d-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="d700d-213">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-213">✔</span></span> |
| [<span data-ttu-id="d700d-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="d700d-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="d700d-215">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-215">✔</span></span> |
| [<span data-ttu-id="d700d-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="d700d-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="d700d-217">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-217">✔</span></span> |<span data-ttu-id="d700d-218">✔</span><span class="sxs-lookup"><span data-stu-id="d700d-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="d700d-219">Visual Studio Tools para HDInsight</span><span class="sxs-lookup"><span data-stu-id="d700d-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="d700d-220">Para obtener más información, consulte [Navigate Hola recursos vinculados](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="d700d-220">For more information, see [Navigate hello linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="d700d-221"><a id="storageexplorer"></a>Explorador de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d700d-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="d700d-222">*Explorador de almacenamiento de Azure* es una herramienta útil para inspeccionar y modificar datos de Hola de blobs.</span><span class="sxs-lookup"><span data-stu-id="d700d-222">*Azure Storage Explorer* is a useful tool for inspecting and altering hello data in blobs.</span></span> <span data-ttu-id="d700d-223">Se trata de una herramienta gratuita que se puede descargar de [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d700d-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="d700d-224">código de Hello fuente está disponible en este vínculo también.</span><span class="sxs-lookup"><span data-stu-id="d700d-224">hello source code is available from this link as well.</span></span>

<span data-ttu-id="d700d-225">Antes de usar la herramienta de hello, debe conocer la clave de nombre y la cuenta de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-225">Before using hello tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="d700d-226">Para obtener instrucciones sobre cómo obtener esta información, vea Hola "Cómo: ver, copiar y regenerar almacenamiento de claves de acceso" sección de [crear, administrar o eliminar una cuenta de almacenamiento][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="d700d-226">For instructions about getting this information, see hello "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="d700d-227">Ejecute el explorador de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d700d-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="d700d-228">Si es Hola primera vez ha ejecutado Hola Explorador de almacenamiento, se le pedirá para hello **_Storage nombre-cuenta** y **clave de la cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="d700d-228">If this is hello first time you have run hello Storage Explorer, you will be prompted for hello **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="d700d-229">Si ha ejecutado con anterioridad, usar hello **agregar** botón tooadd un nuevo nombre de cuenta de almacenamiento y la clave.</span><span class="sxs-lookup"><span data-stu-id="d700d-229">If you have run it before, use hello **Add** button tooadd a new storage account name and key.</span></span>

    <span data-ttu-id="d700d-230">Escriba Hola nombre y clave de cuenta de almacenamiento de hello utilizada por el clúster de HDInsight y, a continuación, seleccione **Guardar & Abrir**.</span><span class="sxs-lookup"><span data-stu-id="d700d-230">Enter hello name and key for hello storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="d700d-232">En lista de hello de la izquierda de toohello de contenedores de interfaz de hello, haga clic en nombre de Hola Hola del contenedor de que está asociado a su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d700d-232">In hello list of containers toohello left of hello interface, click hello name of hello container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="d700d-233">De forma predeterminada, esto es nombre Hola Hola del clúster de HDInsight, pero puede ser diferente si ha especificado un nombre específico al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="d700d-233">By default, this is hello name of hello HDInsight cluster, but may be different if you entered a specific name when creating hello cluster.</span></span>
3. <span data-ttu-id="d700d-234">Desde la barra de herramientas de hello, seleccione el icono de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="d700d-234">From hello tool bar, select hello upload icon.</span></span>

    ![Barra de herramientas con el icono de carga resaltado](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="d700d-236">Especificar un tooupload de archivo y, a continuación, haga clic en **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="d700d-236">Specify a file tooupload, and then click **Open**.</span></span> <span data-ttu-id="d700d-237">Cuando se le pida, seleccione **cargar** raíz del toohello del archivo tooupload Hola Hola del contenedor de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d700d-237">When prompted, select **Upload** tooupload hello file toohello root of hello storage container.</span></span> <span data-ttu-id="d700d-238">Si desea tooupload Hola archivo tooa ruta de acceso específica, escriba la ruta de acceso de Hola Hola **destino** campo y, a continuación, seleccione **cargar**.</span><span class="sxs-lookup"><span data-stu-id="d700d-238">If you want tooupload hello file tooa specific path, enter hello path in hello **Destination** field and then select **Upload**.</span></span>

    ![Cuadro de diálogo de carga de archivos](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="d700d-240">Una vez que ha finalizado la carga del archivo hello, puede usarlo desde trabajos en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="d700d-240">Once hello file has finished uploading, you can use it from jobs on hello HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="d700d-241">Montar el almacenamiento de blobs de Azure como unidad local</span><span class="sxs-lookup"><span data-stu-id="d700d-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="d700d-242">Vea [Montaje del almacenamiento de blobs de Azure como unidad local](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="d700d-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="d700d-243">Servicios</span><span class="sxs-lookup"><span data-stu-id="d700d-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="d700d-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d700d-244">Azure Data Factory</span></span>
<span data-ttu-id="d700d-245">Hola servicio Data Factory de Azure es un servicio completamente administrado para crear servicios de movimiento de datos, procesamiento de datos y almacenamiento de datos en las canalizaciones de producción de datos optimizado, escalable y confiable.</span><span class="sxs-lookup"><span data-stu-id="d700d-245">hello Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="d700d-246">Factoría de datos de Azure pueden ser datos de toomove usado en el almacenamiento de blobs de Azure, o toocreate las canalizaciones de datos que utilizan directamente funciones HDInsight como Hive y Pig.</span><span class="sxs-lookup"><span data-stu-id="d700d-246">Azure Data Factory can be used toomove data into Azure Blob storage, or toocreate data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="d700d-247">Para obtener más información, vea hello [documentación de Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="d700d-247">For more information, see hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="d700d-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="d700d-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="d700d-249">Sqoop es una herramienta diseñada tootransfer de datos entre bases de datos relacionales y de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d700d-249">Sqoop is a tool designed tootransfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="d700d-250">Puede usar lo tooimport datos desde un sistema de administración de bases de datos relacionales (RDBMS), como SQL Server, MySQL u Oracle en el sistema de archivos distribuido de Hadoop de hello (HDFS), transforme datos hello Hadoop MapReduce o subárbol y, a continuación, exportar datos de hello en un RDBMS.</span><span class="sxs-lookup"><span data-stu-id="d700d-250">You can use it tooimport data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span>

<span data-ttu-id="d700d-251">Para obtener más información, consulte [Use Sqoop with Hadoop in HDInsight (Uso de Sqoop con HDInsight)][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="d700d-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="d700d-252">SDK de desarrollo</span><span class="sxs-lookup"><span data-stu-id="d700d-252">Development SDKs</span></span>
<span data-ttu-id="d700d-253">Almacenamiento de blobs de Azure también puede tener acceso mediante un SDK de Azure de hello después de los lenguajes de programación:</span><span class="sxs-lookup"><span data-stu-id="d700d-253">Azure Blob storage can also be accessed using an Azure SDK from hello following programming languages:</span></span>

* <span data-ttu-id="d700d-254">.NET</span><span class="sxs-lookup"><span data-stu-id="d700d-254">.NET</span></span>
* <span data-ttu-id="d700d-255">Java</span><span class="sxs-lookup"><span data-stu-id="d700d-255">Java</span></span>
* <span data-ttu-id="d700d-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="d700d-256">Node.js</span></span>
* <span data-ttu-id="d700d-257">PHP</span><span class="sxs-lookup"><span data-stu-id="d700d-257">PHP</span></span>
* <span data-ttu-id="d700d-258">Python</span><span class="sxs-lookup"><span data-stu-id="d700d-258">Python</span></span>
* <span data-ttu-id="d700d-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="d700d-259">Ruby</span></span>

<span data-ttu-id="d700d-260">Para obtener más información acerca de cómo instalar hello Azure SDK, vea [descargas de Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="d700d-260">For more information on installing hello Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d700d-261">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="d700d-261">Troubleshooting</span></span>
### <span data-ttu-id="d700d-262"><a id="storageexception"></a>Excepción de almacenamiento para escritura en blob</span><span class="sxs-lookup"><span data-stu-id="d700d-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="d700d-263">**Síntomas**: al usar hello `hadoop` o `hdfs dfs` comandos toowrite los archivos que son ~ 12 GB o mayores en un clúster de HBase, puede encontrar Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="d700d-263">**Symptoms**: When using hello `hadoop` or `hdfs dfs` commands toowrite files that are ~12GB or larger on an HBase cluster, you may encounter hello following error:</span></span>

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="d700d-264">**Causa**: tamaño de bloque predeterminado tooa de 256 KB de clústeres de HBase en HDInsight al escribir tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d700d-264">**Cause**: HBase on HDInsight clusters default tooa block size of 256KB when writing tooAzure storage.</span></span> <span data-ttu-id="d700d-265">Si bien esto funciona para HBase APIs o las API de REST, se producirá un error cuando se usa hello `hadoop` o `hdfs dfs` utilidades de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d700d-265">While this works for HBase APIs or REST APIs, it will result in an error when using hello `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="d700d-266">**Resolución**: Use `fs.azure.write.request.size` toospecify un tamaño de bloque.</span><span class="sxs-lookup"><span data-stu-id="d700d-266">**Resolution**: Use `fs.azure.write.request.size` toospecify a larger block size.</span></span> <span data-ttu-id="d700d-267">Puede hacerlo de forma por uso mediante el uso de hello `-D` parámetro.</span><span class="sxs-lookup"><span data-stu-id="d700d-267">You can do this on a per-use basis by using hello `-D` parameter.</span></span> <span data-ttu-id="d700d-268">Hello aquí te mostramos un ejemplo de cómo utilizar este parámetro con hello `hadoop` comando:</span><span class="sxs-lookup"><span data-stu-id="d700d-268">hello following is an example using this parameter with hello `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="d700d-269">También puede aumentar el valor de Hola de `fs.azure.write.request.size` global mediante el uso de Ambari.</span><span class="sxs-lookup"><span data-stu-id="d700d-269">You can also increase hello value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="d700d-270">Hello siguientes pasos pueden resultar usar valor de hello toochange en hello Ambari Web UI:</span><span class="sxs-lookup"><span data-stu-id="d700d-270">hello following steps can be used toochange hello value in hello Ambari Web UI:</span></span>

1. <span data-ttu-id="d700d-271">En el explorador, vaya toohello Ambari Web UI para el clúster.</span><span class="sxs-lookup"><span data-stu-id="d700d-271">In your browser, go toohello Ambari Web UI for your cluster.</span></span> <span data-ttu-id="d700d-272">Se trata de https://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es Hola nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="d700d-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="d700d-273">Cuando se le solicite, escriba Hola administrador nombre y una contraseña para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="d700d-273">When prompted, enter hello admin name and password for hello cluster.</span></span>
2. <span data-ttu-id="d700d-274">En la parte izquierda de la pantalla de bienvenida de hello, seleccione **HDFS**y, a continuación, seleccione hello **configuraciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="d700d-274">From hello left side of hello screen, select **HDFS**, and then select hello **Configs** tab.</span></span>
3. <span data-ttu-id="d700d-275">Hola **filtro...**  , escriba `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="d700d-275">In hello **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="d700d-276">Se mostrará el campo de Hola y el valor actual en medio de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="d700d-276">This will display hello field and current value in hello middle of hello page.</span></span>
4. <span data-ttu-id="d700d-277">Cambie el valor de hello 262144 (256KB) toohello nuevo valor.</span><span class="sxs-lookup"><span data-stu-id="d700d-277">Change hello value from 262144 (256KB) toohello new value.</span></span> <span data-ttu-id="d700d-278">Por ejemplo, 4194304 (4 MB).</span><span class="sxs-lookup"><span data-stu-id="d700d-278">For example, 4194304 (4MB).</span></span>

![Imagen de cambiar el valor de Hola a través de la interfaz de usuario de Ambari Web](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="d700d-280">Para obtener más información sobre el uso de Ambari, consulte [administrar clústeres de HDInsight con hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="d700d-280">For more information on using Ambari, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d700d-281">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d700d-281">Next steps</span></span>
<span data-ttu-id="d700d-282">Ahora que sabe cómo leer datos de tooget en HDInsight, Hola siguiendo artículos toolearn cómo tooperform analysis:</span><span class="sxs-lookup"><span data-stu-id="d700d-282">Now that you understand how tooget data into HDInsight, read hello following articles toolearn how tooperform analysis:</span></span>

* <span data-ttu-id="d700d-283">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d700d-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="d700d-284">[Envío de trabajos de Hadoop mediante programación][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="d700d-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="d700d-285">[Uso de Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d700d-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d700d-286">[Uso de Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d700d-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
