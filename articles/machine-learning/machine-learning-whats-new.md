---
title: Novedades de Azure Machine Learning | Microsoft Docs
description: "Nuevas características disponibles en Aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: ddc716ed-2615-4806-bf27-6c9a5662a7f2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 551b977b90612ddbfa1514a9c2358ebf8179c385
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-azure-machine-learning"></a><span data-ttu-id="25a56-103">Novedades de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="25a56-103">What's New in Azure Machine Learning</span></span>

### <a name="the-march-2017-release-of-microsoft-azure-machine-learning-updates-provides-the-following-feature"></a><span data-ttu-id="25a56-104">El lanzamiento en marzo de 2017 de las actualizaciones de Microsoft Azure Machine Learning incluye la siguiente característica:</span><span class="sxs-lookup"><span data-stu-id="25a56-104">The March 2017 release of Microsoft Azure Machine Learning updates provides the following feature:</span></span>



* <span data-ttu-id="25a56-105">Función dedicada para trabajos de BES de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="25a56-105">Dedicated Capacity for Azure Machine Learning BES Jobs</span></span>

    <span data-ttu-id="25a56-106">El procesamiento de grupo de lote de Machine Learning emplea el servicio [Azure Batch](../batch/batch-technical-overview.md) para proporcionar una escala administrada por el cliente para el servicio de ejecución de lotes de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="25a56-106">Machine Learning Batch Pool processing uses the [Azure Batch](../batch/batch-technical-overview.md) service to provide customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="25a56-107">El procesamiento de grupo de lote le permite crear grupos de Azure Batch en los que puede enviar trabajos por lotes y hacer que se ejecuten de manera predecible.</span><span class="sxs-lookup"><span data-stu-id="25a56-107">Batch Pool processing allows you to create Azure Batch pools on which you can submit batch jobs and have them execute in a predictable manner.</span></span>

    <span data-ttu-id="25a56-108">Para obtener más información, consulte [Servicio de Azure Batch para trabajos de Machine Learning](machine-learning-dedicated-capacity-for-bes-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="25a56-108">For more information, see [Azure Batch service for Machine Learning jobs](machine-learning-dedicated-capacity-for-bes-jobs.md).</span></span>


### <a name="the-august-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="25a56-109">El lanzamiento en agosto de 2016 de las actualizaciones de Microsoft Azure Machine Learning ofrecen las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="25a56-109">The August 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="25a56-110">Ahora, los servicios web clásicos se pueden administrar en el nuevo portal [Servicios web Microsoft Azure Machine Learning](https://services.azureml.net/) donde pueden administrarse todos los aspectos de los servicios web.</span><span class="sxs-lookup"><span data-stu-id="25a56-110">Classic Web services can now be managed in the new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>    
  * <span data-ttu-id="25a56-111">Dicho portal ofrece las [estadísticas de uso](machine-learning-manage-new-webservice.md) de los servicios web.</span><span class="sxs-lookup"><span data-stu-id="25a56-111">Which provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
  * <span data-ttu-id="25a56-112">Simplifica las pruebas de llamadas de solicitud remota a Azure Machine Learning con datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="25a56-112">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
  * <span data-ttu-id="25a56-113">Ofrece una nueva página de prueba de servicio de ejecución por lotes con datos de ejemplos e historial de envío de trabajos.</span><span class="sxs-lookup"><span data-stu-id="25a56-113">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>
  * <span data-ttu-id="25a56-114">Facilita la administración de los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="25a56-114">Provides easier endpoint management.</span></span>

### <a name="the-july-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="25a56-115">El lanzamiento en julio de 2016 de las actualizaciones de Microsoft Azure Machine Learning ofrecen las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="25a56-115">The July 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="25a56-116">Los servicios web ahora se administran como recursos de Azure administrados a través de interfaces de [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (ARM), con lo que se aportan las siguientes mejoras:</span><span class="sxs-lookup"><span data-stu-id="25a56-116">Web services are now managed as Azure resources managed through [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) interfaces, allowing for the following enhancements:</span></span>
  * <span data-ttu-id="25a56-117">Nuevas [API de REST](https://msdn.microsoft.com/library/azure/Dn950030.aspx) para implementar y administrar los servicios web basados en Resource Manager</span><span class="sxs-lookup"><span data-stu-id="25a56-117">There are new [REST APIs](https://msdn.microsoft.com/library/azure/Dn950030.aspx) to deploy and manage your Resource Manager based Web services.</span></span>
  * <span data-ttu-id="25a56-118">Nuevo portal [Servicios web Microsoft Azure Machine Learning](https://services.azureml.net/), donde pueden administrarse todos los aspectos de los servicios web</span><span class="sxs-lookup"><span data-stu-id="25a56-118">There is a new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>
* <span data-ttu-id="25a56-119">Incorpora un nuevo modelo de implementación de servicios web en varias regiones y mediante suscripción que utiliza API basadas en Azure Resource Manager que emplean el proveedor de recursos de esta solución en los servicios web.</span><span class="sxs-lookup"><span data-stu-id="25a56-119">Incorporates a new subscription-based, multi-region web service deployment model using Resource Manager based APIs leveraging the Resource Manager Resource Provider for Web Services.</span></span>
* <span data-ttu-id="25a56-120">Introduce nuevos [planes de precios](https://azure.microsoft.com/pricing/details/machine-learning/) y funcionalidades de administración de planes que utilizan el nuevo RP de Azure Resource Manager para las tareas de facturación.</span><span class="sxs-lookup"><span data-stu-id="25a56-120">Introduces new [pricing plans](https://azure.microsoft.com/pricing/details/machine-learning/) and plan management capabilities using the new Resource Manager RP for Billing.</span></span>
  * <span data-ttu-id="25a56-121">Ahora puede [implementar el servicio web en varias regiones](machine-learning-how-to-deploy-to-multiple-regions.md) sin necesidad de crear una suscripción en cada región.</span><span class="sxs-lookup"><span data-stu-id="25a56-121">You can now [deploy your web service to multiple regions](machine-learning-how-to-deploy-to-multiple-regions.md) without needing to create a subscription in each region.</span></span>
* <span data-ttu-id="25a56-122">Proporciona las [estadísticas de uso](machine-learning-manage-new-webservice.md)de los servicios web.</span><span class="sxs-lookup"><span data-stu-id="25a56-122">Provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
* <span data-ttu-id="25a56-123">Simplifica las pruebas de llamadas de solicitud remota a Azure Machine Learning con datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="25a56-123">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
* <span data-ttu-id="25a56-124">Ofrece una nueva página de prueba de servicio de ejecución por lotes con datos de ejemplos e historial de envío de trabajos.</span><span class="sxs-lookup"><span data-stu-id="25a56-124">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>

<span data-ttu-id="25a56-125">Además, Machine Learning Studio se ha actualizado para poder implementar según el modelo de servicios web nuevo o seguir implementando con el modelo de servicios web clásico.</span><span class="sxs-lookup"><span data-stu-id="25a56-125">In addition, the Machine Learning Studio has been updated to allow you to deploy to the new Web service model or continue to deploy to the classic Web service model.</span></span> 

