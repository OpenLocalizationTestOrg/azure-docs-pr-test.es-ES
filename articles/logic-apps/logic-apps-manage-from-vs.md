---
title: "aplicaciones de la lógica de aaaManage en Visual Studio: las aplicaciones lógicas de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="ac351-103">Administración de sus aplicaciones lógicas con Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="ac351-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="ac351-104">Aunque hello [portal de Azure](https://portal.azure.com/) ofrece una excelente manera de que toodesign y administrar las aplicaciones lógicas de Azure, puede usar el Explorador de Visual Studio en la nube para administrar muchos de los activos de Azure, incluidas las aplicaciones de lógica.</span><span class="sxs-lookup"><span data-stu-id="ac351-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="ac351-105">Visual Studio Cloud Explorer le permite explorar, administrar, editar y descargar aplicaciones lógicas publicadas.</span><span class="sxs-lookup"><span data-stu-id="ac351-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="ac351-106">Las tareas de administración incluyen habilitar, deshabilitar y ver el historial de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="ac351-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="ac351-107">Para poder acceder a las aplicaciones lógicas y administrarlas en Visual Studio, instale y configure estas herramientas de Visual Studio para Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="ac351-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ac351-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ac351-108">Prerequisites</span></span>

* [<span data-ttu-id="ac351-109">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ac351-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="ac351-110">[SDK de Azure más reciente](https://azure.microsoft.com/downloads/) (2.9.1 o superior)</span><span class="sxs-lookup"><span data-stu-id="ac351-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="ac351-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="ac351-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="ac351-112">Web toohello de acceso al usar el Diseñador de hello incrustado</span><span class="sxs-lookup"><span data-stu-id="ac351-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="ac351-113">Instalación de herramientas de Visual Studio para Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ac351-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="ac351-114">Después de instalar requisitos previos de hello, descargar e instalar aplicaciones de lógica de hello Azure Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ac351-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="ac351-115">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ac351-115">Open Visual Studio.</span></span> <span data-ttu-id="ac351-116">En hello **herramientas** menú, seleccione **extensiones y actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="ac351-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="ac351-117">Expanda hello **Online** categoría para que puedan buscar en línea en hello Galería de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ac351-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="ac351-118">Busque **Logic Apps** hasta que encuentre las **herramientas de Azure Logic Apps para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="ac351-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="ac351-119">toodownload y la extensión de Hola de instalación, haga clic en **descargar**.</span><span class="sxs-lookup"><span data-stu-id="ac351-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="ac351-120">Reinicie Visual Studio después de la instalación.</span><span class="sxs-lookup"><span data-stu-id="ac351-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="ac351-121">Hola toodownload aplicaciones de lógica de Azure Tools para Visual Studio ir directamente, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="ac351-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="ac351-122">Búsqueda de aplicaciones lógicas en Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="ac351-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="ac351-123">tooopen el explorador en la nube, en hello **vista** menú, elija **nube explorador**.</span><span class="sxs-lookup"><span data-stu-id="ac351-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="ac351-124">Busque la aplicación lógica. Puede hacerlo por grupo de recursos o por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="ac351-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="ac351-125">Si se desplaza por tipo de recurso, seleccione la suscripción de Azure, expanda hello **Logic Apps** sección y seleccionar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ac351-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="ac351-126">Si se desplaza por grupo de recursos, expanda grupo de recursos de Hola que tiene la aplicación lógica y seleccione la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ac351-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="ac351-127">tooview comandos para la aplicación lógica, haga clic en la aplicación lógica, o final Hola de explorador en la nube, elija de hello **acciones** menú.</span><span class="sxs-lookup"><span data-stu-id="ac351-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![Búsqueda de su aplicación lógica](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="ac351-129">Edición de la aplicación lógica con el Diseñador de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ac351-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="ac351-130">Desde el Explorador de la nube, puede abrir una aplicación de la lógica implementada actualmente en hello mismo diseñador que se utiliza en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac351-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="ac351-131">tooedit la lógica de aplicación, en el explorador en la nube, haga clic en la aplicación lógica y seleccione **abierto con el Editor de aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="ac351-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="ac351-132">toopublish su toohello actualizaciones en la nube, elija **publicar**.</span><span class="sxs-lookup"><span data-stu-id="ac351-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="ac351-133">toostart una nueva ejecución, elija **desencadenador ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="ac351-133">toostart a new run, choose **Run Trigger**.</span></span>

![Diseñador de Logic Apps](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="ac351-135">Desde el Diseñador de hello, también puede **descargar** una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ac351-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="ac351-136">Esta acción automáticamente parametriza la definición de aplicación lógica de Hola y guarda la definición de hello como una plantilla de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ac351-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="ac351-137">Puede agregar este proyecto de grupo de recursos de Azure de tooyour de plantilla de implementación.</span><span class="sxs-lookup"><span data-stu-id="ac351-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="ac351-138">Búsqueda del historial de ejecución de su aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="ac351-138">Browse your logic app run history</span></span>

<span data-ttu-id="ac351-139">Hola tooview historial para la aplicación de la lógica de ejecución haga clic en la aplicación lógica y seleccione **historial de ejecución de abrir**.</span><span class="sxs-lookup"><span data-stu-id="ac351-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="ac351-140">tooreorder su historial de ejecución se basa en cualquier encabezado de columna de Hola se muestra, seleccione Propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac351-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![Historial de ejecuciones](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="ac351-142">Hola tooshow historial de una instancia de ejecución para poder revisar Hola ejecutar resultados, incluidas Hola entradas y salidas de cada paso, haga doble clic en uno de hello ejecutar instancias.</span><span class="sxs-lookup"><span data-stu-id="ac351-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![Resultados del historial de ejecuciones, entradas y salidas de los pasos](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="ac351-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac351-144">Next steps</span></span>

* [<span data-ttu-id="ac351-145">Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS</span><span class="sxs-lookup"><span data-stu-id="ac351-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="ac351-146">Creación e implementación de aplicaciones lógicas en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac351-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="ac351-147">Ejemplos de aplicaciones lógicas y escenarios comunes</span><span class="sxs-lookup"><span data-stu-id="ac351-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* <span data-ttu-id="ac351-148">[Vídeo: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) (Automatización de los procesos de negocio con Azure Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="ac351-148">[Video: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)</span></span>
* <span data-ttu-id="ac351-149">[Vídeo: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462) (Integración de los sistemas con Azure Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="ac351-149">[Video: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)</span></span>
