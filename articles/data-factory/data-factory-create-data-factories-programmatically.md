---
title: "Creación de canalizaciones de datos mediante el SDK de Azure .NET | Microsoft Docs"
description: "Conozca cómo puede crear, supervisar y administrar factorías de datos de Azure mediante programación con el SDK de Factoría de datos."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 9d9dac75321c5d4e079f49320d9b7c6f56e48754
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="56ca2-103">Creación, supervisión y administración de factorías de datos de Azure mediante el SDK de .NET de Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="56ca2-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="56ca2-104">Información general</span><span class="sxs-lookup"><span data-stu-id="56ca2-104">Overview</span></span>
<span data-ttu-id="56ca2-105">Puede crear, supervisar y administrar factorías de datos de Azure mediante programación con el SDK de .NET de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="56ca2-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="56ca2-106">Este artículo contiene un tutorial que puede seguir para crear una aplicación de consola .NET de ejemplo que crea y controla una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="56ca2-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="56ca2-107">Este artículo no abarca todas las API de .NET de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="56ca2-107">This article does not cover all the Data Factory .NET API.</span></span> <span data-ttu-id="56ca2-108">Para obtener documentación completa sobre la API de .NET para Data Factory, consulte la [referencia de API de .NET de Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="56ca2-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="56ca2-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="56ca2-109">Prerequisites</span></span>
* <span data-ttu-id="56ca2-110">Visual Studio 2012, 2013 o 2015</span><span class="sxs-lookup"><span data-stu-id="56ca2-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="56ca2-111">Descargue e instale el [SDK de .NET de Azure](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="56ca2-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="56ca2-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56ca2-112">Azure PowerShell.</span></span> <span data-ttu-id="56ca2-113">Siga las instrucciones del artículo [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) para instalar Azure PowerShell en su equipo.</span><span class="sxs-lookup"><span data-stu-id="56ca2-113">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="56ca2-114">Azure PowerShell se usa para crear una aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="56ca2-114">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="56ca2-115">Creación de una aplicación en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56ca2-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="56ca2-116">Cree una aplicación de Azure Active Directory, cree una entidad de servicio para dicha aplicación y asígnela al rol **Colaborador de Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="56ca2-116">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="56ca2-117">Inicie **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="56ca2-118">Ejecute el siguiente comando y escriba el nombre de usuario y la contraseña que utiliza para iniciar sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="56ca2-118">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="56ca2-119">Ejecute el siguiente comando para ver todas las suscripciones para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="56ca2-119">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="56ca2-120">Ejecute el comando siguiente para seleccionar la suscripción con la que desea trabajar.</span><span class="sxs-lookup"><span data-stu-id="56ca2-120">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="56ca2-121">Reemplace **&lt;NameOfAzureSubscription**&gt; por el nombre de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="56ca2-121">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="56ca2-122">Anote **SubscriptionId** y **TenantId** de la salida de este comando.</span><span class="sxs-lookup"><span data-stu-id="56ca2-122">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="56ca2-123">Cree un grupo de recursos de Azure con el nombre **ADFTutorialResourceGroup** ejecutando el siguiente comando en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56ca2-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="56ca2-124">Si el grupo de recursos ya existe, especifique si desea actualizarlo (Y) o mantenerlo como está (N).</span><span class="sxs-lookup"><span data-stu-id="56ca2-124">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="56ca2-125">Si usa un otro grupo de recursos, deberá usar su nombre en lugar de ADFTutorialResourceGroup en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="56ca2-125">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="56ca2-126">Cree una aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="56ca2-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="56ca2-127">Si aparece el siguiente error, especifique otra dirección URL distinta y vuelva a ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="56ca2-127">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="56ca2-128">Cree la entidad de servicio de AD.</span><span class="sxs-lookup"><span data-stu-id="56ca2-128">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="56ca2-129">Agregue la entidad de servicio al rol **Colaborador de Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="56ca2-129">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="56ca2-130">Obtenga el identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="56ca2-130">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="56ca2-131">Anote el identificador de aplicación (applicationID) de la salida.</span><span class="sxs-lookup"><span data-stu-id="56ca2-131">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="56ca2-132">Debe tener los cuatro valores siguientes de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="56ca2-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="56ca2-133">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="56ca2-133">Tenant ID</span></span>
* <span data-ttu-id="56ca2-134">Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="56ca2-134">Subscription ID</span></span>
* <span data-ttu-id="56ca2-135">Identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="56ca2-135">Application ID</span></span>
* <span data-ttu-id="56ca2-136">Contraseña (especificado en el primer comando)</span><span class="sxs-lookup"><span data-stu-id="56ca2-136">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="56ca2-137">Tutorial</span><span class="sxs-lookup"><span data-stu-id="56ca2-137">Walkthrough</span></span>
<span data-ttu-id="56ca2-138">En el tutorial, crea una factoría de datos con una canalización que contiene una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="56ca2-138">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="56ca2-139">Esta actividad copia los datos de una carpeta de Azure Blob Storage a otra carpeta de la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="56ca2-139">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span></span> 

<span data-ttu-id="56ca2-140">La actividad de copia realiza el movimiento de datos en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="56ca2-140">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="56ca2-141">La actividad funciona con un servicio disponible de forma global que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="56ca2-141">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="56ca2-142">Consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md) para obtener más información sobre la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="56ca2-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

