---
title: "los usuarios de aaaMake máquinas virtuales disponibles tooyour pila de Azure | Documentos de Microsoft"
description: "Máquinas virtuales de tutorial toomake disponibles en la pila de Azure"
services: azure-stack
documentationcenter: 
author: vhorne
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 345206912f17662e51341c71175c5fe87b692ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machines-available-tooyour-azure-stack-users"></a><span data-ttu-id="8ce96-103">Hacer tooyour disponibles de máquinas virtuales que los usuarios de la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="8ce96-103">Make virtual machines available tooyour Azure Stack users</span></span>
<span data-ttu-id="8ce96-104">Como administrador de la nube de una pila de Azure, puede crear ofertas que se pueden suscribir los usuarios (en ocasiones denominado tooas inquilinos).</span><span class="sxs-lookup"><span data-stu-id="8ce96-104">As an Azure Stack cloud administrator, you can create offers that your users (sometimes referred tooas tenants) can subscribe to.</span></span> <span data-ttu-id="8ce96-105">Con su suscripción, los usuarios podrán consumir servicios de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8ce96-105">Using their subscription, users can then consume Azure Stack services.</span></span>

<span data-ttu-id="8ce96-106">Este artículo muestra cómo toocreate una oferta y, a continuación, vuelva a probarlo.</span><span class="sxs-lookup"><span data-stu-id="8ce96-106">This article shows you how toocreate an offer, and then test it.</span></span> <span data-ttu-id="8ce96-107">Para pruebas de hello, se inicie sesión en el portal de toohello como un usuario, suscribirse toohello oferta y, a continuación, crear una máquina virtual mediante suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce96-107">For hello test, you will log in toohello portal as a user, subscribe toohello offer, and then create a virtual machine using hello subscription.</span></span>

<span data-ttu-id="8ce96-108">Lo qué aprenderá:</span><span class="sxs-lookup"><span data-stu-id="8ce96-108">What you will learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8ce96-109">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="8ce96-109">Create an offer</span></span>
> * <span data-ttu-id="8ce96-110">Añadir una imagen</span><span class="sxs-lookup"><span data-stu-id="8ce96-110">Add an image</span></span>
> * <span data-ttu-id="8ce96-111">Oferta de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="8ce96-111">Test hello offer</span></span>


<span data-ttu-id="8ce96-112">En la pila de Azure, servicios se entregan toousers mediante planes, ofertas y suscripciones.</span><span class="sxs-lookup"><span data-stu-id="8ce96-112">In Azure Stack, services are delivered toousers using subscriptions, offers, and plans.</span></span> <span data-ttu-id="8ce96-113">Los usuarios pueden suscribirse toomultiple ofertas.</span><span class="sxs-lookup"><span data-stu-id="8ce96-113">Users can subscribe toomultiple offers.</span></span> <span data-ttu-id="8ce96-114">Las ofertas pueden tener uno o varios planes, y los planes pueden tener uno o varios servicios.</span><span class="sxs-lookup"><span data-stu-id="8ce96-114">Offers can have one or more plans, and plans can have one or more services.</span></span>

![Planes, ofertas y suscripciones](media/azure-stack-key-features/image4.png)

<span data-ttu-id="8ce96-116">más información, consulte toolearn [principales características y conceptos de Azure pila](azure-stack-key-features.md).</span><span class="sxs-lookup"><span data-stu-id="8ce96-116">toolearn more, see [Key features and concepts in Azure Stack](azure-stack-key-features.md).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="8ce96-117">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="8ce96-117">Create an offer</span></span>

<span data-ttu-id="8ce96-118">Ahora puede preparar todo para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8ce96-118">Now you can get things ready for your users.</span></span> <span data-ttu-id="8ce96-119">Cuando se inicia el proceso de hello, es la primera oferta de hello toocreate solicitadas, a continuación, un plan y, finalmente, las cuotas.</span><span class="sxs-lookup"><span data-stu-id="8ce96-119">When you start hello process, you are first prompted toocreate hello offer, then a plan, and finally quotas.</span></span>

