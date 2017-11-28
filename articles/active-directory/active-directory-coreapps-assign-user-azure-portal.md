---
title: "una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory aaaAssign | Documentos de Microsoft"
description: "¿Cómo tooselect una tooassign de aplicación de empresa una tooit de usuario o grupo en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="0859c-103">Asignar una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0859c-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="0859c-104">Es fácil tooassign un usuario o un grupo tooyour las aplicaciones empresariales en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0859c-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0859c-105">Debe tener la aplicación empresarial de hello permisos adecuados toomanage hello y debe ser administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="0859c-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="0859c-106">¿Cómo se puede asignar acceso de usuario tooan aplicación de empresa?</span><span class="sxs-lookup"><span data-stu-id="0859c-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="0859c-107">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="0859c-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="0859c-108">Seleccione **más servicios**, escriba Azure Active Directory en el cuadro de texto de hello y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="0859c-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="0859c-109">En hello **Azure Active Directory - *directoryname***  hoja (es decir, hello Azure AD hoja para el directorio de hello administra), seleccione **aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0859c-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="0859c-111">En hello **aplicaciones empresariales** hoja, seleccione **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0859c-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="0859c-112">Verá una lista de aplicaciones de hello que puede administrar.</span><span class="sxs-lookup"><span data-stu-id="0859c-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="0859c-113">En hello **aplicaciones empresariales - todas las aplicaciones** hoja, seleccione una aplicación.</span><span class="sxs-lookup"><span data-stu-id="0859c-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="0859c-114">En hello ***appname*** hoja (es decir, Hola hoja con nombre Hola de aplicación seleccionada de hello en el título de hello), seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0859c-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Selección de Hola a todos los comandos de las aplicaciones](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="0859c-116">En hello ***appname*** **-asignación de grupo de & usuario** hoja, seleccione hello **agregar** comando.</span><span class="sxs-lookup"><span data-stu-id="0859c-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="0859c-117">En hello **Agregar asignación** hoja, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0859c-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Asignar una aplicación de usuario o grupo toohello](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="0859c-119">En hello **usuarios y grupos** hoja, seleccione uno o más usuarios o grupos de hello lista y, a continuación, seleccione hello **seleccione** situado en parte inferior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="0859c-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="0859c-120">En hello **Agregar asignación** hoja, seleccione **rol**.</span><span class="sxs-lookup"><span data-stu-id="0859c-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="0859c-121">A continuación, en hello **Seleccionar rol** hoja, seleccione un toohello de tooapply rol seleccionado usuarios o grupos y, a continuación, seleccione hello **Aceptar** situado en parte inferior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="0859c-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="0859c-122">En hello **Agregar asignación** hoja, seleccione hello **asignar** situado en parte inferior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="0859c-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="0859c-123">Hola asignados a los usuarios o grupos tendrán permisos de hello definidos por el rol seleccionado de Hola para esta aplicación de empresa.</span><span class="sxs-lookup"><span data-stu-id="0859c-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0859c-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0859c-124">Next steps</span></span>
* [<span data-ttu-id="0859c-125">Ver todos mis grupos</span><span class="sxs-lookup"><span data-stu-id="0859c-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="0859c-126">Eliminación de asignaciones de usuario o grupo de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="0859c-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="0859c-127">Deshabilitar los inicios de sesión de los usuarios de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="0859c-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="0859c-128">Cambiar el nombre de Hola o el logotipo de una aplicación de empresa</span><span class="sxs-lookup"><span data-stu-id="0859c-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
