---
title: "Deshabilitación de los inicios de sesión de usuario de una aplicación empresarial en Azure Active Directory | Microsoft Docs"
description: "Cómo deshabilitar una aplicación empresarial para que ningún usuario pueda iniciar sesión en ella en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 5d27046370eada0c371c94fb573fa1bcf536f7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="328cd-103">Deshabilitación de los inicios de sesión de usuario de una aplicación empresarial en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="328cd-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="328cd-104">Deshabilitar una aplicación empresarial para que ningún usuario pueda iniciar sesión en ella en Azure Active Directory (Azure AD) es fácil.</span><span class="sxs-lookup"><span data-stu-id="328cd-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="328cd-105">Debe tener los permisos adecuados para administrar la aplicación de empresa y debe ser administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="328cd-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="328cd-106">¿Cómo puedo deshabilitar los inicios de sesión de usuario?</span><span class="sxs-lookup"><span data-stu-id="328cd-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="328cd-107">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="328cd-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="328cd-108">Seleccione **Más servicios**, escriba **Azure Active Directory** en el cuadro de texto y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="328cd-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="328cd-109">En la hoja **Azure Active Directory** -  ***nombreDelDirectorio*** (es decir, la hoja de Azure AD del directorio que está administrando), seleccione **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="328cd-109">On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="328cd-111">En la hoja **Aplicaciones empresariales**, seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="328cd-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="328cd-112">Verá una lista de las aplicaciones que puede administrar.</span><span class="sxs-lookup"><span data-stu-id="328cd-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="328cd-113">En la hoja **Enterprise applications (Aplicaciones empresariales) - Todas las aplicaciones** , seleccione una aplicación.</span><span class="sxs-lookup"><span data-stu-id="328cd-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="328cd-114">En la hoja ***nombreDeLaAplicación*** (es decir, la hoja con el nombre de la aplicación seleccionada en el título), seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="328cd-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Selección del comando Todas las aplicaciones](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="328cd-116">En la hoja ***nombreDeLaAplicación*** - **Propiedades**, en **¿Habilitado para que los usuarios inicien sesión?**, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="328cd-116">On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="328cd-117">Haga clic en el comando **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="328cd-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="328cd-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="328cd-118">Next steps</span></span>
* [<span data-ttu-id="328cd-119">Ver todos mis grupos</span><span class="sxs-lookup"><span data-stu-id="328cd-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="328cd-120">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="328cd-120">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="328cd-121">Eliminación de asignaciones de usuario o grupo de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="328cd-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="328cd-122">Cambio del nombre o el logotipo de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="328cd-122">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
