---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar los requisitos de la autenticación multifactor"
description: "Con control de acceso condicional, Azure Active Directory comprueba las condiciones específicas de Hola que elegir al autenticar usuario hello y antes de permitir el acceso toohello aplicación. Una vez que se cumplen estas condiciones, usuario de hello es autenticado y acceso toohello aplicación permitida."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="e1198-104">Determinación de los requisitos de autenticación multifactor para la solución de identidad híbrida</span><span class="sxs-lookup"><span data-stu-id="e1198-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="e1198-105">En este mundo de la movilidad, con usuarios que acceden a datos y aplicaciones en la nube de Hola y desde cualquier dispositivo, proteger esta información se ha convertido en gran importancia.</span><span class="sxs-lookup"><span data-stu-id="e1198-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="e1198-106">Todos los días hay un nuevo titular sobre una infracción de la seguridad.</span><span class="sxs-lookup"><span data-stu-id="e1198-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="e1198-107">Sin embargo, no hay ninguna garantía en brechas de seguridad, la autenticación multifactor, proporciona una capa adicional de seguridad toohelp evitar estas infracciones.</span><span class="sxs-lookup"><span data-stu-id="e1198-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="e1198-108">Iniciar mediante la evaluación de los requisitos de las organizaciones de hello para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="e1198-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="e1198-109">Es decir, ¿qué es Hola organización tratar toosecure.</span><span class="sxs-lookup"><span data-stu-id="e1198-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="e1198-110">Esta evaluación es requisitos técnicos de hello toodefine importante para configurar y permitir que los usuarios de organizaciones de hello para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="e1198-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="e1198-111">Si no está familiarizado con MFA y lo que hace, se recomienda encarecidamente que lea el artículo hello [¿qué es la autenticación multifactor Azure?](../multi-factor-authentication/multi-factor-authentication.md) toocontinue anterior leer esta sección.</span><span class="sxs-lookup"><span data-stu-id="e1198-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="e1198-112">Realice el siguiente de hello tooanswer seguro:</span><span class="sxs-lookup"><span data-stu-id="e1198-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="e1198-113">¿Su empresa está tratando de aplicaciones de Microsoft toosecure?</span><span class="sxs-lookup"><span data-stu-id="e1198-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="e1198-114">¿Cómo se publican estas aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="e1198-114">How these apps are published?</span></span>
* <span data-ttu-id="e1198-115">¿La compañía proporcionará acceso remoto tooallow empleados tooaccess local aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="e1198-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="e1198-116">¿En caso afirmativo, qué tipo de acceso remoto? También debe tooevaluate donde se ubicarán los usuarios de Hola que obtiene acceso a estas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e1198-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="e1198-117">Esta evaluación es otra estrategia de autenticación multifactor correcta de Hola de toodefine paso importante.</span><span class="sxs-lookup"><span data-stu-id="e1198-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="e1198-118">Asegúrese de seguro hello tooanswer siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="e1198-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e1198-119">¿Dónde se encuentran los usuarios de hello va toobe?</span><span class="sxs-lookup"><span data-stu-id="e1198-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="e1198-120">¿Pueden estar en cualquier parte?</span><span class="sxs-lookup"><span data-stu-id="e1198-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="e1198-121">¿Su compañía quiere restricciones tooestablish según la ubicación del usuario toohello?</span><span class="sxs-lookup"><span data-stu-id="e1198-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="e1198-122">Una vez que comprenda estos requisitos, es importante tooalso evaluar los requisitos del usuario de hello para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="e1198-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="e1198-123">Esta evaluación es importante porque definirá los requisitos de Hola para implementar la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="e1198-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="e1198-124">Asegúrese de seguro hello tooanswer siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="e1198-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e1198-125">¿Está familiarizado con la autenticación multifactor a los usuarios de hello?</span><span class="sxs-lookup"><span data-stu-id="e1198-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="e1198-126">¿Algunos usos puede tooprovide requiere la autenticación adicional?</span><span class="sxs-lookup"><span data-stu-id="e1198-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="e1198-127">¿En caso afirmativo, todos Hola tiempo, al proceder de redes externas o acceso a aplicaciones específicas, o en otras condiciones?</span><span class="sxs-lookup"><span data-stu-id="e1198-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="e1198-128">Hola ¿necesitarán los usuarios entrenamiento acerca de cómo toosetup e implementar la autenticación multifactor?</span><span class="sxs-lookup"><span data-stu-id="e1198-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="e1198-129">¿Cuáles son los escenarios clave de Hola que su compañía desea tooenable la autenticación multifactor para sus usuarios?</span><span class="sxs-lookup"><span data-stu-id="e1198-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="e1198-130">Después de responder a preguntas anteriores de hello, podrán capaz de toounderstand si no hay ya ha implementado la autenticación multifactor local.</span><span class="sxs-lookup"><span data-stu-id="e1198-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="e1198-131">Esta evaluación es requisitos técnicos de hello toodefine importante para configurar y permitir que los usuarios de organizaciones de hello para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="e1198-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="e1198-132">Asegúrese de seguro hello tooanswer siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="e1198-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e1198-133">¿La compañía necesita cuentas con privilegios de tooprotect con MFA?</span><span class="sxs-lookup"><span data-stu-id="e1198-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="e1198-134">¿La compañía necesita tooenable MFA para ciertas aplicaciones por motivos de cumplimiento?</span><span class="sxs-lookup"><span data-stu-id="e1198-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="e1198-135">¿La compañía necesita tooenable MFA para todos los usuarios válidos de estas aplicaciones o solo los administradores?</span><span class="sxs-lookup"><span data-stu-id="e1198-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="e1198-136">¿Necesita tener MFA siempre habilitado o solo cuando inician sesión los usuarios de hello fuera de la red corporativa?</span><span class="sxs-lookup"><span data-stu-id="e1198-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1198-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1198-137">Next steps</span></span>
[<span data-ttu-id="e1198-138">Definición de una estrategia de adopción de identidad híbrida</span><span class="sxs-lookup"><span data-stu-id="e1198-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="e1198-139">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e1198-139">See also</span></span>
[<span data-ttu-id="e1198-140">Información general sobre las consideraciones de diseño</span><span class="sxs-lookup"><span data-stu-id="e1198-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

