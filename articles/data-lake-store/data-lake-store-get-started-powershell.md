---
title: "aaaUse PowerShell tooget a trabajar con el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Usar PowerShell de Azure toocreate una cuenta de almacén de Data Lake y realizar operaciones básicas"
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
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="2c07f-103">Introducción al Almacén de Azure Data Lake mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c07f-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c07f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="2c07f-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="2c07f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c07f-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="2c07f-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="2c07f-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="2c07f-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="2c07f-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="2c07f-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="2c07f-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="2c07f-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="2c07f-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="2c07f-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="2c07f-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="2c07f-111">Python</span><span class="sxs-lookup"><span data-stu-id="2c07f-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="2c07f-112">Obtenga información acerca de cómo toouse Azure PowerShell toocreate un Azure Data Lake almacenar cuenta y realizar operaciones básicas, como por ejemplo crear carpetas, cargar y descargar archivos de datos, eliminar su cuenta, etcetera. Para más información acerca de Data Lake Store, consulte [Información general de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c07f-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c07f-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2c07f-113">Prerequisites</span></span>
<span data-ttu-id="2c07f-114">Antes de comenzar este tutorial, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="2c07f-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="2c07f-115">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="2c07f-115">**An Azure subscription**.</span></span> <span data-ttu-id="2c07f-116">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c07f-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2c07f-117">**Azure PowerShell 1.0 o versiones posteriores**.</span><span class="sxs-lookup"><span data-stu-id="2c07f-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="2c07f-118">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2c07f-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="2c07f-119">Autenticación</span><span class="sxs-lookup"><span data-stu-id="2c07f-119">Authentication</span></span>
<span data-ttu-id="2c07f-120">En este artículo usa un método de autenticación más sencillo con el almacén de Data Lake que te encuentres tooenter solicitada sus credenciales de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="2c07f-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="2c07f-121">Hola acceso nivel tooData Lake almacén cuenta de sistema de archivos y, a continuación, se rige por el nivel de acceso de Hola de hello usuario registrado.</span><span class="sxs-lookup"><span data-stu-id="2c07f-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="2c07f-122">Sin embargo, hay otros métodos como tooauthenticate bien con el almacén de Data Lake, que son **autenticación de usuario final** o **autenticación del servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="2c07f-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="2c07f-123">Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="2c07f-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="2c07f-124">Creación de una cuenta de Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="2c07f-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="2c07f-125">Desde el escritorio, abra una nueva ventana de Windows PowerShell, escriba Hola después toolog de fragmento de código en tooyour cuenta de Azure, establecer Hola suscripción y registrar proveedor de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="2c07f-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="2c07f-126">Cuando toolog solicitada, asegúrese de que inicie sesión como una suscripción de hello admininistrators/propietario:</span><span class="sxs-lookup"><span data-stu-id="2c07f-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="2c07f-127">La cuenta de Almacén de Azure Data Lake se asocia con un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2c07f-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="2c07f-128">Comience creando un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2c07f-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="2c07f-129">![Creación de un grupo de recursos de Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Creación de un grupo de recursos de Azure")</span><span class="sxs-lookup"><span data-stu-id="2c07f-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="2c07f-130">Cree una cuenta de Almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2c07f-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="2c07f-131">nombre de Hola que especifique debe contener solo letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="2c07f-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="2c07f-132">![Creación de una cuenta de Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Creación de una cuenta de Azure Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="2c07f-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="2c07f-133">Compruebe que la cuenta de hello se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="2c07f-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="2c07f-134">Hola de salida para esto debería ser **True**.</span><span class="sxs-lookup"><span data-stu-id="2c07f-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="2c07f-135">Creación de estructuras de directorios en el Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="2c07f-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="2c07f-136">Puede crear directorios en su toomanage de cuenta de almacén de Azure Data Lake y almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="2c07f-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="2c07f-137">Especifique un directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="2c07f-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="2c07f-138">Crear un nuevo directorio denominado **mynewdirectory** en la raíz especificada Hola.</span><span class="sxs-lookup"><span data-stu-id="2c07f-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="2c07f-139">Compruebe que ese nuevo directorio Hola se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="2c07f-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="2c07f-140">Debería mostrarse una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="2c07f-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="2c07f-141">![Comprobación del directorio](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Comprobación del directorio")</span><span class="sxs-lookup"><span data-stu-id="2c07f-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="2c07f-142">Cargar el almacén de datos tooyour Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="2c07f-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="2c07f-143">Puede cargar el almacén de datos tooData Lake directamente en hello tooa o directorio raíz que ha creado en la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="2c07f-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="2c07f-144">Hola fragmentos siguientes muestran cómo tooupload algún directorio toohello de datos de ejemplo (**mynewdirectory**) que creó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c07f-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="2c07f-145">Si desea obtener algunos tooupload de datos de ejemplo, puede obtener hello **ambulancia datos** carpeta de hello [repositorio de Git de Azure datos Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="2c07f-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="2c07f-146">Descargar archivo hello y almacenarlo en un directorio local en el equipo, como C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="2c07f-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="2c07f-147">Cambio del nombre, descarga y eliminación de los datos del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2c07f-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="2c07f-148">toorename un archivo, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c07f-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="2c07f-149">toodownload un archivo, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c07f-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="2c07f-150">toodelete un archivo, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2c07f-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="2c07f-151">Cuando se le solicite, escriba **Y** toodelete elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2c07f-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="2c07f-152">Si tiene más de un toodelete de archivo, puede proporcionar todas las rutas de acceso de hello separados por coma.</span><span class="sxs-lookup"><span data-stu-id="2c07f-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="2c07f-153">Eliminación de una cuenta del Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="2c07f-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="2c07f-154">Use su cuenta de almacén de Data Lake de hello después toodelete de comando.</span><span class="sxs-lookup"><span data-stu-id="2c07f-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="2c07f-155">Cuando se le solicite, escriba **Y** cuenta de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="2c07f-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="2c07f-156">Guía de rendimiento al usar PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c07f-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="2c07f-157">A continuación se muestran Hola configuraciones más importantes que pueden estar atento tooget Hola obtener el mejor rendimiento al usar PowerShell toowork con almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="2c07f-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="2c07f-158">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2c07f-158">Property</span></span>            | <span data-ttu-id="2c07f-159">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2c07f-159">Default</span></span> | <span data-ttu-id="2c07f-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="2c07f-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="2c07f-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="2c07f-161">PerFileThreadCount</span></span>  | <span data-ttu-id="2c07f-162">10</span><span class="sxs-lookup"><span data-stu-id="2c07f-162">10</span></span>      | <span data-ttu-id="2c07f-163">Este parámetro permite a toochoose número de Hola de subprocesos paralelos para cargar o descargar cada archivo.</span><span class="sxs-lookup"><span data-stu-id="2c07f-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="2c07f-164">Este número representa Hola número máximo de subprocesos que se pueden asignar por archivo, pero es posible que obtenga menos subprocesos según el escenario (por ejemplo, si está cargando un archivo de 1 KB, obtendrá un subproceso, incluso si se le solicite 20 subprocesos).</span><span class="sxs-lookup"><span data-stu-id="2c07f-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="2c07f-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="2c07f-165">ConcurrentFileCount</span></span> | <span data-ttu-id="2c07f-166">10</span><span class="sxs-lookup"><span data-stu-id="2c07f-166">10</span></span>      | <span data-ttu-id="2c07f-167">Este parámetro es específico para cargar o descargar carpetas.</span><span class="sxs-lookup"><span data-stu-id="2c07f-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="2c07f-168">Este parámetro determina el número de Hola de archivos simultáneos que puede ser cargados o descargados.</span><span class="sxs-lookup"><span data-stu-id="2c07f-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="2c07f-169">Este número representa el número máximo de Hola de archivos simultáneos que puede ser cargados o descargados al mismo tiempo, pero es posible que obtenga menos simultaneidad según el escenario (por ejemplo, si va a cargar dos archivos, obtendrá dos cargas de archivos simultáneas, incluso si se le solicite 15).</span><span class="sxs-lookup"><span data-stu-id="2c07f-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="2c07f-170">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="2c07f-170">**Example**</span></span>

