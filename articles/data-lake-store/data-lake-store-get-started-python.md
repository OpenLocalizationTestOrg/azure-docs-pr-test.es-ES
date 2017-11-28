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
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="020ae-103">Introducción al uso de Python por parte de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="020ae-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="020ae-104">Portal</span><span class="sxs-lookup"><span data-stu-id="020ae-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="020ae-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="020ae-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="020ae-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="020ae-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="020ae-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="020ae-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="020ae-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="020ae-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="020ae-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="020ae-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="020ae-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="020ae-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="020ae-111">Python</span><span class="sxs-lookup"><span data-stu-id="020ae-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="020ae-112">Obtenga información acerca de cómo toouse Hola Python SDK de Azure y almacén de Azure Data Lake tooperform las operaciones básicas, como crean carpetas, cargar y descargar archivos de datos, etcetera. Para más información sobre Data Lake, consulte [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="020ae-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="020ae-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="020ae-113">Prerequisites</span></span>

* <span data-ttu-id="020ae-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="020ae-114">**Python**.</span></span> <span data-ttu-id="020ae-115">Python se puede descargar desde [aquí](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="020ae-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="020ae-116">En este artículo se usa Python 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="020ae-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="020ae-117">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="020ae-117">**An Azure subscription**.</span></span> <span data-ttu-id="020ae-118">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="020ae-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="020ae-119">**Cree una aplicación de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="020ae-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="020ae-120">Usar la aplicación de almacén de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="020ae-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="020ae-121">Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="020ae-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="020ae-122">Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="020ae-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="020ae-123">Instalar los módulos de Hola</span><span class="sxs-lookup"><span data-stu-id="020ae-123">Install hello modules</span></span>

