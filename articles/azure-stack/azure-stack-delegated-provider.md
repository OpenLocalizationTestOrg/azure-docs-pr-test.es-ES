---
title: "Delegación de ofertas en Azure Stack | Microsoft Docs"
description: "Obtenga información acerca de cómo delegar a otras personas sus tareas de crear ofertas y registrar a usuarios."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: 157f0207-bddc-42e5-8351-197ec23f9d46
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: alfredop
ms.openlocfilehash: c56c0669cbcd66fe1d7177846e02ba28838c0544
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="delegating-offers-in-azure-stack"></a><span data-ttu-id="8b90e-103">Delegación de ofertas en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8b90e-103">Delegating offers in Azure Stack</span></span>

<span data-ttu-id="8b90e-104">Como operador en la nube de Azure Stack, es posible que a veces quiera delegar a otras personas las tareas de crear ofertas y registrar a usuarios.</span><span class="sxs-lookup"><span data-stu-id="8b90e-104">As the Azure Stack cloud operator, you often want to put other people in charge of creating offers and signing up users for you.</span></span> <span data-ttu-id="8b90e-105">Por ejemplo, si es un proveedor de servicios y quiere que los distribuidores registren a los clientes y los administren en su nombre.</span><span class="sxs-lookup"><span data-stu-id="8b90e-105">For example, if you are a service provider and you want resellers to sign up customers and manage them on your behalf.</span></span> <span data-ttu-id="8b90e-106">Esto también puede ocurrir en una empresa si forma parte de un grupo de TI central y quiere que las divisiones o las subsidiarias registren usuarios sin su intervención.</span><span class="sxs-lookup"><span data-stu-id="8b90e-106">It can also happen in an enterprise if you are part of a central IT group and want divisions or subsidiaries to sign up users without your intervention.</span></span>

<span data-ttu-id="8b90e-107">La delegación le ayuda con estas tareas y le permite alcanzar y administrar a más usuarios que si lo hiciera directamente.</span><span class="sxs-lookup"><span data-stu-id="8b90e-107">Delegation helps you with these tasks, helping you to reach and manage more users than you would be able to do directly.</span></span> <span data-ttu-id="8b90e-108">En la siguiente ilustración se muestra un nivel de delegación, pero Azure Stack admite varios niveles.</span><span class="sxs-lookup"><span data-stu-id="8b90e-108">The following illustration shows one level of delegation, but Azure Stack supports multiple levels.</span></span> <span data-ttu-id="8b90e-109">Los proveedores delegados pueden a su vez delegar las tareas a otros proveedores, en hasta cinco niveles.</span><span class="sxs-lookup"><span data-stu-id="8b90e-109">Delegated providers can in turn delegate to other providers, up to five levels.</span></span>

![](media/azure-stack-delegated-provider/image1.png)

<span data-ttu-id="8b90e-110">Los operadores de la nube de Azure Stack pueden delegar la creación de ofertas e inquilinos a otros usuarios mediante la funcionalidad de delegación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-110">Azure Stack cloud operators can delegate the creation of offers and tenants to other users by using the delegation functionality.</span></span>

## <a name="roles-and-steps-in-delegation"></a><span data-ttu-id="8b90e-111">Roles y pasos de la delegación</span><span class="sxs-lookup"><span data-stu-id="8b90e-111">Roles and steps in delegation</span></span>
<span data-ttu-id="8b90e-112">Para comprender la delegación, es necesario tener en cuenta que existen tres roles implicados:</span><span class="sxs-lookup"><span data-stu-id="8b90e-112">To understand delegation, keep in mind that there are three roles involved:</span></span>

* <span data-ttu-id="8b90e-113">El **operador en la nube** administra la infraestructura de Azure Stack, crea una plantilla de oferta y la delega a otras personas para que la ofrezcan a sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="8b90e-113">The **cloud operator** manages the Azure Stack infrastructure, creates an offer template, and delegates others to offer it to their users.</span></span>
* <span data-ttu-id="8b90e-114">Se llaman a los administradores delegados en la nube **delegado proveedores**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-114">The delegated cloud administrators are called **delegated providers**.</span></span> <span data-ttu-id="8b90e-115">Pueden pertenecer a otras organizaciones (por ejemplo, a otros inquilinos de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8b90e-115">They can belong to other organizations (such as other Azure Active Directory tenants).</span></span>
* <span data-ttu-id="8b90e-116">Los **usuarios** se suscriben a las ofertas y las usan para administrar las cargas de trabajo, crear máquinas virtuales, almacenar datos, etc.</span><span class="sxs-lookup"><span data-stu-id="8b90e-116">**Users** sign up for the offers and use them for managing their workloads, creating VMs, storing data, etc.</span></span>

