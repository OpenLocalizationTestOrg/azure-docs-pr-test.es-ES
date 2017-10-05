---
title: Uso de un grupo para administrar el acceso a aplicaciones SaaS| Microsoft Docs
description: "Cómo usar grupos en Azure Active Directory Premium o Basic para asignar el acceso a aplicaciones SaaS integradas con Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="1769f-103">Uso de un grupo para administrar el acceso a las aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="1769f-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="1769f-104">Con Azure Active Directory (Azure AD) y una licencia de Azure AD Premium o Azure AD Basic, puede usar grupos para asignar el acceso a una aplicación SaaS integrada con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1769f-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="1769f-105">Por ejemplo, si desea asignar acceso al departamento de marketing para utilizar cinco aplicaciones SaaS diferentes, puede crear un grupo que contenga a los usuarios del departamento de marketing y, a continuación, asignar ese grupo a las cinco aplicaciones SaaS requeridas por el departamento de marketing.</span><span class="sxs-lookup"><span data-stu-id="1769f-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="1769f-106">De este modo, ahorrará tiempo administrando la pertenencia a grupos del departamento de marketing en un solo lugar.</span><span class="sxs-lookup"><span data-stu-id="1769f-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="1769f-107">A continuación, los usuarios se asignan a la aplicación cuando se agregan como miembros del grupo de marketing, y se eliminan sus asignaciones de la aplicación cuando se eliminan del grupo de marketing.</span><span class="sxs-lookup"><span data-stu-id="1769f-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1769f-108">Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1769f-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="1769f-109">Esta función se puede utilizar con cientos de aplicaciones que puede agregar desde la Galería de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1769f-109">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="1769f-110">**Para asignar acceso para un grupo a una aplicación SaaS**</span><span class="sxs-lookup"><span data-stu-id="1769f-110">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="1769f-111">En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory** en la barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="1769f-111">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="1769f-112">Seleccione la pestaña **Directorio** y abra el directorio en el que desea asignar el acceso para un grupo a una aplicación SaaS.</span><span class="sxs-lookup"><span data-stu-id="1769f-112">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="1769f-113">Seleccione la pestaña **Aplicaciones** . Seleccione una aplicación que haya agregado desde la Galería de aplicaciones y haga clic en la pestaña **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1769f-113">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="1769f-114">En la pestaña **Usuarios y grupos**, en el campo **Empezando por**, escriba el nombre del grupo al que desea asignar acceso y seleccione la marca de verificación en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="1769f-114">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="1769f-115">Solo necesita escribir la primera parte del nombre de un grupo.</span><span class="sxs-lookup"><span data-stu-id="1769f-115">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="1769f-116">Seleccione el grupo y luego seleccione el botón **Asignar acceso** .</span><span class="sxs-lookup"><span data-stu-id="1769f-116">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="1769f-117">Seleccione **Sí** cuando aparezca el mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="1769f-117">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="1769f-118">No se admiten las pertenencias a grupos anidadas para la asignación basada en grupos a aplicaciones en este momento.</span><span class="sxs-lookup"><span data-stu-id="1769f-118">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="1769f-119">También puede ver qué usuarios están asignados a la aplicación, directamente o mediante la pertenencia a un grupo.</span><span class="sxs-lookup"><span data-stu-id="1769f-119">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="1769f-120">Para ello, cambie la opción **Mostrar lista desplegable de "Grupos"** a **"Todos los usuarios"**.</span><span class="sxs-lookup"><span data-stu-id="1769f-120">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="1769f-121">La lista muestra los usuarios en el directorio y si cada uno de ellos está asignado o no a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1769f-121">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="1769f-122">La lista también muestra si los usuarios asignados están asignados a la aplicación directamente (el tipo de asignación aparece como "Directo"), o en virtud de la pertenencia a un grupo (el tipo de asignación aparece como "Heredado").</span><span class="sxs-lookup"><span data-stu-id="1769f-122">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="1769f-123">Solo después de habilitar Azure AD Premium o Azure AD Basic verá la pestaña Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="1769f-123">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="1769f-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1769f-124">Next steps</span></span>
<span data-ttu-id="1769f-125">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1769f-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="1769f-126">Administración del acceso a los recursos con grupos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1769f-126">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="1769f-127">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1769f-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="1769f-128">Cmdlets de Azure Active Directory para configurar las opciones de grupo</span><span class="sxs-lookup"><span data-stu-id="1769f-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="1769f-129">¿Qué es Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1769f-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="1769f-130">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1769f-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
