---
title: "Uso de PowerShell como introducción a Azure Data Lake Store | Microsoft Docs"
description: "Uso de Azure PowerShell para crear una cuenta de Almacén de Data Lake y realización de operaciones básicas"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 23c9aaa089251bff5132652475f4daadc2c128fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="690b7-103">Introducción al Almacén de Azure Data Lake mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="690b7-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="690b7-104">Portal</span><span class="sxs-lookup"><span data-stu-id="690b7-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="690b7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="690b7-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="690b7-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="690b7-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="690b7-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="690b7-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="690b7-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="690b7-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="690b7-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="690b7-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="690b7-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="690b7-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="690b7-111">Python</span><span class="sxs-lookup"><span data-stu-id="690b7-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="690b7-112">Aprenda a usar Azure PowerShell para crear una cuenta del Almacén de Azure Data Lake y realizar operaciones básicas como crear carpetas, cargar y descargar archivos de datos, eliminar la cuenta, etc. Para más información acerca de Data Lake Store, consulte [Información general de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="690b7-112">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="690b7-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="690b7-113">Prerequisites</span></span>
<span data-ttu-id="690b7-114">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="690b7-114">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="690b7-115">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="690b7-115">**An Azure subscription**.</span></span> <span data-ttu-id="690b7-116">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="690b7-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="690b7-117">**Azure PowerShell 1.0 o versiones posteriores**.</span><span class="sxs-lookup"><span data-stu-id="690b7-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="690b7-118">Consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="690b7-118">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="690b7-119">Autenticación</span><span class="sxs-lookup"><span data-stu-id="690b7-119">Authentication</span></span>
<span data-ttu-id="690b7-120">En este artículo se utiliza un enfoque de autenticación más sencillo con Data Lake Store en el que se le solicita que escriba las credenciales de la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="690b7-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="690b7-121">El nivel de acceso a la cuenta de Data Lake Store y al sistema de archivos está determinado por el nivel de acceso del usuario que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="690b7-121">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="690b7-122">No obstante, existen otros enfoques para realizar la autenticación con Data Lake Store, que son **autenticación de usuario final** o **autenticación de servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="690b7-122">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="690b7-123">Para obtener instrucciones y más información acerca de cómo realizar la autenticación, consulte [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticación entre servicios con Data Lake Store mediante Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="690b7-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="690b7-124">Creación de una cuenta de Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="690b7-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="690b7-125">En el escritorio, abra una nueva ventana de Windows PowerShell y escriba el siguiente fragmento de código para iniciar sesión en su cuenta de Azure, establecer la suscripción y registrar el proveedor de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="690b7-125">From your desktop, open a new Windows PowerShell window, and enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span></span> <span data-ttu-id="690b7-126">Cuando se le solicite iniciar sesión, asegúrese de iniciarla como uno de los administradores o propietario de la suscripción:</span><span class="sxs-lookup"><span data-stu-id="690b7-126">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="690b7-127">La cuenta de Almacén de Azure Data Lake se asocia con un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="690b7-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="690b7-128">Comience creando un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="690b7-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="690b7-129">![Creación de un grupo de recursos de Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Creación de un grupo de recursos de Azure")</span><span class="sxs-lookup"><span data-stu-id="690b7-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="690b7-130">Cree una cuenta del Almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="690b7-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="690b7-131">El nombre que especifique debe contener solo letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="690b7-131">The name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="690b7-132">![Creación de una cuenta de Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Creación de una cuenta de Azure Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="690b7-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="690b7-133">Compruebe que la cuenta se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="690b7-133">Verify that the account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="690b7-134">El resultado debe ser **True**.</span><span class="sxs-lookup"><span data-stu-id="690b7-134">The output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="690b7-135">Creación de estructuras de directorios en el Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="690b7-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="690b7-136">Puede crear directorios bajo su cuenta de Almacén de Azure Data Lake para administrar y almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="690b7-136">You can create directories under your Azure Data Lake Store account to manage and store data.</span></span>

1. <span data-ttu-id="690b7-137">Especifique un directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="690b7-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="690b7-138">Cree un nuevo directorio denominado **mynewdirectory** en la raíz especificada.</span><span class="sxs-lookup"><span data-stu-id="690b7-138">Create a new directory called **mynewdirectory** under the specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="690b7-139">Compruebe que el nuevo directorio se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="690b7-139">Verify that the new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="690b7-140">Debe mostrar un resultado parecido al siguiente:</span><span class="sxs-lookup"><span data-stu-id="690b7-140">It should show an output like the following:</span></span>

    <span data-ttu-id="690b7-141">![Comprobación del directorio](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Comprobación del directorio")</span><span class="sxs-lookup"><span data-stu-id="690b7-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-to-your-azure-data-lake-store"></a><span data-ttu-id="690b7-142">Carga de datos en el Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="690b7-142">Upload data to your Azure Data Lake Store</span></span>
<span data-ttu-id="690b7-143">Puede cargar los datos en el Almacén de Data Lake directamente en el nivel raíz o en un directorio que creó en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="690b7-143">You can upload your data to Data Lake Store directly at the root level or to a directory that you created within the account.</span></span> <span data-ttu-id="690b7-144">Los fragmentos de código siguientes muestran cómo cargar datos de ejemplo en el directorio (**mynewdirectory**) que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="690b7-144">The snippets below demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span></span>

<span data-ttu-id="690b7-145">Si busca datos de ejemplo para cargar, puede obtener la carpeta **Ambulance Data** en el [repositorio Git de Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="690b7-145">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="690b7-146">Descargue el archivo y almacénelo en un directorio local del equipo, como C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="690b7-146">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="690b7-147">Cambio del nombre, descarga y eliminación de los datos del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="690b7-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="690b7-148">Para cambiar el nombre de un archivo, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="690b7-148">To rename a file, use the following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="690b7-149">Para descargar un archivo, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="690b7-149">To download a file, use the following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="690b7-150">Para eliminar un archivo, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="690b7-150">To delete a file, use the following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="690b7-151">Cuando se le solicite, escriba **Y** para eliminar el elemento.</span><span class="sxs-lookup"><span data-stu-id="690b7-151">When prompted, enter **Y** to delete the item.</span></span> <span data-ttu-id="690b7-152">Si tiene más de un archivo para eliminar, puede proporcionar todas las rutas de acceso separadas por comas.</span><span class="sxs-lookup"><span data-stu-id="690b7-152">If you have more than one file to delete, you can provide all the paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="690b7-153">Eliminación de una cuenta del Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="690b7-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="690b7-154">Use el siguiente comando para eliminar la cuenta del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="690b7-154">Use the following command to delete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="690b7-155">Cuando se le solicite, escriba **Y** para eliminar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="690b7-155">When prompted, enter **Y** to delete the account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="690b7-156">Guía de rendimiento al usar PowerShell</span><span class="sxs-lookup"><span data-stu-id="690b7-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="690b7-157">A continuación se muestran los valores más importantes que se pueden optimizar para obtener el mejor rendimiento al usar PowerShell para trabajar con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="690b7-157">Below are the most important settings that can be tuned to get the best performance while using PowerShell to work with Data Lake Store:</span></span>

| <span data-ttu-id="690b7-158">Propiedad</span><span class="sxs-lookup"><span data-stu-id="690b7-158">Property</span></span>            | <span data-ttu-id="690b7-159">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="690b7-159">Default</span></span> | <span data-ttu-id="690b7-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="690b7-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="690b7-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="690b7-161">PerFileThreadCount</span></span>  | <span data-ttu-id="690b7-162">10</span><span class="sxs-lookup"><span data-stu-id="690b7-162">10</span></span>      | <span data-ttu-id="690b7-163">Este parámetro permite elegir el número de subprocesos paralelos para cargar o descargar cada archivo.</span><span class="sxs-lookup"><span data-stu-id="690b7-163">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="690b7-164">Este número representa el número máximo de subprocesos que se pueden asignar por archivo, pero, según el escenario, es posible que obtenga menos subprocesos (por ejemplo, si está cargando un archivo de 1 KB, obtendrá un subproceso, aunque solicite 20).</span><span class="sxs-lookup"><span data-stu-id="690b7-164">This number represents the max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="690b7-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="690b7-165">ConcurrentFileCount</span></span> | <span data-ttu-id="690b7-166">10</span><span class="sxs-lookup"><span data-stu-id="690b7-166">10</span></span>      | <span data-ttu-id="690b7-167">Este parámetro es específico para cargar o descargar carpetas.</span><span class="sxs-lookup"><span data-stu-id="690b7-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="690b7-168">Este parámetro determina el número de archivos simultáneos que se pueden cargar o descargar.</span><span class="sxs-lookup"><span data-stu-id="690b7-168">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="690b7-169">Este número representa el número máximo de archivos simultáneos que se pueden cargar o descargar al mismo tiempo, pero, según el escenario, es posible que obtenga una menor simultaneidad (por ejemplo, si está cargando dos archivos, obtendrá dos cargas de archivos simultáneos, aunque solicite 15).</span><span class="sxs-lookup"><span data-stu-id="690b7-169">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="690b7-170">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="690b7-170">**Example**</span></span>

<span data-ttu-id="690b7-171">Este comando descarga los archivos de Azure Data Lake Store en la unidad local del usuario con 20 subprocesos por archivo y 100 archivos simultáneos.</span><span class="sxs-lookup"><span data-stu-id="690b7-171">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-the-value-to-set-for-these-parameters"></a><span data-ttu-id="690b7-172">¿Cómo puedo determinar qué valor establecer para estos parámetros?</span><span class="sxs-lookup"><span data-stu-id="690b7-172">How do I determine the value to set for these parameters?</span></span>

<span data-ttu-id="690b7-173">A continuación hay algunas instrucciones que puede usar.</span><span class="sxs-lookup"><span data-stu-id="690b7-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="690b7-174">**Paso 1: Determinación del número total de subprocesos**: debe empezar por calcular el recuento total de subprocesos que se usará.</span><span class="sxs-lookup"><span data-stu-id="690b7-174">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span></span> <span data-ttu-id="690b7-175">Como norma general, debe usar seis subprocesos por cada núcleo físico.</span><span class="sxs-lookup"><span data-stu-id="690b7-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="690b7-176">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="690b7-176">**Example**</span></span>

    <span data-ttu-id="690b7-177">Suponga que está ejecutando los comandos de PowerShell desde una máquina virtual D14 que tiene 16 núcleos.</span><span class="sxs-lookup"><span data-stu-id="690b7-177">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="690b7-178">**Paso 2: Cálculo de PerFileThreadCount**: calculamos nuestro PerFileThreadCount en función del tamaño de los archivos.</span><span class="sxs-lookup"><span data-stu-id="690b7-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span></span> <span data-ttu-id="690b7-179">Para archivos menores de 2,5 GB, no hay ninguna necesidad de cambiar este parámetro, ya que el valor predeterminado (10) es suficiente.</span><span class="sxs-lookup"><span data-stu-id="690b7-179">For files smaller than 2.5GB, there is no need to change this parameter because the default of 10 is sufficient.</span></span> <span data-ttu-id="690b7-180">Para los archivos mayores de 2,5 GB, debe usar diez subprocesos como base para las primeras 2,5 GB y agregar un subproceso por cada aumento de 256 MB en el tamaño del archivo.</span><span class="sxs-lookup"><span data-stu-id="690b7-180">For files larger than 2.5GB, you should use 10 threads as the base for the first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="690b7-181">Si está copiando una carpeta con muchos tamaños de archivo, considere la posibilidad de agruparlos por tamaños de archivo similares.</span><span class="sxs-lookup"><span data-stu-id="690b7-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="690b7-182">Tener tamaños de archivo diferentes puede provocar un rendimiento no óptimo.</span><span class="sxs-lookup"><span data-stu-id="690b7-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="690b7-183">Si no es posible agrupar los archivos con un tamaño similar, debe establecer PerFileThreadCount en función del tamaño de archivo más grande.</span><span class="sxs-lookup"><span data-stu-id="690b7-183">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span></span>

        PerFileThreadCount = 10 threads for the first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="690b7-184">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="690b7-184">**Example**</span></span>

    <span data-ttu-id="690b7-185">Suponiendo que tenga 100 archivos que oscilan entre 1 GB y 10 GB, usaremos los 10 GB como el tamaño de archivo más grande para la ecuación, que debería ser similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="690b7-185">Assuming you have 100 files ranging from 1GB to 10GB, we use the 10GB as the largest file size for equation, which would read like the following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="690b7-186">**Paso 3: Cálculo de ConcurrentFilecount**: use el número total de subprocesos y PerFileThreadCount para calcular ConcurrentFileCount basado en la siguiente ecuación.</span><span class="sxs-lookup"><span data-stu-id="690b7-186">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="690b7-187">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="690b7-187">**Example**</span></span>

    <span data-ttu-id="690b7-188">En función de los valores del ejemplo que hemos usado</span><span class="sxs-lookup"><span data-stu-id="690b7-188">Based on the example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="690b7-189">Por tanto, **ConcurrentFileCount** es **2,4**, que se puede redondear a **2**.</span><span class="sxs-lookup"><span data-stu-id="690b7-189">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="690b7-190">Ajuste adicional</span><span class="sxs-lookup"><span data-stu-id="690b7-190">Further tuning</span></span>

<span data-ttu-id="690b7-191">Es posible que necesite un ajuste adicional porque se va a trabajar con diversos tamaños de archivo.</span><span class="sxs-lookup"><span data-stu-id="690b7-191">You might require further tuning because there is a range of file sizes to work with.</span></span> <span data-ttu-id="690b7-192">El cálculo anterior funciona bien si todos o la mayoría de los archivos son más grandes y más cercanos a las 10 GB.</span><span class="sxs-lookup"><span data-stu-id="690b7-192">The above calculation works well if all or most of the files are larger and closer to the 10GB range.</span></span> <span data-ttu-id="690b7-193">Por el contrario, si hay muchos tamaños de archivo diferentes, con muchos archivos pequeños, podría reducir PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="690b7-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="690b7-194">Al reducir PerFileThreadCount, podemos aumentar ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="690b7-194">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="690b7-195">Por lo tanto, si suponemos que la mayoría de nuestros archivos son pequeños, aproximadamente 5 GB, podemos repetir nuestro cálculo:</span><span class="sxs-lookup"><span data-stu-id="690b7-195">So, if we assume that most of our files are smaller in the 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="690b7-196">Por lo tanto, **ConcurrentFileCount** ahora será 96/20, cuyo resultado es 4,8, redondeado a **4**.</span><span class="sxs-lookup"><span data-stu-id="690b7-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off to **4**.</span></span>

<span data-ttu-id="690b7-197">Puede continuar ajustando esta configuración aumentando o reduciendo **PerFileThreadCount** en función de la distribución de los tamaños de archivo.</span><span class="sxs-lookup"><span data-stu-id="690b7-197">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="690b7-198">Limitación</span><span class="sxs-lookup"><span data-stu-id="690b7-198">Limitation</span></span>

* <span data-ttu-id="690b7-199">**El número de archivos es menor que ConcurrentFileCount**: si el número de archivos que va a cargar es menor que el valor de **ConcurrentFileCount** que ha calculado, debería reducir **ConcurrentFileCount** para que sea igual al número de archivos.</span><span class="sxs-lookup"><span data-stu-id="690b7-199">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span></span> <span data-ttu-id="690b7-200">También puede utilizar los subprocesos restantes para aumentar **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="690b7-200">You can use any remaining threads to increase **PerFileThreadCount**.</span></span>

* <span data-ttu-id="690b7-201">**Demasiados subprocesos**: si aumenta demasiado el número de subprocesos sin aumentar el tamaño del clúster, corre el riesgo de degradar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="690b7-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span></span> <span data-ttu-id="690b7-202">Puede haber problemas de contención al cambiar de contexto en la CPU.</span><span class="sxs-lookup"><span data-stu-id="690b7-202">There can be contention issues when context-switching on the CPU.</span></span>

* <span data-ttu-id="690b7-203">**Simultaneidad insuficiente**: si la simultaneidad no es suficiente, el clúster puede ser demasiado pequeño.</span><span class="sxs-lookup"><span data-stu-id="690b7-203">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="690b7-204">Puede aumentar el número de nodos en el clúster, lo que proporcionará más simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="690b7-204">You can increase the number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="690b7-205">**Errores de limitación**: es posible que vea errores de limitación si la simultaneidad es demasiado alta.</span><span class="sxs-lookup"><span data-stu-id="690b7-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="690b7-206">Si ve errores de limitación, reduzca la simultaneidad o póngase en contacto con nosotros.</span><span class="sxs-lookup"><span data-stu-id="690b7-206">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="690b7-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="690b7-207">Next steps</span></span>
* [<span data-ttu-id="690b7-208">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="690b7-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="690b7-209">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="690b7-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="690b7-210">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="690b7-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

