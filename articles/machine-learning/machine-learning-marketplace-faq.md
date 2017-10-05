---
title: "(obsoleto) Preguntas frecuentes: publicación y uso de aplicaciones de Machine Learning en Azure Marketplace | Microsoft Docs"
description: "(obsoleto) Preguntas frecuentes sobre la publicación de aplicaciones de Machine Learning en Azure Marketplace"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a><span data-ttu-id="eb19c-103">(obsoleto) Publicación y uso de aplicaciones de Machine Learning en Azure Marketplace: preguntas frecuentes</span><span class="sxs-lookup"><span data-stu-id="eb19c-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="eb19c-104">DataMarket y Data Services están en proceso de retirada, y las suscripciones existentes se retirarán y cancelarán a partir del 31 de marzo de 2017.</span><span class="sxs-lookup"><span data-stu-id="eb19c-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="eb19c-105">Como resultado, este artículo se ha quedado obsoleto.</span><span class="sxs-lookup"><span data-stu-id="eb19c-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="eb19c-106">Aún tiene la posibilidad de publicar sus experimentos de Machine Learning en la [Galería de Cortana Intelligence](https://gallery.cortanaintelligence.com/) en beneficio de la comunidad de la ciencia de datos.</span><span class="sxs-lookup"><span data-stu-id="eb19c-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="eb19c-107">Para obtener más información, consulte [Uso compartido y descubrimiento de soluciones en la Galería de Cortana Intelligence](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="eb19c-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="eb19c-108">Preguntas acerca del consumo en Marketplace</span><span class="sxs-lookup"><span data-stu-id="eb19c-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="eb19c-109">**1. Por qué obtengo el siguiente mensaje de error tras especificar una entrada para el servicio web:**</span><span class="sxs-lookup"><span data-stu-id="eb19c-109">**1. Why do I get the following error message after I enter input for the web service:**</span></span>

<span data-ttu-id="eb19c-110">**La solicitud ha ocasionado un tiempo de espera de back-end o un error de back-end. El equipo está investigando el problema. Lamentamos los inconvenientes. (500)**</span><span class="sxs-lookup"><span data-stu-id="eb19c-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span></span>

<span data-ttu-id="eb19c-111">Los parámetros de entrada no pueden ajustarse al formato requerido para el servicio web específico.</span><span class="sxs-lookup"><span data-stu-id="eb19c-111">Your input parameter(s) may not conform to the required format for the specific web service.</span></span> <span data-ttu-id="eb19c-112">Consulte el vínculo correspondiente de la documentación para encontrar el formato correcto de los parámetros de entrada y las limitaciones de este servicio web.</span><span class="sxs-lookup"><span data-stu-id="eb19c-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="eb19c-113">**2. Si copio el vínculo de la API del servicio web que aparece en la página "Explorar este conjunto de datos" y lo pego en otra ventana del explorador, ¿qué credenciales tengo que usar para obtener acceso a los resultados y cómo puedo verlos?**</span><span class="sxs-lookup"><span data-stu-id="eb19c-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span></span>

<span data-ttu-id="eb19c-114">Debe usar la cuenta de Marketplace como nombre de usuario y la clave de la cuenta principal como contraseña.</span><span class="sxs-lookup"><span data-stu-id="eb19c-114">You should use your Marketplace account as the username and the primary account key as the password.</span></span> <span data-ttu-id="eb19c-115">La clave de la cuenta principal se puede encontrar en la página **Explorar este conjunto de datos** en la descripción del servicio web (haga clic en el botón **Mostrar**).</span><span class="sxs-lookup"><span data-stu-id="eb19c-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span></span> <span data-ttu-id="eb19c-116">El resultado se puede mostrar en el explorador o estar disponible para descargarlo, en función de qué explorador use.</span><span class="sxs-lookup"><span data-stu-id="eb19c-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span></span>

<span data-ttu-id="eb19c-117">**3. ¿Por qué obtengo el siguiente mensaje de error tras especificar una entrada para el servicio web en la página "Explorar este conjunto de datos":**?</span><span class="sxs-lookup"><span data-stu-id="eb19c-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span></span> 

<span data-ttu-id="eb19c-118">**Se ha producido un error inesperado al procesar la solicitud. Vuelva a intentarlo.**</span><span class="sxs-lookup"><span data-stu-id="eb19c-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="eb19c-119">Uno o varios parámetros de entrada del servicio web pueden haber excedido el límite de longitud al consumir el servicio web en la página **Explorar este conjunto de datos** de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eb19c-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="eb19c-120">Los servicios pueden llamarse con una longitud de entrada mediante los métodos HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="eb19c-120">The services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="eb19c-121">Para obtener ejemplos, consulte [Soluciones de ejemplo con R en Aprendizaje automático y publicados en Marketplace](machine-learning-r-csharp-web-service-examples.md).</span><span class="sxs-lookup"><span data-stu-id="eb19c-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="eb19c-122">**4. ¿Por qué no veo nada en la pestaña "EXPLORADOR DE API" en el almacén en el Portal de Azure clásico?**</span><span class="sxs-lookup"><span data-stu-id="eb19c-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span></span> 

<span data-ttu-id="eb19c-123">Se trata de un problema conocido con el Portal de Azure clásico Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eb19c-123">This is a known issue with the Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="eb19c-124">El equipo está trabajando para resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="eb19c-124">The team is working to resolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="eb19c-125">Preguntas acerca de la publicación desde Aprendizaje automático de Azure en Marketplace</span><span class="sxs-lookup"><span data-stu-id="eb19c-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="eb19c-126">**1. ¿Por qué mis transacciones de logotipos o imágenes no se actualizan en mi servicio web?**</span><span class="sxs-lookup"><span data-stu-id="eb19c-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="eb19c-127">Los logotipos y las imágenes se almacenan en caché en el portal de publicación y la actualización del nuevo logotipo o de la nueva imagen en el portal puede tardar hasta 10 días en completarse.</span><span class="sxs-lookup"><span data-stu-id="eb19c-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span></span>

<span data-ttu-id="eb19c-128">**2. ¿Por qué aparece un error en la pestaña "Detalles" del servicio web de Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="eb19c-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="eb19c-129">Hay un problema conocido de Marketplace al conectarse a Aprendizaje automático de Azure para obtener detalles del servicio.</span><span class="sxs-lookup"><span data-stu-id="eb19c-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span></span> <span data-ttu-id="eb19c-130">El equipo está trabajando para resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="eb19c-130">The team is working to resolve this issue.</span></span>

<span data-ttu-id="eb19c-131">**3. ¿Por qué no funciona el código de ejemplo R en los servicios web de Aprendizaje automático de Azure para consumir los servicios web en Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="eb19c-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span></span>

<span data-ttu-id="eb19c-132">Los sistemas de autenticación son diferentes al conectarse a servicios web de Aprendizaje automático de Azure directamente y al conectarse a estos servicios web a través de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eb19c-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span></span> <span data-ttu-id="eb19c-133">Los servicios de Marketplace son servicios de OData y se les puede llamar con los métodos GET o POST.</span><span class="sxs-lookup"><span data-stu-id="eb19c-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="eb19c-134">**4. ¿Por qué los vínculos de soporte técnico de las ofertas del servicio web no se actualizan correctamente para algunas de mis ofertas?**</span><span class="sxs-lookup"><span data-stu-id="eb19c-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="eb19c-135">Los vínculos de soporte técnico son globales por publicador, no por oferta.</span><span class="sxs-lookup"><span data-stu-id="eb19c-135">The support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="eb19c-136">**5. ¿Cómo puedo publicar un servicio web con el modo de entrada por lotes en Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="eb19c-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="eb19c-137">El modo de entrada por lotes no se admite actualmente en los servicios web de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eb19c-137">The batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="eb19c-138">**6. ¿Con quién debo comunicarme para obtener ayuda si tengo preguntas sobre cómo convertirme en un publicador de datos o si tengo problemas durante la publicación?**</span><span class="sxs-lookup"><span data-stu-id="eb19c-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="eb19c-139">Póngase en contacto con el equipo de Azure Marketplace en <mailto:datamarketbd@microsoft.com> para más información.</span><span class="sxs-lookup"><span data-stu-id="eb19c-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

