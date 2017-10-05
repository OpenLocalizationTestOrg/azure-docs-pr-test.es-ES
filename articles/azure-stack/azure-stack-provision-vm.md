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
ms.date: 7/21/2017
ms.author: erikje
ms.openlocfilehash: 4e3f90fe35b7fb2509db0eb7a467305f4c4167ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="2dd01-103">Creación de una máquina virtual en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2dd01-103">Create a test virtual machine in Azure Stack</span></span>
<span data-ttu-id="2dd01-104">Como un operador en la nube, puede crear una máquina virtual de prueba para validar la implementación de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2dd01-104">As a cloud operator, you can create a test virtual machine to validate your Azure Stack deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="2dd01-105">Antes de poder aprovisionar las máquinas virtuales, debe [agregar la imagen de evaluación de Windows Server 2016 en Marketplace de Azure Stack](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="2dd01-105">Before you can provision virtual machines, you must [add the Windows Server 2016 Evaluation image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="2dd01-106">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2dd01-106">Create a virtual machine</span></span>
1. <span data-ttu-id="2dd01-107">En servidor host de Azure Stack Development Kit, [inicie sesión en](azure-stack-connect-azure-stack.md) el portal del administrador (`https://adminportal.local.azurestack.external`) y, a continuación, haga clic en **Nuevo** > **Proceso** > **Windows Server 2016 Datacenter Eval** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2dd01-107">On the Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) to the administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="2dd01-108">En la hoja **Aspectos básicos**, escriba un **Nombre**, **Nombre de usuario** y **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2dd01-108">In the **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="2dd01-109">Elija una **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="2dd01-109">Choose a **Subscription**.</span></span> <span data-ttu-id="2dd01-110">Cree un **grupo de recursos** o seleccione uno existente y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2dd01-110">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="2dd01-111">En la hoja **Elegir un tamaño**, haga clic en **A1 Estándar** y, después, en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="2dd01-111">In the **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="2dd01-112">En la hoja de **configuración**, acepte los valores predeterminados y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2dd01-112">In the **Settings** blade, accept the defaults and click **OK**</span></span>
5. <span data-ttu-id="2dd01-113">En la hoja **Resumen**, haga clic en **Aceptar** para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2dd01-113">In the **Summary** blade, click **OK** to create the virtual machine.</span></span>  
6. <span data-ttu-id="2dd01-114">Para ver la nueva máquina virtual, haga clic en **Todos los recursos** y, a continuación, busque la máquina virtual y haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="2dd01-114">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="2dd01-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2dd01-115">Next steps</span></span>
[<span data-ttu-id="2dd01-116">Usar los portales de administración y de usuarios en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2dd01-116">Using the administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
