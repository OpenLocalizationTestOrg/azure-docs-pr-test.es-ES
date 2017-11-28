---
title: "un área de trabajo de aprendizaje automático de aaaCreate | Documentos de Microsoft"
description: "¿Cómo toocreate un área de trabajo de estudio de aprendizaje automático de Azure"
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
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="3af9f-103">Creación y uso compartido de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="3af9f-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="3af9f-104">Este menú vincula tootopics que describen cómo tooset seguridad Hola varios entornos de ciencia de datos utilizan por hello proceso de análisis de Cortana (CAP).</span><span class="sxs-lookup"><span data-stu-id="3af9f-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="3af9f-105">toouse estudio de aprendizaje automático de Azure, deberá toohave un área de trabajo de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="3af9f-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="3af9f-106">Esta área de trabajo contiene herramientas de Hola que necesita toocreate, administrar y publicar experimentos.</span><span class="sxs-lookup"><span data-stu-id="3af9f-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="3af9f-107">toocreate un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="3af9f-107">toocreate a workspace</span></span>
1. <span data-ttu-id="3af9f-108">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="3af9f-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="3af9f-109">toosign en y crear un área de trabajo, deberá toobe un administrador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3af9f-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="3af9f-110">Haga clic en **+ Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="3af9f-110">Click **+New**</span></span>

3. <span data-ttu-id="3af9f-111">Seleccione **Intelligence + analytics**, haga clic en el **área de trabajo de Machine Learning** y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3af9f-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="3af9f-112">Escriba la información de su área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3af9f-112">Enter your workspace information</span></span>

    - <span data-ttu-id="3af9f-113">Hola *nombre de área de trabajo* puede ser up too260 caracteres, no termina en un espacio.</span><span class="sxs-lookup"><span data-stu-id="3af9f-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="3af9f-114">nombre de Hello no puede incluir estos caracteres:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="3af9f-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="3af9f-115">Hola *plan del servicio web* elija (o cree), junto con los asociados de hello *tarifa* seleccione, se usa si implementa servicios web desde esta área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3af9f-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Crear un área de trabajo](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="3af9f-117">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="3af9f-117">Click **Create**</span></span>

<span data-ttu-id="3af9f-118">Una vez implementado el área de trabajo de hello, puede abrirlo en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="3af9f-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="3af9f-119">Examinar tooMachine estudio de aprendizaje en [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="3af9f-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="3af9f-120">Seleccione el área de trabajo en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="3af9f-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![Selección del área de trabajo](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="3af9f-122">Haga clic en **my experiments** (Mis experimentos).</span><span class="sxs-lookup"><span data-stu-id="3af9f-122">Click **my experiments**.</span></span>

    ![Abrir experimentos](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="3af9f-124">Para obtener más información sobre cómo administrar un área de trabajo, consulte [Administración de un área de trabajo de Aprendizaje automático de Azure](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="3af9f-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="3af9f-125">Si se produce un problema al crear el área de trabajo, consulte [Guía de solución de problemas: crear y conectar el área de trabajo de aprendizaje automático de tooa](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="3af9f-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="3af9f-126">Uso compartido de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="3af9f-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="3af9f-127">Una vez que se crea un área de trabajo de aprendizaje automático, puede invitar a los usuarios tooyour área de trabajo tooshare acceso tooyour área de trabajo y todos los sus experimentos, conjuntos de datos, blocs de notas, etcetera. Puede agregar usuarios en uno de estos roles:</span><span class="sxs-lookup"><span data-stu-id="3af9f-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="3af9f-128">**Usuario** -un usuario del área de trabajo puede crear, abrir, modificar y eliminar experimentos, conjuntos de datos, etc. en el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3af9f-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="3af9f-129">**Propietario** : puede invitar un propietario y quitar usuarios en área de trabajo de hello en suma toowhat un usuario pueden hacer.</span><span class="sxs-lookup"><span data-stu-id="3af9f-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="3af9f-130">cuenta de administrador de Hola que crea el área de trabajo de Hola se agrega automáticamente el área de trabajo de toohello como propietario del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3af9f-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="3af9f-131">Sin embargo, otros administradores o usuarios en que la suscripción no son automáticamente concedido acceso toohello área de trabajo, deberá tooinvite ellos explícitamente.</span><span class="sxs-lookup"><span data-stu-id="3af9f-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="3af9f-132">tooshare un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="3af9f-132">tooshare a workspace</span></span>

1. <span data-ttu-id="3af9f-133">Inicie sesión en tooMachine estudio de aprendizaje en [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="3af9f-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="3af9f-134">En el panel izquierdo de hello, haga clic en **configuración**</span><span class="sxs-lookup"><span data-stu-id="3af9f-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="3af9f-135">Haga clic en hello **usuarios** ficha</span><span class="sxs-lookup"><span data-stu-id="3af9f-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="3af9f-136">Haga clic en **invitar a más usuarios** final Hola de página Hola</span><span class="sxs-lookup"><span data-stu-id="3af9f-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Configuración de Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="3af9f-138">Escriba una o varias direcciones de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="3af9f-138">Enter one or more email addresses.</span></span> <span data-ttu-id="3af9f-139">los usuarios de Hello necesitan una cuenta válida de Microsoft o una cuenta profesional (de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3af9f-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="3af9f-140">Seleccione si desea que los usuarios de hello tooadd como propietario o usuario.</span><span class="sxs-lookup"><span data-stu-id="3af9f-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="3af9f-141">Haga clic en hello **Aceptar** botón de marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="3af9f-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="3af9f-142">Cada usuario que agregue recibirán un correo electrónico con instrucciones sobre cómo toosign en toohello comparte el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3af9f-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="3af9f-143">Para los usuarios toobe puede toodeploy o administrar servicios web en esta área de trabajo, deben ser un colaborador o administrador de hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3af9f-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



