---
title: "Asignación de grupos a aplicaciones de Azure AD | Microsoft Docs"
description: "Cómo implementar la asignación de grupos para aplicaciones de Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="9efdf-103">Asignación de grupos de Azure Active Directory a una aplicación</span><span class="sxs-lookup"><span data-stu-id="9efdf-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="9efdf-104">Para poder asignar usuarios y grupos a una aplicación, debe requerir la asignación de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9efdf-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="9efdf-105">Para obtener información sobre cómo requerir la asignación de usuarios, consulte el artículo [Necesidad de asignación de usuario](active-directory-applications-guiding-developers-requiring-user-assignment.md) .</span><span class="sxs-lookup"><span data-stu-id="9efdf-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="9efdf-106">En este artículo se supone que ya ha creado grupos en el Active Directory que está usando para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="9efdf-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="9efdf-107">Asignación de grupos a una aplicación</span><span class="sxs-lookup"><span data-stu-id="9efdf-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="9efdf-108">Inicie sesión en el portal de Azure con una cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="9efdf-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="9efdf-109">Haga clic en el elemento **Todos los elementos** del menú principal.</span><span class="sxs-lookup"><span data-stu-id="9efdf-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="9efdf-110">Elija el directorio que está usando para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9efdf-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="9efdf-111">Haga clic en la pestaña **APLICACIONES** .</span><span class="sxs-lookup"><span data-stu-id="9efdf-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="9efdf-112">Seleccione la aplicación en la lista de aplicaciones asociada a este directorio.</span><span class="sxs-lookup"><span data-stu-id="9efdf-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="9efdf-113">Haga clic en la pestaña **USUARIOS Y GRUPOS** .</span><span class="sxs-lookup"><span data-stu-id="9efdf-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="9efdf-114">Filtre la lista de grupos en Active Directory mediante la lista desplegable **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="9efdf-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="9efdf-115">Seleccione el grupo.</span><span class="sxs-lookup"><span data-stu-id="9efdf-115">Select the group.</span></span>
9. <span data-ttu-id="9efdf-116">Haga clic en **ASIGNAR**.</span><span class="sxs-lookup"><span data-stu-id="9efdf-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="9efdf-117">Haga clic en **Sí** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="9efdf-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9efdf-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9efdf-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
