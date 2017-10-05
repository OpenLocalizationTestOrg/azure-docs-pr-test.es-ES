---
title: "Administración de Azure Data Lake Analytics con Azure PowerShell | Microsoft Docs"
description: "Aprenda a administrar cuentas de Data Lake Analytics, orígenes de datos, trabajos y elementos de catálogo. "
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
ms.openlocfilehash: 862e9551f1e129b7bba06651fbae94e337c92dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="abdc7-103">Administración de Análisis de Azure Data Lake mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="abdc7-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="abdc7-104">Aprenda a administrar cuentas de Azure Data Lake Analytics, orígenes de datos, trabajos y elementos de catálogo mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abdc7-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="abdc7-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="abdc7-105">Prerequisites</span></span>

<span data-ttu-id="abdc7-106">Al crear una cuenta de Data Lake Analytics, debe saber:</span><span class="sxs-lookup"><span data-stu-id="abdc7-106">When creating a Data Lake Analytics account, you need to know:</span></span>

* <span data-ttu-id="abdc7-107">**Id. de suscripción**: Id. de la suscripción de Azure en la que reside la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="abdc7-107">**Subscription ID**: The Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="abdc7-108">**Grupo de recursos**: el nombre del grupo de recursos de Azure que contiene la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="abdc7-108">**Resource group**: The name of the Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="abdc7-109">**Nombre de la cuenta de Data Lake Analytics**: el nombre de la cuenta solo debe contener letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="abdc7-109">**Data Lake Analytics account name**: The account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="abdc7-110">**Cuenta predeterminada de Data Lake Store**: cada cuenta de Data Lake Analytics tiene una cuenta de Data Lake Store predeterminada.</span><span class="sxs-lookup"><span data-stu-id="abdc7-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="abdc7-111">Estas cuentas deben estar en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="abdc7-111">These accounts must be in the same location.</span></span>
* <span data-ttu-id="abdc7-112">**Ubicación**: la ubicación de la cuenta de Data Lake Analytics como "Este de EE. UU. 2" u otras ubicaciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="abdc7-112">**Location**: The location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="abdc7-113">Las ubicaciones admitidas se pueden consultar en nuestra [página de precios](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="abdc7-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="abdc7-114">Los fragmentos de código de PowerShell de este tutorial usan estas variables para almacenar esta información</span><span class="sxs-lookup"><span data-stu-id="abdc7-114">The PowerShell snippets in this tutorial use these variables to store this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="abdc7-115">Registro</span><span class="sxs-lookup"><span data-stu-id="abdc7-115">Log in</span></span>

<span data-ttu-id="abdc7-116">Inicie sesión con un identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="abdc7-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="abdc7-117">Inicie sesión con un nombre de suscripción.</span><span class="sxs-lookup"><span data-stu-id="abdc7-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="abdc7-118">El cmdlet `Login-AzureRmAccount` siempre pide las credenciales.</span><span class="sxs-lookup"><span data-stu-id="abdc7-118">The `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="abdc7-119">Puede evitar que se le pidan mediante los cmdlets siguientes:</span><span class="sxs-lookup"><span data-stu-id="abdc7-119">You can avoid being prompted by using the following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="abdc7-120">Administración de cuentas</span><span class="sxs-lookup"><span data-stu-id="abdc7-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="abdc7-121">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="abdc7-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="abdc7-122">Si aún no tiene un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) para usar, cree uno.</span><span class="sxs-lookup"><span data-stu-id="abdc7-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) to use, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="abdc7-123">Cada cuenta de Data Lake Analytics requiere una cuenta predeterminada de Data Lake Store que se usa para almacenar registros.</span><span class="sxs-lookup"><span data-stu-id="abdc7-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="abdc7-124">Puede reutilizar una cuenta existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="abdc7-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="abdc7-125">Una vez que un grupo de recursos y una cuenta de Data Lake Store estén disponibles, cree una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="abdc7-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="abdc7-126">Obtener información de una cuenta</span><span class="sxs-lookup"><span data-stu-id="abdc7-126">Get information about an account</span></span>

<span data-ttu-id="abdc7-127">Obtener detalles acerca de una cuenta.</span><span class="sxs-lookup"><span data-stu-id="abdc7-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="abdc7-128">Comprobar la existencia de una cuenta específica de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="abdc7-128">Check the existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="abdc7-129">El cmdlet devuelve `True` o `False`.</span><span class="sxs-lookup"><span data-stu-id="abdc7-129">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="abdc7-130">Compruebe la existencia de una cuenta determinada de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="abdc7-130">Check the existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="abdc7-131">El cmdlet devuelve `True` o `False`.</span><span class="sxs-lookup"><span data-stu-id="abdc7-131">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="abdc7-132">Lista de cuentas</span><span class="sxs-lookup"><span data-stu-id="abdc7-132">Listing accounts</span></span>

<span data-ttu-id="abdc7-133">Enumerar cuentas de Data Lake Analytics dentro de la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="abdc7-133">List Data Lake Analytics accounts within the current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="abdc7-134">Enumerar cuentas de Data Lake Analytics dentro de un grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="abdc7-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="abdc7-135">Administración de reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="abdc7-135">Managing firewall rules</span></span>

<span data-ttu-id="abdc7-136">Enumerar reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="abdc7-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="abdc7-137">Agregar una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="abdc7-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="abdc7-138">Cambiar una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="abdc7-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="abdc7-139">Eliminar una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="abdc7-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="abdc7-140">Permitir direcciones IP de Azure.</span><span class="sxs-lookup"><span data-stu-id="abdc7-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="abdc7-141">Administración de orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="abdc7-141">Managing data sources</span></span>
<span data-ttu-id="abdc7-142">Actualmente, Azure Data Lake Analytics admite los siguientes orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="abdc7-142">Azure Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="abdc7-143">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="abdc7-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="abdc7-144">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="abdc7-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="abdc7-145">Cuando se crea una cuenta de Analytics, se debe designar una cuenta de Data Lake Store para que sea el origen de datos predeterminado.</span><span class="sxs-lookup"><span data-stu-id="abdc7-145">When you create an Analytics account, you must designate a Data Lake Store account to be the default data source.</span></span> <span data-ttu-id="abdc7-146">La cuenta predeterminada de Almacén de Data Lake sirve para almacenar los registros de auditoría y de metadatos de trabajos.</span><span class="sxs-lookup"><span data-stu-id="abdc7-146">The default Data Lake Store account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="abdc7-147">Una vez creada la cuenta de Data Lake Analytics, puede agregar más cuentas de Data Lake Store o cuentas de Storage.</span><span class="sxs-lookup"><span data-stu-id="abdc7-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-the-default-data-lake-store-account"></a><span data-ttu-id="abdc7-148">Búsqueda de la cuenta predeterminada de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="abdc7-148">Find the default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="abdc7-149">Puede encontrar la cuenta predeterminada de Data Lake Store si filtra la lista de orígenes de datos por la propiedad `IsDefault`:</span><span class="sxs-lookup"><span data-stu-id="abdc7-149">You can find the default Data Lake Store account by filtering the list of datasources by the `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="abdc7-150">Agregar un origen de datos</span><span class="sxs-lookup"><span data-stu-id="abdc7-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="abdc7-151">Enumerar orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="abdc7-151">List data sources</span></span>

```powershell
# List all the data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="abdc7-152">Envío de trabajos de U-SQL</span><span class="sxs-lookup"><span data-stu-id="abdc7-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="abdc7-153">Enviar una cadena como un script U-SQL</span><span class="sxs-lookup"><span data-stu-id="abdc7-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="abdc7-154">Enviar un archivo como un script U-SQL</span><span class="sxs-lookup"><span data-stu-id="abdc7-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="abdc7-155">Enumerar trabajos en una cuenta</span><span class="sxs-lookup"><span data-stu-id="abdc7-155">List jobs in an account</span></span>

### <a name="list-all-the-jobs-in-the-account"></a><span data-ttu-id="abdc7-156">Muestre todos los trabajos de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="abdc7-156">List all the jobs in the account.</span></span> 

<span data-ttu-id="abdc7-157">El resultado incluye los trabajos actualmente en ejecución y aquellos que se han completado recientemente.</span><span class="sxs-lookup"><span data-stu-id="abdc7-157">The output includes the currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="abdc7-158">Mostrar un número determinado de trabajos</span><span class="sxs-lookup"><span data-stu-id="abdc7-158">List a specific number of jobs</span></span>

<span data-ttu-id="abdc7-159">De forma predeterminada, la lista de trabajos se ordena por hora de envío.</span><span class="sxs-lookup"><span data-stu-id="abdc7-159">By default the list of jobs is sorted on submit time.</span></span> <span data-ttu-id="abdc7-160">Así, los trabajos enviados más recientemente aparecen en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="abdc7-160">So the most recently submitted jobs appear first.</span></span> <span data-ttu-id="abdc7-161">De forma predeterminada, la cuenta de ADLA recuerda los trabajos durante 180 días, pero el cmdlet Ge-AdlJob devuelve solo los primeros 500.</span><span class="sxs-lookup"><span data-stu-id="abdc7-161">By default, The ADLA account remembers jobs for 180 days, but the Ge-AdlJob  cmdlet by default returns only the first 500.</span></span> <span data-ttu-id="abdc7-162">Use el parámetro -Top para mostrar un número específico de trabajos.</span><span class="sxs-lookup"><span data-stu-id="abdc7-162">Use -Top parameter to list a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-the-value-of-job-property"></a><span data-ttu-id="abdc7-163">Enumerar trabajos según el valor de la propiedad del trabajo</span><span class="sxs-lookup"><span data-stu-id="abdc7-163">List jobs based on the value of job property</span></span>

<span data-ttu-id="abdc7-164">Mediante el parámetro `-State`.</span><span class="sxs-lookup"><span data-stu-id="abdc7-164">Using the `-State` parameter.</span></span> <span data-ttu-id="abdc7-165">Puede combinar cualquiera de estos valores:</span><span class="sxs-lookup"><span data-stu-id="abdc7-165">You can combine any of these values:</span></span>

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
# List the running jobs
Get-AdlJob -Account $adla -State Running

# List the jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List the jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="abdc7-166">Use el parámetro `-Result` para detectar si los trabajos finalizados se han realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="abdc7-166">Use the `-Result` parameter to detect whether ended jobs completed successfully.</span></span> <span data-ttu-id="abdc7-167">Tiene estos valores:</span><span class="sxs-lookup"><span data-stu-id="abdc7-167">It has these values:</span></span>

* <span data-ttu-id="abdc7-168">Cancelado</span><span class="sxs-lookup"><span data-stu-id="abdc7-168">Cancelled</span></span>
* <span data-ttu-id="abdc7-169">Con error</span><span class="sxs-lookup"><span data-stu-id="abdc7-169">Failed</span></span>
* <span data-ttu-id="abdc7-170">None</span><span class="sxs-lookup"><span data-stu-id="abdc7-170">None</span></span>
* <span data-ttu-id="abdc7-171">Correcto</span><span class="sxs-lookup"><span data-stu-id="abdc7-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="abdc7-172">El parámetro `-Submitter` ayuda a identificar quién ha enviado un trabajo.</span><span class="sxs-lookup"><span data-stu-id="abdc7-172">The `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="abdc7-173">`-SubmittedAfter` es útil al filtrar por un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="abdc7-173">The `-SubmittedAfter` is useful in filtering to a time range.</span></span>


```powershell
# List  jobs submitted in the last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in the last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="abdc7-174">Escenarios comunes para enumerar trabajos</span><span class="sxs-lookup"><span data-stu-id="abdc7-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in the last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within the past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="abdc7-175">Filtrado de una lista de trabajos</span><span class="sxs-lookup"><span data-stu-id="abdc7-175">Filtering a list of jobs</span></span>

<span data-ttu-id="abdc7-176">Una vez que tenga una lista de trabajos en la sesión actual de PowerShell,</span><span class="sxs-lookup"><span data-stu-id="abdc7-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="abdc7-177">puede usar cmdlets normales de PowerShell para filtrar la lista.</span><span class="sxs-lookup"><span data-stu-id="abdc7-177">You can use normal PowerShell cmdlets to filter the list.</span></span>

<span data-ttu-id="abdc7-178">Filtrar una lista de trabajos por los trabajos enviados en las últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="abdc7-178">Filter a list of jobs to the jobs submitted in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="abdc7-179">Filtrar una lista de trabajos por los trabajos finalizados en las últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="abdc7-179">Filter a list of jobs to the jobs that ended in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="abdc7-180">Filtre una lista de trabajos por los trabajos que se han empezado a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="abdc7-180">Filter a list of jobs to the jobs that started running.</span></span> <span data-ttu-id="abdc7-181">Se puede producir un error en un trabajo en tiempo de compilación, por lo que nunca se inicia.</span><span class="sxs-lookup"><span data-stu-id="abdc7-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="abdc7-182">Se van a examinar los trabajos con errores que realmente empezaron a ejecutarse y luego experimentaron un error.</span><span class="sxs-lookup"><span data-stu-id="abdc7-182">Let's look at the failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="abdc7-183">Análisis de una lista de trabajos</span><span class="sxs-lookup"><span data-stu-id="abdc7-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="abdc7-184">Use el cmdlet `Group-Object` para analizar una lista de trabajos.</span><span class="sxs-lookup"><span data-stu-id="abdc7-184">Use the `Group-Object` cmdlet to analyze a list of jobs.</span></span>

```
# Count the number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count the number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count the number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count the number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="abdc7-185">Al realizar un análisis, puede ser útil agregar propiedades a los objetos de trabajo para facilitar el filtrado y la agrupación.</span><span class="sxs-lookup"><span data-stu-id="abdc7-185">When performing an analysis, it can be useful to add properties to the Job objects to make filtering and grouping simpler.</span></span> <span data-ttu-id="abdc7-186">El fragmento de código siguiente muestra cómo anotar un elemento JobInfo con propiedades calculadas.</span><span class="sxs-lookup"><span data-stu-id="abdc7-186">The following  snippet shows how to annotate a JobInfo with calculated properties.</span></span>

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

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="abdc7-187">Obtención de información sobre canalizaciones y repeticiones</span><span class="sxs-lookup"><span data-stu-id="abdc7-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="abdc7-188">Use el cmdlet `Get-AdlJobPipeline` para ver la información de canalización de trabajos enviados previamente.</span><span class="sxs-lookup"><span data-stu-id="abdc7-188">Use the `Get-AdlJobPipeline` cmdlet to see the pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="abdc7-189">Use el cmdlet `Get-AdlJobRecurrence` para ver la información de repetición de trabajos enviados previamente.</span><span class="sxs-lookup"><span data-stu-id="abdc7-189">Use the `Get-AdlJobRecurrence` cmdlet to see the recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="abdc7-190">Obtención de información sobre un trabajo</span><span class="sxs-lookup"><span data-stu-id="abdc7-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="abdc7-191">Obtención de estado del trabajo</span><span class="sxs-lookup"><span data-stu-id="abdc7-191">Get job status</span></span>

<span data-ttu-id="abdc7-192">Obtenga el estado de un trabajo específico.</span><span class="sxs-lookup"><span data-stu-id="abdc7-192">Get the status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-the-job-outputs"></a><span data-ttu-id="abdc7-193">Examen de las salidas del trabajo</span><span class="sxs-lookup"><span data-stu-id="abdc7-193">Examine the job outputs</span></span>

<span data-ttu-id="abdc7-194">Después de finalizar el trabajo, compruebe si existe el archivo de salida; para ello, enumere los archivos de una carpeta.</span><span class="sxs-lookup"><span data-stu-id="abdc7-194">After the job has ended, check if the output file exists by listing the files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="abdc7-195">Administración de trabajos en ejecución</span><span class="sxs-lookup"><span data-stu-id="abdc7-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="abdc7-196">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="abdc7-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-to-finish"></a><span data-ttu-id="abdc7-197">Espera de fin de un trabajo</span><span class="sxs-lookup"><span data-stu-id="abdc7-197">Wait for a job to finish</span></span>

<span data-ttu-id="abdc7-198">En lugar de repetir `Get-AdlAnalyticsJob` hasta que finalice un trabajo, puede usar el cmdlet `Wait-AdlJob` para esperar a que finalice el trabajo.</span><span class="sxs-lookup"><span data-stu-id="abdc7-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use the `Wait-AdlJob` cmdlet to wait for the job to end.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="abdc7-199">Administración de nodos directivas de proceso</span><span class="sxs-lookup"><span data-stu-id="abdc7-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="abdc7-200">Lista de directivas de proceso existentes</span><span class="sxs-lookup"><span data-stu-id="abdc7-200">List existing compute policies</span></span>

<span data-ttu-id="abdc7-201">El cmdlet `Get-AdlAnalyticsComputePolicy` recupera información sobre las directivas de proceso de una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="abdc7-201">The `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="abdc7-202">Creación de una directiva de proceso</span><span class="sxs-lookup"><span data-stu-id="abdc7-202">Create a compute policy</span></span>

<span data-ttu-id="abdc7-203">El cmdlet `New-AdlAnalyticsComputePolicy` crea una nueva directiva de proceso para una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="abdc7-203">The `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="abdc7-204">En este ejemplo se establecen las unidades de asignación (AU) máximas disponibles para el usuario especificado en 50 y la prioridad mínima del trabajo en 250.</span><span class="sxs-lookup"><span data-stu-id="abdc7-204">This example sets  the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-the-existence-of-a-file"></a><span data-ttu-id="abdc7-205">Compruebe la existencia de un archivo.</span><span class="sxs-lookup"><span data-stu-id="abdc7-205">Check for the existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="abdc7-206">Carga y descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="abdc7-206">Uploading and downloading</span></span>

<span data-ttu-id="abdc7-207">Cargar un archivo.</span><span class="sxs-lookup"><span data-stu-id="abdc7-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="abdc7-208">Cargue una carpeta completa de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="abdc7-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="abdc7-209">Descargar un archivo.</span><span class="sxs-lookup"><span data-stu-id="abdc7-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="abdc7-210">Descargue una carpeta completa de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="abdc7-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="abdc7-211">Si se interrumpe el proceso de carga o descarga, puede intentar reanudar el proceso ejecutando el cmdlet de nuevo con la opción ``-Resume``.</span><span class="sxs-lookup"><span data-stu-id="abdc7-211">If the upload or download process is interrupted, you can attempt to resume the process by running the cmdlet again with the ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="abdc7-212">Administración de elementos de catálogo</span><span class="sxs-lookup"><span data-stu-id="abdc7-212">Manage catalog items</span></span>

<span data-ttu-id="abdc7-213">El catálogo de U-SQL se usa para estructurar datos y código, para que puedan compartirse mediante scripts de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="abdc7-213">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="abdc7-214">El catálogo permite el mayor rendimiento posible con los datos en Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="abdc7-214">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="abdc7-215">Para obtener más información, consulte [Uso del catálogo de U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="abdc7-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-the-u-sql-catalog"></a><span data-ttu-id="abdc7-216">Enumerar elementos en el catálogo de U-SQL</span><span class="sxs-lookup"><span data-stu-id="abdc7-216">List items in the U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="abdc7-217">Enumere todos los ensamblados de todas las bases de datos de una cuenta de ADLA.</span><span class="sxs-lookup"><span data-stu-id="abdc7-217">List all the assemblies in all the databases in an ADLA Account.</span></span>

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

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="abdc7-218">Obtener detalles sobre un elemento de catálogo</span><span class="sxs-lookup"><span data-stu-id="abdc7-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="abdc7-219">Crear credenciales en un catálogo</span><span class="sxs-lookup"><span data-stu-id="abdc7-219">Create credentials in a catalog</span></span>

<span data-ttu-id="abdc7-220">Dentro de una base de datos U-SQL, cree un objeto de credenciales para una base de datos hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="abdc7-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="abdc7-221">Actualmente, las credenciales U-SQL son el único tipo de elemento de catálogo que se puede crear a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abdc7-221">Currently, U-SQL credentials are the only type of catalog item that you can create through PowerShell.</span></span>

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

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="abdc7-222">Obtener información básica sobre una cuenta de ADLA</span><span class="sxs-lookup"><span data-stu-id="abdc7-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="abdc7-223">Dado un nombre de cuenta, el código siguiente busca información básica sobre la cuenta</span><span class="sxs-lookup"><span data-stu-id="abdc7-223">Given an account name, the following code looks up basic information about the account</span></span>

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

## <a name="working-with-azure"></a><span data-ttu-id="abdc7-224">Trabajo con Azure</span><span class="sxs-lookup"><span data-stu-id="abdc7-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="abdc7-225">Obtener detalles de errores de AzureRm</span><span class="sxs-lookup"><span data-stu-id="abdc7-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="abdc7-226">Comprobar si está ejecutando como administrador</span><span class="sxs-lookup"><span data-stu-id="abdc7-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="abdc7-227">Buscar un elemento TenantID</span><span class="sxs-lookup"><span data-stu-id="abdc7-227">Find a TenantID</span></span>

<span data-ttu-id="abdc7-228">A partir de un nombre de suscripción:</span><span class="sxs-lookup"><span data-stu-id="abdc7-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="abdc7-229">A partir de un identificador de suscripción:</span><span class="sxs-lookup"><span data-stu-id="abdc7-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="abdc7-230">A partir de una dirección de dominio como "contoso.com"</span><span class="sxs-lookup"><span data-stu-id="abdc7-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="abdc7-231">Enumerar todas las suscripciones e identificadores de inquilino</span><span class="sxs-lookup"><span data-stu-id="abdc7-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="abdc7-232">Creación de una cuenta de Data Lake Analytics mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="abdc7-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="abdc7-233">También puede usar una plantilla de grupo de recursos de Azure mediante el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="abdc7-233">You can also use an Azure Resource Group template using the following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update the JSON template path 

# Log in to Azure
Login-AzureRmAccount -SubscriptionId $subId

# Create the resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create the Data Lake Analytics account with the default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="abdc7-234">Para obtener más información , consulte el artículo sobre cómo [implementar una aplicación con la plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) y [crear plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="abdc7-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="abdc7-235">**Plantilla de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="abdc7-235">**Example template**</span></span>

<span data-ttu-id="abdc7-236">Guarde el siguiente texto como un archivo `.json` y, a continuación, utilice el script de PowerShell anterior para usar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="abdc7-236">Save the following text as a `.json` file, and then use the preceding PowerShell script to use the template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Analytics account to create."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Store account to create."
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

## <a name="next-steps"></a><span data-ttu-id="abdc7-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abdc7-237">Next steps</span></span>
* [<span data-ttu-id="abdc7-238">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="abdc7-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="abdc7-239">Introducción a Data Lake Analytics mediante [Azure Portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="abdc7-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="abdc7-240">Administración de Azure Data Lake Analytics mediante [Azure Portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="abdc7-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
