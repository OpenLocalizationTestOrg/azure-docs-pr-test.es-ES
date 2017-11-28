---
title: "Solucionar problemas: Crear y conectar el área de trabajo de aprendizaje automático de tooa | Documentos de Microsoft"
description: "Soluciones para problemas comunes de creación y la conexión de área de trabajo de aprendizaje automático de Azure tooan"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="8ffc5-103">Guía de solución de problemas: crear y conectar el área de trabajo de aprendizaje automático de tooan</span><span class="sxs-lookup"><span data-stu-id="8ffc5-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="8ffc5-104">Esta guía proporciona soluciones para algunos de los desafíos más comunes al configurar áreas de trabajo de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="8ffc5-105">Propietario del espacio de trabajo</span><span class="sxs-lookup"><span data-stu-id="8ffc5-105">Workspace owner</span></span>
<span data-ttu-id="8ffc5-106">tooopen un área de trabajo en estudio de aprendizaje automático, debe ser firmado en toohello Account de Microsoft usa el área de trabajo de toocreate hello, o si debe tooreceive una invitación de área de trabajo de hello propietario toojoin Hola.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="8ffc5-107">De hello portal de Azure puede administrar Hola área de trabajo, que incluye el acceso de hello capacidad tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="8ffc5-108">Para obtener más información sobre cómo administrar un área de trabajo, consulte [Administración de un área de trabajo de Aprendizaje automático de Azure].</span><span class="sxs-lookup"><span data-stu-id="8ffc5-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[Administración de un área de trabajo de Aprendizaje automático de Azure]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="8ffc5-110">Regiones permitidas</span><span class="sxs-lookup"><span data-stu-id="8ffc5-110">Allowed regions</span></span>
<span data-ttu-id="8ffc5-111">Aprendizaje automático se encuentra actualmente disponible en un número limitado de regiones.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="8ffc5-112">Si su suscripción no incluye una de estas regiones, verá el mensaje de error de hello, "No tiene suscripciones en hello permiten regiones."</span><span class="sxs-lookup"><span data-stu-id="8ffc5-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="8ffc5-113">toorequest que una región de ser agregado tooyour suscripción, cree una nueva solicitud de soporte técnico de Microsoft de hello portal de Azure, elija **facturación** como tipo de problema de Hola y seguir Hola solicita toosubmit su solicitud.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="8ffc5-114">Cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8ffc5-114">Storage account</span></span>
<span data-ttu-id="8ffc5-115">Hola servicio aprendizaje automático necesita un toostore de datos de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="8ffc5-116">Puede usar una cuenta de almacenamiento existente, o puede crear una nueva cuenta de almacenamiento al crear el área de trabajo de aprendizaje automático nuevo hello (si tiene una cuenta de almacenamiento toocreate de cuota).</span><span class="sxs-lookup"><span data-stu-id="8ffc5-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="8ffc5-117">Después de crea el área de trabajo de hello nuevo aprendizaje automático, puede iniciar sesión tooMachine estudio de aprendizaje con cuenta de Microsoft hello que usa el área de trabajo de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="8ffc5-118">Si se produce el mensaje de error de hello, "Área de trabajo no encontrado" (toohello similar siguiente captura de pantalla), utilice Hola siguiendo los pasos toodelete las cookies del explorador.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![Espacio de trabajo no encontrado][screen3]

<span data-ttu-id="8ffc5-120">**cookies del explorador toodelete**</span><span class="sxs-lookup"><span data-stu-id="8ffc5-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="8ffc5-121">Si utiliza Internet Explorer, haga clic en hello **herramientas** situado en la esquina superior derecha de Hola y seleccione **opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![Opciones de Internet][screen4]

2. <span data-ttu-id="8ffc5-123">En hello **General** , haga clic en **eliminar...**</span><span class="sxs-lookup"><span data-stu-id="8ffc5-123">Under hello **General** tab, click **Delete…**</span></span>

![Pestaña General][screen5]

3. <span data-ttu-id="8ffc5-125">Hola **eliminar el historial de exploración** diálogo cuadro, asegúrese de que **Cookies y datos del sitio Web** está seleccionada y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Eliminación de cookies][screen6]

<span data-ttu-id="8ffc5-127">Después de eliminarán las cookies de hello, reinicie el Explorador de hello y, a continuación, vaya toohello [aprendizaje automático de Microsoft Azure](https://studio.azureml.net) página.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="8ffc5-128">Cuando se le pida, escriba un nombre de usuario y una contraseña, Hola la misma cuenta de Microsoft que usa el área de trabajo de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="8ffc5-129">Comentarios</span><span class="sxs-lookup"><span data-stu-id="8ffc5-129">Comments</span></span>

<span data-ttu-id="8ffc5-130">Nuestro objetivo es toomake Hola máxima uniformidad posible de experiencia de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="8ffc5-131">Publique los comentarios y problemas en hello [foro de aprendizaje automático de Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp nos ofrecerle un servicio mejor.</span><span class="sxs-lookup"><span data-stu-id="8ffc5-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