<span data-ttu-id="8b90e-117">Como se muestra en el siguiente gráfico, hay dos pasos para configurar la delegación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-117">As shown in the following graphic, there are two steps in setting up delegation.</span></span>

1. <span data-ttu-id="8b90e-118">**Identificar a los proveedores delegados** suscribiéndolos a una oferta basada en un plan que contiene solo el servicio de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="8b90e-118">**Identify the delegated providers** by subscribing them to an offer based on a plan that contains only the subscriptions service.</span></span>
   <span data-ttu-id="8b90e-119">Los usuarios que se suscriben a esta oferta adquirir algunas de las capacidades del Administrador de la nube, incluida la capacidad para ampliar las ofertas y desconectar a los usuarios hacia arriba para ellos.</span><span class="sxs-lookup"><span data-stu-id="8b90e-119">Users who subscribe to this offer acquire some of the cloud administrator’s capabilities, including the ability to extend offers and sign users up for them.</span></span>
2. <span data-ttu-id="8b90e-120">**Delegar una oferta al proveedor delegado**: esta oferta funciona como una plantilla para lo que puede ofrecer el proveedor delegado.</span><span class="sxs-lookup"><span data-stu-id="8b90e-120">**Delegate an offer to the delegated provider**, this offer functions as a template for what the delegated provider can offer.</span></span> <span data-ttu-id="8b90e-121">El proveedor delegado ya puede coger la oferta, asignarle un nombre (pero sin cambiar sus servicios ni cuotas) y ofrecerla a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="8b90e-121">The delegated provider is now able to take the offer, choose a name for it (but not change its services and quotas), and offer it to customers.</span></span>

![](media/azure-stack-delegated-provider/image2.png)

<span data-ttu-id="8b90e-122">Para actuar como proveedor delegado, los usuarios deben establecer una relación con el proveedor principal, en otras palabras, deben crear una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8b90e-122">To act as delegated providers, users need to establish a relationship with the main provider; in other words, they need to create a subscription.</span></span> <span data-ttu-id="8b90e-123">En este escenario, esta suscripción proporciona a los proveedores delegados el derecho a presentar ofertas en nombre del proveedor principal.</span><span class="sxs-lookup"><span data-stu-id="8b90e-123">In this scenario, this subscription identifies the delegated providers as having the right to present offers on behalf of the main provider.</span></span>

<span data-ttu-id="8b90e-124">Una vez establecida esta relación, el operador en la nube puede delegar una oferta al proveedor delegado.</span><span class="sxs-lookup"><span data-stu-id="8b90e-124">Once this relationship is established, the cloud operator can delegate an offer to the delegated provider.</span></span> <span data-ttu-id="8b90e-125">El proveedor delegado ya puede coger la oferta, asignarle un nombre (pero sin cambiar el contenido) y ofrecerla a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="8b90e-125">The delegated provider is now able to take the offer, rename it (but not change its substance), and offer it to its customers.</span></span>

<span data-ttu-id="8b90e-126">En las siguientes secciones se describe cómo establecer un proveedor delegado, delegar una oferta y comprobar que los usuarios pueden subscribirse a la misma.</span><span class="sxs-lookup"><span data-stu-id="8b90e-126">The following sections describe how to establish a delegated provider, delegate an offer, and verify that users can sign up for it.</span></span>

## <a name="set-up-roles"></a><span data-ttu-id="8b90e-127">Configurar los roles</span><span class="sxs-lookup"><span data-stu-id="8b90e-127">Set up roles</span></span>

<span data-ttu-id="8b90e-128">Para ver un proveedor delegado en el trabajo, necesita cuentas de Azure Active Directory adicionales además de su cuenta de operador en la nube.</span><span class="sxs-lookup"><span data-stu-id="8b90e-128">To see a delegated provider at work, you need additional Azure Active Directory accounts in addition to your cloud operator account.</span></span> <span data-ttu-id="8b90e-129">Si no las tiene, debe crear las dos cuentas.</span><span class="sxs-lookup"><span data-stu-id="8b90e-129">If you do not have them, create the two accounts.</span></span> <span data-ttu-id="8b90e-130">Las cuentas pueden pertenecer a cualquier inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="8b90e-130">The accounts can belong to any AAD tenant.</span></span> <span data-ttu-id="8b90e-131">Nos referimos a ellos como el proveedor delegado y el usuario.</span><span class="sxs-lookup"><span data-stu-id="8b90e-131">We refer to them as the delegated provider (DP) and the user.</span></span>

