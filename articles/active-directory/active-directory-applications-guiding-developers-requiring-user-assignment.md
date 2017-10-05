---
title: "Procedimiento para requerir la asignación de usuarios: Azure AD | Microsoft Docs"
description: "Cómo requerir la asignación de usuario para aplicaciones de Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 079b806c041a4a21e9350342867aee581c57bf45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-require-user-assignment"></a><span data-ttu-id="7a926-103">Azure AD y aplicaciones: procedimiento para requerir la asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="7a926-103">Azure AD and applications: Require user assignment</span></span>
## <a name="requiring-user-assignment"></a><span data-ttu-id="7a926-104">Necesidad de asignación de usuario</span><span class="sxs-lookup"><span data-stu-id="7a926-104">Requiring User Assignment</span></span>
1. <span data-ttu-id="7a926-105">Inicie sesión en el portal de Azure con una cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="7a926-105">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="7a926-106">Haga clic en el elemento **Todos los elementos** del menú principal.</span><span class="sxs-lookup"><span data-stu-id="7a926-106">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="7a926-107">Elija el directorio que está usando para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7a926-107">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="7a926-108">Haga clic en la pestaña **APLICACIONES** .</span><span class="sxs-lookup"><span data-stu-id="7a926-108">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="7a926-109">Seleccione la aplicación en la lista de aplicaciones asociada a este directorio.</span><span class="sxs-lookup"><span data-stu-id="7a926-109">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="7a926-110">Haga clic en la pestaña **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="7a926-110">Click the **CONFIGURE** tab.</span></span>
7. <span data-ttu-id="7a926-111">Cambie la opción **Asignación de usuario necesaria para acceder a la aplicación** a Sí.</span><span class="sxs-lookup"><span data-stu-id="7a926-111">Change the **User Assignment Required to Access App** toggle to Yes.</span></span>
8. <span data-ttu-id="7a926-112">Haga clic en el botón **Guardar** de la parte inferior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="7a926-112">Click the **Save** button at the bottom of the screen.</span></span>

<span data-ttu-id="7a926-113">Ahora tendrá que asignar usuarios o grupos a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7a926-113">You will now have to assign users and/or groups to the application.</span></span> <span data-ttu-id="7a926-114">Vea [Asignación de usuarios a una aplicación](active-directory-applications-guiding-developers-assigning-users.md) y [Asignación de grupos a una aplicación](active-directory-applications-guiding-developers-assigning-groups.md).</span><span class="sxs-lookup"><span data-stu-id="7a926-114">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a926-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7a926-115">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
