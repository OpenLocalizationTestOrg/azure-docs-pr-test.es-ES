---
title: "Administración de aplicaciones lógicas en Visual Studio: Azure Logic Apps | Microsoft Docs"
description: "Administración de aplicaciones lógicas y otros recursos de Azure con Visual Studio Cloud Explorer"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: a5bf24de1a7a2b6d4c1ae6416c95d83ef7506da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="9e580-103">Administración de sus aplicaciones lógicas con Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9e580-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="9e580-104">Aunque [Azure Portal](https://portal.azure.com/) ofrece un medio excelente para diseñar y administrar Azure Logic Apps, puede usar Visual Studio Cloud Explorer para administrar muchos recursos de Azure, como las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="9e580-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="9e580-105">Visual Studio Cloud Explorer le permite explorar, administrar, editar y descargar aplicaciones lógicas publicadas.</span><span class="sxs-lookup"><span data-stu-id="9e580-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="9e580-106">Las tareas de administración incluyen habilitar, deshabilitar y ver el historial de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="9e580-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="9e580-107">Para poder acceder a las aplicaciones lógicas y administrarlas en Visual Studio, instale y configure estas herramientas de Visual Studio para Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="9e580-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9e580-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9e580-108">Prerequisites</span></span>

* [<span data-ttu-id="9e580-109">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9e580-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="9e580-110">[SDK de Azure más reciente](https://azure.microsoft.com/downloads/) (2.9.1 o superior)</span><span class="sxs-lookup"><span data-stu-id="9e580-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="9e580-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9e580-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="9e580-112">Acceso a la web para usar el diseñador incrustado</span><span class="sxs-lookup"><span data-stu-id="9e580-112">Access to the web when using the embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="9e580-113">Instalación de herramientas de Visual Studio para Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9e580-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="9e580-114">Después de instalar los requisitos previos, descargue e instale las Herramientas de Azure Logic Apps para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e580-114">After you install the prerequisites, download and install the Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="9e580-115">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e580-115">Open Visual Studio.</span></span> <span data-ttu-id="9e580-116">En el menú **Herramientas**, seleccione **Extensiones y actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="9e580-116">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="9e580-117">Expanda la categoría **En línea** para que pueda buscar en línea en la Galería de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e580-117">Expand the **Online** category so you can search online in the Visual Studio Gallery.</span></span>
3. <span data-ttu-id="9e580-118">Busque **Logic Apps** hasta que encuentre las **herramientas de Azure Logic Apps para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="9e580-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="9e580-119">Para descargar e instalar la extensión, haga clic en el botón **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="9e580-119">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="9e580-120">Reinicie Visual Studio después de la instalación.</span><span class="sxs-lookup"><span data-stu-id="9e580-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="9e580-121">Para descargar directamente las Herramientas de Azure Logic Apps para Visual Studio, vaya a [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="9e580-121">To download the Azure Logic Apps Tools for Visual Studio directly, go to the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="9e580-122">Búsqueda de aplicaciones lógicas en Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9e580-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="9e580-123">Para abrir Cloud Explorer, en el menú **Vista**, elija **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9e580-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="9e580-124">Busque la aplicación lógica. Puede hacerlo por grupo de recursos o por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="9e580-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="9e580-125">Si explora por tipo de recurso, seleccione su suscripción de Azure y expanda la sección **Logic Apps**. Luego, seleccione la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9e580-125">If you browse by resource type, select your Azure subscription, expand the **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="9e580-126">Si explora por grupo de recursos, expanda el grupo de recursos que tiene la aplicación lógica y seleccione la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9e580-126">If you browse by resource group, expand the resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="9e580-127">Para ver los comandos de la aplicación lógica, haga clic con el botón derecho en la aplicación lógica; o bien, en la parte inferior de Cloud Explorer, elija del menú **Acciones**.</span><span class="sxs-lookup"><span data-stu-id="9e580-127">To view commands for your logic app, either right-click your logic app, or at the bottom of Cloud Explorer, choose from the **Actions** menu.</span></span>

    ![Búsqueda de su aplicación lógica](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="9e580-129">Edición de la aplicación lógica con el Diseñador de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9e580-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="9e580-130">En Cloud Explorer, puede abrir una aplicación lógica implementada actualmente en el mismo diseñador que usa en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9e580-130">From Cloud Explorer, you can open a currently deployed logic app in the same designer that you use in the Azure portal.</span></span> 

* <span data-ttu-id="9e580-131">Para editar la aplicación lógica, en Cloud Explorer, haga clic con el botón derecho en la aplicación lógica y seleccione **Abrir con el editor de aplicaciones lógicas**.</span><span class="sxs-lookup"><span data-stu-id="9e580-131">To edit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="9e580-132">Para publicar las actualizaciones en la nube, elija **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="9e580-132">To publish your updates to the cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="9e580-133">Para iniciar una nueva ejecución, elija **Ejecutar desencadenador**.</span><span class="sxs-lookup"><span data-stu-id="9e580-133">To start a new run, choose **Run Trigger**.</span></span>

![Diseñador de Logic Apps](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="9e580-135">En el diseñador, también puede **descargar** una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9e580-135">From the designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="9e580-136">Esta acción parametriza automáticamente la definición de aplicación lógica y la guarda como una plantilla de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e580-136">This action automatically parameterizes the logic app definition, and saves the definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="9e580-137">Puede agregar esta plantilla de implementación al proyecto Grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e580-137">You can add this deployment template to your Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="9e580-138">Búsqueda del historial de ejecución de su aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="9e580-138">Browse your logic app run history</span></span>

<span data-ttu-id="9e580-139">Para ver el historial de ejecución de su aplicación lógica, haga clic con el botón derecho en la aplicación lógica y seleccione **Abrir el historial de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="9e580-139">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="9e580-140">Para reordenar su historial de ejecución basándose en cualquiera de las propiedades mostradas, seleccione el encabezado de columna.</span><span class="sxs-lookup"><span data-stu-id="9e580-140">To reorder your run history based on any of the properties shown, select the column header.</span></span>

![Historial de ejecuciones](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="9e580-142">Para mostrar el historial de ejecuciones de una instancia y revisar los resultados de la ejecución, incluidas las entradas y salidas de cada paso, haga doble clic en una de las instancias de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9e580-142">To show the run history for an instance so you can review the run results, including the inputs and outputs from each step, double-click one of the run instances.</span></span>

![Resultados del historial de ejecuciones, entradas y salidas de los pasos](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="9e580-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9e580-144">Next steps</span></span>

* [<span data-ttu-id="9e580-145">Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS</span><span class="sxs-lookup"><span data-stu-id="9e580-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="9e580-146">Creación e implementación de aplicaciones lógicas en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e580-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="9e580-147">Ejemplos de aplicaciones lógicas y escenarios comunes</span><span class="sxs-lookup"><span data-stu-id="9e580-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* <span data-ttu-id="9e580-148">[Vídeo: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) (Automatización de los procesos de negocio con Azure Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="9e580-148">[Video: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)</span></span>
* <span data-ttu-id="9e580-149">[Vídeo: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462) (Integración de los sistemas con Azure Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="9e580-149">[Video: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)</span></span>
