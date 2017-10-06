---
title: "aaaUse Hola Python SDK tooget a trabajar con el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Obtenga información acerca de cómo el sistema de archivos toouse toowork de SDK de Python con hello y cuentas de almacén de Data Lake."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a>Introducción al uso de Python por parte de Azure Data Lake Store

> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK de Java](data-lake-store-get-started-java-sdk.md)
> * [API de REST](data-lake-store-get-started-rest-api.md)
> * [CLI de Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Obtenga información acerca de cómo toouse Hola Python SDK de Azure y almacén de Azure Data Lake tooperform las operaciones básicas, como crean carpetas, cargar y descargar archivos de datos, etcetera. Para más información sobre Data Lake, consulte [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Requisitos previos

* **Python**. Python se puede descargar desde [aquí](https://www.python.org/downloads/). En este artículo se usa Python 3.5.2.

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Cree una aplicación de Azure Active Directory**. Usar la aplicación de almacén de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD. Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**. Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).

## <a name="install-hello-modules"></a>Instalar los módulos de Hola

toowork con el almacén de Data Lake con Python, deberá tooinstall tres módulos.

* Hola `azure-mgmt-resource` módulo. Aquí se incluyen módulos de Azure para Active Directory, etc.
* Hola `azure-mgmt-datalake-store` módulo. Esto incluye operaciones de administración de cuenta de almacén de Azure Data Lake Hola. Para más información acerca de este módulo, consulte [referencia al módulo de Azure Data Lake Management Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).
* Hola `azure-datalake-store` módulo. Esto incluye las operaciones de sistema de archivos de almacén de Azure Data Lake de Hola. Para más información acerca de este módulo, consulte [referencia al módulo de Azure Data Lake Store Filesystem](http://azure-datalake-store.readthedocs.io/en/latest/).

Usar hello después de módulos de hello tooinstall de comandos.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>Creación de una nueva aplicación de Python

1. Hola IDE de su elección, cree una nueva aplicación de Python, por ejemplo, **mysample.py**.

2. Agregar Hola después de módulos de líneas tooimport Hola necesario

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. Guardar cambios toomysample.py.

## <a name="authentication"></a>Autenticación

En esta sección, hablamos tooauthenticate de maneras diferentes de hello con Azure AD. Hola opciones disponibles son:

* Autenticación de usuario final
* Autenticación entre servicios
* Multi-Factor Authentication

Estas opciones de autenticación se deben usar tanto para la administración de cuentas como para los módulos de administración del sistema de archivos.

### <a name="end-user-authentication-for-account-management"></a>Autenticación de usuario final para la administración de cuentas

Utilice este tooauthenticate con Azure AD para operaciones de administración de cuenta (crear o eliminar cuenta de almacén de Data Lake, etcetera.). Debe proporcionar el nombre de usuario y la contraseña para un usuario de Azure AD. Tenga en cuenta que el usuario hello no debe configurarse para la autenticación multifactor.

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>Autenticación de usuario final para operaciones del sistema de archivos

Utilice este tooauthenticate con Azure AD para las operaciones de sistema de archivos (crear carpeta, archivo de carga, etcetera.). Se utiliza con una aplicación **cliente nativa** de Azure AD. usuario de Hello Azure AD para que proporcionar credenciales no debe estar configurado para la autenticación multifactor.

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>Autenticación de servicio a servicio con el secreto de cliente para la administración de cuentas

Utilice este tooauthenticate con Azure AD para operaciones de administración de cuenta (crear o eliminar cuenta de almacén de Data Lake, etcetera.). Hola siguiente fragmento de código puede ser tooauthenticate usado la aplicación de forma no interactiva, usando el secreto del cliente de Hola para una identidad de aplicación / servicio. Utilícelo con una aplicación de "aplicación web" de Azure AD.

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>Autenticación de servicio a servicio con el secreto de cliente para las operaciones del sistema de archivos

Utilice este tooauthenticate con Azure AD para las operaciones de sistema de archivos (crear carpeta, archivo de carga, etcetera.). Hola siguiente fragmento de código puede ser tooauthenticate usado la aplicación de forma no interactiva, usando el secreto del cliente de Hola para una identidad de aplicación / servicio. Utilícelo con una aplicación de "aplicación web" de Azure AD.

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>Multi-Factor Authentication para la administración de cuentas

Utilice este tooauthenticate con Azure AD para operaciones de administración de cuenta (crear o eliminar cuenta de almacén de Data Lake, etcetera.). Hello siguiente fragmento de código se pueden usar tooauthenticate su aplicación mediante la autenticación multifactor. Utilícelo con una aplicación de "aplicación web" de Azure AD.

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a>Multi-Factor Authentication para la administración del sistema de archivos

Utilice este tooauthenticate con Azure AD para las operaciones de sistema de archivos (crear carpeta, archivo de carga, etcetera.). Hello siguiente fragmento de código se pueden usar tooauthenticate su aplicación mediante la autenticación multifactor. Utilícelo con una aplicación de "aplicación web" de Azure AD.

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>Crear un grupo de recursos de Azure

Usar hello siguiente fragmento de código toocreate un grupo de recursos de Azure:

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a>Creación de clientes y de una cuenta de Data Lake Store

Hola siguiente fragmento de código primero crea a cliente de cuenta de almacén de Data Lake Hola. Usa Hola cliente objeto toocreate una cuenta de almacén de Data Lake. Por último, el fragmento de código de hello crea un objeto de cliente de sistema de archivos.

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a>Lista de cuentas de almacén de Data Lake de Hola

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>Creación de directorios

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>Cargar un archivo


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>Descarga de un archivo

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>Eliminación de un directorio

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>Consulte también

- [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
- [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Referencia de SDK de .NET de Data Lake Store](https://msdn.microsoft.com/library/mt581387.aspx)
- [Referencia de REST de Data Lake Store](https://msdn.microsoft.com/library/mt693424.aspx)
