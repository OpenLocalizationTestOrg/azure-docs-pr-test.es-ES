---
title: "Pasos siguientes para la administración de acceso mediante grupos | Microsoft Docs"
description: Procedimientos avanzados para administrar grupos de seguridad y uso de estos grupos para administrar el acceso a un recurso.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="e3678-103">Administración de propietarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="e3678-103">Managing owners for a group</span></span>
<span data-ttu-id="e3678-104">Una vez que un propietario de recursos haya asignado acceso a un recurso a un grupo de Azure AD, el propietario del grupo será quien administre los miembros del grupo.</span><span class="sxs-lookup"><span data-stu-id="e3678-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="e3678-105">El propietario del recursos delega de manera eficaz el permiso para asignar usuarios al recurso al propietario del grupo.</span><span class="sxs-lookup"><span data-stu-id="e3678-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3678-106">Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e3678-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="e3678-107">Asignación de la propiedad de un grupo</span><span class="sxs-lookup"><span data-stu-id="e3678-107">Assigning group ownership</span></span>
<span data-ttu-id="e3678-108">**Para agregar un propietario a un grupo**</span><span class="sxs-lookup"><span data-stu-id="e3678-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="e3678-109">En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y luego abra el directorio de su organización.</span><span class="sxs-lookup"><span data-stu-id="e3678-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="e3678-110">Seleccione la pestaña **Grupos** y abra el grupo al que desea agregar propietarios.</span><span class="sxs-lookup"><span data-stu-id="e3678-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="e3678-111">Seleccione **Agregar propietarios**.</span><span class="sxs-lookup"><span data-stu-id="e3678-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="e3678-112">En la página **Agregar propietarios**, seleccione el usuario que desea agregar como propietario del grupo y asegúrese de que este nombre se agrega al panel **Seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="e3678-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="e3678-113">**Para quitar un propietario de un grupo**</span><span class="sxs-lookup"><span data-stu-id="e3678-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="e3678-114">En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y luego abra el directorio de su organización.</span><span class="sxs-lookup"><span data-stu-id="e3678-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="e3678-115">Seleccione la pestaña **Grupos** y abra el grupo del que desea quitar un propietario.</span><span class="sxs-lookup"><span data-stu-id="e3678-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="e3678-116">Seleccione la pestaña **Propietarios** .</span><span class="sxs-lookup"><span data-stu-id="e3678-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="e3678-117">Seleccione el propietario que desea quitar del grupo y luego seleccione **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="e3678-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="e3678-118">Información adicional</span><span class="sxs-lookup"><span data-stu-id="e3678-118">Additional information</span></span>
<span data-ttu-id="e3678-119">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e3678-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e3678-120">Administración del acceso a los recursos con grupos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3678-120">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="e3678-121">Cmdlets de Azure Active Directory para configurar las opciones de grupo</span><span class="sxs-lookup"><span data-stu-id="e3678-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="e3678-122">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3678-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="e3678-123">¿Qué es Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e3678-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="e3678-124">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3678-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
