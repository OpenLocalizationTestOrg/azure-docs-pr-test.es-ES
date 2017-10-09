---
title: plantillas de aaaDeploy con Visual Studio en la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy plantillas con Visual Studio en la pila de Azure."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: aea917b585a30ef4fbe7263db66f0659b56b21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a><span data-ttu-id="69bcd-103">Implementación de plantillas en Azure Stack con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="69bcd-103">Deploy templates in Azure Stack using Visual Studio</span></span>

<span data-ttu-id="69bcd-104">Utilice las kit de desarrollo de Visual Studio toodeploy Azure Resource Manager plantillas toohello pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="69bcd-104">Use Visual Studio toodeploy Azure Resource Manager templates toohello Azure Stack development kit.</span></span>

1. <span data-ttu-id="69bcd-105">[Instalar y conectar](azure-stack-install-visual-studio.md) tooAzure pila con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69bcd-105">[Install and connect](azure-stack-install-visual-studio.md) tooAzure Stack with Visual Studio.</span></span>
2. <span data-ttu-id="69bcd-106">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69bcd-106">Open Visual Studio.</span></span>
3. <span data-ttu-id="69bcd-107">Haga clic en **archivo**, haga clic en **New**y en hello **nuevo proyecto** haga clic en el cuadro de diálogo **grupo de recursos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="69bcd-107">Click **File**, click **New**, and in hello **New Project** dialog box click **Azure Resource Group**.</span></span>
4. <span data-ttu-id="69bcd-108">Escriba un **nombre** para hello nuevos proyectos y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="69bcd-108">Enter a **Name** for hello new project, and then click **OK**.</span></span>
5. <span data-ttu-id="69bcd-109">Hola **Seleccionar plantilla de Azure** cuadro de diálogo, cambio hello *mostrar plantillas desde esta ubicación* desplegable demasiado**inicio rápido de pila de Azure**</span><span class="sxs-lookup"><span data-stu-id="69bcd-109">In hello **Select Azure Template** dialog box, change hello *Show templates from this location* drop-down too**Azure Stack Quickstart**</span></span>
6. <span data-ttu-id="69bcd-110">Haga clic en **101-create-storage-account** y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="69bcd-110">Click **101-create-storage-account**, and then click **OK**.</span></span>  
7. <span data-ttu-id="69bcd-111">En el proyecto nuevo, puede ver una lista de plantillas de hello disponibles expandiendo hello **plantillas** nodo Hola **el Explorador de soluciones** panel.</span><span class="sxs-lookup"><span data-stu-id="69bcd-111">In your new project, you can see a list of hello templates available by expanding hello **Templates** node in hello **Solution Explorer** pane.</span></span>
8. <span data-ttu-id="69bcd-112">Hola **el Explorador de soluciones** panel, nombre de Hola de menú contextual del proyecto, haga clic en **implementar**, a continuación, haga clic en **nueva implementación**.</span><span class="sxs-lookup"><span data-stu-id="69bcd-112">In hello **Solution Explorer** pane, right-click hello name of your project, click **Deploy**, then click **New Deployment**.</span></span>
9. <span data-ttu-id="69bcd-113">Hola **implementar tooResource grupo** cuadro de diálogo hello **suscripción** lista desplegable, seleccione la suscripción de la pila de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="69bcd-113">In hello **Deploy tooResource Group** dialog box, in hello **Subscription** drop-down, select your Microsoft Azure Stack subscription.</span></span>
10. <span data-ttu-id="69bcd-114">Hola **grupo de recursos** lista, elija un grupo de recursos existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="69bcd-114">In hello **Resource Group** list, choose an existing resource group or create a new one.</span></span>
11. <span data-ttu-id="69bcd-115">Hola **ubicación del grupo de recursos** lista, elija una ubicación y, a continuación, haga clic en **implementar**.</span><span class="sxs-lookup"><span data-stu-id="69bcd-115">In hello **Resource group location** list, choose a location, and then click **Deploy**.</span></span>
12. <span data-ttu-id="69bcd-116">Hola **editar parámetros** diálogo cuadro, escriba valores para los parámetros de hello (que varían según la plantilla) y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="69bcd-116">In hello **Edit Parameters** dialog box, enter values for hello parameters (which vary by template), and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69bcd-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69bcd-117">Next steps</span></span>
[<span data-ttu-id="69bcd-118">Implementación de plantillas de línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="69bcd-118">Deploy templates with hello command line</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="69bcd-119">Desarrollo de plantillas para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="69bcd-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)

