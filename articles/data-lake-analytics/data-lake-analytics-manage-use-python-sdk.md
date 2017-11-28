---
title: "Administración de Azure Data Lake Analytics con Python | Microsoft Docs"
description: "Obtenga información acerca de cómo utilizar Python para crear una cuenta de Data Lake Store y enviar trabajos. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 31326a32f8748e6cfb8bfe24cda46c511ab59352
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="8f384-103">Administración de Azure Data Lake Analytics con Python</span><span class="sxs-lookup"><span data-stu-id="8f384-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="8f384-104">Versiones de Python</span><span class="sxs-lookup"><span data-stu-id="8f384-104">Python versions</span></span>

* <span data-ttu-id="8f384-105">Use una versión de Python de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="8f384-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="8f384-106">Puede usar la distribución estándar de Python que encontrará en la sección de **[descargas de Python.org](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="8f384-106">You can use the standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="8f384-107">Muchos desarrolladores consideran conveniente usar la **[distribución de Python Anaconda](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="8f384-107">Many developers find it convenient to use the **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="8f384-108">Este artículo se escribió para la versión 3.6 de Python con la distribución de Python estándar</span><span class="sxs-lookup"><span data-stu-id="8f384-108">This article was written using Python version 3.6 from the standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="8f384-109">Instalación del SDK de Python de Azure</span><span class="sxs-lookup"><span data-stu-id="8f384-109">Install Azure Python SDK</span></span>

<span data-ttu-id="8f384-110">Instale los siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="8f384-110">Install the following modules:</span></span>

* <span data-ttu-id="8f384-111">El módulo **azure-mgmt-resource** incluye otros módulos de Azure para Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="8f384-111">The **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="8f384-112">El módulo **azure-datalake-store** incluye las operaciones de administración de cuentas de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8f384-112">The **azure-mgmt-datalake-store** module includes the Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="8f384-113">El módulo **azure-datalake-store** incluye las operaciones de sistema de archivos de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8f384-113">The **azure-datalake-store** module includes the Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="8f384-114">El módulo **azure-datalake-analytics** incluye las operaciones de Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8f384-114">The **azure-datalake-analytics** module includes the Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="8f384-115">En primer lugar, asegúrese de que dispone del último `pip`; para ello, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f384-115">First, ensure you have the latest `pip` by running the following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="8f384-116">Este documento se ha escrito con `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="8f384-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="8f384-117">Use el comando `pip` siguiente para instalar los módulos desde la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="8f384-117">Use the following `pip` commands to install the modules from the commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="8f384-118">Creación de un nuevo script de Python</span><span class="sxs-lookup"><span data-stu-id="8f384-118">Create a new Python script</span></span>

<span data-ttu-id="8f384-119">Pegue el código siguiente en el script:</span><span class="sxs-lookup"><span data-stu-id="8f384-119">Paste the following code into the script:</span></span>

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

<span data-ttu-id="8f384-120">Ejecute este script para comprobar que se pueden importar los módulos.</span><span class="sxs-lookup"><span data-stu-id="8f384-120">Run this script to verify that the modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="8f384-121">Autenticación</span><span class="sxs-lookup"><span data-stu-id="8f384-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="8f384-122">Autenticación interactiva de usuarios con elemento emergente</span><span class="sxs-lookup"><span data-stu-id="8f384-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="8f384-123">Este método no se admite.</span><span class="sxs-lookup"><span data-stu-id="8f384-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="8f384-124">Autenticación interactiva de usuarios con código de dispositivo</span><span class="sxs-lookup"><span data-stu-id="8f384-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter the user to authenticate with that has permission to subscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="8f384-125">Autenticación no interactiva con SPI y secreto</span><span class="sxs-lookup"><span data-stu-id="8f384-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="8f384-126">Autenticación no interactiva con API y certificado</span><span class="sxs-lookup"><span data-stu-id="8f384-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="8f384-127">Este método no se admite.</span><span class="sxs-lookup"><span data-stu-id="8f384-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="8f384-128">Variables de script comunes</span><span class="sxs-lookup"><span data-stu-id="8f384-128">Common script variables</span></span>

<span data-ttu-id="8f384-129">Estas variables se usan en los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="8f384-129">These variables are used in the samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-the-clients"></a><span data-ttu-id="8f384-130">Creación de los clientes</span><span class="sxs-lookup"><span data-stu-id="8f384-130">Create the clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="8f384-131">Crear un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="8f384-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="8f384-132">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="8f384-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="8f384-133">En primer lugar, cree una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8f384-133">First create a store account.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
<span data-ttu-id="8f384-134">A continuación, cree una cuenta de ADLA que utilice ese almacén.</span><span class="sxs-lookup"><span data-stu-id="8f384-134">Then create an ADLA account that uses that store.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a><span data-ttu-id="8f384-135">Enviar un trabajo</span><span class="sxs-lookup"><span data-stu-id="8f384-135">Submit a job</span></span>

```python
script = """
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
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-to-end"></a><span data-ttu-id="8f384-136">Esperar a que finalice un trabajo</span><span class="sxs-lookup"><span data-stu-id="8f384-136">Wait for a job to end</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="8f384-137">Enumerar las canalizaciones y las repeticiones</span><span class="sxs-lookup"><span data-stu-id="8f384-137">List pipelines and recurrences</span></span>
<span data-ttu-id="8f384-138">Dependiendo de si los trabajos tienen metadatos adjuntos de canalización o repetición, puede enumerar las canalizaciones y las repeticiones.</span><span class="sxs-lookup"><span data-stu-id="8f384-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="8f384-139">Administrar directivas de cálculo</span><span class="sxs-lookup"><span data-stu-id="8f384-139">Manage compute policies</span></span>

<span data-ttu-id="8f384-140">El objeto de DataLakeAnalyticsAccountManagementClient proporciona métodos para administrar las directivas de proceso de una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8f384-140">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="8f384-141">Enumeración de directivas de proceso</span><span class="sxs-lookup"><span data-stu-id="8f384-141">List compute policies</span></span>

<span data-ttu-id="8f384-142">El código siguiente recupera una lista de directivas de proceso de una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8f384-142">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="8f384-143">Creación de una nueva directiva de proceso</span><span class="sxs-lookup"><span data-stu-id="8f384-143">Create a new compute policy</span></span>

<span data-ttu-id="8f384-144">El siguiente código crea una nueva directiva de cálculo para una cuenta de análisis de Data Lake y establece que el número máximo de AU disponibles para el usuario especificado en 50 y la prioridad del trabajo mínimo en 250.</span><span class="sxs-lookup"><span data-stu-id="8f384-144">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="8f384-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f384-145">Next steps</span></span>

- <span data-ttu-id="8f384-146">Para ver el mismo tutorial con otras herramientas, haga clic en los selectores de pestañas en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="8f384-146">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
- <span data-ttu-id="8f384-147">Para obtener más información sobre U-SQL, consulte [Introducción al lenguaje U-SQL de Análisis de Azure Data Lake](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f384-147">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="8f384-148">Para conocer las tareas de administración, consulte [Administración de Azure Data Lake Analytics mediante el Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8f384-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

