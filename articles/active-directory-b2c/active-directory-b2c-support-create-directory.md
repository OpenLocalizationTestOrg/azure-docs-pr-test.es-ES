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
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="c0c18-103">Solución de problemas a la hora de crear un inquilino de Azure Active Directory o de Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="c0c18-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="c0c18-104">Creación de un inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0c18-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="c0c18-105">Si no se puede crear a un inquilino de Azure Active Directory (Azure AD) en el primer intento de hello, vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="c0c18-105">If you can't create an Azure Active Directory (Azure AD) tenant on hello first attempt, try again.</span></span> <span data-ttu-id="c0c18-106">Si persiste el problema de hello, póngase en contacto con el soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0c18-106">If hello problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="c0c18-107">Creación de un inquilino de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c0c18-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="c0c18-108">Si encuentra problemas cuando se [crear un B2C de Azure Active Directory (Azure AD B2C) inquilino](active-directory-b2c-get-started.md), intente Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="c0c18-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try hello following options:</span></span>

* <span data-ttu-id="c0c18-109">Si el inquilino de Azure AD B2C hello no aparece en la lista de los inquilinos, inténtelo de nuevo inquilino de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c0c18-109">If hello Azure AD B2C tenant doesn't show up in your list of tenants, try again toocreate hello tenant.</span></span>
* <span data-ttu-id="c0c18-110">Si el inquilino de Azure AD B2C Hola aparecen en la lista de los inquilinos y ve Hola siguiente mensaje de error, eliminar el inquilino de Hola y vuelva a crearlo:</span><span class="sxs-lookup"><span data-stu-id="c0c18-110">If hello Azure AD B2C tenant does show up in your list of tenants and you see hello following  error message, delete hello tenant and create it again:</span></span>

    <span data-ttu-id="c0c18-111">"No se pudo completar el Hola creación de inquilinos de B2C hello 'contosob2c'.</span><span class="sxs-lookup"><span data-stu-id="c0c18-111">"Could not complete hello creation of hello B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="c0c18-112">Para obtener más ayuda, visite este [vínculo](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409)".</span><span class="sxs-lookup"><span data-stu-id="c0c18-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="c0c18-113">Se conocen problemas cuando se elimina un B2C existente de AD de Azure de inquilinos y vuelva a crearlo utilizando Hola mismo nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="c0c18-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using hello same domain name.</span></span> <span data-ttu-id="c0c18-114">Al crear un inquilino de Azure AD B2C, debe usar un nombre de dominio diferente.</span><span class="sxs-lookup"><span data-stu-id="c0c18-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="c0c18-115">Si estas soluciones no funcionan, póngase en contacto con el soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0c18-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="c0c18-116">Para obtener más información, consulte [Azure Active Directory B2C: presentación de solicitudes de soporte técnico](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="c0c18-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

