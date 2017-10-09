---
title: "administradores de servidor aaaManage en los servicios de análisis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage administradores de servidor para un servidor de Analysis Services en Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="b49a1-103">Administración de administradores de servidor</span><span class="sxs-lookup"><span data-stu-id="b49a1-103">Manage server administrators</span></span>
<span data-ttu-id="b49a1-104">Los administradores del servidor deben ser un usuario o grupo válido en hello Azure Active Directory (Azure AD) inquilino hello en qué Hola reside el servidor.</span><span class="sxs-lookup"><span data-stu-id="b49a1-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="b49a1-105">Puede usar **administradores de Analysis Services** en la hoja de control de hello para el servidor en el portal de Azure o de los administradores del servidor SSMS toomanage propiedades del servidor.</span><span class="sxs-lookup"><span data-stu-id="b49a1-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="b49a1-106">administradores del servidor tooadd mediante el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b49a1-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="b49a1-107">En la hoja de control de hello para el servidor, haga clic en **administradores de Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="b49a1-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="b49a1-108">Hola  **\<nombreDeServidor >-administradores de Analysis Services** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="b49a1-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="b49a1-109">Hola **agregar los administradores del servidor** hoja, seleccione las cuentas de usuario de Azure AD o invitar a usuarios externos mediante la dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="b49a1-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Administradores del servidor en Azure Portal](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="b49a1-111">administradores del servidor tooadd mediante SSMS</span><span class="sxs-lookup"><span data-stu-id="b49a1-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="b49a1-112">Servidor de hello contextual > **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="b49a1-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="b49a1-113">En **Propiedades de Analysis Server**, haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="b49a1-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="b49a1-114">Haga clic en **agregar**y a continuación, escriba la dirección de correo electrónico de Hola para un usuario o grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b49a1-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![Incorporación de administradores de servidor en SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="b49a1-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b49a1-116">Next steps</span></span> 
[<span data-ttu-id="b49a1-117">Permisos de usuario y autenticación</span><span class="sxs-lookup"><span data-stu-id="b49a1-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
<span data-ttu-id="b49a1-118">[Manage database roles and users](analysis-services-database-users.md) (Administración de roles y usuarios de una base de datos)</span><span class="sxs-lookup"><span data-stu-id="b49a1-118">[Manage database roles and users](analysis-services-database-users.md)</span></span>  
[<span data-ttu-id="b49a1-119">Control de acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="b49a1-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

