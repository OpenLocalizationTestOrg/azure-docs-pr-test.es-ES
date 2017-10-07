---
title: "aaaGet a trabajar con análisis de Data Lake de Azure mediante Azure CLI 2.0 | Documentos de Microsoft"
description: "Obtenga información acerca de cómo crear un trabajo de análisis de Data Lake mediante SQL U toouse Hola 2.0 de la interfaz de línea de comandos de Azure toocreate una cuenta de análisis de Data Lake y enviar el trabajo de Hola. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="5160a-103">Introducción al uso de la CLI de Azure 2.0 por parte de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5160a-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="5160a-104">En este tutorial, se desarrolla un trabajo que lee un archivo de valores separados por tabulaciones (TSV) y lo convierte en un otro de valores separados por comas (CSV).</span><span class="sxs-lookup"><span data-stu-id="5160a-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="5160a-105">toogo a través de hello mismo tutorial usar otros admite las herramientas, lista de desplegable Hola de uso en la parte superior de Hola de esta sección.</span><span class="sxs-lookup"><span data-stu-id="5160a-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5160a-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5160a-106">Prerequisites</span></span>
<span data-ttu-id="5160a-107">Antes de comenzar este tutorial, debe tener Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5160a-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="5160a-108">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="5160a-108">**An Azure subscription**.</span></span> <span data-ttu-id="5160a-109">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5160a-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5160a-110">**CLI de Azure 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5160a-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="5160a-111">Consulte [Instalación y configuración de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5160a-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="5160a-112">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="5160a-112">Log in tooAzure</span></span>

