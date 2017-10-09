---
title: "Paso 1: Creación de un área de trabajo de Machine Learning | Microsoft Docs"
description: "Paso 1 de hello desarrollar un tutorial de solución de predicción: Obtenga información acerca de cómo tooset configurar una nueva área de trabajo de estudio de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="c8269-103">Paso 1 del tutorial: Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="c8269-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="c8269-104">Trata Hola primer paso del tutorial de hello, [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="c8269-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="c8269-105">**Creación de un área de trabajo de Aprendizaje automático**</span><span class="sxs-lookup"><span data-stu-id="c8269-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="c8269-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="c8269-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="c8269-107">Crear un experimento nuevo</span><span class="sxs-lookup"><span data-stu-id="c8269-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="c8269-108">Entrenar y evaluar modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="c8269-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="c8269-109">Implementar el servicio Web de Hola</span><span class="sxs-lookup"><span data-stu-id="c8269-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="c8269-110">Acceder al servicio Web Hola</span><span class="sxs-lookup"><span data-stu-id="c8269-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="c8269-111">toouse estudio de aprendizaje automático, deberá toohave un área de trabajo de aprendizaje automático de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c8269-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="c8269-112">Esta área de trabajo contiene herramientas de Hola que necesita toocreate, administrar y publicar experimentos.</span><span class="sxs-lookup"><span data-stu-id="c8269-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="c8269-113">Administrador de Hello para la suscripción de Azure necesita el área de trabajo de toocreate hello y, a continuación, agregue como un propietario o colaborador.</span><span class="sxs-lookup"><span data-stu-id="c8269-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="c8269-114">Para obtener más información, consulte [Creación y uso compartido de un área de trabajo de Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="c8269-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="c8269-115">Una vez que haya creado el área de trabajo, abra Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="c8269-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="c8269-116">Si tiene más de un área de trabajo, puede seleccionar el área de trabajo de hello en la barra de herramientas de hello en la esquina superior derecha de Hola de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="c8269-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Selección del área de trabajo en Studio][2]

> [!TIP]
> <span data-ttu-id="c8269-118">Si se ha realizado un propietario del área de trabajo de hello, puede compartir experimentos Hola trabaja en Invitar a otros usuarios toohello área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c8269-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="c8269-119">También puede hacerlo en estudio de aprendizaje automático en hello **configuración** página.</span><span class="sxs-lookup"><span data-stu-id="c8269-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="c8269-120">Solo necesita Hola cuenta de Microsoft o cuenta profesional para cada usuario.</span><span class="sxs-lookup"><span data-stu-id="c8269-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="c8269-121">En hello **configuración** página, haga clic en **usuarios**, a continuación, haga clic en **invitar a más usuarios** final Hola de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="c8269-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="c8269-122">**A continuación: [Cargue los datos existentes](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="c8269-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
