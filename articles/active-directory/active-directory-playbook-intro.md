---
title: "Introducción a la guía de prueba de concepto de Azure Active Directory | Microsoft Docs"
description: "Explorar e implementar rápidamente escenarios de administración de identidades y acceso"
services: active-directory
keywords: "azure active directory, guía, prueba de concepto, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="cd0b7-104">Guía de prueba de concepto de Azure Active Directory: Introducción</span><span class="sxs-lookup"><span data-stu-id="cd0b7-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="cd0b7-105">En este artículo se proporcionan instrucciones para explorar las diferentes funcionalidades de Azure AD en una prueba de concepto (PoC).</span><span class="sxs-lookup"><span data-stu-id="cd0b7-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="cd0b7-106">Los destinatarios de este documento son arquitectos de identidad, profesionales de TI e integradores de sistemas</span><span class="sxs-lookup"><span data-stu-id="cd0b7-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="cd0b7-107">Cómo usar esta guía</span><span class="sxs-lookup"><span data-stu-id="cd0b7-107">How to use this Playbook</span></span>

1. <span data-ttu-id="cd0b7-108">Use la sección [Tema](active-directory-playbook-ingredients.md#theme) y elija las áreas de interés según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="cd0b7-109">Defina el ámbito de la prueba de concepto eligiendo los escenarios que se alineen con sus objetivos empresariales.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="cd0b7-110">Cuanto más breve, mejor.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-110">The shorter the better.</span></span> <span data-ttu-id="cd0b7-111">Se recomienda hacerlo tan breve y conciso como sea posible para transmitir el valor a las partes interesadas y, al mismo tiempo, minimizar su complejidad.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="cd0b7-112">Use la sección [Implementación](active-directory-playbook-implementation.md) para comprender los escenarios y lo significarían para su entorno.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="cd0b7-113">En cada escenario, se describe cómo configurar lo que llamamos [Bloques de creación](active-directory-playbook-building-blocks.md)) y cómo navegar por los escenarios.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="cd0b7-114">Cada bloque de creación explica los requisitos previos necesarios, así como un tiempo aproximado de realización.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="cd0b7-115">Esto puede ser de ayuda durante el proceso de planificación.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="cd0b7-116">En función de los puntos 1 al 3 anteriores, defina el [Entorno](active-directory-playbook-ingredients.md#environment) en el que se va a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="cd0b7-117">Le animamos a elegir en lo posible un entorno de producción para hacerse una idea de la experiencia para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="cd0b7-118">Si algunos de los requisitos plantea conflictos, puede utilizar la siguiente matriz de decisión</span><span class="sxs-lookup"><span data-stu-id="cd0b7-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="cd0b7-119">Visualización del valor centrada en el tema</span><span class="sxs-lookup"><span data-stu-id="cd0b7-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="cd0b7-120">Facilidad para preparar, configurar y ejecutar los escenarios</span><span class="sxs-lookup"><span data-stu-id="cd0b7-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="cd0b7-121">Tiempo mínimo para ejecutar los escenarios de destino</span><span class="sxs-lookup"><span data-stu-id="cd0b7-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="cd0b7-122">Tan próximo a un entorno de producción como sea posible dentro de las restricciones</span><span class="sxs-lookup"><span data-stu-id="cd0b7-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="cd0b7-123">En este artículo, verá algunas aplicaciones específicas de terceros y productos que se mencionan como ejemplos para su comodidad.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="cd0b7-124">Azure AD admite miles de aplicaciones en su [Galería de aplicaciones](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) que puede usar en función de sus necesidades y entorno.</span><span class="sxs-lookup"><span data-stu-id="cd0b7-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]