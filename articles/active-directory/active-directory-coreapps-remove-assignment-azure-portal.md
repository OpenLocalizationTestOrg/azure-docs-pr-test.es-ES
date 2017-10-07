---
title: "aaaRemove una asignación de usuario o grupo de una aplicación de empresa en Azure Active Directory | Documentos de Microsoft"
description: "Cómo tooremove Hola tener acceso a la asignación de un usuario o grupo de una aplicación de empresa en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="ea2cc-103">Eliminación de asignaciones de usuario o grupo de una aplicación empresarial en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea2cc-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="ea2cc-104">Es fácil tooremove un usuario o un grupo se asignen tooone de acceso de las aplicaciones empresariales en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea2cc-104">It's easy tooremove a user or a group from being assigned access tooone of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ea2cc-105">Debe tener la aplicación empresarial de hello permisos adecuados toomanage hello y debe ser administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="ea2cc-106">¿Cómo se puede eliminar una asignación de grupo o usuario?</span><span class="sxs-lookup"><span data-stu-id="ea2cc-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="ea2cc-107">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="ea2cc-108">Seleccione **más servicios**, escriba **Azure Active Directory** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="ea2cc-109">En hello **Azure Active Directory - *directoryname***  hoja (es decir, hello Azure AD hoja para el directorio de hello administra), seleccione **aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="ea2cc-111">En hello **aplicaciones empresariales** hoja, seleccione **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="ea2cc-112">Verá una lista de aplicaciones de hello que puede administrar.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="ea2cc-113">En hello **aplicaciones empresariales - todas las aplicaciones** hoja, seleccione una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="ea2cc-114">En hello ***appname*** hoja (es decir, Hola hoja con nombre Hola de aplicación seleccionada de hello en el título de hello), seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Selección de usuarios o grupos](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="ea2cc-116">En hello ***appname*** **-asignación de grupo de & usuario** hoja, seleccione uno de varios usuarios o grupos y, a continuación, seleccione hello **quitar** comando.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-116">On hello ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select hello **Remove** command.</span></span> <span data-ttu-id="ea2cc-117">Confirme su decisión en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea2cc-117">Confirm your decision at hello prompt.</span></span>

    ![Al seleccionar el comando Remove de Hola](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="ea2cc-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea2cc-119">Next steps</span></span>
* [<span data-ttu-id="ea2cc-120">Ver todos mis grupos</span><span class="sxs-lookup"><span data-stu-id="ea2cc-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="ea2cc-121">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="ea2cc-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="ea2cc-122">Deshabilitar los inicios de sesión de los usuarios de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="ea2cc-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="ea2cc-123">Cambiar el nombre de Hola o el logotipo de una aplicación de empresa</span><span class="sxs-lookup"><span data-stu-id="ea2cc-123">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
