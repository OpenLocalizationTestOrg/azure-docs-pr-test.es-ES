---
title: "aaaHow tooperform una revisión de acceso | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooperform un nuevo examen con Hola aplicación de Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="90fe2-103">¿Cómo tooperform un acceso Revise en Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="90fe2-103">How tooperform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="90fe2-104">Active Directory (AD) Privileged Identity Management de Azure simplifica cómo las empresas administran tooresources de acceso con privilegios en Azure AD y otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="90fe2-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="90fe2-105">Si se le asigna el rol administrativo tooan, Administrador de roles con privilegios de su organización puede pedirle que tooregularly confirmar que aún es necesario dicho rol para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="90fe2-105">If you are assigned tooan administrative role, your organization's privileged role administrator may ask you tooregularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="90fe2-106">Puede obtener un correo electrónico que incluye un vínculo, o puede ir recta toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90fe2-106">You might get an email that includes a link, or you can go straight toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="90fe2-107">Siga los pasos de hello en este tooperform artículo revisar automáticamente los roles asignados.</span><span class="sxs-lookup"><span data-stu-id="90fe2-107">Follow hello steps in this article tooperform a self-review of your assigned roles.</span></span>

<span data-ttu-id="90fe2-108">Si es un administrador de roles con privilegios interesado en las revisiones de acceso, obtenga más información en [cómo toostart un acceso revisar](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="90fe2-108">If you're a privileged role administrator interested in access reviews, get more details at [How toostart an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="90fe2-109">Agregar aplicación de hello Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="90fe2-109">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="90fe2-110">Puede utilizar aplicaciones de administración de identidad con privilegios (PIM) hello Azure AD en hello [portal de Azure](https://portal.azure.com/) tooperform revisarse.</span><span class="sxs-lookup"><span data-stu-id="90fe2-110">You can use hello Azure AD Privileged Identity Management (PIM) application in hello [Azure portal](https://portal.azure.com/) tooperform your review.</span></span>  <span data-ttu-id="90fe2-111">Si no tiene la aplicación de Azure AD Privileged Identity Management de hello en el portal, siga estas tooget pasos que se inició.</span><span class="sxs-lookup"><span data-stu-id="90fe2-111">If you don't have hello Azure AD Privileged Identity Management application on your portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="90fe2-112">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90fe2-112">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="90fe2-113">Seleccione el nombre de usuario en hello superior derecho de hello portal de Azure y directorio Hola seleccione donde tendrá estar en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="90fe2-113">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="90fe2-114">Seleccione **más servicios** y usar hello toosearch de cuadro de texto de filtro para **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="90fe2-114">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="90fe2-115">Comprobar **Pin toodashboard** y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="90fe2-115">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="90fe2-116">se abrirá Hola aplicación Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="90fe2-116">hello Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="90fe2-117">Aprobación o denegación de acceso</span><span class="sxs-lookup"><span data-stu-id="90fe2-117">Approve or deny access</span></span>
<span data-ttu-id="90fe2-118">Al aprobar o denegar el acceso, está indicando solo revisor Hola si seguir utilizando este rol o no.</span><span class="sxs-lookup"><span data-stu-id="90fe2-118">When you approve or deny access, you're just telling hello reviewer whether you still use this role or not.</span></span> <span data-ttu-id="90fe2-119">Elija **aprobar** si desea que toostay en función de hello, o **Deny** si no necesita Hola acceso ya.</span><span class="sxs-lookup"><span data-stu-id="90fe2-119">Choose **Approve** if you want toostay in hello role, or **Deny** if you don't need hello access anymore.</span></span> <span data-ttu-id="90fe2-120">Su estado no cambiará inmediatamente, hasta que el revisor de Hola aplica a los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="90fe2-120">Your status won't change right away, until hello reviewer applies hello results.</span></span>
<span data-ttu-id="90fe2-121">Siga estos pasos toofind y completar la revisión de acceso de hello:</span><span class="sxs-lookup"><span data-stu-id="90fe2-121">Follow these steps toofind and complete hello access review:</span></span>

1. <span data-ttu-id="90fe2-122">En la aplicación de PIM hello, seleccione **revisión privilegios de acceso**.</span><span class="sxs-lookup"><span data-stu-id="90fe2-122">In hello PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="90fe2-123">Si tiene cualquier revisiones acceso pendiente, aparecen en hello que acceso de Azure AD revisa hoja.</span><span class="sxs-lookup"><span data-stu-id="90fe2-123">If you have any pending access reviews, they appear in hello Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="90fe2-124">Seleccione revisión Hola desea toocomplete.</span><span class="sxs-lookup"><span data-stu-id="90fe2-124">Select hello review you want toocomplete.</span></span>
3. <span data-ttu-id="90fe2-125">A menos que cree revisión hello, parece como Hola solo usuario en revisión Hola.</span><span class="sxs-lookup"><span data-stu-id="90fe2-125">Unless you created hello review, you appear as hello only user in hello review.</span></span> <span data-ttu-id="90fe2-126">Seleccione siguiente tooyour nombre de marca de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="90fe2-126">Select hello check mark next tooyour name.</span></span>
4. <span data-ttu-id="90fe2-127">Elija **Aprobar** o **Denegar**.</span><span class="sxs-lookup"><span data-stu-id="90fe2-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="90fe2-128">Es posible que tenga una razón para la toma de decisiones en hello tooinclude **proporcionar una razón** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="90fe2-128">You may need tooinclude a reason for your decision in hello **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="90fe2-129">Hola cerrar **roles de Azure AD de revisión** hoja.</span><span class="sxs-lookup"><span data-stu-id="90fe2-129">Close hello **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="90fe2-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90fe2-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
