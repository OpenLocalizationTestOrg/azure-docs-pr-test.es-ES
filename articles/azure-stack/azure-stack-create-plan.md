---
title: "Creación de un plan en Azure Stack | Microsoft Docs"
description: "Como administrador de la nube, cree un plan que permita a los suscriptores aprovisionar máquinas virtuales."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: ff34bcd6ba485806baf7963e11393633dd893fa7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="e1601-103">Creación de un plan en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e1601-103">Create a plan in Azure Stack</span></span>
<span data-ttu-id="e1601-104">Los [planes](azure-stack-key-features.md) son agrupaciones de uno o varios servicios.</span><span class="sxs-lookup"><span data-stu-id="e1601-104">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="e1601-105">Como proveedor puede crear planes y ofrecérselos a sus inquilinos.</span><span class="sxs-lookup"><span data-stu-id="e1601-105">As a provider, you can create plans to offer to your tenants.</span></span> <span data-ttu-id="e1601-106">A su vez, los inquilinos se suscriben a las ofertas para usar los planes y servicios que incluyen.</span><span class="sxs-lookup"><span data-stu-id="e1601-106">In turn, your tenants subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="e1601-107">Este ejemplo muestra cómo crear un plan que incluya a los proveedores de recursos de proceso, de red y de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e1601-107">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span></span> <span data-ttu-id="e1601-108">Este plan ofrece a los suscriptores la capacidad de aprovisionar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e1601-108">This plan gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="e1601-109">Inicie sesión en el portal de administrador de Azure Stack (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="e1601-109">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="e1601-110">Escriba las credenciales de la cuenta que creó en el paso 5 de la sección [Ejecución del script de PowerShell](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="e1601-110">Enter the credentials for the account that you created during step 5 of the [Run the PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="e1601-111">Para crear un plan y una oferta a la que los inquilinos puedan suscribirse, haga clic en **Nuevo** > **Ofertas y planes de inquilino** > **Plan**.</span><span class="sxs-lookup"><span data-stu-id="e1601-111">To create a plan and offer that tenants can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="e1601-112">En la hoja **Nuevo plan**, rellene **Nombre para mostrar** y **Nombre de recurso**.</span><span class="sxs-lookup"><span data-stu-id="e1601-112">In the **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="e1601-113">El Nombre para mostrar es el nombre descriptivo del plan que ven los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="e1601-113">The Display Name is the plan's friendly name that tenants see.</span></span> <span data-ttu-id="e1601-114">Solo el administrador puede ver el nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="e1601-114">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="e1601-115">Es el nombre que usan los administradores para trabajar con el plan como un recurso de Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1601-115">It's the name that admins use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="e1601-116">Cree un nuevo **Grupo de recursos** o seleccione uno existente, como contenedor para el plan.</span><span class="sxs-lookup"><span data-stu-id="e1601-116">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="e1601-117">Haga clic en **Servicios**, seleccione **Microsoft.Compute**, **Microsoft.Network** y **Microsoft.Storage** y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="e1601-117">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="e1601-118">Haga clic en **Cuotas**, haga clic en **Microsoft.Storage (local)** y, a continuación, seleccione la cuota predeterminada o haga clic en **Crear nueva cuota** para personalizar la cuota.</span><span class="sxs-lookup"><span data-stu-id="e1601-118">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="e1601-119">Si va a crear una nueva cuota, escriba un nombre para la cuota > establezca los valores de la cuota > haga clic en **Aceptar** > haga clic en el nombre de la nueva cuota.</span><span class="sxs-lookup"><span data-stu-id="e1601-119">If you're creating a new quota, enter a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="e1601-120">Haga clic en **Microsoft.Network (local)** y, a continuación, seleccione la cuota predeterminada o haga clic en **Crear nueva cuota** para personalizar la cuota.</span><span class="sxs-lookup"><span data-stu-id="e1601-120">Click **Microsoft.Network (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="e1601-121">Si va a crear una nueva cuota, escriba un nombre para la cuota > establezca los valores de la cuota > haga clic en **Aceptar** > haga clic en el nombre de la nueva cuota.</span><span class="sxs-lookup"><span data-stu-id="e1601-121">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="e1601-122">Haga clic en **Microsoft.Compute (local)** y, a continuación, seleccione la cuota predeterminada o haga clic en **Crear nueva cuota** para personalizar la cuota.</span><span class="sxs-lookup"><span data-stu-id="e1601-122">Click **Microsoft.Compute (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="e1601-123">Si va a crear una nueva cuota, escriba un nombre para la cuota > establezca los valores de la cuota > haga clic en **Aceptar** > haga clic en el nombre de la nueva cuota.</span><span class="sxs-lookup"><span data-stu-id="e1601-123">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="e1601-124">En la hoja **Cuotas**, haga clic en **Aceptar** y, a continuación, en la hoja **Nuevo plan** y haga clic en **Crear** para crear el plan.</span><span class="sxs-lookup"><span data-stu-id="e1601-124">In the **Quotas** blade, click **OK**, and then in the **New Plan** blade, click **Create** to create the plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="e1601-125">Para ver el nuevo plan, haga clic en **Todos los recursos**, a continuación, busque el plan y haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="e1601-125">To see your new plan, click **All resources**, then search for the plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="e1601-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1601-126">Next steps</span></span>
[<span data-ttu-id="e1601-127">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="e1601-127">Create an offer</span></span>](azure-stack-create-offer.md)
