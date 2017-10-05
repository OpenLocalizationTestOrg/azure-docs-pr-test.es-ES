---
title: "(obsoleto) Publicación de un servicio web Machine Learning en Azure Marketplace | Microsoft Docs"
description: "(obsoleto) Publicación de un servicio web Machine Learning en Azure Marketplace"
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
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a><span data-ttu-id="48ad0-103">(obsoleto) Publicación de un servicio web Machine Learning en Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="48ad0-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="48ad0-104">DataMarket y Data Services están en proceso de retirada, y las suscripciones existentes se retirarán y cancelarán a partir del 31 de marzo de 2017.</span><span class="sxs-lookup"><span data-stu-id="48ad0-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="48ad0-105">Como resultado, este artículo se ha quedado obsoleto.</span><span class="sxs-lookup"><span data-stu-id="48ad0-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="48ad0-106">Aún tiene la posibilidad de publicar sus experimentos de Machine Learning en la [Galería de Cortana Intelligence](https://gallery.cortanaintelligence.com/) en beneficio de la comunidad de la ciencia de datos.</span><span class="sxs-lookup"><span data-stu-id="48ad0-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="48ad0-107">Para obtener más información, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="48ad0-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="48ad0-108">Azure Marketplace ofrece la posibilidad de publicar servicios web de Aprendizaje automático de Azure como servicios gratuitos o de pago para su consumo por clientes externos.</span><span class="sxs-lookup"><span data-stu-id="48ad0-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="48ad0-109">Este artículo proporciona una introducción a ese proceso, junto con vínculos a directrices para comenzar.</span><span class="sxs-lookup"><span data-stu-id="48ad0-109">This article provides an overview of that process with links to guidelines to get you started.</span></span> <span data-ttu-id="48ad0-110">Mediante este proceso, puede poner a disposición de otros desarrolladores sus servicios web para que los consuman en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="48ad0-110">By using this process, you can make your web services available for other developers to consume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a><span data-ttu-id="48ad0-111">Introducción al proceso de publicación</span><span class="sxs-lookup"><span data-stu-id="48ad0-111">Overview of the publishing process</span></span>
<span data-ttu-id="48ad0-112">A continuación, se muestran los pasos para publicar un servicio web de Aprendizaje automático de Azure en Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="48ad0-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span></span>

