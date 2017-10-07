---
title: "aaaImplement conmutación por error de transmisión por secuencias con servicios multimedia de Azure | Documentos de Microsoft"
description: "Este tema se muestra cómo tooimplement un escenario de transmisión por secuencias de conmutación por error."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fc45d849-eb0d-4739-ae91-0ff648113445
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: ade0bace57f35ab3ed855d3a98f743e08da4f324
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-failover-streaming-with-azure-media-services"></a><span data-ttu-id="59a66-103">Implementación de streaming de conmutación por error con Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="59a66-103">Implement failover streaming with Azure Media Services</span></span>

<span data-ttu-id="59a66-104">Este tutorial se muestra cómo toocopy contenido (BLOB) de un activo a otro de redundancia de toohandle de orden de transmisión por secuencias a petición.</span><span class="sxs-lookup"><span data-stu-id="59a66-104">This walkthrough demonstrates how toocopy content (blobs) from one asset into another in order toohandle redundancy for on-demand streaming.</span></span> <span data-ttu-id="59a66-105">Este escenario es útil si desea tooset una red de entrega de contenido de Azure toofail través entre dos centros de datos, en el caso de una interrupción en un centro de datos.</span><span class="sxs-lookup"><span data-stu-id="59a66-105">This scenario is useful if you want tooset up Azure Content Delivery Network toofail over between two datacenters, in case of an outage in one datacenter.</span></span> <span data-ttu-id="59a66-106">Este tutorial usa Hola SDK de servicios multimedia de Azure, Hola API de REST de servicios multimedia de Azure y Hola Hola de toodemonstrate de SDK de almacenamiento de Azure siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="59a66-106">This walkthrough uses hello Azure Media Services SDK, hello Azure Media Services REST API, and hello Azure Storage SDK toodemonstrate hello following tasks:</span></span>

1. <span data-ttu-id="59a66-107">Configure una cuenta de Media Services en "Centro de datos A".</span><span class="sxs-lookup"><span data-stu-id="59a66-107">Set up a Media Services account in "Data Center A."</span></span>
2. <span data-ttu-id="59a66-108">Cargue un archivo secundario en un recurso de origen.</span><span class="sxs-lookup"><span data-stu-id="59a66-108">Upload a mezzanine file into a source asset.</span></span>
3. <span data-ttu-id="59a66-109">Codificar el activo de hello en archivos MP4 de velocidades de bits múltiples.</span><span class="sxs-lookup"><span data-stu-id="59a66-109">Encode hello asset into multi-bit rate MP4 files.</span></span> 
4. <span data-ttu-id="59a66-110">Cree un localizador de firma de acceso compartido de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="59a66-110">Create a read-only shared access signature locator.</span></span> <span data-ttu-id="59a66-111">Se trata de contenedor Hola origen activo toohave acceso de lectura toohello de cuenta de almacenamiento de Hola que está asociado a activos de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="59a66-111">This is for hello source asset toohave read access toohello container in hello storage account that is associated with hello source asset.</span></span>
5. <span data-ttu-id="59a66-112">Obtener el nombre de contenedor de Hola de activo de origen de hello del localizador de firma de acceso compartido de solo lectura de hello creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="59a66-112">Get hello container name of hello source asset from hello read-only shared access signature locator created in hello previous step.</span></span> <span data-ttu-id="59a66-113">Esto es necesario para la copia de blobs entre cuentas de almacenamiento (se explica más adelante en el tema de Hola.)</span><span class="sxs-lookup"><span data-stu-id="59a66-113">This is necessary for copying blobs between storage accounts (explained later in hello topic.)</span></span>
6. <span data-ttu-id="59a66-114">Crear un localizador de origen de los activos de Hola Hola codificación tarea creada.</span><span class="sxs-lookup"><span data-stu-id="59a66-114">Create an origin locator for hello asset that was created by hello encoding task.</span></span> 

<span data-ttu-id="59a66-115">A continuación, toohandle Hola conmutación por error:</span><span class="sxs-lookup"><span data-stu-id="59a66-115">Then, toohandle hello failover:</span></span>

1. <span data-ttu-id="59a66-116">Configure una cuenta de Media Services en "Centro de datos B".</span><span class="sxs-lookup"><span data-stu-id="59a66-116">Set up a Media Services account in "Data Center B."</span></span>
2. <span data-ttu-id="59a66-117">Crear un recurso vacío de destino en el destino de hello cuenta de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="59a66-117">Create a target empty asset in hello target Media Services account.</span></span>
3. <span data-ttu-id="59a66-118">Cree un localizador de firma de acceso compartido de escritura.</span><span class="sxs-lookup"><span data-stu-id="59a66-118">Create a write shared access signature locator.</span></span> <span data-ttu-id="59a66-119">Esto es para el contenedor de toohello de acceso de escritura toohave recurso vacío de destino hello en la cuenta de almacenamiento de destino de Hola que está asociado con el recurso de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="59a66-119">This is for hello target empty asset toohave write access toohello container in hello target storage account that is associated with hello target asset.</span></span>
4. <span data-ttu-id="59a66-120">Usar toocopy blobs (archivos de recursos) de hello SDK de almacenamiento de Azure entre la cuenta de almacenamiento de origen de hello en el "Centro de datos A" y la cuenta de almacenamiento de destino de hello en "B." Centro de datos"</span><span class="sxs-lookup"><span data-stu-id="59a66-120">Use hello Azure Storage SDK toocopy blobs (asset files) between hello source storage account in "Data Center A" and hello target storage account in "Data Center B."</span></span> <span data-ttu-id="59a66-121">Estas cuentas de almacenamiento están asociadas a los activos de Hola de interés.</span><span class="sxs-lookup"><span data-stu-id="59a66-121">These storage accounts are associated with hello assets of interest.</span></span>
5. <span data-ttu-id="59a66-122">Asociar objetos binarios (archivos de recursos) que estaban toohello copiada contenedor de blob de destino con el recurso de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="59a66-122">Associate blobs (asset files) that were copied toohello target blob container with hello target asset.</span></span> 
6. <span data-ttu-id="59a66-123">Crear un localizador de origen de los activos de Hola de "Centro de datos B" y especifique el Id. de localizador de Hola que fue generado para el recurso de hello en "Centro de datos A."</span><span class="sxs-lookup"><span data-stu-id="59a66-123">Create an origin locator for hello asset in "Data Center B", and specify hello locator ID that was generated for hello asset in "Data Center A."</span></span>