1. <span data-ttu-id="56ca2-143">Con Visual Studio 2012, 2013 o 2015, cree una aplicación de consola .NET de C#.</span><span class="sxs-lookup"><span data-stu-id="56ca2-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="56ca2-144">Inicie **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="56ca2-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="56ca2-145">Haga clic en **Archivo**, seleccione **Nuevo** y, luego, haga clic en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-145">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="56ca2-146">Expanda **Plantillas** y seleccione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="56ca2-147">En este tutorial, se usa C# pero puede usar cualquier lenguaje .NET.</span><span class="sxs-lookup"><span data-stu-id="56ca2-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="56ca2-148">Seleccione **Aplicación de consola** en la lista de tipos de proyecto de la derecha.</span><span class="sxs-lookup"><span data-stu-id="56ca2-148">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="56ca2-149">Escriba **DataFactoryAPITestApp** en Nombre.</span><span class="sxs-lookup"><span data-stu-id="56ca2-149">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="56ca2-150">Seleccione **C:\ADFGetStarted** para Ubicación.</span><span class="sxs-lookup"><span data-stu-id="56ca2-150">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="56ca2-151">Haga clic en **Aceptar** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="56ca2-151">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="56ca2-152">Haga clic en **Herramientas**, seleccione **Administrador de paquetes de NuGet** y haga clic en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-152">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="56ca2-153">En la **Consola del Administrador de paquetes**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="56ca2-153">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="56ca2-154">Ejecute el comando siguiente para instalar el paquete de Data Factory: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="56ca2-154">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="56ca2-155">Ejecute el comando siguiente para instalar el paquete de Azure Active Directory (utilizará la API de Active Directory en el código): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="56ca2-155">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="56ca2-156">Reemplace el contenido del archivo **App.config** del proyecto por el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="56ca2-156">Replace the contents of **App.config** file in the project with the following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="56ca2-157">En el archivo App.Config, actualice los valores de **&lt;Id. de aplicación&gt;**, **&lt;Contraseña&gt;**, **&lt;Id. de suscripción&gt;** e **&lt;Id. de inquilino&gt;** por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="56ca2-157">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="56ca2-158">Agregue las siguientes instrucciones **using** al archivo **Program.cs** del proyecto.</span><span class="sxs-lookup"><span data-stu-id="56ca2-158">Add the following **using** statements to the **Program.cs** file in the project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="56ca2-159">Agregue el código siguiente que crea una instancia de la clase **DataPipelineManagementClient** al método **Main**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-159">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="56ca2-160">Este objeto se usa para crear una factoría de datos, un servicio vinculado, conjuntos de datos de entrada y salida, y una canalización.</span><span class="sxs-lookup"><span data-stu-id="56ca2-160">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="56ca2-161">También se usa para supervisar los segmentos de un conjunto de datos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="56ca2-161">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify the name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: the name of the data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="56ca2-162">Reemplace el valor de **resourcegroupname** por el nombre de su grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="56ca2-162">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span> <span data-ttu-id="56ca2-163">Puede crear un grupo de recursos con el cmdlet [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) .</span><span class="sxs-lookup"><span data-stu-id="56ca2-163">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="56ca2-164">Actualice el nombre de Data Factory (dataFactoryName) para que sea único.</span><span class="sxs-lookup"><span data-stu-id="56ca2-164">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="56ca2-165">El nombre de la factoría de datos debe ser único a nivel global.</span><span class="sxs-lookup"><span data-stu-id="56ca2-165">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="56ca2-166">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="56ca2-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="56ca2-167">Agregue el siguiente código que crea una **factoría de datos** en el método **Main**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-167">Add the following code that creates a **data factory** to the **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="56ca2-168">Agregue el siguiente código que crea un servicio vinculado de **Azure Storage** al método **Main**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-168">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="56ca2-169">Reemplace **storageaccountname** y **accountkey** por el nombre y la clave de su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="56ca2-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="56ca2-170">Agregue el siguiente código que crea **conjuntos de datos de entrada y salida** en el método **Main**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-170">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="56ca2-171">Tenga en cuenta que el valor de **FolderPath** para el blob de entrada está establecido en **adftutorial/**, donde **adftutorial** es el nombre del contenedor en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="56ca2-171">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="56ca2-172">Si este contenedor no existe en el almacenamiento de blobs de Azure, cree un contenedor con este nombre: **adftutorial** y cargue un archivo de texto al contenedor.</span><span class="sxs-lookup"><span data-stu-id="56ca2-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="56ca2-173">Tenga en cuenta que el valor de FolderPath para el blob de salida está establecido en: **adftutorial/apifactoryoutput/{Segmento}**, donde **Segmento** se calcula dinámicamente en función del valor de **SliceStart** (fecha y hora de inicio de cada segmento).</span><span class="sxs-lookup"><span data-stu-id="56ca2-173">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="56ca2-174">Agregue el siguiente código que **crea y activa una canalización** al método **Main**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-174">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="56ca2-175">Esta canalización tiene un elemento **CopyActivity** que toma **BlobSource** como origen y **BlobSink** como receptor.</span><span class="sxs-lookup"><span data-stu-id="56ca2-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="56ca2-176">La actividad de copia realiza el movimiento de datos en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="56ca2-176">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="56ca2-177">La actividad funciona con un servicio disponible de forma global que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="56ca2-177">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="56ca2-178">Consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md) para obtener más información sobre la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="56ca2-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="56ca2-179">Agregue el código siguiente al método **Main** para obtener el estado de un segmento de datos del conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="56ca2-179">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="56ca2-180">Solo se espera un segmento en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="56ca2-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="56ca2-181">**(Opcional)**: agregue el código siguiente para obtener detalles de ejecución de un segmento de datos en el método **Main**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-181">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="56ca2-182">Agregue el siguiente método auxiliar usado por el método **Main** a la clase **Program**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-182">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="56ca2-183">Este método abre un cuadro de diálogo que le permite proporcionar un **nombre de usuario** y una **contraseña** para iniciar sesión en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="56ca2-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="56ca2-184">En el Explorador de soluciones, expanda el proyecto **DataFactoryAPITestApp**, haga clic con el botón derecho en **Referencias** y después haga clic en **Agregar referencia**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-184">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="56ca2-185">Seleccione la casilla del ensamblado de `System.Configuration` y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="56ca2-186">Compile la aplicación de la consola.</span><span class="sxs-lookup"><span data-stu-id="56ca2-186">Build the console application.</span></span> <span data-ttu-id="56ca2-187">Haga clic en **Compilar** en el menú y en **Compilar solución**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-187">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="56ca2-188">Confirme que hay al menos un archivo en el contenedor de adftutorial del almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="56ca2-188">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="56ca2-189">En caso contrario, cree el archivo Emp.txt en el Bloc de notas con el siguiente contenido y cárguelo en el contenedor de adftutorial.</span><span class="sxs-lookup"><span data-stu-id="56ca2-189">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="56ca2-190">Para ejecutar el ejemplo haga clic en **Depurar** -> **Iniciar depuración** en el menú.</span><span class="sxs-lookup"><span data-stu-id="56ca2-190">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="56ca2-191">Cuando vea **Getting run details of a data slice**, espere unos minutos y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-191">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="56ca2-192">Use el Portal de Azure para comprobar que la factoría de datos **APITutorialFactory** se crea con los siguientes artefactos:</span><span class="sxs-lookup"><span data-stu-id="56ca2-192">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="56ca2-193">Servicio vinculado: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="56ca2-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="56ca2-194">Conjunto de datos: **DatasetBlobSource** y **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="56ca2-195">Canalización: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="56ca2-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="56ca2-196">Compruebe que se crea un archivo de salida en la carpeta **apifactoryoutput** del contenedor **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="56ca2-196">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="56ca2-197">Obtener una lista de segmentos de datos con errores</span><span class="sxs-lookup"><span data-stu-id="56ca2-197">Get a list of failed data slices</span></span> 

```csharp
// Parse the resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="56ca2-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56ca2-198">Next steps</span></span>
<span data-ttu-id="56ca2-199">Vea el ejemplo siguiente para crear una canalización mediante el SDK de .NET que copia datos de Azure Blob Storage a Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="56ca2-199">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span></span> 

- [<span data-ttu-id="56ca2-200">Crear una canalización para copiar datos de Blob Storage a SQL Database</span><span class="sxs-lookup"><span data-stu-id="56ca2-200">Create a pipeline to copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