1. <span data-ttu-id="48ad0-113">Crear y publicar un servicio de solicitud-respuesta (RRS) de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="48ad0-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="48ad0-114">Implementar el servicio en producción y obtener la información de extremo de OData y la clave de API</span><span class="sxs-lookup"><span data-stu-id="48ad0-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="48ad0-115">Usar la URL del servicio web publicado para publicar en [Azure Marketplace (DataMarket)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="48ad0-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="48ad0-116">Una vez enviada la oferta, se revisa y es necesario aprobarla antes de que los clientes puedan comenzar a comprarla.</span><span class="sxs-lookup"><span data-stu-id="48ad0-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span></span> <span data-ttu-id="48ad0-117">El proceso de publicación puede tardar varios días laborables.</span><span class="sxs-lookup"><span data-stu-id="48ad0-117">The publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="48ad0-118">Tutorial</span><span class="sxs-lookup"><span data-stu-id="48ad0-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="48ad0-119">Paso 1: crear y publicar un servicio de solicitud-respuesta (RRS) de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="48ad0-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="48ad0-120">Si no lo ha hecho todavía, consulte este [tutorial](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="48ad0-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a><span data-ttu-id="48ad0-121">Paso 2: implementar el servicio en producción y obtener la información de extremo de OData y la clave de API</span><span class="sxs-lookup"><span data-stu-id="48ad0-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span></span>
1. <span data-ttu-id="48ad0-122">En el [Portal de Azure clásico](http://manage.windowsazure.com), elija la opción **Aprendizaje automático** en la barra de navegación de la izquierda y, a continuación, elija el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="48ad0-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="48ad0-123">Haga clic en la pestaña **Servicios web** y, a continuación, seleccione el servicio web que desee publicar en Marketplace.</span><span class="sxs-lookup"><span data-stu-id="48ad0-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="48ad0-125">Elija el extremo que desea ubicar en Marketplace para su consumo.</span><span class="sxs-lookup"><span data-stu-id="48ad0-125">Select the endpoint you would like to have the marketplace consume.</span></span> <span data-ttu-id="48ad0-126">Si no ha creado ningún extremo adicional, puede elegir el extremo **predeterminado** .</span><span class="sxs-lookup"><span data-stu-id="48ad0-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span></span>
4. <span data-ttu-id="48ad0-127">Una vez que haya hecho clic en el extremo, podrá ver la **clave de API**.</span><span class="sxs-lookup"><span data-stu-id="48ad0-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span></span> <span data-ttu-id="48ad0-128">Necesitará esta información más adelante en el paso 3, por lo que se aconseja que la copie.</span><span class="sxs-lookup"><span data-stu-id="48ad0-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="48ad0-130">Haga clic en el método **SOLICITUD/RESPUESTA**. En este momento, no se admite la publicación de servicios de ejecución de lotes en Marketplace.</span><span class="sxs-lookup"><span data-stu-id="48ad0-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span></span> <span data-ttu-id="48ad0-131">Esto le llevará a la página de Ayuda de la API para el método de solicitud/respuesta.</span><span class="sxs-lookup"><span data-stu-id="48ad0-131">That will take you to the API help page for the Request/Response method.</span></span>
6. <span data-ttu-id="48ad0-132">Copie la **dirección de extremo de OData**, ya que necesitará esta información más adelante en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="48ad0-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="48ad0-134">Implementación del servicio en la producción.</span><span class="sxs-lookup"><span data-stu-id="48ad0-134">deploy the service into production.</span></span>

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a><span data-ttu-id="48ad0-135">Paso 3: usar la URL del servicio web publicado para realizar la publicación en Azure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="48ad0-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="48ad0-136">Acceda a [Azure Marketplace (DataMarket)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="48ad0-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="48ad0-137">Haga clic en el vínculo **Publicar** en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="48ad0-137">Click on the **Publish** link at the top of the page.</span></span> <span data-ttu-id="48ad0-138">Esto le llevará a [Portal de publicación de Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="48ad0-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="48ad0-139">Haga clic en la sección **Publicadores** para registrarse como publicador.</span><span class="sxs-lookup"><span data-stu-id="48ad0-139">Click on the **publishers** section to register as a publisher.</span></span>
4. <span data-ttu-id="48ad0-140">Cuando cree una nueva oferta, elija **Servicios de datos** y, a continuación, haga clic en **Crear un nuevo servicio de datos**.</span><span class="sxs-lookup"><span data-stu-id="48ad0-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="48ad0-142">En **Planes** , deberá proporcionar información sobre su oferta, junto con un plan de precios.</span><span class="sxs-lookup"><span data-stu-id="48ad0-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="48ad0-143">Decida si ofrecerá un servicio gratuito o de pago.</span><span class="sxs-lookup"><span data-stu-id="48ad0-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="48ad0-144">Para que le paguen, deberá proporcionar información de pago, por ejemplo, la cuenta bancaria y los datos fiscales.</span><span class="sxs-lookup"><span data-stu-id="48ad0-144">To get paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="48ad0-145">En **Marketing** , proporcione información acerca de la oferta, como el título y la descripción.</span><span class="sxs-lookup"><span data-stu-id="48ad0-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span></span>
7. <span data-ttu-id="48ad0-146">En **Precios** , puede establecer el precio de los planes para países específicos, o dejar que el sistema aplique automáticamente el precio de la oferta.</span><span class="sxs-lookup"><span data-stu-id="48ad0-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span></span>
8. <span data-ttu-id="48ad0-147">En la pestaña **Servicio de datos**, elija **Servicio web** como **Origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="48ad0-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="48ad0-149">Obtenga la clave de API y la dirección URL del servicio web en el Portal de Azure clásico, tal y como se explica en el paso 2 anterior.</span><span class="sxs-lookup"><span data-stu-id="48ad0-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="48ad0-150">En el cuadro de diálogo de configuración del servicio de datos de Marketplace, pegue la dirección de extremo de OData en el cuadro de texto **Dirección URL del servicio** .</span><span class="sxs-lookup"><span data-stu-id="48ad0-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span></span>
11. <span data-ttu-id="48ad0-151">En **Autenticación**, elija **Encabezado** como **Esquema de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="48ad0-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="48ad0-152">Escriba "Autorización" en **Nombre de encabezado**.</span><span class="sxs-lookup"><span data-stu-id="48ad0-152">Enter "Authorization" for the **Header Name**.</span></span>
    * <span data-ttu-id="48ad0-153">En **Valor de encabezado**, escriba "Portador" (sin las comillas), haga clic en la barra **Espacio** y, a continuación, pegue la clave de API.</span><span class="sxs-lookup"><span data-stu-id="48ad0-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span></span>
    * <span data-ttu-id="48ad0-154">Marque la casilla **Este servicio es OData** .</span><span class="sxs-lookup"><span data-stu-id="48ad0-154">Select the **This Service is OData** check box.</span></span>
    * <span data-ttu-id="48ad0-155">Haga clic en **Prueba de conexión** para probar la conexión.</span><span class="sxs-lookup"><span data-stu-id="48ad0-155">Click **Test Connection** to test the connection.</span></span>
12. <span data-ttu-id="48ad0-156">En **Categorías**, asegúrese de que **Machine Learning** esté seleccionado.</span><span class="sxs-lookup"><span data-stu-id="48ad0-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="48ad0-157">Cuando haya terminado de escribir todos los metadatos acerca de la oferta, haga clic en **Publicar** y, a continuación, haga clic en **Pasar a ensayo**.</span><span class="sxs-lookup"><span data-stu-id="48ad0-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span></span> <span data-ttu-id="48ad0-158">En este momento, se le notificarán los problemas restantes que deba corregir.</span><span class="sxs-lookup"><span data-stu-id="48ad0-158">At this point, you will be notified of any remaining issues that you need to fix.</span></span>
14. <span data-ttu-id="48ad0-159">Una vez que se haya asegurado de que no quedan problemas pendientes, haga clic en **Solicitar aprobación para pasar a producción**.</span><span class="sxs-lookup"><span data-stu-id="48ad0-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span></span> <span data-ttu-id="48ad0-160">El proceso de publicación puede tardar varios días laborables.</span><span class="sxs-lookup"><span data-stu-id="48ad0-160">The publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

