---
title: "Máquinas virtuales disponibles para los usuarios de Azure Stack | Microsoft Docs"
description: "Tutorial para que las máquinas virtuales estén disponibles en Azure Stack"
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
ms.openlocfilehash: d2f38bc1c0b97e408f619f3ea2f704725e3bb460
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="make-virtual-machines-available-to-your-azure-stack-users"></a><span data-ttu-id="ea92b-103">Máquinas virtuales disponibles para los usuarios de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ea92b-103">Make virtual machines available to your Azure Stack users</span></span>
<span data-ttu-id="ea92b-104">Como administrador de la nube de Azure Stack, puede crear ofertas a las que se pueden suscribir los usuarios (a veces denominados inquilinos).</span><span class="sxs-lookup"><span data-stu-id="ea92b-104">As an Azure Stack cloud administrator, you can create offers that your users (sometimes referred to as tenants) can subscribe to.</span></span> <span data-ttu-id="ea92b-105">Con su suscripción, los usuarios podrán consumir servicios de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ea92b-105">Using their subscription, users can then consume Azure Stack services.</span></span>

<span data-ttu-id="ea92b-106">En este artículo se muestra cómo crear una oferta y, a continuación, cómo probarla.</span><span class="sxs-lookup"><span data-stu-id="ea92b-106">This article shows you how to create an offer, and then test it.</span></span> <span data-ttu-id="ea92b-107">Para la prueba, inicie sesión en el portal como usuario, suscríbase a la oferta y, a continuación, cree una máquina virtual con la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ea92b-107">For the test, you will log in to the portal as a user, subscribe to the offer, and then create a virtual machine using the subscription.</span></span>

<span data-ttu-id="ea92b-108">Lo qué aprenderá:</span><span class="sxs-lookup"><span data-stu-id="ea92b-108">What you will learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea92b-109">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="ea92b-109">Create an offer</span></span>
> * <span data-ttu-id="ea92b-110">Añadir una imagen</span><span class="sxs-lookup"><span data-stu-id="ea92b-110">Add an image</span></span>
> * <span data-ttu-id="ea92b-111">Probar la oferta</span><span class="sxs-lookup"><span data-stu-id="ea92b-111">Test the offer</span></span>


<span data-ttu-id="ea92b-112">En Azure Stack, los servicios se prestan a los usuarios mediante planes, ofertas y suscripciones.</span><span class="sxs-lookup"><span data-stu-id="ea92b-112">In Azure Stack, services are delivered to users using subscriptions, offers, and plans.</span></span> <span data-ttu-id="ea92b-113">Los usuarios pueden suscribirse a varias ofertas.</span><span class="sxs-lookup"><span data-stu-id="ea92b-113">Users can subscribe to multiple offers.</span></span> <span data-ttu-id="ea92b-114">Las ofertas pueden tener uno o varios planes, y los planes pueden tener uno o varios servicios.</span><span class="sxs-lookup"><span data-stu-id="ea92b-114">Offers can have one or more plans, and plans can have one or more services.</span></span>

![Planes, ofertas y suscripciones](media/azure-stack-key-features/image4.png)

<span data-ttu-id="ea92b-116">Para más información, vea [Características y conceptos clave de Azure Stack](azure-stack-key-features.md).</span><span class="sxs-lookup"><span data-stu-id="ea92b-116">To learn more, see [Key features and concepts in Azure Stack](azure-stack-key-features.md).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="ea92b-117">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="ea92b-117">Create an offer</span></span>

<span data-ttu-id="ea92b-118">Ahora puede preparar todo para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ea92b-118">Now you can get things ready for your users.</span></span> <span data-ttu-id="ea92b-119">Cuando se inicia el proceso, primero deberá crear la oferta, a continuación, un plan y, finalmente, las cuotas.</span><span class="sxs-lookup"><span data-stu-id="ea92b-119">When you start the process, you are first prompted to create the offer, then a plan, and finally quotas.</span></span>

