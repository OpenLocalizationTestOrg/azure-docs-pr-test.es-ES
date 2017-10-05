---
title: Crear roles personalizados de control de acceso basado en roles y asignarlos a usuarios internos y externos en Azure | Microsoft Docs
description: Asignar roles personalizados de RBAC creados con PowerShell y la CLI para usuarios internos y externos
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: d687f94bebfd0b6c1ec0690da798be5409640954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="db244-103">Introducción al control de acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="db244-103">Intro on role-based access control</span></span>

<span data-ttu-id="db244-104">El control de acceso basado en roles es una característica de Azure Portal que permite a los propietarios de una suscripción asignar roles granulares a otros usuarios que pueden administrar ámbitos de recursos específicos en su entorno.</span><span class="sxs-lookup"><span data-stu-id="db244-104">Role-based access control is an Azure portal only feature allowing the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="db244-105">RBAC permite una mejor administración de seguridad para organizaciones grandes y para PYMES que trabajan con colaboradores externos, proveedores o autónomos que necesitan tener acceso a recursos específicos de su entorno, pero no necesariamente a toda la infraestructura ni a los ámbitos relacionados con la facturación.</span><span class="sxs-lookup"><span data-stu-id="db244-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access to specific resources in your environment but not necessarily to the entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="db244-106">RBAC proporciona la flexibilidad de tener una suscripción de Azure administrada por el administrador de la cuenta (rol de administrador de servicio en el nivel de suscripción) y tener múltiples usuarios invitados que trabajen con la misma suscripción pero sin tener derechos administrativos en ella.</span><span class="sxs-lookup"><span data-stu-id="db244-106">RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="db244-107">Desde una perspectiva de facturación y administración, la característica RBAC resulta ser una opción de administración eficaz y rápida para el uso de Azure en distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="db244-107">From a management and billing perspective, the RBAC feature proves to be a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db244-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="db244-108">Prerequisites</span></span>
<span data-ttu-id="db244-109">El uso de RBAC en el entorno de Azure requiere:</span><span class="sxs-lookup"><span data-stu-id="db244-109">Using RBAC in the Azure environment requires:</span></span>

