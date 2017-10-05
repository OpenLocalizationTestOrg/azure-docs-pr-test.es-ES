---
title: "Cambio del nombre o el logotipo de una aplicación empresarial en Azure Active Directory | Microsoft Docs"
description: "Cómo cambiar el nombre o el logotipo de una aplicación empresarial personalizada en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="403c6-103">Cambio del nombre o el logotipo de una aplicación empresarial en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="403c6-103">Change the name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="403c6-104">Cambiar el nombre o el logotipo de una aplicación empresarial personalizada en Azure Active Directory (Azure AD) es fácil.</span><span class="sxs-lookup"><span data-stu-id="403c6-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="403c6-105">Debe tener los permisos adecuados para realizar estos cambios, y debe ser el creador de la aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="403c6-105">You must have the appropriate permissions to make these changes, and you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="403c6-106">¿Cómo puedo cambiar el nombre o el logotipo de una aplicación empresarial?</span><span class="sxs-lookup"><span data-stu-id="403c6-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="403c6-107">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="403c6-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="403c6-108">Seleccione **Más servicios**, escriba **Azure Active Directory** en el cuadro de texto y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="403c6-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="403c6-109">En la hoja **Azure Active Directory - *nombreDelDirectorio*** (es decir, la hoja de Azure AD del directorio que está administrando), seleccione **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="403c6-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="403c6-111">En la hoja **Aplicaciones empresariales**, seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="403c6-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="403c6-112">Verá una lista de las aplicaciones que puede administrar.</span><span class="sxs-lookup"><span data-stu-id="403c6-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="403c6-113">En la hoja **Enterprise applications (Aplicaciones empresariales) - Todas las aplicaciones** , seleccione una aplicación.</span><span class="sxs-lookup"><span data-stu-id="403c6-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="403c6-114">En la hoja ***nombreDeLaAplicación*** (es decir, la hoja con el nombre de la aplicación seleccionada en el título), seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="403c6-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Selección del comando Propiedades](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="403c6-116">En la hoja ***nombreDeAplicación*** **- Propiedades**, busque el archivo que desea usar como nuevo logotipo o edite el nombre de la aplicación, o ambas opciones.</span><span class="sxs-lookup"><span data-stu-id="403c6-116">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![Cambio del logotipo o de la aplicación o comando de propiedades de nombre](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="403c6-118">Haga clic en el comando **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="403c6-118">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="403c6-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="403c6-119">Next steps</span></span>
* [<span data-ttu-id="403c6-120">Ver todos mis grupos</span><span class="sxs-lookup"><span data-stu-id="403c6-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="403c6-121">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="403c6-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="403c6-122">Eliminación de asignaciones de usuario o grupo de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="403c6-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="403c6-123">Deshabilitar los inicios de sesión de los usuarios de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="403c6-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
