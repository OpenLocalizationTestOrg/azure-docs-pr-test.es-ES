---
title: "Creación de una máquina virtual de prueba en Azure Stack | Microsoft Docs"
description: "Aprenda a aprovisionar una máquina virtual de prueba en Azure Stack como un operador en la nube."
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
ms.date: 9/25/2017
ms.author: erikje
ms.openlocfilehash: 233cf4df53af6a49e5fe4c5d51e112d8196a7530
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="9637c-103">Creación de una máquina virtual en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9637c-103">Create a test virtual machine in Azure Stack</span></span>

<span data-ttu-id="9637c-104">*Se aplica a: Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="9637c-104">*Applies to: Azure Stack Development Kit*</span></span>

<span data-ttu-id="9637c-105">Como operador de Azure Stack, puede crear una máquina virtual de prueba para validar la implementación de [Azure Stack](azure-stack-poc.md) Development Kit.</span><span class="sxs-lookup"><span data-stu-id="9637c-105">As an Azure Stack operator, you can create a test virtual machine to validate your [Azure Stack](azure-stack-poc.md) Developer Kit deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="9637c-106">Antes de poder aprovisionar las máquinas virtuales, debe [agregar la imagen de evaluación de Windows Server 2016 en Marketplace de Azure Stack](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="9637c-106">Before you can provision virtual machines, you must [add the Windows Server 2016 Evaluation image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="9637c-107">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9637c-107">Create a virtual machine</span></span>
1. <span data-ttu-id="9637c-108">En servidor host de Azure Stack Development Kit, [inicie sesión en](azure-stack-connect-azure-stack.md) el portal del administrador (`https://adminportal.local.azurestack.external`) y, a continuación, haga clic en **Nuevo** > **Proceso** > **Windows Server 2016 Datacenter Eval** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9637c-108">On the Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) to the administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="9637c-109">En la hoja **Aspectos básicos**, escriba un **Nombre**, **Nombre de usuario** y **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9637c-109">In the **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="9637c-110">Elija una **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="9637c-110">Choose a **Subscription**.</span></span> <span data-ttu-id="9637c-111">Cree un **grupo de recursos** o seleccione uno existente y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9637c-111">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="9637c-112">En la hoja **Elegir un tamaño**, haga clic en **A1 Estándar** y, después, en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="9637c-112">In the **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="9637c-113">En la hoja de **configuración**, acepte los valores predeterminados y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9637c-113">In the **Settings** blade, accept the defaults and click **OK**</span></span>
5. <span data-ttu-id="9637c-114">En la hoja **Resumen**, haga clic en **Aceptar** para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9637c-114">In the **Summary** blade, click **OK** to create the virtual machine.</span></span>  
6. <span data-ttu-id="9637c-115">Para ver la nueva máquina virtual, haga clic en **Todos los recursos** y, a continuación, busque la máquina virtual y haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="9637c-115">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="9637c-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9637c-116">Next steps</span></span>
[<span data-ttu-id="9637c-117">Usar los portales de administración y de usuarios en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9637c-117">Using the administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
