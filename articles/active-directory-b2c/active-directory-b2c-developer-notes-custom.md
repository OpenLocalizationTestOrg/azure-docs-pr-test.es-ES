---
title: 'Azure Active Directory B2C: notas del desarrollador acerca del uso de directivas personalizadas|Microsoft Docs'
description: "Notas para los desarrolladores sobre configuración y mantenimiento de Azure AD B2C con directivas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: a5f222e5b11e05286152a9f1cc55d2c3fc27a9dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="e4411-103">Notas de la versión preliminar de la directiva personalizada de Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="e4411-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="e4411-104">El conjunto de características de la directiva personalizada está disponible para su evaluación en versión preliminar pública para todos los clientes de Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="e4411-104">The custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="e4411-105">Este conjunto de características está destinado a desarrolladores de identidades avanzados que crean las soluciones de identidad más complejas.</span><span class="sxs-lookup"><span data-stu-id="e4411-105">This feature set is targeted at advanced identity developers building the most complex identity solutions.</span></span>  

<span data-ttu-id="e4411-106">En la actualidad, este conjunto de características requiere que los desarrolladores configuren el marco de experiencia de identidad directamente a través de la edición de archivos XML.</span><span class="sxs-lookup"><span data-stu-id="e4411-106">Today, this feature set requires developers to configure the Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="e4411-107">Este método de configuración es eficaz y complejo.</span><span class="sxs-lookup"><span data-stu-id="e4411-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="e4411-108">Los desarrolladores de identidades avanzados que usen el marco de experiencia de identidad deben planear invertir un tiempo en completar los tutoriales y leer los documentos de referencia.</span><span class="sxs-lookup"><span data-stu-id="e4411-108">Advanced identity developers using the Identity Experience Framework should plan to invest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="e4411-109">Características que se incluyen en la versión preliminar pública</span><span class="sxs-lookup"><span data-stu-id="e4411-109">Features included in this public preview</span></span>
<span data-ttu-id="e4411-110">Con las nuevas características introducidas en la versión preliminar pública los desarrolladores pueden realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e4411-110">With the new features introduced in the public preview, developers can perform the following tasks:</span></span><br>

* <span data-ttu-id="e4411-111">Crear y cargar recorridos del usuario de autenticación personalizada mediante directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="e4411-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="e4411-112">Describir los recorridos del usuario paso a paso como intercambios entre proveedores de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="e4411-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="e4411-113">Definir la creación de ramas condicional en recorridos del usuario.</span><span class="sxs-lookup"><span data-stu-id="e4411-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="e4411-114">Integrar servicios con la API de REST habilitada en los recorridos del usuario de autenticación personalizada.</span><span class="sxs-lookup"><span data-stu-id="e4411-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="e4411-115">Agregar federación con proveedores de identidades compatibles con el estándar de OpenIDConnect.</span><span class="sxs-lookup"><span data-stu-id="e4411-115">Add federation with identity providers that are compliant with the OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="e4411-116">Agregar federación con proveedores de identidades que cumplen el protocolo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="e4411-116">Add federation with identity providers that adhere to the SAML 2.0 protocol.</span></span> 

## <a name="terms-of-the-public-preview"></a><span data-ttu-id="e4411-117">Términos de la versión preliminar pública</span><span class="sxs-lookup"><span data-stu-id="e4411-117">Terms of the public preview</span></span>

