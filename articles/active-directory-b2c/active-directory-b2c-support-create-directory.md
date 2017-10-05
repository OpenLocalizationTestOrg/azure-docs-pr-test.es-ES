---
title: "Azure Active Directory B2C: solución de problemas de creación de inquilinos | Microsoft Docs"
description: Problemas y soluciones a la hora de crear un inquilino de Azure Active Directory o de Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 81af4536fc223319369aff262d42149cfbf1a1e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="bcd0c-103">Solución de problemas a la hora de crear un inquilino de Azure Active Directory o de Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="bcd0c-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="bcd0c-104">Creación de un inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcd0c-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="bcd0c-105">Si no puede crear un inquilino de Azure Active Directory (Azure AD) en el primer intento, vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="bcd0c-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span></span> <span data-ttu-id="bcd0c-106">Si el problema persiste, póngase en contacto con el servicio de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd0c-106">If the problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="bcd0c-107">Creación de un inquilino de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bcd0c-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="bcd0c-108">Si detecta problemas al [crear un inquilino de Azure Active Directory B2C (Azure AD B2C)](active-directory-b2c-get-started.md), intente las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="bcd0c-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span></span>

* <span data-ttu-id="bcd0c-109">Si el inquilino de Azure AD B2C no aparece en la lista de inquilinos, vuelva a intentar crear el inquilino.</span><span class="sxs-lookup"><span data-stu-id="bcd0c-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span></span>
* <span data-ttu-id="bcd0c-110">Si el inquilino de Azure AD B2C aparece en la lista de inquilinos y ve el siguiente mensaje de error, elimine el inquilino y vuelva a crearlo:</span><span class="sxs-lookup"><span data-stu-id="bcd0c-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span></span>

    <span data-ttu-id="bcd0c-111">"No se pudo completar la creación del inquilino B2C "contosob2c".</span><span class="sxs-lookup"><span data-stu-id="bcd0c-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="bcd0c-112">Para obtener más ayuda, visite este [vínculo](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409)".</span><span class="sxs-lookup"><span data-stu-id="bcd0c-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="bcd0c-113">Existen problemas conocidos al eliminar un inquilino existente de Azure AD B2C y volver a crearlo con el mismo nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="bcd0c-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span></span> <span data-ttu-id="bcd0c-114">Al crear un inquilino de Azure AD B2C, debe usar un nombre de dominio diferente.</span><span class="sxs-lookup"><span data-stu-id="bcd0c-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="bcd0c-115">Si estas soluciones no funcionan, póngase en contacto con el soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd0c-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="bcd0c-116">Para obtener más información, consulte [Azure Active Directory B2C: presentación de solicitudes de soporte técnico](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="bcd0c-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

