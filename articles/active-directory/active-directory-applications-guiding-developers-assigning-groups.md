---
title: aaaAssign grupos de aplicaciones de AD tooAzure | Documentos de Microsoft
description: "¿Cómo tooimplement grupo asignación para las aplicaciones de Azure."
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
ms.openlocfilehash: 086619df09c13bf259afc3128d45ed804b99e519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-azure-active-directory-groups-tooan-application"></a><span data-ttu-id="a2333-103">Asignar a grupos de Azure Active Directory tooan aplicación</span><span class="sxs-lookup"><span data-stu-id="a2333-103">Assign Azure Active Directory groups tooan application</span></span>
<span data-ttu-id="a2333-104">Antes de poder asignar usuarios y aplicaciones de tooan de grupos, necesita la asignación de usuario.</span><span class="sxs-lookup"><span data-stu-id="a2333-104">Before you can assign users and groups tooan application, you must require user assignment.</span></span> <span data-ttu-id="a2333-105">toolearn cómo toorequire asignación de usuario, vea hello [que requieren la asignación de usuario](active-directory-applications-guiding-developers-requiring-user-assignment.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="a2333-105">toolearn how toorequire user assignment, see hello [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="a2333-106">En este artículo se da por supuesto que ya se han creado grupos de active directory de Hola que usa para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="a2333-106">This article assumes that you have already created groups in hello active directory you are using for this application.</span></span>

## <a name="assigning-groups-tooan-application"></a><span data-ttu-id="a2333-107">Asignar grupos tooan aplicación</span><span class="sxs-lookup"><span data-stu-id="a2333-107">Assigning Groups tooan Application</span></span>
1. <span data-ttu-id="a2333-108">Inicie sesión en toohello portal de Azure con una cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="a2333-108">Log in toohello Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="a2333-109">Haga clic en hello **todos los elementos** elemento en el menú principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2333-109">Click on hello **All Items** item in hello main menu.</span></span>
3. <span data-ttu-id="a2333-110">Elija el directorio de Hola que está usando para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a2333-110">Choose hello directory you are using for hello application.</span></span>
4. <span data-ttu-id="a2333-111">Haga clic en hello **aplicaciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="a2333-111">Click on hello **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="a2333-112">Seleccione la aplicación hello de lista de Hola de las aplicaciones asociadas a este directorio.</span><span class="sxs-lookup"><span data-stu-id="a2333-112">Select hello application from hello list of applications associated with this directory.</span></span>
6. <span data-ttu-id="a2333-113">Haga clic en hello **usuarios y grupos** ficha.</span><span class="sxs-lookup"><span data-stu-id="a2333-113">Click hello **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="a2333-114">Lista de grupos en active directory mediante el uso de Hola Hola de filtros **grupos** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="a2333-114">Filter hello list of groups in your active directory by using hello **Groups** dropdown list.</span></span>
8. <span data-ttu-id="a2333-115">Seleccione el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2333-115">Select hello group.</span></span>
9. <span data-ttu-id="a2333-116">Haga clic en **ASIGNAR**.</span><span class="sxs-lookup"><span data-stu-id="a2333-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="a2333-117">Haga clic en **Sí** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="a2333-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2333-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2333-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
