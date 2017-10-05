---
title: "Introducción a Azure Data Lake Analytics mediante la CLI de Azure 2.0 | Microsoft Docs"
description: "Aprenda a usar la interfaz de la línea de comandos de Azure 2.0 para crear una cuenta de Data Lake Analytics, crear un trabajo de Data Lake Analytics mediante U-SQL y enviar dicho trabajo. "
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
ms.openlocfilehash: fe2b84aac718ff5eddd4d73b5dc2120362952c1e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="19875-103">Introducción al uso de la CLI de Azure 2.0 por parte de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="19875-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="19875-104">En este tutorial, se desarrolla un trabajo que lee un archivo de valores separados por tabulaciones (TSV) y lo convierte en un otro de valores separados por comas (CSV).</span><span class="sxs-lookup"><span data-stu-id="19875-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="19875-105">Para realizar el mismo tutorial con otras herramientas compatibles, use la lista desplegable de la parte superior de esta sección.</span><span class="sxs-lookup"><span data-stu-id="19875-105">To go through the same tutorial using other supported tools, use the dropdown list on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19875-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="19875-106">Prerequisites</span></span>
<span data-ttu-id="19875-107">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="19875-107">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="19875-108">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="19875-108">**An Azure subscription**.</span></span> <span data-ttu-id="19875-109">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19875-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="19875-110">**CLI de Azure 2.0**.</span><span class="sxs-lookup"><span data-stu-id="19875-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="19875-111">Consulte [Instalación y configuración de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="19875-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="19875-112">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="19875-112">Log in to Azure</span></span>

<span data-ttu-id="19875-113">Para iniciar sesión en una suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="19875-113">To log in to your Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="19875-114">Se le solicita que vaya a una dirección URL y que escriba un código de autenticación.</span><span class="sxs-lookup"><span data-stu-id="19875-114">You are requested to browse to a URL, and enter an authentication code.</span></span>  <span data-ttu-id="19875-115">Y, después, debe seguir las instrucciones para escribir sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="19875-115">And then follow the instructions to enter your credentials.</span></span>

<span data-ttu-id="19875-116">Una vez que haya iniciado sesión, el comando de inicio de sesión enumera las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="19875-116">Once you have logged in, the login command lists your subscriptions.</span></span>

<span data-ttu-id="19875-117">Para usar una suscripción concreta:</span><span class="sxs-lookup"><span data-stu-id="19875-117">To use a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="19875-118">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="19875-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="19875-119">Para poder ejecutar cualquier trabajo es preciso tener una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="19875-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="19875-120">Para crearla, debe especificar los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="19875-120">To create a Data Lake Analytics account, you must specify the following items:</span></span>

* <span data-ttu-id="19875-121">**Grupo de recursos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="19875-121">**Azure Resource Group**.</span></span> <span data-ttu-id="19875-122">Se debe crear una cuenta de Data Lake Analytics en un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="19875-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="19875-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permite trabajar con los recursos de la aplicación como un grupo.</span><span class="sxs-lookup"><span data-stu-id="19875-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="19875-124">Puede implementar, actualizar o eliminar todos los recursos de la aplicación en una operación única coordinada.</span><span class="sxs-lookup"><span data-stu-id="19875-124">You can deploy, update, or delete all of the resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="19875-125">Para enumerar los grupos de recursos que contiene su suscripción:</span><span class="sxs-lookup"><span data-stu-id="19875-125">To list the existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="19875-126">Para crear un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="19875-126">To create a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="19875-127">**Nombre de la cuenta de Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="19875-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="19875-128">Cada cuenta de Data Lake Analytics tiene un nombre.</span><span class="sxs-lookup"><span data-stu-id="19875-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="19875-129">**Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="19875-129">**Location**.</span></span> <span data-ttu-id="19875-130">Use uno de los centros de datos de Azure que admita Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="19875-130">Use one of the Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="19875-131">**Cuenta predeterminada de Data Lake Store**: cada cuenta de Data Lake Analytics tiene una cuenta de Data Lake Store predeterminada.</span><span class="sxs-lookup"><span data-stu-id="19875-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="19875-132">Para mostrar la cuenta de Data Lake Store existente:</span><span class="sxs-lookup"><span data-stu-id="19875-132">To list the existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="19875-133">Para crear una nueva cuenta de Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="19875-133">To create a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="19875-134">Use la siguiente sintaxis para crear una cuenta de Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="19875-134">Use the following syntax to create a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="19875-135">Después de crear una cuenta, puede usar los comandos siguientes para enumerar las cuentas y mostrar los detalles de la misma:</span><span class="sxs-lookup"><span data-stu-id="19875-135">After creating an account, you can use the following commands to list the accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-to-data-lake-store"></a><span data-ttu-id="19875-136">Carga de datos en el Almacén Data Lake</span><span class="sxs-lookup"><span data-stu-id="19875-136">Upload data to Data Lake Store</span></span>
<span data-ttu-id="19875-137">En este tutorial, va a procesar algunos registros de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="19875-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="19875-138">El registro de búsqueda se puede almacenar en el Almacén de Data Lake o en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="19875-138">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="19875-139">Azure Portal proporciona una interfaz de usuario para copiar algunos archivos de datos de ejemplo a la cuenta predeterminada de Data Lake Store, entre los que se incluye un archivo de registro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="19875-139">The Azure portal provides a user interface for copying some sample data files to the default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="19875-140">Consulte [Preparar los datos de origen](data-lake-analytics-get-started-portal.md) para cargar los datos en la cuenta del Almacén Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19875-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) to upload the data to the default Data Lake Store account.</span></span>

