---
title: grupos de aaaDedicated en Active Directory de Azure | Documentos de Microsoft
description: "Información general sobre cómo funcionan los grupos específicos en Azure Active Directory y cómo se crean."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="c1234-103">Grupos dedicados en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1234-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="c1234-104">En Azure Active Directory (Azure AD), la característica de grupos dedicados Hola crea y rellena automáticamente la pertenencia a grupos de Azure AD predefinido.</span><span class="sxs-lookup"><span data-stu-id="c1234-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="c1234-105">No se puede agregar los miembros de grupos dedicados o quiten con hello Azure clásico portal, cmdlets de Windows PowerShell, o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="c1234-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="c1234-106">Los grupos dedicados requieren que se asigne una licencia de Azure AD Premium:</span><span class="sxs-lookup"><span data-stu-id="c1234-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="c1234-107">Administrador de Hola que administra la regla de hello en un grupo</span><span class="sxs-lookup"><span data-stu-id="c1234-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="c1234-108">todos los usuarios que están seleccionados de forma Hola regla toobe un miembro del grupo de Hola</span><span class="sxs-lookup"><span data-stu-id="c1234-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="c1234-109">**grupos de tooenable dedicado**</span><span class="sxs-lookup"><span data-stu-id="c1234-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="c1234-110">Hola [portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, a continuación, abra el directorio de su organización.</span><span class="sxs-lookup"><span data-stu-id="c1234-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="c1234-111">Seleccione hello **grupos** ficha y un grupo de hello, a continuación, abra desea tooedit.</span><span class="sxs-lookup"><span data-stu-id="c1234-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="c1234-112">Seleccione hello **configurar** ficha y, a continuación, establezca **habilitar grupos dedicados** demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="c1234-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="c1234-113">Una vez Hola cambiar habilitar grupos dedicados se establece demasiado**Sí**, también puede habilitar Hola directory tooautomatically crear grupo dedicado de todos los usuarios de Hola Hola establecer **habilitar "Todos los usuarios" grupo** cambiar demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="c1234-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="c1234-114">También puede, a continuación, Editar nombre de Hola de este grupo dedicado escribiendo en hello **nombre para mostrar "Todos los usuarios" grupo** campo.</span><span class="sxs-lookup"><span data-stu-id="c1234-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="c1234-115">puede utilizarse el grupo de todos los usuarios de Hello tooassign Hola mismo permisos tooall Hola usuarios del directorio.</span><span class="sxs-lookup"><span data-stu-id="c1234-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="c1234-116">Por ejemplo, puede conceder todos los usuarios en su tooa de acceso de directorio aplicación SaaS mediante la asignación de acceso para todos los usuarios grupo dedicado toothis aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c1234-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="c1234-117">grupo de todos los usuarios de Hello dedicado incluye todos los usuarios en el directorio de hello, incluidos invitados y usuarios externos.</span><span class="sxs-lookup"><span data-stu-id="c1234-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="c1234-118">Si necesita un grupo que excluye los usuarios externos, puede hacerlo mediante la creación de un grupo con una regla dinámica basada en atributos como siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="c1234-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="c1234-119">Para un grupo que excluye a todos los invitados, use una regla como siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="c1234-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="c1234-120">toolearn acerca de cómo toocreate *avanzadas* (reglas que puede contener varias comparaciones) para la pertenencia dinámica a grupos, consulte [utilizando atributos toocreate reglas avanzadas](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="c1234-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="c1234-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1234-121">Next steps</span></span>
<span data-ttu-id="c1234-122">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1234-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c1234-123">Administrar acceso tooresources con grupos de Active Directory de Azure</span><span class="sxs-lookup"><span data-stu-id="c1234-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="c1234-124">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1234-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c1234-125">¿Qué es Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c1234-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="c1234-126">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1234-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
