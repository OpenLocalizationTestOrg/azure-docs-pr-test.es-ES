---
title: "documentación de Ayuda de aaaMulti geográfica | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un área de trabajo y publicar un servicio web en una región de Azure diferente de hello sur Central Estados Unidos (SCUS) región de Azure."
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
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="308d3-103">Documentación de ayuda multigeográfica</span><span class="sxs-lookup"><span data-stu-id="308d3-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="308d3-104">En este artículo se describe cómo crear un área de trabajo y publicar un servicio web en diferentes regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="308d3-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="308d3-105">Hola [productos de Azure por página región](https://azure.microsoft.com/en-us/regions/services/) enumera las áreas donde el aprendizaje automático de Azure está disponible.</span><span class="sxs-lookup"><span data-stu-id="308d3-105">hello [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="308d3-106">Crear un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="308d3-106">Create a workspace</span></span>
1. <span data-ttu-id="308d3-107">Inicie sesión en toohello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="308d3-107">Sign in toohello Azure Classic Portal.</span></span>
2. <span data-ttu-id="308d3-108">Haga clic en **+ NUEVO** > **DATA SERVICES** > **MACHINE LEARNING** > **CREACIÓN RÁPIDA**.</span><span class="sxs-lookup"><span data-stu-id="308d3-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="308d3-109">En **UBICACIÓN**, seleccione otra región, como **Sudeste Asiático**.</span><span class="sxs-lookup"><span data-stu-id="308d3-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="308d3-110">![Imagen de ayuda multigeográfica 1][1]</span><span class="sxs-lookup"><span data-stu-id="308d3-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="308d3-111">Seleccione el área de trabajo de hello y, a continuación, haga clic en **inicio de sesión tooML Studio**.</span><span class="sxs-lookup"><span data-stu-id="308d3-111">Select hello workspace, and then click **Sign-in tooML Studio**.</span></span>
   <span data-ttu-id="308d3-112">![Imagen de ayuda multigeográfica 2][2]</span><span class="sxs-lookup"><span data-stu-id="308d3-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="308d3-113">Ahora dispone de un área de trabajo en otra región que se puede usar como cualquier otra área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="308d3-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="308d3-114">tooswitch entre las áreas de trabajo, busque toohello superior derecha de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="308d3-114">tooswitch among your workspaces, look toohello upper right of your screen.</span></span> <span data-ttu-id="308d3-115">Haga clic en la lista desplegable de hello, región de hello seleccione y área de trabajo de hello, a continuación, seleccione.</span><span class="sxs-lookup"><span data-stu-id="308d3-115">Click hello dropdown, select hello region, and then select hello workspace.</span></span> <span data-ttu-id="308d3-116">Todo lo que es la región del área de trabajo local toohello.</span><span class="sxs-lookup"><span data-stu-id="308d3-116">Everything is local toohello workspace region.</span></span>  <span data-ttu-id="308d3-117">Por ejemplo, todos los servicios web creados a partir de un área de trabajo será Hola misma área de trabajo de Hola de región se encuentra en.</span><span class="sxs-lookup"><span data-stu-id="308d3-117">For example, all of your web services created from a workspace will be in hello same region hello workspace is located in.</span></span>
   <span data-ttu-id="308d3-118">![Imagen de ayuda multigeográfica 3][3]</span><span class="sxs-lookup"><span data-stu-id="308d3-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="308d3-119">Abrir un experimento de Galería</span><span class="sxs-lookup"><span data-stu-id="308d3-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="308d3-120">Si abre un experimento desde la galería, también puede seleccionar qué región que desee toocopy Hola experimento en.</span><span class="sxs-lookup"><span data-stu-id="308d3-120">If you open an experiment from Gallery, you can also select which region you want toocopy hello experiment to.</span></span>

![Imagen de ayuda multigeográfica 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="308d3-122">Administración de servicios web</span><span class="sxs-lookup"><span data-stu-id="308d3-122">Web service management</span></span>
<span data-ttu-id="308d3-123">tooprogrammatically administrar servicios web, como de reciclaje, usar una dirección específica de la región hello:</span><span class="sxs-lookup"><span data-stu-id="308d3-123">tooprogrammatically manage web services, such as for retraining, use hello region-specific address:</span></span>

* <span data-ttu-id="308d3-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="308d3-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="308d3-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="308d3-125">https://europewest.management.azureml.net</span></span>

### <a name="things-toonote"></a><span data-ttu-id="308d3-126">Cosas toonote</span><span class="sxs-lookup"><span data-stu-id="308d3-126">Things toonote</span></span>
1. <span data-ttu-id="308d3-127">Solo puede copiar experimentos entre áreas de trabajo que pertenecen toohello misma región de esta manera.</span><span class="sxs-lookup"><span data-stu-id="308d3-127">You can only copy experiments between workspaces that belong toohello same region this way.</span></span> <span data-ttu-id="308d3-128">Si necesita toocopy experimento en áreas de trabajo en distintas regiones, puede usar hello [PowerShell](http://aka.ms/amlps) commandlet [ *copia AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish que.</span><span class="sxs-lookup"><span data-stu-id="308d3-128">If you need toocopy experiment across workspaces in different regions, you can use hello [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish that.</span></span> <span data-ttu-id="308d3-129">Otra solución alternativa es toopublish Hola experimento en la Galería de modo que no figuran en, y vuelva a abrirla en el área de trabajo de Hola de hello otra región.</span><span class="sxs-lookup"><span data-stu-id="308d3-129">Another workaround is toopublish hello experiment into Gallery in unlisted mode, then open it in hello workspace from hello other region.</span></span>
2. <span data-ttu-id="308d3-130">selector de región de Hello, solo se mostrarán las áreas de una región de trabajo a la vez.</span><span class="sxs-lookup"><span data-stu-id="308d3-130">hello region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="308d3-131">Se creará un área de trabajo libre o un área de trabajo (anónima) de acceso a invitados y se alojará en la zona central del sur de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="308d3-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="308d3-132">Los servicios web implementados desde un área de trabajo del sudeste asiático también se hospedarán en el sudeste asiático.</span><span class="sxs-lookup"><span data-stu-id="308d3-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="308d3-133">Más información</span><span class="sxs-lookup"><span data-stu-id="308d3-133">More information</span></span>
<span data-ttu-id="308d3-134">Formule una pregunta en hello [foro de aprendizaje automático de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="308d3-134">Ask a question on hello [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
