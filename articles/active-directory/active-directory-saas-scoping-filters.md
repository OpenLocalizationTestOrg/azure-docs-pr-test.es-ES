---
title: "aplicaciones de aaaProvisioning con filtros de ámbito | Documentos de Microsoft"
description: "Obtenga información acerca de cómo definir el ámbito toouse filtra los objetos de tooprevent en aplicaciones que admitan el aprovisionamiento automático de usuarios desde que se aprovisiona realmente si un objeto no satisface sus requisitos empresariales."
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
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="69f2e-103">Aprovisionamiento de aplicaciones basado en atributos con filtros de ámbito</span><span class="sxs-lookup"><span data-stu-id="69f2e-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="69f2e-104">objetivo de Hola de esta sección es tooexplain cómo toouse ámbito filtra toodefine basado en atributos reglas que determinan qué usuarios aprovisiona toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="69f2e-104">hello objective of this section is tooexplain how toouse scoping filters toodefine attribute-based rules that determine which users are provisioned toohello application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="69f2e-105">Cláusulas y grupos de ámbitos</span><span class="sxs-lookup"><span data-stu-id="69f2e-105">Clauses and Scope Groups</span></span>
![Filtro de ámbito][1] 

<span data-ttu-id="69f2e-107">Los filtros de ámbito se definen mediante uno o varios **grupos de ámbitos**, y cada uno de ellos contiene una o varias **cláusulas**.</span><span class="sxs-lookup"><span data-stu-id="69f2e-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="69f2e-108">cláusulas de hello toosee para un grupo de ámbito determinado, expándalo haciendo clic en hello flecha toohello a la izquierda del nombre de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f2e-108">toosee hello clauses for a particular scope group, expand it by clicking hello arrow toohello left of hello group name.</span></span>

<span data-ttu-id="69f2e-109">A **cláusula** determina qué usuarios tienen permiso toopass a través de hello filtro de ámbito mediante la evaluación de atributos de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="69f2e-109">A **clause** determines which users are allowed toopass through hello scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="69f2e-110">Por ejemplo, tendrá una cláusula que requiere que "state" atributo igual Nueva York un usuario, por lo que solo los usuarios de Nueva York se aprovisionan en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="69f2e-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into hello application.</span></span>

![Nombre del grupo de ámbito][2] 

<span data-ttu-id="69f2e-112">Cada **grupo del ámbito** comienza con una obligatorio **cláusula**, tal y como se muestra en la captura de pantalla de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="69f2e-112">Each **scope group** starts with one mandatory **clause**, as shown in hello screenshot above.</span></span> <span data-ttu-id="69f2e-113">Esta cláusula indica simplemente que el usuario Hola primero se debe asignar toohello aplicación antes de que se evalúa por los filtros de ámbito.</span><span class="sxs-lookup"><span data-stu-id="69f2e-113">This clause simply states that hello user must first be assigned toohello application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="69f2e-114">Esta cláusula no puede eliminarse ni modificarse.</span><span class="sxs-lookup"><span data-stu-id="69f2e-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="69f2e-115">Puede agregar nuevas cláusulas o nuevos grupos de ámbito presionando el botón correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f2e-115">You can add new clauses or new scope groups by pressing hello appropriate button.</span></span> <span data-ttu-id="69f2e-116">Puede asignar un nombre a cada grupo de ámbitos; para ello, edite la propiedad **Nombre del grupo de ámbitos** .</span><span class="sxs-lookup"><span data-stu-id="69f2e-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="69f2e-117">Evaluación de los filtros de ámbito</span><span class="sxs-lookup"><span data-stu-id="69f2e-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="69f2e-118">Durante el aprovisionamiento, probamos cada usuario asignado en su ámbito toodetermine filtros si ese usuario merece acceso toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="69f2e-118">During provisioning, we test every assigned user against your scoping filters toodetermine if that user deserves access toohello application.</span></span> <span data-ttu-id="69f2e-119">Se puede considerar cada cláusula como una prueba que se debe pasar en orden para hello usuario tooavoid obtener filtran.</span><span class="sxs-lookup"><span data-stu-id="69f2e-119">You can think of each clause as being a test that must be passed in order for hello user tooavoid getting filtered out.</span></span> 

<span data-ttu-id="69f2e-120">Si tiene varios grupos de ámbito definidos, cada usuario debe superar al menos uno de ellos tooaccess aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="69f2e-120">If you have multiple scope groups defined, each user must pass at least one of them tooaccess hello application.</span></span> <span data-ttu-id="69f2e-121">Dentro de cada grupo de ámbito, sin embargo, Hola usuario debe pasar cada cláusula toopass ese grupo de ámbito específico.</span><span class="sxs-lookup"><span data-stu-id="69f2e-121">Within each scope group, however, hello user must pass every clause toopass that specific scope group.</span></span> 

<span data-ttu-id="69f2e-122">En otras palabras, puede pensar en grupos de ámbito como o juntos, y se puede considerar las cláusulas de hello dentro de ellos como AND haría juntos.</span><span class="sxs-lookup"><span data-stu-id="69f2e-122">In other words, you can think of scope groups as being OR’d together, and you can think of hello clauses within them as being AND’d together.</span></span> <span data-ttu-id="69f2e-123">Por ejemplo, considere la posibilidad de hello siguiente filtro de ámbito:</span><span class="sxs-lookup"><span data-stu-id="69f2e-123">For example, consider hello scoping filter below:</span></span>

![Nombre del grupo de ámbito][3]  

<span data-ttu-id="69f2e-125">Según toothis filtro de ámbito, los usuarios deben cumplir los siguientes Hola criterios, toobe aprovisionado:</span><span class="sxs-lookup"><span data-stu-id="69f2e-125">According toothis scoping filter, users must satisfy hello following criteria, toobe provisioned:</span></span>

1. <span data-ttu-id="69f2e-126">Deben estar asignados toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="69f2e-126">They must be assigned toohello application.</span></span>
2. <span data-ttu-id="69f2e-127">Debe trabajar en el departamento de ingeniería de Hola</span><span class="sxs-lookup"><span data-stu-id="69f2e-127">They must work in hello Engineering department</span></span>
3. <span data-ttu-id="69f2e-128">Deben trabajar en San Francisco o Canadá.</span><span class="sxs-lookup"><span data-stu-id="69f2e-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="69f2e-129">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="69f2e-129">Related Articles</span></span>
* [<span data-ttu-id="69f2e-130">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69f2e-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="69f2e-131">Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones</span><span class="sxs-lookup"><span data-stu-id="69f2e-131">Automate User Provisioning and Deprovisioning tooSaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="69f2e-132">Personalización de asignaciones de atributos para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="69f2e-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="69f2e-133">Escritura de expresiones para asignaciones de atributos</span><span class="sxs-lookup"><span data-stu-id="69f2e-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="69f2e-134">Notificaciones de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="69f2e-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="69f2e-135">Uso de SCIM tooenable el aprovisionamiento automático de usuarios y grupos de Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="69f2e-135">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="69f2e-136">Lista de tutoriales sobre cómo tooIntegrate aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="69f2e-136">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
