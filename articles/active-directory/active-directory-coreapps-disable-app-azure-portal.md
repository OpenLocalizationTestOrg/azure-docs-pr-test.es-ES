---
title: "aaaDisable inicios de sesión para una aplicación de empresa en Azure Active Directory | Documentos de Microsoft"
description: "¿Cómo toodisable una aplicación empresarial para que ningún usuario puede iniciar sesión en tooit en Azure Active Directory"
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
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="67a54-103">Deshabilitación de los inicios de sesión de usuario de una aplicación empresarial en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67a54-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="67a54-104">Es fácil toodisable una aplicación empresarial para que ningún usuario puede iniciar sesión en tooit en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67a54-104">It's easy toodisable an enterprise application so that no users may sign in tooit in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="67a54-105">Debe tener la aplicación empresarial de hello permisos adecuados toomanage hello y debe ser administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="67a54-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="67a54-106">¿Cómo puedo deshabilitar los inicios de sesión de usuario?</span><span class="sxs-lookup"><span data-stu-id="67a54-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="67a54-107">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="67a54-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="67a54-108">Seleccione **más servicios**, escriba **Azure Active Directory** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="67a54-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="67a54-109">En hello **Azure Active Directory** -  ***directoryname*** hoja (es decir, hello Azure AD hoja para el directorio de hello administra), seleccione **lasaplicacionesempresariales**.</span><span class="sxs-lookup"><span data-stu-id="67a54-109">On hello **Azure Active Directory** -  ***directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="67a54-111">En hello **aplicaciones empresariales** hoja, seleccione **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="67a54-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="67a54-112">Ver una lista de las aplicaciones de hello que puede administrar.</span><span class="sxs-lookup"><span data-stu-id="67a54-112">You see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="67a54-113">En hello **aplicaciones empresariales - todas las aplicaciones** hoja, seleccione una aplicación.</span><span class="sxs-lookup"><span data-stu-id="67a54-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="67a54-114">En hello ***appname*** hoja (es decir, Hola hoja con nombre Hola de aplicación seleccionada de hello en el título de hello), seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="67a54-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![Selección de Hola a todos los comandos de las aplicaciones](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="67a54-116">En hello ***appname*** - **propiedades** hoja, seleccione **No** para **habilitado para los usuarios de toosign?**.</span><span class="sxs-lookup"><span data-stu-id="67a54-116">On hello ***appname*** - **Properties** blade, select **No** for **Enabled for users toosign-in?**.</span></span>
8. <span data-ttu-id="67a54-117">Seleccione hello **guardar** comando.</span><span class="sxs-lookup"><span data-stu-id="67a54-117">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67a54-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67a54-118">Next steps</span></span>
* [<span data-ttu-id="67a54-119">Ver todos mis grupos</span><span class="sxs-lookup"><span data-stu-id="67a54-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="67a54-120">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="67a54-120">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="67a54-121">Eliminación de asignaciones de usuario o grupo de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="67a54-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="67a54-122">Cambiar el nombre de Hola o el logotipo de una aplicación de empresa</span><span class="sxs-lookup"><span data-stu-id="67a54-122">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
