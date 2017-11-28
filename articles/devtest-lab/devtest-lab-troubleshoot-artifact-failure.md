---
title: errores de artefacto aaaDiagnose en VM de laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot errores de artefactos en los laboratorios de desarrollo y pruebas"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a><span data-ttu-id="f47a8-103">Diagnosticar errores de artefacto en laboratorio Hola</span><span class="sxs-lookup"><span data-stu-id="f47a8-103">Diagnose artifact failures in hello lab</span></span> 
<span data-ttu-id="f47a8-104">Después de haber creado un artefacto, puede comprobar toosee si realizó correctamente o no.</span><span class="sxs-lookup"><span data-stu-id="f47a8-104">After you have created an artifact, you can check toosee if it succeeded or failed.</span></span> <span data-ttu-id="f47a8-105">Registros de artefactos en los laboratorios de desarrollo y pruebas proporcionan información que puede usar toodiagnose un error de artefacto.</span><span class="sxs-lookup"><span data-stu-id="f47a8-105">Artifact logs in DevTest Labs provide information you can use toodiagnose an artifact failure.</span></span> <span data-ttu-id="f47a8-106">Hay un par de formas diferentes puede ver la información de registro de hello artefacto de una VM de Windows.</span><span class="sxs-lookup"><span data-stu-id="f47a8-106">There are a couple different ways you can view hello artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="f47a8-107">tooensure que los errores correctamente se identifican y se ha explicado, es importante ese artefacto Hola está estructurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f47a8-107">tooensure that failures are correctly identified and explained, it is important that hello artifact is properly structured.</span></span> <span data-ttu-id="f47a8-108">Para obtener información acerca de cómo toocorrectly crea un artefacto, consulte [crear artefactos personalizados](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="f47a8-108">For information about how toocorrectly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="f47a8-109">Y toosee un ejemplo de un artefacto correctamente estructurado, consulte esta [tipos de parámetros de prueba](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefacto.</span><span class="sxs-lookup"><span data-stu-id="f47a8-109">And toosee an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a><span data-ttu-id="f47a8-110">Solucionar problemas de errores de artefacto mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f47a8-110">Troubleshoot artifact failures using hello Azure portal</span></span>
<span data-ttu-id="f47a8-111">errores de Azure toodiagnose portal toouse Hola durante la creación de artefacto, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f47a8-111">toouse hello Azure portal toodiagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="f47a8-112">En lista de Hola de recursos, seleccione el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="f47a8-112">From hello list of resources, select your lab.</span></span>

2. <span data-ttu-id="f47a8-113">Elija Hola VM de Windows que incluye el artefacto de hello desea tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="f47a8-113">Choose hello Windows VM that includes hello artifact you want tooinvestigate.</span></span>

3. <span data-ttu-id="f47a8-114">En el panel izquierdo de hello en **GENERAL**, elija **artefactos**.</span><span class="sxs-lookup"><span data-stu-id="f47a8-114">In hello left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="f47a8-115">Aparece una lista de artefactos asociados a esa máquina virtual, lo que indica nombre Hola de artefacto de Hola y su estado.</span><span class="sxs-lookup"><span data-stu-id="f47a8-115">A list of artifacts associated with that VM appears, indicating hello name of hello artifact and its status.</span></span>

   ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="f47a8-117">Elija un artefacto que muestre un estado de **Con error**.</span><span class="sxs-lookup"><span data-stu-id="f47a8-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="f47a8-118">artefacto de Hola se abre y muestra un mensaje de extensión que incluye detalles sobre los errores de Hola de artefacto de Hola.</span><span class="sxs-lookup"><span data-stu-id="f47a8-118">hello artifact opens and shows an extension message that includes details about hello failure of hello artifact.</span></span>

   ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a><span data-ttu-id="f47a8-120">Solucionar errores de artefactos desde dentro de hello VM</span><span class="sxs-lookup"><span data-stu-id="f47a8-120">Troubleshoot artifact failures from within hello VM</span></span>
<span data-ttu-id="f47a8-121">los registros de artefacto de Hola de tooview desde dentro de la máquina virtual de hello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f47a8-121">tooview hello artifact logs from within hello virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="f47a8-122">Inicie sesión en la máquina virtual que contiene el artefacto de hello desea toodiagnose toohello.</span><span class="sxs-lookup"><span data-stu-id="f47a8-122">Log in toohello VM that contains hello artifact you want toodiagnose.</span></span>

2. <span data-ttu-id="f47a8-123">Navegue tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status donde "1.9 es el número de versión de Hola CSE.</span><span class="sxs-lookup"><span data-stu-id="f47a8-123">Navigate tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is hello CSE version number.</span></span>

   ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="f47a8-125">Abra hello **estado** archivo tooview la información que ayuda a diagnosticar errores de artefacto de esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f47a8-125">Open hello **status** file tooview information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="f47a8-126">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="f47a8-126">Related blog posts</span></span>
* [<span data-ttu-id="f47a8-127">Unirse a un dominio de Active Directory mediante una plantilla de administrador de recursos en los laboratorios de desarrollo y pruebas de Azure tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="f47a8-127">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="f47a8-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f47a8-128">Next steps</span></span>
* <span data-ttu-id="f47a8-129">Obtenga información acerca de cómo demasiado[agregar un laboratorio de tooa del repositorio de Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="f47a8-129">Learn how too[add a Git repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

