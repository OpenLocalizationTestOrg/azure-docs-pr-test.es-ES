---
title: Uso de grupos para administrar el acceso a recursos en Azure Active Directory | Microsoft Docs
description: "Cómo usar grupos en Azure Active Directory para administrar el acceso de los usuarios a recursos y aplicaciones en la nube y locales."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cd8125eda7643f0b190d35cbb89edf8b7b4eca30
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="manage-access-to-resources-with-azure-active-directory-groups"></a><span data-ttu-id="34b90-103">Administración del acceso a recursos con grupos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34b90-103">Manage access to resources with Azure Active Directory groups</span></span>
<span data-ttu-id="34b90-104">Azure Active Directory (Azure AD) es una completa solución de administración de identidades y acceso que proporciona un sólido conjunto de capacidades para administrar el acceso a aplicaciones locales y en la nube y recursos de Microsoft Online Services como Office 365 y todo un mundo de aplicaciones SaaS que no son de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="34b90-104">Azure Active Directory (Azure AD) is a comprehensive identity and access management solution that provides a robust set of capabilities to manage access to on-premises and cloud applications and resources including Microsoft online services like Office 365 and a world of non-Microsoft SaaS applications.</span></span> <span data-ttu-id="34b90-105">En este artículo se proporciona información general, pero si desea empezar a usar grupos de Azure AD ahora mismo, siga las instrucciones indicadas en [Administrar grupos de seguridad en Azure AD](active-directory-accessmanagement-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="34b90-105">This article provides an overview, but if you want to start using Azure AD groups right now, follow the instructions in [Managing security groups in Azure AD](active-directory-accessmanagement-manage-groups.md).</span></span> <span data-ttu-id="34b90-106">Para ver cómo se puede usar PowerShell para administrar grupos en Azure Active Directory, consulte [Cmdlets de Azure Active Directory para administrar grupos](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).</span><span class="sxs-lookup"><span data-stu-id="34b90-106">If you want to see how you can use PowerShell to manage groups in Azure Active directory you can read more in [Azure Active Directory cmdlets for group management](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="34b90-107">Para usar Azure Active Directory, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="34b90-107">To use Azure Active Directory, you need an Azure account.</span></span> <span data-ttu-id="34b90-108">Si aún no tiene ninguna, puede [registrarse para obtener una cuenta de Azure gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34b90-108">If you don't have an account, you can [sign up for a free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
>
>

<span data-ttu-id="34b90-109">Dentro de Azure AD, una de las principales características es la capacidad para administrar el acceso a los recursos.</span><span class="sxs-lookup"><span data-stu-id="34b90-109">Within Azure AD, one of the major features is the ability to manage access to resources.</span></span> <span data-ttu-id="34b90-110">Estos recursos pueden formar parte del directorio, como en el caso de los permisos para administrar objetos a través de roles en el directorio o los recursos externos al directorio, como las aplicaciones SaaS, los servicios de Azure y los sitios de SharePoint o los recursos publicados en modo local.</span><span class="sxs-lookup"><span data-stu-id="34b90-110">These resources can be part of the directory, as in the case of permissions to manage objects through roles in the directory, or resources that are external to the directory, such as SaaS applications, Azure services, and SharePoint sites or on-premises resources.</span></span> <span data-ttu-id="34b90-111">Existen cuatro formas de asignar a un usuario derechos de acceso a un recurso:</span><span class="sxs-lookup"><span data-stu-id="34b90-111">There are four ways a user can be assigned access rights to a resource:</span></span>

1. <span data-ttu-id="34b90-112">Asignación directa</span><span class="sxs-lookup"><span data-stu-id="34b90-112">Direct assignment</span></span>

    <span data-ttu-id="34b90-113">El propietario de un recurso puede entonces asignar directamente usuarios al mismo.</span><span class="sxs-lookup"><span data-stu-id="34b90-113">Users can be assigned directly to a resource by the owner of that resource.</span></span>
2. <span data-ttu-id="34b90-114">Pertenencia a grupos</span><span class="sxs-lookup"><span data-stu-id="34b90-114">Group membership</span></span>

    <span data-ttu-id="34b90-115">El propietario de un recurso puede asignarle un grupo y, al hacerlo, conceder acceso al recurso a los miembros de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="34b90-115">A group can be assigned to a resource by the resource owner, and by doing so, granting the members of that group access to the resource.</span></span> <span data-ttu-id="34b90-116">El propietario del grupo puede administrar entonces la pertenencia dicho grupo.</span><span class="sxs-lookup"><span data-stu-id="34b90-116">Membership of the group can then be managed by the owner of the group.</span></span> <span data-ttu-id="34b90-117">El propietario del recurso delega efectivamente en el propietario del grupo el permiso para asignar a usuarios a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="34b90-117">Effectively, the resource owner delegates the permission to assign users to their resource to the owner of the group.</span></span>
3. <span data-ttu-id="34b90-118">Basado en reglas</span><span class="sxs-lookup"><span data-stu-id="34b90-118">Rule-based</span></span>

    <span data-ttu-id="34b90-119">El propietario del recurso puede usar una regla para indicar a qué usuarios se les debe asignar acceso a un recurso.</span><span class="sxs-lookup"><span data-stu-id="34b90-119">The resource owner can use a rule to express which users should be assigned access to a resource.</span></span> <span data-ttu-id="34b90-120">El resultado de la regla depende de los atributos utilizados en dicha regla y de sus valores para usuarios específicos; si se hace así, el propietario del recurso delega efectivamente los derechos de administración de acceso en el origen de autoridad de los atributos usados en la regla.</span><span class="sxs-lookup"><span data-stu-id="34b90-120">The outcome of the rule depends on the attributes used in that rule and their values for specific users, and by doing so, the resource owner effectively delegates the right to manage access to their resource to the authoritative source for the attributes that are used in the rule.</span></span> <span data-ttu-id="34b90-121">El propietario del recurso sigue pudiendo administrar la regla propiamente dicha y determina qué atributos y valores proporcionan acceso a su recurso.</span><span class="sxs-lookup"><span data-stu-id="34b90-121">The resource owner still manages the rule itself and determines which attributes and values provide access to their resource.</span></span>
4. <span data-ttu-id="34b90-122">Autoridad externa</span><span class="sxs-lookup"><span data-stu-id="34b90-122">External authority</span></span>

    <span data-ttu-id="34b90-123">El acceso a un recurso se deriva de un origen externo, por ejemplo, un grupo que se sincroniza desde un origen de autoridad, como un directorio local o una aplicación de SaaS como WorkDay.</span><span class="sxs-lookup"><span data-stu-id="34b90-123">The access to a resource is derived from an external source; for example, a group that is synchronized from an authoritative source such as an on-premises directory or a SaaS app such as WorkDay.</span></span> <span data-ttu-id="34b90-124">El propietario del recurso asigna al grupo para proporcionar acceso al recurso y el origen externo administra a los miembros del grupo.</span><span class="sxs-lookup"><span data-stu-id="34b90-124">The resource owner assigns the group to provide access to the resource, and the external source manages the members of the group.</span></span>

   ![Información general del diagrama de administración del acceso](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a><span data-ttu-id="34b90-126">Vea un vídeo que explica la administración del acceso</span><span class="sxs-lookup"><span data-stu-id="34b90-126">Watch a video that explains access management</span></span>
<span data-ttu-id="34b90-127">Puede ver un breve vídeo que explica más detalladamente este tema:</span><span class="sxs-lookup"><span data-stu-id="34b90-127">You can watch a short video that explains more about this:</span></span>

<span data-ttu-id="34b90-128">**Azure AD: Introducción a las pertenencias dinámicas para grupos**</span><span class="sxs-lookup"><span data-stu-id="34b90-128">**Azure AD: Introduction to dynamic membership for groups**</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a><span data-ttu-id="34b90-129">¿Cómo funciona la administración de acceso en Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34b90-129">How does access management in Azure Active Directory work?</span></span>
<span data-ttu-id="34b90-130">En el centro de la solución de administración de acceso de Azure AD se encuentra el grupo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="34b90-130">At the center of the Azure AD access management solution is the security group.</span></span> <span data-ttu-id="34b90-131">Usar un grupo de seguridad para administrar el acceso a los recursos es un paradigma conocido, lo que permite contar con una forma flexible y fácil de entender de proporcionar acceso a un recurso para el grupo de usuarios previsto.</span><span class="sxs-lookup"><span data-stu-id="34b90-131">Using a security group to manage access to resources is a well-known paradigm, which allows for a flexible and easily understood way to provide access to a resource for the intended group of users.</span></span> <span data-ttu-id="34b90-132">El propietario de los recursos (o el administrador del directorio) puede asignar un grupo para proporcionar determinados derechos de acceso a los recursos que posee.</span><span class="sxs-lookup"><span data-stu-id="34b90-132">The resource owner (or the administrator of the directory) can assign a group to provide a certain access right to the resources they own.</span></span> <span data-ttu-id="34b90-133">Los miembros del grupo recibirán el derecho de acceso y el propietario del recurso puede delegar en otra persona el derecho de administrar la lista de miembros de un grupo, por ejemplo, un administrador de departamento o un administrador de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="34b90-133">The members of the group will be provided the access, and the resource owner can delegate the right to manage the members list of a group to someone else, such as a department manager or a helpdesk administrator.</span></span>

![Diagrama de administración de acceso de Azure Active Directory](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

<span data-ttu-id="34b90-135">El propietario de un grupo también puede hacer que ese grupo esté disponible para solicitudes de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="34b90-135">The owner of a group can also make that group available for self-service requests.</span></span> <span data-ttu-id="34b90-136">De esta forma, un usuario final puede buscar y encontrar el grupo, y solicitar unirse a él pidiendo efectivamente permiso para tener acceso a los recursos que se administran a través del grupo.</span><span class="sxs-lookup"><span data-stu-id="34b90-136">In doing so, an end user can search for and find the group and make a request to join, effectively seeking permission to access the resources that are managed through the group.</span></span> <span data-ttu-id="34b90-137">El propietario del grupo puede configurar el grupo para que las solicitudes de pertenencia se aprueben automáticamente o requieran la aprobación por parte del propietario del grupo.</span><span class="sxs-lookup"><span data-stu-id="34b90-137">The owner of the group can set up the group so that join requests are approved automatically or require approval by the owner of the group.</span></span> <span data-ttu-id="34b90-138">Cuando un usuario realiza una solicitud para unirse a un grupo, la solicitud de pertenencia se reenvía a los propietarios del grupo.</span><span class="sxs-lookup"><span data-stu-id="34b90-138">When a user makes a request to join a group, the join request is forwarded to the owners of the group.</span></span> <span data-ttu-id="34b90-139">Si uno de los propietarios aprueba la solicitud, el usuario solicitante recibe una notificación y se une al grupo.</span><span class="sxs-lookup"><span data-stu-id="34b90-139">If one of the owners approves the request, the requesting user is notified and the user is joined to the group.</span></span> <span data-ttu-id="34b90-140">Si uno de los propietarios rechaza la solicitud, el usuario solicitante recibe una notificación pero no se une al grupo.</span><span class="sxs-lookup"><span data-stu-id="34b90-140">If one of the owners denies the request, the requesting user is notified but not joined to the group.</span></span>

## <a name="getting-started-with-access-management"></a><span data-ttu-id="34b90-141">Introducción a administración de accesos</span><span class="sxs-lookup"><span data-stu-id="34b90-141">Getting started with access management</span></span>
<span data-ttu-id="34b90-142">¿Ya está listo para comenzar?</span><span class="sxs-lookup"><span data-stu-id="34b90-142">Ready to get started?</span></span> <span data-ttu-id="34b90-143">Pruebe algunas de las tareas básicas que se pueden hacer con los grupos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34b90-143">You should try out some of the basic tasks you can do with Azure AD groups.</span></span> <span data-ttu-id="34b90-144">Utilice estas capacidades para proporcionar acceso especializado a distintos grupos de personas para los diferentes recursos de la organización.</span><span class="sxs-lookup"><span data-stu-id="34b90-144">Use these capabilities to provide specialized access to different groups of people for different resources in your organization.</span></span> <span data-ttu-id="34b90-145">A continuación se incluye una lista de los primeros pasos básicos.</span><span class="sxs-lookup"><span data-stu-id="34b90-145">A list of basic first steps are listed below.</span></span>

* [<span data-ttu-id="34b90-146">Crear una regla sencilla para configurar pertenencias dinámicas a un grupo</span><span class="sxs-lookup"><span data-stu-id="34b90-146">Creating a simple rule to configure dynamic memberships for a group</span></span>](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [<span data-ttu-id="34b90-147">Uso de un grupo para administrar el acceso a las aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="34b90-147">Using a group to manage access to SaaS applications</span></span>](active-directory-accessmanagement-group-saasapps.md)
* [<span data-ttu-id="34b90-148">Puesta a disposición de un grupo para el autoservicio del usuario final</span><span class="sxs-lookup"><span data-stu-id="34b90-148">Making a group available for end user self-service</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* [<span data-ttu-id="34b90-149">Sincronización de un grupo local con Azure mediante Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="34b90-149">Syncing an on-premises group to Azure using Azure AD Connect</span></span>](active-directory-aadconnect.md)
* [<span data-ttu-id="34b90-150">Administración de propietarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="34b90-150">Managing owners for a group</span></span>](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a><span data-ttu-id="34b90-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34b90-151">Next steps</span></span>
<span data-ttu-id="34b90-152">Ahora que ha comprendido los conceptos básicos de la administración de accesos, presentamos algunas capacidades avanzadas adicionales disponibles en Azure Active Directory para administrar el acceso a sus aplicaciones y recursos.</span><span class="sxs-lookup"><span data-stu-id="34b90-152">Now that you have understood the basics of access management, here are some additional advanced capabilities available in Azure Active Directory for managing access to your applications and resources.</span></span>

* [<span data-ttu-id="34b90-153">Uso de atributos para crear reglas avanzadas</span><span class="sxs-lookup"><span data-stu-id="34b90-153">Using attributes to create advanced rules</span></span>](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [<span data-ttu-id="34b90-154">Administración de grupos de seguridad en Azure AD</span><span class="sxs-lookup"><span data-stu-id="34b90-154">Managing security groups in Azure AD</span></span>](active-directory-accessmanagement-manage-groups.md)
* [<span data-ttu-id="34b90-155">Configuración de grupos dedicados en Azure AD</span><span class="sxs-lookup"><span data-stu-id="34b90-155">Setting up dedicated groups in Azure AD</span></span>](active-directory-accessmanagement-dedicated-groups.md)
* [<span data-ttu-id="34b90-156">Referencia de API Graph para grupos</span><span class="sxs-lookup"><span data-stu-id="34b90-156">Graph API reference for groups</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [<span data-ttu-id="34b90-157">Cmdlets de Azure Active Directory para configurar las opciones de grupo</span><span class="sxs-lookup"><span data-stu-id="34b90-157">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)