---
title: aaaUsing un tooSaaS de acceso de toomanage aplicaciones de grupo | Documentos de Microsoft
description: "Cómo toouse grupos en Azure Active Directory Premium o básica tooassign tener acceso a las aplicaciones de tooSaaS que se integran con Azure Active Directory."
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
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="d714a-103">Uso de un grupo toomanage acceso tooSaaS las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d714a-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="d714a-104">Con Azure Active Directory (Azure AD) con una licencia de Azure AD Premium o Azure AD Basic, puede usar grupos tooassign acceso tooa aplicación SaaS que está integrado con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d714a-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="d714a-105">Por ejemplo, si desea tener acceso de tooassign para hello marketing departamento toouse cinco aplicaciones SaaS diferentes, puede crear un grupo que contenga los usuarios de Hola Hola departamento de marketing y, a continuación, asignar ese grupo toothese cinco aplicaciones SaaS que son necesario para el departamento de marketing de Hola.</span><span class="sxs-lookup"><span data-stu-id="d714a-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="d714a-106">Este modo ahorrará tiempo debido a que administra la pertenencia de Hola de hello departamento de marketing de un solo lugar.</span><span class="sxs-lookup"><span data-stu-id="d714a-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="d714a-107">Los usuarios, a continuación, se asignan toohello aplicación cuando se agregan como miembros del grupo de marketing de Hola y se eliminan sus asignaciones de la aplicación hello cuando se quitan del grupo de marketing de Hola.</span><span class="sxs-lookup"><span data-stu-id="d714a-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d714a-108">Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="d714a-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="d714a-109">Esta capacidad se puede utilizar con cientos de aplicaciones que pueden agregar desde Hola Galería de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d714a-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="d714a-110">**acceso de tooassign para una aplicación SaaS tooa de grupo**</span><span class="sxs-lookup"><span data-stu-id="d714a-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="d714a-111">Hola [portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory** en la barra de navegación de hello en hello del lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="d714a-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="d714a-112">Seleccione hello **Directory** ficha y directorio de hello, a continuación, abrir en el que desee tooassign acceso para una aplicación SaaS tooa de grupo.</span><span class="sxs-lookup"><span data-stu-id="d714a-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="d714a-113">Seleccione hello **aplicaciones** ficha. Seleccione una aplicación que ha agregado Hola Galería de aplicaciones y, a continuación, haga clic en hello **usuarios y grupos** ficha.</span><span class="sxs-lookup"><span data-stu-id="d714a-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="d714a-114">En hello **usuarios y grupos** ficha Hola **a partir de** , escriba el nombre de Hola de hello grupo toowhich desea acceso tooassign, y, a continuación, seleccione Hola marca de verificación en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="d714a-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="d714a-115">Solo necesita primera parte del nombre de un grupo de Hola de tootype.</span><span class="sxs-lookup"><span data-stu-id="d714a-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="d714a-116">Seleccione el grupo de hello y, a continuación, seleccione hello **asignar acceso** botón.</span><span class="sxs-lookup"><span data-stu-id="d714a-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="d714a-117">Seleccione **Sí** cuando aparezca el mensaje de confirmación de saludo.</span><span class="sxs-lookup"><span data-stu-id="d714a-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="d714a-118">Las pertenencias a grupos anidados no se admiten para la asignación basada en el grupo tooapplications en este momento.</span><span class="sxs-lookup"><span data-stu-id="d714a-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="d714a-119">También puede ver qué usuarios están asignados toohello aplicación, ya sea directamente o por la pertenencia a un grupo.</span><span class="sxs-lookup"><span data-stu-id="d714a-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="d714a-120">toodo, Hola cambio **mostrar el cuadro desplegable de 'Grupos'** demasiado**'Todos los usuarios'**.</span><span class="sxs-lookup"><span data-stu-id="d714a-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="d714a-121">Hola lista muestra los usuarios directory hello y si no se asigne a cada usuario toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="d714a-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="d714a-122">lista de Hello también muestra si los usuarios de hello asignado se asignan toohello aplicación directamente (tipo de asignación mostrado como 'Directa'), o en virtud de la pertenencia a grupos (tipo de asignación mostrado como 'Heredado'.)</span><span class="sxs-lookup"><span data-stu-id="d714a-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="d714a-123">Puede ver Hola a los usuarios y ficha grupos sólo después de haber habilitado Azure AD Premium o básica de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d714a-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="d714a-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d714a-124">Next steps</span></span>
<span data-ttu-id="d714a-125">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d714a-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="d714a-126">Administrar acceso tooresources con grupos de Active Directory de Azure</span><span class="sxs-lookup"><span data-stu-id="d714a-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="d714a-127">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d714a-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d714a-128">Cmdlets de Azure Active Directory para configurar las opciones de grupo</span><span class="sxs-lookup"><span data-stu-id="d714a-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="d714a-129">¿Qué es Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d714a-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="d714a-130">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d714a-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
