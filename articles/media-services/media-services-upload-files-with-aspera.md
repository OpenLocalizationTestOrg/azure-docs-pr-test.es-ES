---
title: archivos de aaaUpload en una cuenta de servicios multimedia de Azure con Aspera | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de carga de archivos en una cuenta de almacenamiento que está asociada con una cuenta de servicios multimedia mediante Hola ** Aspera Server en petición ** el servicio en Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="69d8f-103">Cargar archivos en una cuenta de servicios multimedia mediante Hola servicio Aspera Server On Demand en Azure</span><span class="sxs-lookup"><span data-stu-id="69d8f-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="69d8f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="69d8f-104">Overview</span></span>

<span data-ttu-id="69d8f-105">**Aspera** es un software de transferencia de archivos de alta velocidad.</span><span class="sxs-lookup"><span data-stu-id="69d8f-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="69d8f-106">**Aspera Server On Demand** para Azure permite la carga y descarga a alta velocidad de archivos de gran tamaño directamente en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="69d8f-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="69d8f-107">Para obtener información acerca de **Aspera On Demand**, vea hello [Aspera nube](http://cloud.asperasoft.com/) sitio.</span><span class="sxs-lookup"><span data-stu-id="69d8f-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="69d8f-108">**Aspera Server On Demand** de Azure está disponible para su compra de hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="69d8f-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="69d8f-109">En Ordenar toocomplete una compra de **Aspera Server On Demand** de Azure, inicie sesión en Azure Marketplace con su Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="69d8f-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="69d8f-110">Este tutorial le guiará por los pasos de Hola de carga de archivos en una cuenta de almacenamiento que está asociada con una cuenta de servicios multimedia mediante hello **Aspera Server On Demand** servicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="69d8f-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="69d8f-111">Puede encontrar un ejemplo que muestra cómo las funciones de Azure toouse a Aspera y servicios multimedia [aquí](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="69d8f-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="69d8f-112">Hay un límite toohello tamaño máximo admitido para el procesamiento con servicios multimedia de Azure procesadores multimedia (MP).</span><span class="sxs-lookup"><span data-stu-id="69d8f-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="69d8f-113">Vea [esto](media-services-quotas-and-limitations.md) tema para obtener más información acerca de la limitación de tamaño de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="69d8f-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="69d8f-114">Prerequisites</span></span> 

<span data-ttu-id="69d8f-115">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="69d8f-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="69d8f-116">Un Windows Live ID</span><span class="sxs-lookup"><span data-stu-id="69d8f-116">A Windows Live ID</span></span>
* <span data-ttu-id="69d8f-117">Una [cuenta de Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="69d8f-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="69d8f-118">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69d8f-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="69d8f-119">Una [cuenta de Azure Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="69d8f-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="69d8f-120">Compra de Aspera On Demand para Azure</span><span class="sxs-lookup"><span data-stu-id="69d8f-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="69d8f-121">Una vez que han iniciado sesión en Azure Marketplace, siga estos pasos básicos toocomplete la compra de Aspera On Demand para Azure.</span><span class="sxs-lookup"><span data-stu-id="69d8f-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="69d8f-122">Busque Aspera y seleccione "Server On Demand".</span><span class="sxs-lookup"><span data-stu-id="69d8f-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="69d8f-124">Revise los planes de suscripción de Hola y haga clic en "Inicio de sesión de seguridad"</span><span class="sxs-lookup"><span data-stu-id="69d8f-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="69d8f-126">Rellene los detalles de hello para el servidor en la suscripción a petición.</span><span class="sxs-lookup"><span data-stu-id="69d8f-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="69d8f-128">Haga clic en hello **tarifa** y seleccione el volumen mensual deseado en el panel de sub Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="69d8f-129">Hola **planear detalles** el panel, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="69d8f-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="69d8f-130">A continuación, en hello **elija el nivel de precios** del panel, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="69d8f-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="69d8f-132">Haga clic en **condiciones legales** tooview y acepte los términos legales de hello en el panel de sub Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="69d8f-133">Una vez que haya revisado condiciones legales de hello, haga clic en **compra**.</span><span class="sxs-lookup"><span data-stu-id="69d8f-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="69d8f-135">Complete la compra de hello haciendo clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="69d8f-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="69d8f-137">Hola panel Azure anunciará que está aprovisionando servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="69d8f-138">Una vez que se completó con el aprovisionamiento, puede encontrar nueva suscripción de hello mediante la búsqueda en los recursos de nombre de hello del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="69d8f-139">Una vez haya encontrado el servicio de hello, haga doble clic en él portal de administración de servicios de toolaunch Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="69d8f-141">Inicie el portal de administración de Aspera Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="69d8f-142">Una vez haya encontrado el nuevo servicio de Aspera, puede obtener el portal de administración de acceso toohello, haciendo clic en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="69d8f-143">Se abrirá un nuevo panel.</span><span class="sxs-lookup"><span data-stu-id="69d8f-143">A new panel will be launched.</span></span> <span data-ttu-id="69d8f-144">Desde dentro de dicho panel nuevo, deberá tooclick en hello **nombre de recurso** de su nuevo servicio.</span><span class="sxs-lookup"><span data-stu-id="69d8f-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="69d8f-145">En la siguiente captura de pantalla de hello, nombre de recurso de hello es 'AsperaTransferDemo'.</span><span class="sxs-lookup"><span data-stu-id="69d8f-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="69d8f-146">Cuando hace clic en el nombre del recurso de hello, se inicia otro panel.</span><span class="sxs-lookup"><span data-stu-id="69d8f-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="69d8f-147">En ese panel recién abierto, verá un vínculo "Manage" (Administrar).</span><span class="sxs-lookup"><span data-stu-id="69d8f-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="69d8f-148">Haga clic en hello portal de administración de "Administrar" vínculo toolaunch hello Aspera.</span><span class="sxs-lookup"><span data-stu-id="69d8f-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="69d8f-150">Haciendo clic en hello vínculo Administrar, aparecerá la página de registro de toohello, que es necesario tooaccess Hola servicio.</span><span class="sxs-lookup"><span data-stu-id="69d8f-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="69d8f-152">En este punto, debe tener acceso toohello Aspera service portal de administración, donde puede crear teclas de acceso, descargar licencias y los clientes de Aspera, ver el uso y obtener información acerca de las API de Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="69d8f-153">Hello captura de pantalla siguiente muestra hello acceso creación.</span><span class="sxs-lookup"><span data-stu-id="69d8f-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="69d8f-155">Hello captura de pantalla siguiente muestra uso Hola reporting interfaces en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="69d8f-157">Carga de archivos con Aspera</span><span class="sxs-lookup"><span data-stu-id="69d8f-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="69d8f-158">Descargue e instale el software de cliente de Hola Aspera:</span><span class="sxs-lookup"><span data-stu-id="69d8f-158">Download and install hello Aspera client software:</span></span>
    
    * [<span data-ttu-id="69d8f-159">Complemento del explorador</span><span class="sxs-lookup"><span data-stu-id="69d8f-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="69d8f-160">Cliente enriquecido</span><span class="sxs-lookup"><span data-stu-id="69d8f-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="69d8f-161">Realice su primera transferencia.</span><span class="sxs-lookup"><span data-stu-id="69d8f-161">Make your first transfer.</span></span> <span data-ttu-id="69d8f-162">En orden toouse hello Aspera cliente tootransfer con hello Aspera el servicio de transferencia, necesita toocomplete Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="69d8f-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="69d8f-163">Cree una clave de acceso, mediante el portal de Aspera Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="69d8f-164">Descarga, instalación y cliente de licencia hello Aspera (software puede encontrarse en el portal de hello Aspera).</span><span class="sxs-lookup"><span data-stu-id="69d8f-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="69d8f-165">Sírvase leer esta guía de cliente hello Aspera para obtener información de configuración.</span><span class="sxs-lookup"><span data-stu-id="69d8f-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="69d8f-166">Recuperar información de la cuenta de almacenamiento que está asociada a la cuenta de multimedia de Azure con hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="69d8f-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="69d8f-167">En concreto, del nombre y la clave y el nombre del contenedor de blob de almacenamiento de hello en toowhich desea tooplace su contenido.</span><span class="sxs-lookup"><span data-stu-id="69d8f-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="69d8f-168">información de almacenamiento de hello tooget desde el portal de hello: buscar la cuenta de almacenamiento, haga clic en las teclas de acceso de Hola y clave de hello y nombre de Hola de copia de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="69d8f-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="69d8f-169">nombre del contenedor de hello tooget: buscar la cuenta de almacenamiento, seleccione **Blobs**, seleccione nombre de hello del contenedor de hello desea tooupload Hola contenido en.</span><span class="sxs-lookup"><span data-stu-id="69d8f-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="69d8f-170">A continuación se muestra hello captura de pantalla de cliente de hello Aspera **Connection Manager** donde debe especificar el tipo de almacenamiento 'Azure' hello y credenciales, así como contenedor de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="69d8f-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="69d8f-172">Recursos</span><span class="sxs-lookup"><span data-stu-id="69d8f-172">Resources</span></span>

<span data-ttu-id="69d8f-173">Hola recursos siguientes se menciona en este artículo.</span><span class="sxs-lookup"><span data-stu-id="69d8f-173">hello following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="69d8f-174">Complemento del explorador de Connect</span><span class="sxs-lookup"><span data-stu-id="69d8f-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="69d8f-175">Guía de Connect</span><span class="sxs-lookup"><span data-stu-id="69d8f-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="69d8f-176">Cliente Aspera</span><span class="sxs-lookup"><span data-stu-id="69d8f-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="69d8f-177">Guía de cliente</span><span class="sxs-lookup"><span data-stu-id="69d8f-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="69d8f-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69d8f-178">Next steps</span></span>

<span data-ttu-id="69d8f-179">Ahora puede [copiar blobs de una cuenta de almacenamiento a una cuenta de AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="69d8f-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="69d8f-180">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="69d8f-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="69d8f-181">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="69d8f-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

