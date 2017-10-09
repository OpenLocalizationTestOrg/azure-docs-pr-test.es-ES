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
# <a name="manage-azure-data-lake-analytics-using-python"></a>Administración de Azure Data Lake Analytics con Python

## <a name="python-versions"></a>Versiones de Python

* Use una versión de Python de 64 bits.
* Puede utilizar la distribución Python estándar Hola que se encuentra en  **[Python.org descarga](https://www.python.org/downloads/)**. 
* Muchos desarrolladores resulte conveniente toouse hello  **[distribución de Anaconda Python](https://www.continuum.io/downloads)**.  
* En este artículo se escribió con Python versión 3.6 de distribución estándar de Python de Hola

## <a name="install-azure-python-sdk"></a>Instalación del SDK de Python de Azure

Instalar Hola siguientes módulos:

* Hola **recursos de administración de azure** módulo incluye otros módulos de Azure para Active Directory, etcetera.
* Hola **datalake tienda azure-mgmt** módulo incluye operaciones de administración de cuenta de almacén de Azure Data Lake Hola.
* Hola **tienda de azure datalake** módulo incluye operaciones de sistema de archivos de almacén de Azure Data Lake de Hola. 
* Hola **análisis de datalake de azure** módulo incluye las operaciones de análisis de Azure Data Lake de Hola. 

En primer lugar, asegúrese de tener hello más reciente `pip` ejecutando Hola siguiente comando:

```
python -m pip install --upgrade pip
```

Este documento se ha escrito con `pip version 9.0.1`.

Utilice siguiente hello `pip` comandos tooinstall módulos de Hola desde la línea de comandos hello:

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a>Creación de un nuevo script de Python

Pegue Hola siguiente código en el script de Hola:

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

Ejecute este script tooverify ese hello módulos pueden importarse.

## <a name="authentication"></a>Autenticación

### <a name="interactive-user-authentication-with-a-pop-up"></a>Autenticación interactiva de usuarios con elemento emergente

Este método no se admite.

### <a name="interactive-user-authentication-with-a-device-code"></a>Autenticación interactiva de usuarios con código de dispositivo

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a>Autenticación no interactiva con SPI y secreto

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a>Autenticación no interactiva con API y certificado

Este método no se admite.

## <a name="common-script-variables"></a>Variables de script comunes

Estas variables se utilizan en los ejemplos de hello.

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a>Crear a clientes Hola

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a>Crear un grupo de recursos de Azure

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a>Creación de una cuenta de Análisis de Data Lake

En primer lugar, cree una cuenta de almacenamiento.

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
A continuación, cree una cuenta de ADLA que utilice ese almacén.

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

## <a name="submit-a-job"></a>Enviar un trabajo

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

## <a name="wait-for-a-job-tooend"></a>Espere a que un trabajo tooend

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a>Enumerar las canalizaciones y las repeticiones
Dependiendo de si los trabajos tienen metadatos adjuntos de canalización o repetición, puede enumerar las canalizaciones y las repeticiones.

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a>Administración de nodos directivas de proceso

objeto de Hello DataLakeAnalyticsAccountManagementClient proporciona métodos para administrar Hola proceso directivas para una cuenta de análisis de Data Lake.

### <a name="list-compute-policies"></a>Enumeración de directivas de proceso

Hola siguiente código recupera una lista de las directivas de proceso para una cuenta de análisis de Data Lake.

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a>Creación de una nueva directiva de proceso

Hola siguiente código crea una nueva directiva de cálculo para una cuenta de análisis de Data Lake, configuración Hola máximo AUs disponible toohello especificada too50 de usuario y too250 de prioridad de trabajo mínimo de Hola.

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a>Pasos siguientes

- Hola toosee mismo tutorial con otras herramientas, haga clic en los selectores de pestaña hello en la parte superior de Hola de página Hola.
- toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
- Para conocer las tareas de administración, consulte [Administración de Azure Data Lake Analytics mediante el Azure Portal](data-lake-analytics-manage-use-portal.md).

