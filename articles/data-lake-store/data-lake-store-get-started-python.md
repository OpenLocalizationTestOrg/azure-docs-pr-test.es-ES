---
title: "Uso del SDK de Python como introducción a Azure Data Lake Store | Microsoft Docs"
description: Aprenda a usar el SDK de Python para trabajar con cuentas de Data Lake Store y el sistema de archivos.
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
ms.openlocfilehash: 375a603360ac249fc1b08923a94c85652390a3fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="3c3ad-103">Introducción al uso de Python por parte de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3c3ad-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c3ad-104">Portal</span><span class="sxs-lookup"><span data-stu-id="3c3ad-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="3c3ad-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c3ad-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="3c3ad-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="3c3ad-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="3c3ad-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="3c3ad-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="3c3ad-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="3c3ad-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="3c3ad-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="3c3ad-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="3c3ad-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="3c3ad-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="3c3ad-111">Python</span><span class="sxs-lookup"><span data-stu-id="3c3ad-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="3c3ad-112">Aprenda a utilizar el SDK de Python para Azure y Azure Data Lake Store para realizar operaciones básicas como crear carpetas, cargar y descargar archivos de datos, etc. Para más información sobre Data Lake, consulte [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-112">Learn how to use the Python SDK for Azure and Azure Data Lake Store to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c3ad-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3c3ad-113">Prerequisites</span></span>

* <span data-ttu-id="3c3ad-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-114">**Python**.</span></span> <span data-ttu-id="3c3ad-115">Python se puede descargar desde [aquí](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="3c3ad-116">En este artículo se usa Python 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="3c3ad-117">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-117">**An Azure subscription**.</span></span> <span data-ttu-id="3c3ad-118">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="3c3ad-119">**Cree una aplicación de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="3c3ad-120">Utilice la aplicación Azure AD para autenticar la aplicación Data Lake Store con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="3c3ad-121">Existen diferentes enfoques para realizar la autenticación con Azure AD, que son la **autenticación de usuario final** o la **autenticación de servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="3c3ad-122">Para obtener instrucciones y más información acerca de cómo realizar la autenticación, consulte [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticación entre servicios con Data Lake Store mediante Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="3c3ad-123">Instalación de los módulos</span><span class="sxs-lookup"><span data-stu-id="3c3ad-123">Install the modules</span></span>

<span data-ttu-id="3c3ad-124">Para trabajar con Data Lake Store mediante Python, debe instalar tres módulos.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-124">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="3c3ad-125">El módulo `azure-mgmt-resource`.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-125">The `azure-mgmt-resource` module.</span></span> <span data-ttu-id="3c3ad-126">Aquí se incluyen módulos de Azure para Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="3c3ad-127">El módulo `azure-mgmt-datalake-store`.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-127">The `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="3c3ad-128">Aquí se incluyen las operaciones de administración de cuentas de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-128">This includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="3c3ad-129">Para más información acerca de este módulo, consulte [referencia al módulo de Azure Data Lake Management Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="3c3ad-130">El módulo `azure-datalake-store`.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-130">The `azure-datalake-store` module.</span></span> <span data-ttu-id="3c3ad-131">Aquí se incluyen las operaciones del sistema de archivos de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-131">This includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="3c3ad-132">Para más información acerca de este módulo, consulte [referencia al módulo de Azure Data Lake Store Filesystem](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="3c3ad-133">Utilice el comando siguiente para instalar los módulos.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-133">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="3c3ad-134">Creación de una nueva aplicación de Python</span><span class="sxs-lookup"><span data-stu-id="3c3ad-134">Create a new Python application</span></span>

1. <span data-ttu-id="3c3ad-135">En el IDE que prefiera, cree una nueva aplicación de Python, por ejemplo, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-135">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="3c3ad-136">Agregue las líneas siguientes para importar los módulos necesarios.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-136">Add the following lines to import the required modules</span></span>

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

3. <span data-ttu-id="3c3ad-137">Guarde los cambios en mysample.py.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-137">Save changes to mysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="3c3ad-138">Autenticación</span><span class="sxs-lookup"><span data-stu-id="3c3ad-138">Authentication</span></span>

<span data-ttu-id="3c3ad-139">En esta sección, se explican las distintas maneras de autenticarse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-139">In this section, we talk about the different ways to authenticate with Azure AD.</span></span> <span data-ttu-id="3c3ad-140">Las opciones disponibles son:</span><span class="sxs-lookup"><span data-stu-id="3c3ad-140">The options available are:</span></span>

* <span data-ttu-id="3c3ad-141">Autenticación de usuario final</span><span class="sxs-lookup"><span data-stu-id="3c3ad-141">End-user authentication</span></span>
* <span data-ttu-id="3c3ad-142">Autenticación entre servicios</span><span class="sxs-lookup"><span data-stu-id="3c3ad-142">Service-to-service authentication</span></span>
* <span data-ttu-id="3c3ad-143">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3c3ad-143">Multi-factor authentication</span></span>

<span data-ttu-id="3c3ad-144">Estas opciones de autenticación se deben usar tanto para la administración de cuentas como para los módulos de administración del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="3c3ad-145">Autenticación de usuario final para la administración de cuentas</span><span class="sxs-lookup"><span data-stu-id="3c3ad-145">End-user authentication for account management</span></span>

<span data-ttu-id="3c3ad-146">Se utiliza para autenticarse en Azure AD para operaciones de administración de cuentas (crear o eliminar una cuenta de Data Lake Store, etc.).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-146">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="3c3ad-147">Debe proporcionar el nombre de usuario y la contraseña para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="3c3ad-148">Tenga en cuenta que el usuario no debe estar configurado en Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-148">Note that the user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="3c3ad-149">Autenticación de usuario final para operaciones del sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="3c3ad-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="3c3ad-150">Se utiliza para autenticarse en Azure AD para las operaciones de sistema de archivos (crear carpeta, cargar archivo, etc.).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-150">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="3c3ad-151">Se utiliza con una aplicación **cliente nativa** de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="3c3ad-152">El usuario de Azure AD al que se proporcionan las credenciales no debe estar configurado en Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-152">The Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="3c3ad-153">Autenticación de servicio a servicio con el secreto de cliente para la administración de cuentas</span><span class="sxs-lookup"><span data-stu-id="3c3ad-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="3c3ad-154">Se utiliza para autenticarse en Azure AD para operaciones de administración de cuentas (crear o eliminar una cuenta de Data Lake Store, etc.).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-154">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="3c3ad-155">El siguiente fragmento de código se puede utilizar para autenticar la aplicación de forma no interactiva, para lo que se usa el secreto del cliente para una entidad de servicio o aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-155">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="3c3ad-156">Utilícelo con una aplicación de "aplicación web" de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="3c3ad-157">Autenticación de servicio a servicio con el secreto de cliente para las operaciones del sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="3c3ad-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="3c3ad-158">Se utiliza para autenticarse en Azure AD para las operaciones de sistema de archivos (crear carpeta, cargar archivo, etc.).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-158">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="3c3ad-159">El siguiente fragmento de código se puede utilizar para autenticar la aplicación de forma no interactiva, para lo que se usa el secreto del cliente para una entidad de servicio o aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-159">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="3c3ad-160">Utilícelo con una aplicación de "aplicación web" de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="3c3ad-161">Multi-Factor Authentication para la administración de cuentas</span><span class="sxs-lookup"><span data-stu-id="3c3ad-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="3c3ad-162">Se utiliza para autenticarse en Azure AD para operaciones de administración de cuentas (crear o eliminar una cuenta de Data Lake Store, etc.).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-162">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="3c3ad-163">El siguiente fragmento de código se puede utilizar para autenticar una aplicación mediante Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-163">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="3c3ad-164">Utilícelo con una aplicación de "aplicación web" de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-164">Use this with an existing Azure AD "Web App" application.</span></span>

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

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="3c3ad-165">Multi-Factor Authentication para la administración del sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="3c3ad-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="3c3ad-166">Se utiliza para autenticarse en Azure AD para las operaciones de sistema de archivos (crear carpeta, cargar archivo, etc.).</span><span class="sxs-lookup"><span data-stu-id="3c3ad-166">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="3c3ad-167">El siguiente fragmento de código se puede utilizar para autenticar una aplicación mediante Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-167">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="3c3ad-168">Utilícelo con una aplicación de "aplicación web" de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="3c3ad-169">Crear un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="3c3ad-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="3c3ad-170">Utilice el siguiente fragmento de código para crear un grupo de recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="3c3ad-170">Use the following code snippet to create an Azure Resource Group:</span></span>

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

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="3c3ad-171">Creación de clientes y de una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3c3ad-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="3c3ad-172">El siguiente fragmento de código crea primero el cliente de la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-172">The following snippet first creates the Data Lake Store account client.</span></span> <span data-ttu-id="3c3ad-173">Usa el objeto de cliente para crear una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-173">It uses the client object to create a Data Lake Store account.</span></span> <span data-ttu-id="3c3ad-174">Por último, el fragmento de código crea un objeto de cliente del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="3c3ad-174">Finally, the snippet creates a filesystem client object.</span></span>

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

## <a name="list-the-data-lake-store-accounts"></a><span data-ttu-id="3c3ad-175">Enumeración de las cuentas de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3c3ad-175">List the Data Lake Store accounts</span></span>

    ## List the existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="3c3ad-176">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="3c3ad-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="3c3ad-177">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="3c3ad-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="3c3ad-178">Descarga de un archivo</span><span class="sxs-lookup"><span data-stu-id="3c3ad-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="3c3ad-179">Eliminación de un directorio</span><span class="sxs-lookup"><span data-stu-id="3c3ad-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="3c3ad-180">Consulte también</span><span class="sxs-lookup"><span data-stu-id="3c3ad-180">See also</span></span>

- [<span data-ttu-id="3c3ad-181">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="3c3ad-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="3c3ad-182">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="3c3ad-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="3c3ad-183">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="3c3ad-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="3c3ad-184">Referencia de SDK de .NET de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3c3ad-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="3c3ad-185">Referencia de REST de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3c3ad-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
