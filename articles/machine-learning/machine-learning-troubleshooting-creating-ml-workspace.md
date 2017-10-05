---
title: "Solución de problemas: Creación de un área de trabajo de Machine Learning y conexión a la misma | Microsoft Docs"
description: "Soluciones para problemas comunes al crear y conectarse a un área de trabajo de aprendizaje automático de Azure"
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
ms.openlocfilehash: 398ac3d9c9d32a1ab10413ce0d7ce8d448890409
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="84041-103">Guía de solución de problemas: Creación de un área de trabajo de Aprendizaje automático y conexión a la misma</span><span class="sxs-lookup"><span data-stu-id="84041-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="84041-104">Esta guía proporciona soluciones para algunos de los desafíos más comunes al configurar áreas de trabajo de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="84041-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="84041-105">Propietario del espacio de trabajo</span><span class="sxs-lookup"><span data-stu-id="84041-105">Workspace owner</span></span>
<span data-ttu-id="84041-106">Para abrir un área de trabajo en Machine Learning Studio, debe iniciar sesión en la cuenta Microsoft que utilizó para crear el área de trabajo, o bien, puede ser necesario que reciba una invitación del propietario para unirse al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="84041-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="84041-107">Desde Azure Portal puede administrar el área de trabajo, lo que incluye la capacidad de configurar el acceso.</span><span class="sxs-lookup"><span data-stu-id="84041-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="84041-108">Para obtener más información sobre cómo administrar un área de trabajo, consulte [Administración de un área de trabajo de Aprendizaje automático de Azure].</span><span class="sxs-lookup"><span data-stu-id="84041-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

<span data-ttu-id="84041-109">[Administración de un área de trabajo de Aprendizaje automático de Azure]: machine-learning-manage-workspace.md</span><span class="sxs-lookup"><span data-stu-id="84041-109">[Manage an Azure Machine Learning workspace]: machine-learning-manage-workspace.md</span></span>

## <a name="allowed-regions"></a><span data-ttu-id="84041-110">Regiones permitidas</span><span class="sxs-lookup"><span data-stu-id="84041-110">Allowed regions</span></span>
<span data-ttu-id="84041-111">Aprendizaje automático se encuentra actualmente disponible en un número limitado de regiones.</span><span class="sxs-lookup"><span data-stu-id="84041-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="84041-112">Si su suscripción no incluye una de estas regiones, es posible que vea el mensaje de error "No dispone de una suscripción en las regiones permitidas".</span><span class="sxs-lookup"><span data-stu-id="84041-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="84041-113">Para solicitar que una región se agregue a su suscripción, cree una nueva solicitud de soporte técnico de Microsoft desde Azure Portal, elija **Facturación** como el tipo de problema y siga las indicaciones para enviar su solicitud.</span><span class="sxs-lookup"><span data-stu-id="84041-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="84041-114">Cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="84041-114">Storage account</span></span>
<span data-ttu-id="84041-115">El servicio de Aprendizaje automático necesita una cuenta de almacenamiento para almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="84041-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="84041-116">Puede utilizar una cuenta de almacenamiento existente o crear una nueva cuenta de almacenamiento al crear la nueva área de trabajo de Aprendizaje automático (si dispone de cuota para crear una nueva cuenta de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="84041-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="84041-117">Tras crear la nueva área de trabajo de Machine Learning, puede iniciar sesión en Machine Learning Studio con la cuenta de Microsoft que usó para crear el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="84041-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="84041-118">Si encuentra el mensaje de error "No se encontró el área de trabajo" (similar a la captura de pantalla siguiente), use estos pasos para eliminar las cookies del explorador.</span><span class="sxs-lookup"><span data-stu-id="84041-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![Espacio de trabajo no encontrado][screen3]

<span data-ttu-id="84041-120">**Para eliminar las cookies del explorador**</span><span class="sxs-lookup"><span data-stu-id="84041-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="84041-121">Si usa Internet Explorer, haga clic en el botón **Herramientas** en la esquina superior derecha y seleccione **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="84041-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![Opciones de Internet][screen4]

2. <span data-ttu-id="84041-123">En la pestaña **General**, haga clic en **Eliminar…**</span><span class="sxs-lookup"><span data-stu-id="84041-123">Under the **General** tab, click **Delete…**</span></span>

![Pestaña General][screen5]

3. <span data-ttu-id="84041-125">En el cuadro de diálogo **Eliminar el historial de exploración**, asegúrese de que **Cookies y datos del sitio web** está seleccionado y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="84041-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Eliminación de cookies][screen6]

<span data-ttu-id="84041-127">Una vez eliminadas las cookies, reinicie el explorador y vaya a la página [Aprendizaje automático de Microsoft Azure](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="84041-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="84041-128">Cuando se le solicite un nombre de usuario y contraseña, especifique la misma cuenta Microsoft que usó para crear el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="84041-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="84041-129">Comentarios</span><span class="sxs-lookup"><span data-stu-id="84041-129">Comments</span></span>

<span data-ttu-id="84041-130">Nuestro objeto es hacer que la experiencia de Aprendizaje automático sea lo más directa posible.</span><span class="sxs-lookup"><span data-stu-id="84041-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="84041-131">Publique cualquier comentario o problema en el [foro de Aprendizaje automático de Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) para ayudarnos a ofrecerle un mejor servicio.</span><span class="sxs-lookup"><span data-stu-id="84041-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