3. <span data-ttu-id="ea92b-120">**Creación de una oferta**</span><span class="sxs-lookup"><span data-stu-id="ea92b-120">**Create an offer**</span></span>

   <span data-ttu-id="ea92b-121">Las ofertas son grupos de uno o varios planes que los proveedores presentan a los usuarios para que estos los compren o se suscriban a ellos.</span><span class="sxs-lookup"><span data-stu-id="ea92b-121">Offers are groups of one or more plans that providers present to users to purchase or subscribe to.</span></span>

   <span data-ttu-id="ea92b-122">a.</span><span class="sxs-lookup"><span data-stu-id="ea92b-122">a.</span></span> <span data-ttu-id="ea92b-123">[Inicie sesión](azure-stack-connect-azure-stack.md) en el portal como administrador de la nube y, a continuación, haga clic en **Nuevo** > **Ofertas para los inquilinos + Planes** > **Oferta**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-123">[Sign in](azure-stack-connect-azure-stack.md) to the portal as a cloud administrator and then click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>
   <span data-ttu-id="ea92b-124">![Nueva oferta](media/azure-stack-tutorial-tenant-vm/image01.png)</span><span class="sxs-lookup"><span data-stu-id="ea92b-124">![New offer](media/azure-stack-tutorial-tenant-vm/image01.png)</span></span>

   <span data-ttu-id="ea92b-125">b.</span><span class="sxs-lookup"><span data-stu-id="ea92b-125">b.</span></span> <span data-ttu-id="ea92b-126">En la sección **Nueva oferta**, rellene el **nombre para mostrar** y el **nombre de recurso** y, a continuación, seleccione un **grupo de recursos** nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="ea92b-126">In the **New Offer** section, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="ea92b-127">El nombre para mostrar es el nombre descriptivo de la oferta.</span><span class="sxs-lookup"><span data-stu-id="ea92b-127">The Display Name is the offer's friendly name.</span></span> <span data-ttu-id="ea92b-128">Solo el operador de la nube puede ver el nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="ea92b-128">Only the cloud operator can see the Resource Name.</span></span> <span data-ttu-id="ea92b-129">Es el nombre que usan los administradores para trabajar con la oferta como un recurso de Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea92b-129">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![Nombre para mostrar](media/azure-stack-tutorial-tenant-vm/image02.png)

   <span data-ttu-id="ea92b-131">c.</span><span class="sxs-lookup"><span data-stu-id="ea92b-131">c.</span></span> <span data-ttu-id="ea92b-132">Haga clic en **Planes base** y en la sección **Plan**, haga clic en **Agregar** para agregar un nuevo plan a la oferta.</span><span class="sxs-lookup"><span data-stu-id="ea92b-132">Click **Base plans**, and in the **Plan** section, click **Add** to add a new plan to the offer.</span></span>

   ![Agregar un plan](media/azure-stack-tutorial-tenant-vm/image03.png)

   <span data-ttu-id="ea92b-134">d.</span><span class="sxs-lookup"><span data-stu-id="ea92b-134">d.</span></span> <span data-ttu-id="ea92b-135">En la sección **Nuevo plan**, rellene el **nombre para mostrar** y el **nombre del recurso**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-135">In the **New Plan** section, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="ea92b-136">El nombre para mostrar es el nombre descriptivo del plan que ven los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ea92b-136">The Display Name is the plan's friendly name that users see.</span></span> <span data-ttu-id="ea92b-137">Solo el operador de la nube puede ver el nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="ea92b-137">Only the cloud operator can see the Resource Name.</span></span> <span data-ttu-id="ea92b-138">Es el nombre que usan los operadores de la nube para trabajar con el plan como recurso de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea92b-138">It's the name that cloud operators use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![Nombre para mostrar del plan](media/azure-stack-tutorial-tenant-vm/image04.png)

   <span data-ttu-id="ea92b-140">e.</span><span class="sxs-lookup"><span data-stu-id="ea92b-140">e.</span></span> <span data-ttu-id="ea92b-141">Haga clic en **Servicios**, seleccione **Microsoft.Compute**, **Microsoft.Network** y **Microsoft.Storage** y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-141">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![Servicios del plan](media/azure-stack-tutorial-tenant-vm/image05.png)

   <span data-ttu-id="ea92b-143">f.</span><span class="sxs-lookup"><span data-stu-id="ea92b-143">f.</span></span> <span data-ttu-id="ea92b-144">Haga clic en **Cuotas** y, a continuación, seleccione el primer servicio para el que desea crear una cuota.</span><span class="sxs-lookup"><span data-stu-id="ea92b-144">Click **Quotas**, and then select the first service for which you want to create a quota.</span></span> <span data-ttu-id="ea92b-145">Para una cuota de la infraestructura como servicio, siga estos pasos para los servicios de proceso, red y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ea92b-145">For an IaaS quota, follow these steps for the Compute, Network, and Storage services.</span></span>

   <span data-ttu-id="ea92b-146">En este ejemplo, primero se crea una cuota para el servicio de proceso.</span><span class="sxs-lookup"><span data-stu-id="ea92b-146">In this example, we first create a quota for the Compute service.</span></span> <span data-ttu-id="ea92b-147">En la lista de espacio de nombres, seleccione el espacio de nombres **Microsoft.Compute** y, a continuación, haga clic en **Crear nueva cuota**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-147">In the namespace list, select the **Microsoft.Compute** namespace and then click **Create new quota**.</span></span>
   
   ![Crear nueva cuota](media/azure-stack-tutorial-tenant-vm/image06.png)

   <span data-ttu-id="ea92b-149">g.</span><span class="sxs-lookup"><span data-stu-id="ea92b-149">g.</span></span> <span data-ttu-id="ea92b-150">En la sección **Crear cuota**, escriba un nombre para la cuota y establezca los parámetros deseados para la cuota y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-150">On the **Create quota** section, type a name for the quota and set the desired parameters for the quota and click **OK**.</span></span>

   ![Nombre de cuota](media/azure-stack-tutorial-tenant-vm/image07.png)

   <span data-ttu-id="ea92b-152">h.</span><span class="sxs-lookup"><span data-stu-id="ea92b-152">h.</span></span> <span data-ttu-id="ea92b-153">Ahora, para **Microsoft.Compute**, seleccione la cuota que ha creado.</span><span class="sxs-lookup"><span data-stu-id="ea92b-153">Now, for **Microsoft.Compute**, select the quota that you created.</span></span>

   ![Seleccione la cuota](media/azure-stack-tutorial-tenant-vm/image08.png)

   <span data-ttu-id="ea92b-155">Repita estos pasos para Network y Storage services y, a continuación, haga clic en **Aceptar** en la sección **Cuotas**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-155">Repeat these steps for the Network and Storage services, and then click **OK** on the **Quotas** section.</span></span>

   <span data-ttu-id="ea92b-156">i.</span><span class="sxs-lookup"><span data-stu-id="ea92b-156">i.</span></span> <span data-ttu-id="ea92b-157">Haga clic en **Aceptar** en la sección **Nuevo plan**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-157">Click **OK** on the **New plan** section.</span></span>

   <span data-ttu-id="ea92b-158">j.</span><span class="sxs-lookup"><span data-stu-id="ea92b-158">j.</span></span> <span data-ttu-id="ea92b-159">En la sección **Plan**, seleccione el nuevo plan y haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-159">On the **Plan** section, select the new plan and click **Select**.</span></span>

   <span data-ttu-id="ea92b-160">k.</span><span class="sxs-lookup"><span data-stu-id="ea92b-160">k.</span></span> <span data-ttu-id="ea92b-161">En la sección **Nueva oferta**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-161">On the **New offer** section, click **Create**.</span></span> <span data-ttu-id="ea92b-162">Verá una notificación cuando se haya creado la oferta.</span><span class="sxs-lookup"><span data-stu-id="ea92b-162">You see a notification when the offer has been created.</span></span>

   <span data-ttu-id="ea92b-163">l.</span><span class="sxs-lookup"><span data-stu-id="ea92b-163">l.</span></span> <span data-ttu-id="ea92b-164">En el menú del panel, haga clic en **Ofertas** y, a continuación, haga clic en la oferta que ha creado.</span><span class="sxs-lookup"><span data-stu-id="ea92b-164">On the dashboard menu, click **Offers** and then click the offer you created.</span></span>

   <span data-ttu-id="ea92b-165">m.</span><span class="sxs-lookup"><span data-stu-id="ea92b-165">m.</span></span> <span data-ttu-id="ea92b-166">Haga clic en **Cambiar estado** y, a continuación, haga clic en **Público**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-166">Click **Change State**, and then click **Public**.</span></span>

   ![Estado público](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a><span data-ttu-id="ea92b-168">Añadir una imagen</span><span class="sxs-lookup"><span data-stu-id="ea92b-168">Add an image</span></span>

<span data-ttu-id="ea92b-169">Antes de poder aprovisionar a las máquinas virtuales, debe agregar una imagen en Marketplace de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ea92b-169">Before you can provision virtual machines, you must add an image to the Azure Stack marketplace.</span></span> <span data-ttu-id="ea92b-170">Puede agregar la imagen que desee, incluidas las imágenes de Linux, de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ea92b-170">You can add the image of your choice, including Linux images, from the Azure Marketplace.</span></span>

<span data-ttu-id="ea92b-171">Si trabaja en un escenario conectado y si ha registrado la instancia de Azure Stack con Azure, a continuación, puede descargar la imagen de la VM de Windows Server 2016 de Azure Marketplace mediante el uso de los pasos descritos en el tema [Descarga de elementos Marketplace de Azure en Azure Stack](azure-stack-download-azure-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="ea92b-171">If you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure, then you can download the Windows Server 2016 VM image from the Azure Marketplace by using the steps described in the [Download marketplace items from Azure to Azure Stack](azure-stack-download-azure-marketplace-item.md) topic.</span></span>

<span data-ttu-id="ea92b-172">Para obtener información acerca de cómo agregar diferentes elementos a Marketplace, vea [Marketplace de Azure Stack](azure-stack-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="ea92b-172">For information about adding different items to the marketplace, see [The Azure Stack Marketplace](azure-stack-marketplace.md).</span></span>

## <a name="test-the-offer"></a><span data-ttu-id="ea92b-173">Probar la oferta</span><span class="sxs-lookup"><span data-stu-id="ea92b-173">Test the offer</span></span>

<span data-ttu-id="ea92b-174">Ahora que ha creado una oferta, puede probarla.</span><span class="sxs-lookup"><span data-stu-id="ea92b-174">Now that you’ve created an offer, you can test it.</span></span> <span data-ttu-id="ea92b-175">Inicie sesión como usuario y suscríbase a la oferta y, a continuación, agregue una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea92b-175">Log in as a user and subscribe to the offer and then add a virtual machine.</span></span>

1. <span data-ttu-id="ea92b-176">**Suscripción a una oferta**</span><span class="sxs-lookup"><span data-stu-id="ea92b-176">**Subscribe to an offer**</span></span>

   <span data-ttu-id="ea92b-177">Ahora puede iniciar sesión en el portal como usuario para suscribirse a una oferta.</span><span class="sxs-lookup"><span data-stu-id="ea92b-177">Now you can log in to the portal as a user to subscribe to an offer.</span></span>

   <span data-ttu-id="ea92b-178">a.</span><span class="sxs-lookup"><span data-stu-id="ea92b-178">a.</span></span> <span data-ttu-id="ea92b-179">En el equipo del Kit de desarrollo de Azure Stack, inicie sesión en `https://portal.local.azurestack.external` como inquilino y haga clic en **Obtener una suscripción**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-179">On the Azure Stack Deployment Kit computer, log in to `https://portal.local.azurestack.external` as a user and click **Get a Subscription**.</span></span>

   ![Obtener una suscripción](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   <span data-ttu-id="ea92b-181">b.</span><span class="sxs-lookup"><span data-stu-id="ea92b-181">b.</span></span> <span data-ttu-id="ea92b-182">En el campo **Nombre para mostrar**, escriba un nombre para la suscripción, haga clic en **Oferta**, haga clic en una de las ofertas en la sección **Elija una oferta** y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-182">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** section, and then click **Create**.</span></span>

   ![Creación de una oferta](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   <span data-ttu-id="ea92b-184">c.</span><span class="sxs-lookup"><span data-stu-id="ea92b-184">c.</span></span> <span data-ttu-id="ea92b-185">Para ver la suscripción que ha creado, haga clic en **Más servicios**, en **Suscripciones** y, luego, en la nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="ea92b-185">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

   <span data-ttu-id="ea92b-186">Después de suscribirse a una oferta, actualice el portal para ver los servicios que forman parte de la nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="ea92b-186">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>

2. <span data-ttu-id="ea92b-187">**Aprovisionamiento de una máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="ea92b-187">**Provision a virtual machine**</span></span>

   <span data-ttu-id="ea92b-188">Ahora puede iniciar sesión en el portal como usuario para aprovisionar a una máquina virtual mediante la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ea92b-188">Now you can log in to the portal as a user to provision a virtual machine using the subscription.</span></span> 

   <span data-ttu-id="ea92b-189">a.</span><span class="sxs-lookup"><span data-stu-id="ea92b-189">a.</span></span> <span data-ttu-id="ea92b-190">En el equipo del Kit de desarrollo de Azure Stack, inicie sesión en `https://portal.local.azurestack.external` como usuario y, a continuación, haga clic en **Nuevo** > **Proceso** > **Windows Server 2016 Datacenter Eval**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-190">On the Azure Stack Deployment Kit computer, log in to `https://portal.local.azurestack.external` as a user, and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval**.</span></span>  

   <span data-ttu-id="ea92b-191">b.</span><span class="sxs-lookup"><span data-stu-id="ea92b-191">b.</span></span> <span data-ttu-id="ea92b-192">En la sección **Aspectos básicos**, escriba un **Nombre**, **Nombre de usuario** y **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-192">In the **Basics** section, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="ea92b-193">Para **Tipo de disco de máquina virtual**, elija **HDD**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-193">For **VM disk type**, choose **HDD**.</span></span> <span data-ttu-id="ea92b-194">Elija una **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-194">Choose a **Subscription**.</span></span> <span data-ttu-id="ea92b-195">Cree un **grupo de recursos** o seleccione uno existente y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-195">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  

   <span data-ttu-id="ea92b-196">c.</span><span class="sxs-lookup"><span data-stu-id="ea92b-196">c.</span></span> <span data-ttu-id="ea92b-197">En la sección **Elegir un tamaño**, haga clic en **A1 Básico**y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-197">In the **Choose a size** section, click **A1 Basic**, and then click **Select**.</span></span>  

   <span data-ttu-id="ea92b-198">d.</span><span class="sxs-lookup"><span data-stu-id="ea92b-198">d.</span></span> <span data-ttu-id="ea92b-199">En la sección **Configuración**, haga clic en **Red virtual**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-199">In the **Settings** section, click **Virtual network**.</span></span> <span data-ttu-id="ea92b-200">En la sección **Elegir red virtual** , haga clic en **Crear nueva**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-200">In the **Choose virtual network** section, click **Create new**.</span></span> <span data-ttu-id="ea92b-201">En la sección **Crear red virtual**, acepte todos los valores predeterminados y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-201">In the **Create virtual network** section, accept all the defaults, and click **OK**.</span></span> <span data-ttu-id="ea92b-202">En la sección **Configuración**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ea92b-202">In the **Settings** section, click **OK**.</span></span>

   ![Creación de una red virtual](media/azure-stack-provision-vm/image04.png)

   <span data-ttu-id="ea92b-204">e.</span><span class="sxs-lookup"><span data-stu-id="ea92b-204">e.</span></span> <span data-ttu-id="ea92b-205">En la sección **Resumen**, haga clic en **Aceptar** para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea92b-205">In the **Summary** section, click **OK** to create the virtual machine.</span></span>  

   <span data-ttu-id="ea92b-206">f.</span><span class="sxs-lookup"><span data-stu-id="ea92b-206">f.</span></span> <span data-ttu-id="ea92b-207">Para ver la nueva máquina virtual, haga clic en **Todos los recursos** y, a continuación, busque la máquina virtual y haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="ea92b-207">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span></span>

    ![Todos los recursos](media/azure-stack-provision-vm/image06.png)

<span data-ttu-id="ea92b-209">En este tutorial aprendió:</span><span class="sxs-lookup"><span data-stu-id="ea92b-209">What you learned in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea92b-210">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="ea92b-210">Create an offer</span></span>
> * <span data-ttu-id="ea92b-211">Añadir una imagen</span><span class="sxs-lookup"><span data-stu-id="ea92b-211">Add an image</span></span>
> * <span data-ttu-id="ea92b-212">Probar la oferta</span><span class="sxs-lookup"><span data-stu-id="ea92b-212">Test the offer</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ea92b-213">Aplicaciones web, móviles y API Apps disponibles para los usuarios de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ea92b-213">Make web, mobile, and API apps available to your Azure Stack users</span></span>](azure-stack-tutorial-app-service.md)