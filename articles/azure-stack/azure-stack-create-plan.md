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
ms.openlocfilehash: 30759dca746fd7fd02653556cb105f419f5bf854
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="e223f-103">Creación de un plan en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e223f-103">Create a plan in Azure Stack</span></span>

<span data-ttu-id="e223f-104">*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="e223f-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="e223f-105">Los [planes](azure-stack-key-features.md) son agrupaciones de uno o varios servicios.</span><span class="sxs-lookup"><span data-stu-id="e223f-105">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="e223f-106">Como proveedor puede crear planes y ofrecérselos a sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="e223f-106">As a provider, you can create plans to offer to your users.</span></span> <span data-ttu-id="e223f-107">A su vez, los usuarios se suscriben a las ofertas para usar los planes y los servicios que incluyen.</span><span class="sxs-lookup"><span data-stu-id="e223f-107">In turn, your users subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="e223f-108">Este ejemplo muestra cómo crear un plan que incluya a los proveedores de recursos de proceso, de red y de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e223f-108">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span></span> <span data-ttu-id="e223f-109">Este plan ofrece a los suscriptores la capacidad de aprovisionar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e223f-109">This plan gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="e223f-110">Inicie sesión en el portal de administrador de Azure Stack (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="e223f-110">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="e223f-111">Escriba las credenciales de la cuenta que creó en el paso 5 de la sección [Ejecución del script de PowerShell](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="e223f-111">Enter the credentials for the account that you created during step 5 of the [Run the PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="e223f-112">Para crear un plan y una oferta a la que los usuarios puedan suscribirse, haga clic en **Nuevo** > **Ofertas y planes de inquilino** > **Plan**.</span><span class="sxs-lookup"><span data-stu-id="e223f-112">To create a plan and offer that users can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="e223f-113">En la hoja **Nuevo plan**, rellene **Nombre para mostrar** y **Nombre de recurso**.</span><span class="sxs-lookup"><span data-stu-id="e223f-113">In the **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="e223f-114">El nombre para mostrar es el nombre descriptivo del plan que ven los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e223f-114">The Display Name is the plan's friendly name that users see.</span></span> <span data-ttu-id="e223f-115">Solo el administrador puede ver el nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="e223f-115">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="e223f-116">Es el nombre que usan los administradores para trabajar con el plan como un recurso de Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e223f-116">It's the name that admins use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="e223f-117">Cree un nuevo **Grupo de recursos** o seleccione uno existente, como contenedor para el plan.</span><span class="sxs-lookup"><span data-stu-id="e223f-117">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="e223f-118">Haga clic en **Servicios**, seleccione **Microsoft.Compute**, **Microsoft.Network** y **Microsoft.Storage** y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="e223f-118">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="e223f-119">Haga clic en **Cuotas**, haga clic en **Microsoft.Storage (local)** y, a continuación, seleccione la cuota predeterminada o haga clic en **Crear nueva cuota** para personalizar la cuota.</span><span class="sxs-lookup"><span data-stu-id="e223f-119">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="e223f-120">Si va a crear una nueva cuota, escriba un nombre para la cuota > establezca los valores de la cuota > haga clic en **Aceptar** > haga clic en el nombre de la nueva cuota.</span><span class="sxs-lookup"><span data-stu-id="e223f-120">If you're creating a new quota, enter a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="e223f-121">Haga clic en **Microsoft.Network (local)** y, a continuación, seleccione la cuota predeterminada o haga clic en **Crear nueva cuota** para personalizar la cuota.</span><span class="sxs-lookup"><span data-stu-id="e223f-121">Click **Microsoft.Network (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="e223f-122">Si va a crear una nueva cuota, escriba un nombre para la cuota > establezca los valores de la cuota > haga clic en **Aceptar** > haga clic en el nombre de la nueva cuota.</span><span class="sxs-lookup"><span data-stu-id="e223f-122">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="e223f-123">Haga clic en **Microsoft.Compute (local)** y, a continuación, seleccione la cuota predeterminada o haga clic en **Crear nueva cuota** para personalizar la cuota.</span><span class="sxs-lookup"><span data-stu-id="e223f-123">Click **Microsoft.Compute (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="e223f-124">Si va a crear una nueva cuota, escriba un nombre para la cuota > establezca los valores de la cuota > haga clic en **Aceptar** > haga clic en el nombre de la nueva cuota.</span><span class="sxs-lookup"><span data-stu-id="e223f-124">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="e223f-125">En la hoja **Cuotas**, haga clic en **Aceptar** y, a continuación, en la hoja **Nuevo plan** y haga clic en **Crear** para crear el plan.</span><span class="sxs-lookup"><span data-stu-id="e223f-125">In the **Quotas** blade, click **OK**, and then in the **New Plan** blade, click **Create** to create the plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="e223f-126">Para ver el nuevo plan, haga clic en **Todos los recursos**, a continuación, busque el plan y haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="e223f-126">To see your new plan, click **All resources**, then search for the plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="e223f-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e223f-127">Next steps</span></span>
[<span data-ttu-id="e223f-128">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="e223f-128">Create an offer</span></span>](azure-stack-create-offer.md)