<span data-ttu-id="2c07f-171">Este comando descarga los archivos de la unidad local del usuario de almacén de Azure Data Lake toohello con 20 subprocesos por archivo y 100 archivos simultáneos.</span><span class="sxs-lookup"><span data-stu-id="2c07f-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="2c07f-172">¿Cómo determino hello tooset de valor para estos parámetros?</span><span class="sxs-lookup"><span data-stu-id="2c07f-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="2c07f-173">A continuación hay algunas instrucciones que puede usar.</span><span class="sxs-lookup"><span data-stu-id="2c07f-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="2c07f-174">**Paso 1: Determinar el número total de subprocesos de hello** -debe empezar por el cálculo toouse de recuento total de subprocesos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c07f-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="2c07f-175">Como norma general, debe usar seis subprocesos por cada núcleo físico.</span><span class="sxs-lookup"><span data-stu-id="2c07f-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="2c07f-176">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="2c07f-176">**Example**</span></span>

    <span data-ttu-id="2c07f-177">Suponiendo que se está ejecutando Hola PowerShell comandos de una máquina virtual D14 que tiene 16 núcleos</span><span class="sxs-lookup"><span data-stu-id="2c07f-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="2c07f-178">**Paso 2: Calcular PerFileThreadCount** -calculamos nuestro PerFileThreadCount según Hola tamaño de los archivos de saludo.</span><span class="sxs-lookup"><span data-stu-id="2c07f-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="2c07f-179">Para archivos de menos de 2,5 GB, no hay ninguna necesidad de toochange este parámetro porque predeterminado Hola de 10 es suficiente.</span><span class="sxs-lookup"><span data-stu-id="2c07f-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="2c07f-180">Para los archivos mayores de GB 2.5, debe usar 10 subprocesos como base Hola Hola primera 2,5 GB y agregar 1 subproceso de cada aumento adicional de 256 MB de tamaño del archivo.</span><span class="sxs-lookup"><span data-stu-id="2c07f-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="2c07f-181">Si está copiando una carpeta con muchos tamaños de archivo, considere la posibilidad de agruparlos por tamaños de archivo similares.</span><span class="sxs-lookup"><span data-stu-id="2c07f-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="2c07f-182">Tener tamaños de archivo diferentes puede provocar un rendimiento no óptimo.</span><span class="sxs-lookup"><span data-stu-id="2c07f-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="2c07f-183">Si no es posible toogroup tamaños de archivo similares, debe establecer PerFileThreadCount según Hola mayor tamaño de archivo.</span><span class="sxs-lookup"><span data-stu-id="2c07f-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="2c07f-184">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="2c07f-184">**Example**</span></span>

    <span data-ttu-id="2c07f-185">Suponiendo que tenga 100 archivos comprendido entre 1GB too10GB, usamos Hola 10GB como Hola de mayor tamaño de ecuación, que se lee como Hola siguiente del archivo.</span><span class="sxs-lookup"><span data-stu-id="2c07f-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="2c07f-186">**Paso 3: Calcular ConcurrentFilecount** -recuento de uso total de subprocesos de Hola y PerFileThreadCount toocalculate ConcurrentFileCount basándose en hello después de la ecuación.</span><span class="sxs-lookup"><span data-stu-id="2c07f-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="2c07f-187">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="2c07f-187">**Example**</span></span>

    <span data-ttu-id="2c07f-188">En función de los valores de ejemplo de Hola que se ha utilizado</span><span class="sxs-lookup"><span data-stu-id="2c07f-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="2c07f-189">Por lo tanto, **ConcurrentFileCount** es **2.4**, que se puede redondear demasiado**2**.</span><span class="sxs-lookup"><span data-stu-id="2c07f-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="2c07f-190">Ajuste adicional</span><span class="sxs-lookup"><span data-stu-id="2c07f-190">Further tuning</span></span>

