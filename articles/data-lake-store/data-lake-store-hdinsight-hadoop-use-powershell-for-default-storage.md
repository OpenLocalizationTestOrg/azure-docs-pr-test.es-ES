---
title: "Creación de clústeres de HDInsight con Data Lake Store como almacenamiento predeterminado mediante PowerShell | Microsoft Docs"
description: "Uso de Azure PowerShell para crear y usar clústeres de HDInsight con Azure Data Lake Store"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: 77eb83b80312eca401e6f60d57ed6a5668ea442e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="49bf8-103">Creación de clústeres de HDInsight con Data Lake Store como almacenamiento predeterminado mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="49bf8-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49bf8-104">Uso de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="49bf8-104">Use the Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="49bf8-105">Uso de PowerShell (para el almacenamiento predeterminado)</span><span class="sxs-lookup"><span data-stu-id="49bf8-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="49bf8-106">Uso de PowerShell (para almacenamiento adicional)</span><span class="sxs-lookup"><span data-stu-id="49bf8-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="49bf8-107">Uso de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="49bf8-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="49bf8-108">Obtenga información sobre cómo usar Azure PowerShell para configurar clústeres de Azure HDInsight con Azure Data Lake Store, como almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="49bf8-108">Learn how to use Azure PowerShell to configure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="49bf8-109">Para obtener instrucciones sobre la creación de un clúster de HDInsight con Azure Data Lake Store como almacenamiento adicional, consulte [Uso de Azure PowerShell para crear clústeres de HDInsight con Data Lake Store (como almacenamiento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="49bf8-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="49bf8-110">Estas son algunas consideraciones importantes que deben tenerse en cuenta al usar HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="49bf8-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="49bf8-111">La opción para crear clústeres de HDInsight con acceso a Data Lake Store como almacenamiento predeterminado está disponible para la versión 3.5 y 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="49bf8-111">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="49bf8-112">La opción para crear clústeres de HDInsight con acceso a Data Lake Store como almacenamiento predeterminado *no está disponible* para clústeres de HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="49bf8-112">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="49bf8-113">Para configurar HDInsight para trabajar con Data Lake Store con PowerShell, siga las instrucciones que aparecen en las cinco secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="49bf8-113">To configure HDInsight to work with Data Lake Store by using PowerShell, follow the instructions in the next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49bf8-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="49bf8-114">Prerequisites</span></span>
<span data-ttu-id="49bf8-115">Antes de comenzar este tutorial, asegúrese de que se cumplen los requisitos siguientes:</span><span class="sxs-lookup"><span data-stu-id="49bf8-115">Before you begin this tutorial, make sure that you meet the following requirements:</span></span>

