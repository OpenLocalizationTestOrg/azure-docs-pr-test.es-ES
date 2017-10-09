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
# <a name="manage-server-administrators"></a>Administración de administradores de servidor
Los administradores del servidor deben ser un usuario o grupo válido en hello Azure Active Directory (Azure AD) inquilino hello en qué Hola reside el servidor. Puede usar **administradores de Analysis Services** en la hoja de control de hello para el servidor en el portal de Azure o de los administradores del servidor SSMS toomanage propiedades del servidor. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>administradores del servidor tooadd mediante el portal de Azure
1. En la hoja de control de hello para el servidor, haga clic en **administradores de Analysis Services**.
2. Hola  **\<nombreDeServidor >-administradores de Analysis Services** hoja, haga clic en **agregar**.
3. Hola **agregar los administradores del servidor** hoja, seleccione las cuentas de usuario de Azure AD o invitar a usuarios externos mediante la dirección de correo electrónico.

    ![Administradores del servidor en Azure Portal](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>administradores del servidor tooadd mediante SSMS
1. Servidor de hello contextual > **propiedades**.
2. En **Propiedades de Analysis Server**, haga clic en **Seguridad**.
3. Haga clic en **agregar**y a continuación, escriba la dirección de correo electrónico de Hola para un usuario o grupo en Azure AD.
   
    ![Incorporación de administradores de servidor en SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Pasos siguientes 
[Permisos de usuario y autenticación](analysis-services-manage-users.md)  
[Manage database roles and users](analysis-services-database-users.md) (Administración de roles y usuarios de una base de datos)  
[Control de acceso basado en roles](../active-directory/role-based-access-control-what-is.md)  