<span data-ttu-id="2c07f-191">Es posible que necesite para la optimización adicional porque no hay un intervalo de toowork de tamaños de archivo con.</span><span class="sxs-lookup"><span data-stu-id="2c07f-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="2c07f-192">Hola anteriormente cálculo funciona bien si todos o la mayoría de los archivos de hello es intervalos de 10GB de toohello más grandes y más cercano.</span><span class="sxs-lookup"><span data-stu-id="2c07f-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="2c07f-193">Por el contrario, si hay muchos tamaños de archivo diferentes, con muchos archivos pequeños, podría reducir PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="2c07f-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="2c07f-194">Reduciendo hello PerFileThreadCount, podemos ampliamos ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="2c07f-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="2c07f-195">Por lo tanto, si suponemos que la mayoría de los archivos es más pequeña en el intervalo de 5GB de hello, se puede volver a realizar nuestro cálculo:</span><span class="sxs-lookup"><span data-stu-id="2c07f-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="2c07f-196">Por lo tanto, **ConcurrentFileCount** se ahora 96/20, que es 4.8, redondeará demasiado**4**.</span><span class="sxs-lookup"><span data-stu-id="2c07f-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="2c07f-197">Puede seguir tootune esta configuración cambiando hello **PerFileThreadCount** arriba y abajo según distribución Hola de los tamaños de archivo.</span><span class="sxs-lookup"><span data-stu-id="2c07f-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="2c07f-198">Limitación</span><span class="sxs-lookup"><span data-stu-id="2c07f-198">Limitation</span></span>

* <span data-ttu-id="2c07f-199">**Número de archivos es menor que ConcurrentFileCount**: si el número de Hola de archivos que se va a cargar es menor que hello **ConcurrentFileCount** que calcula, a continuación, se debe reducir  **ConcurrentFileCount** toobe toohello igual número de archivos.</span><span class="sxs-lookup"><span data-stu-id="2c07f-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="2c07f-200">Puede usar cualquier tooincrease de subprocesos restantes **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="2c07f-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="2c07f-201">**Hay demasiados subprocesos**: si se aumenta el subproceso número demasiada sin aumentar el tamaño del clúster, se corre el riesgo de Hola de reducción del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2c07f-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="2c07f-202">Puede haber problemas de contención al cambio de contexto en hello CPU.</span><span class="sxs-lookup"><span data-stu-id="2c07f-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="2c07f-203">**Simultaneidad suficiente**: si no es suficiente la simultaneidad de hello, el clúster puede ser demasiado pequeño.</span><span class="sxs-lookup"><span data-stu-id="2c07f-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="2c07f-204">Puede aumentar el número de Hola de nodos en el clúster lo que le proporcionará más simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="2c07f-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="2c07f-205">**Errores de limitación**: es posible que vea errores de limitación si la simultaneidad es demasiado alta.</span><span class="sxs-lookup"><span data-stu-id="2c07f-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="2c07f-206">Si ve errores de limitación, debe reducir la simultaneidad de Hola o póngase en contacto con nosotros.</span><span class="sxs-lookup"><span data-stu-id="2c07f-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c07f-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2c07f-207">Next steps</span></span>
* [<span data-ttu-id="2c07f-208">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2c07f-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="2c07f-209">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2c07f-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="2c07f-210">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2c07f-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