<span data-ttu-id="19875-141">Para cargar archivos mediante la CLI 2.0, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="19875-141">To upload files using CLI 2.0, use the following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="19875-142">Análisis de Data Lake también puede acceder al almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="19875-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="19875-143">Para cargar datos al almacenamiento de blobs de Azure, consulte [Uso de la CLI de Azure con Almacenamiento de Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="19875-143">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="19875-144">Envío de trabajos de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="19875-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="19875-145">Los trabajos de Análisis de Data Lake se escriben en el lenguaje U-SQL.</span><span class="sxs-lookup"><span data-stu-id="19875-145">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="19875-146">Para más información acerca de U-SQL, consulte [Introducción a U-SQL](data-lake-analytics-u-sql-get-started.md) y [U-SQL Language Reference](http://go.microsoft.com/fwlink/?LinkId=691348) (Referencia del lenguaje U-SQL).</span><span class="sxs-lookup"><span data-stu-id="19875-146">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="19875-147">**Para crear un script de trabajo de Análisis de Data Lake**</span><span class="sxs-lookup"><span data-stu-id="19875-147">**To create a Data Lake Analytics job script**</span></span>

<span data-ttu-id="19875-148">Cree un archivo de texto con el siguiente script U-SQL y guarde el archivo de texto en la estación de trabajo:</span><span class="sxs-lookup"><span data-stu-id="19875-148">Create a text file with following U-SQL script, and save the text file to your workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="19875-149">Este script de U-SQL lee el archivo de datos de origen mediante **Extractors.Tsv()** y crea un archivo csv con **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="19875-149">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="19875-150">No modifique ninguna de las dos rutas a menos que copie el archivo de origen en una ubicación diferente.</span><span class="sxs-lookup"><span data-stu-id="19875-150">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="19875-151">Data Lake Analytics creará la carpeta de salida si no existe.</span><span class="sxs-lookup"><span data-stu-id="19875-151">Data Lake Analytics creates the output folder if it doesn't exist.</span></span>

<span data-ttu-id="19875-152">Es más fácil usar rutas de acceso relativas para los archivos almacenados en las cuentas predeterminadas de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="19875-152">It is simpler to use relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="19875-153">También puede usar rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="19875-153">You can also use absolute paths.</span></span>  <span data-ttu-id="19875-154">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="19875-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="19875-155">Debe usar rutas de acceso absolutas para acceder a los archivos de cuentas de almacenamiento vinculadas.</span><span class="sxs-lookup"><span data-stu-id="19875-155">You must use absolute paths to access files in linked Storage accounts.</span></span>  <span data-ttu-id="19875-156">La sintaxis de los archivos almacenados en la cuenta de Almacenamiento de Azure vinculada es:</span><span class="sxs-lookup"><span data-stu-id="19875-156">The syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="19875-157">El contenedor de blobs de Azure con blobs públicos no se admite.</span><span class="sxs-lookup"><span data-stu-id="19875-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="19875-158">El contenedor de blobs de Azure con contenedores públicos no se admite.</span><span class="sxs-lookup"><span data-stu-id="19875-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="19875-159">**Para enviar trabajos**</span><span class="sxs-lookup"><span data-stu-id="19875-159">**To submit jobs**</span></span>

<span data-ttu-id="19875-160">Para enviar un trabajo, use la sintaxis siguiente.</span><span class="sxs-lookup"><span data-stu-id="19875-160">Use the following syntax to submit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="19875-161">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="19875-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="19875-162">**Para enumerar los trabajos y mostrar los detalles de un trabajo**</span><span class="sxs-lookup"><span data-stu-id="19875-162">**To list jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="19875-163">**Para cancelar trabajos**</span><span class="sxs-lookup"><span data-stu-id="19875-163">**To cancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="19875-164">Recuperación de los resultados de un trabajo</span><span class="sxs-lookup"><span data-stu-id="19875-164">Retrieve job results</span></span>

<span data-ttu-id="19875-165">Una vez que se completa un trabajo, puede usar los siguientes comandos para enumerar los archivos de salida y descargar los archivos:</span><span class="sxs-lookup"><span data-stu-id="19875-165">After a job is completed, you can use the following commands to list the output files, and download the files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="19875-166">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="19875-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="19875-167">Canalizaciones y repeticiones</span><span class="sxs-lookup"><span data-stu-id="19875-167">Pipelines and recurrences</span></span>

<span data-ttu-id="19875-168">**Obtención de información sobre canalizaciones y repeticiones**</span><span class="sxs-lookup"><span data-stu-id="19875-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="19875-169">Utilice los comandos `az dla job pipeline` para ver la información de canalización de trabajos enviados previamente.</span><span class="sxs-lookup"><span data-stu-id="19875-169">Use the `az dla job pipeline` commands to see the pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="19875-170">Utilice los comandos `az dla job recurrence` para ver la información de repetición de trabajos enviados previamente.</span><span class="sxs-lookup"><span data-stu-id="19875-170">Use the `az dla job recurrence` commands to see the recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="19875-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19875-171">Next steps</span></span>

* <span data-ttu-id="19875-172">Para ver el documento de referencia de la CLI de Data Lake Analytics 2.0, consulte [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="19875-172">To see the Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="19875-173">Para ver el documento de referencia de la CLI de Data Lake Store 2.0, consulte [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="19875-173">To see the Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="19875-174">Para ver una consulta más compleja, consulte la página sobre el [análisis de registros de sitio web mediante Análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="19875-174">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
