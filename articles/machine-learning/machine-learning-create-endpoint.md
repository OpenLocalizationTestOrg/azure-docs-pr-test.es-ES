---
title: "extremos de servicios Web de aaaCreating en el aprendizaje automático | Documentos de Microsoft"
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
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="0839c-103">Creación de extremos</span><span class="sxs-lookup"><span data-stu-id="0839c-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="0839c-104">En este tema se describe técnicas aplicables tooa **clásico** servicio Web de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="0839c-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="0839c-105">Al crear servicios Web que venden a los clientes tooyour hacia delante, deberá a tooprovide modelos entrenados tooeach cliente experimento toohello todavía vinculado desde qué hello Web se creó el servicio.</span><span class="sxs-lookup"><span data-stu-id="0839c-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="0839c-106">Además, las actualizaciones debe toohello experimento aplican selectivamente tooan extremo sin sobrescribir las personalizaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="0839c-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="0839c-107">tooaccomplish, aprendizaje automático de Azure permite toocreate varios puntos de conexión de un servicio Web implementado.</span><span class="sxs-lookup"><span data-stu-id="0839c-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="0839c-108">Cada extremo de servicio Web de hello independientemente está dirigido, limitada y administra.</span><span class="sxs-lookup"><span data-stu-id="0839c-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="0839c-109">Cada punto de conexión es una clave única de autorización y la dirección URL que puede distribuir a los clientes de tooyour.</span><span class="sxs-lookup"><span data-stu-id="0839c-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="0839c-110">Agregar servicio Web de los puntos de conexión tooa</span><span class="sxs-lookup"><span data-stu-id="0839c-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="0839c-111">Hay tres tooadd formas un tooa punto de conexión del servicio Web.</span><span class="sxs-lookup"><span data-stu-id="0839c-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="0839c-112">De manera programática</span><span class="sxs-lookup"><span data-stu-id="0839c-112">Programmatically</span></span>
* <span data-ttu-id="0839c-113">A través del portal de servicios Web de Azure Machine Learning Hola</span><span class="sxs-lookup"><span data-stu-id="0839c-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="0839c-114">Aunque Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="0839c-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="0839c-115">Una vez que se crea el extremo de hello, puede consumir a través de la API sincrónicas, lote API y las hojas de cálculo de excel.</span><span class="sxs-lookup"><span data-stu-id="0839c-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="0839c-116">Además tooadding los puntos de conexión a través de esta interfaz de usuario, también puede usar hello las API de administración de punto de conexión tooprogrammatically agregar puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="0839c-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="0839c-117">Si ha agregado los puntos de conexión adicionales toohello servicio Web, no se puede eliminar el punto de conexión de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0839c-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="0839c-118">Incorporación de un punto de conexión mediante programación</span><span class="sxs-lookup"><span data-stu-id="0839c-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="0839c-119">Puede agregar un servicio de punto de conexión tooyour Web mediante programación con hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0839c-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="0839c-120">Agregar un punto de conexión mediante el portal de servicios Web de Azure Machine Learning Hola</span><span class="sxs-lookup"><span data-stu-id="0839c-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="0839c-121">En estudio de aprendizaje automático, en la columna de navegación izquierdo de hello, haga clic en servicios Web.</span><span class="sxs-lookup"><span data-stu-id="0839c-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="0839c-122">En hello parte inferior del panel de servicio de hello Web, haga clic en **administrar puntos de conexión**.</span><span class="sxs-lookup"><span data-stu-id="0839c-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="0839c-123">portal de servicios Web de Azure Machine Learning Hola abrirá la página de los puntos de conexión de toohello de hello servicio Web.</span><span class="sxs-lookup"><span data-stu-id="0839c-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="0839c-124">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="0839c-124">Click **New**.</span></span>
4. <span data-ttu-id="0839c-125">Escriba un nombre y una descripción para el nuevo punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="0839c-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="0839c-126">Los nombres de los puntos de conexión deben tener 24 caracteres o menos y deben estar formados por letras en minúsculas o números.</span><span class="sxs-lookup"><span data-stu-id="0839c-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="0839c-127">Seleccione el nivel de registro de hello y si los datos de ejemplo está habilitado.</span><span class="sxs-lookup"><span data-stu-id="0839c-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="0839c-128">Para obtener más información sobre el registro, consulte [Habilitación del registro para los servicios web Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="0839c-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="0839c-129">Agregar un punto de conexión mediante Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="0839c-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="0839c-130">Inicie sesión en toohello [portal de Azure clásico](http://manage.windowsazure.com), haga clic en **aprendizaje automático** en la columna izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="0839c-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="0839c-131">Haga clic en el área de trabajo de Hola que contiene el servicio Web de hello en el que esté interesado.</span><span class="sxs-lookup"><span data-stu-id="0839c-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Navegue tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="0839c-133">Haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="0839c-133">Click **Web Services**.</span></span>
   
    ![Explorar los servicios de tooWeb](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="0839c-135">Haga clic en el servicio Web de hello está interesado en la lista de hello toosee de puntos de conexión disponibles.</span><span class="sxs-lookup"><span data-stu-id="0839c-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Navegue tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="0839c-137">En la parte inferior de Hola de página de hello, haga clic en **Agregar extremo**.</span><span class="sxs-lookup"><span data-stu-id="0839c-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="0839c-138">Escriba un nombre y una descripción, asegúrese de que no hay ningún otros puntos de conexión con el mismo nombre en este servicio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="0839c-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="0839c-139">Deje el nivel de limitación de hello con su valor predeterminado a menos que tenga requisitos especiales.</span><span class="sxs-lookup"><span data-stu-id="0839c-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="0839c-140">toolearn más acerca de la limitación, consulte [ajuste de escala en los extremos de API](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="0839c-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Crear extremo](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="0839c-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0839c-142">Next Steps</span></span>
<span data-ttu-id="0839c-143">[¿Cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="0839c-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

