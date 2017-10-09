---
title: aaaAzure administra las aplicaciones de hello Marketplace | Documentos de Microsoft
description: "Azure se describen las aplicaciones que están disponibles a través de hello Marketplace administrado."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="02c7a-103">Las aplicaciones de Hola Marketplace administrado de Azure</span><span class="sxs-lookup"><span data-stu-id="02c7a-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="02c7a-104">Pueden usar varios MSP, ISV e integradores de sistema (SIs) Azure administra aplicaciones toooffer sus clientes de Azure Marketplace de soluciones tooall.</span><span class="sxs-lookup"><span data-stu-id="02c7a-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="02c7a-105">Estas soluciones reducen mantenimiento hello y sobrecarga de mantenimiento para los clientes.</span><span class="sxs-lookup"><span data-stu-id="02c7a-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="02c7a-106">Pueden vender publicadores de infraestructura y el software a través de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="02c7a-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="02c7a-107">Pueden adjuntar soporte operacional toomanaged aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="02c7a-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="02c7a-108">Para más información, consulte [Información general sobre las aplicaciones administradas](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="02c7a-109">Este artículo explica cómo un MSP, ISV o SI puede publicar un toohello aplicación Marketplace y hacer que toocustomers ampliamente disponibles.</span><span class="sxs-lookup"><span data-stu-id="02c7a-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="02c7a-110">Requisitos previos para publicar una aplicación administrada</span><span class="sxs-lookup"><span data-stu-id="02c7a-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="02c7a-111">Requisitos previos toolisting Hola Marketplace:</span><span class="sxs-lookup"><span data-stu-id="02c7a-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="02c7a-112">Requisitos previos técnicos</span><span class="sxs-lookup"><span data-stu-id="02c7a-112">Technical</span></span>

    *  <span data-ttu-id="02c7a-113">Para obtener información acerca de la estructura básica de Hola y la sintaxis de plantillas del Administrador de recursos de Azure, consulte [plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="02c7a-114">soluciones de tooview plantilla completa, consulte [plantillas de inicio rápido de Azure](https://azure.microsoft.com/en-us/documentation/templates/) o hello [repositorio de plantilla de inicio rápido](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="02c7a-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="02c7a-115">Para obtener información acerca de cómo toocreate Hola interfaz para los clientes que implementación la aplicación a través de hello Marketplace, vea [crear un archivo de definición de interfaz de usuario](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="02c7a-116">Requisitos previos no técnicos (empresariales)</span><span class="sxs-lookup"><span data-stu-id="02c7a-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="02c7a-117">Su empresa o sus filiales deben encontrarse en un país o región donde se admiten las ventas por hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="02c7a-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="02c7a-118">Debe tener una licencia del producto de forma que sea compatible con facturación modelos admitidos por hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="02c7a-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="02c7a-119">Es responsabilidad suya toocustomers de soporte técnico disponibles de manera comercialmente razonable.</span><span class="sxs-lookup"><span data-stu-id="02c7a-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="02c7a-120">compatibilidad de Hello puede ser libre, de pago, o a través de la Comunidad de soporte.</span><span class="sxs-lookup"><span data-stu-id="02c7a-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="02c7a-121">Asimismo, es responsable de la concesión de licencias para su software y las dependencias de software de terceros.</span><span class="sxs-lookup"><span data-stu-id="02c7a-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="02c7a-122">Debe proporcionar el contenido que cumpla los criterios de la oferta toobe enumerados en el Marketplace de Hola y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="02c7a-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="02c7a-123">Debe aceptar toohello términos del acuerdo de publicador y directivas de participación de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="02c7a-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="02c7a-124">Debe aceptar toocomply con hello las condiciones de uso, la declaración de privacidad de Microsoft y contrato de programa de certificación de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="02c7a-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="02c7a-125">Creación de una nueva oferta de aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="02c7a-125">Create a new Azure application offer</span></span>

<span data-ttu-id="02c7a-126">Después de cumplir los requisitos previos de hello, está listo toocreate su oferta de la aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="02c7a-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="02c7a-127">Hagamos un repaso rápido a los conceptos de oferta y de SKU.</span><span class="sxs-lookup"><span data-stu-id="02c7a-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="02c7a-128">Oferta</span><span class="sxs-lookup"><span data-stu-id="02c7a-128">Offer</span></span>

<span data-ttu-id="02c7a-129">oferta de Hola para una aplicación administrada corresponde tooa clase de producto de la oferta de un publicador.</span><span class="sxs-lookup"><span data-stu-id="02c7a-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="02c7a-130">Si tiene un nuevo tipo de solución o aplicación que desea toomake disponible en hello Marketplace, se puede configurar como una oferta nueva.</span><span class="sxs-lookup"><span data-stu-id="02c7a-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="02c7a-131">Una oferta es una colección de SKU.</span><span class="sxs-lookup"><span data-stu-id="02c7a-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="02c7a-132">Cada oferta aparece como su propia entidad Hola Marketplace.</span><span class="sxs-lookup"><span data-stu-id="02c7a-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="02c7a-133">SKU</span><span class="sxs-lookup"><span data-stu-id="02c7a-133">SKU</span></span>

<span data-ttu-id="02c7a-134">Un SKU es Hola unidad más pequeña puede adquirir de una oferta.</span><span class="sxs-lookup"><span data-stu-id="02c7a-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="02c7a-135">Puede usar una SKU de hello mismo producto (oferta) de la clase toodifferentiate entre:</span><span class="sxs-lookup"><span data-stu-id="02c7a-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="02c7a-136">Distintas características que se admiten.</span><span class="sxs-lookup"><span data-stu-id="02c7a-136">Different features that are supported.</span></span>
* <span data-ttu-id="02c7a-137">Si la oferta de hello es managed o unmanaged.</span><span class="sxs-lookup"><span data-stu-id="02c7a-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="02c7a-138">Los modelos de facturación que se admiten.</span><span class="sxs-lookup"><span data-stu-id="02c7a-138">Billing models that are supported.</span></span>

<span data-ttu-id="02c7a-139">Una SKU aparece debajo de la oferta de primario Hola Hola Marketplace.</span><span class="sxs-lookup"><span data-stu-id="02c7a-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="02c7a-140">Aparece como su propia entidad puede adquirir en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="02c7a-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="02c7a-141">Configuración de una oferta</span><span class="sxs-lookup"><span data-stu-id="02c7a-141">Set up an offer</span></span>

1. <span data-ttu-id="02c7a-142">Inicie sesión en toohello [portal de partners de nube](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="02c7a-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="02c7a-143">En el panel de navegación de Hola Hola izquierda, seleccione **+ oferta nueva** > **aplicaciones de Azure**.</span><span class="sxs-lookup"><span data-stu-id="02c7a-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Nueva oferta](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="02c7a-145">Rellenar formularios de Hola que aparecen en hello restante en hello **Editor** vista.</span><span class="sxs-lookup"><span data-stu-id="02c7a-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="02c7a-146">Los campos obligatorios están marcados con un asterisco rojo (*).</span><span class="sxs-lookup"><span data-stu-id="02c7a-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Configuración de oferta](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="02c7a-148">Cuatro formas básicas son toocreate usa una aplicación administrada:</span><span class="sxs-lookup"><span data-stu-id="02c7a-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="02c7a-149">a.</span><span class="sxs-lookup"><span data-stu-id="02c7a-149">a.</span></span> <span data-ttu-id="02c7a-150">Configuración de oferta</span><span class="sxs-lookup"><span data-stu-id="02c7a-150">Offer Settings</span></span>

    <span data-ttu-id="02c7a-151">b.</span><span class="sxs-lookup"><span data-stu-id="02c7a-151">b.</span></span> <span data-ttu-id="02c7a-152">SKU</span><span class="sxs-lookup"><span data-stu-id="02c7a-152">SKUs</span></span>

    <span data-ttu-id="02c7a-153">c.</span><span class="sxs-lookup"><span data-stu-id="02c7a-153">c.</span></span> <span data-ttu-id="02c7a-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="02c7a-154">Marketplace</span></span>

    <span data-ttu-id="02c7a-155">d.</span><span class="sxs-lookup"><span data-stu-id="02c7a-155">d.</span></span> <span data-ttu-id="02c7a-156">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="02c7a-156">Support</span></span>

<span data-ttu-id="02c7a-157">Estos formatos se describen con más detalle en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="02c7a-158">Formulario de configuración de oferta</span><span class="sxs-lookup"><span data-stu-id="02c7a-158">Offer Settings form</span></span>
<span data-ttu-id="02c7a-159">Use esta configuración de oferta de forma básica toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="02c7a-160">Rellene hello **ofrecen configuración** formulario.</span><span class="sxs-lookup"><span data-stu-id="02c7a-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="02c7a-161">Hola distintos campos son:</span><span class="sxs-lookup"><span data-stu-id="02c7a-161">hello different fields are:</span></span>

    <span data-ttu-id="02c7a-162">a.</span><span class="sxs-lookup"><span data-stu-id="02c7a-162">a.</span></span> <span data-ttu-id="02c7a-163">**Identificador de la oferta**: este identificador único identifica Hola oferta dentro de un perfil de publicador.</span><span class="sxs-lookup"><span data-stu-id="02c7a-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="02c7a-164">Este identificador se muestra en las direcciones URL de producto, las plantillas de Resource Manager y los informes de facturación.</span><span class="sxs-lookup"><span data-stu-id="02c7a-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="02c7a-165">Puede contener solo caracteres alfanuméricos en minúscula o guiones (-).</span><span class="sxs-lookup"><span data-stu-id="02c7a-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="02c7a-166">Id. de Hello no puede terminar con un guión.</span><span class="sxs-lookup"><span data-stu-id="02c7a-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="02c7a-167">Es limitado tooa máximo de 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="02c7a-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="02c7a-168">En cuanto se lanza una oferta, este campo se bloquea.</span><span class="sxs-lookup"><span data-stu-id="02c7a-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="02c7a-169">b.</span><span class="sxs-lookup"><span data-stu-id="02c7a-169">b.</span></span> <span data-ttu-id="02c7a-170">**Id. de publicador**: usar este perfil de publicador de lista desplegable toochoose Hola desea toopublish esta oferta en.</span><span class="sxs-lookup"><span data-stu-id="02c7a-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="02c7a-171">En cuanto se lanza una oferta, este campo se bloquea.</span><span class="sxs-lookup"><span data-stu-id="02c7a-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="02c7a-172">c.</span><span class="sxs-lookup"><span data-stu-id="02c7a-172">c.</span></span> <span data-ttu-id="02c7a-173">**Nombre**: este nombre para mostrar para su oferta aparece en hello Marketplace y en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="02c7a-174">Puede tener un máximo de 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="02c7a-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="02c7a-175">Incluya un nombre de marca que identifique el producto.</span><span class="sxs-lookup"><span data-stu-id="02c7a-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="02c7a-176">No incluya aquí el nombre de su empresa a menos que sea así como se comercializa.</span><span class="sxs-lookup"><span data-stu-id="02c7a-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="02c7a-177">Si está marketing esta oferta en su propio sitio Web, asegúrese de que ese nombre hello es exactamente cómo aparece en el sitio Web.</span><span class="sxs-lookup"><span data-stu-id="02c7a-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="02c7a-178">Seleccione **guardar** toosave su progreso.</span><span class="sxs-lookup"><span data-stu-id="02c7a-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="02c7a-179">Formulario de SKU</span><span class="sxs-lookup"><span data-stu-id="02c7a-179">SKUs form</span></span>
<span data-ttu-id="02c7a-180">Hola siguiente paso es tooadd SKU para su oferta.</span><span class="sxs-lookup"><span data-stu-id="02c7a-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="02c7a-181">Seleccione **SKU** > **SKU nueva**.</span><span class="sxs-lookup"><span data-stu-id="02c7a-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Selección de SKU nueva](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="02c7a-183">Escriba un **Identificador de SKU**.</span><span class="sxs-lookup"><span data-stu-id="02c7a-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="02c7a-184">Un identificador de SKU es un identificador único para hello SKU dentro de una oferta.</span><span class="sxs-lookup"><span data-stu-id="02c7a-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="02c7a-185">Este identificador se muestra en las direcciones URL de producto, las plantillas de Resource Manager y los informes de facturación.</span><span class="sxs-lookup"><span data-stu-id="02c7a-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="02c7a-186">Puede contener solo caracteres alfanuméricos en minúscula o guiones (-).</span><span class="sxs-lookup"><span data-stu-id="02c7a-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="02c7a-187">Id. de Hello no puede terminar con un guión y es limitado tooa máximo de 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="02c7a-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="02c7a-188">En cuanto se lanza una oferta, este campo se bloquea.</span><span class="sxs-lookup"><span data-stu-id="02c7a-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="02c7a-189">Puede tener varias SKU dentro de una oferta.</span><span class="sxs-lookup"><span data-stu-id="02c7a-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="02c7a-190">Necesita una SKU para cada imagen piensa toopublish.</span><span class="sxs-lookup"><span data-stu-id="02c7a-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="02c7a-191">Rellene hello **detalles del SKU** sección en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="02c7a-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![Proporcionar una nueva SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="02c7a-193">Rellene Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="02c7a-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="02c7a-194">a.</span><span class="sxs-lookup"><span data-stu-id="02c7a-194">a.</span></span> <span data-ttu-id="02c7a-195">**Título**: escriba un título para esta SKU.</span><span class="sxs-lookup"><span data-stu-id="02c7a-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="02c7a-196">Este título aparece en la Galería de Hola para este elemento.</span><span class="sxs-lookup"><span data-stu-id="02c7a-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="02c7a-197">b.</span><span class="sxs-lookup"><span data-stu-id="02c7a-197">b.</span></span> <span data-ttu-id="02c7a-198">**Resumen**: proporcione un breve resumen de esta SKU.</span><span class="sxs-lookup"><span data-stu-id="02c7a-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="02c7a-199">Este texto aparece debajo del título de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="02c7a-200">c.</span><span class="sxs-lookup"><span data-stu-id="02c7a-200">c.</span></span> <span data-ttu-id="02c7a-201">**Descripción**: escriba una descripción detallada acerca de hello SKU.</span><span class="sxs-lookup"><span data-stu-id="02c7a-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="02c7a-202">d.</span><span class="sxs-lookup"><span data-stu-id="02c7a-202">d.</span></span> <span data-ttu-id="02c7a-203">**Tipo de SKU**: Hola valores permitidos son **aplicación administrada** y **plantillas de solución**.</span><span class="sxs-lookup"><span data-stu-id="02c7a-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="02c7a-204">En este caso, seleccione **Aplicación administrada**.</span><span class="sxs-lookup"><span data-stu-id="02c7a-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="02c7a-205">Rellene hello **detalles del paquete** sección en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="02c7a-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![Paquete](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="02c7a-207">Rellene Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="02c7a-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="02c7a-208">a.</span><span class="sxs-lookup"><span data-stu-id="02c7a-208">a.</span></span> <span data-ttu-id="02c7a-209">**Versión actual**: escriba una versión de paquete de hello cargar.</span><span class="sxs-lookup"><span data-stu-id="02c7a-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="02c7a-210">Debe estar en formato de hello `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="02c7a-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="02c7a-211">b.</span><span class="sxs-lookup"><span data-stu-id="02c7a-211">b.</span></span> <span data-ttu-id="02c7a-212">**Seleccione un archivo de paquete**: este paquete contiene los siguientes archivos que se comprimen en un archivo .zip de hello:</span><span class="sxs-lookup"><span data-stu-id="02c7a-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="02c7a-213">**applianceMainTemplate.json**: archivo de plantilla de implementación de Hola que ha usado toodeploy Hola/aplicación de la solución.</span><span class="sxs-lookup"><span data-stu-id="02c7a-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="02c7a-214">Para obtener información acerca de cómo ver archivos de plantilla de implementación de toocreate, [crear la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="02c7a-215">**appliancecreateUIDefinition.json**: interfaz de usuario de Hola de toogenerate portal Azure de Hola que ha usado tooprovision esta solución/aplicación usa este archivo.</span><span class="sxs-lookup"><span data-stu-id="02c7a-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="02c7a-216">Para más información, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="02c7a-217">**mainTemplate.json**: este archivo de plantilla contiene solo los recursos de Microsoft.Solution/appliances de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="02c7a-218">archivo de Hello mainTemplate incluye Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="02c7a-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="02c7a-219">**tipo**: Use **Marketplace** para las aplicaciones administradas en hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="02c7a-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="02c7a-220">**ManagedResourceGroupId**: este grupo de recursos de suscripción del cliente de hello es donde se implementan todos los recursos de hello definidos en applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="02c7a-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="02c7a-221">**PublisherPackageId**: esta cadena identifica de forma única los paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="02c7a-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="02c7a-222">Proporcionan un valor con formato Hola Hola `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="02c7a-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="02c7a-223">Obtener hello **identificador ofrecen** y **Id. de publicador** de hello publicación portal, como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="02c7a-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![Id. de oferta](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="02c7a-225">Obtener hello **identificador de SKU**, tal y como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="02c7a-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![Identificador de SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="02c7a-227">Obtener paquete hello **versión**, tal y como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="02c7a-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![Versión del paquete](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="02c7a-229">En función de hello anteriores ejemplos, Hola valor de **PublisherPackageId** es `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="02c7a-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="02c7a-230">Ejemplo de mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="02c7a-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="02c7a-231">Este paquete debe contener el resto de las plantillas anidada o scripts que son necesario toosuccessfully aprovisionar esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="02c7a-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="02c7a-232">Hello mainTemplate.json, applianceMainTemplate.json y applianceCreateUIDefinition.json archivos deben estar presentes en la carpeta raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="02c7a-233">**Autorizaciones**: esta propiedad define quién obtiene hello y acceso de nivel de acceso de recursos de toohello en las suscripciones de los clientes.</span><span class="sxs-lookup"><span data-stu-id="02c7a-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="02c7a-234">publicador de Hello utilizarla toomanage aplicación de hello en nombre de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="02c7a-235">**PrincipalId**: esta propiedad es el identificador de hello Azure Active Directory (Azure AD) de un usuario, el grupo de usuarios o la aplicación que ha concedido ciertos permisos en recursos de Hola de suscripción del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="02c7a-236">Hola definición de rol describe los permisos de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="02c7a-237">**Definición de roles**: esta propiedad es una lista de todos los Hola Control de acceso basado en roles (RBAC) roles integrados proporcionados por Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02c7a-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="02c7a-238">Puede seleccionar Hola rol de recursos de Hola de toomanage toouse más apropiados en nombre del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="02c7a-239">Puede agregar varias autorizaciones.</span><span class="sxs-lookup"><span data-stu-id="02c7a-239">You can add multiple authorizations.</span></span> <span data-ttu-id="02c7a-240">Se recomienda que cree un grupo de usuarios de AD y especifique su identificador en **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="02c7a-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="02c7a-241">De esta manera, puede agregar el grupo de usuarios de toohello a los usuarios más sin necesidad de Hola tooupdate Hola SKU.</span><span class="sxs-lookup"><span data-stu-id="02c7a-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="02c7a-242">Para obtener más información sobre la RBAC, consulte [comience a usar RBAC en hello portal de Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="02c7a-243">Formulario de Marketplace</span><span class="sxs-lookup"><span data-stu-id="02c7a-243">Marketplace form</span></span>

<span data-ttu-id="02c7a-244">Hola formulario Marketplace solicita campos que se muestran en hello [Azure Marketplace](https://azuremarketplace.microsoft.com) y en hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="02c7a-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="02c7a-245">Id. de suscripción de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="02c7a-245">Preview subscription IDs</span></span>

<span data-ttu-id="02c7a-246">Escriba una lista de identificadores que puede tener acceso a la oferta de hello después de haberlo publicado de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="02c7a-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="02c7a-247">Puede usar estos oferta de hello muestra una vista previa de lista blanca suscripciones tootest antes de efectuarlo live.</span><span class="sxs-lookup"><span data-stu-id="02c7a-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="02c7a-248">Puede compilar una lista blanca de configurar las suscripciones de too100 en el portal de partners de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="02c7a-249">Categorías sugeridas</span><span class="sxs-lookup"><span data-stu-id="02c7a-249">Suggested categories</span></span>

<span data-ttu-id="02c7a-250">Seleccione las categorías de toofive de lista de Hola que su oferta puede estar asociada mejor.</span><span class="sxs-lookup"><span data-stu-id="02c7a-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="02c7a-251">Estas categorías es toomap usado en las categorías de producto de oferta toohello que están disponibles en hello [Azure Marketplace](https://azuremarketplace.microsoft.com) hello y [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="02c7a-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="02c7a-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="02c7a-252">Azure Marketplace</span></span>

<span data-ttu-id="02c7a-253">Resumen de Hola de las aplicaciones administradas muestra hello siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="02c7a-253">hello summary of your managed application displays hello following fields:</span></span>

![Resumen de Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="02c7a-255">Hola **Introducción** ficha correspondiente a la aplicación administrada muestra hello siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="02c7a-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![Introducción a Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="02c7a-257">Hola **planes + precios** ficha correspondiente a la aplicación administrada muestra hello siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="02c7a-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Planes de Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="02c7a-259">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="02c7a-259">Azure portal</span></span>

<span data-ttu-id="02c7a-260">Resumen de Hola de las aplicaciones administradas muestra hello siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="02c7a-260">hello summary of your managed application displays hello following fields:</span></span>

![Resumen del portal](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="02c7a-262">información general de Hola para una aplicación administrada muestra hello siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="02c7a-262">hello overview for your managed application displays hello following fields:</span></span>

![Información general de Azure Portal](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="02c7a-264">Directrices para logotipos</span><span class="sxs-lookup"><span data-stu-id="02c7a-264">Logo guidelines</span></span>

<span data-ttu-id="02c7a-265">Siga estas directrices para ningún logotipo que se carga en el portal de partners de la nube de hello:</span><span class="sxs-lookup"><span data-stu-id="02c7a-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="02c7a-266">Hola diseño de Azure tiene una paleta de colores simple.</span><span class="sxs-lookup"><span data-stu-id="02c7a-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="02c7a-267">Limitar el número de Hola de principal y los colores de base de datos secundaria en el logotipo.</span><span class="sxs-lookup"><span data-stu-id="02c7a-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="02c7a-268">colores del tema Hola de portal de hello son blancos y negros.</span><span class="sxs-lookup"><span data-stu-id="02c7a-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="02c7a-269">No use estos colores como color de fondo de hello para el logotipo.</span><span class="sxs-lookup"><span data-stu-id="02c7a-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="02c7a-270">Usar un color que realiza su logotipo destacada en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="02c7a-271">Nosotros recomendamos usar colores primarios simples.</span><span class="sxs-lookup"><span data-stu-id="02c7a-271">We recommend simple primary colors.</span></span> <span data-ttu-id="02c7a-272">*Si usa un fondo transparente, asegúrese de que Hola logotipo y texto no están blancos, negro o azul.*</span><span class="sxs-lookup"><span data-stu-id="02c7a-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="02c7a-273">No use un fondo degradado en logotipo Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="02c7a-274">No coloque el texto en el logotipo de hello, ni siquiera su empresa o nombre de la marca.</span><span class="sxs-lookup"><span data-stu-id="02c7a-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="02c7a-275">Hola apariencia y funcionamiento de su logotipo debe ser sin formato y evite degradados.</span><span class="sxs-lookup"><span data-stu-id="02c7a-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="02c7a-276">Asegúrese de que no ajusta el logotipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="02c7a-277">Logotipo de imagen prominente</span><span class="sxs-lookup"><span data-stu-id="02c7a-277">Hero logo</span></span>

<span data-ttu-id="02c7a-278">logotipo de héroe de Hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="02c7a-278">hello hero logo is optional.</span></span> <span data-ttu-id="02c7a-279">publicador de Hello puede elegir no tooupload un logotipo héroe.</span><span class="sxs-lookup"><span data-stu-id="02c7a-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="02c7a-280">Después de carga el icono de héroe de hello, no se puede eliminar.</span><span class="sxs-lookup"><span data-stu-id="02c7a-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="02c7a-281">En ese momento, socio Hola debe seguir instrucciones de Marketplace de Hola para iconos héroe.</span><span class="sxs-lookup"><span data-stu-id="02c7a-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="02c7a-282">Siga estas directrices para el icono del logotipo de hello héroe:</span><span class="sxs-lookup"><span data-stu-id="02c7a-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="02c7a-283">nombre para mostrar Hello publicador, título de plan de Hola y oferta de hello resumida largas se muestran en blanco.</span><span class="sxs-lookup"><span data-stu-id="02c7a-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="02c7a-284">Por lo tanto, no use un color claro para el fondo de hello del icono de héroe de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="02c7a-285">Los fondos transparentes y de color negro o blanco no pueden utilizarse en los iconos de imagen prominente.</span><span class="sxs-lookup"><span data-stu-id="02c7a-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="02c7a-286">Después de que se muestra la oferta de hello, publicador Hola nombre para mostrar, título del plan de hello, resumidas largas de oferta de Hola y Hola **crear** botón incrustados mediante programación dentro de logotipo héroe de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="02c7a-287">Por lo tanto, no se especifica ningún texto mientras diseña el logotipo de héroe de Hola.</span><span class="sxs-lookup"><span data-stu-id="02c7a-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="02c7a-288">Dejar espacios en blanco en hello derecho porque texto hello se incluye mediante programación en ese espacio.</span><span class="sxs-lookup"><span data-stu-id="02c7a-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="02c7a-289">espacio vacío de Hola para texto hello debe ser 415 x 100 píxeles en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="02c7a-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="02c7a-290">Se ve compensado por 370 píxeles de hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="02c7a-290">It's offset by 370 pixels from hello left.</span></span>

    ![Ejemplo de logotipo de imagen prominente](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="02c7a-292">Formulario de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="02c7a-292">Support form</span></span>

<span data-ttu-id="02c7a-293">Rellene hello **admite** formulario con el soporte técnico se pone en contacto de su empresa.</span><span class="sxs-lookup"><span data-stu-id="02c7a-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="02c7a-294">Esta información podría contener contactos de ingeniería y contactos de soporte técnico al cliente.</span><span class="sxs-lookup"><span data-stu-id="02c7a-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="02c7a-295">Publicación de una oferta</span><span class="sxs-lookup"><span data-stu-id="02c7a-295">Publish an offer</span></span>

<span data-ttu-id="02c7a-296">Después de rellenar todas las secciones de hello, seleccione **publicar** proceso de hello toostart que hace que su toocustomers disponible de la oferta.</span><span class="sxs-lookup"><span data-stu-id="02c7a-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02c7a-297">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="02c7a-297">Next steps</span></span>

* <span data-ttu-id="02c7a-298">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="02c7a-299">Para obtener información acerca de cómo consumir una aplicación administrada de hello Marketplace, vea [Azure consumir las aplicaciones en hello Marketplace administradas](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="02c7a-300">Para información sobre cómo publicar una aplicación administrada del catálogo de servicios, consulte [Creación y publicación de una aplicación administrada del catálogo de servicios](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="02c7a-301">Para información sobre cómo usar una aplicación administrada del catálogo de servicios, consulte [Uso de una aplicación administrada del catálogo de servicios](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="02c7a-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
