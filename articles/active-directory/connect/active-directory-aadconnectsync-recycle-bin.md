---
title: "Azure AD Connect Sync: Habilitación de la papelera de reciclaje de AD | Microsoft Docs"
description: "En este tema recomienda el uso de Hola de característica de Papelera de reciclaje de AD con Azure AD Connect."
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
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="743d4-104">Azure AD Connect Sync: Habilitación de la papelera de reciclaje de AD</span><span class="sxs-lookup"><span data-stu-id="743d4-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="743d4-105">Se recomienda habilitar característica de Papelera de reciclaje de hello AD para los directorios Active local, que son tooAzure sincronizada AD.</span><span class="sxs-lookup"><span data-stu-id="743d4-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="743d4-106">Si ha eliminado accidentalmente una implementación local objeto de usuario de AD y restauración mediante la característica de hello, Azure AD restaura objeto de usuario de Azure AD correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="743d4-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="743d4-107">Para obtener información acerca de la característica de Papelera de reciclaje de hello AD, consulte tooarticle [Introducción a los escenarios de restauración de eliminar objetos de Active Directory](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="743d4-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="743d4-108">Ventajas de la habilitación de hello AD Papelera de reciclaje</span><span class="sxs-lookup"><span data-stu-id="743d4-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="743d4-109">Esta característica ayuda a con la restauración de objetos de usuario de Azure AD mediante acciones Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="743d4-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="743d4-110">Si ha eliminado accidentalmente una implementación local objeto de usuario de AD, objeto de usuario de Azure AD correspondiente Hola se eliminará de hello siguiente ciclo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="743d4-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="743d4-111">De forma predeterminada, Azure AD mantiene el objeto de usuario de Azure AD Hola eliminado en estado eliminado durante 30 días.</span><span class="sxs-lookup"><span data-stu-id="743d4-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="743d4-112">Si tienes local habilitada la característica de Papelera de reciclaje de AD, puede restaurar Hola eliminado local objeto de usuario de Active Directory sin cambiar su valor de delimitador de origen.</span><span class="sxs-lookup"><span data-stu-id="743d4-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="743d4-113">Cuando Hola recuperado local se sincroniza el objeto de usuario de AD tooAzure AD, Azure AD restaurará Hola correspondiente eliminado objeto de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="743d4-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="743d4-114">Para obtener información sobre el atributo de delimitador de origen, consulte tooarticle [Azure AD Connect: conceptos de diseño](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="743d4-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="743d4-115">Si no tiene local habilitada la característica de Papelera de reciclaje de AD, es posible que toocreate requiere un objeto AD usuario objeto tooreplace Hola eliminado.</span><span class="sxs-lookup"><span data-stu-id="743d4-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="743d4-116">Si el servicio de sincronización de Connect de Azure AD toouse configurado generados por el sistema AD atributo (por ejemplo, ObjectGuid) para el atributo de delimitador de origen de hello, hello recién creado objetos de usuario de AD no habrá Hola mismo valor de delimitador de origen como Hola eliminado el objeto de usuario de AD.</span><span class="sxs-lookup"><span data-stu-id="743d4-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="743d4-117">Una vez hello recién creado objetos de usuario de AD tooAzure sincronizada AD, Azure AD crea un nuevo objeto de usuario de Azure AD en lugar de restaurar el objeto de usuario de Azure AD Hola eliminado.</span><span class="sxs-lookup"><span data-stu-id="743d4-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="743d4-118">De forma predeterminada, Azure AD mantiene los objetos de usuario de Azure AD eliminados en estado de eliminación temporal durante 30 días antes de eliminarlos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="743d4-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="743d4-119">Sin embargo, los administradores pueden acelerar la eliminación de Hola de dichos objetos.</span><span class="sxs-lookup"><span data-stu-id="743d4-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="743d4-120">Una vez que se eliminan permanentemente los objetos de hello, ya no se pueden recuperar, incluso si está habilitada la característica de Papelera de reciclaje de AD en local real.</span><span class="sxs-lookup"><span data-stu-id="743d4-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="743d4-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="743d4-121">Next steps</span></span>
<span data-ttu-id="743d4-122">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="743d4-122">**Overview topics**</span></span>

* [<span data-ttu-id="743d4-123">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="743d4-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="743d4-124">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="743d4-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
