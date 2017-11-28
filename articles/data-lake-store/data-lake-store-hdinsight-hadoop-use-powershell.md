---
title: "PowerShell: clúster de Azure HDInsight con Data Lake Store como almacenamiento complementario | Microsoft Docs"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/08/2017
ms.author: nitinme
ms.openlocfilehash: 7a7069adab5742a9dae2833c13a1db57337a41a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ec974-102">Uso de Azure PowerShell para crear clústeres de HDInsight con Data Lake Store (como almacenamiento adicional)</span><span class="sxs-lookup"><span data-stu-id="ec974-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec974-103">Uso del Portal</span><span class="sxs-lookup"><span data-stu-id="ec974-103">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="ec974-104">Uso de PowerShell (para el almacenamiento predeterminado)</span><span class="sxs-lookup"><span data-stu-id="ec974-104">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="ec974-105">Uso de PowerShell (para el almacenamiento adicional)</span><span class="sxs-lookup"><span data-stu-id="ec974-105">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="ec974-106">Uso de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec974-106">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="ec974-107">Aprenda a usar Azure PowerShell para configurar un clúster de HDInsight con Azure Data Lake Store **como almacenamiento adicional**.</span><span class="sxs-lookup"><span data-stu-id="ec974-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="ec974-108">Para obtener instrucciones acerca de cómo crear un clúster de HDInsight con Azure Data Lake Store como almacenamiento predeterminado, consulte [Creación de un clúster de HDInsight con Data Lake Store mediante Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ec974-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ec974-109">Si va a usar Azure Data Lake Store como almacenamiento adicional para un clúster de HDInsight, se recomienda encarecidamente hacer esto al crear el clúster como se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ec974-109">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="ec974-110">La adición de Azure Data Lake Store como almacenamiento adicional a un clúster de HDInsight existente es un proceso complicado y en la que es fácil que se produzcan errores.</span><span class="sxs-lookup"><span data-stu-id="ec974-110">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

<span data-ttu-id="ec974-111">En el caso de los tipos de clúster compatibles, Data Lake Store se puede usar como almacenamiento predeterminado o como cuenta de almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="ec974-111">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="ec974-112">Cuando Data Lake Store se usa como almacenamiento adicional, la cuenta de almacenamiento predeterminada para los clústeres seguirá siendo Azure Storage Blobs (WASB) y los archivos relacionados con clústeres (como registros, etc.) seguirán escribiéndose en el almacenamiento predeterminado, mientras que los datos que quiere procesar pueden almacenarse en una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec974-112">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="ec974-113">Utilizar el Almacén de Data Lake como una cuenta de almacenamiento adicional no afecta al rendimiento o la capacidad de lectura y escritura en el almacenamiento del clúster.</span><span class="sxs-lookup"><span data-stu-id="ec974-113">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="ec974-114">Uso de Data Lake Store para el almacenamiento de clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec974-114">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="ec974-115">Estas son algunas consideraciones importantes que deben tenerse en cuenta al usar HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="ec974-115">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="ec974-116">La opción para crear clústeres de HDInsight con acceso a Data Lake Store como almacenamiento está disponible para las versiones 3.2, 3.4, 3.5 y 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec974-116">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="ec974-117">La configuración de HDInsight para trabajar con el Almacén de Data Lake mediante PowerShell consta de los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ec974-117">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span></span>

