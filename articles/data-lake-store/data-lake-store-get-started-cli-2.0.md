---
title: "aaaUse 2.0 de línea de comandos de Azure interfaz tooget a trabajar con el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Usar línea de comandos multiplataforma Azure 2.0 toocreate una cuenta de almacén de Data Lake y realizar operaciones básicas"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="ba20b-103">Introducción a Azure Data Lake Store mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ba20b-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba20b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ba20b-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="ba20b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba20b-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="ba20b-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="ba20b-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="ba20b-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="ba20b-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="ba20b-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="ba20b-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="ba20b-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ba20b-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="ba20b-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="ba20b-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="ba20b-111">Python</span><span class="sxs-lookup"><span data-stu-id="ba20b-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="ba20b-112">Obtenga información acerca de cómo toouse CLI de Azure 2.0 toocreate un Azure Data Lake almacenar cuenta y realizar operaciones básicas, como por ejemplo crear carpetas, cargar y descargar archivos de datos, eliminar su cuenta, etcetera. Para más información acerca de Data Lake Store, consulte [Información general de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba20b-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="ba20b-113">Hola 2.0 de CLI de Azure es la nueva experiencia de línea de comandos de Azure para administrar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba20b-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="ba20b-114">Se puede usar en macOS, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="ba20b-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="ba20b-115">Para más información, consulte la [introducción a la CLI 2.0 de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba20b-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="ba20b-116">También puede mirar hello [referencia de Azure Data Lake almacén CLI 2.0](https://docs.microsoft.com/cli/azure/dls) para obtener una lista completa de comandos y la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="ba20b-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ba20b-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ba20b-117">Prerequisites</span></span>
<span data-ttu-id="ba20b-118">Antes de comenzar este artículo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="ba20b-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="ba20b-119">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="ba20b-119">**An Azure subscription**.</span></span> <span data-ttu-id="ba20b-120">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba20b-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="ba20b-121">**CLI 2.0 de Azure**: consulte [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalación de la CLI 2.0 de Azure) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="ba20b-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="ba20b-122">Autenticación</span><span class="sxs-lookup"><span data-stu-id="ba20b-122">Authentication</span></span>

<span data-ttu-id="ba20b-123">En este artículo se utiliza un enfoque de autenticación más sencillo con Data Lake Store, donde inicia sesión como usuario final.</span><span class="sxs-lookup"><span data-stu-id="ba20b-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="ba20b-124">Hola acceso nivel tooData Lake almacén cuenta de sistema de archivos y, a continuación, se rige por el nivel de acceso de Hola de hello usuario registrado.</span><span class="sxs-lookup"><span data-stu-id="ba20b-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="ba20b-125">Sin embargo, hay otros métodos como tooauthenticate bien con el almacén de Data Lake, que son **autenticación de usuario final** o **autenticación del servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="ba20b-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="ba20b-126">Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ba20b-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="ba20b-127">Inicie sesión en tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="ba20b-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="ba20b-128">Inicie sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba20b-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="ba20b-129">Obtener un toouse de código en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="ba20b-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="ba20b-130">Use un https://aka.ms/devicelogin web explorador tooopen Hola página e introduzca hello código tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="ba20b-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="ba20b-131">Son toolog solicitada en con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="ba20b-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="ba20b-132">Una vez que inicie sesión en todas las listas de ventanas de Hola Hola suscripciones de Azure que están asociadas a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="ba20b-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="ba20b-133">Usar hello después comando toouse una suscripción específica.</span><span class="sxs-lookup"><span data-stu-id="ba20b-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="ba20b-134">Creación de una cuenta de Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ba20b-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="ba20b-135">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ba20b-135">Create a new resource group.</span></span> <span data-ttu-id="ba20b-136">En el siguiente comando de hello, proporcionar Hola valores de parámetro que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="ba20b-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="ba20b-137">Si el nombre de la ubicación de hello contiene espacios en blanco, poner entre comillas.</span><span class="sxs-lookup"><span data-stu-id="ba20b-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="ba20b-138">Por ejemplo "East US 2".</span><span class="sxs-lookup"><span data-stu-id="ba20b-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="ba20b-139">Crear cuenta de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="ba20b-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="ba20b-140">Crear carpetas en una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="ba20b-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="ba20b-141">Puede crear carpetas en su toomanage de cuenta de almacén de Azure Data Lake y almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="ba20b-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="ba20b-142">Hola de uso después de toocreate comando llama a una carpeta **MiNuevaCarpeta** en raíz Hola Hola almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ba20b-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="ba20b-143">Hola `--folder` parámetro garantiza que el comando de hello crea una carpeta.</span><span class="sxs-lookup"><span data-stu-id="ba20b-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="ba20b-144">Si este parámetro no está presente, el comando de hello crea un archivo vacío denominado MiNuevaCarpeta en raíz Hola Hola cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ba20b-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="ba20b-145">Cargar la cuenta de almacén de Data Lake tooa de datos</span><span class="sxs-lookup"><span data-stu-id="ba20b-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="ba20b-146">Puede cargar el almacén de datos tooData Lake directamente en hello tooa o nivel de carpeta raíz que ha creado en la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="ba20b-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="ba20b-147">Hola fragmentos siguientes muestran cómo tooupload alguna carpeta de toohello de datos de ejemplo (**MiNuevaCarpeta**) que creó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba20b-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="ba20b-148">Si desea obtener algunos tooupload de datos de ejemplo, puede obtener hello **ambulancia datos** carpeta de hello [repositorio de Git de Azure datos Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="ba20b-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="ba20b-149">Descargar archivo hello y almacenarlo en un directorio local en el equipo, como C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="ba20b-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="ba20b-150">Para el destino de hello, debe especificar ruta completa de hello incluido el nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba20b-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="ba20b-151">Enumeración de archivos en una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ba20b-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="ba20b-152">Usar hello siguientes comando toolist Hola archivos en una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ba20b-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="ba20b-153">salida de Hello de este debe ser similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="ba20b-153">hello output of this should be similar toohello following:</span></span>

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="ba20b-154">Cambio del nombre, descarga y eliminación de datos en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ba20b-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="ba20b-155">**toorename un archivo**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba20b-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="ba20b-156">**toodownload un archivo**, utilizar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba20b-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="ba20b-157">Asegúrese de que la ruta de acceso de destino de hello especificada ya existe.</span><span class="sxs-lookup"><span data-stu-id="ba20b-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="ba20b-158">comando de Hello crea la carpeta de destino de hello si no existe.</span><span class="sxs-lookup"><span data-stu-id="ba20b-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="ba20b-159">**toodelete un archivo**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba20b-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="ba20b-160">Si desea que la carpeta de hello toodelete **MiNuevaCarpeta** y archivo hello **vehicle1_09142014_copy.csv** juntos en un solo comando, use Hola--recurse parámetro</span><span class="sxs-lookup"><span data-stu-id="ba20b-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="ba20b-161">Uso de permisos y listas ACL para una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ba20b-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="ba20b-162">En esta sección aprenderá cómo toomanage ACL y permisos mediante la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="ba20b-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="ba20b-163">Para obtener una explicación detallada sobre cómo se implementan las listas ACL de Azure Data Lake Store, consulte [Control de acceso en Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="ba20b-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="ba20b-164">**propietario de hello tooupdate de una archivo o carpeta**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba20b-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="ba20b-165">**permisos de hello tooupdate para un archivo o carpeta**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba20b-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="ba20b-166">**Hola tooget ACL para una ruta de acceso dada**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba20b-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="ba20b-167">salida de Hello debe ser similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="ba20b-167">hello output should be similar toohello following:</span></span>

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* <span data-ttu-id="ba20b-168">**tooset una entrada para una ACL**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba20b-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="ba20b-169">**tooremove una entrada para una ACL**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba20b-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="ba20b-170">**tooremove una ACL predeterminada todo**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba20b-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="ba20b-171">**tooremove una ACL no predeterminado toda**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba20b-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="ba20b-172">Eliminar una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="ba20b-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="ba20b-173">Usar hello después comando toodelete una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ba20b-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="ba20b-174">Cuando se le solicite, escriba **Y** cuenta de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="ba20b-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba20b-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba20b-175">Next steps</span></span>

* [<span data-ttu-id="ba20b-176">Referencia de la CLI 2.0 de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ba20b-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="ba20b-177">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="ba20b-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="ba20b-178">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="ba20b-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ba20b-179">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="ba20b-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
