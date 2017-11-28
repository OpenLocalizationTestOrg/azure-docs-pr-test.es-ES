---
title: Grupos dedicados en Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="578da-103">Grupos dedicados en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="578da-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="578da-104">En Azure Active Directory (Azure AD), la característica de grupos dedicados crea y rellena automáticamente la pertenencia para grupos predefinidos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="578da-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="578da-105">No es posible agregar ni quitar miembros de grupos dedicados mediante el Portal de Azure clásico, los cmdlets de Windows PowerShell o de manera programática.</span><span class="sxs-lookup"><span data-stu-id="578da-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="578da-106">Los grupos dedicados requieren que se asigne una licencia de Azure AD Premium:</span><span class="sxs-lookup"><span data-stu-id="578da-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="578da-107">Al administrador que administra la regla en un grupo</span><span class="sxs-lookup"><span data-stu-id="578da-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="578da-108">A todos los usuarios que la regla selecciona para que sean miembros del grupo</span><span class="sxs-lookup"><span data-stu-id="578da-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="578da-109">**Para habilitar los grupos dedicados**</span><span class="sxs-lookup"><span data-stu-id="578da-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="578da-110">En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y luego abra el directorio de su organización.</span><span class="sxs-lookup"><span data-stu-id="578da-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="578da-111">Seleccione la pestaña **Grupos** y abra el grupo que desea editar.</span><span class="sxs-lookup"><span data-stu-id="578da-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="578da-112">Seleccione la pestaña **Configurar** y en **Habilitar grupos dedicados**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="578da-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="578da-113">Una vez que en Habilitar grupos dedicados se selecciona **Sí**, se puede habilitar el directorio para que cree automáticamente el grupo dedicado Todos los usuarios, para lo que en **Habilitar grupo " Todos los usuarios"** es preciso seleccionar **Sí**.</span><span class="sxs-lookup"><span data-stu-id="578da-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="578da-114">También puede editar el nombre de este grupo dedicado; para ello, escríbalo en el campo **Nombre para mostrar del grupo “**Todos los usuarios**”** .</span><span class="sxs-lookup"><span data-stu-id="578da-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="578da-115">El grupo Todos los usuarios puede usarse para asignar los mismos permisos a todos los usuarios del directorio.</span><span class="sxs-lookup"><span data-stu-id="578da-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="578da-116">Por ejemplo, puede otorgar a todos los usuarios del directorio acceso a una aplicación SaaS si asigna acceso a esta aplicación para el grupo dedicado Todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="578da-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="578da-117">El grupo dedicado Todos los usuarios incluye a todos los usuarios del directorio, incluidos los invitados y los usuarios externos.</span><span class="sxs-lookup"><span data-stu-id="578da-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="578da-118">Si necesita un grupo que excluya a los usuarios externos, puede crear un grupo con una regla dinámica basada en atributos, como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="578da-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="578da-119">Para crear un grupo que excluya a todos los invitados, use una regla como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="578da-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="578da-120">Para obtener información acerca de cómo crear reglas *avanzadas* (reglas que pueden contener comparaciones múltiples) para la pertenencia a grupos dinámicos, consulte [Uso de atributos para crear reglas avanzadas](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="578da-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="578da-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="578da-121">Next steps</span></span>
<span data-ttu-id="578da-122">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="578da-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="578da-123">Administración del acceso a los recursos con grupos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="578da-123">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="578da-124">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="578da-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="578da-125">¿Qué es Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="578da-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="578da-126">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="578da-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