* <span data-ttu-id="ec974-118">Creación de un Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ec974-118">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="ec974-119">Configuración de la autenticación para el acceso basado en roles al Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="ec974-119">Set up authentication for role-based access to Data Lake Store</span></span>
* <span data-ttu-id="ec974-120">Creación de un clúster de HDInsight con autenticación en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="ec974-120">Create HDInsight cluster with authentication to Data Lake Store</span></span>
* <span data-ttu-id="ec974-121">Ejecución de un trabajo de prueba en el clúster</span><span class="sxs-lookup"><span data-stu-id="ec974-121">Run a test job on the cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec974-122">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ec974-122">Prerequisites</span></span>
<span data-ttu-id="ec974-123">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ec974-123">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="ec974-124">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="ec974-124">**An Azure subscription**.</span></span> <span data-ttu-id="ec974-125">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec974-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ec974-126">**Azure PowerShell 1.0 o versiones posteriores**.</span><span class="sxs-lookup"><span data-stu-id="ec974-126">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="ec974-127">Consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ec974-127">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ec974-128">**Windows SDK**.</span><span class="sxs-lookup"><span data-stu-id="ec974-128">**Windows SDK**.</span></span> <span data-ttu-id="ec974-129">Puede instalarlo desde [aquí](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="ec974-129">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="ec974-130">Úselo para crear un certificado de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ec974-130">You use this to create a security certificate.</span></span>
* <span data-ttu-id="ec974-131">**Entidad de servicio de Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="ec974-131">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="ec974-132">En los pasos de este tutorial se proporcionan instrucciones sobre cómo crear entidades de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec974-132">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="ec974-133">Sin embargo, debe ser administrador de Azure AD para poder crearlas.</span><span class="sxs-lookup"><span data-stu-id="ec974-133">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="ec974-134">Si ya lo es, puede hacer caso omiso a este requisito previo y continuar con el tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec974-134">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="ec974-135">**Si no lo es**, no podrá realizar los pasos necesarios para crear una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="ec974-135">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="ec974-136">En este caso, su administrador de Azure AD debe generar primero una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec974-136">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="ec974-137">Además, la entidad de servicio debe crearse con un certificado, tal y como se describe en [Creación de una entidad de servicio](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="ec974-137">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="ec974-138">Creación de un Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ec974-138">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="ec974-139">Siga estos pasos para crear un Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ec974-139">Follow these steps to create a Data Lake Store.</span></span>

1. <span data-ttu-id="ec974-140">En el escritorio, abra una nueva ventana de Azure PowerShell y escriba el siguiente fragmento.</span><span class="sxs-lookup"><span data-stu-id="ec974-140">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span></span> <span data-ttu-id="ec974-141">Cuando se le solicite iniciar sesión, asegúrese de iniciarla como uno de los administradores o propietario de la suscripción:</span><span class="sxs-lookup"><span data-stu-id="ec974-141">When prompted to log in, make sure you log in as one of the subscription administrator/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="ec974-142">Si recibe un error similar a `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` al registrar el proveedor de recursos de Data Lake Store, es posible que su suscripción no esté en la lista de permitidas de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec974-142">If you receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` when registering the Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="ec974-143">Asegúrese de habilitar su suscripción de Azure en la versión preliminar pública de Data Lake Store siguiendo estas [instrucciones](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ec974-143">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="ec974-144">La cuenta de Almacén de Azure Data Lake se asocia con un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ec974-144">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="ec974-145">Comience creando un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ec974-145">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="ec974-146">La salida debe ser parecida a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="ec974-146">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="ec974-147">Cree una cuenta de Almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ec974-147">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="ec974-148">El nombre de cuenta que especifique debe contener solo letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="ec974-148">The account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="ec974-149">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ec974-149">You should see an output like the following:</span></span>

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

5. <span data-ttu-id="ec974-150">Cargue datos de ejemplo a Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ec974-150">Upload some sample data to Azure Data Lake.</span></span> <span data-ttu-id="ec974-151">Los usaremos más adelante en este artículo para comprobar que se puede acceder a los datos desde un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec974-151">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="ec974-152">Si busca datos de ejemplo para cargar, puede obtener la carpeta **Ambulance Data** en el [repositorio Git de Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="ec974-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="ec974-153">Configuración de la autenticación para el acceso basado en roles al Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="ec974-153">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="ec974-154">Cada una de las suscripciones de Azure está asociada a un Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec974-154">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="ec974-155">Los usuarios y los servicios que acceden a los recursos de la suscripción mediante el Portal de Azure clásico o la API de Azure Resource Manager deben autenticarse primero en ese Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec974-155">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="ec974-156">Para conceder acceso a servicios y suscripciones de Azure, se les asigna el rol adecuado en un recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="ec974-156">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span>  <span data-ttu-id="ec974-157">Para los servicios, una entidad de servicio identifica al servicio en Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="ec974-157">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="ec974-158">En esta sección, se muestra cómo conceder a un servicio de aplicación, como HDInsight, acceso a un recurso de Azure (la cuenta de Almacén de Azure Data Lake creada antes) mediante la creación de una entidad de servicio para la aplicación y la asignación de roles a ella a través de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec974-158">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span></span>

<span data-ttu-id="ec974-159">Para configurar la autenticación de Active Directory para Azure Data Lake, debe realizar las siguientes tareas.</span><span class="sxs-lookup"><span data-stu-id="ec974-159">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span></span>

* <span data-ttu-id="ec974-160">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="ec974-160">Create a self-signed certificate</span></span>
* <span data-ttu-id="ec974-161">Creación de una aplicación en Azure Active Directory y una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="ec974-161">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="ec974-162">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="ec974-162">Create a self-signed certificate</span></span>
<span data-ttu-id="ec974-163">Asegúrese de que tiene [Windows SDK](https://dev.windows.com/en-us/downloads) instalado antes de continuar con los pasos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="ec974-163">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="ec974-164">También debe crear un directorio, como **C:\mycertdir**, donde se creará el certificado.</span><span class="sxs-lookup"><span data-stu-id="ec974-164">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span></span>

1. <span data-ttu-id="ec974-165">En la ventana de PowerShell, vaya a la ubicación donde instaló Windows SDK (normalmente, `C:\Program Files (x86)\Windows Kits\10\bin\x86`) y use la utilidad [MakeCert][makecert] para crear un certificado autofirmado y una clave privada.</span><span class="sxs-lookup"><span data-stu-id="ec974-165">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="ec974-166">Use los comandos siguientes.</span><span class="sxs-lookup"><span data-stu-id="ec974-166">Use the following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="ec974-167">Se le pedirá que escriba la contraseña de la clave privada.</span><span class="sxs-lookup"><span data-stu-id="ec974-167">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="ec974-168">Después de que el comando se ejecute correctamente, debería ver los archivos **CertFile.cer** y **mykey.pvk** en el directorio de certificado especificado.</span><span class="sxs-lookup"><span data-stu-id="ec974-168">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span></span>
2. <span data-ttu-id="ec974-169">Emplee la utilidad [Pvk2Pfx][pvk2pfx] para convertir los archivos .pvk y .cer que MakeCert creó en un archivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="ec974-169">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="ec974-170">Ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="ec974-170">Run the following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="ec974-171">Cuando se le pida, escriba la contraseña de la clave privada que especificó antes.</span><span class="sxs-lookup"><span data-stu-id="ec974-171">When prompted enter the private key password you specified earlier.</span></span> <span data-ttu-id="ec974-172">El valor especificado para el parámetro **-po** es la contraseña asociada al archivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="ec974-172">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span></span> <span data-ttu-id="ec974-173">Cuando el comando se complete correctamente, debería ver un archivo CertFile.pfx en el directorio de certificado especificado.</span><span class="sxs-lookup"><span data-stu-id="ec974-173">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="ec974-174">Creación de una aplicación en Azure Active Directory y una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="ec974-174">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="ec974-175">En esta sección, llevará a cabo los pasos para crear una entidad de servicio para una aplicación de Azure Active Directory, asignar un rol a la entidad de servicio y autenticarse como la entidad de servicio proporcionando un certificado.</span><span class="sxs-lookup"><span data-stu-id="ec974-175">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="ec974-176">Ejecute los comandos siguientes para crear una aplicación en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec974-176">Run the following commands to create an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="ec974-177">Pegue los siguientes cmdlets en la ventana de consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec974-177">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="ec974-178">Asegúrese de que el valor especificado para la propiedad **- DisplayName** sea único.</span><span class="sxs-lookup"><span data-stu-id="ec974-178">Make sure the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="ec974-179">Además, los valores de **-HomePage** e **-IdentiferUris** son valores de marcador de posición y no se comprueban.</span><span class="sxs-lookup"><span data-stu-id="ec974-179">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

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
2. <span data-ttu-id="ec974-180">Cree una entidad de servicio con el identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec974-180">Create a service principal using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="ec974-181">Conceda acceso de entidad de servicio al archivo o la carpeta de Data Lake Store a la que accederá desde el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec974-181">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span></span> <span data-ttu-id="ec974-182">El fragmento de código siguiente proporciona acceso a la raíz de la cuenta de Data Lake Store (donde copió el archivo de datos de ejemplo) y al propio archivo.</span><span class="sxs-lookup"><span data-stu-id="ec974-182">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ec974-183">Creación de un clúster de HDInsight en Linux con Data Lake Store como almacenamiento adicional</span><span class="sxs-lookup"><span data-stu-id="ec974-183">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="ec974-184">En esta sección, se creará un clúster de Hadoop en HDInsight basado en Linux con Data Lake Store como almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="ec974-184">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="ec974-185">En esta versión, el clúster de HDInsight y Data Lake Store deben estar en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="ec974-185">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="ec974-186">Comience recuperando el identificador del inquilino de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ec974-186">Start with retrieving the subscription tenant ID.</span></span> <span data-ttu-id="ec974-187">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="ec974-187">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="ec974-188">En esta versión, para un clúster de Hadoop, el Almacén de Data Lake solo sirve como almacenamiento adicional para el clúster.</span><span class="sxs-lookup"><span data-stu-id="ec974-188">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span></span> <span data-ttu-id="ec974-189">El almacenamiento predeterminado seguirá siendo los blobs de almacenamiento de Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="ec974-189">The default storage will still be the Azure storage blobs (WASB).</span></span> <span data-ttu-id="ec974-190">En primer lugar, crearemos la cuenta de almacenamiento y los contenedores de almacenamiento necesarios para el clúster.</span><span class="sxs-lookup"><span data-stu-id="ec974-190">So, we'll first create the storage account and storage containers required for the cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="ec974-191">Cree el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec974-191">Create the HDInsight cluster.</span></span> <span data-ttu-id="ec974-192">Use los siguientes cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ec974-192">Use the following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="ec974-193">Una vez que el cmdlet se complete correctamente, debería ver un resultado con la información del clúster.</span><span class="sxs-lookup"><span data-stu-id="ec974-193">After the cmdlet successfully completes, you should see an output listing the cluster details.</span></span>


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="ec974-194">Ejecución de trabajos de prueba en el clúster de HDInsight para usar el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="ec974-194">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="ec974-195">Después de configurar un clúster de HDInsight, puede ejecutar trabajos de prueba en el clúster para probar que el clúster de HDInsight pueda acceder al Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ec974-195">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="ec974-196">Para hacerlo, ejecutaremos un trabajo de Hive de ejemplo que crea una tabla con los datos de ejemplo que cargó antes en el Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ec974-196">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="ec974-197">En esta sección, aprenderá a usar SSH en el clúster de Linux en HDInsight que creó y ejecutará una consulta de Hive de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ec974-197">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span></span>

* <span data-ttu-id="ec974-198">Si usa un cliente Windows para usar SSH en el clúster, consulte [Utilización de SSH con Hadoop en HDInsight basado en Linux desde Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ec974-198">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ec974-199">Si usa un cliente Linux para usar SSH en el clúster, consulte [Utilización de SSH con Hadoop en HDInsight basado en Linux desde Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ec974-199">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="ec974-200">Una vez conectado, inicie la CLI de Hive con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ec974-200">Once connected, start the Hive CLI by using the following command:</span></span>

        hive
2. <span data-ttu-id="ec974-201">Mediante la CLI, especifique las siguientes instrucciones para crear una tabla nueva denominada **vehicles** con los datos de ejemplo del Almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="ec974-201">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="ec974-202">Debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="ec974-202">You should see an output similar to the following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="ec974-203">Acceso al Almacén de Data Lake mediante comandos de HDFS</span><span class="sxs-lookup"><span data-stu-id="ec974-203">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="ec974-204">Una vez que configure el clúster de HDInsight para que use el Almacén de Data Lake, puede usar los comandos de shell de HDFS para acceder al almacén.</span><span class="sxs-lookup"><span data-stu-id="ec974-204">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="ec974-205">En esta sección, aprenderá a usar SSH en el clúster de Linux en HDInsight que creó y ejecutará los comandos de HDFS.</span><span class="sxs-lookup"><span data-stu-id="ec974-205">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span></span>

* <span data-ttu-id="ec974-206">Si usa un cliente Windows para usar SSH en el clúster, consulte [Utilización de SSH con Hadoop en HDInsight basado en Linux desde Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ec974-206">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ec974-207">Si usa un cliente Linux para usar SSH en el clúster, consulte [Utilización de SSH con Hadoop en HDInsight basado en Linux desde Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ec974-207">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="ec974-208">Una vez conectado, utilice el siguiente comando del sistema de archivos HDFS para enumerar los archivos del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ec974-208">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="ec974-209">Se debería incluir el archivo que cargó antes en el Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ec974-209">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="ec974-210">También puede usar el comando `hdfs dfs -put` para cargar algunos archivos en el almacén de Data Lake y después usar `hdfs dfs -ls` para comprobar si los archivos se cargaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="ec974-210">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="ec974-211">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ec974-211">See Also</span></span>
* [<span data-ttu-id="ec974-212">Aprovisionamiento de un clúster de HDInsight con el Almacén de Data Lake mediante el Portal de vista previa de Azure</span><span class="sxs-lookup"><span data-stu-id="ec974-212">Portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