<span data-ttu-id="5160a-113">toolog en tooyour suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="5160a-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="5160a-114">Están solicitada toobrowse tooa una dirección URL y escriba un código de autenticación.</span><span class="sxs-lookup"><span data-stu-id="5160a-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="5160a-115">Y, a continuación, siga Hola instrucciones tooenter sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="5160a-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="5160a-116">Una vez que haya iniciado sesión, comando de inicio de sesión de hello muestra las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="5160a-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="5160a-117">toouse una suscripción específica:</span><span class="sxs-lookup"><span data-stu-id="5160a-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="5160a-118">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="5160a-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="5160a-119">Para poder ejecutar cualquier trabajo es preciso tener una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5160a-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="5160a-120">una cuenta de análisis de Data Lake toocreate, debe especificar Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5160a-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="5160a-121">**Grupo de recursos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="5160a-121">**Azure Resource Group**.</span></span> <span data-ttu-id="5160a-122">Se debe crear una cuenta de Data Lake Analytics en un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5160a-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="5160a-123">[El Administrador de recursos Azure](../azure-resource-manager/resource-group-overview.md) permite toowork con recursos de hello en la aplicación como un grupo.</span><span class="sxs-lookup"><span data-stu-id="5160a-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="5160a-124">Puede implementar, actualizar o eliminar todos los recursos de Hola para su aplicación en una única operación coordinada.</span><span class="sxs-lookup"><span data-stu-id="5160a-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="5160a-125">toolist Hola existente grupos de recursos bajo su suscripción:</span><span class="sxs-lookup"><span data-stu-id="5160a-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="5160a-126">toocreate un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="5160a-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="5160a-127">**Nombre de la cuenta de Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="5160a-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="5160a-128">Cada cuenta de Data Lake Analytics tiene un nombre.</span><span class="sxs-lookup"><span data-stu-id="5160a-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="5160a-129">**Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="5160a-129">**Location**.</span></span> <span data-ttu-id="5160a-130">Utilice uno de los centros de datos de Azure de Hola que admita el análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5160a-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="5160a-131">**Cuenta predeterminada de Data Lake Store**: cada cuenta de Data Lake Analytics tiene una cuenta de Data Lake Store predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5160a-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="5160a-132">cuenta toolist Hola existente almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="5160a-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="5160a-133">toocreate una nueva cuenta de almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="5160a-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="5160a-134">Usar hello siguiendo la sintaxis toocreate una cuenta de análisis de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="5160a-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="5160a-135">Después de crear una cuenta, puede usar hello siguiendo las cuentas de comandos toolist hello y mostrar detalles de la cuenta:</span><span class="sxs-lookup"><span data-stu-id="5160a-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="5160a-136">Cargar el almacén de datos tooData Lake</span><span class="sxs-lookup"><span data-stu-id="5160a-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="5160a-137">En este tutorial, va a procesar algunos registros de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="5160a-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="5160a-138">registro de búsqueda de Hello puede almacenarse en el almacén de Data Lake o almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="5160a-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="5160a-139">Hola portal de Azure proporciona una interfaz de usuario para copiar algunos ejemplo datos archivos toohello almacén de Data Lake cuenta predeterminada, que incluyen un archivo de registro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="5160a-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="5160a-140">Vea [preparar los datos de origen](data-lake-analytics-get-started-portal.md) cuenta de almacén de Data Lake tooupload Hola datos toohello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5160a-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="5160a-141">los archivos de tooupload mediante 2.0 de CLI, utilizan Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="5160a-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="5160a-142">Análisis de Data Lake también puede acceder al almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="5160a-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="5160a-143">Para cargar el almacenamiento de blobs de tooAzure de datos, vea [Using Hola CLI de Azure con el almacenamiento de Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5160a-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="5160a-144">Envío de trabajos de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="5160a-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="5160a-145">trabajos de análisis de Data Lake de Hola se escriben en lenguaje SQL U Hola.</span><span class="sxs-lookup"><span data-stu-id="5160a-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="5160a-146">toolearn más información acerca de T-SQL, consulte [empezar a trabajar con lenguaje SQL U](data-lake-analytics-u-sql-get-started.md) y [eence de lenguaje SQL U](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="5160a-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="5160a-147">**toocreate un script de trabajo de análisis de Data Lake**</span><span class="sxs-lookup"><span data-stu-id="5160a-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="5160a-148">Crear un archivo de texto con el siguiente script SQL U y guarde la estación de trabajo de hello texto archivo tooyour:</span><span class="sxs-lookup"><span data-stu-id="5160a-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="5160a-149">Este script U-SQL lee el archivo de datos de origen de hello mediante **Extractors.Tsv()**y, a continuación, crea un archivo csv mediante **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="5160a-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="5160a-150">No modifique dos rutas de acceso de Hola a menos que copie el archivo de código fuente de hello en una ubicación diferente.</span><span class="sxs-lookup"><span data-stu-id="5160a-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="5160a-151">Análisis de Data Lake crea la carpeta de salida de hello si no existe.</span><span class="sxs-lookup"><span data-stu-id="5160a-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="5160a-152">Resulta más sencillos rutas de acceso relativas toouse para archivos almacenados en las cuentas de almacén de Data Lake de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5160a-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="5160a-153">También puede usar rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="5160a-153">You can also use absolute paths.</span></span>  <span data-ttu-id="5160a-154">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5160a-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="5160a-155">Debe usar archivos de tooaccess de rutas de acceso absolutas en las cuentas de almacenamiento vinculadas.</span><span class="sxs-lookup"><span data-stu-id="5160a-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="5160a-156">sintaxis de Hola para archivos almacenados en la cuenta de almacenamiento de Azure vinculada es:</span><span class="sxs-lookup"><span data-stu-id="5160a-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="5160a-157">El contenedor de blobs de Azure con blobs públicos no se admite.</span><span class="sxs-lookup"><span data-stu-id="5160a-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="5160a-158">El contenedor de blobs de Azure con contenedores públicos no se admite.</span><span class="sxs-lookup"><span data-stu-id="5160a-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="5160a-159">**trabajos de toosubmit**</span><span class="sxs-lookup"><span data-stu-id="5160a-159">**toosubmit jobs**</span></span>

<span data-ttu-id="5160a-160">Usar hello siguiendo la sintaxis toosubmit un trabajo.</span><span class="sxs-lookup"><span data-stu-id="5160a-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="5160a-161">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5160a-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="5160a-162">**trabajos de toolist y mostrar detalles del trabajo**</span><span class="sxs-lookup"><span data-stu-id="5160a-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="5160a-163">**trabajos de toocancel**</span><span class="sxs-lookup"><span data-stu-id="5160a-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="5160a-164">Recuperación de los resultados de un trabajo</span><span class="sxs-lookup"><span data-stu-id="5160a-164">Retrieve job results</span></span>

<span data-ttu-id="5160a-165">Después de que se completa un trabajo, puede usar hello siguientes archivos de salida de comandos toolist hello y descargar archivos de hello:</span><span class="sxs-lookup"><span data-stu-id="5160a-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="5160a-166">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5160a-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="5160a-167">Canalizaciones y repeticiones</span><span class="sxs-lookup"><span data-stu-id="5160a-167">Pipelines and recurrences</span></span>

<span data-ttu-id="5160a-168">**Obtención de información sobre canalizaciones y repeticiones**</span><span class="sxs-lookup"><span data-stu-id="5160a-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="5160a-169">Hola de uso `az dla job pipeline` comandos anteriormente envía la información de canalización de Hola de toosee trabajos.</span><span class="sxs-lookup"><span data-stu-id="5160a-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="5160a-170">Hola de uso `az dla job recurrence` comandos toosee información de periodicidad de Hola para los trabajos enviados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5160a-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="5160a-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5160a-171">Next steps</span></span>

* <span data-ttu-id="5160a-172">Hola toosee documento de referencia de Data Lake Analytics CLI 2.0, consulte [análisis de Data Lake](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="5160a-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="5160a-173">Hola toosee documento de referencia de almacén de Data Lake CLI 2.0, consulte [almacén de Data Lake](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="5160a-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="5160a-174">toosee una consulta más compleja, vea [sitio Web de analizar registros con análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="5160a-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
