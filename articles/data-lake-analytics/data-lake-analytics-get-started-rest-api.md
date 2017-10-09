---
title: "aaaGet a trabajar con análisis de Data Lake mediante API de REST | Documentos de Microsoft"
description: "Use las API de REST de WebHDFS tooperform operaciones de análisis de Data Lake"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a>Introducción a Azure Data Lake Analytics mediante API de REST
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Obtenga información acerca de cómo toouse WebHDFS API de REST y las API de REST de análisis de datos Lake toomanage análisis de Data Lake cuentas, trabajos y de catálogo. 

## <a name="prerequisites"></a>Requisitos previos
* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Cree una aplicación de Azure Active Directory**. Usar la aplicación de análisis de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD. Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**. Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticar con análisis de Data Lake con Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). En este artículo usa toodemonstrate cURL cómo toomake API de REST se llama con una cuenta de análisis de Data Lake.

## <a name="authenticate-with-azure-active-directory"></a>Autenticación mediante Azure Active Directory
Hay dos métodos para autenticar con Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Autenticación de usuario final (interactiva)
Con este método, aplicación solicita Hola usuario toolog en y se realizan todas las operaciones de hello en contexto de saludo del usuario de Hola. 

Siga estos pasos para la autenticación interactiva:

1. A través de la aplicación, redirigir Hola usuario toohello después de la dirección URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<URI de redireccionamiento > necesita toobe codificado para su uso en una dirección URL. Por lo tanto, para https://localhost, use `https%3A%2F%2Flocalhost`).
   > 
   > 
   
    A fin de Hola de este tutorial, puede reemplazar los valores de marcador de posición de hello en dirección URL de hello anteriormente y péguelo en la barra de direcciones del explorador de web. Será redirigido tooauthenticate mediante el inicio de sesión de Azure. Una vez correctamente, inicie sesión, respuesta de Hola se muestra en la barra de direcciones del explorador de Hola. respuesta de Hello será Hola siguiendo el formato siguiente:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Capturar el código de autorización de Hola de respuesta de Hola. Para este tutorial, puede copiar el código de autorización de Hola de barra de direcciones de hello del explorador web de Hola y páselo en hello POST solicitud toohello extremo de token, tal y como se muestra a continuación:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > En este caso, Hola \<REDIRECT-URI > no deben codificarse.
   > 
   > 
