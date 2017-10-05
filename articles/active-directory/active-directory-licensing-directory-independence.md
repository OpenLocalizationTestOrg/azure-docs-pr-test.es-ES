---
title: "Características de la interacción de inquilinos de Azure Active Directory | Microsoft Docs"
description: "Administre sus inquilinos de Azure Active Directory considerándolos como recursos completamente independientes."
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: d25d2c731034d0785bbd404ec693c4c41d913d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="40d19-103">Información de cómo interactúan varios inquilinos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40d19-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="40d19-104">En Azure Active Directory (Azure AD), cada inquilino es un recurso totalmente independiente: un recurso del mismo nivel, que es lógicamente independiente de otros inquilinos que administre.</span><span class="sxs-lookup"><span data-stu-id="40d19-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="40d19-105">No hay ninguna relación de elementos primarios y secundarios entre los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="40d19-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="40d19-106">Esta independencia entre inquilinos incluye la de los recursos, la independencia administrativa y la de sincronización.</span><span class="sxs-lookup"><span data-stu-id="40d19-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="40d19-107">Independencia de recursos</span><span class="sxs-lookup"><span data-stu-id="40d19-107">Resource independence</span></span>
* <span data-ttu-id="40d19-108">Si crea o elimina un recurso en un inquilino, no tiene efecto en ningún recurso de los demás inquilinos, con la excepción parcial de los usuarios externos.</span><span class="sxs-lookup"><span data-stu-id="40d19-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="40d19-109">Si usa uno de los nombres de dominio con un inquilino, no se puede usar con ningún otro.</span><span class="sxs-lookup"><span data-stu-id="40d19-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="40d19-110">Independencia administrativa</span><span class="sxs-lookup"><span data-stu-id="40d19-110">Administrative independence</span></span>
<span data-ttu-id="40d19-111">Si un usuario no administrador del inquilino "Contoso" crea un directorio de prueba "Prueba", en ese caso:</span><span class="sxs-lookup"><span data-stu-id="40d19-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="40d19-112">De forma predeterminada, el usuario que crea un inquilino se agrega como un usuario externo en ese nuevo inquilino y se le asigna el rol de administrador global en ese inquilino.</span><span class="sxs-lookup"><span data-stu-id="40d19-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="40d19-113">Los administradores del inquilino "Contoso" no tienen privilegios administrativos directos en el inquilino "Prueba", a menos que el administrador de "Prueba" se los otorgue específicamente.</span><span class="sxs-lookup"><span data-stu-id="40d19-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="40d19-114">Sin embargo, los administradores de "Contoso" pueden controlar el acceso al inquilino "Prueba" si controlan la cuenta de usuario que creó "Prueba".</span><span class="sxs-lookup"><span data-stu-id="40d19-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="40d19-115">Si se agrega o quita un rol de administrador para un usuario en un inquilino, el cambio no afecta a los roles de administrador que tenga el usuario en otro inquilino.</span><span class="sxs-lookup"><span data-stu-id="40d19-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="40d19-116">Independencia de sincronización</span><span class="sxs-lookup"><span data-stu-id="40d19-116">Synchronization independence</span></span>
<span data-ttu-id="40d19-117">Puede configurar cada inquilino de Azure AD de manera independiente para que los datos se sincronicen desde una sola instancia de:</span><span class="sxs-lookup"><span data-stu-id="40d19-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="40d19-118">La herramienta Azure AD Connect, para sincronizar los datos con un único bosque de AD.</span><span class="sxs-lookup"><span data-stu-id="40d19-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="40d19-119">El conector de inquilinos de Azure Active Directory para Forefront Identity Manager, para sincronizar datos con uno o varios bosques locales u orígenes de datos distintos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40d19-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="40d19-120">Adición de un inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="40d19-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="40d19-121">Para agregar un inquilino de Azure AD en Azure Portal, inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que sea un administrador global de Azure AD y, a la izquierda, seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="40d19-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="40d19-122">A diferencia de otros recursos de Azure, los inquilinos no son recursos secundarios de una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="40d19-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="40d19-123">Si su suscripción a Azure se cancela o expira, aún podrá tener acceso a los datos de su inquilino mediante Azure PowerShell, Azure Graph API o el Centro de administración de Office 365.</span><span class="sxs-lookup"><span data-stu-id="40d19-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="40d19-124">También puede asociar otra suscripción al inquilino.</span><span class="sxs-lookup"><span data-stu-id="40d19-124">You can also associate another subscription with the tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="40d19-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="40d19-125">Next steps</span></span>
<span data-ttu-id="40d19-126">Para obtener una amplia visión general de los problemas de licencias de Azure AD y prácticas recomendadas, consulte [¿Qué es la licencia de inquilinos de Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="40d19-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
