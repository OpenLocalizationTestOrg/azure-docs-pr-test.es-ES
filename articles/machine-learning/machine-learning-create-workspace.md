---
title: "Creación y uso compartido de un área de trabajo de Aprendizaje automático de Azure | Microsoft Docs"
description: "Creación de un área de trabajo para Estudio de aprendizaje automático de Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 182a34822e71d63f4d7229548ae3f59d9f195337
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="b64f6-103">Creación y uso compartido de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="b64f6-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="b64f6-104">Este menú vincula a temas en los que se describe cómo configurar los diversos entornos de ciencia de datos usados por el proceso de Cortana Analytics (CAPS).</span><span class="sxs-lookup"><span data-stu-id="b64f6-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="b64f6-105">Para usar Estudio de aprendizaje automático de Azure, debe tener un área de trabajo de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="b64f6-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span></span> <span data-ttu-id="b64f6-106">Esta área de trabajo contiene las herramientas que necesita para crear, administrar y publicar experimentos.</span><span class="sxs-lookup"><span data-stu-id="b64f6-106">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="to-create-a-workspace"></a><span data-ttu-id="b64f6-107">Para crear un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="b64f6-107">To create a workspace</span></span>
1. <span data-ttu-id="b64f6-108">Inicie sesión en el [Portal de Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="b64f6-108">Sign in to the [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="b64f6-109">Para crear un área de trabajo e iniciar sesión en ella, debe ser un administrador de suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b64f6-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="b64f6-110">Haga clic en **+ Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="b64f6-110">Click **+New**</span></span>

3. <span data-ttu-id="b64f6-111">Seleccione **Intelligence + analytics**, haga clic en el **área de trabajo de Machine Learning** y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b64f6-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="b64f6-112">Escriba la información de su área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b64f6-112">Enter your workspace information</span></span>

    - <span data-ttu-id="b64f6-113">El *nombre de área de trabajo* puede tener hasta 260 caracteres, pero no puede terminar con un espacio.</span><span class="sxs-lookup"><span data-stu-id="b64f6-113">The *workspace name* may be up to 260 characters, not ending in a space.</span></span> <span data-ttu-id="b64f6-114">El nombre no puede incluir estos caracteres: `< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="b64f6-114">The name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="b64f6-115">El *plan de servicio web* elegido (o creado), junto con el *plan de tarifa* asociado seleccionado, se usa si implementa servicios web desde esta área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b64f6-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Crear un área de trabajo](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="b64f6-117">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="b64f6-117">Click **Create**</span></span>

<span data-ttu-id="b64f6-118">Una vez implementado el área de trabajo, puede abrirlo en Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b64f6-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="b64f6-119">Examine Machine Learning Studio en [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="b64f6-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="b64f6-120">Seleccione el área de trabajo en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="b64f6-120">Select your workspace in the upper-right-hand corner.</span></span>

    ![Selección del área de trabajo](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="b64f6-122">Haga clic en **my experiments** (Mis experimentos).</span><span class="sxs-lookup"><span data-stu-id="b64f6-122">Click **my experiments**.</span></span>

    ![Abrir experimentos](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="b64f6-124">Para obtener más información sobre cómo administrar un área de trabajo, consulte [Administración de un área de trabajo de Aprendizaje automático de Azure](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="b64f6-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="b64f6-125">Si experimenta algún problema al crear el área de trabajo, vea [Guía de solución de problemas: Creación de un área de trabajo de Machine Learning y conexión a la misma](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="b64f6-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="b64f6-126">Uso compartido de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="b64f6-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="b64f6-127">Tras crear un área de trabajo de Machine Learning, puede invitar usuarios a ella, a fin de compartir el acceso a dicha área y todos sus experimentos, conjuntos de datos, bloc de notas, etc. Puede agregar usuarios en uno de estos roles:</span><span class="sxs-lookup"><span data-stu-id="b64f6-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="b64f6-128">**Usuario**: los usuarios de un área de trabajo pueden crear, abrir, modificar y eliminar experimentos, conjuntos de datos y otros elementos en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b64f6-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span></span>
* <span data-ttu-id="b64f6-129">**Propietario**: un propietario puede invitar y quitar usuarios en el área de trabajo, además de lo que pueden hacer los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b64f6-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="b64f6-130">La cuenta de administrador que crea el área de trabajo se agrega automáticamente al área de trabajo como propietario de dicha área.</span><span class="sxs-lookup"><span data-stu-id="b64f6-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span></span> <span data-ttu-id="b64f6-131">No obstante, a los otros administradores o usuarios de dicha suscripción no se les concede acceso automáticamente al área de trabajo; debe invitarlos de manera explícita.</span><span class="sxs-lookup"><span data-stu-id="b64f6-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span></span>
> 
> 

### <a name="to-share-a-workspace"></a><span data-ttu-id="b64f6-132">Para compartir un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="b64f6-132">To share a workspace</span></span>

1. <span data-ttu-id="b64f6-133">Inicie sesión en Machine Learning Studio en [https://studio.azureml.net/Home](https://studio.azureml.net/Home).</span><span class="sxs-lookup"><span data-stu-id="b64f6-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="b64f6-134">En el panel izquierdo, haga clic en **SETTINGS** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="b64f6-134">In the left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="b64f6-135">Haga clic en la pestaña **USERS** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="b64f6-135">Click the **USERS** tab</span></span>

4. <span data-ttu-id="b64f6-136">Haga clic en **INVITE MORE USERS** (Invitar más usuarios) en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="b64f6-136">Click **INVITE MORE USERS** at the bottom of the page</span></span>

    ![Configuración de Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="b64f6-138">Escriba una o varias direcciones de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="b64f6-138">Enter one or more email addresses.</span></span> <span data-ttu-id="b64f6-139">Los usuarios necesitan una cuenta Microsoft o una cuenta de organización (de Azure Active Directory) válidas.</span><span class="sxs-lookup"><span data-stu-id="b64f6-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="b64f6-140">Seleccione si desea agregar los usuarios como propietario o usuario.</span><span class="sxs-lookup"><span data-stu-id="b64f6-140">Select whether you want to add the users as Owner or User.</span></span>

7. <span data-ttu-id="b64f6-141">Haga clic en el botón de marca de verificación **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="b64f6-141">Click the **OK** checkmark button.</span></span>

<span data-ttu-id="b64f6-142">Cada usuario agregado recibirá un correo electrónico con instrucciones sobre cómo iniciar sesión en el área de trabajo compartida.</span><span class="sxs-lookup"><span data-stu-id="b64f6-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="b64f6-143">Para que los usuarios puedan implementar o administrar servicios web en esta área de trabajo, deben ser colaborador o administrador de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b64f6-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span></span> 



