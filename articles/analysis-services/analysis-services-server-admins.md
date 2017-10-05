---
title: "Administración de administradores de servidor en Azure Analysis Services | Microsoft Docs"
description: Aprenda a administrar administradores de servidor de Analysis Services en Azure.
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
ms.openlocfilehash: a1b58125dafdf73f245b6a8cd0f4917513b22ea9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="dda83-103">Administración de administradores de servidor</span><span class="sxs-lookup"><span data-stu-id="dda83-103">Manage server administrators</span></span>
<span data-ttu-id="dda83-104">Los administradores del servidor deben ser un usuario o grupo válido en Azure Active Directory (Azure AD) para el inquilino en el que reside el servidor.</span><span class="sxs-lookup"><span data-stu-id="dda83-104">Server administrators must be a valid user or group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span></span> <span data-ttu-id="dda83-105">Puede usar **Administradores de Analysis Services** en la hoja de control del servidor en Azure Portal o Propiedades del servidor en SSMS para administrar los administradores de servidor.</span><span class="sxs-lookup"><span data-stu-id="dda83-105">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> 

## <a name="to-add-server-administrators-by-using-azure-portal"></a><span data-ttu-id="dda83-106">Incorporación de administradores de servidor mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dda83-106">To add server administrators by using Azure portal</span></span>
1. <span data-ttu-id="dda83-107">En la hoja de control del servidor, haga clic en **Administradores de Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="dda83-107">In the control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="dda83-108">En la hoja **\<nombreDeServidor > Administradores de Analysis Services**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dda83-108">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="dda83-109">En la hoja **Agregar administradores de servidor**, seleccione las cuentas de usuario de Azure AD o invite usuarios externos por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="dda83-109">In the **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Administradores del servidor en Azure Portal](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a><span data-ttu-id="dda83-111">Incorporación de administradores de servidor mediante SSMS</span><span class="sxs-lookup"><span data-stu-id="dda83-111">To add server administrators by using SSMS</span></span>
1. <span data-ttu-id="dda83-112">Haga clic con el botón derecho en el servidor > **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="dda83-112">Right-click the server > **Properties**.</span></span>
2. <span data-ttu-id="dda83-113">En **Propiedades de Analysis Server**, haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="dda83-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="dda83-114">Haga clic en **Agregar** y escriba la dirección de correo electrónico de un usuario o grupo de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dda83-114">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span></span>
   
    ![Incorporación de administradores de servidor en SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="dda83-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dda83-116">Next steps</span></span> 
[<span data-ttu-id="dda83-117">Permisos de usuario y autenticación</span><span class="sxs-lookup"><span data-stu-id="dda83-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
<span data-ttu-id="dda83-118">[Manage database roles and users](analysis-services-database-users.md) (Administración de roles y usuarios de una base de datos)</span><span class="sxs-lookup"><span data-stu-id="dda83-118">[Manage database roles and users](analysis-services-database-users.md)</span></span>  
[<span data-ttu-id="dda83-119">Control de acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="dda83-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

