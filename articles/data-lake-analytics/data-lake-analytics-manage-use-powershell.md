---
title: "Análisis de Data Lake de Azure con Azure PowerShell aaaManage | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage cuentas de análisis de Data Lake, orígenes de datos, trabajos y elementos del catálogo. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="53b5c-103">Administración de Análisis de Azure Data Lake mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="53b5c-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="53b5c-104">Obtenga información acerca de cómo trabajos de cuentas de análisis de Azure Data Lake toomanage, orígenes de datos y elementos del catálogo con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53b5c-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="53b5c-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="53b5c-105">Prerequisites</span></span>

<span data-ttu-id="53b5c-106">Al crear una cuenta de análisis de Data Lake, necesita tooknow:</span><span class="sxs-lookup"><span data-stu-id="53b5c-106">When creating a Data Lake Analytics account, you need tooknow:</span></span>

* <span data-ttu-id="53b5c-107">**Id. de suscripción**: Hola Id. de suscripción de Azure en el que reside la cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="53b5c-107">**Subscription ID**: hello Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="53b5c-108">**Grupo de recursos**: nombre de Hola Hola Azure del grupo de recursos que contiene la cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="53b5c-108">**Resource group**: hello name of hello Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="53b5c-109">**Nombre de la cuenta de análisis de Data Lake**: Hola cuenta nombre solo debe contener letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="53b5c-109">**Data Lake Analytics account name**: hello account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="53b5c-110">**Cuenta predeterminada de Data Lake Store**: cada cuenta de Data Lake Analytics tiene una cuenta de Data Lake Store predeterminada.</span><span class="sxs-lookup"><span data-stu-id="53b5c-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="53b5c-111">Estas cuentas deben estar en hello misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="53b5c-111">These accounts must be in hello same location.</span></span>
* <span data-ttu-id="53b5c-112">**Ubicación**: ubicación de saludo de la cuenta de análisis de Data Lake, como "UU 2" u otra admite ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="53b5c-112">**Location**: hello location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="53b5c-113">Las ubicaciones admitidas se pueden consultar en nuestra [página de precios](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="53b5c-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="53b5c-114">fragmentos de código de PowerShell de Hello en este tutorial usa estas variables toostore esta información</span><span class="sxs-lookup"><span data-stu-id="53b5c-114">hello PowerShell snippets in this tutorial use these variables toostore this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="53b5c-115">Registro</span><span class="sxs-lookup"><span data-stu-id="53b5c-115">Log in</span></span>

<span data-ttu-id="53b5c-116">Inicie sesión con un identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="53b5c-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="53b5c-117">Inicie sesión con un nombre de suscripción.</span><span class="sxs-lookup"><span data-stu-id="53b5c-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="53b5c-118">Hola `Login-AzureRmAccount` cmdlet siempre pide las credenciales.</span><span class="sxs-lookup"><span data-stu-id="53b5c-118">hello `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="53b5c-119">Puede evitar que se le solicite mediante el uso de hello siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="53b5c-119">You can avoid being prompted by using hello following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="53b5c-120">Administración de cuentas</span><span class="sxs-lookup"><span data-stu-id="53b5c-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="53b5c-121">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="53b5c-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="53b5c-122">Si aún no tiene un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, cree uno.</span><span class="sxs-lookup"><span data-stu-id="53b5c-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="53b5c-123">Cada cuenta de Data Lake Analytics requiere una cuenta predeterminada de Data Lake Store que se usa para almacenar registros.</span><span class="sxs-lookup"><span data-stu-id="53b5c-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="53b5c-124">Puede reutilizar una cuenta existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="53b5c-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="53b5c-125">Una vez que un grupo de recursos y una cuenta de Data Lake Store estén disponibles, cree una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="53b5c-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="53b5c-126">Obtener información de una cuenta</span><span class="sxs-lookup"><span data-stu-id="53b5c-126">Get information about an account</span></span>

<span data-ttu-id="53b5c-127">Obtener detalles acerca de una cuenta.</span><span class="sxs-lookup"><span data-stu-id="53b5c-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="53b5c-128">Comprobar la existencia de Hola de una cuenta de análisis de Data Lake concreta.</span><span class="sxs-lookup"><span data-stu-id="53b5c-128">Check hello existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="53b5c-129">Hola cmdlet devuelve `True` o `False`.</span><span class="sxs-lookup"><span data-stu-id="53b5c-129">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="53b5c-130">Comprobar la existencia de Hola de una cuenta de almacén de Data Lake concreta.</span><span class="sxs-lookup"><span data-stu-id="53b5c-130">Check hello existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="53b5c-131">Hola cmdlet devuelve `True` o `False`.</span><span class="sxs-lookup"><span data-stu-id="53b5c-131">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="53b5c-132">Lista de cuentas</span><span class="sxs-lookup"><span data-stu-id="53b5c-132">Listing accounts</span></span>

<span data-ttu-id="53b5c-133">Cuentas de análisis de Data Lake de lista dentro de la suscripción actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="53b5c-133">List Data Lake Analytics accounts within hello current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="53b5c-134">Enumerar cuentas de Data Lake Analytics dentro de un grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="53b5c-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="53b5c-135">Administración de reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="53b5c-135">Managing firewall rules</span></span>

<span data-ttu-id="53b5c-136">Enumerar reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="53b5c-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="53b5c-137">Agregar una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="53b5c-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="53b5c-138">Cambiar una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="53b5c-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="53b5c-139">Eliminar una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="53b5c-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="53b5c-140">Permitir direcciones IP de Azure.</span><span class="sxs-lookup"><span data-stu-id="53b5c-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="53b5c-141">Administración de orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="53b5c-141">Managing data sources</span></span>
<span data-ttu-id="53b5c-142">Análisis de Azure Data Lake admite actualmente Hola siguientes orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="53b5c-142">Azure Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="53b5c-143">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="53b5c-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="53b5c-144">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="53b5c-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="53b5c-145">Cuando se crea una cuenta de análisis, debe designar un origen de datos de almacén de Data Lake cuenta toobe Hola predeterminado.</span><span class="sxs-lookup"><span data-stu-id="53b5c-145">When you create an Analytics account, you must designate a Data Lake Store account toobe hello default data source.</span></span> <span data-ttu-id="53b5c-146">Hello almacén de Data Lake cuenta predeterminada se utiliza registros de auditoría de metadatos de trabajo toostore y trabajo.</span><span class="sxs-lookup"><span data-stu-id="53b5c-146">hello default Data Lake Store account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="53b5c-147">Una vez creada la cuenta de Data Lake Analytics, puede agregar más cuentas de Data Lake Store o cuentas de Storage.</span><span class="sxs-lookup"><span data-stu-id="53b5c-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-hello-default-data-lake-store-account"></a><span data-ttu-id="53b5c-148">Buscar cuenta de almacén de Data Lake Hola predeterminada</span><span class="sxs-lookup"><span data-stu-id="53b5c-148">Find hello default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="53b5c-149">Puede encontrar cuenta de almacén de Data Lake Hola predeterminada si filtra la lista de Hola de orígenes de datos por hello `IsDefault` propiedad:</span><span class="sxs-lookup"><span data-stu-id="53b5c-149">You can find hello default Data Lake Store account by filtering hello list of datasources by hello `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="53b5c-150">Agregar un origen de datos</span><span class="sxs-lookup"><span data-stu-id="53b5c-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="53b5c-151">Enumerar orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="53b5c-151">List data sources</span></span>

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="53b5c-152">Envío de trabajos de U-SQL</span><span class="sxs-lookup"><span data-stu-id="53b5c-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="53b5c-153">Enviar una cadena como un script U-SQL</span><span class="sxs-lookup"><span data-stu-id="53b5c-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="53b5c-154">Enviar un archivo como un script U-SQL</span><span class="sxs-lookup"><span data-stu-id="53b5c-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="53b5c-155">Enumerar trabajos en una cuenta</span><span class="sxs-lookup"><span data-stu-id="53b5c-155">List jobs in an account</span></span>

### <a name="list-all-hello-jobs-in-hello-account"></a><span data-ttu-id="53b5c-156">Enumera todos los trabajos de hello en la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="53b5c-156">List all hello jobs in hello account.</span></span> 

<span data-ttu-id="53b5c-157">salida de Hello incluye Hola actualmente en ejecución trabajos y los pasos de trabajo completaron recientemente.</span><span class="sxs-lookup"><span data-stu-id="53b5c-157">hello output includes hello currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="53b5c-158">Mostrar un número determinado de trabajos</span><span class="sxs-lookup"><span data-stu-id="53b5c-158">List a specific number of jobs</span></span>

<span data-ttu-id="53b5c-159">De forma predeterminada se ordena la lista Hola de trabajos en el momento del envío.</span><span class="sxs-lookup"><span data-stu-id="53b5c-159">By default hello list of jobs is sorted on submit time.</span></span> <span data-ttu-id="53b5c-160">Por lo que se envió más recientemente Hola trabajos aparecen en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="53b5c-160">So hello most recently submitted jobs appear first.</span></span> <span data-ttu-id="53b5c-161">De forma predeterminada, Hola cuenta ADLA recuerda trabajos durante 180 días, pero Hola Ge AdlJob cmdlet devuelve de forma predeterminada sólo Hola 500 primeros.</span><span class="sxs-lookup"><span data-stu-id="53b5c-161">By default, hello ADLA account remembers jobs for 180 days, but hello Ge-AdlJob  cmdlet by default returns only hello first 500.</span></span> <span data-ttu-id="53b5c-162">Use - toolist parámetro superior un número específico de trabajos.</span><span class="sxs-lookup"><span data-stu-id="53b5c-162">Use -Top parameter toolist a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a><span data-ttu-id="53b5c-163">Enumerar trabajos según Hola valor de propiedad del trabajo</span><span class="sxs-lookup"><span data-stu-id="53b5c-163">List jobs based on hello value of job property</span></span>

<span data-ttu-id="53b5c-164">Con hello `-State` parámetro.</span><span class="sxs-lookup"><span data-stu-id="53b5c-164">Using hello `-State` parameter.</span></span> <span data-ttu-id="53b5c-165">Puede combinar cualquiera de estos valores:</span><span class="sxs-lookup"><span data-stu-id="53b5c-165">You can combine any of these values:</span></span>

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="53b5c-166">Hola de uso `-Result` toodetect parámetro si los trabajos finalizados se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="53b5c-166">Use hello `-Result` parameter toodetect whether ended jobs completed successfully.</span></span> <span data-ttu-id="53b5c-167">Tiene estos valores:</span><span class="sxs-lookup"><span data-stu-id="53b5c-167">It has these values:</span></span>

* <span data-ttu-id="53b5c-168">Cancelado</span><span class="sxs-lookup"><span data-stu-id="53b5c-168">Cancelled</span></span>
* <span data-ttu-id="53b5c-169">Con error</span><span class="sxs-lookup"><span data-stu-id="53b5c-169">Failed</span></span>
* <span data-ttu-id="53b5c-170">None</span><span class="sxs-lookup"><span data-stu-id="53b5c-170">None</span></span>
* <span data-ttu-id="53b5c-171">Correcto</span><span class="sxs-lookup"><span data-stu-id="53b5c-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="53b5c-172">Hola `-Submitter` parámetro ayuda a identificar quién envió un trabajo.</span><span class="sxs-lookup"><span data-stu-id="53b5c-172">hello `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="53b5c-173">Hola `-SubmittedAfter` es útil en el intervalo de tiempo de tooa de filtrado.</span><span class="sxs-lookup"><span data-stu-id="53b5c-173">hello `-SubmittedAfter` is useful in filtering tooa time range.</span></span>


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="53b5c-174">Escenarios comunes para enumerar trabajos</span><span class="sxs-lookup"><span data-stu-id="53b5c-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="53b5c-175">Filtrado de una lista de trabajos</span><span class="sxs-lookup"><span data-stu-id="53b5c-175">Filtering a list of jobs</span></span>

<span data-ttu-id="53b5c-176">Una vez que tenga una lista de trabajos en la sesión actual de PowerShell,</span><span class="sxs-lookup"><span data-stu-id="53b5c-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="53b5c-177">Puede usar la lista de Hola de toofilter de cmdlets de PowerShell normal.</span><span class="sxs-lookup"><span data-stu-id="53b5c-177">You can use normal PowerShell cmdlets toofilter hello list.</span></span>

<span data-ttu-id="53b5c-178">Filtrar una lista de trabajos de toohello trabajos enviados en hello últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="53b5c-178">Filter a list of jobs toohello jobs submitted in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="53b5c-179">Filtrar una lista de trabajos de toohello de trabajos que finalizaron en hello últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="53b5c-179">Filter a list of jobs toohello jobs that ended in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="53b5c-180">Filtrar una lista de trabajos de toohello de trabajos que se empezó a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="53b5c-180">Filter a list of jobs toohello jobs that started running.</span></span> <span data-ttu-id="53b5c-181">Se puede producir un error en un trabajo en tiempo de compilación, por lo que nunca se inicia.</span><span class="sxs-lookup"><span data-stu-id="53b5c-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="53b5c-182">Echemos un vistazo a los trabajos de hello no se pudo que realmente empezó a ejecutarse y, a continuación, no se pudo.</span><span class="sxs-lookup"><span data-stu-id="53b5c-182">Let's look at hello failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="53b5c-183">Análisis de una lista de trabajos</span><span class="sxs-lookup"><span data-stu-id="53b5c-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="53b5c-184">Hola de uso `Group-Object` cmdlet tooanalyze una lista de trabajos.</span><span class="sxs-lookup"><span data-stu-id="53b5c-184">Use hello `Group-Object` cmdlet tooanalyze a list of jobs.</span></span>

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="53b5c-185">Al realizar un análisis, puede ser útil tooadd propiedades toohello trabajo objetos toomake de filtrado y agrupación más sencilla.</span><span class="sxs-lookup"><span data-stu-id="53b5c-185">When performing an analysis, it can be useful tooadd properties toohello Job objects toomake filtering and grouping simpler.</span></span> <span data-ttu-id="53b5c-186">Hola siguiente fragmento de código muestra el modo en que tooannotate una JobInfo con calcula propiedades.</span><span class="sxs-lookup"><span data-stu-id="53b5c-186">hello following  snippet shows how tooannotate a JobInfo with calculated properties.</span></span>

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="53b5c-187">Obtención de información sobre canalizaciones y repeticiones</span><span class="sxs-lookup"><span data-stu-id="53b5c-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="53b5c-188">Hola de uso `Get-AdlJobPipeline` información de canalización de cmdlet toosee Hola enviados previamente trabajos.</span><span class="sxs-lookup"><span data-stu-id="53b5c-188">Use hello `Get-AdlJobPipeline` cmdlet toosee hello pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="53b5c-189">Hola de uso `Get-AdlJobRecurrence` información de periodicidad de cmdlet toosee Hola para los trabajos enviados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="53b5c-189">Use hello `Get-AdlJobRecurrence` cmdlet toosee hello recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="53b5c-190">Obtención de información sobre un trabajo</span><span class="sxs-lookup"><span data-stu-id="53b5c-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="53b5c-191">Obtención de estado del trabajo</span><span class="sxs-lookup"><span data-stu-id="53b5c-191">Get job status</span></span>

<span data-ttu-id="53b5c-192">Obtener estado de Hola de un trabajo específico.</span><span class="sxs-lookup"><span data-stu-id="53b5c-192">Get hello status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a><span data-ttu-id="53b5c-193">Examinar Hola salidas de trabajo</span><span class="sxs-lookup"><span data-stu-id="53b5c-193">Examine hello job outputs</span></span>

<span data-ttu-id="53b5c-194">Una vez ha finalizado el trabajo de hello, compruebe si existe el archivo de salida de hello haciendo una lista de archivos de hello en una carpeta.</span><span class="sxs-lookup"><span data-stu-id="53b5c-194">After hello job has ended, check if hello output file exists by listing hello files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="53b5c-195">Administración de trabajos en ejecución</span><span class="sxs-lookup"><span data-stu-id="53b5c-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="53b5c-196">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="53b5c-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a><span data-ttu-id="53b5c-197">Espere a que un trabajo toofinish</span><span class="sxs-lookup"><span data-stu-id="53b5c-197">Wait for a job toofinish</span></span>

<span data-ttu-id="53b5c-198">En lugar de repetir `Get-AdlAnalyticsJob` hasta que finalice un trabajo, puede usar hello `Wait-AdlJob` toowait de cmdlet para hello tooend de trabajo.</span><span class="sxs-lookup"><span data-stu-id="53b5c-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use hello `Wait-AdlJob` cmdlet toowait for hello job tooend.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="53b5c-199">Administración de nodos directivas de proceso</span><span class="sxs-lookup"><span data-stu-id="53b5c-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="53b5c-200">Lista de directivas de proceso existentes</span><span class="sxs-lookup"><span data-stu-id="53b5c-200">List existing compute policies</span></span>

<span data-ttu-id="53b5c-201">Hola `Get-AdlAnalyticsComputePolicy` cmdlet recupera información acerca de las directivas de proceso para una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="53b5c-201">hello `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="53b5c-202">Creación de una directiva de proceso</span><span class="sxs-lookup"><span data-stu-id="53b5c-202">Create a compute policy</span></span>

<span data-ttu-id="53b5c-203">Hola `New-AdlAnalyticsComputePolicy` crea una nueva directiva de cálculo para una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="53b5c-203">hello `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="53b5c-204">En este ejemplo conjuntos Hola toohello disponible de AUs máximo especificado too50 de usuario y too250 de prioridad de trabajo mínimo de Hola.</span><span class="sxs-lookup"><span data-stu-id="53b5c-204">This example sets  hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a><span data-ttu-id="53b5c-205">Comprobar existencia de Hola de un archivo.</span><span class="sxs-lookup"><span data-stu-id="53b5c-205">Check for hello existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="53b5c-206">Carga y descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="53b5c-206">Uploading and downloading</span></span>

<span data-ttu-id="53b5c-207">Cargar un archivo.</span><span class="sxs-lookup"><span data-stu-id="53b5c-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="53b5c-208">Cargue una carpeta completa de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="53b5c-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="53b5c-209">Descargar un archivo.</span><span class="sxs-lookup"><span data-stu-id="53b5c-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="53b5c-210">Descargue una carpeta completa de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="53b5c-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="53b5c-211">Si hello cargar o se interrumpe el proceso de descarga, puede intentar el proceso de hello tooresume mediante la ejecución del cmdlet Hola nuevo con hello ``-Resume`` marca.</span><span class="sxs-lookup"><span data-stu-id="53b5c-211">If hello upload or download process is interrupted, you can attempt tooresume hello process by running hello cmdlet again with hello ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="53b5c-212">Administración de elementos de catálogo</span><span class="sxs-lookup"><span data-stu-id="53b5c-212">Manage catalog items</span></span>

<span data-ttu-id="53b5c-213">catálogo de Hello U-SQL es toostructure usa datos y el código para que pueda compartir por secuencias de comandos SQL U.</span><span class="sxs-lookup"><span data-stu-id="53b5c-213">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="53b5c-214">catálogo de Hello permite Hola mayor rendimiento posible con los datos de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="53b5c-214">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="53b5c-215">Para obtener más información, consulte [Uso del catálogo de U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="53b5c-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-hello-u-sql-catalog"></a><span data-ttu-id="53b5c-216">Elementos de lista en el catálogo de hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="53b5c-216">List items in hello U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="53b5c-217">Enumerar todos los ensamblados de hello en todas las bases de datos de hello en una cuenta de ADLA.</span><span class="sxs-lookup"><span data-stu-id="53b5c-217">List all hello assemblies in all hello databases in an ADLA Account.</span></span>

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="53b5c-218">Obtener detalles sobre un elemento de catálogo</span><span class="sxs-lookup"><span data-stu-id="53b5c-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="53b5c-219">Crear credenciales en un catálogo</span><span class="sxs-lookup"><span data-stu-id="53b5c-219">Create credentials in a catalog</span></span>

<span data-ttu-id="53b5c-220">Dentro de una base de datos U-SQL, cree un objeto de credenciales para una base de datos hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="53b5c-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="53b5c-221">Actualmente, las credenciales SQL U son Hola único tipo de elemento de catálogo que se puede crear a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53b5c-221">Currently, U-SQL credentials are hello only type of catalog item that you can create through PowerShell.</span></span>

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="53b5c-222">Obtener información básica sobre una cuenta de ADLA</span><span class="sxs-lookup"><span data-stu-id="53b5c-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="53b5c-223">Debido a un nombre de cuenta, Hola siguiente código busca información básica acerca de la cuenta de hello</span><span class="sxs-lookup"><span data-stu-id="53b5c-223">Given an account name, hello following code looks up basic information about hello account</span></span>

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a><span data-ttu-id="53b5c-224">Trabajo con Azure</span><span class="sxs-lookup"><span data-stu-id="53b5c-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="53b5c-225">Obtener detalles de errores de AzureRm</span><span class="sxs-lookup"><span data-stu-id="53b5c-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="53b5c-226">Comprobar si está ejecutando como administrador</span><span class="sxs-lookup"><span data-stu-id="53b5c-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="53b5c-227">Buscar un elemento TenantID</span><span class="sxs-lookup"><span data-stu-id="53b5c-227">Find a TenantID</span></span>

<span data-ttu-id="53b5c-228">A partir de un nombre de suscripción:</span><span class="sxs-lookup"><span data-stu-id="53b5c-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="53b5c-229">A partir de un identificador de suscripción:</span><span class="sxs-lookup"><span data-stu-id="53b5c-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="53b5c-230">A partir de una dirección de dominio como "contoso.com"</span><span class="sxs-lookup"><span data-stu-id="53b5c-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="53b5c-231">Enumerar todas las suscripciones e identificadores de inquilino</span><span class="sxs-lookup"><span data-stu-id="53b5c-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="53b5c-232">Creación de una cuenta de Data Lake Analytics mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="53b5c-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="53b5c-233">También puede usar una plantilla de grupo de recursos de Azure con hello siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="53b5c-233">You can also use an Azure Resource Group template using hello following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="53b5c-234">Para obtener más información , consulte el artículo sobre cómo [implementar una aplicación con la plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) y [crear plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="53b5c-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="53b5c-235">**Plantilla de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="53b5c-235">**Example template**</span></span>

<span data-ttu-id="53b5c-236">Guardar Hola después de texto como un `.json` de archivos y, a continuación, usar hello anterior plantilla de hello toouse de script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53b5c-236">Save hello following text as a `.json` file, and then use hello preceding PowerShell script toouse hello template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="53b5c-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="53b5c-237">Next steps</span></span>
* [<span data-ttu-id="53b5c-238">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="53b5c-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="53b5c-239">Introducción a Data Lake Analytics mediante [Azure Portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="53b5c-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="53b5c-240">Administración de Azure Data Lake Analytics mediante [Azure Portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="53b5c-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
