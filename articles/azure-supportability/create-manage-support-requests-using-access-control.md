---
title: "Control de acceso basado en rol (RBAC) de Azure para controlar los derechos de acceso para crear y administrar solicitudes de soporte técnico | Microsoft Docs"
description: "Control de acceso basado en rol (RBAC) de Azure para controlar los derechos de acceso para crear y administrar solicitudes de soporte técnico"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: 20ebd324cbf379980b43d255d468673de2b6d950
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-based-access-control-rbac-to-control-access-rights-to-create-and-manage-support-requests"></a><span data-ttu-id="491ff-103">Control de acceso basado en rol (RBAC) de Azure para controlar los derechos de acceso para crear y administrar solicitudes de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="491ff-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span></span>

<span data-ttu-id="491ff-104">El [control de acceso basado en rol (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permite realizar una administración detallada del acceso en Azure.</span><span class="sxs-lookup"><span data-stu-id="491ff-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="491ff-105">La creación de solicitudes de soporte técnico en Azure Portal, [portal.azure.com](https://portal.azure.com), usa el modelo RBAC de Azure para definir quién puede crear y administrar solicitudes de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="491ff-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span></span>
<span data-ttu-id="491ff-106">El acceso se concede mediante la asignación del rol RBAC adecuado a los usuarios, grupos y aplicaciones de un determinado ámbito, que puede ser una suscripción, un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="491ff-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="491ff-107">Veamos un ejemplo: como propietario de un grupo de recursos con permisos de lectura en el ámbito de la suscripción puede administrar todos los recursos en el grupo de recursos, como sitios web, máquinas virtuales y subredes.</span><span class="sxs-lookup"><span data-stu-id="491ff-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="491ff-108">Sin embargo, al intentar crear una solicitud de soporte técnico en el recurso de la máquina virtual, aparece el siguiente error</span><span class="sxs-lookup"><span data-stu-id="491ff-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span></span>

![Error de suscripción](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="491ff-110">En la administración de solicitudes de soporte técnico, se necesita permiso de escritura o un rol que tenga la acción de soporte técnico Microsoft.Support/* en el ámbito Suscripción para poder crear y administrar solicitudes de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="491ff-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/* at the Subscription scope to be able to create and manage support requests.</span></span>

<span data-ttu-id="491ff-111">En el siguiente artículo se explica cómo se puede usar el control de acceso basado en rol (RBAC) de Azure para crear y administrar solicitudes de soporte técnico en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="491ff-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="491ff-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="491ff-112">Getting Started</span></span>

<span data-ttu-id="491ff-113">Con el ejemplo anterior podría crear una solicitud de soporte técnico para el recurso, si el propietario de la suscripción le asigna un rol RBAC personalizado en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="491ff-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span></span>
<span data-ttu-id="491ff-114">Se pueden crear [roles RBAC personalizados](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) mediante Azure PowerShell, la interfaz de la línea de comandos (CLI) de Azure y la API de REST.</span><span class="sxs-lookup"><span data-stu-id="491ff-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span></span>

<span data-ttu-id="491ff-115">La propiedad Actions de un rol personalizado especifica las operaciones de Azure para las que el rol concede acceso.</span><span class="sxs-lookup"><span data-stu-id="491ff-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span></span>
<span data-ttu-id="491ff-116">Para crear un rol personalizado para la administración de la solicitud de soporte técnico, el rol debe tener la acción Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="491ff-116">To create a custom role for support request management, the role must have the action Microsoft.Support/*</span></span>

<span data-ttu-id="491ff-117">A continuación, verá un ejemplo de un rol personalizado que se puede usar para crear y administrar solicitudes de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="491ff-117">Here’s an example of a custom role you can use to create and manage support requests.</span></span>
<span data-ttu-id="491ff-118">Hemos denominado a este rol "Support Request Contributor" y así es cómo nos referimos al rol personalizado en este artículo.</span><span class="sxs-lookup"><span data-stu-id="491ff-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span></span>

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

<span data-ttu-id="491ff-119">Siga los pasos que se describen en [este vídeo](https://www.youtube.com/watch?v=-PaBaDmfwKI) para aprender a crear un rol personalizado para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="491ff-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-the-azure-portal"></a><span data-ttu-id="491ff-120">Creación y administración de solicitudes de soporte en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="491ff-120">Create and manage support requests in the Azure portal</span></span>

<span data-ttu-id="491ff-121">Veamos un ejemplo: es el propietario de la suscripción "Visual Studio MSDN Subscription".</span><span class="sxs-lookup"><span data-stu-id="491ff-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="491ff-122">Joe es alguien de su mismo nivel que es el propietario de los recursos de algunos de los grupos de recursos de esta suscripción y tiene permiso de lectura en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="491ff-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span></span>
<span data-ttu-id="491ff-123">Desea conceder a Joe acceso a la capacidad de crear y administrar las incidencias de soporte técnico de los recursos de esta suscripción.</span><span class="sxs-lookup"><span data-stu-id="491ff-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span></span>

1. <span data-ttu-id="491ff-124">El primer paso es ir a la suscripción y en "Configuración" verá una lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="491ff-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="491ff-125">Haga clic en el usuario Joe, que tiene acceso de lectura en la suscripción y asígnele un nuevo rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="491ff-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span></span>

    ![Agregar rol](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="491ff-127">Haga clic en "Agregar" en la hoja "Usuarios".</span><span class="sxs-lookup"><span data-stu-id="491ff-127">Click "Add" under the "Users" blade.</span></span> <span data-ttu-id="491ff-128">Seleccione el rol personalizado "Support Request Contributor" en la lista de roles</span><span class="sxs-lookup"><span data-stu-id="491ff-128">Select the custom role "Support Request Contributor" from the list of roles</span></span>

    ![Agregar rol de colaborador de soporte técnico](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="491ff-130">Después de seleccionar el nombre del rol, haga clic en "Agregar usuarios" y escriba las credenciales de correo electrónico de Joe.</span><span class="sxs-lookup"><span data-stu-id="491ff-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span></span> <span data-ttu-id="491ff-131">Haga clic en "Seleccionar"</span><span class="sxs-lookup"><span data-stu-id="491ff-131">Click "Select"</span></span>

    ![Agregar usuarios](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="491ff-133">Haga clic en "Aceptar" para continuar</span><span class="sxs-lookup"><span data-stu-id="491ff-133">Click "Ok" to proceed</span></span>

    ![Agregar acceso](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="491ff-135">Ahora verá el usuario con el rol personalizado recién agregado "Support Request Contributor" en la suscripción de la que es propietario</span><span class="sxs-lookup"><span data-stu-id="491ff-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span></span>

    ![Usuario agregado](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="491ff-137">Cuando Joe inicia sesión en el portal, ve la suscripción a la que se le agregó.</span><span class="sxs-lookup"><span data-stu-id="491ff-137">When Joe logs in the portal, he sees the subscription to which he was added.</span></span>

7. <span data-ttu-id="491ff-138">Joe hace clic en "Nueva solicitud de soporte técnico" en la hoja "Ayuda y soporte técnico" y puede crear solicitudes de soporte técnico para "Visual Studio Ultimate con MSDN"</span><span class="sxs-lookup"><span data-stu-id="491ff-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nueva solicitud de soporte](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="491ff-140">Haga clic en "Todos admiten solicitudes" Juan puede ver la lista de solicitudes de soporte creada para esta suscripción ![caso la vista de detalles](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="491ff-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-the-azure-portal"></a><span data-ttu-id="491ff-141">Eliminación del acceso a solicitud de soporte técnico en el Azure Portal</span><span class="sxs-lookup"><span data-stu-id="491ff-141">Remove support request access in the Azure portal</span></span>

<span data-ttu-id="491ff-142">Al igual que se puede conceder acceso a un usuario para crear y administrar solicitudes de soporte técnico, también se puede quitar el acceso al usuario.</span><span class="sxs-lookup"><span data-stu-id="491ff-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span></span>
<span data-ttu-id="491ff-143">Para quitar la capacidad de crear y administrar solicitudes de soporte técnico, vaya a la suscripción, haga clic en "Configuración" y haga clic en el usuario (en este caso, Joe).</span><span class="sxs-lookup"><span data-stu-id="491ff-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span></span>
<span data-ttu-id="491ff-144">Haga clic con el botón derecho en el nombre del rol, "Support Request Contributor", y después en "Quitar"</span><span class="sxs-lookup"><span data-stu-id="491ff-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span></span>

![Quitar el acceso a la solicitud de soporte técnico](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="491ff-146">Cuando Joe inicia sesión en el portal e intenta crear una solicitud de soporte técnico, aparece el siguiente error</span><span class="sxs-lookup"><span data-stu-id="491ff-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span></span>

![Error de suscripción-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="491ff-148">Joe no ve ninguna de las solicitudes de soporte técnico al hacer clic en "All support requests" (Todas las solicitudes de soporte técnico)</span><span class="sxs-lookup"><span data-stu-id="491ff-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![vista de detalles del caso-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
