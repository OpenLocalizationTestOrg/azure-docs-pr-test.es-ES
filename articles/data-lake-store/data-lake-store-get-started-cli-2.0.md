---
title: "Uso de la interfaz de la línea de comandos 2.0 de Azure para empezar a trabajar con Azure Data Lake Store | Microsoft Docs"
description: "Uso de la línea de comandos 2.0 multiplataforma de Azure para crear una cuenta de Data Lake Store y realizar operaciones básicas"
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
ms.openlocfilehash: ed78d25f2bac0a9996f1796ee503f31a36940977
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="a8645-103">Introducción a Azure Data Lake Store mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a8645-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8645-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a8645-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="a8645-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8645-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="a8645-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="a8645-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="a8645-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="a8645-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="a8645-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="a8645-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="a8645-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a8645-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="a8645-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="a8645-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="a8645-111">Python</span><span class="sxs-lookup"><span data-stu-id="a8645-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="a8645-112">Aprenda a usar la CLI 2.0 de Azure para crear una cuenta de Azure Data Lake Store y realizar operaciones básicas como crear carpetas, cargar y descargar archivos de datos, eliminar la cuenta, etc. Para más información acerca de Data Lake Store, consulte [Información general de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8645-112">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="a8645-113">La CLI 2.0 de Azure es la nueva experiencia de línea de comandos de Azure para administrar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8645-113">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="a8645-114">Se puede usar en macOS, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="a8645-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="a8645-115">Para más información, consulte la [introducción a la CLI 2.0 de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a8645-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="a8645-116">También puede examinar la [referencia de la CLI 2.0 de Azure Data Lake Store](https://docs.microsoft.com/cli/azure/dls) para obtener una lista completa de comandos y sintaxis.</span><span class="sxs-lookup"><span data-stu-id="a8645-116">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a8645-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a8645-117">Prerequisites</span></span>
<span data-ttu-id="a8645-118">Antes de empezar este artículo, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a8645-118">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="a8645-119">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="a8645-119">**An Azure subscription**.</span></span> <span data-ttu-id="a8645-120">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8645-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="a8645-121">**CLI 2.0 de Azure**: consulte [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalación de la CLI 2.0 de Azure) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="a8645-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="a8645-122">Autenticación</span><span class="sxs-lookup"><span data-stu-id="a8645-122">Authentication</span></span>

<span data-ttu-id="a8645-123">En este artículo se utiliza un enfoque de autenticación más sencillo con Data Lake Store, donde inicia sesión como usuario final.</span><span class="sxs-lookup"><span data-stu-id="a8645-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="a8645-124">El nivel de acceso a la cuenta de Data Lake Store y al sistema de archivos está determinado por el nivel de acceso del usuario que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="a8645-124">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="a8645-125">No obstante, existen otros enfoques para realizar la autenticación con Data Lake Store, que son **autenticación de usuario final** o **autenticación de servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="a8645-125">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="a8645-126">Para obtener instrucciones y más información acerca de cómo realizar la autenticación, consulte [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticación entre servicios con Data Lake Store mediante Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a8645-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="a8645-127">Inicio de sesión en la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="a8645-127">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="a8645-128">Inicie sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8645-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="a8645-129">Obtendrá un código que usará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="a8645-129">You get a code to use in the next step.</span></span> <span data-ttu-id="a8645-130">Use un explorador web para abrir la página https://aka.ms/devicelogin y escriba el código para autenticarse.</span><span class="sxs-lookup"><span data-stu-id="a8645-130">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="a8645-131">Se le pedirá que inicie sesión con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="a8645-131">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="a8645-132">Una vez que inicie sesión, la ventana muestra todas las suscripciones de Azure que están asociadas a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="a8645-132">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="a8645-133">Use el comando siguiente para utilizar una suscripción específica.</span><span class="sxs-lookup"><span data-stu-id="a8645-133">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="a8645-134">Creación de una cuenta de Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="a8645-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="a8645-135">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a8645-135">Create a new resource group.</span></span> <span data-ttu-id="a8645-136">En el siguiente comando, proporcione los valores de los parámetros que desee usar.</span><span class="sxs-lookup"><span data-stu-id="a8645-136">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="a8645-137">Si el nombre de la ubicación contiene espacios, escríbalo entre comillas.</span><span class="sxs-lookup"><span data-stu-id="a8645-137">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="a8645-138">Por ejemplo "East US 2".</span><span class="sxs-lookup"><span data-stu-id="a8645-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="a8645-139">Cree una cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a8645-139">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="a8645-140">Crear carpetas en una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="a8645-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="a8645-141">Puede crear carpetas en su cuenta de Almacén de Azure Data Lake para administrar y almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="a8645-141">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="a8645-142">Use el siguiente comando para crear una carpeta denominada **minuevacarpeta** en la raíz de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a8645-142">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="a8645-143">El parámetro `--folder` garantiza que el comando crea una carpeta.</span><span class="sxs-lookup"><span data-stu-id="a8645-143">The `--folder` parameter ensures that the command creates a folder.</span></span> <span data-ttu-id="a8645-144">Si este parámetro no está presente, el comando crea un archivo vacío llamado minuevacarpeta en la raíz de la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a8645-144">If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="a8645-145">Carga de datos en una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a8645-145">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="a8645-146">Puede cargar datos en Data Lake Store directamente en el nivel raíz o en la carpeta que haya creado en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="a8645-146">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="a8645-147">Los fragmentos de código siguientes muestran cómo cargar algunos datos de ejemplo en la carpeta (**miNuevaCarpeta**) que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="a8645-147">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="a8645-148">Si busca datos de ejemplo para cargar, puede obtener la carpeta **Ambulance Data** en el [repositorio Git de Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="a8645-148">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="a8645-149">Descargue el archivo y almacénelo en un directorio local del equipo, como C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="a8645-149">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="a8645-150">Como destino, debe especificar la ruta de acceso completa, incluido el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="a8645-150">For the destination, you must specify the complete path including the file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="a8645-151">Enumeración de archivos en una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a8645-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="a8645-152">Use el siguiente comando para enumera los archivos de una cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a8645-152">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="a8645-153">La salida de este comando debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="a8645-153">The output of this should be similar to the following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="a8645-154">Cambio del nombre, descarga y eliminación de datos en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a8645-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="a8645-155">**Para cambiar el nombre de un archivo**, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="a8645-155">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="a8645-156">**Para descargar un archivo**, use el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="a8645-156">**To download a file**, use the following command.</span></span> <span data-ttu-id="a8645-157">Asegúrese de que la ruta de destino especificada ya existe.</span><span class="sxs-lookup"><span data-stu-id="a8645-157">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="a8645-158">El comando crea la carpeta de destino si no existe.</span><span class="sxs-lookup"><span data-stu-id="a8645-158">The command creates the destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="a8645-159">**Para eliminar un archivo**, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="a8645-159">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="a8645-160">Si quiere eliminar la carpeta **minuevacarpeta** y el archivo **vehicle1_09142014_copy.csv** juntos en un solo comando, use el parámetro -- recurse.</span><span class="sxs-lookup"><span data-stu-id="a8645-160">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="a8645-161">Uso de permisos y listas ACL para una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a8645-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="a8645-162">En esta sección aprenderá a administrar listas ACL y permisos mediante la CLI 2.0 de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8645-162">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="a8645-163">Para obtener una explicación detallada sobre cómo se implementan las listas ACL de Azure Data Lake Store, consulte [Control de acceso en Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a8645-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="a8645-164">**Para actualizar el propietario de un archivo o carpeta**, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a8645-164">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="a8645-165">**Para actualizar los permisos de un archivo o carpeta**, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a8645-165">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="a8645-166">**Para obtener las listas ACL para una ruta de acceso dada**, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a8645-166">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="a8645-167">La salida debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="a8645-167">The output should be similar to the following:</span></span>

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

* <span data-ttu-id="a8645-168">**Para establecer una entrada para una lista ACL**, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a8645-168">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="a8645-169">**Para quitar una entrada de una lista ACL**, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a8645-169">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="a8645-170">**Para quitar una lista ACL entera predeterminada**, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a8645-170">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="a8645-171">**Para quitar una lista ACL entera no predeterminada**, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a8645-171">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="a8645-172">Eliminar una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="a8645-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="a8645-173">Use el comando siguiente para eliminar la cuenta del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a8645-173">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="a8645-174">Cuando se le solicite, escriba **Y** para eliminar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="a8645-174">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8645-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8645-175">Next steps</span></span>

* [<span data-ttu-id="a8645-176">Referencia de la CLI 2.0 de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a8645-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="a8645-177">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="a8645-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="a8645-178">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="a8645-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="a8645-179">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="a8645-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
