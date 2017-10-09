---
title: aaaDelegating ofrece en la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooput otras personas a encargar de crear ofertas y suscribirse a los usuarios."
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
ms.openlocfilehash: d539cac3ed56f342338c830d95fbec7e93175929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delegating-offers-in-azure-stack"></a><span data-ttu-id="e8f02-103">Delegación de ofertas en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e8f02-103">Delegating offers in Azure Stack</span></span>

<span data-ttu-id="e8f02-104">Como operador de nube de Azure pila hello, a menudo es conveniente tooput otras personas a encargar de crear ofertas y suscribirse a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e8f02-104">As hello Azure Stack cloud operator, you often want tooput other people in charge of creating offers and signing up users for you.</span></span> <span data-ttu-id="e8f02-105">Por ejemplo, si es un proveedor de servicios y desea toosign de distribuidores de clientes y administrarlos en su nombre.</span><span class="sxs-lookup"><span data-stu-id="e8f02-105">For example, if you are a service provider and you want resellers toosign up customers and manage them on your behalf.</span></span> <span data-ttu-id="e8f02-106">También puede ocurrir en una empresa si forma parte de un grupo de TI central y desea divisiones o subsidiarias toosign configurar usuarios sin intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="e8f02-106">It can also happen in an enterprise if you are part of a central IT group and want divisions or subsidiaries toosign up users without your intervention.</span></span>

<span data-ttu-id="e8f02-107">La delegación ayuda a estas tareas, que ayudan a tooreach y administrar más usuarios sería capaz de toodo directamente.</span><span class="sxs-lookup"><span data-stu-id="e8f02-107">Delegation helps you with these tasks, helping you tooreach and manage more users than you would be able toodo directly.</span></span> <span data-ttu-id="e8f02-108">Hello en la ilustración siguiente se muestra un nivel de delegación, pero la pila de Azure es compatible con varios niveles.</span><span class="sxs-lookup"><span data-stu-id="e8f02-108">hello following illustration shows one level of delegation, but Azure Stack supports multiple levels.</span></span> <span data-ttu-id="e8f02-109">Proveedores de delegado a su vez pueden delegar tooother proveedores, los niveles de toofive.</span><span class="sxs-lookup"><span data-stu-id="e8f02-109">Delegated providers can in turn delegate tooother providers, up toofive levels.</span></span>

![](media/azure-stack-delegated-provider/image1.png)

<span data-ttu-id="e8f02-110">Los operadores de nube de Azure pila pueden delegar la creación de hello de usuarios tooother ofertas y los inquilinos mediante la funcionalidad de delegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f02-110">Azure Stack cloud operators can delegate hello creation of offers and tenants tooother users by using hello delegation functionality.</span></span>

## <a name="roles-and-steps-in-delegation"></a><span data-ttu-id="e8f02-111">Roles y pasos de la delegación</span><span class="sxs-lookup"><span data-stu-id="e8f02-111">Roles and steps in delegation</span></span>
<span data-ttu-id="e8f02-112">delegación de toounderstand, tenga en cuenta que hay tres roles implicados:</span><span class="sxs-lookup"><span data-stu-id="e8f02-112">toounderstand delegation, keep in mind that there are three roles involved:</span></span>

