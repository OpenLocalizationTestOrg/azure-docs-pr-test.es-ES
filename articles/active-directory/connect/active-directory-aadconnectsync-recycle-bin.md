---
title: "Azure AD Connect Sync: Habilitación de la papelera de reciclaje de AD | Microsoft Docs"
description: "En este tema, se recomienda el uso de la característica Papelera de reciclaje de AD con Azure AD Connect."
services: active-directory
keywords: "Papelera de reciclaje de AD, eliminación accidental, sourceAnchor"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: eb455477547f3db8245cf3601576eba9c6fdc56f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="83ddd-104">Azure AD Connect Sync: Habilitación de la papelera de reciclaje de AD</span><span class="sxs-lookup"><span data-stu-id="83ddd-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="83ddd-105">Se recomienda que habilite la característica Papelera de reciclaje de AD en sus instancias locales de Active Directory, que se sincronizan con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83ddd-105">It is recommended that you enable the AD Recycle Bin feature for your on-premises Active Directories, which are synchronized to Azure AD.</span></span> 

<span data-ttu-id="83ddd-106">Si ha eliminado accidentalmente un objeto de usuario local de AD y lo restaura con esta característica, Azure AD restaura el objeto de usuario de Azure AD correspondiente.</span><span class="sxs-lookup"><span data-stu-id="83ddd-106">If you accidentally deleted an on-premises AD user object and restore it using the feature, Azure AD restores the corresponding Azure AD user object.</span></span>  <span data-ttu-id="83ddd-107">Para más información acerca de la característica Papelera de reciclaje de AD, consulte el artículo [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx) (Información general sobre el escenario de restauración de objetos de Active Directory eliminados).</span><span class="sxs-lookup"><span data-stu-id="83ddd-107">For information about the AD Recycle Bin feature, refer to article [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-the-ad-recycle-bin"></a><span data-ttu-id="83ddd-108">Ventajas de habilitar la Papelera de reciclaje de AD</span><span class="sxs-lookup"><span data-stu-id="83ddd-108">Benefits of enabling the AD recycle bin</span></span>
<span data-ttu-id="83ddd-109">Esta característica ayuda a restaurar objetos de usuario de Azure AD mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="83ddd-109">This feature helps with restoring Azure AD user objects by doing the following:</span></span>

* <span data-ttu-id="83ddd-110">Si ha eliminado accidentalmente un objeto de usuario de una implementación de AD local, se eliminará el objeto de usuario de Azure AD correspondiente en el siguiente ciclo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="83ddd-110">If you accidentally deleted an on-premises AD user object, the corresponding Azure AD user object will be deleted in the next sync cycle.</span></span> <span data-ttu-id="83ddd-111">De forma predeterminada, Azure AD mantiene el objeto de usuario de Azure AD eliminado en estado de eliminación temporal durante 30 días.</span><span class="sxs-lookup"><span data-stu-id="83ddd-111">By default, Azure AD keeps the deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="83ddd-112">Si tiene habilitada la característica Papelera de reciclaje de su instancia local de AD, puede restaurar el objeto de usuario de su instancia de AD local sin cambiar el valor de sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="83ddd-112">If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="83ddd-113">Cuando el objeto de usuario de la instancia de AD local recuperado se sincroniza con Azure AD, Azure AD restaurará el objeto correspondiente de usuario de Azure AD en estado de eliminación temporal.</span><span class="sxs-lookup"><span data-stu-id="83ddd-113">When the recovered on-premises AD user object is synchronized to Azure AD, Azure AD will restore the corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="83ddd-114">Para más información sobre el atributo sourceAnchor, consulte el artículo [Azure AD Connect: conceptos de diseño](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="83ddd-114">For information about Source Anchor attribute, refer to article [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="83ddd-115">Si no tiene habilitada la característica Papelera de reciclaje de su instancia de AD local, será necesario crear un objeto de usuario de AD para reemplazar el objeto eliminado.</span><span class="sxs-lookup"><span data-stu-id="83ddd-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object.</span></span> <span data-ttu-id="83ddd-116">Si Azure AD Connect Synchronization Service está configurado para usar un atributo de AD generado por el sistema (por ejemplo, ObjectGuid) para el atributo sourceAnchor, el objeto de usuario de AD recién creado no tendrá el mismo valor de sourceAnchor que el objeto de usuario de AD eliminado.</span><span class="sxs-lookup"><span data-stu-id="83ddd-116">If Azure AD Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object will not have the same Source Anchor value as the deleted AD user object.</span></span> <span data-ttu-id="83ddd-117">Cuando el objeto de usuario de AD recién creado se sincroniza con Azure AD, Azure AD crea un nuevo objeto de usuario de Azure AD en lugar de restaurar el objeto de usuario de Azure AD en estado de eliminación temporal.</span><span class="sxs-lookup"><span data-stu-id="83ddd-117">When the newly created AD user object is synchronized to Azure AD, Azure AD creates a new Azure AD user object instead of restoring the soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="83ddd-118">De forma predeterminada, Azure AD mantiene los objetos de usuario de Azure AD eliminados en estado de eliminación temporal durante 30 días antes de eliminarlos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="83ddd-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="83ddd-119">Sin embargo, los administradores pueden acelerar la eliminación de dichos objetos.</span><span class="sxs-lookup"><span data-stu-id="83ddd-119">However, administrators can accelerate the deletion of such objects.</span></span> <span data-ttu-id="83ddd-120">Una vez que los objetos se eliminan permanentemente, ya no se puedan recuperar, aunque esté habilitada la característica Papelera de reciclaje de la instancia de AD local.</span><span class="sxs-lookup"><span data-stu-id="83ddd-120">Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="83ddd-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="83ddd-121">Next steps</span></span>
<span data-ttu-id="83ddd-122">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="83ddd-122">**Overview topics**</span></span>

* [<span data-ttu-id="83ddd-123">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="83ddd-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="83ddd-124">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83ddd-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