<span data-ttu-id="59a66-124">Esto deja Hola direcciones URL de streaming donde son rutas de acceso relativas de Hola de direcciones URL de Hola Hola igual (solo hello base direcciones URL son diferentes).</span><span class="sxs-lookup"><span data-stu-id="59a66-124">This gives you hello streaming URLs where hello relative paths of hello URLs are hello same (only hello base URLs are different).</span></span> 

<span data-ttu-id="59a66-125">A continuación, toohandle las interrupciones, puede crear una red de entrega de contenido sobre los localizadores de origen.</span><span class="sxs-lookup"><span data-stu-id="59a66-125">Then, toohandle any outages, you can create a Content Delivery Network on top of these origin locators.</span></span> 

<span data-ttu-id="59a66-126">Hola siguientes consideraciones se aplica:</span><span class="sxs-lookup"><span data-stu-id="59a66-126">hello following considerations apply:</span></span>

* <span data-ttu-id="59a66-127">versión actual de Hola de SDK de servicios multimedia no admite la generación mediante programación información de IAssetFile que asociaría un activo con archivos de recursos.</span><span class="sxs-lookup"><span data-stu-id="59a66-127">hello current version of Media Services SDK does not support programmatically generating IAssetFile information that would associate an asset with asset files.</span></span> <span data-ttu-id="59a66-128">En su lugar, utilice Hola API de REST de servicios multimedia de CreateFileInfos toodo esto.</span><span class="sxs-lookup"><span data-stu-id="59a66-128">Instead, use hello CreateFileInfos Media Services REST API toodo this.</span></span> 
* <span data-ttu-id="59a66-129">Recursos cifrados almacenados (AssetCreationOptions.StorageEncrypted) no se admiten para la replicación (porque la clave de cifrado de hello es diferente en las cuentas de servicios multimedia).</span><span class="sxs-lookup"><span data-stu-id="59a66-129">Storage encrypted assets (AssetCreationOptions.StorageEncrypted) are not supported for replication (because hello encryption key is different in both Media Services accounts).</span></span> 
* <span data-ttu-id="59a66-130">Si desea tootake aprovechar el empaquetado dinámico, asegúrese de hello origen desde el que desea que toostream el contenido está en hello **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="59a66-130">If you want tootake advantage of dynamic packaging, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>