3. respuesta de Hello es un objeto JSON que contiene un token de acceso (p. ej., `"access_token": "<ACCESS_TOKEN>"`) y un token de actualización (p. ej., `"refresh_token": "<REFRESH_TOKEN>"`). La aplicación usa Hola token de acceso al obtener acceso a almacén de Azure Data Lake y tooget de token de actualización de hello otro token de acceso cuando caduca un token de acceso.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Cuando expira el token de acceso de hello, puede solicitar un nuevo token de acceso con el token de actualización de hello, tal y como se muestra a continuación:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Para más información sobre la autenticación interactiva de usuarios, consulte el [flujo de concesión de un código de autorización](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Autenticación de servicio a servicio (no interactiva)
Con este método, aplicación proporciona sus propias credenciales operaciones de hello tooperform. Para ello, debe emitir una solicitud POST como Hola se muestra a continuación: 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

salida de Hello de esta solicitud incluirá un token de autorización (indicado por `access-token` en la siguiente salida de Hola) que se pasará posteriormente con las llamadas de API de REST. Guarde este token de autenticación en un archivo de texto; lo necesitará más adelante en este artículo.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

En este artículo usa hello **no interactivo** enfoque. Para obtener más información sobre no interactivo (llamadas de servicio a servicio), consulte [llamadas de tooservice utilizando las credenciales del servicio](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-analytics-account"></a>Creación de una cuenta de Análisis de Data Lake
Debe crear un grupo de recursos de Azure y una cuenta de Data Lake Store antes de poder crear una cuenta de Data Lake Analytics.  Consulte [Creación de una cuenta de Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).

Hola después del comando Curl mostrará cómo toocreate una cuenta:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

Reemplace \< `REDACTED` \> con token de autorización de hello, \< `AzureSubscriptionID` \> con su identificador de suscripción, \< `AzureResourceGroupName` \> con un recurso de Azure existente Nombre de grupo, y \< `NewAzureDataLakeAnalyticsAccountName` \> con un nuevo nombre de cuenta de análisis de Data Lake. carga de la solicitud de Hola para este comando se encuentra en hello **CreateDatalakeAnalyticsAccountRequest.json** archivo que se proporciona para hello `-d` parámetro anterior. Hola contenido del archivo de input.json hello es similar siguiente hello:

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a>Lista de las cuentas de Data Lake Analytics en una suscripción
Hola siguiente Curl comando muestra cómo toolist cuentas en una suscripción:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

Reemplace \< `REDACTED` \> con token de autorización de hello, \< `AzureSubscriptionID` \> con su identificador de suscripción. es similar a la salida de Hello:

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a>Información acerca de una cuenta de Data Lake Analytics
Hola después del comando Curl mostrará cómo tooget una información de cuenta:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

Reemplace \< `REDACTED` \> con token de autorización de hello, \< `AzureSubscriptionID` \> con su identificador de suscripción, \< `AzureResourceGroupName` \> con un recurso de Azure existente Nombre de grupo, y \< `DataLakeAnalyticsAccountName` \> con el nombre de Hola de una cuenta de análisis de Data Lake existente. es similar a la salida de Hello:

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a>Lista de instancias de Data Lake Store de una cuenta de Data Lake Analytics
Hola siguiente Curl comando muestra cómo almacena toolist Data Lake de una cuenta:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

Reemplace \< `REDACTED` \> con token de autorización de hello, \< `AzureSubscriptionID` \> con su identificador de suscripción, \< `AzureResourceGroupName` \> con un recurso de Azure existente Nombre de grupo, y \< `DataLakeAnalyticsAccountName` \> con el nombre de Hola de una cuenta de análisis de Data Lake existente. es similar a la salida de Hello:

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a>Envío de trabajos de U-SQL
Hola después del comando Curl mostrará cómo trabajo toosubmit U T-SQL:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

Reemplace \< `REDACTED` \> con token de autorización de hello, \< `DataLakeAnalyticsAccountName` \> con el nombre de Hola de una cuenta de análisis de Data Lake existente. carga de la solicitud de Hola para este comando se encuentra en hello **SubmitADLAJob.json** archivo que se proporciona para hello `-d` parámetro anterior. Hola contenido del archivo de input.json hello es similar siguiente hello:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

es similar a la salida de Hello:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a>Lista de trabajos de U-SQL
Hola después del comando Curl mostrará cómo trabajos toolist U-SQL:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

Reemplace \< `REDACTED` \> con token de autorización de Hola y \< `DataLakeAnalyticsAccountName` \> con el nombre de Hola de una cuenta de análisis de Data Lake existente. 

es similar a la salida de Hello:

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a>Obtener elementos del catálogo
Hola siguiente Curl comando muestra cómo las bases de datos de tooget Hola de Hola catálogo:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

es similar a la salida de Hello:

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a>Otras referencias
* toosee una consulta más compleja, vea [sitio Web de analizar registros con análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* tooget a desarrollar aplicaciones SQL U, consulte [scripts U T-SQL desarrollar con Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
* Para conocer las tareas de administración, consulte [Administración de Azure Data Lake Analytics mediante el Azure Portal](data-lake-analytics-manage-use-portal.md).
* vea tooget un resumen de análisis de Data Lake [información general de análisis de Azure Data Lake](data-lake-analytics-overview.md).
* Hola toosee mismo tutorial con otras herramientas, haga clic en los selectores de pestaña hello en la parte superior de Hola de página Hola.

