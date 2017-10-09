---
title: "Análisis de Azure Data Lake aaaManage con Python | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Python toocreate un Data Lake almacenar la cuenta así como enviar trabajos. "
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
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="b47c2-103">Administración de Azure Data Lake Analytics con Python</span><span class="sxs-lookup"><span data-stu-id="b47c2-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="b47c2-104">Versiones de Python</span><span class="sxs-lookup"><span data-stu-id="b47c2-104">Python versions</span></span>

* <span data-ttu-id="b47c2-105">Use una versión de Python de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="b47c2-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="b47c2-106">Puede utilizar la distribución Python estándar Hola que se encuentra en  **[Python.org descarga](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="b47c2-106">You can use hello standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="b47c2-107">Muchos desarrolladores resulte conveniente toouse hello  **[distribución de Anaconda Python](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="b47c2-107">Many developers find it convenient toouse hello **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="b47c2-108">En este artículo se escribió con Python versión 3.6 de distribución estándar de Python de Hola</span><span class="sxs-lookup"><span data-stu-id="b47c2-108">This article was written using Python version 3.6 from hello standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="b47c2-109">Instalación del SDK de Python de Azure</span><span class="sxs-lookup"><span data-stu-id="b47c2-109">Install Azure Python SDK</span></span>

<span data-ttu-id="b47c2-110">Instalar Hola siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="b47c2-110">Install hello following modules:</span></span>

* <span data-ttu-id="b47c2-111">Hola **recursos de administración de azure** módulo incluye otros módulos de Azure para Active Directory, etcetera.</span><span class="sxs-lookup"><span data-stu-id="b47c2-111">hello **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="b47c2-112">Hola **datalake tienda azure-mgmt** módulo incluye operaciones de administración de cuenta de almacén de Azure Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="b47c2-112">hello **azure-mgmt-datalake-store** module includes hello Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="b47c2-113">Hola **tienda de azure datalake** módulo incluye operaciones de sistema de archivos de almacén de Azure Data Lake de Hola.</span><span class="sxs-lookup"><span data-stu-id="b47c2-113">hello **azure-datalake-store** module includes hello Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="b47c2-114">Hola **análisis de datalake de azure** módulo incluye las operaciones de análisis de Azure Data Lake de Hola.</span><span class="sxs-lookup"><span data-stu-id="b47c2-114">hello **azure-datalake-analytics** module includes hello Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="b47c2-115">En primer lugar, asegúrese de tener hello más reciente `pip` ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b47c2-115">First, ensure you have hello latest `pip` by running hello following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="b47c2-116">Este documento se ha escrito con `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="b47c2-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="b47c2-117">Utilice siguiente hello `pip` comandos tooinstall módulos de Hola desde la línea de comandos hello:</span><span class="sxs-lookup"><span data-stu-id="b47c2-117">Use hello following `pip` commands tooinstall hello modules from hello commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="b47c2-118">Creación de un nuevo script de Python</span><span class="sxs-lookup"><span data-stu-id="b47c2-118">Create a new Python script</span></span>

<span data-ttu-id="b47c2-119">Pegue Hola siguiente código en el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="b47c2-119">Paste hello following code into hello script:</span></span>

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

<span data-ttu-id="b47c2-120">Ejecute este script tooverify ese hello módulos pueden importarse.</span><span class="sxs-lookup"><span data-stu-id="b47c2-120">Run this script tooverify that hello modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="b47c2-121">Autenticación</span><span class="sxs-lookup"><span data-stu-id="b47c2-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="b47c2-122">Autenticación interactiva de usuarios con elemento emergente</span><span class="sxs-lookup"><span data-stu-id="b47c2-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="b47c2-123">Este método no se admite.</span><span class="sxs-lookup"><span data-stu-id="b47c2-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="b47c2-124">Autenticación interactiva de usuarios con código de dispositivo</span><span class="sxs-lookup"><span data-stu-id="b47c2-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="b47c2-125">Autenticación no interactiva con SPI y secreto</span><span class="sxs-lookup"><span data-stu-id="b47c2-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="b47c2-126">Autenticación no interactiva con API y certificado</span><span class="sxs-lookup"><span data-stu-id="b47c2-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="b47c2-127">Este método no se admite.</span><span class="sxs-lookup"><span data-stu-id="b47c2-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="b47c2-128">Variables de script comunes</span><span class="sxs-lookup"><span data-stu-id="b47c2-128">Common script variables</span></span>

<span data-ttu-id="b47c2-129">Estas variables se utilizan en los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="b47c2-129">These variables are used in hello samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a><span data-ttu-id="b47c2-130">Crear a clientes Hola</span><span class="sxs-lookup"><span data-stu-id="b47c2-130">Create hello clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="b47c2-131">Crear un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="b47c2-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="b47c2-132">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="b47c2-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="b47c2-133">En primer lugar, cree una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b47c2-133">First create a store account.</span></span>

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
<span data-ttu-id="b47c2-134">A continuación, cree una cuenta de ADLA que utilice ese almacén.</span><span class="sxs-lookup"><span data-stu-id="b47c2-134">Then create an ADLA account that uses that store.</span></span>

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

## <a name="submit-a-job"></a><span data-ttu-id="b47c2-135">Enviar un trabajo</span><span class="sxs-lookup"><span data-stu-id="b47c2-135">Submit a job</span></span>

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
    too"/data.csv"
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

## <a name="wait-for-a-job-tooend"></a><span data-ttu-id="b47c2-136">Espere a que un trabajo tooend</span><span class="sxs-lookup"><span data-stu-id="b47c2-136">Wait for a job tooend</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="b47c2-137">Enumerar las canalizaciones y las repeticiones</span><span class="sxs-lookup"><span data-stu-id="b47c2-137">List pipelines and recurrences</span></span>
<span data-ttu-id="b47c2-138">Dependiendo de si los trabajos tienen metadatos adjuntos de canalización o repetición, puede enumerar las canalizaciones y las repeticiones.</span><span class="sxs-lookup"><span data-stu-id="b47c2-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="b47c2-139">Administración de nodos directivas de proceso</span><span class="sxs-lookup"><span data-stu-id="b47c2-139">Manage compute policies</span></span>

<span data-ttu-id="b47c2-140">objeto de Hello DataLakeAnalyticsAccountManagementClient proporciona métodos para administrar Hola proceso directivas para una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b47c2-140">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="b47c2-141">Enumeración de directivas de proceso</span><span class="sxs-lookup"><span data-stu-id="b47c2-141">List compute policies</span></span>

<span data-ttu-id="b47c2-142">Hola siguiente código recupera una lista de las directivas de proceso para una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b47c2-142">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="b47c2-143">Creación de una nueva directiva de proceso</span><span class="sxs-lookup"><span data-stu-id="b47c2-143">Create a new compute policy</span></span>

<span data-ttu-id="b47c2-144">Hola siguiente código crea una nueva directiva de cálculo para una cuenta de análisis de Data Lake, configuración Hola máximo AUs disponible toohello especificada too50 de usuario y too250 de prioridad de trabajo mínimo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b47c2-144">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="b47c2-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b47c2-145">Next steps</span></span>

- <span data-ttu-id="b47c2-146">Hola toosee mismo tutorial con otras herramientas, haga clic en los selectores de pestaña hello en la parte superior de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="b47c2-146">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
- <span data-ttu-id="b47c2-147">toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b47c2-147">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="b47c2-148">Para conocer las tareas de administración, consulte [Administración de Azure Data Lake Analytics mediante el Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b47c2-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

