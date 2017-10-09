---
title: "aaaCreate una prueba de la máquina virtual en la pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprovision una prueba de la máquina virtual en la pila de Azure como un operador en la nube."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/21/2017
ms.author: erikje
ms.openlocfilehash: 9633cc20852e16283ad4522da78971133028efdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="97374-103">Creación de una máquina virtual en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="97374-103">Create a test virtual machine in Azure Stack</span></span>
<span data-ttu-id="97374-104">Como un operador en la nube, puede crear un toovalidate de máquina virtual de prueba de la implementación de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="97374-104">As a cloud operator, you can create a test virtual machine toovalidate your Azure Stack deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="97374-105">Antes de poder aprovisionar máquinas virtuales, debe [agregar marketplace de pila de Azure de hello evaluación de Windows Server 2016 imagen toohello](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="97374-105">Before you can provision virtual machines, you must [add hello Windows Server 2016 Evaluation image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="97374-106">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="97374-106">Create a virtual machine</span></span>
1. <span data-ttu-id="97374-107">En el host del Kit de desarrollo de pila de Azure de hello, [iniciar sesión en](azure-stack-connect-azure-stack.md) toohello portal del administrador (`https://adminportal.local.azurestack.external`) y, a continuación, haga clic en **New** > **proceso**  >  **Datacenter de Windows Server 2016 Eval** > **crear**.</span><span class="sxs-lookup"><span data-stu-id="97374-107">On hello Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) toohello administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="97374-108">Hola **Fundamentos** hoja, escriba un **nombre**, **nombre de usuario**, y **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="97374-108">In hello **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="97374-109">Elija una **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="97374-109">Choose a **Subscription**.</span></span> <span data-ttu-id="97374-110">Cree un **grupo de recursos** o seleccione uno existente y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="97374-110">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="97374-111">Hola **elegir un tamaño de** hoja, haga clic en **estándar A1**y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="97374-111">In hello **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="97374-112">Hola **configuración** hoja, acepte los valores predeterminados de Hola y haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="97374-112">In hello **Settings** blade, accept hello defaults and click **OK**</span></span>
5. <span data-ttu-id="97374-113">Hola **resumen** hoja, haga clic en **Aceptar** máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="97374-113">In hello **Summary** blade, click **OK** toocreate hello virtual machine.</span></span>  
6. <span data-ttu-id="97374-114">toosee la nueva máquina virtual, haga clic en **todos los recursos**, a continuación, busque la máquina virtual de Hola y haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="97374-114">toosee your new virtual machine, click **All resources**, then search for hello virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="97374-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97374-115">Next steps</span></span>
[<span data-ttu-id="97374-116">Uso de portales de administrador y usuario de hello en la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="97374-116">Using hello administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
