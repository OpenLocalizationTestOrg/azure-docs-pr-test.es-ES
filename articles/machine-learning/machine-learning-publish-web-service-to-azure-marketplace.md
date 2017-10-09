---
title: "máquina de publicación de aaa(deprecated) tooAzure de servicio web Marketplace de aprendizaje | Documentos de Microsoft"
description: "(desusado) Cómo toopublish su toohello de servicio de Web de aprendizaje de máquina de Azure Marketplace de Azure"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="6bcb0-103">(desusado) Publicar el servicio Web de Azure Machine Learning toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6bcb0-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="6bcb0-104">DataMarket y Data Services están en proceso de retirada, y las suscripciones existentes se retirarán y cancelarán a partir del 31 de marzo de 2017.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="6bcb0-105">Como resultado, este artículo se ha quedado obsoleto.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="6bcb0-106">Como alternativa, puede publicar su toohello de experimentos de aprendizaje automático [Cortana Intelligence galería](https://gallery.cortanaintelligence.com/) para beneficio de Hola de comunidad de ciencia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="6bcb0-107">Para obtener más información, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="6bcb0-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="6bcb0-108">Hola Azure Marketplace permite Hola servicios web de aprendizaje automático de Azure de toopublish como pagados o liberar servicios para su uso por clientes externos.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="6bcb0-109">Este artículo proporciona información general de dicho proceso con vínculos tooguidelines tooget que se inició.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="6bcb0-110">Mediante el uso de este proceso, puede hacer que los servicios web disponibles para otro tooconsume a los desarrolladores en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="6bcb0-111">Información general del proceso de publicación de Hola</span><span class="sxs-lookup"><span data-stu-id="6bcb0-111">Overview of hello publishing process</span></span>
<span data-ttu-id="6bcb0-112">siguiente Hola es pasos de Hola para publicar un tooAzure de servicio web de aprendizaje automático de Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="6bcb0-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="6bcb0-113">Crear y publicar un servicio de solicitud-respuesta (RRS) de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="6bcb0-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="6bcb0-114">Implementar Hola servicio tooproduction y obtener información de extremo de OData y clave de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="6bcb0-115">Dirección URL de Hola de uso de hello publicado toopublish de servicio web demasiado[Azure Marketplace (mercado de datos)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="6bcb0-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="6bcb0-116">Una vez que se envía, se revisa su oferta y necesita toobe aprobada antes de sus clientes podrán compras.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="6bcb0-117">proceso de publicación de Hello puede tardar unos días laborables.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="6bcb0-118">Tutorial</span><span class="sxs-lookup"><span data-stu-id="6bcb0-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="6bcb0-119">Paso 1: crear y publicar un servicio de solicitud-respuesta (RRS) de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="6bcb0-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="6bcb0-120">Si no lo ha hecho todavía, consulte este [tutorial](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6bcb0-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="6bcb0-121">Paso 2: Implementar Hola servicio tooproduction y obtener información de extremo de OData y clave de API de Hola</span><span class="sxs-lookup"><span data-stu-id="6bcb0-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="6bcb0-122">De hello [Portal clásico de Azure](http://manage.windowsazure.com), seleccione hello **aprendizaje automático** opción de barra de navegación izquierda de Hola y seleccione el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="6bcb0-123">Haga clic en hello **servicios WEB** ficha y seleccione hello web servicio le gustaría toopublish toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="6bcb0-125">Seleccionar extremo de hello como toohave Hola marketplace consumiría.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="6bcb0-126">Si no ha creado ningún punto de conexión adicional, puede seleccionar hello **predeterminado** punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="6bcb0-127">Una vez que haya hecho clic en el extremo de hello, será capaz de toosee hello **clave de API**.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="6bcb0-128">Necesitará esta información más adelante en el paso 3, por lo que se aconseja que la copie.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="6bcb0-130">Haga clic en hello **solicitud/respuesta** toohello marketplace de servicios de método, en este momento no se admite publicar la ejecución por lotes.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="6bcb0-131">Esto le llevará página de Ayuda de toohello API de hello método de solicitud/respuesta.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="6bcb0-132">Hola copia **dirección de extremo de OData**, necesitará esta información más adelante en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="6bcb0-134">implementar el servicio de hello en producción.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="6bcb0-135">Paso 3: Dirección URL de Hola de uso de hello publica web servicio toopublish tooAzure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="6bcb0-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="6bcb0-136">Navegue demasiado[Azure Marketplace (mercado de datos)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="6bcb0-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="6bcb0-137">Haga clic en hello **publicar** vínculo situado en la parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="6bcb0-138">Esto le llevará toohello [Portal de publicación de Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="6bcb0-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="6bcb0-139">Haga clic en hello **publicadores** sección tooregister como un publicador.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="6bcb0-140">Cuando cree una nueva oferta, elija **Servicios de datos** y, a continuación, haga clic en **Crear un nuevo servicio de datos**.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="6bcb0-142">En **Planes** , deberá proporcionar información sobre su oferta, junto con un plan de precios.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="6bcb0-143">Decida si ofrecerá un servicio gratuito o de pago.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="6bcb0-144">tooget de pago, proporcionan información de pago como su información bancaria y de impuestos.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="6bcb0-145">En **Marketing** proporcionan información acerca de su oferta, como el título de hello y una descripción para su oferta.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="6bcb0-146">En **precios** puede establecer el precio de Hola para los planes para países específicos, o deje que el sistema de Hola "autoprice" su oferta.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="6bcb0-147">En hello **servicio de datos** , haga clic en **servicio Web** como hello **origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="6bcb0-149">Obtener hello web service URL y API de la clave de hello Portal clásico de Azure, tal como se describe en el paso 2 anterior.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="6bcb0-150">En el cuadro de diálogo de configuración de servicio de datos de Marketplace de hello pegue dirección del extremo de OData de hello en hello **dirección URL del servicio** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="6bcb0-151">Para **autenticación**, elija **encabezado** como hello **esquema de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="6bcb0-152">Escriba "Autorización" de hello **nombre de encabezado**.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="6bcb0-153">Para hello **valor del encabezado**, escriba "Portador" (sin las comillas de hello), haga clic en hello **espacio** barra y, a continuación, pegue la clave de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="6bcb0-154">Seleccione hello **este servicio es OData** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="6bcb0-155">Haga clic en **Probar conexión** conexión de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="6bcb0-156">En **Categorías**, asegúrese de que **Machine Learning** esté seleccionado.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="6bcb0-157">Cuando haya terminado de especificar todos Hola metadatos acerca de su oferta, haga clic en **publicar**y, a continuación, **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="6bcb0-158">En este momento, se le notificará de los problemas restantes que necesita toofix.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="6bcb0-159">Una vez se haya asegurado de finalización de todas las cuestiones pendientes de hello, haga clic en **solicitar aprobación toopush tooProduction**.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="6bcb0-160">proceso de publicación de Hello puede tardar unos días laborables.</span><span class="sxs-lookup"><span data-stu-id="6bcb0-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

