---
title: "Componentes de la guía de prueba de concepto de Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="99dca-104">Componentes de la guía de prueba de concepto de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99dca-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="99dca-105">Tema</span><span class="sxs-lookup"><span data-stu-id="99dca-105">Theme</span></span>
<span data-ttu-id="99dca-106">Azure AD proporciona soluciones de identidad y acceso en múltiples áreas de la empresa.</span><span class="sxs-lookup"><span data-stu-id="99dca-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="99dca-107">Los escenarios se clasifican en las áreas siguientes:</span><span class="sxs-lookup"><span data-stu-id="99dca-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="99dca-108">Gran cantidad de aplicaciones, una identidad</span><span class="sxs-lookup"><span data-stu-id="99dca-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="99dca-109">Mejorar la seguridad</span><span class="sxs-lookup"><span data-stu-id="99dca-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="99dca-110">Escalable con autoservicio</span><span class="sxs-lookup"><span data-stu-id="99dca-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="99dca-111">Definir un tema para enmarcar la prueba de concepto ayuda a alinear los esfuerzos con los objetivos empresariales que, a menudo, son los primeros desencadenadores de la participación en una prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="99dca-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="99dca-112">Environment</span><span class="sxs-lookup"><span data-stu-id="99dca-112">Environment</span></span>

<span data-ttu-id="99dca-113">Es importante determinar los detalles del entorno donde se entregará la prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="99dca-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="99dca-114">Siempre es posible construir sobre ella una vez ha sido completada.</span><span class="sxs-lookup"><span data-stu-id="99dca-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="99dca-115">El entorno de destino es fundamental y debe buscar el equilibrio adecuado entre ser tan real como sea posible y la sobrecarga de las restricciones o consideraciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="99dca-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="99dca-116">Los entornos típicos de las pruebas de concepto son:</span><span class="sxs-lookup"><span data-stu-id="99dca-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="99dca-117">**Producción:** los escenarios se implementarán en un entorno activo y ya implementado de Microsoft Cloud Services (AD en producción, Office 365, inquilino Azure AD/solución SSO).</span><span class="sxs-lookup"><span data-stu-id="99dca-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="99dca-118">**Pruebas de aceptación de usuario (UAT) o entorno de desarrollo:** Se dispone de una infraestructura de prueba (AD en paralelo y potencialmente un inquilino Azure AD, o una solución SSO) con datos de prueba similares a los de producción.</span><span class="sxs-lookup"><span data-stu-id="99dca-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="99dca-119">Normalmente, el entorno de prueba se comparte entre varios proyectos de la empresa.</span><span class="sxs-lookup"><span data-stu-id="99dca-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="99dca-120">La mayoría de los escenarios en esta guía son aditivos por naturaleza.</span><span class="sxs-lookup"><span data-stu-id="99dca-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="99dca-121">Por ello, se pueden implementar en el inquilino de producción sin que afecte a los usuarios ajenos a la prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="99dca-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="99dca-122">En este documento, se advertirá sobre los escenarios que pudieran tener efecto en todo el inquilino.</span><span class="sxs-lookup"><span data-stu-id="99dca-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="99dca-123">En esos casos, podría valorarse un entorno que no sea de producción.</span><span class="sxs-lookup"><span data-stu-id="99dca-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="99dca-124">Usuarios de destino</span><span class="sxs-lookup"><span data-stu-id="99dca-124">Target Users</span></span>

<span data-ttu-id="99dca-125">Es importante determinar el conjunto de destino de los usuarios que actúan sobre los escenarios, especialmente cuando el entorno es de producción o de prueba.</span><span class="sxs-lookup"><span data-stu-id="99dca-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="99dca-126">Las categorías de usuarios de destino para la prueba de concepto son:</span><span class="sxs-lookup"><span data-stu-id="99dca-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="99dca-127">**Usuarios piloto:** usuarios reales del entorno que van a utilizar la solución con la misma cuenta que utilizan diariamente para sus funciones de trabajo</span><span class="sxs-lookup"><span data-stu-id="99dca-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="99dca-128">**Usuarios de prueba:** cuentas de prueba creadas en el entorno</span><span class="sxs-lookup"><span data-stu-id="99dca-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="99dca-129">La mayoría de los escenarios de esta guía pueden realizarse con usuarios piloto.</span><span class="sxs-lookup"><span data-stu-id="99dca-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="99dca-130">En este documento, se advertirá sobre consideraciones de los usuarios de destino si es necesario.</span><span class="sxs-lookup"><span data-stu-id="99dca-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]