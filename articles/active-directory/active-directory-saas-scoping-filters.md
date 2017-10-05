---
title: "Aprovisionamiento de aplicaciones con filtros de ámbito | Microsoft Docs"
description: "Obtenga información sobre cómo usar los filtros de ámbito para evitar el aprovisionamiento real de los objetos de las aplicaciones que admiten el aprovisionamiento automático de usuarios, en caso de que un objeto no satisfaga los requisitos empresariales."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="f383a-103">Aprovisionamiento de aplicaciones basado en atributos con filtros de ámbito</span><span class="sxs-lookup"><span data-stu-id="f383a-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="f383a-104">El objetivo de esta sección es explicar cómo usar filtros de ámbito para definir reglas basadas en atributos que determinarán qué usuarios se aprovisionarán en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f383a-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="f383a-105">Cláusulas y grupos de ámbitos</span><span class="sxs-lookup"><span data-stu-id="f383a-105">Clauses and Scope Groups</span></span>
![Filtro de ámbito][1] 

<span data-ttu-id="f383a-107">Los filtros de ámbito se definen mediante uno o varios **grupos de ámbitos**, y cada uno de ellos contiene una o varias **cláusulas**.</span><span class="sxs-lookup"><span data-stu-id="f383a-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="f383a-108">Para ver las cláusulas de un grupo de ámbitos concreto, haga clic en la flecha situada a la izquierda del nombre del grupo para expandirlo.</span><span class="sxs-lookup"><span data-stu-id="f383a-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="f383a-109">Una **cláusula** determina qué usuarios pueden pasar a través del filtro de ámbito mediante la evaluación de los atributos de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="f383a-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="f383a-110">Por ejemplo, podría tener una cláusula que requiere que el atributo "state" del usuario sea igual a Nueva York, de modo que solo se aprovisionará a los usuarios de Nueva York en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f383a-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![Nombre del grupo de ámbito][2] 

<span data-ttu-id="f383a-112">Cada **grupo de ámbitos** comienza con una **cláusula** obligatoria, como se muestra en la captura de pantalla anterior.</span><span class="sxs-lookup"><span data-stu-id="f383a-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="f383a-113">Esta cláusula sólo indica que primero es necesario asignar al usuario a la aplicación antes de que los filtros de ámbito lo evalúen.</span><span class="sxs-lookup"><span data-stu-id="f383a-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="f383a-114">Esta cláusula no puede eliminarse ni modificarse.</span><span class="sxs-lookup"><span data-stu-id="f383a-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="f383a-115">Puede agregar cláusulas nuevas o grupos de ámbitos nuevos; para ello, haga clic en el botón correspondiente.</span><span class="sxs-lookup"><span data-stu-id="f383a-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="f383a-116">Puede asignar un nombre a cada grupo de ámbitos; para ello, edite la propiedad **Nombre del grupo de ámbitos** .</span><span class="sxs-lookup"><span data-stu-id="f383a-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="f383a-117">Evaluación de los filtros de ámbito</span><span class="sxs-lookup"><span data-stu-id="f383a-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="f383a-118">Durante el aprovisionamiento, probamos a cada usuario asignado con los filtros de ámbito para determinar si es posible dar acceso a un usuario a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f383a-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="f383a-119">Puede considerar cada cláusula como una prueba que se debe superar para evitar que el filtro rechace a un usuario.</span><span class="sxs-lookup"><span data-stu-id="f383a-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="f383a-120">Si ha definido varios grupos de ámbitos, cada usuario debe pasar al menos uno de ellos para poder tener acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f383a-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="f383a-121">Dentro de cada grupo de ámbitos, sin embargo, el usuario debe pasar cada cláusula para pasar ese grupo de ámbitos específico.</span><span class="sxs-lookup"><span data-stu-id="f383a-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="f383a-122">En otras palabras, puede considerar los grupos de ámbitos como agrupaciones mediante el operador OR, y puede considerar las cláusulas contenidas en ellos como agrupaciones mediante el operador AND.</span><span class="sxs-lookup"><span data-stu-id="f383a-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="f383a-123">Por ejemplo, considere el siguiente filtro de ámbito:</span><span class="sxs-lookup"><span data-stu-id="f383a-123">For example, consider the scoping filter below:</span></span>

![Nombre del grupo de ámbito][3]  

<span data-ttu-id="f383a-125">Según este filtro de ámbito, los usuarios deben cumplir los siguientes criterios, a fin de que se les pueda aprovisionar:</span><span class="sxs-lookup"><span data-stu-id="f383a-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="f383a-126">Se les debe haber asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f383a-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="f383a-127">Deben trabajar en el departamento de ingeniería.</span><span class="sxs-lookup"><span data-stu-id="f383a-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="f383a-128">Deben trabajar en San Francisco o Canadá.</span><span class="sxs-lookup"><span data-stu-id="f383a-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="f383a-129">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="f383a-129">Related Articles</span></span>
* [<span data-ttu-id="f383a-130">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f383a-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="f383a-131">Aprovisionamiento y desaprovisionamiento automático de usuarios para aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="f383a-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="f383a-132">Personalización de asignaciones de atributos para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="f383a-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="f383a-133">Escritura de expresiones para asignaciones de atributos</span><span class="sxs-lookup"><span data-stu-id="f383a-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="f383a-134">Notificaciones de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="f383a-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="f383a-135">Uso de SCIM para habilitar el aprovisionamiento automático de usuarios y grupos de Azure Active Directory a aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f383a-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="f383a-136">Lista de tutoriales sobre cómo integrar aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="f383a-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
