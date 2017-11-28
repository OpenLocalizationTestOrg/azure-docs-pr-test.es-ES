---
title: "toocontrol de Control de acceso basado en roles (RBAC) aaaAzure toocreate de derechos de acceso y administrar solicitudes de soporte técnico | Documentos de Microsoft"
description: "Azure toocontrol de Control de acceso basado en roles (RBAC) toocreate de derechos de acceso y administrar solicitudes de soporte técnico"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="3873c-103">Azure toocontrol de Control de acceso basado en roles (RBAC) toocreate de derechos de acceso y administrar solicitudes de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="3873c-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="3873c-104">El [control de acceso basado en rol (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permite realizar una administración detallada del acceso en Azure.</span><span class="sxs-lookup"><span data-stu-id="3873c-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="3873c-105">Admite la creación de solicitud en el portal de Azure, hello [portal.azure.com](https://portal.azure.com), usa toodefine de modelo RBAC de Azure que puede crear y administrar solicitudes de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="3873c-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="3873c-106">Se concede acceso mediante la asignación de hello adecuado RBAC rol toousers, grupos y las aplicaciones en un ámbito determinado, que puede ser una suscripción, el grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="3873c-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="3873c-107">Veamos un ejemplo: como propietario de un grupo de recursos con permisos de lectura en el ámbito de la suscripción de hello, puede administrar todos los recursos de hello en el grupo de recursos de hello, como sitios Web, máquinas virtuales y subredes.</span><span class="sxs-lookup"><span data-stu-id="3873c-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="3873c-108">Sin embargo, cuando intente toocreate una solicitud de soporte técnico en un recurso de la máquina virtual de hello, encontrar Hola tras error</span><span class="sxs-lookup"><span data-stu-id="3873c-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![Error de suscripción](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="3873c-110">En administración de solicitudes de soporte técnico, necesita permiso de escritura o un rol que tenga Hola acción Microsoft.Support/* en hello suscripción ámbito toobe capaz de toocreate y administrar solicitudes de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="3873c-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="3873c-111">Hola artículo siguiente explica cómo puede utilizar toocreate de Control de acceso basado en roles (RBAC) personalizado de Azure y administrar solicitudes de soporte técnico en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3873c-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="3873c-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="3873c-112">Getting Started</span></span>

<span data-ttu-id="3873c-113">Utilizando el ejemplo de Hola anterior, sería capaz de toocreate una solicitud de soporte técnico para el recurso si se asigna un rol personalizado de RBAC en suscripción Hola por el propietario de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3873c-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="3873c-114">[Roles personalizados de RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) pueden crearse con hello API de REST, interfaz de línea de comandos (CLI) de Azure y Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3873c-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="3873c-115">propiedad de las acciones de Hola de un rol personalizado especifica hello Azure operaciones toowhich Hola función concede acceso.</span><span class="sxs-lookup"><span data-stu-id="3873c-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="3873c-116">toocreate un rol personalizado para la administración de la solicitud de soporte técnico, el rol de hello debe tener la acción de hello Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="3873c-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="3873c-117">Este es un ejemplo de un rol personalizado puede utilizar toocreate y administrar las solicitudes de soporte.</span><span class="sxs-lookup"><span data-stu-id="3873c-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="3873c-118">Nos hemos denominado este rol "Colaborador de solicitud de soporte técnico" y así es cómo nos referimos toohello rol personalizado en este artículo.</span><span class="sxs-lookup"><span data-stu-id="3873c-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="3873c-119">Siga los pasos de hello descritos en [este vídeo](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn cómo toocreate un rol personalizado para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="3873c-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="3873c-120">Crear y administrar solicitudes de soporte técnico en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3873c-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="3873c-121">Veamos un ejemplo: es propietario de Hola de suscripción "Visual Studio MSDN suscripción."</span><span class="sxs-lookup"><span data-stu-id="3873c-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="3873c-122">Juan es el punto que es un toosome de propietario de recursos de grupos de recursos de hello en esta suscripción y tiene la suscripción de toohello de permiso de lectura.</span><span class="sxs-lookup"><span data-stu-id="3873c-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="3873c-123">Desea toogive acceso tooyour del mismo nivel, Joe, toocreate de capacidad de Hola y administrar incidencias de soporte técnico para los recursos de hello en esta suscripción.</span><span class="sxs-lookup"><span data-stu-id="3873c-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="3873c-124">Hola primer paso es toogo toohello suscripción y en "Configuración" verá una lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3873c-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="3873c-125">Haga clic en el usuario de Hola Juan quién tiene acceso de lectura de hello suscripción y vamos a asignar un nuevo toohim roles personalizados.</span><span class="sxs-lookup"><span data-stu-id="3873c-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![Agregar rol](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="3873c-127">En la hoja de "Users" Hola, haga clic en "Agregar".</span><span class="sxs-lookup"><span data-stu-id="3873c-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="3873c-128">Seleccionar roles personalizados de Hola "Colaborador de solicitud de soporte técnico" de lista de Hola de roles</span><span class="sxs-lookup"><span data-stu-id="3873c-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![Agregar rol de colaborador de soporte técnico](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="3873c-130">Después de seleccionar el nombre de la función hello, haga clic en "Agregar usuarios" y escriba las credenciales de correo electrónico de Hola Juan.</span><span class="sxs-lookup"><span data-stu-id="3873c-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="3873c-131">Haga clic en "Seleccionar"</span><span class="sxs-lookup"><span data-stu-id="3873c-131">Click "Select"</span></span>

    ![Agregar usuarios](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="3873c-133">Haga clic en "Aceptar" tooproceed</span><span class="sxs-lookup"><span data-stu-id="3873c-133">Click "Ok" tooproceed</span></span>

    ![Agregar acceso](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="3873c-135">Ahora verá el usuario de hello con hello roles personalizados recién agregado "Compatibilidad con solicitudes Colaborador" en la suscripción de Hola que es propietario de Hola</span><span class="sxs-lookup"><span data-stu-id="3873c-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![Usuario agregado](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="3873c-137">Cuando Juan inicia sesión en el portal de hello, ve hello toowhich de suscripción que se agregó.</span><span class="sxs-lookup"><span data-stu-id="3873c-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="3873c-138">Juan hace clic en "Nueva solicitud de soporte técnico" de la hoja de "Ayuda y soporte técnico" hello y puede crear solicitudes de soporte técnico para "Visual Studio Ultimate con MSDN"</span><span class="sxs-lookup"><span data-stu-id="3873c-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nueva solicitud de soporte](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="3873c-140">Haga clic en "Todos admiten solicitudes" Juan puede ver lista de Hola de solicitudes de soporte creada para esta suscripción ![caso la vista de detalles](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="3873c-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="3873c-141">Quitar el acceso de solicitud de soporte en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3873c-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="3873c-142">Del mismo modo que es posible toogrant acceso tooa usuario toocreate y administrar solicitudes de soporte técnico, es acceso tooremove posibles para el usuario de hello así.</span><span class="sxs-lookup"><span data-stu-id="3873c-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="3873c-143">tooremove Hola capacidad toocreate administrar solicitudes de soporte técnico, vaya toohello suscripción, haga clic en "Configuración" y haga clic en usuario hello (en este caso, Juan).</span><span class="sxs-lookup"><span data-stu-id="3873c-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="3873c-144">Haga clic en nombre de rol de hello, "Colaborador de solicitud de soporte técnico" y haga clic en "Quitar"</span><span class="sxs-lookup"><span data-stu-id="3873c-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![Quitar el acceso a la solicitud de soporte técnico](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="3873c-146">Cuando Juan inicia sesión en el portal de toohello e intenta toocreate una solicitud de soporte técnico, encuentra Hola tras error</span><span class="sxs-lookup"><span data-stu-id="3873c-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![Error de suscripción-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="3873c-148">Joe no ve ninguna de las solicitudes de soporte técnico al hacer clic en "All support requests" (Todas las solicitudes de soporte técnico)</span><span class="sxs-lookup"><span data-stu-id="3873c-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![vista de detalles del caso-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
