---
title: aaaCreate un plan en la pila de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 3665bae5d212002da43316e62ce73686b4c66eea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="f8d52-103">Creación de un plan en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f8d52-103">Create a plan in Azure Stack</span></span>
<span data-ttu-id="f8d52-104">Los [planes](azure-stack-key-features.md) son agrupaciones de uno o varios servicios.</span><span class="sxs-lookup"><span data-stu-id="f8d52-104">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="f8d52-105">Como proveedor, puede crear planes de inquilinos de tooyour toooffer.</span><span class="sxs-lookup"><span data-stu-id="f8d52-105">As a provider, you can create plans toooffer tooyour tenants.</span></span> <span data-ttu-id="f8d52-106">A su vez, los inquilinos suscribirán tooyour ofertas toouse Hola planes y servicios que se incluyen.</span><span class="sxs-lookup"><span data-stu-id="f8d52-106">In turn, your tenants subscribe tooyour offers toouse hello plans and services they include.</span></span> <span data-ttu-id="f8d52-107">Este ejemplo muestra cómo toocreate un plan que incluya Hola proveedores de recursos de proceso, red y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f8d52-107">This example shows you how toocreate a plan that includes hello compute, network, and storage resource providers.</span></span> <span data-ttu-id="f8d52-108">Este plan ofrece a los suscriptores Hola capacidad tooprovision las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f8d52-108">This plan gives subscribers hello ability tooprovision virtual machines.</span></span>

1. <span data-ttu-id="f8d52-109">Inicie sesión en toohello portal del Administrador de pila de Azure (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="f8d52-109">Sign in toohello Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="f8d52-110">Escriba credenciales de Hola de cuenta de hello que creó durante el paso 5 de hello [ejecutar script de PowerShell de hello](azure-stack-run-powershell-script.md) sección.</span><span class="sxs-lookup"><span data-stu-id="f8d52-110">Enter hello credentials for hello account that you created during step 5 of hello [Run hello PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="f8d52-111">toocreate un plan y la oferta que los inquilinos pueden suscribirse a, haga clic en **New** > **inquilino ofrece + planes** > **Plan**.</span><span class="sxs-lookup"><span data-stu-id="f8d52-111">toocreate a plan and offer that tenants can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="f8d52-112">Hola **nuevo Plan** hoja, rellene **nombre para mostrar** y **nombre del recurso**.</span><span class="sxs-lookup"><span data-stu-id="f8d52-112">In hello **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="f8d52-113">Hola nombre para mostrar es el nombre descriptivo del plan de Hola que ven los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="f8d52-113">hello Display Name is hello plan's friendly name that tenants see.</span></span> <span data-ttu-id="f8d52-114">Hola, administrador solo puede ver Hola nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="f8d52-114">Only hello admin can see hello Resource Name.</span></span> <span data-ttu-id="f8d52-115">Su Hola nombre administradores usar toowork con hello plan como un recurso de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f8d52-115">It's hello name that admins use toowork with hello plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="f8d52-116">Crear un nuevo **grupo de recursos**, o seleccione uno existente, como un contenedor para el plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8d52-116">Create a new **Resource Group**, or select an existing one, as a container for hello plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="f8d52-117">Haga clic en **Servicios**, seleccione **Microsoft.Compute**, **Microsoft.Network** y **Microsoft.Storage** y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="f8d52-117">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="f8d52-118">Haga clic en **cuotas**, haga clic en **almacenamiento de Microsoft (local)**y, a continuación, ya sea Hola seleccione predeterminado de cuota o haga clic en **crear nueva cuota** cuota de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="f8d52-118">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="f8d52-119">Si va a crear una nueva cuota, escriba un nombre para la cuota de hello > establecer los valores de cuota de hello > haga clic en **Aceptar** > haga clic en nombre de Hola de cuota nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="f8d52-119">If you're creating a new quota, enter a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="f8d52-120">Haga clic en **Microsoft.Network (local)**y, a continuación, ya sea Hola seleccione predeterminado de cuota o haga clic en **crear nueva cuota** cuota de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="f8d52-120">Click **Microsoft.Network (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="f8d52-121">Si va a crear una nueva cuota, escriba un nombre para la cuota de hello > establecer los valores de cuota de hello > haga clic en **Aceptar** > haga clic en nombre de Hola de cuota nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="f8d52-121">If you're creating a new quota, type a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="f8d52-122">Haga clic en **Microsoft.Compute (local)**y, a continuación, ya sea Hola seleccione predeterminado de cuota o haga clic en **crear nueva cuota** cuota de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="f8d52-122">Click **Microsoft.Compute (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="f8d52-123">Si va a crear una nueva cuota, escriba un nombre para la cuota de hello > establecer los valores de cuota de hello > haga clic en **Aceptar** > haga clic en nombre de Hola de cuota nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="f8d52-123">If you're creating a new quota, type a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="f8d52-124">Hola **cuotas** hoja, haga clic en **Aceptar**y, a continuación, en hello **nuevo Plan** hoja, haga clic en **crear** plan de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f8d52-124">In hello **Quotas** blade, click **OK**, and then in hello **New Plan** blade, click **Create** toocreate hello plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="f8d52-125">toosee su nuevo plan, haga clic en **todos los recursos**, a continuación, busque el plan de Hola y haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="f8d52-125">toosee your new plan, click **All resources**, then search for hello plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="f8d52-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8d52-126">Next steps</span></span>
[<span data-ttu-id="f8d52-127">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="f8d52-127">Create an offer</span></span>](azure-stack-create-offer.md)
