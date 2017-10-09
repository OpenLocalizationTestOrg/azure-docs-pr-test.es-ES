---
<span data-ttu-id="30e4b-101">título: aaa "PowerShell: clúster de HDInsight de Azure con el almacén de Data Lake como almacenamiento adicional | Servicios de Microsoft Docs":-: almacén de data lake, hdinsight documentationcenter: '' autor: nitinme manager: editor jhubbard: cgronlun</span><span class="sxs-lookup"><span data-stu-id="30e4b-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="30e4b-102">MS.AssetId: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: almacén de data lake ms.devlang: na ms.topic: artículo ms.tgt_pltfrm: na ms.workload: ms.date de grandes cantidades de datos: 06/08/2017 ms.author: nitinme</span><span class="sxs-lookup"><span data-stu-id="30e4b-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="30e4b-103">Use toocreate un clúster de HDInsight de Azure PowerShell con almacén de Data Lake (como almacenamiento adicional)</span><span class="sxs-lookup"><span data-stu-id="30e4b-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30e4b-104">Uso del Portal</span><span class="sxs-lookup"><span data-stu-id="30e4b-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="30e4b-105">Uso de PowerShell (para el almacenamiento predeterminado)</span><span class="sxs-lookup"><span data-stu-id="30e4b-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="30e4b-106">Uso de PowerShell (para el almacenamiento adicional)</span><span class="sxs-lookup"><span data-stu-id="30e4b-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="30e4b-107">Uso de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="30e4b-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="30e4b-108">Obtenga información acerca de cómo toouse Azure PowerShell tooconfigure un HDInsight de clúster con el almacén de Azure Data Lake **como almacenamiento adicional**.</span><span class="sxs-lookup"><span data-stu-id="30e4b-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="30e4b-109">Para obtener instrucciones sobre cómo toocreate una HDInsight de clúster con el almacén de Data Lake de Azure como almacenamiento predeterminado, consulte [crear un clúster de HDInsight con el almacén de Data Lake como almacenamiento predeterminado](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="30e4b-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="30e4b-110">Si va a almacén de toouse Azure Data Lake como almacenamiento adicional para el clúster de HDInsight, se recomienda hacer esto al crear el clúster de hello tal como se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="30e4b-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="30e4b-111">Agregar almacén de Azure Data Lake como almacenamiento adicional tooan clúster de HDInsight existente es un proceso complicado y propensa a tooerrors.</span><span class="sxs-lookup"><span data-stu-id="30e4b-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="30e4b-112">En el caso de los tipos de clúster compatibles, Data Lake Store se puede usar como almacenamiento predeterminado o como cuenta de almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="30e4b-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="30e4b-113">Cuando se utiliza el almacén de Data Lake como almacenamiento adicional, cuenta de almacenamiento predeterminada de Hola para clústeres de hello seguirán estando Blobs de almacenamiento de Azure (WASB) y archivos relacionados con el clúster de hello (por ejemplo, registros, etc.) se escriben todavía almacenamiento predeterminado de toohello, mientras que los datos de Hola que desea tooprocess pueden almacenarse en una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="30e4b-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="30e4b-114">Usar almacén de Data Lake como una cuenta de almacenamiento adicional no afecta a rendimiento u Hola capacidad tooread/escritura toohello almacenamiento Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="30e4b-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="30e4b-115">Uso de Data Lake Store para el almacenamiento de clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="30e4b-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="30e4b-116">Estas son algunas consideraciones importantes que deben tenerse en cuenta al usar HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="30e4b-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="30e4b-117">Clústeres de HDInsight de toocreate opción con acceso tooData Lake almacén como almacenamiento adicional está disponible para las versiones 3.2, 3.4, 3.5 y 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="30e4b-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="30e4b-118">Configuración de HDInsight toowork con el almacén de Data Lake con PowerShell implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="30e4b-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="30e4b-119">Creación de un Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="30e4b-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="30e4b-120">Configure la autenticación para basada en roles acceder tooData Lake almacén</span><span class="sxs-lookup"><span data-stu-id="30e4b-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="30e4b-121">Crear el clúster de HDInsight con el almacén de autenticación tooData Lake</span><span class="sxs-lookup"><span data-stu-id="30e4b-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="30e4b-122">Ejecutar un trabajo de prueba en el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="30e4b-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30e4b-123">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="30e4b-123">Prerequisites</span></span>
<span data-ttu-id="30e4b-124">Antes de comenzar este tutorial, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="30e4b-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="30e4b-125">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="30e4b-125">**An Azure subscription**.</span></span> <span data-ttu-id="30e4b-126">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30e4b-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="30e4b-127">**Azure PowerShell 1.0 o versiones posteriores**.</span><span class="sxs-lookup"><span data-stu-id="30e4b-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="30e4b-128">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="30e4b-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="30e4b-129">**Windows SDK**.</span><span class="sxs-lookup"><span data-stu-id="30e4b-129">**Windows SDK**.</span></span> <span data-ttu-id="30e4b-130">Puede instalarlo desde [aquí](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="30e4b-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="30e4b-131">Utilice este toocreate un certificado de seguridad.</span><span class="sxs-lookup"><span data-stu-id="30e4b-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="30e4b-132">**Entidad de servicio de Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="30e4b-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="30e4b-133">Pasos de este tutorial proporcionan instrucciones sobre cómo toocreate una entidad de servicio en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30e4b-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="30e4b-134">Sin embargo, debe ser un toocreate capaz de Azure AD administrador toobe una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="30e4b-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="30e4b-135">Si eres un administrador de Azure AD, puede omitir este requisito previo y continuar con tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="30e4b-136">**Si no es un administrador de Azure AD**, no será capaz de tooperform Hola pasos necesarios toocreate una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="30e4b-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="30e4b-137">En este caso, su administrador de Azure AD debe generar primero una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="30e4b-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="30e4b-138">Además, entidad de servicio de hello debe crearse con un certificado, como se describe en [crear una entidad de servicio con el certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="30e4b-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="30e4b-139">Creación de un Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="30e4b-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="30e4b-140">Siga estos toocreate pasos un almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="30e4b-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="30e4b-141">Desde el escritorio, abra una nueva ventana de PowerShell de Azure y escriba el siguiente fragmento de código de hello.</span><span class="sxs-lookup"><span data-stu-id="30e4b-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="30e4b-142">Cuando toolog solicitada, asegúrese de que inicie sesión como un administrador o propietario de la suscripción de hello:</span><span class="sxs-lookup"><span data-stu-id="30e4b-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="30e4b-143">Si recibe un mensaje de error similar demasiado`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` al registrar el proveedor de recursos de almacén de Data Lake hello, es posible que la suscripción no está permitido para el almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="30e4b-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="30e4b-144">Asegúrese de habilitar su suscripción de Azure en la versión preliminar pública de Data Lake Store siguiendo estas [instrucciones](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="30e4b-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="30e4b-145">La cuenta de Almacén de Azure Data Lake se asocia con un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="30e4b-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="30e4b-146">Comience creando un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="30e4b-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="30e4b-147">La salida debe ser parecida a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="30e4b-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="30e4b-148">Cree una cuenta de Almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="30e4b-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="30e4b-149">cuenta de Hello nombre que especifique debe contener solo letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="30e4b-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="30e4b-150">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="30e4b-150">You should see an output like hello following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. <span data-ttu-id="30e4b-151">Cargar algunos tooAzure de datos de ejemplo Data Lake.</span><span class="sxs-lookup"><span data-stu-id="30e4b-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="30e4b-152">Vamos a usar más adelante en este tooverify de artículo que datos de hello sean accesibles desde un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="30e4b-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="30e4b-153">Si desea obtener algunos tooupload de datos de ejemplo, puede obtener hello **ambulancia datos** carpeta de hello [repositorio de Git de Azure datos Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="30e4b-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="30e4b-154">Configure la autenticación para basada en roles acceder tooData Lake almacén</span><span class="sxs-lookup"><span data-stu-id="30e4b-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="30e4b-155">Cada una de las suscripciones de Azure está asociada a un Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30e4b-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="30e4b-156">Los usuarios y servicios que tienen acceso a recursos de suscripción de hello mediante el Portal de Azure clásico de Hola o API de administrador de recursos de Azure deben autenticarse primero con la que Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30e4b-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="30e4b-157">Se concede acceso tooAzure suscripciones y servicios mediante la asignación de rol adecuado de hello en un recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="30e4b-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="30e4b-158">Para los servicios, una entidad de servicio identifica servicio Hola Hola Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="30e4b-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="30e4b-159">Esta sección muestra cómo toogrant una aplicación de servicio, como HDInsight, tooan de acceso a recursos de Azure (Hola cuenta de almacén de Data Lake de Azure que creó anteriormente) al crear una entidad de servicio para la aplicación hello y asignarles roles toothat a través de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30e4b-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="30e4b-160">tooset la autenticación de Active Directory para Data Lake de Azure, debe realizar Hola siguiente las tareas.</span><span class="sxs-lookup"><span data-stu-id="30e4b-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="30e4b-161">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="30e4b-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="30e4b-162">Creación de una aplicación en Azure Active Directory y una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="30e4b-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="30e4b-163">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="30e4b-163">Create a self-signed certificate</span></span>
<span data-ttu-id="30e4b-164">Asegúrese de que tiene [Windows SDK](https://dev.windows.com/en-us/downloads) instalado antes de continuar con hello pasos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="30e4b-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="30e4b-165">Debe también ha creado un directorio, como **C:\mycertdir**, donde se creará el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="30e4b-166">Desde la ventana de PowerShell de hello, navegue ubicación toohello donde se instaló el SDK de Windows (normalmente, `C:\Program Files (x86)\Windows Kits\10\bin\x86` y usar hello [MakeCert] [ makecert] toocreate utilidad un certificado autofirmado y un clave privada.</span><span class="sxs-lookup"><span data-stu-id="30e4b-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="30e4b-167">Usar hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="30e4b-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="30e4b-168">Es posible que la contraseña de clave privada tooenter solicitadas Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="30e4b-169">Después de comando de Hola se ejecuta correctamente, debería ver un **CertFile.cer** y **mykey.pvk** en directorio de hello certificado especificado.</span><span class="sxs-lookup"><span data-stu-id="30e4b-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="30e4b-170">Hola de uso [Pvk2Pfx] [ pvk2pfx] utilidad tooconvert Hola .pvk y .cer archivos archivo .pfx MakeCert tooa creado.</span><span class="sxs-lookup"><span data-stu-id="30e4b-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="30e4b-171">Ejecutar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="30e4b-172">Cuando se le solicite escribir contraseña de clave privada de hello especificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="30e4b-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="30e4b-173">Hola valor especificado en hello **-po** parámetro es la contraseña de Hola que está asociado con el archivo .pfx de Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="30e4b-174">Después de que se complete correctamente el comando hello, también verá un CertFile.pfx en directorio de hello certificado especificado.</span><span class="sxs-lookup"><span data-stu-id="30e4b-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="30e4b-175">Creación de una aplicación en Azure Active Directory y una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="30e4b-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="30e4b-176">En esta sección, realizar pasos de hello toocreate una entidad de servicio para una aplicación de Azure Active Directory, asignar a una entidad de servicio de rol toohello y autenticarse como entidad de servicio de hello proporcionando un certificado.</span><span class="sxs-lookup"><span data-stu-id="30e4b-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="30e4b-177">Ejecutar Hola después toocreate de comandos en una aplicación en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30e4b-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="30e4b-178">Pegue Hola siguientes cmdlets en la ventana de consola de PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="30e4b-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="30e4b-179">Asegúrese de que valor Hola que especifique para hello **- DisplayName** propiedad es única.</span><span class="sxs-lookup"><span data-stu-id="30e4b-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="30e4b-180">Además, Hola valores para **- página principal** y **- IdentiferUris** son valores de marcador de posición y no se comprueban.</span><span class="sxs-lookup"><span data-stu-id="30e4b-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="30e4b-181">Crear a una entidad de servicio con Id. de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="30e4b-182">Conceda carpeta de almacén de Data Lake del toohello de acceso principal de servicio de Hola y archivo hello que tendrá acceso de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="30e4b-183">fragmento de código de Hello siguiente proporciona raíz de toohello de acceso del programa Hola a almacén de Data Lake (donde haya copiado el archivo de datos de ejemplo de Hola) de la cuenta y Hola propio archivo.</span><span class="sxs-lookup"><span data-stu-id="30e4b-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="30e4b-184">Creación de un clúster de HDInsight en Linux con Data Lake Store como almacenamiento adicional</span><span class="sxs-lookup"><span data-stu-id="30e4b-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="30e4b-185">En esta sección, se creará un clúster de Hadoop en HDInsight basado en Linux con Data Lake Store como almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="30e4b-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="30e4b-186">En esta versión, clúster de HDInsight de Hola y Hola almacén de Data Lake deben estar en hello misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="30e4b-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="30e4b-187">Iniciar al recuperar el identificador del inquilino de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="30e4b-188">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="30e4b-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="30e4b-189">En esta versión, para un clúster de Hadoop, almacén de Data Lake solo sirve como un almacenamiento adicional para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="30e4b-190">almacenamiento predeterminado de Hello seguirán siendo blobs hello en el almacenamiento de Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="30e4b-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="30e4b-191">Por lo tanto, primero crearemos Hola contenedores de almacenamiento y la cuenta de almacenamiento necesarios para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="30e4b-192">Crear el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="30e4b-193">Usar hello siguientes cmdlets.</span><span class="sxs-lookup"><span data-stu-id="30e4b-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="30e4b-194">Después de que se complete correctamente el cmdlet de hello, debería ver una salida de hello clúster detalles del anuncio.</span><span class="sxs-lookup"><span data-stu-id="30e4b-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="30e4b-195">Ejecutar trabajos de prueba en Hola de toouse de clúster de HDInsight de hello almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="30e4b-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="30e4b-196">Después de haber configurado un clúster de HDInsight, se puede ejecutar trabajos de prueba en hello clúster tootest ese hello HDInsight clúster puede tener acceso a almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="30e4b-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="30e4b-197">toodo por lo tanto, se ejecutará un trabajo de Hive de ejemplo que crea una tabla con datos de ejemplo de Hola que cargan almacén de Data Lake de tooyour anteriores.</span><span class="sxs-lookup"><span data-stu-id="30e4b-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="30e4b-198">En esta sección aprenderá lo SSH en hello HDInsight Linux de clúster que ha creado y ejecutar una consulta de Hive de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="30e4b-199">Si está usando un tooSSH de cliente de Windows en clúster de hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="30e4b-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="30e4b-200">Si está usando un tooSSH de cliente de Linux en clúster de hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="30e4b-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="30e4b-201">Una vez conectado, inicie Hola Hive CLI mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="30e4b-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="30e4b-202">Hola CLI, escriba Hola siguiendo las instrucciones toocreate una nueva tabla denominada **vehículos** mediante el uso de datos de ejemplo de Hola Hola almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="30e4b-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="30e4b-203">Debería ver un siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="30e4b-203">You should see an output similar toohello following:</span></span>

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="30e4b-204">Acceso al Almacén de Data Lake mediante comandos de HDFS</span><span class="sxs-lookup"><span data-stu-id="30e4b-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="30e4b-205">Una vez haya configurado el almacén de hello HDInsight clúster toouse Data Lake, puede usar comandos de shell de hello HDFS tooaccess Hola almacén.</span><span class="sxs-lookup"><span data-stu-id="30e4b-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="30e4b-206">En esta sección aprenderá lo SSH en hello HDInsight Linux de clúster que ha creado y ejecutar comandos HDFS Hola.</span><span class="sxs-lookup"><span data-stu-id="30e4b-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="30e4b-207">Si está usando un tooSSH de cliente de Windows en clúster de hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="30e4b-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="30e4b-208">Si está usando un tooSSH de cliente de Linux en clúster de hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="30e4b-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="30e4b-209">Una vez conectado, use Hola siguientes archivos HDFS filesystem comando toolist Hola Hola almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="30e4b-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="30e4b-210">Esto debería incluir archivo hello que cargan almacén de Data Lake de toohello anteriores.</span><span class="sxs-lookup"><span data-stu-id="30e4b-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="30e4b-211">También puede usar hello `hdfs dfs -put` comando tooupload algunos toohello archivos del almacén de Data Lake y, a continuación, usar `hdfs dfs -ls` tooverify si los archivos de saludo se cargaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="30e4b-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="30e4b-212">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="30e4b-212">See Also</span></span>
* [<span data-ttu-id="30e4b-213">Portal: Crear un toouse de clúster de HDInsight almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="30e4b-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
