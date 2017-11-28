---
title: "Implementación de plantillas con Visual Studio en Azure Stack | Microsoft Docs"
description: Aprenda a implementar las plantillas con Visual Studio en Azure Stack.
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
ms.openlocfilehash: e9b467f47f166198d9790f19dbdd3d1d0fd79947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a><span data-ttu-id="190d4-103">Implementación de plantillas en Azure Stack con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="190d4-103">Deploy templates in Azure Stack using Visual Studio</span></span>

<span data-ttu-id="190d4-104">Use Visual Studio para implementar plantillas de Azure Resource Manager en el kit de desarrollo de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="190d4-104">Use Visual Studio to deploy Azure Resource Manager templates to the Azure Stack development kit.</span></span>

1. <span data-ttu-id="190d4-105">[Instale Azure Stack y conéctese](azure-stack-install-visual-studio.md) a esta infraestructura con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="190d4-105">[Install and connect](azure-stack-install-visual-studio.md) to Azure Stack with Visual Studio.</span></span>
2. <span data-ttu-id="190d4-106">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="190d4-106">Open Visual Studio.</span></span>
3. <span data-ttu-id="190d4-107">Haga clic en **Archivo**, en **Nuevo** y, en el cuadro de diálogo **Nuevo proyecto**, haga clic en **Grupo de recursos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="190d4-107">Click **File**, click **New**, and in the **New Project** dialog box click **Azure Resource Group**.</span></span>
4. <span data-ttu-id="190d4-108">Escriba un **nombre** para el nuevo proyecto y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="190d4-108">Enter a **Name** for the new project, and then click **OK**.</span></span>
5. <span data-ttu-id="190d4-109">En el cuadro de diálogo **Seleccionar plantilla de Azure**, cambie la lista desplegable *Mostrar plantillas de esta ubicación* a **Azure Stack Quickstart** (Inicio rápido de Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="190d4-109">In the **Select Azure Template** dialog box, change the *Show templates from this location* drop-down to **Azure Stack Quickstart**</span></span>
6. <span data-ttu-id="190d4-110">Haga clic en **101-create-storage-account** y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="190d4-110">Click **101-create-storage-account**, and then click **OK**.</span></span>  
7. <span data-ttu-id="190d4-111">En el nuevo proyecto, puede ver una lista de plantillas disponibles expandiendo el nodo **Plantillas** en el panel **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="190d4-111">In your new project, you can see a list of the templates available by expanding the **Templates** node in the **Solution Explorer** pane.</span></span>
8. <span data-ttu-id="190d4-112">En el panel **Explorador de soluciones**, haga clic con el botón derecho en el nombre del proyecto, haga clic en **Implementar** y, finalmente, en **Nueva implementación**.</span><span class="sxs-lookup"><span data-stu-id="190d4-112">In the **Solution Explorer** pane, right-click the name of your project, click **Deploy**, then click **New Deployment**.</span></span>
9. <span data-ttu-id="190d4-113">En el cuadro de diálogo **Implementar en grupo de recursos**, en la lista desplegable **Suscripción**, seleccione la suscripción de Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="190d4-113">In the **Deploy to Resource Group** dialog box, in the **Subscription** drop-down, select your Microsoft Azure Stack subscription.</span></span>
10. <span data-ttu-id="190d4-114">En la lista **Grupo de recursos** , elija un grupo de recursos existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="190d4-114">In the **Resource Group** list, choose an existing resource group or create a new one.</span></span>
11. <span data-ttu-id="190d4-115">En la lista **Ubicación del grupo de recursos**, elija una ubicación y haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="190d4-115">In the **Resource group location** list, choose a location, and then click **Deploy**.</span></span>
12. <span data-ttu-id="190d4-116">En el cuadro de diálogo **Editar parámetros**, escriba los valores para los parámetros (que varían según la plantilla) y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="190d4-116">In the **Edit Parameters** dialog box, enter values for the parameters (which vary by template), and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="190d4-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="190d4-117">Next steps</span></span>
[<span data-ttu-id="190d4-118">Implementación de plantillas con la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="190d4-118">Deploy templates with the command line</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="190d4-119">Desarrollo de plantillas para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="190d4-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)