* <span data-ttu-id="e4411-118">Se aconseja usar las nuevas características solo con fines de evaluación.</span><span class="sxs-lookup"><span data-stu-id="e4411-118">We encourage you to use the new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="e4411-119">Las nuevas características no están pensadas para que se usen en entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="e4411-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="e4411-120">Los Acuerdos de Nivel de Servicio (SLA) no se aplican a las nuevas características.</span><span class="sxs-lookup"><span data-stu-id="e4411-120">Service level agreements (SLAs) do not apply to the new features.</span></span> <br>
* <span data-ttu-id="e4411-121">Las solicitudes de soporte técnico pueden enviarse a través de los canales de soporte técnico habituales.</span><span class="sxs-lookup"><span data-stu-id="e4411-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="e4411-122">No se puede garantizar ninguna fecha de disponibilidad general.</span><span class="sxs-lookup"><span data-stu-id="e4411-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="e4411-123">Microsoft se reserva el derecho, a su entera discreción y por cualquier motivo, de marcar y rechazar o restringir aquellos escenarios y recorridos del usuario que superen el ámbito de la carta de producto de Azure AD B2C para actuar como plataforma de administración de acceso e identidad de clientes (CIAM).</span><span class="sxs-lookup"><span data-stu-id="e4411-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed the scope of the Azure AD B2C product charter to serve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="e4411-124">Responsabilidades de los desarrolladores de conjunto de características de directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="e4411-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="e4411-125">La configuración manual de directivas concede un acceso de nivel inferior a la plataforma subyacente de Azure AD B2C y da como resultado la creación de un marco de confianza único y totalmente personalizable.</span><span class="sxs-lookup"><span data-stu-id="e4411-125">Manual policy configuration grants lower-level access to the underlying platform of Azure AD B2C and results in the creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="e4411-126">Las posibles permutaciones de proveedores de identidades personalizados, las relaciones de confianza, las integraciones con servicios externos y los flujos de trabajo paso a paso exigen más a los desarrolladores avanzados que los utilizan.</span><span class="sxs-lookup"><span data-stu-id="e4411-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on the advanced developers consuming them.</span></span>

<span data-ttu-id="e4411-127">Para aprovechar de forma completa la versión preliminar pública, se recomienda que los desarrolladores que utilizan el conjunto de características de directivas personalizadas cumplan las directrices siguientes:</span><span class="sxs-lookup"><span data-stu-id="e4411-127">To fully benefit from the public preview, we suggest that developers consuming the custom policy feature set adhere to the following guidelines:</span></span>
* <span data-ttu-id="e4411-128">Conocer el lenguaje de configuración de Identity Experience Engine y la administración de claves/secretos.</span><span class="sxs-lookup"><span data-stu-id="e4411-128">Become familiar with the configuration language of the Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="e4411-129">Tomar posesión de escenarios e integraciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="e4411-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="e4411-130">Realizar pruebas metódicas de los escenarios.</span><span class="sxs-lookup"><span data-stu-id="e4411-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="e4411-131">Seguir los procedimientos recomendados de desarrollo de software y almacenamiento provisional con un mínimo de un entorno de desarrollo y prueba, y un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e4411-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="e4411-132">Mantenerse informado sobre los nuevos desarrollos de los proveedores de identidad y los servicios con los que está integrado.</span><span class="sxs-lookup"><span data-stu-id="e4411-132">Stay informed about new developments from the identity providers and services you integrate with.</span></span> <span data-ttu-id="e4411-133">Por ejemplo, realizar un seguimiento de cambios en los secretos y los cambios programados y no programados en el servicio.</span><span class="sxs-lookup"><span data-stu-id="e4411-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes to the service.</span></span>
* <span data-ttu-id="e4411-134">Configurar la supervisión activa y supervisar la capacidad de respuesta de los entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="e4411-134">Set up active monitoring, and monitor the responsiveness of production environments.</span></span>
* <span data-ttu-id="e4411-135">Mantener actualizadas las direcciones de correo electrónico de contacto y responder a los correos mensajes de correo electrónico del equipo del sitio activo de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e4411-135">Keep contact email addresses current, and stay responsive to the Microsoft live-site team emails.</span></span>
* <span data-ttu-id="e4411-136">Realizar las acciones pertinentes cuando se lo indique el equipo del sitio activo de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e4411-136">Take timely action when advised to do so by the Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="e4411-137">Estas características pueden llegar a incluirse en las directivas integradas de Azure AD, lo que hace que todos los desarrolladores puedan acceder más fácilmente a ellas.</span><span class="sxs-lookup"><span data-stu-id="e4411-137">These features might eventually be included in Azure AD built-in policies, making them more accessible to all developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4411-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4411-138">Next steps</span></span>
<span data-ttu-id="e4411-139">[Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e4411-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
