---
title: aaaManage tooresources de permisos en la pila de Azure (Administrador de servicios e inquilino) por usuario | Documentos de Microsoft
description: "Como administrador de servicios o inquilinos, obtenga información acerca de cómo toomanage permisos de RBAC."
services: azure-stack
documentationcenter: 
author: Heathl17
manager: byronr
editor: 
ms.assetid: cccac19a-e1bf-4e36-8ac8-2228e8487646
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 461feab12a4cb8b9402c6c61b721371c50f60559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control"></a><span data-ttu-id="95a20-103">Administrar el control de acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="95a20-103">Manage Role-Based Access Control</span></span>
<span data-ttu-id="95a20-104">En Azure Stack, un usuario puede ser un lector, propietario o colaborador de cada una de las instancias de una suscripción, grupo de recursos o servicio.</span><span class="sxs-lookup"><span data-stu-id="95a20-104">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span></span> <span data-ttu-id="95a20-105">Por ejemplo, el usuario A podría tener permisos de lector tooSubscription 1, pero tener permisos de propietario tooVirtual 7 de la máquina.</span><span class="sxs-lookup"><span data-stu-id="95a20-105">For example, User A might have reader permissions tooSubscription 1, but have owner permissions tooVirtual Machine 7.</span></span>

* <span data-ttu-id="95a20-106">Lector: el usuario puede ver todo el contenido, pero no puede realizar cambios.</span><span class="sxs-lookup"><span data-stu-id="95a20-106">Reader: User can view everything, but can’t make any changes.</span></span>
* <span data-ttu-id="95a20-107">Colaborador: Usuario puede administrarlo todo excepto tooresources de acceso.</span><span class="sxs-lookup"><span data-stu-id="95a20-107">Contributor: User can manage everything except access tooresources.</span></span>
* <span data-ttu-id="95a20-108">Propietario: Usuario puede administrarlo todo, incluidos los tooresources de acceso.</span><span class="sxs-lookup"><span data-stu-id="95a20-108">Owner: User can manage everything, including access tooresources.</span></span>

## <a name="set-access-permissions-for-a-user"></a><span data-ttu-id="95a20-109">Establecimiento de los permisos de acceso de un usuario</span><span class="sxs-lookup"><span data-stu-id="95a20-109">Set access permissions for a user</span></span>
1. <span data-ttu-id="95a20-110">Inicie sesión con una cuenta que tenga recursos de toohello de permisos de propietario que desee toomanage.</span><span class="sxs-lookup"><span data-stu-id="95a20-110">Sign in with an account that has owner permissions toohello resource you want toomanage.</span></span>
2. <span data-ttu-id="95a20-111">En la hoja de hello para el recurso de hello, haga clic en hello **acceso** icono ![](media/azure-stack-manage-permissions/image1.png).</span><span class="sxs-lookup"><span data-stu-id="95a20-111">In hello blade for hello resource, click hello **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span></span>
3. <span data-ttu-id="95a20-112">Hola **usuarios** hoja, haga clic en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="95a20-112">In hello **Users** blade, click **Roles**.</span></span>
4. <span data-ttu-id="95a20-113">Hola **Roles** hoja, haga clic en **agregar** tooadd permisos de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="95a20-113">In hello **Roles** blade, click **Add** tooadd permissions for hello user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95a20-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95a20-114">Next steps</span></span>
[<span data-ttu-id="95a20-115">Add a new Azure Stack tenant account in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95a20-115">Add an Azure Stack tenant</span></span>](azure-stack-add-new-user-aad.md)