* <span data-ttu-id="e8f02-113">Hola **operador nube** administra la infraestructura de la pila de Azure de hello, crea una plantilla de oferta y delegados de otros usuarios para ofrecer a los usuarios de tootheir.</span><span class="sxs-lookup"><span data-stu-id="e8f02-113">hello **cloud operator** manages hello Azure Stack infrastructure, creates an offer template, and delegates others to offer it tootheir users.</span></span>
* <span data-ttu-id="e8f02-114">Hello en la nube delegados administradores se denomina **delegado proveedores**.</span><span class="sxs-lookup"><span data-stu-id="e8f02-114">hello delegated cloud administrators are called **delegated providers**.</span></span> <span data-ttu-id="e8f02-115">Pertenezcan tooother organizaciones (por ejemplo, otros inquilinos de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e8f02-115">They can belong tooother organizations (such as other Azure Active Directory tenants).</span></span>
* <span data-ttu-id="e8f02-116">**Los usuarios** suscribirse a ofertas de Hola y usarlas para administrar sus cargas de trabajo, crear máquinas virtuales, almacenamiento de datos, etcetera.</span><span class="sxs-lookup"><span data-stu-id="e8f02-116">**Users** sign up for hello offers and use them for managing their workloads, creating VMs, storing data, etc.</span></span>

<span data-ttu-id="e8f02-117">Como se muestra en el siguiente gráfico de hello, hay dos pasos para configurar la delegación.</span><span class="sxs-lookup"><span data-stu-id="e8f02-117">As shown in hello following graphic, there are two steps in setting up delegation.</span></span>

1. <span data-ttu-id="e8f02-118">**Identificar los proveedores de hello delegada** suscribiéndose a tooan oferta basado en un plan que contiene solo el servicio de suscripciones Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f02-118">**Identify hello delegated providers** by subscribing them tooan offer based on a plan that contains only hello subscriptions service.</span></span>
   <span data-ttu-id="e8f02-119">Los usuarios que se suscriben toothis oferta adquirir algunas de las capacidades del Administrador de la nube de hello, incluidos Hola capacidad tooextend ofertas y usuarios de inicio de sesión para disfrutar de ellos.</span><span class="sxs-lookup"><span data-stu-id="e8f02-119">Users who subscribe toothis offer acquire some of hello cloud administrator’s capabilities, including hello ability tooextend offers and sign users up for them.</span></span>
2. <span data-ttu-id="e8f02-120">**Delegado una oferta toohello delegado proveedor**, esta oferta funciona como una plantilla para qué Hola proveedor delegado puede ofrecer.</span><span class="sxs-lookup"><span data-stu-id="e8f02-120">**Delegate an offer toohello delegated provider**, this offer functions as a template for what hello delegated provider can offer.</span></span> <span data-ttu-id="e8f02-121">Hello proveedor delegado es ahora tootake capaz de hello oferta, elija un nombre para ella (pero no cambiar sus servicios y cuotas) y ofrecen toocustomers.</span><span class="sxs-lookup"><span data-stu-id="e8f02-121">hello delegated provider is now able tootake hello offer, choose a name for it (but not change its services and quotas), and offer it toocustomers.</span></span>

![](media/azure-stack-delegated-provider/image2.png)

<span data-ttu-id="e8f02-122">tooact como proveedores de delegados, los usuarios necesitan tooestablish una relación con el proveedor principal de hello; en otras palabras, deben toocreate una suscripción.</span><span class="sxs-lookup"><span data-stu-id="e8f02-122">tooact as delegated providers, users need tooestablish a relationship with hello main provider; in other words, they need toocreate a subscription.</span></span> <span data-ttu-id="e8f02-123">En este escenario, esta suscripción identifica los proveedores de delegado como si tuviera derecho toopresent ofrece en nombre de proveedor principal de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f02-123">In this scenario, this subscription identifies the delegated providers as having hello right toopresent offers on behalf of hello main provider.</span></span>

<span data-ttu-id="e8f02-124">Una vez establecida esta relación, operador de hello en la nube puede delegar un proveedor de la oferta de toohello delegados.</span><span class="sxs-lookup"><span data-stu-id="e8f02-124">Once this relationship is established, hello cloud operator can delegate an offer toohello delegated provider.</span></span> <span data-ttu-id="e8f02-125">Hello proveedor delegado es ahora tootake capaz de hello oferta, cámbiele el nombre (pero no cambiar su sustancia) y ofrecen tooits clientes.</span><span class="sxs-lookup"><span data-stu-id="e8f02-125">hello delegated provider is now able tootake hello offer, rename it (but not change its substance), and offer it tooits customers.</span></span>

<span data-ttu-id="e8f02-126">Hola las secciones siguientes describe cómo delegar una oferta tooestablish un proveedor de delegados y compruebe que los usuarios pueden suscribirse para él.</span><span class="sxs-lookup"><span data-stu-id="e8f02-126">hello following sections describe how tooestablish a delegated provider, delegate an offer, and verify that users can sign up for it.</span></span>

## <a name="set-up-roles"></a><span data-ttu-id="e8f02-127">Configurar los roles</span><span class="sxs-lookup"><span data-stu-id="e8f02-127">Set up roles</span></span>

<span data-ttu-id="e8f02-128">toosee un proveedor de delegado en el trabajo, necesita cuentas de Azure Active Directory adicionales en la cuenta de operador de suma tooyour en la nube.</span><span class="sxs-lookup"><span data-stu-id="e8f02-128">toosee a delegated provider at work, you need additional Azure Active Directory accounts in addition tooyour cloud operator account.</span></span> <span data-ttu-id="e8f02-129">Si no los tiene, cree Hola dos cuentas.</span><span class="sxs-lookup"><span data-stu-id="e8f02-129">If you do not have them, create hello two accounts.</span></span> <span data-ttu-id="e8f02-130">las cuentas de Hello pueden pertenecer a tooany inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="e8f02-130">hello accounts can belong tooany AAD tenant.</span></span> <span data-ttu-id="e8f02-131">Nos referimos toothem como Hola había delegada proveedor (DP) y el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f02-131">We refer toothem as hello delegated provider (DP) and hello user.</span></span>

| <span data-ttu-id="e8f02-132">**Rol**</span><span class="sxs-lookup"><span data-stu-id="e8f02-132">**Role**</span></span> | <span data-ttu-id="e8f02-133">**Derechos organizativos**</span><span class="sxs-lookup"><span data-stu-id="e8f02-133">**Organizational rights**</span></span> |
| --- | --- |
| <span data-ttu-id="e8f02-134">Proveedor delegado</span><span class="sxs-lookup"><span data-stu-id="e8f02-134">Delegated Provider</span></span> |<span data-ttu-id="e8f02-135">Usuario</span><span class="sxs-lookup"><span data-stu-id="e8f02-135">User</span></span> |
| <span data-ttu-id="e8f02-136">Usuario</span><span class="sxs-lookup"><span data-stu-id="e8f02-136">User</span></span> |<span data-ttu-id="e8f02-137">Usuario</span><span class="sxs-lookup"><span data-stu-id="e8f02-137">User</span></span> |

## <a name="identify-hello-delegated-providers"></a><span data-ttu-id="e8f02-138">Identificar los proveedores de hello delegada</span><span class="sxs-lookup"><span data-stu-id="e8f02-138">Identify hello delegated providers</span></span>
1. <span data-ttu-id="e8f02-139">Inicie sesión como operador en la nube.</span><span class="sxs-lookup"><span data-stu-id="e8f02-139">Sign in as cloud operator.</span></span>
2. <span data-ttu-id="e8f02-140">Crear una oferta de Hola que permite a los usuarios toobecome delegado proveedores.</span><span class="sxs-lookup"><span data-stu-id="e8f02-140">Create hello offer that enables users toobecome delegated providers.</span></span> <span data-ttu-id="e8f02-141">Esto requiere la creación de un plan y una oferta basada en este:</span><span class="sxs-lookup"><span data-stu-id="e8f02-141">This requires that you create a plan and an offer based on it:</span></span>
   
   <span data-ttu-id="e8f02-142">a.</span><span class="sxs-lookup"><span data-stu-id="e8f02-142">a.</span></span>  <span data-ttu-id="e8f02-143">[Cree un plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="e8f02-143">[Create a plan](azure-stack-create-plan.md).</span></span>
       <span data-ttu-id="e8f02-144">Este plan debe incluir solo el servicio de suscripciones Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f02-144">This plan should include only hello subscriptions service.</span></span> <span data-ttu-id="e8f02-145">En este artículo, se usa un plan denominado PlanForDelegation.</span><span class="sxs-lookup"><span data-stu-id="e8f02-145">In this article, we use a plan called PlanForDelegation.</span></span>
   
   <span data-ttu-id="e8f02-146">b.</span><span class="sxs-lookup"><span data-stu-id="e8f02-146">b.</span></span>  <span data-ttu-id="e8f02-147">[Cree una oferta](azure-stack-create-offer.md) en función de este plan.</span><span class="sxs-lookup"><span data-stu-id="e8f02-147">[Create an offer](azure-stack-create-offer.md) based on this plan.</span></span> <span data-ttu-id="e8f02-148">En este artículo, usamos una oferta denominada OfferToDP.</span><span class="sxs-lookup"><span data-stu-id="e8f02-148">In this article, we use an offer called OfferToDP.</span></span>
   
   <span data-ttu-id="e8f02-149">c.</span><span class="sxs-lookup"><span data-stu-id="e8f02-149">c.</span></span>  <span data-ttu-id="e8f02-150">Una vez completada la creación de hello de oferta de hello, agregar proveedor delegados de hello como una oferta de toothis de suscriptor, haga clic en **suscripciones** &gt; **agregar** &gt; **nuevo Suscripción de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="e8f02-150">Once hello creation of hello offer is complete, add hello delegated provider as a subscriber toothis offer by clicking **Subscriptions** &gt; **Add** &gt; **New Tenant Subscription**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> <span data-ttu-id="e8f02-151">Como con todas las ofertas de pila de Azure, tiene la opción de Hola de hacer que la oferta de hello públicas y permitiéndole usuarios suscribirse a él o mantener privado y tienen operador en la nube de hello administrar Hola inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e8f02-151">As with all Azure Stack offers, you have hello option of making hello offer public and letting users sign up for it, or keeping it private and have hello cloud operator manage hello sign-up.</span></span> <span data-ttu-id="e8f02-152">Proveedores de delegados suelen ser un pequeño grupo y desea toocontrol que se admitan tooit, por lo que mantener esta oferta privada tiene sentido en la mayoría de los casos.</span><span class="sxs-lookup"><span data-stu-id="e8f02-152">Delegated providers are usually a small group and you want toocontrol who is admitted tooit, so keeping this offer private makes sense in most cases.</span></span>
> 
> 

## <a name="cloud-operator-creates-hello-delegated-offer"></a><span data-ttu-id="e8f02-153">Operador de nube crea Hola delegados oferta</span><span class="sxs-lookup"><span data-stu-id="e8f02-153">Cloud operator creates hello delegated offer</span></span>

<span data-ttu-id="e8f02-154">Ya ha establecido su proveedor delegado.</span><span class="sxs-lookup"><span data-stu-id="e8f02-154">You have now established your delegated provider.</span></span> <span data-ttu-id="e8f02-155">paso siguiente Hola consiste en Crear plan de Hola y ofrecer que se van toodelegate y que utilizarán los clientes.</span><span class="sxs-lookup"><span data-stu-id="e8f02-155">hello next step is to create hello plan and offer that you are going toodelegate, and which your customers will use.</span></span> <span data-ttu-id="e8f02-156">Debe definir esta oferta exactamente como desea que los clientes toosee, porque Hola delegada proveedor no podrá cambiar los planes de Hola y las cuotas que incluye.</span><span class="sxs-lookup"><span data-stu-id="e8f02-156">You should define this offer exactly as you want the customers toosee it, because hello delegated provider will not be able to change hello plans and quotas it includes.</span></span>

1. <span data-ttu-id="e8f02-157">Como operador en la nube, [cree un plan](azure-stack-create-plan.md) y [una oferta](azure-stack-create-offer.md) basada en él.</span><span class="sxs-lookup"><span data-stu-id="e8f02-157">As cloud operator, [create a plan](azure-stack-create-plan.md) and [an offer](azure-stack-create-offer.md) based on it.</span></span> <span data-ttu-id="e8f02-158">En este artículo, usamos una oferta denominada DelegatedOffer.</span><span class="sxs-lookup"><span data-stu-id="e8f02-158">For this article, we use an offer called DelegatedOffer.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e8f02-159">Esta oferta no tiene toobe público.</span><span class="sxs-lookup"><span data-stu-id="e8f02-159">This offer does not have toobe public.</span></span> <span data-ttu-id="e8f02-160">Se pueda hacer público si elige pero, en la mayoría de los casos, solo desea delegados proveedores toohave acceso tooit.</span><span class="sxs-lookup"><span data-stu-id="e8f02-160">It can be made public if you choose, but, in most cases, you only want delegated providers toohave access tooit.</span></span> <span data-ttu-id="e8f02-161">Una vez delegar una oferta privada como se describe en los pasos de hello, proveedor delegados hello tiene acceso tooit.</span><span class="sxs-lookup"><span data-stu-id="e8f02-161">Once you delegate a private offer as described in hello following steps, hello delegated provider has access tooit.</span></span>
   > 
   > 
1. <span data-ttu-id="e8f02-162">Oferta de Hola de delegado.</span><span class="sxs-lookup"><span data-stu-id="e8f02-162">Delegate hello offer.</span></span> <span data-ttu-id="e8f02-163">TooDelegatedOffer y, en el panel de configuración de hello, haga clic en **delegado proveedores** &gt; **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e8f02-163">Go tooDelegatedOffer, and in hello Settings pane, click **Delegated Providers** &gt; **Add**.</span></span>
2. <span data-ttu-id="e8f02-164">Seleccionar suscripción del proveedor de hello delegada de cuadro de lista desplegable de Hola y haga clic en **delegado**.</span><span class="sxs-lookup"><span data-stu-id="e8f02-164">Select hello delegated provider’s subscription from hello drop-down list box and click **Delegate**.</span></span>

> ![](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-hello-offer"></a><span data-ttu-id="e8f02-165">Proveedor de delegado personaliza oferta Hola</span><span class="sxs-lookup"><span data-stu-id="e8f02-165">Delegated provider customizes hello offer</span></span>

<span data-ttu-id="e8f02-166">Inicie sesión en toohello **portal del inquilino** como Hola delega el proveedor y crear una oferta nueva con hello delegados oferta como una plantilla.</span><span class="sxs-lookup"><span data-stu-id="e8f02-166">Sign in toohello **tenant portal** as hello delegated provider and create a new offer using hello delegated offer as a template.</span></span>

1. <span data-ttu-id="e8f02-167">Haga clic en **Nueva** &gt; **Ofertas + Planes de inquilinos** &gt; **Oferta**.</span><span class="sxs-lookup"><span data-stu-id="e8f02-167">Click **New** &gt; **Tenant Offers + Plans** &gt; **Offer**.</span></span>

    ![](media/azure-stack-delegated-provider/image5.png)


1. <span data-ttu-id="e8f02-168">Asignar una oferta de toohello nombre.</span><span class="sxs-lookup"><span data-stu-id="e8f02-168">Assign a name toohello offer.</span></span> <span data-ttu-id="e8f02-169">Aquí elegiremos ResellerOffer.</span><span class="sxs-lookup"><span data-stu-id="e8f02-169">Here we choose ResellerOffer.</span></span> <span data-ttu-id="e8f02-170">Seleccione Hola delegado toobase de oferta en y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="e8f02-170">Select hello delegated offer toobase it on and then click **Create**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > <span data-ttu-id="e8f02-171">Nota Hola diferencia en comparación con creación de toooffer igual que las experimentadas por el operador de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="e8f02-171">Note hello difference compared toooffer creation as experienced by hello cloud operator.</span></span> <span data-ttu-id="e8f02-172">proveedor de delegados de Hello no construye Hola oferta de planes de base y complemento; solo pueden elegir de ofertas que se han delegado toothem y no se puede realizar cambios toothose ofertas.</span><span class="sxs-lookup"><span data-stu-id="e8f02-172">hello delegated provider does not construct hello offer from base plans and add-on plans; they can only choose from offers that have been delegated toothem, and can't make changes toothose offers.</span></span>

1. <span data-ttu-id="e8f02-173">Hacer Hola ofrecen público haciendo clic en **examinar** &gt; **ofrece**, seleccionar la oferta de Hola y haga clic en **cambio de estado**.</span><span class="sxs-lookup"><span data-stu-id="e8f02-173">Make hello offer public by clicking **Browse** &gt; **Offers**, selecting hello offer, and clicking **Change State**.</span></span>
2. <span data-ttu-id="e8f02-174">proveedor delegado Hello expone estas ofertas a través de su propio portal de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e8f02-174">hello delegated provider exposes these offers through their own portal URL.</span></span> <span data-ttu-id="e8f02-175">Estas ofertas son visibles solo a través de portal de hello delegada.</span><span class="sxs-lookup"><span data-stu-id="e8f02-175">These offers are visible only through hello delegated portal.</span></span> <span data-ttu-id="e8f02-176">toofind y cambiar esta dirección URL:</span><span class="sxs-lookup"><span data-stu-id="e8f02-176">toofind and change this URL:</span></span>
   
    <span data-ttu-id="e8f02-177">a.</span><span class="sxs-lookup"><span data-stu-id="e8f02-177">a.</span></span>  <span data-ttu-id="e8f02-178">Haga clic en **examinar** &gt; **más servicios** &gt; **suscripciones** &gt; Hola seleccione delegada suscripción del proveedor, en nuestro caso su *DPSubscription* &gt; **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="e8f02-178">Click **Browse**&gt; **More services**&gt; **Subscriptions**&gt; Select hello delegated provider subscription, in our case its *DPSubscription*&gt; **Properties**.</span></span>
   
    <span data-ttu-id="e8f02-179">b.</span><span class="sxs-lookup"><span data-stu-id="e8f02-179">b.</span></span>  <span data-ttu-id="e8f02-180">Copie Hola portal URL tooa ubicación independiente, como el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="e8f02-180">Copy hello portal URL tooa separate location, such as Notepad.</span></span>
   
    ![](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   <span data-ttu-id="e8f02-181">Ahora ha completado la creación de hello de una oferta delegada como un proveedor de delegado.</span><span class="sxs-lookup"><span data-stu-id="e8f02-181">You have now completed hello creation of a delegated offer as a delegated provider.</span></span> <span data-ttu-id="e8f02-182">Cierre la sesión como Hola proveedor delegado.</span><span class="sxs-lookup"><span data-stu-id="e8f02-182">Sign out as hello delegated provider.</span></span> <span data-ttu-id="e8f02-183">Cerrar la pestaña de explorador Hola que ha utilizado.</span><span class="sxs-lookup"><span data-stu-id="e8f02-183">Close hello browser tab you have been using.</span></span>

## <a name="sign-up-for-hello-offer"></a><span data-ttu-id="e8f02-184">Suscríbase a Hola oferta</span><span class="sxs-lookup"><span data-stu-id="e8f02-184">Sign up for hello offer</span></span>
1. <span data-ttu-id="e8f02-185">En una nueva ventana del explorador, vaya portal delegados toohello dirección URL que guardó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f02-185">In a new browser window, go toohello delegated portal URL you saved in hello previous step.</span></span> <span data-ttu-id="e8f02-186">Inicie sesión en el portal de toohello como usuario.</span><span class="sxs-lookup"><span data-stu-id="e8f02-186">Sign in toohello portal as user.</span></span> <span data-ttu-id="e8f02-187">Nota: Hola Use delegados portal para este paso.</span><span class="sxs-lookup"><span data-stu-id="e8f02-187">Note: Use hello delegated portal for this step.</span></span> <span data-ttu-id="e8f02-188">oferta delegados de Hello no son visibles en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="e8f02-188">hello delegated offer are not visible otherwise.</span></span>
2. <span data-ttu-id="e8f02-189">En el panel de hello, haga clic en **obtener una suscripción**.</span><span class="sxs-lookup"><span data-stu-id="e8f02-189">In hello dashboard, click **Get a subscription**.</span></span> <span data-ttu-id="e8f02-190">Verá que sólo proporciona Hola delegado creado por el proveedor de hello delegada se presenta toohello usuario:</span><span class="sxs-lookup"><span data-stu-id="e8f02-190">You will see that only hello delegated offers created by hello delegated provider are presented toohello user:</span></span>

> ![](media/azure-stack-delegated-provider/image8.png)
> 
> 

<span data-ttu-id="e8f02-191">Esto concluye el proceso de Hola de delegación de la oferta.</span><span class="sxs-lookup"><span data-stu-id="e8f02-191">This concludes hello process of offer delegation.</span></span> <span data-ttu-id="e8f02-192">usuario de Hello ahora puede registrarse en esta oferta obteniendo una suscripción para ella.</span><span class="sxs-lookup"><span data-stu-id="e8f02-192">hello user can now sign up for this offer by getting a subscription for it.</span></span>

## <a name="multiple-tier-delegation"></a><span data-ttu-id="e8f02-193">Delegación de varios niveles</span><span class="sxs-lookup"><span data-stu-id="e8f02-193">Multiple-tier delegation</span></span>

<span data-ttu-id="e8f02-194">Delegación de varios niveles permite Hola delegada proveedor toodelegate las entidades de tooother de oferta.</span><span class="sxs-lookup"><span data-stu-id="e8f02-194">Multiple-tier delegation allows hello delegated provider toodelegate the offer tooother entities.</span></span> <span data-ttu-id="e8f02-195">Esto permite, por ejemplo, creación de hello de canales de reseller un poco más, en el que hello proveedor administra Azure pila delega un distribuidor de tooa oferta, que a su vez delega tooreseller.</span><span class="sxs-lookup"><span data-stu-id="e8f02-195">This allows, for example, hello creation of deeper reseller channels, in which hello provider managing Azure Stack delegates an offer tooa distributor, who in turn delegates tooreseller.</span></span>
<span data-ttu-id="e8f02-196">Pila de Azure es compatible con los niveles de toofive de delegación.</span><span class="sxs-lookup"><span data-stu-id="e8f02-196">Azure Stack supports up toofive levels of delegation.</span></span>

<span data-ttu-id="e8f02-197">toocreate varios niveles de ofrecen la delegación, proveedor delegados Hola delega a su vez toohello siguiente proveedor de oferta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8f02-197">toocreate multiple tiers of offer delegation, hello delegated provider in turn delegates hello offer toohello next provider.</span></span> <span data-ttu-id="e8f02-198">proceso Hello es Hola igual para proveedor delegados de Hola igual que con el operador de hello en la nube (consulte [operador en la nube crea Hola delegados oferta](#cloud-operator-creates-the-delegated-offer)).</span><span class="sxs-lookup"><span data-stu-id="e8f02-198">hello process is hello same for hello delegated provider as it was for hello cloud operator (see [Cloud operator creates hello delegated offer](#cloud-operator-creates-the-delegated-offer)).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8f02-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e8f02-199">Next steps</span></span>
[<span data-ttu-id="e8f02-200">Aprovisionar una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e8f02-200">Provision a VM</span></span>](azure-stack-provision-vm.md)

