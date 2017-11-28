---
title: "Documentación de ayuda multigeográfica | Microsoft Docs"
description: "Aprenda a crear un área de trabajo y a publicar un servicio web en una región de Azure diferente de la región central del sur de Estados Unidos (SCUS) de Azure."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="d92e1-103">Documentación de ayuda multigeográfica</span><span class="sxs-lookup"><span data-stu-id="d92e1-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="d92e1-104">En este artículo se describe cómo crear un área de trabajo y publicar un servicio web en diferentes regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="d92e1-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="d92e1-105">La página [Productos de Azure por región](https://azure.microsoft.com/en-us/regions/services/) enumera las áreas donde Azure Machine Learning está disponible.</span><span class="sxs-lookup"><span data-stu-id="d92e1-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="d92e1-106">Crear un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="d92e1-106">Create a workspace</span></span>
1. <span data-ttu-id="d92e1-107">Inicie sesión en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="d92e1-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="d92e1-108">Haga clic en **+ NUEVO** > **DATA SERVICES** > **MACHINE LEARNING** > **CREACIÓN RÁPIDA**.</span><span class="sxs-lookup"><span data-stu-id="d92e1-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="d92e1-109">En **UBICACIÓN**, seleccione otra región, como **Sudeste Asiático**.</span><span class="sxs-lookup"><span data-stu-id="d92e1-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="d92e1-110">![Imagen de ayuda multigeográfica 1][1]</span><span class="sxs-lookup"><span data-stu-id="d92e1-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="d92e1-111">Seleccione el área de trabajo y, a continuación, haga clic en **Inicio de sesión en Estudio de aprendizaje automático**.</span><span class="sxs-lookup"><span data-stu-id="d92e1-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="d92e1-112">![Imagen de ayuda multigeográfica 2][2]</span><span class="sxs-lookup"><span data-stu-id="d92e1-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="d92e1-113">Ahora dispone de un área de trabajo en otra región que se puede usar como cualquier otra área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d92e1-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="d92e1-114">Para cambiar entre las áreas de trabajo, busque la esquina superior derecha de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="d92e1-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="d92e1-115">Haga clic en la lista desplegable, seleccione la región y, a continuación, seleccione el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d92e1-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="d92e1-116">Todo es local para la región del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d92e1-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="d92e1-117">Por ejemplo, todos los servicios web creados a partir de un área de trabajo estarán en la misma región en la que se encuentra el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d92e1-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="d92e1-118">![Imagen de ayuda multigeográfica 3][3]</span><span class="sxs-lookup"><span data-stu-id="d92e1-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="d92e1-119">Abrir un experimento de Galería</span><span class="sxs-lookup"><span data-stu-id="d92e1-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="d92e1-120">Si abre un experimento de Galería, también puede seleccionar en qué región desea copiar el experimento.</span><span class="sxs-lookup"><span data-stu-id="d92e1-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Imagen de ayuda multigeográfica 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="d92e1-122">Administración de servicios web</span><span class="sxs-lookup"><span data-stu-id="d92e1-122">Web service management</span></span>
<span data-ttu-id="d92e1-123">Para administrar mediante programación los servicios web, como el reciclaje, use la dirección específica de la región:</span><span class="sxs-lookup"><span data-stu-id="d92e1-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="d92e1-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="d92e1-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="d92e1-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="d92e1-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="d92e1-126">Puntos a tener en cuenta</span><span class="sxs-lookup"><span data-stu-id="d92e1-126">Things to note</span></span>
1. <span data-ttu-id="d92e1-127">Solo se pueden copiar experimentos entre áreas de trabajo que pertenecen a la misma región.</span><span class="sxs-lookup"><span data-stu-id="d92e1-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="d92e1-128">Si necesita copiar el experimento en áreas de trabajo de distintas regiones, puede usar el commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) de [PowerShell](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="d92e1-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="d92e1-129">Otra solución consiste en publicar el experimento en la galería en el modo fuera de lista y abrirlo en el área de trabajo de la otra región.</span><span class="sxs-lookup"><span data-stu-id="d92e1-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="d92e1-130">El selector de región solo mostrará áreas de trabajo de una región de cada vez.</span><span class="sxs-lookup"><span data-stu-id="d92e1-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="d92e1-131">Se creará un área de trabajo libre o un área de trabajo (anónima) de acceso a invitados y se alojará en la zona central del sur de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="d92e1-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="d92e1-132">Los servicios web implementados desde un área de trabajo del sudeste asiático también se hospedarán en el sudeste asiático.</span><span class="sxs-lookup"><span data-stu-id="d92e1-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="d92e1-133">Más información</span><span class="sxs-lookup"><span data-stu-id="d92e1-133">More information</span></span>
<span data-ttu-id="d92e1-134">Formule una pregunta en el [Foro de Aprendizaje automático de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="d92e1-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