<span data-ttu-id="020ae-124">toowork con el almacén de Data Lake con Python, deberá tooinstall tres módulos.</span><span class="sxs-lookup"><span data-stu-id="020ae-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="020ae-125">Hola `azure-mgmt-resource` módulo.</span><span class="sxs-lookup"><span data-stu-id="020ae-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="020ae-126">Aquí se incluyen módulos de Azure para Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="020ae-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="020ae-127">Hola `azure-mgmt-datalake-store` módulo.</span><span class="sxs-lookup"><span data-stu-id="020ae-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="020ae-128">Esto incluye operaciones de administración de cuenta de almacén de Azure Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="020ae-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="020ae-129">Para más información acerca de este módulo, consulte [referencia al módulo de Azure Data Lake Management Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="020ae-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="020ae-130">Hola `azure-datalake-store` módulo.</span><span class="sxs-lookup"><span data-stu-id="020ae-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="020ae-131">Esto incluye las operaciones de sistema de archivos de almacén de Azure Data Lake de Hola.</span><span class="sxs-lookup"><span data-stu-id="020ae-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="020ae-132">Para más información acerca de este módulo, consulte [referencia al módulo de Azure Data Lake Store Filesystem](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="020ae-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="020ae-133">Usar hello después de módulos de hello tooinstall de comandos.</span><span class="sxs-lookup"><span data-stu-id="020ae-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="020ae-134">Creación de una nueva aplicación de Python</span><span class="sxs-lookup"><span data-stu-id="020ae-134">Create a new Python application</span></span>

1. <span data-ttu-id="020ae-135">Hola IDE de su elección, cree una nueva aplicación de Python, por ejemplo, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="020ae-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="020ae-136">Agregar Hola después de módulos de líneas tooimport Hola necesario</span><span class="sxs-lookup"><span data-stu-id="020ae-136">Add hello following lines tooimport hello required modules</span></span>

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

3. <span data-ttu-id="020ae-137">Guardar cambios toomysample.py.</span><span class="sxs-lookup"><span data-stu-id="020ae-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="020ae-138">Autenticación</span><span class="sxs-lookup"><span data-stu-id="020ae-138">Authentication</span></span>

<span data-ttu-id="020ae-139">En esta sección, hablamos tooauthenticate de maneras diferentes de hello con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="020ae-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="020ae-140">Hola opciones disponibles son:</span><span class="sxs-lookup"><span data-stu-id="020ae-140">hello options available are:</span></span>

* <span data-ttu-id="020ae-141">Autenticación de usuario final</span><span class="sxs-lookup"><span data-stu-id="020ae-141">End-user authentication</span></span>
* <span data-ttu-id="020ae-142">Autenticación entre servicios</span><span class="sxs-lookup"><span data-stu-id="020ae-142">Service-to-service authentication</span></span>
* <span data-ttu-id="020ae-143">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="020ae-143">Multi-factor authentication</span></span>

<span data-ttu-id="020ae-144">Estas opciones de autenticación se deben usar tanto para la administración de cuentas como para los módulos de administración del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="020ae-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="020ae-145">Autenticación de usuario final para la administración de cuentas</span><span class="sxs-lookup"><span data-stu-id="020ae-145">End-user authentication for account management</span></span>

<span data-ttu-id="020ae-146">Utilice este tooauthenticate con Azure AD para operaciones de administración de cuenta (crear o eliminar cuenta de almacén de Data Lake, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="020ae-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="020ae-147">Debe proporcionar el nombre de usuario y la contraseña para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="020ae-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="020ae-148">Tenga en cuenta que el usuario hello no debe configurarse para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="020ae-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="020ae-149">Autenticación de usuario final para operaciones del sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="020ae-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="020ae-150">Utilice este tooauthenticate con Azure AD para las operaciones de sistema de archivos (crear carpeta, archivo de carga, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="020ae-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="020ae-151">Se utiliza con una aplicación **cliente nativa** de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="020ae-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="020ae-152">usuario de Hello Azure AD para que proporcionar credenciales no debe estar configurado para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="020ae-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="020ae-153">Autenticación de servicio a servicio con el secreto de cliente para la administración de cuentas</span><span class="sxs-lookup"><span data-stu-id="020ae-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="020ae-154">Utilice este tooauthenticate con Azure AD para operaciones de administración de cuenta (crear o eliminar cuenta de almacén de Data Lake, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="020ae-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="020ae-155">Hola siguiente fragmento de código puede ser tooauthenticate usado la aplicación de forma no interactiva, usando el secreto del cliente de Hola para una identidad de aplicación / servicio.</span><span class="sxs-lookup"><span data-stu-id="020ae-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="020ae-156">Utilícelo con una aplicación de "aplicación web" de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="020ae-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="020ae-157">Autenticación de servicio a servicio con el secreto de cliente para las operaciones del sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="020ae-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="020ae-158">Utilice este tooauthenticate con Azure AD para las operaciones de sistema de archivos (crear carpeta, archivo de carga, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="020ae-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="020ae-159">Hola siguiente fragmento de código puede ser tooauthenticate usado la aplicación de forma no interactiva, usando el secreto del cliente de Hola para una identidad de aplicación / servicio.</span><span class="sxs-lookup"><span data-stu-id="020ae-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="020ae-160">Utilícelo con una aplicación de "aplicación web" de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="020ae-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="020ae-161">Multi-Factor Authentication para la administración de cuentas</span><span class="sxs-lookup"><span data-stu-id="020ae-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="020ae-162">Utilice este tooauthenticate con Azure AD para operaciones de administración de cuenta (crear o eliminar cuenta de almacén de Data Lake, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="020ae-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="020ae-163">Hello siguiente fragmento de código se pueden usar tooauthenticate su aplicación mediante la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="020ae-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="020ae-164">Utilícelo con una aplicación de "aplicación web" de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="020ae-164">Use this with an existing Azure AD "Web App" application.</span></span>

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

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="020ae-165">Multi-Factor Authentication para la administración del sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="020ae-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="020ae-166">Utilice este tooauthenticate con Azure AD para las operaciones de sistema de archivos (crear carpeta, archivo de carga, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="020ae-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="020ae-167">Hello siguiente fragmento de código se pueden usar tooauthenticate su aplicación mediante la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="020ae-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="020ae-168">Utilícelo con una aplicación de "aplicación web" de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="020ae-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="020ae-169">Crear un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="020ae-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="020ae-170">Usar hello siguiente fragmento de código toocreate un grupo de recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="020ae-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

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

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="020ae-171">Creación de clientes y de una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="020ae-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="020ae-172">Hola siguiente fragmento de código primero crea a cliente de cuenta de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="020ae-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="020ae-173">Usa Hola cliente objeto toocreate una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="020ae-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="020ae-174">Por último, el fragmento de código de hello crea un objeto de cliente de sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="020ae-174">Finally, hello snippet creates a filesystem client object.</span></span>

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

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="020ae-175">Lista de cuentas de almacén de Data Lake de Hola</span><span class="sxs-lookup"><span data-stu-id="020ae-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="020ae-176">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="020ae-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="020ae-177">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="020ae-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="020ae-178">Descarga de un archivo</span><span class="sxs-lookup"><span data-stu-id="020ae-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="020ae-179">Eliminación de un directorio</span><span class="sxs-lookup"><span data-stu-id="020ae-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="020ae-180">Consulte también</span><span class="sxs-lookup"><span data-stu-id="020ae-180">See also</span></span>

- [<span data-ttu-id="020ae-181">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="020ae-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="020ae-182">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="020ae-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="020ae-183">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="020ae-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="020ae-184">Referencia de SDK de .NET de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="020ae-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="020ae-185">Referencia de REST de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="020ae-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
