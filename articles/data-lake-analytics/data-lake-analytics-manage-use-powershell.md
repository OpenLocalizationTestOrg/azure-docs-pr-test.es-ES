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
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Administración de Análisis de Azure Data Lake mediante Azure PowerShell
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Obtenga información acerca de cómo trabajos de cuentas de análisis de Azure Data Lake toomanage, orígenes de datos y elementos del catálogo con Azure PowerShell. 

## <a name="prerequisites"></a>Requisitos previos

Al crear una cuenta de análisis de Data Lake, necesita tooknow:

* **Id. de suscripción**: Hola Id. de suscripción de Azure en el que reside la cuenta de análisis de Data Lake.
* **Grupo de recursos**: nombre de Hola Hola Azure del grupo de recursos que contiene la cuenta de análisis de Data Lake.
* **Nombre de la cuenta de análisis de Data Lake**: Hola cuenta nombre solo debe contener letras minúsculas y números.
* **Cuenta predeterminada de Data Lake Store**: cada cuenta de Data Lake Analytics tiene una cuenta de Data Lake Store predeterminada. Estas cuentas deben estar en hello misma ubicación.
* **Ubicación**: ubicación de saludo de la cuenta de análisis de Data Lake, como "UU 2" u otra admite ubicaciones. Las ubicaciones admitidas se pueden consultar en nuestra [página de precios](https://azure.microsoft.com/pricing/details/data-lake-analytics/).

fragmentos de código de PowerShell de Hello en este tutorial usa estas variables toostore esta información

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>Registro

Inicie sesión con un identificador de suscripción.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

Inicie sesión con un nombre de suscripción.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

Hola `Login-AzureRmAccount` cmdlet siempre pide las credenciales. Puede evitar que se le solicite mediante el uso de hello siguientes cmdlets:

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>Administración de cuentas

### <a name="create-a-data-lake-analytics-account"></a>Creación de una cuenta de Análisis de Data Lake

Si aún no tiene un [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, cree uno. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

Cada cuenta de Data Lake Analytics requiere una cuenta predeterminada de Data Lake Store que se usa para almacenar registros. Puede reutilizar una cuenta existente o crear una nueva. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

Una vez que un grupo de recursos y una cuenta de Data Lake Store estén disponibles, cree una cuenta de Data Lake Analytics.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>Obtener información de una cuenta

Obtener detalles acerca de una cuenta.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

Comprobar la existencia de Hola de una cuenta de análisis de Data Lake concreta. Hola cmdlet devuelve `True` o `False`.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

Comprobar la existencia de Hola de una cuenta de almacén de Data Lake concreta. Hola cmdlet devuelve `True` o `False`.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>Lista de cuentas

Cuentas de análisis de Data Lake de lista dentro de la suscripción actual de Hola.

```powershell
Get-AdlAnalyticsAccount
```

Enumerar cuentas de Data Lake Analytics dentro de un grupo de recursos específico.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>Administración de reglas de firewall

Enumerar reglas de firewall.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

Agregar una regla de firewall.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Cambiar una regla de firewall.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Eliminar una regla de firewall.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Permitir direcciones IP de Azure.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>Administración de orígenes de datos
Análisis de Azure Data Lake admite actualmente Hola siguientes orígenes de datos:

* [Almacén de Azure Data Lake](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

Cuando se crea una cuenta de análisis, debe designar un origen de datos de almacén de Data Lake cuenta toobe Hola predeterminado. Hello almacén de Data Lake cuenta predeterminada se utiliza registros de auditoría de metadatos de trabajo toostore y trabajo. Una vez creada la cuenta de Data Lake Analytics, puede agregar más cuentas de Data Lake Store o cuentas de Storage. 

### <a name="find-hello-default-data-lake-store-account"></a>Buscar cuenta de almacén de Data Lake Hola predeterminada

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

Puede encontrar cuenta de almacén de Data Lake Hola predeterminada si filtra la lista de Hola de orígenes de datos por hello `IsDefault` propiedad:

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>Agregar un origen de datos

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>Enumerar orígenes de datos

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>Envío de trabajos de U-SQL

### <a name="submit-a-string-as-a-u-sql-script"></a>Enviar una cadena como un script U-SQL

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


### <a name="submit-a-file-as-a-u-sql-script"></a>Enviar un archivo como un script U-SQL

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>Enumerar trabajos en una cuenta

### <a name="list-all-hello-jobs-in-hello-account"></a>Enumera todos los trabajos de hello en la cuenta de hello. 

salida de Hello incluye Hola actualmente en ejecución trabajos y los pasos de trabajo completaron recientemente.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>Mostrar un número determinado de trabajos

De forma predeterminada se ordena la lista Hola de trabajos en el momento del envío. Por lo que se envió más recientemente Hola trabajos aparecen en primer lugar. De forma predeterminada, Hola cuenta ADLA recuerda trabajos durante 180 días, pero Hola Ge AdlJob cmdlet devuelve de forma predeterminada sólo Hola 500 primeros. Use - toolist parámetro superior un número específico de trabajos.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>Enumerar trabajos según Hola valor de propiedad del trabajo

Con hello `-State` parámetro. Puede combinar cualquiera de estos valores:

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

Hola de uso `-Result` toodetect parámetro si los trabajos finalizados se ha completado correctamente. Tiene estos valores:

* Cancelado
* Con error
* None
* Correcto

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


Hola `-Submitter` parámetro ayuda a identificar quién envió un trabajo.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

Hola `-SubmittedAfter` es útil en el intervalo de tiempo de tooa de filtrado.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>Escenarios comunes para enumerar trabajos


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

## <a name="filtering-a-list-of-jobs"></a>Filtrado de una lista de trabajos

Una vez que tenga una lista de trabajos en la sesión actual de PowerShell, Puede usar la lista de Hola de toofilter de cmdlets de PowerShell normal.

Filtrar una lista de trabajos de toohello trabajos enviados en hello últimas 24 horas

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

Filtrar una lista de trabajos de toohello de trabajos que finalizaron en hello últimas 24 horas

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

Filtrar una lista de trabajos de toohello de trabajos que se empezó a ejecutarse. Se puede producir un error en un trabajo en tiempo de compilación, por lo que nunca se inicia. Echemos un vistazo a los trabajos de hello no se pudo que realmente empezó a ejecutarse y, a continuación, no se pudo.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>Análisis de una lista de trabajos

Hola de uso `Group-Object` cmdlet tooanalyze una lista de trabajos.

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
Al realizar un análisis, puede ser útil tooadd propiedades toohello trabajo objetos toomake de filtrado y agrupación más sencilla. Hola siguiente fragmento de código muestra el modo en que tooannotate una JobInfo con calcula propiedades.

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

## <a name="get-information-about-pipelines-and-recurrences"></a>Obtención de información sobre canalizaciones y repeticiones

Hola de uso `Get-AdlJobPipeline` información de canalización de cmdlet toosee Hola enviados previamente trabajos.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

Hola de uso `Get-AdlJobRecurrence` información de periodicidad de cmdlet toosee Hola para los trabajos enviados anteriormente.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>Obtención de información sobre un trabajo

### <a name="get-job-status"></a>Obtención de estado del trabajo

Obtener estado de Hola de un trabajo específico.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Examinar Hola salidas de trabajo

Una vez ha finalizado el trabajo de hello, compruebe si existe el archivo de salida de hello haciendo una lista de archivos de hello en una carpeta.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>Administración de trabajos en ejecución

### <a name="cancel-a-job"></a>Cancelación de un trabajo

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>Espere a que un trabajo toofinish

En lugar de repetir `Get-AdlAnalyticsJob` hasta que finalice un trabajo, puede usar hello `Wait-AdlJob` toowait de cmdlet para hello tooend de trabajo.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>Administración de nodos directivas de proceso

### <a name="list-existing-compute-policies"></a>Lista de directivas de proceso existentes

Hola `Get-AdlAnalyticsComputePolicy` cmdlet recupera información acerca de las directivas de proceso para una cuenta de análisis de Data Lake.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>Creación de una directiva de proceso

Hola `New-AdlAnalyticsComputePolicy` crea una nueva directiva de cálculo para una cuenta de análisis de Data Lake. En este ejemplo conjuntos Hola toohello disponible de AUs máximo especificado too50 de usuario y too250 de prioridad de trabajo mínimo de Hola.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Comprobar existencia de Hola de un archivo.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>Carga y descarga de archivos

Cargar un archivo.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

Cargue una carpeta completa de forma recursiva.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

Descargar un archivo.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

Descargue una carpeta completa de forma recursiva.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Si hello cargar o se interrumpe el proceso de descarga, puede intentar el proceso de hello tooresume mediante la ejecución del cmdlet Hola nuevo con hello ``-Resume`` marca.

## <a name="manage-catalog-items"></a>Administración de elementos de catálogo

catálogo de Hello U-SQL es toostructure usa datos y el código para que pueda compartir por secuencias de comandos SQL U. catálogo de Hello permite Hola mayor rendimiento posible con los datos de Azure Data Lake. Para obtener más información, consulte [Uso del catálogo de U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-items-in-hello-u-sql-catalog"></a>Elementos de lista en el catálogo de hello U-SQL

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

Enumerar todos los ensamblados de hello en todas las bases de datos de hello en una cuenta de ADLA.

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

### <a name="get-details-about-a-catalog-item"></a>Obtener detalles sobre un elemento de catálogo

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>Crear credenciales en un catálogo

Dentro de una base de datos U-SQL, cree un objeto de credenciales para una base de datos hospedada en Azure. Actualmente, las credenciales SQL U son Hola único tipo de elemento de catálogo que se puede crear a través de PowerShell.

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

### <a name="get-basic-information-about-an-adla-account"></a>Obtener información básica sobre una cuenta de ADLA

Debido a un nombre de cuenta, Hola siguiente código busca información básica acerca de la cuenta de hello

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

## <a name="working-with-azure"></a>Trabajo con Azure

### <a name="get-details-of-azurerm-errors"></a>Obtener detalles de errores de AzureRm

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>Comprobar si está ejecutando como administrador

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>Buscar un elemento TenantID

A partir de un nombre de suscripción:

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

A partir de un identificador de suscripción:

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

A partir de una dirección de dominio como "contoso.com"


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>Enumerar todas las suscripciones e identificadores de inquilino

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>Creación de una cuenta de Data Lake Analytics mediante una plantilla

También puede usar una plantilla de grupo de recursos de Azure con hello siguiente script de PowerShell:

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

Para obtener más información , consulte el artículo sobre cómo [implementar una aplicación con la plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) y [crear plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

**Plantilla de ejemplo**

Guardar Hola después de texto como un `.json` de archivos y, a continuación, usar hello anterior plantilla de hello toouse de script de PowerShell. 

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

## <a name="next-steps"></a>Pasos siguientes
* [Información general de Análisis de Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* Introducción a Data Lake Analytics mediante [Azure Portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)
* Administración de Azure Data Lake Analytics mediante [Azure Portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) 
