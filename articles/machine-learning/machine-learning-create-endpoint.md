---
title: "Creación de puntos de conexión de servicio web en Machine Learning | Microsoft Docs"
description: "Creación de puntos de conexión de servicio web en Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 9f83ffc9cf7dbe37c1ce9980fd7f5b9133fe78f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="e9b56-103">Creación de extremos</span><span class="sxs-lookup"><span data-stu-id="e9b56-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="e9b56-104">En este tema se describen técnicas que se aplican a un servicio web Machine Learning **clásico**.</span><span class="sxs-lookup"><span data-stu-id="e9b56-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="e9b56-105">Al crear servicios web que puede vender a sus clientes, necesitará proporcionar modelos entrenados para cada cliente que aún siga vinculado al experimento desde el que se creó el servicio web.</span><span class="sxs-lookup"><span data-stu-id="e9b56-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="e9b56-106">Además, las actualizaciones en el experimento pueden aplicarse de manera selectiva a un punto de conexión sin sobrescribir las personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="e9b56-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="e9b56-107">Para ello, Azure Machine Learning permite crear varios puntos de conexión para un servicio web implementado.</span><span class="sxs-lookup"><span data-stu-id="e9b56-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="e9b56-108">Cada punto de conexión del servicio web se administra, limita y dirige de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="e9b56-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="e9b56-109">Cada punto de conexión es una dirección URL única y clave de autorización que se puede distribuir a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="e9b56-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="e9b56-110">Incorporación de puntos de conexión al servicio web</span><span class="sxs-lookup"><span data-stu-id="e9b56-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="e9b56-111">Hay tres maneras de agregar un punto de conexión a un servicio web.</span><span class="sxs-lookup"><span data-stu-id="e9b56-111">There are three ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="e9b56-112">De manera programática</span><span class="sxs-lookup"><span data-stu-id="e9b56-112">Programmatically</span></span>
* <span data-ttu-id="e9b56-113">A través del portal de servicios web de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e9b56-113">Through the Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="e9b56-114">A través del Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="e9b56-114">Though the Azure classic portal</span></span>

<span data-ttu-id="e9b56-115">Una vez creado el extremo, puede consumirlo a través de API sincrónicas, API de lotes y hojas de cálculo de Excel.</span><span class="sxs-lookup"><span data-stu-id="e9b56-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="e9b56-116">Además de agregar extremos a través de esta interfaz de usuario, también puede usar las API de administración de extremos para agregar extremos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="e9b56-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="e9b56-117">Si ha agregado más puntos de conexión al servicio web, no podrá eliminar el predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e9b56-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="e9b56-118">Incorporación de un punto de conexión mediante programación</span><span class="sxs-lookup"><span data-stu-id="e9b56-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="e9b56-119">Puede agregar un punto de conexión al servicio web mediante programación utilizando el código de ejemplo [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="e9b56-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="e9b56-120">Incorporación de un punto de conexión mediante el portal de servicios web de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e9b56-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="e9b56-121">En Machine Learning Studio, en la columna de navegación izquierda, haga clic en Servicios web.</span><span class="sxs-lookup"><span data-stu-id="e9b56-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="e9b56-122">En la parte inferior del panel de servicios web, haga clic en **Manage endpoints**(Administrar puntos de conexión).</span><span class="sxs-lookup"><span data-stu-id="e9b56-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="e9b56-123">El portal de servicios web de Azure Machine Learning se abre en la página de puntos de conexión del servicio web.</span><span class="sxs-lookup"><span data-stu-id="e9b56-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="e9b56-124">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="e9b56-124">Click **New**.</span></span>
4. <span data-ttu-id="e9b56-125">Escriba un nombre y una descripción para el nuevo punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="e9b56-125">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="e9b56-126">Los nombres de los puntos de conexión deben tener 24 caracteres o menos y deben estar formados por letras en minúsculas o números.</span><span class="sxs-lookup"><span data-stu-id="e9b56-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="e9b56-127">Seleccione el nivel de registro y si los datos de ejemplo están habilitados.</span><span class="sxs-lookup"><span data-stu-id="e9b56-127">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="e9b56-128">Para obtener más información sobre el registro, consulte [Habilitación del registro para los servicios web Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="e9b56-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a><span data-ttu-id="e9b56-129">Configuración de puntos de conexión con el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="e9b56-129">Adding an endpoint using the Azure classic portal</span></span>
1. <span data-ttu-id="e9b56-130">Inicie sesión en el [Portal de Azure clásico](http://manage.windowsazure.com), haga clic en **Machine Learning** en la columna izquierda.</span><span class="sxs-lookup"><span data-stu-id="e9b56-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span></span> <span data-ttu-id="e9b56-131">Haga clic en el área de trabajo que contiene el servicio web en el que esté interesado.</span><span class="sxs-lookup"><span data-stu-id="e9b56-131">Click the workspace which contains the Web service in which you are interested.</span></span>
   
    ![Navegar a área de trabajo](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="e9b56-133">Haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="e9b56-133">Click **Web Services**.</span></span>
   
    ![Acceso a servicios web](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="e9b56-135">Haga clic en el servicio web en el que esté interesado para ver la lista de puntos de conexión disponibles.</span><span class="sxs-lookup"><span data-stu-id="e9b56-135">Click the Web service you're interested in to see the list of available endpoints.</span></span>
   
    ![Navegar a extremo](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="e9b56-137">Haga clic en **Agregar extremo**en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="e9b56-137">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="e9b56-138">Escriba un nombre y una descripción, asegúrese de que no hay ningún otro punto de conexión con el mismo nombre en este servicio web.</span><span class="sxs-lookup"><span data-stu-id="e9b56-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span></span> <span data-ttu-id="e9b56-139">Deje el nivel de limitación con su valor predeterminado, a menos que tenga requisitos especiales.</span><span class="sxs-lookup"><span data-stu-id="e9b56-139">Leave the throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="e9b56-140">Para obtener más información sobre las limitaciones, consulte el artículo sobre [escalado de puntos de conexión de API](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e9b56-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Crear extremo](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="e9b56-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e9b56-142">Next Steps</span></span>
<span data-ttu-id="e9b56-143">[Cómo consumir un servicio web Azure Machine Learning](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="e9b56-143">[How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

