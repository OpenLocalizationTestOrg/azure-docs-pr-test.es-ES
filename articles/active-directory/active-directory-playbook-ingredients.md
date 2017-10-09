---
title: "aaaAzure ingredientes de guía de prueba de concepto de Active Directory | Documentos de Microsoft"
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
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="f33cb-104">Componentes de la guía de prueba de concepto de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f33cb-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="f33cb-105">Tema</span><span class="sxs-lookup"><span data-stu-id="f33cb-105">Theme</span></span>
<span data-ttu-id="f33cb-106">Azure AD proporciona soluciones de identidad y acceso a través de varias áreas de empresa de Hola.</span><span class="sxs-lookup"><span data-stu-id="f33cb-106">Azure AD provides identity and access solutions across multiple areas in hello enterprise.</span></span> <span data-ttu-id="f33cb-107">Se clasificación escenarios Hola Hola siguientes áreas:</span><span class="sxs-lookup"><span data-stu-id="f33cb-107">We classify hello scenarios in hello following areas:</span></span> 

* [<span data-ttu-id="f33cb-108">Gran cantidad de aplicaciones, una identidad</span><span class="sxs-lookup"><span data-stu-id="f33cb-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="f33cb-109">Mejorar la seguridad</span><span class="sxs-lookup"><span data-stu-id="f33cb-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="f33cb-110">Escalable con autoservicio</span><span class="sxs-lookup"><span data-stu-id="f33cb-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="f33cb-111">Definir un tema tooframe ¡hello PoC ayuda a los esfuerzos de hello toofocus clara con los objetivos empresariales, que a menudo son desencadenadores de Hola de interés de hello en una prueba de concepto en primer lugar en Hola.</span><span class="sxs-lookup"><span data-stu-id="f33cb-111">Defining a theme tooframe hello PoC helps toofocus hello efforts that resonates with business goals, which oftentimes are hello triggers of hello interest in a proof of concept in hello first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="f33cb-112">Environment</span><span class="sxs-lookup"><span data-stu-id="f33cb-112">Environment</span></span>

<span data-ttu-id="f33cb-113">Es detalles de Hola toodetermine importante del entorno de Hola donde entregará Hola prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="f33cb-113">It is important toodetermine hello details of hello environment where you will deliver hello PoC.</span></span> <span data-ttu-id="f33cb-114">Lo ideal es que puede crear en él después de Hola que se ha completado la prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="f33cb-114">Ideally you can build upon it after hello PoC is completed.</span></span> <span data-ttu-id="f33cb-115">entorno de destino de Hello es crucial y debería encontrar el equilibrio adecuado de hello entre realizar, como real posible y la sobrecarga de Hola de restricciones o consideraciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="f33cb-115">hello target environment is crucial and you should find hello right balance between making it as real as possible and hello overhead of constraints or extra considerations.</span></span> <span data-ttu-id="f33cb-116">Hola entornos típicos para PoCs son:</span><span class="sxs-lookup"><span data-stu-id="f33cb-116">hello typical environments for PoCs are:</span></span>
* <span data-ttu-id="f33cb-117">**Producción:** escenarios Hola se implementará en el entorno activo y ya implementado Microsoft Cloud services (solución de producción AD, Office 365, Azure AD inquilino/SSO).</span><span class="sxs-lookup"><span data-stu-id="f33cb-117">**Production:** hello scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="f33cb-118">**Pruebas de aceptación de usuario (UAT) o entorno de desarrollo:** Se dispone de una infraestructura de prueba (AD en paralelo y potencialmente un inquilino Azure AD, o una solución SSO) con datos de prueba similares a los de producción.</span><span class="sxs-lookup"><span data-stu-id="f33cb-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="f33cb-119">Por lo general, entorno de prueba de Hola se comparte entre varios proyectos de empresa de Hola.</span><span class="sxs-lookup"><span data-stu-id="f33cb-119">Typically, hello test environment is shared across multiple projects in hello enterprise.</span></span>

<span data-ttu-id="f33cb-120">La mayoría de los escenarios en esta guía son aditivos por naturaleza.</span><span class="sxs-lookup"><span data-stu-id="f33cb-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="f33cb-121">Como resultado, puede implementarse en el inquilino de producción de hello sin que afecte a los usuarios ajenos a Hola prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="f33cb-121">As a result, they can be deployed in hello production tenant without affecting users outside hello PoC.</span></span> <span data-ttu-id="f33cb-122">En este documento, se advertirá sobre los escenarios que pudieran tener efecto en todo el inquilino.</span><span class="sxs-lookup"><span data-stu-id="f33cb-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="f33cb-123">En esos casos, conviene tooconsider un entorno no productivo.</span><span class="sxs-lookup"><span data-stu-id="f33cb-123">In those cases, you might want tooconsider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="f33cb-124">Usuarios de destino</span><span class="sxs-lookup"><span data-stu-id="f33cb-124">Target Users</span></span>

<span data-ttu-id="f33cb-125">Es importante toodetermine Hola destino conjunto de usuarios que actúan sobre escenarios de hello, especialmente cuando el entorno de hello es de producción o de prueba.</span><span class="sxs-lookup"><span data-stu-id="f33cb-125">It is important toodetermine hello target set of users that will exercise hello scenarios, especially when hello environment is production or test.</span></span> <span data-ttu-id="f33cb-126">Hola categorías de usuarios de destino para la prueba de concepto son:</span><span class="sxs-lookup"><span data-stu-id="f33cb-126">hello categories of target users for PoC are:</span></span>
* <span data-ttu-id="f33cb-127">**Los usuarios del piloto:** funciones de trabajo de usuarios reales en el entorno de Hola que va a utilizar soluciones de hello con cuenta de hello que usan para su tooday día</span><span class="sxs-lookup"><span data-stu-id="f33cb-127">**Pilot Users:** Real users in hello environment that will be using hello solution with hello account they use for their day tooday job functions</span></span>
* <span data-ttu-id="f33cb-128">**Los usuarios de prueba:** probar las cuentas creadas en el entorno de Hola</span><span class="sxs-lookup"><span data-stu-id="f33cb-128">**Test Users:** Test accounts created in hello environment</span></span> 

<span data-ttu-id="f33cb-129">La mayoría de los escenarios de esta guía pueden realizarse con usuarios piloto.</span><span class="sxs-lookup"><span data-stu-id="f33cb-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="f33cb-130">En este documento, se advertirá sobre consideraciones de los usuarios de destino si es necesario.</span><span class="sxs-lookup"><span data-stu-id="f33cb-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]