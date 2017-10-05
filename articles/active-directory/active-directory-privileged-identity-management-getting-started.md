---
title: "Introducción a Azure AD Privileged Identity Management | Microsoft Docs"
description: "Aprenda a administrar identidades con privilegios con la aplicación Privileged Identity Management de Azure Active Directory en el Portal de Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 17cdff033cc3dbb199d11c3b8ac1acbc92499877
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a><span data-ttu-id="4ba1b-103">Comenzar a usar Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="4ba1b-103">Start using Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="4ba1b-104">Con Privileged Identity Management de Azure Active Directory (AD), puede administrar, controlar y supervisar el acceso dentro de su organización.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="4ba1b-105">Este ámbito incluye el acceso a los recursos de Azure AD y otros servicios de Microsoft Online Services, como Office 365 o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-105">This scope includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="4ba1b-106">En este artículo se explica cómo agregar la aplicación PIM (Privileged Identity Management) de Azure AD al panel del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="4ba1b-107">Incorporación de la aplicación Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="4ba1b-107">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="4ba1b-108">Antes de usar Privileged Identity Management de Azure AD, debe agregar la aplicación al panel del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-108">Before you use Azure AD Privileged Identity Management, you need to add the application to your Azure portal dashboard.</span></span>

1. <span data-ttu-id="4ba1b-109">Inicie sesión en el [Portal de Azure](https://portal.azure.com/) como administrador global de su directorio.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-109">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="4ba1b-110">Si su organización tiene más de un directorio, seleccione su nombre de usuario en la esquina superior derecha del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-110">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="4ba1b-111">Seleccione el directorio en el que quiere usar PIM.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-111">Select the directory where you want to use PIM.</span></span>
3. <span data-ttu-id="4ba1b-112">Seleccione **Más servicios** y use el cuadro de texto Filtro para buscar **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-112">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="4ba1b-113">Active **Anclar al panel** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-113">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="4ba1b-114">Se abre la aplicación Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-114">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="4ba1b-115">Si es la primera persona que usa Azure AD Privileged Identity Management en el directorio, se le asignarán automáticamente los roles de **Administrador de seguridad** y **Administrador de roles con privilegios** del directorio.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-115">If you're the first person to use Azure AD Privileged Identity Management in your directory, you are automatically assigned the **Security administrator** and **Privileged role administrator** roles in the directory.</span></span> <span data-ttu-id="4ba1b-116">Solo los administradores de roles con privilegios pueden administrar las asignaciones de roles de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-116">Only privileged role administrators can manage role assignments of users.</span></span> <span data-ttu-id="4ba1b-117">Además, puede elegir ejecutar el [asistente para la seguridad.](active-directory-privileged-identity-management-security-wizard.md)</span><span class="sxs-lookup"><span data-stu-id="4ba1b-117">In addition, you may choose to run the [security wizard.](active-directory-privileged-identity-management-security-wizard.md)</span></span> <span data-ttu-id="4ba1b-118">Esto le lleva a través de la experiencia inicial de detección y asignación.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-118">that walks you through the initial discovery and assignment experience.</span></span>

## <a name="navigate-to-your-tasks"></a><span data-ttu-id="4ba1b-119">Navegación a sus tareas</span><span class="sxs-lookup"><span data-stu-id="4ba1b-119">Navigate to your tasks</span></span>
<span data-ttu-id="4ba1b-120">Después de configurar Azure AD Privileged Identity Management, verá la hoja de navegación cada vez que abra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-120">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span> <span data-ttu-id="4ba1b-121">Utilice esta hoja para realizar las tareas de administración de identidades.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-121">Use this blade to accomplish your identity management tasks.</span></span>

![Tareas de nivel superior para PIM (captura de pantalla)](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* <span data-ttu-id="4ba1b-123">**Mis roles** le lleva a la lista de roles que tiene asignados.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-123">**My Roles** takes you to a list of roles that are assigned to you.</span></span> <span data-ttu-id="4ba1b-124">Esta sección es donde activará los roles para los que es apto.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-124">This section is where you activate any roles that you are eligible for.</span></span>
* <span data-ttu-id="4ba1b-125">**Aprobar solicitudes (versión preliminar)** muestra una lista de solicitudes de activación pendientes de los usuarios del directorio.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-125">**Approve Requests (Preview)** displays a list of pending activation requests from users in your directory.</span></span> [<span data-ttu-id="4ba1b-126">Más información.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-126">Learn more.</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* <span data-ttu-id="4ba1b-127">**Solicitudes pendientes (versión preliminar)** muestra las solicitudes actuales que hay que activar.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-127">**Pending Requests (Preview)** displays any current requests to have made to activate.</span></span>
* <span data-ttu-id="4ba1b-128">**Revisar acceso** le lleva a todas las revisiones de acceso pendientes que necesita completar, tanto si revisa su acceso como el de otro usuario.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-128">**Review Access** takes you to any pending access reviews that you need to complete, whether you're reviewing access for yourself or someone else.</span></span>
* <span data-ttu-id="4ba1b-129">**Roles de directorios de Azure AD** situado en la sección "Administración" es el panel para que los administradores de roles con privilegios administren las asignaciones de roles, cambien la configuración de activación de roles e inicien revisiones del acceso, entre otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-129">**Azure AD Directory Roles** located under the 'Manage' section is the dashboard for privileged role admins to manage role assignments, change role activation settings, start access reviews, and more.</span></span> <span data-ttu-id="4ba1b-130">Las opciones de este panel están deshabilitadas para todos aquellos que no sean administradores de roles con privilegios.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-130">The options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ba1b-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ba1b-131">Next steps</span></span>
<span data-ttu-id="4ba1b-132">En la información general de [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) , se incluye más información sobre cómo administrar el acceso administrativo en una organización.</span><span class="sxs-lookup"><span data-stu-id="4ba1b-132">The [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