3. <span data-ttu-id="8ce96-120">**Creación de una oferta**</span><span class="sxs-lookup"><span data-stu-id="8ce96-120">**Create an offer**</span></span>

   <span data-ttu-id="8ce96-121">Ofertas son grupos de uno o varios planes que toopurchase toousers presente de proveedores o suscriben a.</span><span class="sxs-lookup"><span data-stu-id="8ce96-121">Offers are groups of one or more plans that providers present toousers toopurchase or subscribe to.</span></span>

   <span data-ttu-id="8ce96-122">a.</span><span class="sxs-lookup"><span data-stu-id="8ce96-122">a.</span></span> <span data-ttu-id="8ce96-123">[Inicie sesión en](azure-stack-connect-azure-stack.md) toohello portal como un administrador de la nube y, a continuación, haga clic en **New** > **inquilino ofrece + planes** > **ofrecen**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-123">[Sign in](azure-stack-connect-azure-stack.md) toohello portal as a cloud administrator and then click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>
   <span data-ttu-id="8ce96-124">![Nueva oferta](media/azure-stack-tutorial-tenant-vm/image01.png)</span><span class="sxs-lookup"><span data-stu-id="8ce96-124">![New offer](media/azure-stack-tutorial-tenant-vm/image01.png)</span></span>

   <span data-ttu-id="8ce96-125">b.</span><span class="sxs-lookup"><span data-stu-id="8ce96-125">b.</span></span> <span data-ttu-id="8ce96-126">Hola **ofrecen nuevas** sección, rellene **nombre para mostrar** y **nombre de recurso**y, a continuación, seleccione un nuevo o existente **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-126">In hello **New Offer** section, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="8ce96-127">Hola nombre para mostrar es el nombre descriptivo de la oferta de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce96-127">hello Display Name is hello offer's friendly name.</span></span> <span data-ttu-id="8ce96-128">Operador en la nube de hello sólo puede ver Hola nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="8ce96-128">Only hello cloud operator can see hello Resource Name.</span></span> <span data-ttu-id="8ce96-129">Su Hola nombre que administradores utilizar toowork con Hola oferta como un recurso de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8ce96-129">It's hello name that admins use toowork with hello offer as an Azure Resource Manager resource.</span></span>

   ![Nombre para mostrar](media/azure-stack-tutorial-tenant-vm/image02.png)

   <span data-ttu-id="8ce96-131">c.</span><span class="sxs-lookup"><span data-stu-id="8ce96-131">c.</span></span> <span data-ttu-id="8ce96-132">Haga clic en **Base planes**y en hello **Plan** sección, haga clic en **agregar** tooadd una nueva oferta de toohello de plan.</span><span class="sxs-lookup"><span data-stu-id="8ce96-132">Click **Base plans**, and in hello **Plan** section, click **Add** tooadd a new plan toohello offer.</span></span>

   ![Agregar un plan](media/azure-stack-tutorial-tenant-vm/image03.png)

   <span data-ttu-id="8ce96-134">d.</span><span class="sxs-lookup"><span data-stu-id="8ce96-134">d.</span></span> <span data-ttu-id="8ce96-135">Hola **nuevo Plan** sección, rellene **nombre para mostrar** y **nombre del recurso**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-135">In hello **New Plan** section, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="8ce96-136">Hola nombre para mostrar es el nombre descriptivo del plan de Hola que ven los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8ce96-136">hello Display Name is hello plan's friendly name that users see.</span></span> <span data-ttu-id="8ce96-137">Operador en la nube de hello sólo puede ver Hola nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="8ce96-137">Only hello cloud operator can see hello Resource Name.</span></span> <span data-ttu-id="8ce96-138">Su Hola nombre operadores en la nube usar toowork con hello plan como un recurso de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8ce96-138">It's hello name that cloud operators use toowork with hello plan as an Azure Resource Manager resource.</span></span>

   ![Nombre para mostrar del plan](media/azure-stack-tutorial-tenant-vm/image04.png)

   <span data-ttu-id="8ce96-140">e.</span><span class="sxs-lookup"><span data-stu-id="8ce96-140">e.</span></span> <span data-ttu-id="8ce96-141">Haga clic en **Servicios**, seleccione **Microsoft.Compute**, **Microsoft.Network** y **Microsoft.Storage** y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-141">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![Servicios del plan](media/azure-stack-tutorial-tenant-vm/image05.png)

   <span data-ttu-id="8ce96-143">f.</span><span class="sxs-lookup"><span data-stu-id="8ce96-143">f.</span></span> <span data-ttu-id="8ce96-144">Haga clic en **cuotas**y, a continuación, seleccione primer servicio de hello para el que desea toocreate una cuota.</span><span class="sxs-lookup"><span data-stu-id="8ce96-144">Click **Quotas**, and then select hello first service for which you want toocreate a quota.</span></span> <span data-ttu-id="8ce96-145">Para una cuota de IaaS, siga estos pasos para los servicios de proceso, red y almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce96-145">For an IaaS quota, follow these steps for hello Compute, Network, and Storage services.</span></span>

   <span data-ttu-id="8ce96-146">En este ejemplo, primero se crea una cuota para el servicio de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce96-146">In this example, we first create a quota for hello Compute service.</span></span> <span data-ttu-id="8ce96-147">En la lista del espacio de nombres de hello, seleccione hello **Microsoft.Compute** espacio de nombres y, a continuación, haga clic en **crear nueva cuota**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-147">In hello namespace list, select hello **Microsoft.Compute** namespace and then click **Create new quota**.</span></span>
   
   ![Crear nueva cuota](media/azure-stack-tutorial-tenant-vm/image06.png)

   <span data-ttu-id="8ce96-149">g.</span><span class="sxs-lookup"><span data-stu-id="8ce96-149">g.</span></span> <span data-ttu-id="8ce96-150">En hello **Crear cuota** sección, escriba un nombre para la cuota de Hola y establezca Hola parámetros que desee para la cuota de Hola y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-150">On hello **Create quota** section, type a name for hello quota and set hello desired parameters for hello quota and click **OK**.</span></span>

   ![Nombre de cuota](media/azure-stack-tutorial-tenant-vm/image07.png)

   <span data-ttu-id="8ce96-152">h.</span><span class="sxs-lookup"><span data-stu-id="8ce96-152">h.</span></span> <span data-ttu-id="8ce96-153">Ahora, para **Microsoft.Compute**, seleccione cuota Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="8ce96-153">Now, for **Microsoft.Compute**, select hello quota that you created.</span></span>

   ![Seleccione la cuota](media/azure-stack-tutorial-tenant-vm/image08.png)

   <span data-ttu-id="8ce96-155">Repita estos pasos para los servicios de red y almacenamiento de hello y, a continuación, haga clic en **Aceptar** en hello **cuotas** sección.</span><span class="sxs-lookup"><span data-stu-id="8ce96-155">Repeat these steps for hello Network and Storage services, and then click **OK** on hello **Quotas** section.</span></span>

   <span data-ttu-id="8ce96-156">i.</span><span class="sxs-lookup"><span data-stu-id="8ce96-156">i.</span></span> <span data-ttu-id="8ce96-157">Haga clic en **Aceptar** en hello **nuevo plan** sección.</span><span class="sxs-lookup"><span data-stu-id="8ce96-157">Click **OK** on hello **New plan** section.</span></span>

   <span data-ttu-id="8ce96-158">j.</span><span class="sxs-lookup"><span data-stu-id="8ce96-158">j.</span></span> <span data-ttu-id="8ce96-159">En hello **Plan** sección, seleccione Nuevo plan de Hola y haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-159">On hello **Plan** section, select hello new plan and click **Select**.</span></span>

   <span data-ttu-id="8ce96-160">k.</span><span class="sxs-lookup"><span data-stu-id="8ce96-160">k.</span></span> <span data-ttu-id="8ce96-161">En hello **oferta nueva** sección, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-161">On hello **New offer** section, click **Create**.</span></span> <span data-ttu-id="8ce96-162">Verá una notificación cuando se ha creado la oferta de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce96-162">You see a notification when hello offer has been created.</span></span>

   <span data-ttu-id="8ce96-163">l.</span><span class="sxs-lookup"><span data-stu-id="8ce96-163">l.</span></span> <span data-ttu-id="8ce96-164">En el menú del panel hello, haga clic en **ofrece** y, a continuación, haga clic en oferta Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="8ce96-164">On hello dashboard menu, click **Offers** and then click hello offer you created.</span></span>

   <span data-ttu-id="8ce96-165">m.</span><span class="sxs-lookup"><span data-stu-id="8ce96-165">m.</span></span> <span data-ttu-id="8ce96-166">Haga clic en **Cambiar estado** y, a continuación, haga clic en **Público**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-166">Click **Change State**, and then click **Public**.</span></span>

   ![Estado público](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a><span data-ttu-id="8ce96-168">Añadir una imagen</span><span class="sxs-lookup"><span data-stu-id="8ce96-168">Add an image</span></span>

<span data-ttu-id="8ce96-169">Antes de poder aprovisionar máquinas virtuales, debe agregar un marketplace de imagen toohello pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ce96-169">Before you can provision virtual machines, you must add an image toohello Azure Stack marketplace.</span></span> <span data-ttu-id="8ce96-170">Puede agregar imagen de Hola de su elección, incluidas las imágenes de Linux, de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8ce96-170">You can add hello image of your choice, including Linux images, from hello Azure Marketplace.</span></span>

<span data-ttu-id="8ce96-171">Si trabaja en un escenario conectado y si se ha registrado la instancia de la pila de Azure con Azure, puede descargar imagen de VM de Windows Server 2016 Hola de hello Azure Marketplace siguiendo los pasos de hello descritos en hello [descargar elementos del Marketplace de Azure tooAzure pila](azure-stack-download-azure-marketplace-item.md) tema.</span><span class="sxs-lookup"><span data-stu-id="8ce96-171">If you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure, then you can download hello Windows Server 2016 VM image from hello Azure Marketplace by using hello steps described in hello [Download marketplace items from Azure tooAzure Stack](azure-stack-download-azure-marketplace-item.md) topic.</span></span>

<span data-ttu-id="8ce96-172">Para obtener información acerca de cómo agregar diferentes elementos toohello marketplace, vea [hello Azure Marketplace de pila](azure-stack-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="8ce96-172">For information about adding different items toohello marketplace, see [hello Azure Stack Marketplace](azure-stack-marketplace.md).</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="8ce96-173">Oferta de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="8ce96-173">Test hello offer</span></span>

<span data-ttu-id="8ce96-174">Ahora que ha creado una oferta, puede probarla.</span><span class="sxs-lookup"><span data-stu-id="8ce96-174">Now that you’ve created an offer, you can test it.</span></span> <span data-ttu-id="8ce96-175">Inicie sesión como un usuario y suscribirse toohello oferta y, a continuación, agregar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8ce96-175">Log in as a user and subscribe toohello offer and then add a virtual machine.</span></span>

1. <span data-ttu-id="8ce96-176">**Suscribirse tooan oferta**</span><span class="sxs-lookup"><span data-stu-id="8ce96-176">**Subscribe tooan offer**</span></span>

   <span data-ttu-id="8ce96-177">Ahora puede iniciar sesión en portal toohello como una oferta de tooan toosubscribe de usuario.</span><span class="sxs-lookup"><span data-stu-id="8ce96-177">Now you can log in toohello portal as a user toosubscribe tooan offer.</span></span>

   <span data-ttu-id="8ce96-178">a.</span><span class="sxs-lookup"><span data-stu-id="8ce96-178">a.</span></span> <span data-ttu-id="8ce96-179">En el equipo del Kit de implementación de pila de Azure de hello, inicie sesión demasiado`https://portal.local.azurestack.external` como un usuario y haga clic en **obtener una suscripción**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-179">On hello Azure Stack Deployment Kit computer, log in too`https://portal.local.azurestack.external` as a user and click **Get a Subscription**.</span></span>

   ![Obtener una suscripción](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   <span data-ttu-id="8ce96-181">b.</span><span class="sxs-lookup"><span data-stu-id="8ce96-181">b.</span></span> <span data-ttu-id="8ce96-182">Hola **nombre para mostrar** campo, escriba un nombre para la suscripción, haga clic en **ofrecen**, haga clic en una de las ofertas de Hola Hola **elija una oferta** sección y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-182">In hello **Display Name** field, type a name for your subscription, click **Offer**, click one of hello offers in hello **Choose an offer** section, and then click **Create**.</span></span>

   ![Creación de una oferta](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   <span data-ttu-id="8ce96-184">c.</span><span class="sxs-lookup"><span data-stu-id="8ce96-184">c.</span></span> <span data-ttu-id="8ce96-185">suscripción de hello tooview que ha creado, haga clic en **más servicios**, haga clic en **suscripciones**, a continuación, haga clic en la nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="8ce96-185">tooview hello subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

   <span data-ttu-id="8ce96-186">Después de suscribirse tooan oferta, actualice hello toosee portal los servicios que forman parte de la nueva suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce96-186">After you subscribe tooan offer, refresh hello portal toosee which services are part of hello new subscription.</span></span>

2. <span data-ttu-id="8ce96-187">**Aprovisionamiento de una máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="8ce96-187">**Provision a virtual machine**</span></span>

   <span data-ttu-id="8ce96-188">Ahora puede registrar en el portal de toohello como un usuario tooprovision una máquina virtual mediante suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce96-188">Now you can log in toohello portal as a user tooprovision a virtual machine using hello subscription.</span></span> 

   <span data-ttu-id="8ce96-189">a.</span><span class="sxs-lookup"><span data-stu-id="8ce96-189">a.</span></span> <span data-ttu-id="8ce96-190">En el equipo del Kit de implementación de pila de Azure de hello, inicie sesión demasiado`https://portal.local.azurestack.external` como un usuario y, a continuación, haga clic en **New** > **proceso** > **centro de datos de Windows Server 2016 Eval**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-190">On hello Azure Stack Deployment Kit computer, log in too`https://portal.local.azurestack.external` as a user, and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval**.</span></span>  

   <span data-ttu-id="8ce96-191">b.</span><span class="sxs-lookup"><span data-stu-id="8ce96-191">b.</span></span> <span data-ttu-id="8ce96-192">Hola **Fundamentos** sección, escriba un **nombre**, **nombre de usuario**, y **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-192">In hello **Basics** section, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="8ce96-193">Para **Tipo de disco de máquina virtual**, elija **HDD**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-193">For **VM disk type**, choose **HDD**.</span></span> <span data-ttu-id="8ce96-194">Elija una **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-194">Choose a **Subscription**.</span></span> <span data-ttu-id="8ce96-195">Cree un **grupo de recursos** o seleccione uno existente y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-195">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  

   <span data-ttu-id="8ce96-196">c.</span><span class="sxs-lookup"><span data-stu-id="8ce96-196">c.</span></span> <span data-ttu-id="8ce96-197">Hola **elegir un tamaño de** sección, haga clic en **A1 básica**y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-197">In hello **Choose a size** section, click **A1 Basic**, and then click **Select**.</span></span>  

   <span data-ttu-id="8ce96-198">d.</span><span class="sxs-lookup"><span data-stu-id="8ce96-198">d.</span></span> <span data-ttu-id="8ce96-199">Hola **configuración** sección, haga clic en **red Virtual**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-199">In hello **Settings** section, click **Virtual network**.</span></span> <span data-ttu-id="8ce96-200">Hola **red virtual de elegir** sección, haga clic en **crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-200">In hello **Choose virtual network** section, click **Create new**.</span></span> <span data-ttu-id="8ce96-201">Hola **crear red virtual** sección, acepte todos los valores predeterminados de Hola y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-201">In hello **Create virtual network** section, accept all hello defaults, and click **OK**.</span></span> <span data-ttu-id="8ce96-202">Hola **configuración** sección, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8ce96-202">In hello **Settings** section, click **OK**.</span></span>

   ![Creación de una red virtual](media/azure-stack-provision-vm/image04.png)

   <span data-ttu-id="8ce96-204">e.</span><span class="sxs-lookup"><span data-stu-id="8ce96-204">e.</span></span> <span data-ttu-id="8ce96-205">Hola **resumen** sección, haga clic en **Aceptar** máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce96-205">In hello **Summary** section, click **OK** toocreate hello virtual machine.</span></span>  

   <span data-ttu-id="8ce96-206">f.</span><span class="sxs-lookup"><span data-stu-id="8ce96-206">f.</span></span> <span data-ttu-id="8ce96-207">toosee la nueva máquina virtual, haga clic en **todos los recursos**, a continuación, busque la máquina virtual de Hola y haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="8ce96-207">toosee your new virtual machine, click **All resources**, then search for hello virtual machine and click its name.</span></span>

    ![Todos los recursos](media/azure-stack-provision-vm/image06.png)

<span data-ttu-id="8ce96-209">En este tutorial aprendió:</span><span class="sxs-lookup"><span data-stu-id="8ce96-209">What you learned in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8ce96-210">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="8ce96-210">Create an offer</span></span>
> * <span data-ttu-id="8ce96-211">Añadir una imagen</span><span class="sxs-lookup"><span data-stu-id="8ce96-211">Add an image</span></span>
> * <span data-ttu-id="8ce96-212">Oferta de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="8ce96-212">Test hello offer</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8ce96-213">Asegúrese de web, móviles y los usuarios de API aplicaciones disponibles tooyour pila de Azure</span><span class="sxs-lookup"><span data-stu-id="8ce96-213">Make web, mobile, and API apps available tooyour Azure Stack users</span></span>](azure-stack-tutorial-app-service.md)