* <span data-ttu-id="db244-110">Tener una suscripción de Azure independiente asignada al usuario como propietario (rol de suscripción)</span><span class="sxs-lookup"><span data-stu-id="db244-110">Having a standalone Azure subscription assigned to the user as owner (subscription role)</span></span>
* <span data-ttu-id="db244-111">Tener el rol de propietario de la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="db244-111">Have the Owner role of the Azure subscription</span></span>
* <span data-ttu-id="db244-112">Tener acceso a [Azure Portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="db244-112">Have access to the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="db244-113">Asegúrese de tener los siguientes proveedores de recursos registrados para la suscripción del usuario: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="db244-113">Make sure to have the following Resource Providers registered for the user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="db244-114">Para más información sobre cómo registrar los proveedores de recursos, consulte [Proveedores del Administrador de recursos, regiones, versiones de API y esquemas](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="db244-114">For more information on how to register the resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="db244-115">Las suscripciones de Office 365 y las licencias de Azure Active Directory (por ejemplo, acceso a Azure Active Directory) aprovisionadas desde el portal de O365 no permiten el uso de RBAC.</span><span class="sxs-lookup"><span data-stu-id="db244-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access to Azure Active Directory) provisioned from the O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="db244-116">Uso de RBAC</span><span class="sxs-lookup"><span data-stu-id="db244-116">How can RBAC be used</span></span>
<span data-ttu-id="db244-117">RBAC puede aplicarse en tres ámbitos diferentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="db244-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="db244-118">Del ámbito más alto al más bajo, son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="db244-118">From the highest scope to the lowest one, they are as follows:</span></span>

* <span data-ttu-id="db244-119">Suscripción (más alto)</span><span class="sxs-lookup"><span data-stu-id="db244-119">Subscription (highest)</span></span>
* <span data-ttu-id="db244-120">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="db244-120">Resource group</span></span>
* <span data-ttu-id="db244-121">Ámbito de recurso (el nivel más bajo de acceso, que ofrece permisos destinados al ámbito de un recurso individual de Azure)</span><span class="sxs-lookup"><span data-stu-id="db244-121">Resource scope (the lowest access level offering targeted permissions to an individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-the-subscription-scope"></a><span data-ttu-id="db244-122">Asignación de roles RBAC en el ámbito de la suscripción</span><span class="sxs-lookup"><span data-stu-id="db244-122">Assign RBAC roles at the subscription scope</span></span>
<span data-ttu-id="db244-123">Hay dos ejemplos comunes (entre otros) en los que se utiliza RBAC:</span><span class="sxs-lookup"><span data-stu-id="db244-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="db244-124">Existencia de usuarios externos a las organizaciones (no forman parte del inquilino de Azure Active Directory del usuario administrador) invitados a administrar determinados recursos o la suscripción completa</span><span class="sxs-lookup"><span data-stu-id="db244-124">Having external users from the organizations (not part of the admin user's Azure Active Directory tenant) invited to manage certain resources or the whole subscription</span></span>
* <span data-ttu-id="db244-125">Existencia de usuarios dentro de la organización (forman parte del inquilino de Azure Active Directory del usuario administrador) que son parte de equipos o grupos distintos y necesitan acceso granular bien a la suscripción completa o a determinados grupos de recursos o ámbitos de recursos del entorno.</span><span class="sxs-lookup"><span data-stu-id="db244-125">Working with users inside the organization (they are part of the user's Azure Active Directory tenant) but part of different teams or groups which need granular access either to the whole subscription or to certain resource groups or resource scopes in the environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="db244-126">Conceder acceso en el nivel de suscripción para un usuario fuera de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db244-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="db244-127">Solo los **Propietarios** de la suscripción pueden conceder roles RBAC, por tanto, el usuario administrador debe haber iniciado sesión con un nombre de usuario que tiene este rol asignado previamente o que ha creado la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="db244-127">RBAC roles can be granted only by **Owners** of the subscription therefore the admin user must be logged with a username which has this role pre-assigned or has created the Azure subscription.</span></span>

<span data-ttu-id="db244-128">En Azure Portal, una vez que inicie sesión como administrador, seleccione "Suscripciones" y seleccione la suscripción deseada.</span><span class="sxs-lookup"><span data-stu-id="db244-128">From the Azure portal, after you sign-in as admin, select “Subscriptions” and chose the desired one.</span></span>
<span data-ttu-id="db244-129">![Hoja Suscripciones en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) De forma predeterminada, si el usuario administrador adquirió la suscripción de Azure, el usuario aparecerá como **Administrador de la cuenta**, siendo este el rol de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="db244-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if the admin user has purchased the Azure subscription, the user will show up as **Account Admin**, this being the subscription role.</span></span> <span data-ttu-id="db244-130">Para más detalles sobre los roles de la suscripción de Azure, consulte [Adición o cambio de roles de administrador de Azure que administran la suscripción o los servicios](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="db244-130">For more details on the Azure subscription roles, see [Add or change Azure administrator roles that manage the subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="db244-131">En este ejemplo, el usuario "alflanigan@outlook.com" es el **Propietario** de la suscripción "Free Trial" en el inquilino de AAD "Default tenant Azure".</span><span class="sxs-lookup"><span data-stu-id="db244-131">In this example, the user "alflanigan@outlook.com" is the **Owner** of the "Free Trial" subscription in the AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="db244-132">Puesto que este usuario es el creador de la suscripción de Azure con la cuenta de Microsoft "Outlook" inicial (Microsoft Account = Outlook, Live, etc.), el nombre de dominio predeterminado para todos los demás usuarios agregados en este inquilino será **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="db244-132">Since this user is the creator of the Azure subscription with the initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) the default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="db244-133">Por diseño, la sintaxis del nuevo dominio se forma uniendo el nombre de usuario y el nombre de dominio del usuario que creó el inquilino y agregando la extensión **".onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="db244-133">By design, the syntax of the new domain is formed by putting together the username and domain name of the user who created the tenant and adding the extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="db244-134">Además, los usuarios pueden iniciar sesión con un nombre de dominio personalizado en el inquilino después de agregarlo y comprobarlo para el nuevo inquilino.</span><span class="sxs-lookup"><span data-stu-id="db244-134">Furthermore, users can sign-in with a custom domain name in the tenant after adding and verifying it for the new tenant.</span></span> <span data-ttu-id="db244-135">Para más información sobre cómo comprobar un nombre de dominio personalizado en un inquilino de Azure Active Directory, consulte [Agregar un nombre de dominio personalizado a su directorio](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="db244-135">For more details on how to verify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name to your directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="db244-136">En este ejemplo, el directorio "Default tenant Azure" contiene solo usuarios con el nombre de dominio "@alflanigan.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="db244-136">In this example, the "Default tenant Azure" directory contains only users with the domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="db244-137">Después de seleccionar la suscripción, el usuario administrador debe hacer clic en **Control de acceso (IAM)** y, a continuación, en **Agregar un nuevo rol**.</span><span class="sxs-lookup"><span data-stu-id="db244-137">After selecting the subscription, the admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Característica de control de acceso IAM en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Agregar un nuevo usuario en la característica de control de acceso IAM en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="db244-140">El siguiente paso es seleccionar el rol que se va a asignar y el usuario al que se va a asignar el rol de RBAC.</span><span class="sxs-lookup"><span data-stu-id="db244-140">The next step is to select the role to be assigned and the user whom the RBAC role will be assigned to.</span></span> <span data-ttu-id="db244-141">En el menú desplegable **Rol** el usuario administrador ve únicamente los roles RBAC integrados que están disponibles en Azure.</span><span class="sxs-lookup"><span data-stu-id="db244-141">In the **Role** dropdown menu the admin user sees only the built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="db244-142">Para obtener explicaciones detalladas de cada rol y sus ámbitos asignables, consulte [Roles integrados en el control de acceso basado en roles de Azure](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="db244-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="db244-143">El usuario administrador, a continuación, debe agregar la dirección de correo electrónico del usuario externo.</span><span class="sxs-lookup"><span data-stu-id="db244-143">The admin user then needs to add the email address of the external user.</span></span> <span data-ttu-id="db244-144">El comportamiento esperado para el usuario externo es que no aparezca en el inquilino existente.</span><span class="sxs-lookup"><span data-stu-id="db244-144">The expected behavior is for the external user to not show up in the existing tenant.</span></span> <span data-ttu-id="db244-145">Cuando el usuario externo haya sido invitado, será visible en **Suscripciones > Control de acceso (IAM)** con todos los usuarios que están asignados actualmente a un rol de RBAC en el ámbito de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="db244-145">After the external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all the current users which are currently assigned an RBAC role at the Subscription scope.</span></span>





![Agregar permisos al nuevo rol de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Lista de roles RBAC en el nivel de suscripción](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="db244-148">El usuario "chessercarlton@gmail.com" ha sido invitado como **Propietario** de la suscripción "Free Trial".</span><span class="sxs-lookup"><span data-stu-id="db244-148">The user "chessercarlton@gmail.com" has been invited to be an **Owner** for the “Free Trial” subscription.</span></span> <span data-ttu-id="db244-149">Después de enviar la invitación, el usuario externo recibirá una confirmación por correo electrónico con un enlace de activación.</span><span class="sxs-lookup"><span data-stu-id="db244-149">After sending the invitation, the external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="db244-150">![invitación por correo electrónico para el rol de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="db244-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="db244-151">Al ser un usuario externo a la organización, el nuevo usuario no tiene ningún atributo en el directorio "Default tenant Azure".</span><span class="sxs-lookup"><span data-stu-id="db244-151">Being external to the organization, the new user does not have any existing attributes in the "Default tenant Azure" directory.</span></span> <span data-ttu-id="db244-152">Estos se crearán después de que el usuario externo haya dado su consentimiento para ser registrado en el directorio asociado con la suscripción para la que se le ha asignado el rol.</span><span class="sxs-lookup"><span data-stu-id="db244-152">They will be created after the external user has given consent to be recorded in the directory which is associated with the subscription which he has been assigned a role to.</span></span>





![Mensaje de invitación por correo electrónico para el rol de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="db244-154">El usuario externo aparece en el inquilino de Azure Active Directory a partir de ahora como un usuario externo, y se puede ver tanto en Azure Portal como en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="db244-154">The external user shows in the Azure Active Directory tenant from now on as external user and this can be viewed both in the Azure portal and in the classic portal.</span></span>





![Hoja de usuarios de Azure Active Directory en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Hoja de usuarios de Azure Active Directory en el Portal de Azure clásico](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="db244-157">En la vista **Usuarios** de ambos portales, los usuarios externos se pueden reconocer por:</span><span class="sxs-lookup"><span data-stu-id="db244-157">In the **Users** view in both portals the external users can be recognized by:</span></span>

* <span data-ttu-id="db244-158">Un tipo de icono diferente en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="db244-158">The different icon type in the Azure portal</span></span>
* <span data-ttu-id="db244-159">Un punto de origen diferente en el portal clásico</span><span class="sxs-lookup"><span data-stu-id="db244-159">The different sourcing point in the classic portal</span></span>

<span data-ttu-id="db244-160">Sin embargo, conceder acceso como **Propietario** o **Colaborador** a un usuario externo en el ámbito de la **Suscripción** no permite el acceso al directorio del usuario administrador, a menos que el **Administrador global** lo permita.</span><span class="sxs-lookup"><span data-stu-id="db244-160">However, granting **Owner** or **Contributor** access to an external user at the **Subscription** scope, does not allow the access to the admin user's directory, unless the **Global Admin** allows it.</span></span> <span data-ttu-id="db244-161">En las propiedades del usuario, el **Tipo de usuario**, que tiene dos parámetros comunes, se pueden identificar **Miembro** e **Invitado**.</span><span class="sxs-lookup"><span data-stu-id="db244-161">In the user proprieties,  the **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="db244-162">Un miembro es un usuario que está registrado en el directorio, mientras que un invitado es un usuario invitado al directorio desde un origen externo.</span><span class="sxs-lookup"><span data-stu-id="db244-162">A member is a user which is registered in the directory while a guest is a user invited to the directory from an external source.</span></span> <span data-ttu-id="db244-163">Para más información, consulte [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](/active-directory/active-directory-b2b-admin-add-users)</span><span class="sxs-lookup"><span data-stu-id="db244-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="db244-164">Asegúrese de que, después de escribir las credenciales en el portal, el usuario externo selecciona el directorio correcto en el que se iniciará sesión.</span><span class="sxs-lookup"><span data-stu-id="db244-164">Make sure that after entering the credentials in the portal, the external user selects the correct directory to sign-in to.</span></span> <span data-ttu-id="db244-165">El mismo usuario puede tener acceso a varios directorios y puede seleccionar cualquiera de ellos haciendo clic en el nombre de usuario en la parte superior derecha de Azure Portal y, a continuación, seleccionando el directorio adecuado en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="db244-165">The same user can have access to multiple directories and can select either one of  them by clicking the username in the top right-hand side in the Azure portal and then choose the appropriate directory from the dropdown list.</span></span>

<span data-ttu-id="db244-166">Al ser un invitado en el directorio, el usuario externo puede administrar todos los recursos de la suscripción de Azure, pero no tiene acceso al directorio.</span><span class="sxs-lookup"><span data-stu-id="db244-166">While being a guest in the directory, the external user can manage all resources for the Azure subscription, but can't access the directory.</span></span>





![Acceso restringido a Azure Active Directory en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="db244-168">Azure Active Directory y una suscripción de Azure no tienen una relación de primario-secundario como tienen otros recursos de Azure (por ejemplo: las máquinas virtuales, las redes virtuales, las aplicaciones web, el almacenamiento, etc.) en una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="db244-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="db244-169">Todo lo anterior se crea, administra y factura en una suscripción de Azure, mientras que se usa una suscripción de Azure para administrar el acceso a un directorio de Azure.</span><span class="sxs-lookup"><span data-stu-id="db244-169">All the latter is created, managed and billed under an Azure subscription while an Azure subscription is used to manage the access to an Azure directory.</span></span> <span data-ttu-id="db244-170">Para más información, consulte [Cómo se relaciona una suscripción de Azure a Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="db244-170">For more details, see [How an Azure subscription is related to Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="db244-171">De todos los roles integrados de RBAC, **Propietario** y **Colaborador** ofrecen acceso administrativo completo a todos los recursos del entorno, la diferencia radica en que un colaborador no puede crear y eliminar nuevos roles RBAC.</span><span class="sxs-lookup"><span data-stu-id="db244-171">From all the built-in RBAC roles, **Owner** and **Contributor** offer full management access to all resources in the environment, the difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="db244-172">Otros roles integrados, como **Colaborador de la máquina virtual**, ofrecen acceso de administración completa solo a los recursos indicados por el nombre, con independencia del **Grupo de recursos** en el que se creen.</span><span class="sxs-lookup"><span data-stu-id="db244-172">The other built-in roles like **Virtual Machine Contributor** offer full management access only to the resources indicated by the name, regardless of the **Resource Group** they are being created into.</span></span>

<span data-ttu-id="db244-173">Asignar el rol integrado de RBAC de **Colaborador de la máquina virtual** en el nivel de suscripción significa que el usuario al que se le ha asignado el rol:</span><span class="sxs-lookup"><span data-stu-id="db244-173">Assigning the built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that the user assigned the role:</span></span>

* <span data-ttu-id="db244-174">Puede ver todas las máquinas virtuales con independencia de su fecha de implementación y del grupo de recursos del que forman parte.</span><span class="sxs-lookup"><span data-stu-id="db244-174">Can view all virtual machines regardless their deployment date and the resource groups they are part of</span></span>
* <span data-ttu-id="db244-175">Tiene acceso completo de administración a las máquinas virtuales de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="db244-175">Has full management access to the virtual machines in the subscription</span></span>
* <span data-ttu-id="db244-176">No puede ver ningún otro tipo de recursos de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="db244-176">Can't view any other resource types in the subscription</span></span>
* <span data-ttu-id="db244-177">No puede realizar ningún cambio desde la perspectiva de facturación.</span><span class="sxs-lookup"><span data-stu-id="db244-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="db244-178">Al ser RBAC una característica solo de Azure Portal, no concede acceso al portal clásico.</span><span class="sxs-lookup"><span data-stu-id="db244-178">RBAC being an Azure portal only feature, it doesn't grant access to the classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-to-an-external-user"></a><span data-ttu-id="db244-179">Asignación de un rol integrado de RBAC a un usuario externo</span><span class="sxs-lookup"><span data-stu-id="db244-179">Assign a built-in RBAC role to an external user</span></span>
<span data-ttu-id="db244-180">Para un escenario diferente en esta prueba, el usuario externo "alflanigan@gmail.com" se agrega como un **Colaborador de la máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="db244-180">For a different scenario in this test, the external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![Rol integrado de colaborador de la máquina virtual](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="db244-182">El comportamiento normal para un usuario externo con este rol integrado es ver y administrar máquinas virtuales y solo sus recursos adyacentes necesarios de Resource Manager durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="db244-182">The normal behavior for this external user with this built-in role is to see and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="db244-183">Por diseño, estos roles limitados ofrecen acceso solo a los recursos correspondientes creados en Azure Portal, aunque algunos recursos aún pueden ser implementados también en el portal clásico (por ejemplo, máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="db244-183">By design, these limited roles offer access only to their correspondent resources created in the Azure portal, regardless some can still be deployed in the classic portal as well (for example: virtual machines).</span></span>





![Información general sobre el rol de colaborador de la máquina virtual en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-the-same-directory"></a><span data-ttu-id="db244-185">Concesión de acceso en el nivel de suscripción a un usuario del mismo directorio</span><span class="sxs-lookup"><span data-stu-id="db244-185">Grant access at a subscription level for a user in the same directory</span></span>
<span data-ttu-id="db244-186">El flujo del proceso es idéntico al agregar un usuario externo, tanto desde la perspectiva del administrador que concede el rol de RBAC como del usuario al que se concede el acceso al rol.</span><span class="sxs-lookup"><span data-stu-id="db244-186">The process flow is identical to adding an external user, both from the admin perspective granting the RBAC role as well as the user being granted access to the role.</span></span> <span data-ttu-id="db244-187">La diferencia es que el usuario invitado no recibe ninguna invitación por correo electrónico ya que los ámbitos de recursos de la suscripción estarán disponibles en el panel después de iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="db244-187">The difference here is that the invited user will not receive any email invitations as all the resource scopes within the subscription will be available in the dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-the-resource-group-scope"></a><span data-ttu-id="db244-188">Asignación de roles de RBAC en el ámbito del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="db244-188">Assign RBAC roles at the resource group scope</span></span>
<span data-ttu-id="db244-189">El proceso de asignación de un rol de RBAC en un ámbito **Grupo de recursos** es idéntico al de asignar el rol en el nivel de suscripción para ambos tipos de usuarios: internos o externos (parte del mismo directorio).</span><span class="sxs-lookup"><span data-stu-id="db244-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning the role at the subscription level, for both types of users - either external or internal (part of the same directory).</span></span> <span data-ttu-id="db244-190">Los usuarios a los que se les ha asignado del rol de RBAC verán en su entorno únicamente el grupo de recursos al que se les asignó acceso desde el icono **Grupo de recursos** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="db244-190">The users which are assigned the RBAC role is to see in their environment only the resource group they have been assigned access from the **Resource Groups** icon in the Azure portal.</span></span>

## <a name="assign-rbac-roles-at-the-resource-scope"></a><span data-ttu-id="db244-191">Asignación de roles de RBAC en el ámbito del recurso</span><span class="sxs-lookup"><span data-stu-id="db244-191">Assign RBAC roles at the resource scope</span></span>
<span data-ttu-id="db244-192">El proceso de asignación de un rol de RBAC en el ámbito del recurso en Azure es idéntico al de asignar un rol en el nivel de suscripción o de grupo de recursos, y se sigue el mismo flujo de trabajo en ambos escenarios.</span><span class="sxs-lookup"><span data-stu-id="db244-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning the role at the subscription level or at the resource group level, following the same workflow for both scenarios.</span></span> <span data-ttu-id="db244-193">Del mismo modo, los usuarios a los que se ha asignado el rol de RBAC solo pueden ver los elementos a los que se les ha asignado acceso, tanto en la pestaña **Todos los recursos** como directamente en su panel.</span><span class="sxs-lookup"><span data-stu-id="db244-193">Again, the users which are assigned the RBAC role can see only the items that they have been assigned access to, either in the **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="db244-194">Un aspecto importante de RBAC tanto en el ámbito de un grupo de recursos como en el de un recurso es asegurarse de que los usuarios inician sesión en el directorio correcto.</span><span class="sxs-lookup"><span data-stu-id="db244-194">An important aspect for RBAC both at resource group scope or resource scope is for the users to make sure to sign-in to the correct directory.</span></span>





![Inicio de sesión en un directorio en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="db244-196">Asignación de roles de RBAC en un grupo de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db244-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="db244-197">Todos los escenarios que usan RBAC en los tres ámbitos distintos de Azure ofrecen el privilegio de administrar e implementar diversos recursos como usuario asignado sin necesidad de administrar una suscripción personal.</span><span class="sxs-lookup"><span data-stu-id="db244-197">All the scenarios using RBAC at the three different scopes in Azure offer the privilege of managing, deploying and administering various resources as an assigned user without the need of managing a personal subscription.</span></span> <span data-ttu-id="db244-198">Aunque el rol de RBAC se asigna para un ámbito de suscripción, grupo de recursos o recurso, todos los recursos creados por los usuarios asignados se facturan a una suscripción de Azure a la que los usuarios tienen acceso.</span><span class="sxs-lookup"><span data-stu-id="db244-198">Regardless the RBAC role is assigned for a subscription, resource group or resource scope, all the resources created further on by the assigned users are billed under the one Azure subscription where the users have access to.</span></span> <span data-ttu-id="db244-199">De este modo, los usuarios que tienen permisos de administrador de facturación para la suscripción de Azure tienen una información general completa del consumo, independientemente de quién administra los recursos.</span><span class="sxs-lookup"><span data-stu-id="db244-199">This way, the users who have billing administrator permissions for that entire Azure subscription has a complete overview on the consumption, regardless who is managing the resources.</span></span>

<span data-ttu-id="db244-200">Para organizaciones de mayor tamaño, los roles de RBAC se pueden aplicar del mismo modo para grupos de Azure Active Directory, dando por hecho que el usuario administrador quiera conceder acceso granular a equipos o departamentos enteros y no individualmente a cada usuario, considerándose así una opción muy eficiente en tiempo y administración.</span><span class="sxs-lookup"><span data-stu-id="db244-200">For larger organizations, RBAC roles can be applied in the same way for Azure Active Directory groups considering the perspective that the admin user wants to grant the granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="db244-201">Para ilustrar este ejemplo, el rol **Colaborador** se ha agregado a uno de los grupos en el inquilino en el nivel de suscripción.</span><span class="sxs-lookup"><span data-stu-id="db244-201">To illustrate this example, the **Contributor** role has been added to one of the groups in the tenant at the subscription level.</span></span>





![Agregar rol de RBAC para grupos de AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="db244-203">Estos grupos son grupos de seguridad que se aprovisionan y administran únicamente dentro de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db244-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-powershell"></a><span data-ttu-id="db244-204">Creación de un rol de RBAC personalizado para abrir solicitudes de soporte técnico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="db244-204">Create a custom RBAC role to open support requests using PowerShell</span></span>
<span data-ttu-id="db244-205">Los roles de RBAC integrados disponibles en Azure aseguran ciertos niveles de permisos en función de los recursos disponibles en el entorno.</span><span class="sxs-lookup"><span data-stu-id="db244-205">The built-in RBAC roles which are available in Azure ensure certain permission levels based on the available resources in the environment.</span></span> <span data-ttu-id="db244-206">Sin embargo, si ninguno de estos roles se ajusta a las necesidades del usuario administrador, existe la opción de limitar aún más el acceso mediante la creación de roles de RBAC personalizados.</span><span class="sxs-lookup"><span data-stu-id="db244-206">However, if none of these roles suit the admin user's needs, there is the option to limit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="db244-207">La creación de un rol de RBAC personalizado implica tomar un rol integrado, editarlo e importarlo de vuelta en el entorno.</span><span class="sxs-lookup"><span data-stu-id="db244-207">Creating custom RBAC roles requires to take one built-in role, edit it and then import it back in the environment.</span></span> <span data-ttu-id="db244-208">La descarga y la carga del rol se administran mediante PowerShell o la CLI.</span><span class="sxs-lookup"><span data-stu-id="db244-208">The download and upload of the role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="db244-209">Es importante entender los requisitos previos para la creación de un rol personalizado que pueda conceder acceso granular en el nivel de suscripción y también dar al usuario invitado la flexibilidad de abrir solicitudes de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="db244-209">It is important to understand the prerequisites of creating a custom role which can grant granular access at the subscription level and also allow the invited user the flexibility of opening support requests.</span></span>

<span data-ttu-id="db244-210">En este ejemplo, el rol integrado **Lector**, que otorga a los usuarios acceso para ver todos los ámbitos de recurso pero no editarlos ni crear nuevos, ha sido personalizado para permitir al usuario la opción de abrir solicitudes de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="db244-210">For this example the built-in role **Reader** which allows users access to view all the resource scopes but not to edit them or create new ones has been customized to allow the user the option of opening support requests.</span></span>

<span data-ttu-id="db244-211">La primera acción de exportación del rol **Lector** debe realizarse en PowerShell ejecutado con permisos elevados como administrador.</span><span class="sxs-lookup"><span data-stu-id="db244-211">The first action of exporting the **Reader** role needs to be completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Captura de pantalla de PowerShell para el rol Lector de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="db244-213">A continuación, debe extraer la plantilla JSON del rol.</span><span class="sxs-lookup"><span data-stu-id="db244-213">Then you need to extract the JSON template of the role.</span></span>





![Plantilla JSON para el rol personalizado Lector de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="db244-215">Un rol de RBAC típico se compone de tres secciones principales, **Actions**, **NotActions** y **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="db244-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="db244-216">En la sección **Action** se enumeran todas las operaciones permitidas para este rol.</span><span class="sxs-lookup"><span data-stu-id="db244-216">In the **Action** section are listed all the permitted operations for this role.</span></span> <span data-ttu-id="db244-217">Es importante comprender que cada acción se asigna desde un proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="db244-217">It's important to understand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="db244-218">En este caso, para la creación de incidencias de soporte técnico, el proveedor de recursos **Microsoft.Support** debe aparecer enumerado.</span><span class="sxs-lookup"><span data-stu-id="db244-218">In this case, for creating support tickets the **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="db244-219">Para poder ver todos los proveedores de recursos disponibles y registrados en su suscripción, puede usar PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db244-219">To be able to see all the resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="db244-220">Además, puede comprobar todos los cmdlets de PowerShell disponibles para administrar proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="db244-220">Additionally, you can check for the all the available PowerShell cmdlets to manage the resource providers.</span></span>
    <span data-ttu-id="db244-221">![Captura de pantalla de PowerShell para la administración de proveedores de recursos](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="db244-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="db244-222">Para restringir todas las acciones de un rol determinado de RBAC, los proveedores de recursos aparecen en la sección **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="db244-222">To restrict all the actions for a particular RBAC role, resource providers are listed under the section **NotActions**.</span></span>
<span data-ttu-id="db244-223">Por último, es obligatorio del rol de RBAC contenga los identificadores explícitos de suscripción en las que es utilizado.</span><span class="sxs-lookup"><span data-stu-id="db244-223">Last, it's mandatory that the RBAC role contains the explicit subscription IDs where it is used.</span></span> <span data-ttu-id="db244-224">Los identificadores de suscripción aparecen en la sección **AssignableScopes**, en caso contrario, no podrá importar el rol en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="db244-224">The subscription IDs are listed under the **AssignableScopes**, otherwise you will not be allowed to import the role in your subscription.</span></span>

<span data-ttu-id="db244-225">Después de crear y personalizar el rol de RBAC, debe importarse de vuelta en el entorno.</span><span class="sxs-lookup"><span data-stu-id="db244-225">After creating and customizing the RBAC role, it needs to be imported back the environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="db244-226">En este ejemplo, el nombre personalizado para este rol de RBAC es "Reader support tickets access level" y permite al usuario ver todo en la suscripción y también para abrir solicitudes de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="db244-226">In this example, the custom name for this RBAC role is "Reader support tickets access level" allowing the user to view everything in the subscription and also to open support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="db244-227">Los dos únicos roles integrados de RBAC que permiten la acción de apertura de solicitudes de soporte técnico son **Propietario** y **Colaborador**.</span><span class="sxs-lookup"><span data-stu-id="db244-227">The only two built-in RBAC roles allowing the action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="db244-228">Para que un usuario sea capaz de abrir solicitudes de soporte técnico, se le debe asignar un rol de RBAC solo en el ámbito de la suscripción, ya que todas las solicitudes de soporte técnico se crean en función de una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="db244-228">For a user to be able to open support requests, he must be assigned an RBAC role only at the subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="db244-229">Este nuevo rol personalizado se ha asignado a un usuario del mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="db244-229">This new custom role has been assigned to an user from the same directory.</span></span>





![Captura de pantalla de un rol personalizado de RBAC importado en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![Captura de pantalla de la asignación de un rol importado personalizado de RBAC a un usuario del mismo directorio](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Captura de pantalla de los permisos de un rol importado personalizado de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="db244-233">Este ejemplo se ha detallado más para destacar los límites de este rol de RBAC personalizado, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="db244-233">The example has been further detailed to emphasize the limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="db244-234">Puede crear nuevas solicitudes de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="db244-234">Can create new support requests</span></span>
* <span data-ttu-id="db244-235">No puede crear nuevos ámbitos de recursos (por ejemplo: máquinas virtuales)</span><span class="sxs-lookup"><span data-stu-id="db244-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="db244-236">No puede crear nuevos grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="db244-236">Can't create new resource groups</span></span>





![Captura de pantalla de un rol personalizado de RBAC que puede crear solicitudes de soporte técnico](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![Captura de pantalla de un rol personalizado de RBAC que no puede crear máquinas virtuales](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![Captura de pantalla de un rol personalizado de RBAC que no puede crear nuevos grupos de recursos](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-azure-cli"></a><span data-ttu-id="db244-240">Creación de un rol personalizado de RBAC para abrir solicitudes de soporte técnico con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="db244-240">Create a custom RBAC role to open support requests using Azure CLI</span></span>
<span data-ttu-id="db244-241">Trabajando en un Mac y sin tener acceso a PowerShell, la CLI de Azure es la mejor opción.</span><span class="sxs-lookup"><span data-stu-id="db244-241">Running on a Mac and without having access to PowerShell, Azure CLI is the way to go.</span></span>

<span data-ttu-id="db244-242">Los pasos para crear un rol personalizado son los mismos, con la única excepción de que con la CLI el rol no se puede descargar en una plantilla JSON, pero puede verse en la CLI.</span><span class="sxs-lookup"><span data-stu-id="db244-242">The steps to create a custom role are the same, with the sole exception that using CLI the role can't be downloaded in a JSON template, but it can be viewed in the CLI.</span></span>

<span data-ttu-id="db244-243">En este ejemplo se ha elegido el rol integrado **Lector de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="db244-243">For this example I have chosen the built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Captura de pantalla de la CLI que muestra un rol de lector de copia de seguridad](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="db244-245">Al editar el rol en Visual Studio después de copiar las propiedades en una plantilla JSON, el proveedor de recursos **Microsoft.Support** se ha agregado en la sección **Acciones** para que este usuario pueda abrir solicitudes de soporte técnico mientras sigue siendo un lector para los almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="db244-245">Editing the role in Visual Studio after copying the proprieties in a JSON template, the **Microsoft.Support** resource provider has been added in the **Actions** sections so that this user can open support requests while continuing to be a reader for the backup vaults.</span></span> <span data-ttu-id="db244-246">De nuevo, es necesario agregar el identificador de suscripción en la que se usará este rol en la sección **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="db244-246">Again it is necessary to add the subscription ID where this role will be used in the **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Captura de pantalla de la CLI con la importación de un rol personalizado de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="db244-248">El nuevo rol ahora está disponible en Azure Portal y el proceso de asignación es el mismo que en los ejemplos anteriores.</span><span class="sxs-lookup"><span data-stu-id="db244-248">The new role is now available in the Azure portal and the assignation process is the same as in the previous examples.</span></span>





![Captura de pantalla de Azure Portal de un rol personalizado de RBAC creado con la CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="db244-250">A partir de la última compilación de 2017, Azure Cloud Shell está disponible con carácter general.</span><span class="sxs-lookup"><span data-stu-id="db244-250">As of the latest Build 2017, the Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="db244-251">Azure Cloud Shell es un complemento del IDE y de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="db244-251">Azure Cloud Shell is a complement to IDE and the Azure Portal.</span></span> <span data-ttu-id="db244-252">Con este servicio, tiene un shell basado en explorador, autenticado y hospedado en Azure, que puede usar en lugar de la CLI instalada en su equipo.</span><span class="sxs-lookup"><span data-stu-id="db244-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