* <span data-ttu-id="49bf8-116">**Suscripción a Azure**: Vaya a [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49bf8-116">**An Azure subscription**: Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="49bf8-117">**Azure PowerShell 1.0 o posterior**: Consulte [How to install and configure PowerShell](/powershell/azure/overview) (Instalación y configuración de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="49bf8-117">**Azure PowerShell 1.0 or greater**: See [How to install and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="49bf8-118">**Kit de desarrollo de software (SDK) de Windows**: Para instalar el SDK de Windows, vaya a [Descargas y herramientas para Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="49bf8-118">**Windows Software Development Kit (SDK)**: To install Windows SDK, go to [Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="49bf8-119">El SDK se usa para crear un certificado de seguridad.</span><span class="sxs-lookup"><span data-stu-id="49bf8-119">The SDK is used to create a security certificate.</span></span>
* <span data-ttu-id="49bf8-120">**Entidad de servicio de Azure Active Directory**: Este tutorial describe cómo crear una entidad de servicio en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49bf8-120">**Azure Active Directory service principal**: This tutorial describes how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="49bf8-121">Sin embargo, para crear una entidad de servicio, debe ser administrador de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49bf8-121">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="49bf8-122">Si ya lo es, puede hacer caso omiso a este requisito previo y continuar con el tutorial.</span><span class="sxs-lookup"><span data-stu-id="49bf8-122">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="49bf8-123">Solamente puede crear una entidad de servicio si es administrador de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49bf8-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="49bf8-124">Su administrador de Azure AD debe generar una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49bf8-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="49bf8-125">La entidad de servicio se debe crear con un certificado, tal y como se describe en [Creación de entidad de servicio con certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="49bf8-125">The service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="49bf8-126">Crear una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="49bf8-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="49bf8-127">Para crear una cuenta de Data Lake Store, realice el siguiente procedimiento:</span><span class="sxs-lookup"><span data-stu-id="49bf8-127">To create a Data Lake Store account, do the following:</span></span>

1. <span data-ttu-id="49bf8-128">En el escritorio, abra una ventana de PowerShell y escriba los siguientes fragmentos de código:</span><span class="sxs-lookup"><span data-stu-id="49bf8-128">From your desktop, open a PowerShell window, and then enter the snippets below.</span></span> <span data-ttu-id="49bf8-129">Cuando se le pida que inicie sesión, hágalo como uno de los propietarios o administradores de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="49bf8-129">When you are prompted to sign in, sign in as one of the subscription administrators or owners.</span></span> 

        # Sign in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="49bf8-130">Si registra el proveedor de recursos de Data Lake Store y recibe un error similar a `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, su suscripción podría no estar en la lista de permitidas para Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49bf8-130">If you register the Data Lake Store resource provider and receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="49bf8-131">Para habilitar la suscripción de Azure para la versión preliminar pública de Data Lake Store, siga las instrucciones que se encuentran en [Introducción a Azure Data Lake Store mediante Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="49bf8-131">To enable your Azure subscription for the Data Lake Store public preview, follow the instructions in [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="49bf8-132">Una cuenta de Data Lake Store se asocia con un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="49bf8-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="49bf8-133">Comience a crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="49bf8-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="49bf8-134">La salida debe ser parecida a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="49bf8-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="49bf8-135">Cree una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49bf8-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="49bf8-136">El nombre de cuenta que especifique solo debe contener letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="49bf8-136">The account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="49bf8-137">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="49bf8-137">You should see an output like the following:</span></span>

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

4. <span data-ttu-id="49bf8-138">El uso de Data Lake Store como almacenamiento predeterminado requiere especificar una ruta de acceso raíz en la que se copiarán los archivos específicos del clúster durante su creación.</span><span class="sxs-lookup"><span data-stu-id="49bf8-138">Using Data Lake Store as default storage requires you to specify a root path to which the cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="49bf8-139">Para crear una ruta de acceso raíz, que es **/clusters/hdiadlcluster** en el fragmento de código, use los cmdlets siguientes:</span><span class="sxs-lookup"><span data-stu-id="49bf8-139">To create a root path, which is **/clusters/hdiadlcluster** in the  snippet, use the following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="49bf8-140">Configuración de la autenticación para el acceso basado en roles al Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="49bf8-140">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="49bf8-141">Cada una de las suscripciones de Azure está asociada a una entidad de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49bf8-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="49bf8-142">Los usuarios y los servicios que acceden a los recursos de la suscripción Azure Portal o la API de Azure Resource Manager deben autenticarse primero en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49bf8-142">Users and services that access subscription resources by using the Azure portal or the Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="49bf8-143">Para conceder acceso a servicios y suscripciones de Azure, se les asigna el rol adecuado en un recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="49bf8-143">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span> <span data-ttu-id="49bf8-144">Para los servicios, una entidad de servicio identifica al servicio en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49bf8-144">For services, a service principal identifies the service in Azure AD.</span></span>

<span data-ttu-id="49bf8-145">En esta sección se muestra cómo conceder a un servicio de aplicación, como HDInsight, acceso a un recurso de Azure (la cuenta de Data Lake Store que creó anteriormente).</span><span class="sxs-lookup"><span data-stu-id="49bf8-145">This section illustrates how to grant an application service, such as HDInsight, access to an Azure resource (the Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="49bf8-146">La forma de hacerlo es crear una entidad de servicio para la aplicación y asignarla roles a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49bf8-146">You do so by creating a service principal for the application and assigning roles to it via PowerShell.</span></span>

<span data-ttu-id="49bf8-147">Para configurar la autenticación de Active Directory para Azure Data Lake, realice las tareas en las dos secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="49bf8-147">To set up Active Directory authentication for Azure Data Lake, perform the tasks in the following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="49bf8-148">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="49bf8-148">Create a self-signed certificate</span></span>
<span data-ttu-id="49bf8-149">Asegúrese de que tiene [Windows SDK](https://dev.windows.com/en-us/downloads) instalado antes de continuar con los pasos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="49bf8-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="49bf8-150">También debe crear un directorio, como *C:\mycertdir*, donde creará el certificado.</span><span class="sxs-lookup"><span data-stu-id="49bf8-150">You must have also created a directory, such as *C:\mycertdir*, where you create the certificate.</span></span>

1. <span data-ttu-id="49bf8-151">En la ventana de PowerShell, vaya a la ubicación donde instaló Windows SDK (normalmente, *C:\Archivos de programa (x86)\Windows Kits\10\bin\x86*) y use la utilidad [MakeCert][makecert] para crear un certificado autofirmado y una clave privada.</span><span class="sxs-lookup"><span data-stu-id="49bf8-151">From the PowerShell window, go to the location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="49bf8-152">Use los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="49bf8-152">Use the following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="49bf8-153">Se le pedirá que escriba la contraseña de la clave privada.</span><span class="sxs-lookup"><span data-stu-id="49bf8-153">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="49bf8-154">Después de que el comando se ejecute correctamente, debería ver los archivos **CertFile.cer** y **mykey.pvk** en el directorio de certificado que especificó.</span><span class="sxs-lookup"><span data-stu-id="49bf8-154">After the command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in the certificate directory that you specified.</span></span>
2. <span data-ttu-id="49bf8-155">Emplee la utilidad [Pvk2Pfx][pvk2pfx] para convertir los archivos .pvk y .cer que MakeCert creó en un archivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="49bf8-155">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="49bf8-156">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="49bf8-156">Run the following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="49bf8-157">Cuando se le pida, escriba la contraseña de la clave privada que especificó antes.</span><span class="sxs-lookup"><span data-stu-id="49bf8-157">When you are prompted, enter the private key password that you specified earlier.</span></span> <span data-ttu-id="49bf8-158">El valor especificado para el parámetro **-po** es la contraseña asociada al archivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="49bf8-158">The value you specify for the **-po** parameter is the password that's associated with the .pfx file.</span></span> <span data-ttu-id="49bf8-159">Cuando el comando se haya completado correctamente, debería ver un archivo **CertFile.pfx** en el directorio de certificado que especificó.</span><span class="sxs-lookup"><span data-stu-id="49bf8-159">After the command has been completed successfully, you should also see a **CertFile.pfx** in the certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="49bf8-160">Creación de una aplicación en Azure AD y una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="49bf8-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="49bf8-161">En esta sección, creará una entidad de servicio para una aplicación de Azure AD, asignará un rol a la entidad de servicio y la autenticará como la entidad de servicio proporcionando un certificado.</span><span class="sxs-lookup"><span data-stu-id="49bf8-161">In this section, you create a service principal for an Azure AD application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="49bf8-162">Para crear una aplicación en Azure AD, ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="49bf8-162">To create an application in Azure AD, run the following commands:</span></span>

1. <span data-ttu-id="49bf8-163">Pegue los siguientes cmdlets en la ventana de consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49bf8-163">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="49bf8-164">Asegúrese de que el valor especificado para la propiedad **- DisplayName** sea único.</span><span class="sxs-lookup"><span data-stu-id="49bf8-164">Make sure that the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="49bf8-165">Los valores de **-HomePage** e **-IdentiferUris** son valores de marcador de posición y no se comprueban.</span><span class="sxs-lookup"><span data-stu-id="49bf8-165">The values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="49bf8-166">Cree una entidad de servicio mediante el identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="49bf8-166">Create a service principal by using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="49bf8-167">Conceda a la entidad de servicio acceso a la raíz de Data Lake Store y a todas las carpetas de la ruta de acceso raíz que especificó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="49bf8-167">Grant the service principal access to the Data Lake Store root and all the folders in the root path that you specified earlier.</span></span> <span data-ttu-id="49bf8-168">Use los siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="49bf8-168">Use the following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-the-default-storage"></a><span data-ttu-id="49bf8-169">Creación de un clúster de HDInsight en Linux con Data Lake Store como almacenamiento predeterminado</span><span class="sxs-lookup"><span data-stu-id="49bf8-169">Create an HDInsight Linux cluster with Data Lake Store as the default storage</span></span>

<span data-ttu-id="49bf8-170">En esta sección, creará un clúster de Hadoop en HDInsight basado en Linux con Data Lake Store como almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="49bf8-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as the default storage.</span></span> <span data-ttu-id="49bf8-171">En esta versión, el clúster de HDInsight y Data Lake Store deben estar en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="49bf8-171">For this release, the HDInsight cluster and Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="49bf8-172">Recupere el identificador de inquilino de suscripción y almacénelo para usarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="49bf8-172">Retrieve the subscription tenant ID, and store it to use later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="49bf8-173">Cree el clúster de HDInsight mediante los cmdlets siguientes:</span><span class="sxs-lookup"><span data-stu-id="49bf8-173">Create the HDInsight cluster by using the following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="49bf8-174">Cuando el cmdlet se haya completado correctamente, debería ver una salida con la información del clúster.</span><span class="sxs-lookup"><span data-stu-id="49bf8-174">After the cmdlet has been successfully completed, you should see an output that lists the cluster details.</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-data-lake-store"></a><span data-ttu-id="49bf8-175">Ejecución de trabajos de prueba en el clúster de HDInsight para usar Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="49bf8-175">Run test jobs on the HDInsight cluster to use Data Lake Store</span></span>
<span data-ttu-id="49bf8-176">Después de configurar un clúster de HDInsight, puede ejecutar trabajos de prueba en él para garantizar que puede acceder a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49bf8-176">After you have configured an HDInsight cluster, you can run test jobs on it to ensure that it can access Data Lake Store.</span></span> <span data-ttu-id="49bf8-177">Para hacerlo, ejecute un trabajo de Hive de ejemplo para crear una tabla que usa los datos de ejemplo que ya están disponibles en Data Lake Store en *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="49bf8-177">To do so, run a sample Hive job to create a table that uses the sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="49bf8-178">En esta sección, realiza una conexión de Secure Shell (SSH) en el clúster de HDInsight en Linux que creó y luego ejecute una consulta de Hive de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="49bf8-178">In this section, you make a Secure Shell (SSH) connection into the HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="49bf8-179">Si usa un cliente Windows para realizar una conexión SSH en el clúster, consulte [Uso de SSH con clústeres de HDInsight desde PuTTY en Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="49bf8-179">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="49bf8-180">Si usa un cliente Linux para realizar una conexión SSH en el clúster, consulte [Uso de SSH con HDInsight (Hadoop) desde Bash en Windows 10, Linux, Unix u OS X](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="49bf8-180">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="49bf8-181">Después de haber realizado la conexión, inicie la interfaz de la línea de comandos (CLI) de Hive con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="49bf8-181">After you have made the connection, start the Hive command-line interface (CLI) by using the following command:</span></span>

        hive
2. <span data-ttu-id="49bf8-182">Use la CLI para especificar las siguientes instrucciones para crear una tabla nueva denominada **vehicles** con los datos de ejemplo de Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="49bf8-182">Use the CLI to enter the following statements to create a new table named **vehicles** by using the sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="49bf8-183">Debería ver el resultado de la consulta en la consola SSH.</span><span class="sxs-lookup"><span data-stu-id="49bf8-183">You should see the query output on the SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="49bf8-184">La ruta de acceso a los datos de ejemplo del comando CREATE TABLE anterior es `adl:///example/data/`, donde `adl:///` es la raíz de clúster.</span><span class="sxs-lookup"><span data-stu-id="49bf8-184">The path to the sample data in the preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is the cluster root.</span></span> <span data-ttu-id="49bf8-185">Siguiendo el ejemplo de la raíz de clúster especificada en este tutorial, el comando es `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="49bf8-185">Following the example of the cluster root that's specified in this tutorial, the command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="49bf8-186">Puede usar la alternativa más corta o proporcionar la ruta de acceso a la raíz de clúster completa.</span><span class="sxs-lookup"><span data-stu-id="49bf8-186">You can either use the shorter alternative or provide the complete path to the cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="49bf8-187">Acceso a Data Lake Store mediante comandos de HDFS</span><span class="sxs-lookup"><span data-stu-id="49bf8-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="49bf8-188">Después de configurar el clúster de HDInsight para que use Data Lake Store, puede usar los comandos de shell del sistema de archivos distribuido de hadoop (HDFS) para acceder al almacén.</span><span class="sxs-lookup"><span data-stu-id="49bf8-188">After you have configured the HDInsight cluster to use Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands to access the store.</span></span>

<span data-ttu-id="49bf8-189">En esta sección, realiza una conexión SSH en el clúster de HDInsight en Linux que creó y luego ejecuta los comandos de HDFS.</span><span class="sxs-lookup"><span data-stu-id="49bf8-189">In this section, you make an SSH connection into the HDInsight Linux cluster that you created, and then you run the HDFS commands.</span></span>

* <span data-ttu-id="49bf8-190">Si usa un cliente Windows para realizar una conexión SSH en el clúster, consulte [Uso de SSH con clústeres de HDInsight desde PuTTY en Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="49bf8-190">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="49bf8-191">Si usa un cliente Linux para realizar una conexión SSH en el clúster, consulte [Uso de SSH con HDInsight (Hadoop) desde Bash en Windows 10, Linux, Unix u OS X](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="49bf8-191">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="49bf8-192">Después de realizar la conexión, pasa a enumerar los archivos de Data Lake Store mediante el siguiente comando de sistema de archivos de HDFS.</span><span class="sxs-lookup"><span data-stu-id="49bf8-192">After you've made the connection, list the files in Data Lake Store by using the following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="49bf8-193">También puede usar el comando `hdfs dfs -put` para cargar algunos archivos en Data Lake Store y después usar `hdfs dfs -ls` para comprobar si los archivos se cargaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="49bf8-193">You can also use the `hdfs dfs -put` command to upload some files to Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="49bf8-194">Consulte también</span><span class="sxs-lookup"><span data-stu-id="49bf8-194">See also</span></span>
* [<span data-ttu-id="49bf8-195">Azure Portal: Creación de un clúster de HDInsight para usar Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="49bf8-195">Azure portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
