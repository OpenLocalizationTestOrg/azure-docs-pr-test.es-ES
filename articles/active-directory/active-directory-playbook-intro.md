---
title: "Introducción de guía de prueba de concepto de Active Directory aaaAzure | Documentos de Microsoft"
description: "Exploración e implementación rápida de escenarios de administración de identidades y acceso"
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="6fa04-104">Guía de prueba de concepto de Azure Active Directory: Introducción</span><span class="sxs-lookup"><span data-stu-id="6fa04-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="6fa04-105">Este artículo proporciona instrucciones tooexplore Azure AD diferentes funciones en una prueba de concepto (PoC).</span><span class="sxs-lookup"><span data-stu-id="6fa04-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="6fa04-106">Hola pensado destinatarios de este documento son los arquitectos de identidad y profesionales de TI, integradores de sistema</span><span class="sxs-lookup"><span data-stu-id="6fa04-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="6fa04-107">¿Cómo toouse esta guía</span><span class="sxs-lookup"><span data-stu-id="6fa04-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="6fa04-108">Hola de uso [tema](active-directory-playbook-ingredients.md#theme) sección y elegir Hola áreas de interés según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="6fa04-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="6fa04-109">Definir el ámbito de hello PoC eligiendo los escenarios de Hola que estén alineadas con sus objetivos empresariales.</span><span class="sxs-lookup"><span data-stu-id="6fa04-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="6fa04-110">Hola más corto Hola mejor.</span><span class="sxs-lookup"><span data-stu-id="6fa04-110">hello shorter hello better.</span></span> <span data-ttu-id="6fa04-111">Se recomienda hacerlo como breve y conciso como valor de hello tooconvey posibles toohello las partes interesadas y reduce su Hola toorealize de complejidad.</span><span class="sxs-lookup"><span data-stu-id="6fa04-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="6fa04-112">Hola de uso [implementación](active-directory-playbook-implementation.md) escenarios de sección toounderstand hello y lo que significaría que para su entorno.</span><span class="sxs-lookup"><span data-stu-id="6fa04-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="6fa04-113">En cada escenario, se describe cómo tooset, configúrelo (lo que llamamos [bloques de creación](active-directory-playbook-building-blocks.md)), y cómo toonavigate Hola escenarios.</span><span class="sxs-lookup"><span data-stu-id="6fa04-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="6fa04-114">Cada bloque de creación explica Hola cumplen los requisitos previos necesarios, así como un toocomplete tiempo aproximado.</span><span class="sxs-lookup"><span data-stu-id="6fa04-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="6fa04-115">Esto puede ayudarle durante el proceso de planeamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6fa04-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="6fa04-116">En función de 1 al 3 anteriores, definir hello [entorno](active-directory-playbook-ingredients.md#environment) en qué tooexecute.</span><span class="sxs-lookup"><span data-stu-id="6fa04-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="6fa04-117">Le recomendamos toostrive para un tooget del entorno de producción una idea de la experiencia de Hola para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="6fa04-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="6fa04-118">Si algunos de los requisitos plantea conflictos, puede utilizar la siguiente matriz de decisión</span><span class="sxs-lookup"><span data-stu-id="6fa04-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="6fa04-119">Visualización del valor centrada en el tema</span><span class="sxs-lookup"><span data-stu-id="6fa04-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="6fa04-120">Escenarios de suavidad tooprepare, tooset seguridad y tooexecute Hola</span><span class="sxs-lookup"><span data-stu-id="6fa04-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="6fa04-121">Escenarios de destino de un tiempo mínimo tooexecute Hola</span><span class="sxs-lookup"><span data-stu-id="6fa04-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="6fa04-122">Como cerrar tooproduction como sea posible dentro de las restricciones</span><span class="sxs-lookup"><span data-stu-id="6fa04-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="6fa04-123">En este artículo, verá algunas aplicaciones específicas de terceros y productos que se mencionan como ejemplos para su comodidad.</span><span class="sxs-lookup"><span data-stu-id="6fa04-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="6fa04-124">Azure AD admite miles de aplicaciones en su [Galería de aplicaciones](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) que puede usar en función de sus necesidades y entorno.</span><span class="sxs-lookup"><span data-stu-id="6fa04-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]