| <span data-ttu-id="8b90e-132">**Rol**</span><span class="sxs-lookup"><span data-stu-id="8b90e-132">**Role**</span></span> | <span data-ttu-id="8b90e-133">**Derechos organizativos**</span><span class="sxs-lookup"><span data-stu-id="8b90e-133">**Organizational rights**</span></span> |
| --- | --- |
| <span data-ttu-id="8b90e-134">Proveedor delegado</span><span class="sxs-lookup"><span data-stu-id="8b90e-134">Delegated Provider</span></span> |<span data-ttu-id="8b90e-135">Usuario</span><span class="sxs-lookup"><span data-stu-id="8b90e-135">User</span></span> |
| <span data-ttu-id="8b90e-136">Usuario</span><span class="sxs-lookup"><span data-stu-id="8b90e-136">User</span></span> |<span data-ttu-id="8b90e-137">Usuario</span><span class="sxs-lookup"><span data-stu-id="8b90e-137">User</span></span> |

## <a name="identify-the-delegated-providers"></a><span data-ttu-id="8b90e-138">Identificar los proveedores delegados</span><span class="sxs-lookup"><span data-stu-id="8b90e-138">Identify the delegated providers</span></span>
1. <span data-ttu-id="8b90e-139">Inicie sesión como operador en la nube.</span><span class="sxs-lookup"><span data-stu-id="8b90e-139">Sign in as cloud operator.</span></span>
2. <span data-ttu-id="8b90e-140">Cree la oferta que permite que los usuarios se conviertan en proveedores delegados.</span><span class="sxs-lookup"><span data-stu-id="8b90e-140">Create the offer that enables users to become delegated providers.</span></span> <span data-ttu-id="8b90e-141">Esto requiere la creación de un plan y una oferta basada en este:</span><span class="sxs-lookup"><span data-stu-id="8b90e-141">This requires that you create a plan and an offer based on it:</span></span>
   
   <span data-ttu-id="8b90e-142">a.</span><span class="sxs-lookup"><span data-stu-id="8b90e-142">a.</span></span>  <span data-ttu-id="8b90e-143">[Cree un plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="8b90e-143">[Create a plan](azure-stack-create-plan.md).</span></span>
       <span data-ttu-id="8b90e-144">Este plan debe incluir solo el servicio de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="8b90e-144">This plan should include only the subscriptions service.</span></span> <span data-ttu-id="8b90e-145">En este artículo, se usa un plan denominado PlanForDelegation.</span><span class="sxs-lookup"><span data-stu-id="8b90e-145">In this article, we use a plan called PlanForDelegation.</span></span>
   
   <span data-ttu-id="8b90e-146">b.</span><span class="sxs-lookup"><span data-stu-id="8b90e-146">b.</span></span>  <span data-ttu-id="8b90e-147">[Cree una oferta](azure-stack-create-offer.md) en función de este plan.</span><span class="sxs-lookup"><span data-stu-id="8b90e-147">[Create an offer](azure-stack-create-offer.md) based on this plan.</span></span> <span data-ttu-id="8b90e-148">En este artículo, usamos una oferta denominada OfferToDP.</span><span class="sxs-lookup"><span data-stu-id="8b90e-148">In this article, we use an offer called OfferToDP.</span></span>
   
   <span data-ttu-id="8b90e-149">c.</span><span class="sxs-lookup"><span data-stu-id="8b90e-149">c.</span></span>  <span data-ttu-id="8b90e-150">Una vez completada la creación de la oferta, agregue el proveedor delegado como un suscriptor a esta oferta haciendo clic en **Suscripciones** &gt; **Agregar** &gt; **Nueva suscripción de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-150">Once the creation of the offer is complete, add the delegated provider as a subscriber to this offer by clicking **Subscriptions** &gt; **Add** &gt; **New Tenant Subscription**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> <span data-ttu-id="8b90e-151">Como con todas las ofertas de Azure Stack, tiene la opción de hacer la oferta pública y permitir que los usuarios se subscriban; o mantenerla privada y dejar que el operador en la nube administre la suscripción.</span><span class="sxs-lookup"><span data-stu-id="8b90e-151">As with all Azure Stack offers, you have the option of making the offer public and letting users sign up for it, or keeping it private and have the cloud operator manage the sign-up.</span></span> <span data-ttu-id="8b90e-152">Los proveedores delegados suelen ser un grupo pequeño y usted quiere controlar quién se admitió, por lo que mantener esta oferta en privado tiene sentido en la mayoría de los casos.</span><span class="sxs-lookup"><span data-stu-id="8b90e-152">Delegated providers are usually a small group and you want to control who is admitted to it, so keeping this offer private makes sense in most cases.</span></span>
> 
> 

## <a name="cloud-operator-creates-the-delegated-offer"></a><span data-ttu-id="8b90e-153">El operador en la nube crea la oferta delegada</span><span class="sxs-lookup"><span data-stu-id="8b90e-153">Cloud operator creates the delegated offer</span></span>

<span data-ttu-id="8b90e-154">Ya ha establecido su proveedor delegado.</span><span class="sxs-lookup"><span data-stu-id="8b90e-154">You have now established your delegated provider.</span></span> <span data-ttu-id="8b90e-155">El siguiente paso es crear el plan y la oferta que va a delegar y que usarán los clientes.</span><span class="sxs-lookup"><span data-stu-id="8b90e-155">The next step is to create the plan and offer that you are going to delegate, and which your customers will use.</span></span> <span data-ttu-id="8b90e-156">Debe definir esta oferta exactamente como desea que los clientes la vean, porque el proveedor delegado no podrá cambiar los planes ni las cuotas que incluye.</span><span class="sxs-lookup"><span data-stu-id="8b90e-156">You should define this offer exactly as you want the customers to see it, because the delegated provider will not be able to change the plans and quotas it includes.</span></span>

1. <span data-ttu-id="8b90e-157">Como operador en la nube, [cree un plan](azure-stack-create-plan.md) y [una oferta](azure-stack-create-offer.md) basada en él.</span><span class="sxs-lookup"><span data-stu-id="8b90e-157">As cloud operator, [create a plan](azure-stack-create-plan.md) and [an offer](azure-stack-create-offer.md) based on it.</span></span> <span data-ttu-id="8b90e-158">En este artículo, usamos una oferta denominada DelegatedOffer.</span><span class="sxs-lookup"><span data-stu-id="8b90e-158">For this article, we use an offer called DelegatedOffer.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8b90e-159">Esta oferta no tiene que ser pública.</span><span class="sxs-lookup"><span data-stu-id="8b90e-159">This offer does not have to be public.</span></span> <span data-ttu-id="8b90e-160">Se pueda hacer pública si así lo elige, pero en la mayoría de los casos, solo querrá que los proveedores delegados tengan acceso a la misma.</span><span class="sxs-lookup"><span data-stu-id="8b90e-160">It can be made public if you choose, but, in most cases, you only want delegated providers to have access to it.</span></span> <span data-ttu-id="8b90e-161">Una vez que delegue una oferta privada tal como se describe en los pasos siguientes, el proveedor delegado tendrá acceso a la misma.</span><span class="sxs-lookup"><span data-stu-id="8b90e-161">Once you delegate a private offer as described in the following steps, the delegated provider has access to it.</span></span>
   > 
   > 
1. <span data-ttu-id="8b90e-162">Delegue la oferta.</span><span class="sxs-lookup"><span data-stu-id="8b90e-162">Delegate the offer.</span></span> <span data-ttu-id="8b90e-163">Vaya a DelegatedOffer y en el panel Configuración, haga clic en **Proveedores delegados** &gt; **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-163">Go to DelegatedOffer, and in the Settings pane, click **Delegated Providers** &gt; **Add**.</span></span>
2. <span data-ttu-id="8b90e-164">Seleccione la suscripción del proveedor delegado en el cuadro de lista desplegable y haga clic en **Delegado**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-164">Select the delegated provider’s subscription from the drop-down list box and click **Delegate**.</span></span>

> ![](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-the-offer"></a><span data-ttu-id="8b90e-165">El proveedor delegado personaliza la oferta</span><span class="sxs-lookup"><span data-stu-id="8b90e-165">Delegated provider customizes the offer</span></span>

<span data-ttu-id="8b90e-166">Inicie sesión en el **portal del inquilino** como proveedor delegado y cree una oferta nueva usando la oferta delegada como plantilla.</span><span class="sxs-lookup"><span data-stu-id="8b90e-166">Sign in to the **tenant portal** as the delegated provider and create a new offer using the delegated offer as a template.</span></span>

1. <span data-ttu-id="8b90e-167">Haga clic en **Nueva** &gt; **Ofertas + Planes de inquilinos** &gt; **Oferta**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-167">Click **New** &gt; **Tenant Offers + Plans** &gt; **Offer**.</span></span>

    ![](media/azure-stack-delegated-provider/image5.png)


1. <span data-ttu-id="8b90e-168">Asigne un nombre a la oferta.</span><span class="sxs-lookup"><span data-stu-id="8b90e-168">Assign a name to the offer.</span></span> <span data-ttu-id="8b90e-169">Aquí elegiremos ResellerOffer.</span><span class="sxs-lookup"><span data-stu-id="8b90e-169">Here we choose ResellerOffer.</span></span> <span data-ttu-id="8b90e-170">Seleccione la oferta delegada en la que basarse y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-170">Select the delegated offer to base it on and then click **Create**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > <span data-ttu-id="8b90e-171">Tenga en cuenta cómo difiere la creación de la oferta tal y como la experimenta el operador en la nube.</span><span class="sxs-lookup"><span data-stu-id="8b90e-171">Note the difference compared to offer creation as experienced by the cloud operator.</span></span> <span data-ttu-id="8b90e-172">El proveedor delegado no construye la oferta a partir de planes base ni complementarios; solo puede elegir entre ofertas que le han sido delegadas y no las puede modificar.</span><span class="sxs-lookup"><span data-stu-id="8b90e-172">The delegated provider does not construct the offer from base plans and add-on plans; they can only choose from offers that have been delegated to them, and can't make changes to those offers.</span></span>

1. <span data-ttu-id="8b90e-173">Para hacer la oferta pública, haga clic en **Examinar** &gt; **Ofertas**, seleccione la oferta y haga clic en **Cambiar estado**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-173">Make the offer public by clicking **Browse** &gt; **Offers**, selecting the offer, and clicking **Change State**.</span></span>
2. <span data-ttu-id="8b90e-174">El proveedor delegado expone estas ofertas a través de la URL de su propio portal.</span><span class="sxs-lookup"><span data-stu-id="8b90e-174">The delegated provider exposes these offers through their own portal URL.</span></span> <span data-ttu-id="8b90e-175">Estas ofertas solo son visibles en el portal de delegado.</span><span class="sxs-lookup"><span data-stu-id="8b90e-175">These offers are visible only through the delegated portal.</span></span> <span data-ttu-id="8b90e-176">Para buscar y cambiar esta dirección URL:</span><span class="sxs-lookup"><span data-stu-id="8b90e-176">To find and change this URL:</span></span>
   
    <span data-ttu-id="8b90e-177">a.</span><span class="sxs-lookup"><span data-stu-id="8b90e-177">a.</span></span>  <span data-ttu-id="8b90e-178">Haga clic en **Examinar** &gt; **Más servicios** &gt; **Suscripciones** &gt; Seleccione la suscripción del proveedor delegado, en nuestro caso es *DPSubscription* &gt; **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-178">Click **Browse**&gt; **More services**&gt; **Subscriptions**&gt; Select the delegated provider subscription, in our case its *DPSubscription*&gt; **Properties**.</span></span>
   
    <span data-ttu-id="8b90e-179">b.</span><span class="sxs-lookup"><span data-stu-id="8b90e-179">b.</span></span>  <span data-ttu-id="8b90e-180">Copie la URL del portal en una ubicación diferente, como el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="8b90e-180">Copy the portal URL to a separate location, such as Notepad.</span></span>
   
    ![](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   <span data-ttu-id="8b90e-181">Ya ha completado la creación de una oferta delegada como un proveedor delegado.</span><span class="sxs-lookup"><span data-stu-id="8b90e-181">You have now completed the creation of a delegated offer as a delegated provider.</span></span> <span data-ttu-id="8b90e-182">Cierre sesión como proveedor delegado.</span><span class="sxs-lookup"><span data-stu-id="8b90e-182">Sign out as the delegated provider.</span></span> <span data-ttu-id="8b90e-183">Cierre la pestaña de explorador que ha usado.</span><span class="sxs-lookup"><span data-stu-id="8b90e-183">Close the browser tab you have been using.</span></span>

## <a name="sign-up-for-the-offer"></a><span data-ttu-id="8b90e-184">Suscribirse a la oferta</span><span class="sxs-lookup"><span data-stu-id="8b90e-184">Sign up for the offer</span></span>
1. <span data-ttu-id="8b90e-185">En una nueva ventana del explorador, vaya a la URL del portal de delegado que guardó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="8b90e-185">In a new browser window, go to the delegated portal URL you saved in the previous step.</span></span> <span data-ttu-id="8b90e-186">Inicie sesión como usuario del portal.</span><span class="sxs-lookup"><span data-stu-id="8b90e-186">Sign in to the portal as user.</span></span> <span data-ttu-id="8b90e-187">Nota: Use el portal de delegado para este paso,</span><span class="sxs-lookup"><span data-stu-id="8b90e-187">Note: Use the delegated portal for this step.</span></span> <span data-ttu-id="8b90e-188">si no la oferta delegada no será visible.</span><span class="sxs-lookup"><span data-stu-id="8b90e-188">The delegated offer are not visible otherwise.</span></span>
2. <span data-ttu-id="8b90e-189">En el panel, haga clic en **Obtener una suscripción**.</span><span class="sxs-lookup"><span data-stu-id="8b90e-189">In the dashboard, click **Get a subscription**.</span></span> <span data-ttu-id="8b90e-190">Verá que solo se presentan las ofertas delegadas que creó el proveedor delegado al usuario:</span><span class="sxs-lookup"><span data-stu-id="8b90e-190">You will see that only the delegated offers created by the delegated provider are presented to the user:</span></span>

> ![](media/azure-stack-delegated-provider/image8.png)
> 
> 

<span data-ttu-id="8b90e-191">Esto concluye el proceso de delegación de la oferta.</span><span class="sxs-lookup"><span data-stu-id="8b90e-191">This concludes the process of offer delegation.</span></span> <span data-ttu-id="8b90e-192">El usuario puede subscribirse a esta oferta obteniendo una suscripción para ella.</span><span class="sxs-lookup"><span data-stu-id="8b90e-192">The user can now sign up for this offer by getting a subscription for it.</span></span>

## <a name="multiple-tier-delegation"></a><span data-ttu-id="8b90e-193">Delegación de varios niveles</span><span class="sxs-lookup"><span data-stu-id="8b90e-193">Multiple-tier delegation</span></span>

<span data-ttu-id="8b90e-194">La delegación de varios niveles permite al proveedor delegado delegar la oferta a otras entidades.</span><span class="sxs-lookup"><span data-stu-id="8b90e-194">Multiple-tier delegation allows the delegated provider to delegate the offer to other entities.</span></span> <span data-ttu-id="8b90e-195">Esto permite, por ejemplo, la creación de canales de reventa más profundos, en los que el proveedor que administra Azure Stack delega una oferta a un distribuidor que, a su vez, la delega a un revendedor.</span><span class="sxs-lookup"><span data-stu-id="8b90e-195">This allows, for example, the creation of deeper reseller channels, in which the provider managing Azure Stack delegates an offer to a distributor, who in turn delegates to reseller.</span></span>
<span data-ttu-id="8b90e-196">Azure Stack admite hasta cinco niveles de delegación.</span><span class="sxs-lookup"><span data-stu-id="8b90e-196">Azure Stack supports up to five levels of delegation.</span></span>

<span data-ttu-id="8b90e-197">Para crear varios niveles de delegación de ofertas, el proveedor delegado, a su vez, delega la oferta al siguiente proveedor.</span><span class="sxs-lookup"><span data-stu-id="8b90e-197">To create multiple tiers of offer delegation, the delegated provider in turn delegates the offer to the next provider.</span></span> <span data-ttu-id="8b90e-198">El proceso es el mismo para el proveedor delegado que para el operador en la nube (consulte [El operador en la nube crea la oferta delegada](#cloud-operator-creates-the-delegated-offer)).</span><span class="sxs-lookup"><span data-stu-id="8b90e-198">The process is the same for the delegated provider as it was for the cloud operator (see [Cloud operator creates the delegated offer](#cloud-operator-creates-the-delegated-offer)).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b90e-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8b90e-199">Next steps</span></span>
[<span data-ttu-id="8b90e-200">Aprovisionar una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8b90e-200">Provision a VM</span></span>](azure-stack-provision-vm.md)