> [!NOTE]
> <span data-ttu-id="59a66-131">Considere el uso de servicios multimedia de hello [herramienta replicador](http://replicator.codeplex.com/) como una alternativa tooimplementing una conmutación por error de transmisión por secuencias escenario manualmente.</span><span class="sxs-lookup"><span data-stu-id="59a66-131">Consider using hello Media Services [Replicator Tool](http://replicator.codeplex.com/) as an alternative tooimplementing a failover streaming scenario manually.</span></span> <span data-ttu-id="59a66-132">Esta herramienta permite a tooreplicate activos entre dos cuentas de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="59a66-132">This tool allows you tooreplicate assets across two Media Services accounts.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="59a66-133">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="59a66-133">Prerequisites</span></span>
* <span data-ttu-id="59a66-134">Dos cuentas de Media Services en una suscripción de Azure nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="59a66-134">Two Media Services accounts in a new or existing Azure subscription.</span></span> <span data-ttu-id="59a66-135">Vea [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="59a66-135">See [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="59a66-136">Sistema operativo: Windows 7, Windows 2008 R2 o Windows 8.</span><span class="sxs-lookup"><span data-stu-id="59a66-136">Operating system: Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="59a66-137">.NET Framework 4.5 o .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="59a66-137">.NET Framework 4.5 or .NET Framework 4.</span></span>
* <span data-ttu-id="59a66-138">Visual Studio 2010 SP1 o una versión posterior (Professional, Premium, Ultimate o Express).</span><span class="sxs-lookup"><span data-stu-id="59a66-138">Visual Studio 2010 SP1 or later version (Professional, Premium, Ultimate, or Express).</span></span>

## <a name="set-up-your-project"></a><span data-ttu-id="59a66-139">Configurar su proyecto</span><span class="sxs-lookup"><span data-stu-id="59a66-139">Set up your project</span></span>
<span data-ttu-id="59a66-140">En esta sección, va a crear y configurar un proyecto de aplicación de consola de C#.</span><span class="sxs-lookup"><span data-stu-id="59a66-140">In this section, you create and set up a C# Console Application project.</span></span>

1. <span data-ttu-id="59a66-141">Use Visual Studio toocreate una nueva solución que contiene el proyecto de aplicación de consola de C# de Hola.</span><span class="sxs-lookup"><span data-stu-id="59a66-141">Use Visual Studio toocreate a new solution that contains hello C# Console Application project.</span></span> <span data-ttu-id="59a66-142">Escriba **HandleRedundancyForOnDemandStreaming** para nombre de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="59a66-142">Enter **HandleRedundancyForOnDemandStreaming** for hello name, and then click **OK**.</span></span>
2. <span data-ttu-id="59a66-143">Crear hello **SupportFiles** carpeta Hola de mismo nivel como hello **HandleRedundancyForOnDemandStreaming.csproj** archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="59a66-143">Create hello **SupportFiles** folder on hello same level as hello **HandleRedundancyForOnDemandStreaming.csproj** project file.</span></span> <span data-ttu-id="59a66-144">En hello **SupportFiles** carpeta, crear hello **inicioarchivos** y **MP4Files** carpetas.</span><span class="sxs-lookup"><span data-stu-id="59a66-144">Under hello **SupportFiles** folder, create hello **OutputFiles** and **MP4Files** folders.</span></span> <span data-ttu-id="59a66-145">Copie un archivo. mp4 en hello **MP4Files** carpeta.</span><span class="sxs-lookup"><span data-stu-id="59a66-145">Copy an .mp4 file into hello **MP4Files** folder.</span></span> <span data-ttu-id="59a66-146">(En este ejemplo, Hola **BigBuckBunny.mp4** se utiliza el archivo.)</span><span class="sxs-lookup"><span data-stu-id="59a66-146">(In this example, hello **BigBuckBunny.mp4** file is used.)</span></span> 
3. <span data-ttu-id="59a66-147">Use **Nuget** tooadd referencias tooDLLs relacionados con los servicios de tooMedia.</span><span class="sxs-lookup"><span data-stu-id="59a66-147">Use **Nuget** tooadd references tooDLLs related tooMedia Services.</span></span> <span data-ttu-id="59a66-148">En el **menú principal de Visual Studio**, seleccione **HERRAMIENTAS** > **Library Package Manager (Administrador de paquetes de biblioteca)** > **Package Manager Console** (Consola del administrador de paquetes).</span><span class="sxs-lookup"><span data-stu-id="59a66-148">In **Visual Studio Main Menu**, select **TOOLS** > **Library Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="59a66-149">En la ventana de la consola de hello, escriba **windowsazure.mediaservices Install-Package**, y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="59a66-149">In hello console window, type **Install-Package windowsazure.mediaservices**, and press Enter.</span></span>
4. <span data-ttu-id="59a66-150">Agregue otras referencias que son necesarias para este proyecto: System.Configuration, System.Runtime.Serialization y System.Web.</span><span class="sxs-lookup"><span data-stu-id="59a66-150">Add other references that are required for this project: System.Configuration, System.Runtime.Serialization, and System.Web.</span></span>
5. <span data-ttu-id="59a66-151">Reemplace **con** las instrucciones que se agregaron toohello **Programs.cs** archivo de forma predeterminada con hello los siguiendo:</span><span class="sxs-lookup"><span data-stu-id="59a66-151">Replace **using** statements that were added toohello **Programs.cs** file by default with hello following ones:</span></span>
   
        using System;
        using System.Configuration;
        using System.Globalization;
        using System.IO;
        using System.Net;
        using System.Runtime.Serialization.Json;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using System.Web;
        using System.Xml;
        using System.Linq;
        using Microsoft.WindowsAzure;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using Microsoft.WindowsAzure.Storage.Auth;
6. <span data-ttu-id="59a66-152">Agregar hello **appSettings** sección toohello **.config** archivo y actualizar valores de hello basan en los servicios multimedia y almacenamiento de valores de clave y el nombres.</span><span class="sxs-lookup"><span data-stu-id="59a66-152">Add hello **appSettings** section toohello **.config** file, and update hello values based on your Media Services and Storage key and name values.</span></span> 
   
        <appSettings>
          <add key="MediaServicesAccountNameSource" value="Media-Services-Account-Name-Source"/>
          <add key="MediaServicesAccountKeySource" value="Media-Services-Account-Key-Source"/>
          <add key="MediaServicesStorageAccountNameSource" value="Media-Services-Storage-Account-Name-Source"/>
          <add key="MediaServicesStorageAccountKeySource" value="Media-Services-Storage-Account-Key-Source"/>
          <add key="MediaServicesAccountNameTarget" value="Media-Services-Account-Name-Target" />
          <add key="MediaServicesAccountKeyTarget" value=" Media-Services-Account-Key-Target" />
          <add key="MediaServicesStorageAccountNameTarget" value=" Media-Services-Storage-Account-Name-Target" />
          <add key="MediaServicesStorageAccountKeyTarget" value=" Media-Services-Storage-Account-Key-Target" />
        </appSettings>

## <a name="add-code-that-handles-redundancy-for-on-demand-streaming"></a><span data-ttu-id="59a66-153">Incorporación de código que controle la redundancia del streaming a petición</span><span class="sxs-lookup"><span data-stu-id="59a66-153">Add code that handles redundancy for on-demand streaming</span></span>
<span data-ttu-id="59a66-154">En esta sección, creará Hola capacidad toohandle de redundancia.</span><span class="sxs-lookup"><span data-stu-id="59a66-154">In this section, you create hello ability toohandle redundancy.</span></span>

1. <span data-ttu-id="59a66-155">Agregar Hola después de la clase de campos de nivel de clase toohello Program.</span><span class="sxs-lookup"><span data-stu-id="59a66-155">Add hello following class-level fields toohello Program class.</span></span>
       
        // Read values from hello App.config file.
        private static readonly string MediaServicesAccountNameSource = ConfigurationManager.AppSettings["MediaServicesAccountNameSource"];
        private static readonly string MediaServicesAccountKeySource = ConfigurationManager.AppSettings["MediaServicesAccountKeySource"];
        private static readonly string StorageNameSource = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameSource"];
        private static readonly string StorageKeySource = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeySource"];
        
        private static readonly string MediaServicesAccountNameTarget = ConfigurationManager.AppSettings["MediaServicesAccountNameTarget"];
        private static readonly string MediaServicesAccountKeyTarget = ConfigurationManager.AppSettings["MediaServicesAccountKeyTarget"];
        private static readonly string StorageNameTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameTarget"];
        private static readonly string StorageKeyTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeyTarget"];
        
        // Base support files path.  Update this field toopoint toohello base path  
        // for hello local support files folder that you create. 
        private static readonly string SupportFiles = Path.GetFullPath(@"../..\SupportFiles");
        
        // Paths toosupport files (within hello above base path). 
        private static readonly string SingleInputMp4Path = Path.GetFullPath(SupportFiles + @"\MP4Files\BigBuckBunny.mp4");
        private static readonly string OutputFilesFolder = Path.GetFullPath(SupportFiles + @"\OutputFiles");
        
        // Class-level field used tookeep a reference toohello service context.
        static private CloudMediaContext _contextSource = null;
        static private CloudMediaContext _contextTarget = null;
        static private MediaServicesCredentials _cachedCredentialsSource = null;
        static private MediaServicesCredentials _cachedCredentialsTarget = null;

2. <span data-ttu-id="59a66-156">Reemplace definición de método Main de hello predeterminado con hello sigue uno.</span><span class="sxs-lookup"><span data-stu-id="59a66-156">Replace hello default Main method definition with hello following one.</span></span> <span data-ttu-id="59a66-157">A continuación se llama a las definiciones de método desde Main.</span><span class="sxs-lookup"><span data-stu-id="59a66-157">Method definitions that are called from Main are defined below.</span></span>
        
        static void Main(string[] args)
        {
            _cachedCredentialsSource = new MediaServicesCredentials(
                            MediaServicesAccountNameSource,
                            MediaServicesAccountKeySource);
        
            _cachedCredentialsTarget = new MediaServicesCredentials(
                            MediaServicesAccountNameTarget,
                            MediaServicesAccountKeyTarget);
        
            // Get server context.    
            _contextSource = new CloudMediaContext(_cachedCredentialsSource);
            _contextTarget = new CloudMediaContext(_cachedCredentialsTarget);
        
            IAsset assetSingleFile = CreateAssetAndUploadSingleFile(_contextSource,
                                        AssetCreationOptions.None,
                                        SingleInputMp4Path);
        
            IJob job = CreateEncodingJob(_contextSource, assetSingleFile);
        
            if (job.State != JobState.Error)
            {
                IAsset sourceOutputAsset = job.OutputMediaAssets[0];
                // Get hello locator for Smooth Streaming
                var sourceOriginLocator = GetStreamingOriginLocator(_contextSource, sourceOutputAsset);
        
                Console.WriteLine("Locator Id: {0}", sourceOriginLocator.Id);
                
                // 1.Create a read-only SAS locator for hello source asset toohave read access toohello container in hello source Storage account (associated with hello source Media Services account)
                var readSasLocator = GetSasReadLocator(_contextSource, sourceOutputAsset);
        
                // 2.Get hello container name of hello source asset from hello read-only SAS locator created in hello previous step
                string containerName = (new Uri(readSasLocator.Path)).Segments[1];
        
                // 3.Create a target empty asset in hello target Media Services account
                var targetAsset = CreateTargetEmptyAsset(_contextTarget, containerName);
        
                // 4.Create a write SAS locator for hello target empty asset toohave write access toohello container in hello target Storage account (associated with hello target Media Services account)
                ILocator writeSasLocator = CreateSasWriteLocator(_contextTarget, targetAsset);
        
                // Get asset container name.
                string targetContainerName = (new Uri(writeSasLocator.Path)).Segments[1];
        
                // 5.Copy hello blobs in hello source container (source asset) toohello target container (target empty asset)
                CopyBlobsFromDifferentStorage(containerName, targetContainerName, StorageNameSource, StorageKeySource, StorageNameTarget, StorageKeyTarget);
        
                // 6.Use hello CreateFileInfos Media Services REST API tooautomatically generate all hello IAssetFile’s for hello target asset. 
                //      This API call is not supported in hello current Media Services SDK for .NET. 
                CreateFileInfosForAssetWithRest(_contextTarget, targetAsset, MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget);
        
                // Check if hello AssetFiles are now  associated with hello asset.
                Console.WriteLine("Asset files assocated with hello {0} asset:", targetAsset.Name);
                foreach (var af in targetAsset.AssetFiles)
                {
                    Console.WriteLine(af.Name);
                }
        
                // 7.Copy hello Origin locator of hello source asset toohello target asset by using hello same Id
                var replicatedLocatorPath = CreateOriginLocatorWithRest(_contextTarget,
                            MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget,
                            sourceOriginLocator.Id, targetAsset.Id);
        
                // Create a full URL toohello manifest file. Use this for playback
                // in streaming media clients. 
                string originalUrlForClientStreaming = sourceOriginLocator.Path + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Original Locator Path: {0}\n", originalUrlForClientStreaming);
        
                string replicatedUrlForClientStreaming = replicatedLocatorPath + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Replicated Locator Path: {0}", replicatedUrlForClientStreaming);
        
                readSasLocator.Delete();
                writeSasLocator.Delete();
        }

3. <span data-ttu-id="59a66-158">Hola siguiendo las definiciones de método se llama desde Main.</span><span class="sxs-lookup"><span data-stu-id="59a66-158">hello following method definitions are called from Main.</span></span>

    >[!NOTE]
    ><span data-ttu-id="59a66-159">Hay un límite de 1 000 000 directivas para diferentes directivas de Media Services (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="59a66-159">There is a limit of 1,000,000 policies for different Media Services policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="59a66-160">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días y acceso a permisos.</span><span class="sxs-lookup"><span data-stu-id="59a66-160">You should use hello same policy ID if you are always using hello same days and access permissions.</span></span> <span data-ttu-id="59a66-161">Por ejemplo, use hello mismo identificador para las directivas de localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="59a66-161">For example, use hello same ID for policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="59a66-162">Para más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies).</span><span class="sxs-lookup"><span data-stu-id="59a66-162">For more information, see [this topic](media-services-dotnet-manage-entities.md#limit-access-policies).</span></span>

        public static IAsset CreateAssetAndUploadSingleFile(CloudMediaContext context,
                                                        AssetCreationOptions assetCreationOptions,
                                                        string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
   
            var asset = context.Assets.Create(assetName, assetCreationOptions);
   
            Console.WriteLine("Asset name: " + asset.Name);
   
            var fileName = Path.GetFileName(singleFilePath);
   
            var assetFile = asset.AssetFiles.Create(fileName);
   
            Console.WriteLine("Created assetFile {0}", assetFile.Name);
   
            Console.WriteLine("Upload {0}", assetFile.Name);
   
            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);
   
            return asset;
        }
   
        public static IJob CreateEncodingJob(CloudMediaContext context, IAsset asset)
        {
            // Declare a new job.
            IJob job = context.Jobs.Create("My encoding job");
   
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName(context,
                                                    "Media Encoder Standard");
   
            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.ProtectedConfiguration);
   
            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
   
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is in hello clear (unencrypted). 
            var outputAssetName = "OutputAsset_" + Guid.NewGuid();
            task.OutputAssets.AddNew(outputAssetName,
                AssetCreationOptions.None);
   
            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);
   
            // Launch hello job.
            job.Submit();
   
            // Optionally log job details. This displays basic job details
            // toohello console and saves them tooa JobDetails-{JobId}.txt file 
            // in your output folder.
            LogJobDetails(context, job.Id);
   
            // Check job execution and wait for job toofinish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();
   
            // Get an updated job reference.
            job = GetJob(context, job.Id);
   
            // Since we hello output asset contains a set of Smooth Streaming files,
            // set hello .ism file toobe hello primary file
            if (job.State != JobState.Error)
                SetPrimaryFile(job.OutputMediaAssets[0]);
   
            return job;
        }
   
        public static ILocator GetStreamingOriginLocator(CloudMediaContext context, IAsset assetToStream)
        {
            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 
            IAssetFile manifestFile = GetPrimaryFile(assetToStream);
   
            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
   
            IAccessPolicy policy = context.AccessPolicies.Create("Streaming policy",
                TimeSpan.FromDays(30),
                AccessPermissions.Read);
   
            // Create a locator toohello streaming content on an origin. 
            ILocator originLocator = context.Locators.CreateLocator(LocatorType.OnDemandOrigin,
                assetToStream,
                policy,
                DateTime.UtcNow.AddMinutes(-5));
   
            // Return hello locator. 
            return originLocator;
        }
   
        public static ILocator GetSasReadLocator(CloudMediaContext context, IAsset asset)
        {
            IAccessPolicy accessPolicy = context.AccessPolicies.Create("File Download Policy",
                TimeSpan.FromDays(30), AccessPermissions.Read);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, accessPolicy);
   
            return sasLocator;
        }
   
        public static ILocator CreateSasWriteLocator(CloudMediaContext context, IAsset asset)
        {
   
            IAccessPolicy writePolicy = context.AccessPolicies.Create("Write Policy",
                TimeSpan.FromDays(30), AccessPermissions.Write);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, writePolicy);
   
            return sasLocator;
        }
   
        public static IAsset CreateTargetEmptyAsset(CloudMediaContext context, string containerName)
        {
            // Create a new asset.
            IAsset assetToBeProcessed = context.Assets.Create(containerName,
                AssetCreationOptions.None);
   
            return assetToBeProcessed;
        }
   
        public static void CreateFileInfosForAssetWithRest(CloudMediaContext context, IAsset asset, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget)
        {
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                CreateFileInfos(apiServer, acsToken, asset.Id);
            }
        }
   
        public static string CreateOriginLocatorWithRest(CloudMediaContext context, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget, string locatorIdToReplicate, string targetAssetId)
        {
            //Make sure we are not asking for a duplicate:
            var locator = context.Locators.Where(l => l.Id == locatorIdToReplicate).FirstOrDefault();
            if (locator != null)
                return "";
   
            string locatorNewPath = "";
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                var asset = context.Assets.Where(a => a.Id == targetAssetId).FirstOrDefault();
   
                // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
                var accessPolicy = context.AccessPolicies.Create("RestTest", TimeSpan.FromDays(100),
                                                                    AccessPermissions.Read);
                if (asset != null)
                {
                    string redirectedServiceUri = null;
   
                    var xmlResponse = CreateLocator(apiServer, out redirectedServiceUri, acsToken,
                                                                asset.Id, accessPolicy.Id,
                                                                (int)LocatorType.OnDemandOrigin,
                                                                DateTime.UtcNow.AddMinutes(-10), locatorIdToReplicate);
   
                    Console.WriteLine("Redirected to: " + redirectedServiceUri);
                    if (xmlResponse != null)
                    {
                        Console.WriteLine(String.Format("Locator Id: {0}",
                                                        xmlResponse.GetElementsByTagName("Id")[0].InnerText));
                        Console.WriteLine(String.Format("Locator Path: {0}",
                                xmlResponse.GetElementsByTagName("Path")[0].InnerText));

                        locatorNewPath = xmlResponse.GetElementsByTagName("Path")[0].InnerText;
                    }
                }
            }

            return locatorNewPath;
        }

        public static void SetPrimaryFile(IAsset asset)
        {

            var ismAssetFiles = asset.AssetFiles.ToList().
                        Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase))
                        .ToArray();

            if (ismAssetFiles.Count() != 1)
                throw new ArgumentException("hello asset should have only one, .ism file");

            ismAssetFiles.First().IsPrimary = true;
            ismAssetFiles.First().Update();
        }

        public static IAssetFile GetPrimaryFile(IAsset asset)
        {
            var theManifest =
                    from f in asset.AssetFiles
                    where f.Name.EndsWith(".ism")
                    select f;

            // Cast hello reference tooa true IAssetFile type. 
            IAssetFile manifestFile = theManifest.First();

            return manifestFile;
        }

        public static IAsset RefreshAsset(CloudMediaContext context, IAsset asset)
        {
            asset = context.Assets.Where(a => a.Id == asset.Id).FirstOrDefault();
            return asset;
        }

        public static void CopyBlobsFromDifferentStorage(string sourceContainerName, string targetContainerName,
                                            string srcAccountName, string srcAccountKey,
                                            string destAccountName, string destAccountKey)
        {
            var srcAccount = new CloudStorageAccount(new StorageCredentials(srcAccountName, srcAccountKey), true);
            var destAccount = new CloudStorageAccount(new StorageCredentials(destAccountName, destAccountKey), true);

            var cloudBlobClient = srcAccount.CreateCloudBlobClient();
            var targetBlobClient = destAccount.CreateCloudBlobClient();

            var sourceContainer = cloudBlobClient.GetContainerReference(sourceContainerName);
            var targetContainer = targetBlobClient.GetContainerReference(targetContainerName);
            targetContainer.CreateIfNotExists();

            string blobToken = sourceContainer.GetSharedAccessSignature(new SharedAccessBlobPolicy()
            {
                // Specify hello expiration time for hello signature.
                SharedAccessExpiryTime = DateTime.Now.AddDays(1),
                // Specify hello permissions granted by hello signature.
                Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read
            });

            foreach (var sourceBlob in sourceContainer.ListBlobs())
            {
                string fileName = (sourceBlob as ICloudBlob).Name;
                var sourceCloudBlob = sourceContainer.GetBlockBlobReference(fileName);
                sourceCloudBlob.FetchAttributes();

                if (sourceCloudBlob.Properties.Length > 0)
                {
                    // In Azure Media Services, hello files are stored as block blobs. 
                    // Page blobs are not supported by Azure Media Services.  
                    var destinationBlob = targetContainer.GetBlockBlobReference(fileName);
                    destinationBlob.StartCopyFromBlob(new Uri(sourceBlob.Uri.AbsoluteUri + blobToken));

                    while (true)
                    {
                        // hello StartCopyFromBlob is an async operation, 
                        // so we want toocheck if hello copy operation is completed before proceeding. 
                        // toodo that, we call FetchAttributes on hello blob and check hello CopyStatus. 
                        destinationBlob.FetchAttributes();
                        if (destinationBlob.CopyState.Status != CopyStatus.Pending)
                        {
                            break;
                        }
                        //It's still not completed. So wait for some time.
                        System.Threading.Thread.Sleep(1000);
                    }
                }

                Console.WriteLine(fileName);
            }

            Console.WriteLine("Done copying.");
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(CloudMediaContext context, string mediaProcessorName)
        {

            var processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        // This method is a handler for events that track job progress.   
        private static void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("********************");
                    Console.WriteLine("Job is finished.");
                    Console.WriteLine("Please wait while local tasks or downloads complete...");
                    Console.WriteLine("********************");
                    Console.WriteLine();
                    Console.WriteLine();
                    break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    Console.WriteLine("Please wait...\n");
                    break;
                case JobState.Canceled:
                case JobState.Error:
                    // Cast sender as a job.
                    IJob job = (IJob)sender;
                    // Display or log error details as needed.
                    LogJobStop(null, job.Id);
                    break;
                default:
                    break;
            }
        }

        private static void LogJobStop(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nThe job stopped due toocancellation or an error.");
            builder.AppendLine("***************************");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job State: " + job.State.ToString());
            builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
            // Log job errors if they exist.  
            if (job.State == JobState.Error)
            {
                builder.Append("Error Details: \n");
                foreach (ITask task in job.Tasks)
                {
                    foreach (ErrorDetail detail in task.ErrorDetails)
                    {
                        builder.AppendLine("  Task Id: " + task.Id);
                        builder.AppendLine("    Error Code: " + detail.Code);
                        builder.AppendLine("    Error Message: " + detail.Message + "\n");
                    }
                }
            }
            builder.AppendLine("***************************\n");
            // Write hello output tooa local file and toohello console. hello template 
            // for an error output file is:  JobStop-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        private static void LogJobDetails(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nJob ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job submitted (client UTC time): " + DateTime.UtcNow.ToString());

            // Write hello output tooa local file and toohello console. hello template 
            // for an error output file is:  JobDetails-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobDetails-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        // Replace ":" with "_" in Job id values so they can 
        // be used as log file names.  
        private static string JobIdAsFileName(string jobID)
        {
            return jobID.Replace(":", "_");
        }

        // Write method output toohello output files folder.
        private static void WriteToFile(string outFilePath, string fileContent)
        {
            StreamWriter sr = File.CreateText(outFilePath);
            sr.WriteLine(fileContent);
            sr.Close();
        }

        private static IJob GetJob(CloudMediaContext context, string jobId)
        {
            // Use a Linq select query tooget an updated 
            // reference by Id. 
            var jobInstance =
                from j in context.Jobs
                where j.Id == jobId
                select j;

            // Return hello job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }

        private static IAsset GetAsset(CloudMediaContext context, string assetId)
        {
            // Use a LINQ Select query tooget an asset.
            var assetInstance =
                from a in context.Assets
                where a.Id == assetId
                select a;

            // Reference hello asset as an IAsset.
            IAsset asset = assetInstance.FirstOrDefault();

            return asset;
        }

        public static void DeleteAllAssets(CloudMediaContext context)
        {
            // Loop through and delete all assets.
            foreach (IAsset asset in context.Assets)
            {
                DeleteLocatorsForAsset(context, asset);

                asset.Delete();
            }
        }

        public static void DeleteLocatorsForAsset(CloudMediaContext context, IAsset asset)
        {
            string assetId = asset.Id;
            var locators = from a in context.Locators
                            where a.AssetId == assetId
                            select a;
            foreach (var locator in locators)
            {
                Console.WriteLine("Deleting locator {0} for asset {1}", locator.Path, assetId);

                locator.Delete();
            }
        }

        public static void DeleteAccessPolicy(CloudMediaContext context, string existingPolicyId)
        {
            // toodelete a specific access policy, get a reference toohello policy.  
            // based on hello policy Id passed toohello method.
            var policyInstance =
                    from p in context.AccessPolicies
                    where p.Id == existingPolicyId
                    select p;

            IAccessPolicy policy = policyInstance.FirstOrDefault();

            policy.Delete();

        }

        //////////////////////////////////////////////////////
        /// hello following methods use REST calls.
        //////////////////////////////////////////////////////

        public static string GetAcsBearerToken(string clientId, string clientSecret, string scope, string accessControlServiceUri)
        {
            if (string.IsNullOrEmpty(clientId))
                throw new ArgumentNullException("clientId");

            if (string.IsNullOrEmpty(clientSecret))
                throw new ArgumentNullException("clientSecret");

            if (string.IsNullOrEmpty(scope))
            {
                scope = "urn:WindowsAzureMediaServices";
            }
            else if (!scope.ToLower().StartsWith("urn:"))
            {
                scope = "urn:" + scope;
            }

            if (string.IsNullOrEmpty(accessControlServiceUri))
            {
                accessControlServiceUri = "https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13";
            }
            else if (!accessControlServiceUri.ToLower().EndsWith("/v2/oauth2-13"))
            {
                accessControlServiceUri = accessControlServiceUri.TrimEnd('/') + "/v2/OAuth2-13";
            }

            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(accessControlServiceUri);
            request.Method = "POST";
            request.ContentType = "application/x-www-form-urlencoded";
            request.KeepAlive = true;
            string acsBearerToken = null;

            var requestBytes = Encoding.ASCII.GetBytes("grant_type=client_credentials&client_id=" +
                clientId + "&client_secret=" + HttpUtility.UrlEncode(clientSecret) +
                "&scope=" + HttpUtility.UrlEncode(scope));
            request.ContentLength = requestBytes.Length;

            var requestStream = request.GetRequestStream();
            requestStream.Write(requestBytes, 0, requestBytes.Length);
            requestStream.Close();

            var response = (HttpWebResponse)request.GetResponse();

            if (response.StatusCode == HttpStatusCode.OK)
            {
                using (Stream responseStream = response.GetResponseStream())
                {
                    using (StreamReader stream = new StreamReader(responseStream))
                    {
                        string responseString = stream.ReadToEnd();
                        var reader = JsonReaderWriterFactory.CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                            new XmlDictionaryReaderQuotas());

                        while (reader.Read())
                        {
                            if ((reader.Name == "access_token") && (reader.NodeType == XmlNodeType.Element))
                            {
                                if (reader.Read())
                                {
                                    acsBearerToken = reader.Value;
                                    break;
                                }
                            }
                        }
                    }
                }
            }

            return acsBearerToken;
        }

        public static XmlDocument CreateLocator(string mediaServicesApiServerUri,
                                                out string redirectedMediaServicesApiServerUri,
                                                string acsBearerToken, string assetId,
                                                string accessPolicyId, int locatorType,
                                                DateTime startTime, string locatorIdToReplicate = null,
                                                bool autoRedirect = true)
        {
            if (string.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (string.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (string.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");
            if (string.IsNullOrEmpty(accessPolicyId)) throw new ArgumentNullException("accessPolicyId");

            redirectedMediaServicesApiServerUri = null;
            XmlDocument xmlResponse = null;

            StringBuilder sb = new StringBuilder();
            sb.Append("{ \"AssetId\" : \"" + assetId + "\"");
            sb.Append(", \"AccessPolicyId\" : \"" + accessPolicyId + "\"");
            sb.Append(", \"Type\" : \"" + locatorType + "\"");
            if (startTime != DateTime.MinValue)
                sb.Append(", \"StartTime\" : \"" + startTime.ToString("G", CultureInfo.CreateSpecificCulture("en-us")) + "\"");
            if (!string.IsNullOrEmpty(locatorIdToReplicate))
                sb.Append(", \"Id\" : \"" + locatorIdToReplicate + "\"");
            sb.Append("}");

            string requestbody = sb.ToString();

            try
            {
                var request = GenerateRequest("POST", mediaServicesApiServerUri, "Locators",
                    null, acsBearerToken, requestbody);
                var response = (HttpWebResponse)request.GetResponse();

                switch (response.StatusCode)
                {
                    case HttpStatusCode.MovedPermanently:
                        //Recurse once with hello mediaServicesApiServerUri redirect Location:
                        if (autoRedirect)
                        {
                            redirectedMediaServicesApiServerUri = response.Headers["Location"];
                            string secondRedirection = null;
                            xmlResponse = CreateLocator(redirectedMediaServicesApiServerUri,
                                                        out secondRedirection, acsBearerToken,
                                                        assetId, accessPolicyId, locatorType,
                                                        startTime, locatorIdToReplicate, false);
                        }
                        else
                        {
                            Console.WriteLine("Redirection too{0} failed.",
                                mediaServicesApiServerUri);
                            return null;
                        }
                        break;
                    case HttpStatusCode.Created:
                        using (Stream responseStream = response.GetResponseStream())
                        {
                            using (StreamReader stream = new StreamReader(responseStream))
                            {
                                string responseString = stream.ReadToEnd();
                                var reader = JsonReaderWriterFactory.
                                    CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                                        new XmlDictionaryReaderQuotas());

                                xmlResponse = new XmlDocument();
                                reader.Read();
                                xmlResponse.LoadXml(reader.ReadInnerXml());
                            }
                        }
                        break;

                    default:
                        Console.WriteLine(response.StatusDescription);
                        break;
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }

            return xmlResponse;
        }

        public static void CreateFileInfos(string mediaServicesApiServerUri,
                                    string acsBearerToken,
                                    string assetId
                                    )
        {
            if (String.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (String.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (String.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");


            string id = assetId.Replace(":", "%");

            UriBuilder builder = new UriBuilder(mediaServicesApiServerUri);
            builder.Path = Path.Combine(builder.Path, "CreateFileInfos");
            builder.Query = String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId);

            try
            {
                var request = GenerateRequest("GET", mediaServicesApiServerUri, "CreateFileInfos",
                    String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId), acsBearerToken, null);

                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    if (response.StatusCode == HttpStatusCode.MovedPermanently)
                    {
                        string redirectedMediaServicesApiUrl = response.Headers["Location"];

                        CreateFileInfos(redirectedMediaServicesApiUrl, acsBearerToken, assetId);
                    }
                    else if ((response.StatusCode != HttpStatusCode.OK) &&
                        (response.StatusCode != HttpStatusCode.Accepted) &&
                        (response.StatusCode != HttpStatusCode.Created) &&
                        (response.StatusCode != HttpStatusCode.NoContent))
                    {
                        // TODO: Throw a more specific exception.
                        throw new Exception("Invalid response received ");
                    }
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }
        }

        private static HttpWebRequest GenerateRequest(string verb,
                                                        string mediaServicesApiServerUri,
                                                        string resourcePath, string query,
                                                        string acsBearerToken, string requestbody)
        {
            var uriBuilder = new UriBuilder(mediaServicesApiServerUri);
            uriBuilder.Path += resourcePath;
            if (query != null)
            {
                uriBuilder.Query = query;
            }
            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(uriBuilder.Uri);
            request.AllowAutoRedirect = false; //We manage our own redirects.
            request.Method = verb;

            if (resourcePath == "$metadata")
                request.MediaType = "application/xml";
            else
            {
                request.ContentType = "application/json;odata=verbose";
                request.Accept = "application/json;odata=verbose";
            }

            request.Headers.Add("DataServiceVersion", "3.0");
            request.Headers.Add("MaxDataServiceVersion", "3.0");
            request.Headers.Add("x-ms-version", "2.1");
            request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + acsBearerToken);

            if (requestbody != null)
            {
                var requestBytes = Encoding.ASCII.GetBytes(requestbody);
                request.ContentLength = requestBytes.Length;

                var requestStream = request.GetRequestStream();
                requestStream.Write(requestBytes, 0, requestBytes.Length);
                requestStream.Close();
            }
            else
            {
                request.ContentLength = 0;
            }
            return request;
        }

## <a name="next-steps"></a><span data-ttu-id="59a66-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59a66-163">Next steps</span></span>
<span data-ttu-id="59a66-164">Puede usar ahora un solicitudes de tooroute del Administrador de tráfico entre dos centros de datos de Hola y conmutación por error, por tanto, en el caso de los que las interrupciones.</span><span class="sxs-lookup"><span data-stu-id="59a66-164">You can now use a traffic manager tooroute requests between hello two datacenters, and thus fail over in case of any outages.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="59a66-165">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="59a66-165">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="59a66-166">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="59a66-166">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

