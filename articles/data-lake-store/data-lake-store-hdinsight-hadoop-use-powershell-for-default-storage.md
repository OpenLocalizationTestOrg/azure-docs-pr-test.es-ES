---
title: "clústeres de HDInsight aaaCreate con almacén de Data Lake como almacenamiento predeterminado mediante PowerShell | Documentos de Microsoft"
description: "Utilice toocreate de PowerShell de Azure y clústeres de HDInsight con el almacén de Azure Data Lake"
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
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="e638f-103">Creación de clústeres de HDInsight con Data Lake Store como almacenamiento predeterminado mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="e638f-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e638f-104">Usar hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e638f-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="e638f-105">Uso de PowerShell (para el almacenamiento predeterminado)</span><span class="sxs-lookup"><span data-stu-id="e638f-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="e638f-106">Uso de PowerShell (para almacenamiento adicional)</span><span class="sxs-lookup"><span data-stu-id="e638f-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="e638f-107">Uso de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e638f-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="e638f-108">Obtenga información acerca de cómo clústeres toouse tooconfigure de PowerShell de Azure HDInsight de Azure con Azure almacén de Data Lake, como almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e638f-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="e638f-109">Para obtener instrucciones sobre la creación de un clúster de HDInsight con Azure Data Lake Store como almacenamiento adicional, consulte [Uso de Azure PowerShell para crear clústeres de HDInsight con Data Lake Store (como almacenamiento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e638f-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="e638f-110">Estas son algunas consideraciones importantes que deben tenerse en cuenta al usar HDInsight con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="e638f-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="e638f-111">clústeres de HDInsight de Hello opción toocreate con acceso tooData Lake almacén como almacenamiento predeterminado está disponible para HDInsight versión 3.5 y 3.6.</span><span class="sxs-lookup"><span data-stu-id="e638f-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="e638f-112">Hola opción toocreate clústeres de HDInsight con acceso tooData Lake almacén como almacenamiento predeterminado es *no está disponible* para los clústeres de HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="e638f-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="e638f-113">tooconfigure toowork de HDInsight con el almacén de Data Lake con PowerShell, siga las instrucciones de hello en las secciones siguientes cinco de Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e638f-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e638f-114">Prerequisites</span></span>
<span data-ttu-id="e638f-115">Antes de comenzar este tutorial, asegúrese de que se cumple Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="e638f-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="e638f-116">**Una suscripción de Azure**: vaya demasiado[evaluación gratuita de Azure obtener](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e638f-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e638f-117">**Azure PowerShell 1.0 o mayor**: vea [cómo tooinstall y configurar PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e638f-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e638f-118">**Kit de desarrollo de Software (SDK) de Windows**: tooinstall SDK de Windows, vaya demasiado[descarga y las herramientas para Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="e638f-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="e638f-119">Hola SDK es toocreate usa un certificado de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e638f-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="e638f-120">**Entidad de servicio de Azure Active Directory**: en este tutorial se describe cómo toocreate una entidad de servicio en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e638f-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e638f-121">Sin embargo, toocreate una entidad de servicio, debe ser un administrador de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e638f-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="e638f-122">Si es administrador, puede omitir este requisito previo y continuar con tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e638f-123">Solamente puede crear una entidad de servicio si es administrador de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e638f-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="e638f-124">Su administrador de Azure AD debe generar una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e638f-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="e638f-125">Hello entidad de servicio debe crearse con un certificado, como se describe en [crear una entidad de servicio con el certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="e638f-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="e638f-126">Crear una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="e638f-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="e638f-127">toocreate una cuenta de almacén de Data Lake Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e638f-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="e638f-128">Desde el escritorio, abra una ventana de PowerShell y, a continuación, escriba los siguientes fragmentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="e638f-129">Cuando esté toosign solicitada en Inicio de sesión como uno de los administradores de suscripciones de Hola o propietarios.</span><span class="sxs-lookup"><span data-stu-id="e638f-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="e638f-130">Si registrar proveedor de recursos de almacén de Data Lake hello y recibe un mensaje de error similar demasiado`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, su suscripción no estén en la lista blanca para almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e638f-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="e638f-131">tooenable su suscripción de Azure para preview pública de almacén de Data Lake de hello, siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake utilizando Hola portal de Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e638f-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="e638f-132">Una cuenta de Data Lake Store se asocia con un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e638f-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="e638f-133">Comience a crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e638f-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="e638f-134">La salida debe ser parecida a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="e638f-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="e638f-135">Cree una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e638f-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="e638f-136">cuenta de Hello nombre que especifique debe contener solo letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="e638f-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="e638f-137">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e638f-137">You should see an output like hello following:</span></span>

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

4. <span data-ttu-id="e638f-138">El uso de almacén de Data Lake como almacenamiento predeterminado requiere toospecify que una ruta de acceso los raíz toowhich Hola específicos para clúster archivos se copian durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="e638f-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="e638f-139">una ruta de acceso raíz, que es toocreate **/clústeres/hdiadlcluster** en el fragmento de código de hello, usar hello siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="e638f-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="e638f-140">Configure la autenticación para basada en roles acceder tooData Lake almacén</span><span class="sxs-lookup"><span data-stu-id="e638f-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="e638f-141">Cada una de las suscripciones de Azure está asociada a una entidad de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e638f-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="e638f-142">Los usuarios y servicios que acceder a los recursos de suscripción mediante el uso de Hola portal de Azure u Hola API del Administrador de recursos de Azure deben autenticarse primero con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e638f-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="e638f-143">Se concede acceso tooAzure suscripciones y servicios mediante la asignación de rol adecuado de hello en un recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="e638f-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="e638f-144">Servicios, una entidad de servicio identifica el servicio de hello en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e638f-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="e638f-145">Esta sección muestra cómo service toogrant una aplicación, por ejemplo, HDInsight, tooan de acceso a recursos de Azure (Hola cuenta de almacén de Data Lake que creó anteriormente).</span><span class="sxs-lookup"><span data-stu-id="e638f-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="e638f-146">La forma de hacerlo es mediante la creación de un servicio principal para la aplicación hello y asignación de roles tooit a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e638f-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="e638f-147">tooset la autenticación de Active Directory para Azure Data Lake, realizar tareas de Hola Hola siguientes dos secciones.</span><span class="sxs-lookup"><span data-stu-id="e638f-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="e638f-148">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="e638f-148">Create a self-signed certificate</span></span>
<span data-ttu-id="e638f-149">Asegúrese de que tiene [Windows SDK](https://dev.windows.com/en-us/downloads) instalado antes de continuar con hello pasos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="e638f-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="e638f-150">Debe también ha creado un directorio, como *C:\mycertdir*, donde crear certificado Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="e638f-151">Desde la ventana de PowerShell de hello, vaya ubicación toohello donde se instaló el SDK de Windows (normalmente, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) y usar hello [MakeCert] [ makecert] toocreate utilidad un certificado autofirmado y una clave privada.</span><span class="sxs-lookup"><span data-stu-id="e638f-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="e638f-152">Usar hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e638f-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="e638f-153">Es posible que la contraseña de clave privada tooenter solicitadas Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="e638f-154">Después de que el comando de Hola se ejecuta correctamente, debería ver **CertFile.cer** y **mykey.pvk** en directorio de certificado de Hola que especificó.</span><span class="sxs-lookup"><span data-stu-id="e638f-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="e638f-155">Hola de uso [Pvk2Pfx] [ pvk2pfx] utilidad tooconvert Hola .pvk y .cer archivos archivo .pfx MakeCert tooa creado.</span><span class="sxs-lookup"><span data-stu-id="e638f-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="e638f-156">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e638f-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="e638f-157">Cuando se le pida, escriba Hola contraseña de clave privada que especificó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e638f-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="e638f-158">Hola valor especificado en hello **-po** parámetro es la contraseña de Hola que esté asociada con el archivo .pfx de hello.</span><span class="sxs-lookup"><span data-stu-id="e638f-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="e638f-159">Una vez se ha completado correctamente el comando hello, también debería observar una **CertFile.pfx** en directorio de certificado de Hola que especificó.</span><span class="sxs-lookup"><span data-stu-id="e638f-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="e638f-160">Creación de una aplicación en Azure AD y una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="e638f-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="e638f-161">En esta sección, cree a una entidad de servicio para una aplicación de Azure AD, asignar a una entidad de servicio de rol toohello y autenticarse como entidad de servicio de hello proporcionando un certificado.</span><span class="sxs-lookup"><span data-stu-id="e638f-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="e638f-162">toocreate una aplicación en Azure AD, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e638f-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="e638f-163">Pegue Hola siguientes cmdlets en la ventana de consola de PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="e638f-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="e638f-164">Asegúrese de que ese valor de Hola que especifique para hello **- DisplayName** propiedad es única.</span><span class="sxs-lookup"><span data-stu-id="e638f-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="e638f-165">Hola valores para **- página principal** y **- IdentiferUris** son valores de marcador de posición y no se comprueban.</span><span class="sxs-lookup"><span data-stu-id="e638f-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="e638f-166">Crear a una entidad de servicio mediante el uso de Id. de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="e638f-167">Conceda raíz del almacén de Data Lake de toohello de hello servicio acceso principal y todas las carpetas de hello en la ruta de acceso raíz de Hola que especificó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e638f-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="e638f-168">Usar hello siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="e638f-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="e638f-169">Crear un clúster de HDInsight Linux con el almacén de Data Lake como almacenamiento predeterminado de Hola</span><span class="sxs-lookup"><span data-stu-id="e638f-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="e638f-170">En esta sección, creará un clúster de HDInsight Hadoop Linux con el almacén de Data Lake como almacenamiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="e638f-171">En esta versión, Hola clúster de HDInsight y almacén de Data Lake debe ser Hola misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="e638f-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="e638f-172">Recuperar el Id. de inquilino de suscripción de Hola y almacenarlo toouse más tarde.</span><span class="sxs-lookup"><span data-stu-id="e638f-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="e638f-173">Crear el clúster de HDInsight de hello mediante Hola siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="e638f-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
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

    <span data-ttu-id="e638f-174">Después de hello cmdlet se ha completado correctamente, debería ver una salida que muestra detalles del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="e638f-175">Ejecutar trabajos de prueba en toouse de clúster de HDInsight de hello almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="e638f-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="e638f-176">Después de haber configurado un clúster de HDInsight, puede ejecutar trabajos de prueba en el mismo tooensure que puede tener acceso a almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e638f-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="e638f-177">toodo por lo tanto, ejecute un toocreate de trabajo de Hive de ejemplo una tabla que usa datos de ejemplo de Hola que ya está disponibles en el almacén de Data Lake en  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="e638f-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="e638f-178">En esta sección, se realiza una conexión de Secure Shell (SSH) en hello clúster de HDInsight Linux que creó y, a continuación, ejecutar una consulta de Hive de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e638f-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="e638f-179">Si usas un toomake de cliente de Windows una conexión SSH en el clúster hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e638f-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="e638f-180">Si usas un toomake de cliente de Linux una conexión SSH en el clúster hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e638f-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="e638f-181">Después de realizar la conexión de hello, iniciar la interfaz de línea de comandos de hello Hive (CLI) mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e638f-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="e638f-182">Use Hola CLI tooenter Hola siguiendo las instrucciones toocreate una nueva tabla denominada **vehículos** mediante el uso de datos de ejemplo de Hola en almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="e638f-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="e638f-183">Debería ver el resultado de la consulta de hello en la consola de SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e638f-184">Hola datos de ejemplo de ruta de acceso toohello Hola anterior comando CREATE TABLE están `adl:///example/data/`, donde `adl:///` es Hola clúster raíz.</span><span class="sxs-lookup"><span data-stu-id="e638f-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="e638f-185">Después de ejemplo de Hola de raíz de clúster de Hola que se especifica en este tutorial, el comando de hello es `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="e638f-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="e638f-186">Puede usar alternativa más corto de Hola o proporcionar Hola ruta de acceso completa toohello clúster raíz.</span><span class="sxs-lookup"><span data-stu-id="e638f-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="e638f-187">Acceso a Data Lake Store mediante comandos de HDFS</span><span class="sxs-lookup"><span data-stu-id="e638f-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="e638f-188">Después de haber configurado el almacén de hello HDInsight clúster toouse Data Lake, puede usar almacén de sistema de archivos distribuido de Hadoop (HDFS) shell comandos tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="e638f-189">En esta sección, se realiza una conexión SSH en hello clúster de HDInsight Linux que ha creado y, a continuación, ejecutar comandos HDFS Hola.</span><span class="sxs-lookup"><span data-stu-id="e638f-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="e638f-190">Si usas un toomake de cliente de Windows una conexión SSH en el clúster hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e638f-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="e638f-191">Si usas un toomake de cliente de Linux una conexión SSH en el clúster hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e638f-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="e638f-192">Una vez que haya realizado la conexión de hello, enumerar archivos de hello en el almacén de Data Lake mediante Hola siguiente comando de sistema de archivo HDFS.</span><span class="sxs-lookup"><span data-stu-id="e638f-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="e638f-193">También puede usar hello `hdfs dfs -put` comando tooupload un almacén de archivos tooData Lake y, a continuación, usar `hdfs dfs -ls` tooverify si los archivos de saludo se cargaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="e638f-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="e638f-194">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e638f-194">See also</span></span>
* [<span data-ttu-id="e638f-195">Portal de Azure: crear un toouse de clúster de HDInsight almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="e638f-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
