---
title: "Consideraciones sobre el diseño de identidad híbrida de Azure Active Directory: determinación de los requisitos de autenticación multifactor| Microsoft Azure"
description: "Con el control de acceso condicional, Azure Active Directory comprueba las condiciones específicas que se eligen al autenticar al usuario y antes de permitirle acceso a la aplicación. Si se cumplen las condiciones, el usuario queda autenticado y se le permite el acceso a la aplicación."
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
ms.openlocfilehash: 5b3a8ce6e4203dfb3700f324e32687dd910118af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="b06b4-104">Determinación de los requisitos de autenticación multifactor para la solución de identidad híbrida</span><span class="sxs-lookup"><span data-stu-id="b06b4-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="b06b4-105">En este mundo de la movilidad en el que los usuarios acceden a datos y aplicaciones en la nube desde cualquier dispositivo, la seguridad de la información se ha convertido en algo primordial.</span><span class="sxs-lookup"><span data-stu-id="b06b4-105">In this world of mobility, with users accessing data and applications in the cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="b06b4-106">Todos los días hay un nuevo titular sobre una infracción de la seguridad.</span><span class="sxs-lookup"><span data-stu-id="b06b4-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="b06b4-107">Aunque no existe ninguna garantía contra tales infracciones, la autenticación multifactor ofrece una capa de seguridad adicional para ayudar a evitarlas.</span><span class="sxs-lookup"><span data-stu-id="b06b4-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security to help prevent these breaches.</span></span>
<span data-ttu-id="b06b4-108">Para comenzar, evalúe los requisitos de las organizaciones de autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="b06b4-108">Start by evaluating the organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="b06b4-109">Es decir, que intenta proteger la organización.</span><span class="sxs-lookup"><span data-stu-id="b06b4-109">That is, what is the organization trying to secure.</span></span>  <span data-ttu-id="b06b4-110">Esta evaluación es importante para definir los requisitos técnicos para configurar y habilitar a los usuarios de las organizaciones para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="b06b4-110">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="b06b4-111">Si no está familiarizado con MFA y cómo funciona, se recomienda encarecidamente que lea el artículo [¿Qué es Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) antes de continuar leyendo esta sección.</span><span class="sxs-lookup"><span data-stu-id="b06b4-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read the article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior to continue reading this section.</span></span>
> 
> 

<span data-ttu-id="b06b4-112">Asegúrese de responder a las siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="b06b4-112">Make sure to answer the following:</span></span>

* <span data-ttu-id="b06b4-113">¿Intenta su empresa proteger aplicaciones de Microsoft?</span><span class="sxs-lookup"><span data-stu-id="b06b4-113">Is your company trying to secure Microsoft apps?</span></span> 
* <span data-ttu-id="b06b4-114">¿Cómo se publican estas aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="b06b4-114">How these apps are published?</span></span>
* <span data-ttu-id="b06b4-115">¿Proporciona su empresa acceso remoto para permitir a los empleados el acceso a aplicaciones locales?</span><span class="sxs-lookup"><span data-stu-id="b06b4-115">Does your company provide remote access to allow employees to access on-premises apps?</span></span>

<span data-ttu-id="b06b4-116">En caso afirmativo, ¿qué tipo de acceso remoto? También debe evaluar dónde se ubicarán los usuarios que están teniendo acceso a estas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b06b4-116">If yes, what type of remote access?You also need to evaluate where the users who are accessing these applications will be located.</span></span> <span data-ttu-id="b06b4-117">Esta evaluación es otro paso importante para definir la estrategia adecuada de autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="b06b4-117">This evaluation is another important step to define the proper multi-factor authentication strategy.</span></span> <span data-ttu-id="b06b4-118">Asegúrese de responder a las siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="b06b4-118">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="b06b4-119">¿Dónde se van a encontrar los usuarios?</span><span class="sxs-lookup"><span data-stu-id="b06b4-119">Where are the users going to be located?</span></span>
* <span data-ttu-id="b06b4-120">¿Pueden estar en cualquier parte?</span><span class="sxs-lookup"><span data-stu-id="b06b4-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="b06b4-121">¿Desea su empresa establecer restricciones de acuerdo con la ubicación del usuario?</span><span class="sxs-lookup"><span data-stu-id="b06b4-121">Does your company want to establish restrictions according to the user’s location?</span></span>

