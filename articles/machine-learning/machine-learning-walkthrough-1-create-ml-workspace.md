---
title: "Paso 1: Creación de un área de trabajo de Machine Learning | Microsoft Docs"
description: "Paso 1 del tutorial Desarrollo de una solución predictiva: carga de datos públicos almacenados en Estudio de aprendizaje automático de Azure."
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
ms.openlocfilehash: 8ca42ef8f5314866301f5c9e93caa90dc837a66e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="321dd-103">Paso 1 del tutorial: Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="321dd-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="321dd-104">Este es el primer paso del tutorial [Desarrollo de una solución de análisis predictiva para la evaluación del riesgo de crédito en Aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="321dd-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="321dd-105">**Creación de un área de trabajo de Aprendizaje automático**</span><span class="sxs-lookup"><span data-stu-id="321dd-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="321dd-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="321dd-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="321dd-107">Crear un experimento nuevo</span><span class="sxs-lookup"><span data-stu-id="321dd-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="321dd-108">Entrenamiento y evaluación de los modelos</span><span class="sxs-lookup"><span data-stu-id="321dd-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="321dd-109">Implementación del servicio web</span><span class="sxs-lookup"><span data-stu-id="321dd-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="321dd-110">Acceso al servicio web</span><span class="sxs-lookup"><span data-stu-id="321dd-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

<span data-ttu-id="321dd-111">Para usar Estudio de aprendizaje automático, debe tener un área de trabajo de Aprendizaje automático de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="321dd-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="321dd-112">Esta área de trabajo contiene las herramientas que necesita para crear, administrar y publicar experimentos.</span><span class="sxs-lookup"><span data-stu-id="321dd-112">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="321dd-113">El administrador de su suscripción de Azure debe crear el área de trabajo y, a continuación, agregarlo como un propietario o colaborador.</span><span class="sxs-lookup"><span data-stu-id="321dd-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="321dd-114">Para obtener más información, consulte [Creación y uso compartido de un área de trabajo de Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="321dd-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="321dd-115">Una vez que haya creado el área de trabajo, abra Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="321dd-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="321dd-116">Si tiene más de un área de trabajo, puede seleccionar la que desee en la barra de herramientas de la esquina superior derecha de la ventana.</span><span class="sxs-lookup"><span data-stu-id="321dd-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span></span>

![Selección del área de trabajo en Studio][2]

> [!TIP]
> <span data-ttu-id="321dd-118">Si le han convertido en el propietario del área de trabajo, puede compartir los experimentos en los que esté trabajando invitando a otros al área.</span><span class="sxs-lookup"><span data-stu-id="321dd-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span></span> <span data-ttu-id="321dd-119">Para ello, en Estudio de aprendizaje automático, vaya a la página **CONFIGURACIÓN** .</span><span class="sxs-lookup"><span data-stu-id="321dd-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span></span> <span data-ttu-id="321dd-120">Solo necesita la cuenta Microsoft o la cuenta de organización de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="321dd-120">You just need the Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="321dd-121">En la página **CONFIGURACIÓN**, haga clic en **USUARIOS** y, después, haga clic en **INVITE MORE USERS** (INVITAR A MÁS USUARIOS) en la parte inferior de la ventana.</span><span class="sxs-lookup"><span data-stu-id="321dd-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span></span>
> 
> 

- - -
<span data-ttu-id="321dd-122">**A continuación: [Cargue los datos existentes](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="321dd-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