<span data-ttu-id="b06b4-122">Una vez que comprenda estos requisitos, es importante evaluar también los requisitos del usuario de autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="b06b4-122">Once you understand these requirements, it is important to also evaluate the user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="b06b4-123">Esta evaluación es importante porque definirá los requisitos para implementar la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="b06b4-123">This evaluation is important because it will define the requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="b06b4-124">Asegúrese de responder a las siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="b06b4-124">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="b06b4-125">¿Están los usuarios familiarizados con la autenticación multifactor?</span><span class="sxs-lookup"><span data-stu-id="b06b4-125">Are the users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="b06b4-126">¿Algunos usuarios deben proporcionar autenticación adicional?</span><span class="sxs-lookup"><span data-stu-id="b06b4-126">Will some uses be required to provide additional authentication?</span></span>  
  * <span data-ttu-id="b06b4-127">En caso afirmativo, ¿siempre, cuando proceden de redes externas o cuando acceden a aplicaciones específicas, o en otras condiciones?</span><span class="sxs-lookup"><span data-stu-id="b06b4-127">If yes, all the time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="b06b4-128">¿Necesitarán los usuarios entrenamiento sobre cómo configurar e implementar la autenticación multifactor?</span><span class="sxs-lookup"><span data-stu-id="b06b4-128">Will the users require training on how to setup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="b06b4-129">¿Cuáles son los principales escenarios en los que su empresa quiere habilitar la autenticación multifactor para sus usuarios?</span><span class="sxs-lookup"><span data-stu-id="b06b4-129">What are the key scenarios that your company wants to enable multi-factor authentication for their users?</span></span>

<span data-ttu-id="b06b4-130">Después de responder a las preguntas anteriores, podrá comprender si la autenticación multifactor ya está implementada de forma local.</span><span class="sxs-lookup"><span data-stu-id="b06b4-130">After answering the previous questions, you will be able to understand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="b06b4-131">Esta evaluación es importante para definir los requisitos técnicos para configurar y habilitar a los usuarios de las organizaciones para la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="b06b4-131">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span> <span data-ttu-id="b06b4-132">Asegúrese de responder a las siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="b06b4-132">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="b06b4-133">¿Necesita su empresa proteger las cuentas con privilegios con MFA?</span><span class="sxs-lookup"><span data-stu-id="b06b4-133">Does your company need to protect privileged accounts with MFA?</span></span>
* <span data-ttu-id="b06b4-134">¿Necesita su empresa habilitar MFA en ciertas aplicaciones por motivos de cumplimiento?</span><span class="sxs-lookup"><span data-stu-id="b06b4-134">Does your company need to enable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="b06b4-135">¿Necesita habilitar su empresa MFA para todos los usuarios elegidos de estas aplicaciones o solo para los administradores?</span><span class="sxs-lookup"><span data-stu-id="b06b4-135">Does your company need to enable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="b06b4-136">¿Necesita tiene MFA siempre habilitado o solo cuando los usuarios se registran fuera de la red corporativa?</span><span class="sxs-lookup"><span data-stu-id="b06b4-136">Do you need have MFA always enabled or only when the users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="b06b4-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b06b4-137">Next steps</span></span>
[<span data-ttu-id="b06b4-138">Definición de una estrategia de adopción de identidad híbrida</span><span class="sxs-lookup"><span data-stu-id="b06b4-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="b06b4-139">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b06b4-139">See also</span></span>
[<span data-ttu-id="b06b4-140">Información general sobre las consideraciones de diseño</span><span class="sxs-lookup"><span data-stu-id="b06b4-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

