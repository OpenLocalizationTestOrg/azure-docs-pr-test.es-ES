---
title: usuarios aaaAssign tooa dominio personalizado en Azure Active Directory | Documentos de Microsoft
description: "¿Cómo toopopulate un dominio personalizado en Azure Active Directory con cuentas de usuario."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="cdac8-103">Asignar los usuarios de dominio personalizado de tooa</span><span class="sxs-lookup"><span data-stu-id="cdac8-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="cdac8-104">Después de haber agregado su tooAzure Active Directory de dominio personalizado, debe agregar cuentas de usuario de Hola para este dominio para que pueda empezar a autenticarlos.</span><span class="sxs-lookup"><span data-stu-id="cdac8-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdac8-105">Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="cdac8-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="cdac8-106">Para cómo toomanage los nombres de dominio en el centro de administración de hello Azure AD, consulte [administrar nombres de dominio personalizado en Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cdac8-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="cdac8-107">Usuarios sincronizados desde un directorio local</span><span class="sxs-lookup"><span data-stu-id="cdac8-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="cdac8-108">Si ya se han configurado una conexión entre sus instalaciones en Active Directory y Azure Active Directory, la sincronización puede rellenar las cuentas de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdac8-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="cdac8-109">Para obtener más información sobre cómo toosynchronize Azure Active Directory con su Active Directory local, vea [integrar las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="cdac8-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="cdac8-110">Usuarios agregan y administran en la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="cdac8-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="cdac8-111">dominio de hello toochange para una cuenta de usuario existente:</span><span class="sxs-lookup"><span data-stu-id="cdac8-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="cdac8-112">Abra hello Azure portal clásico con una cuenta que sea un administrador global o un administrador del usuario.</span><span class="sxs-lookup"><span data-stu-id="cdac8-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="cdac8-113">Abra el directorio.</span><span class="sxs-lookup"><span data-stu-id="cdac8-113">Open your directory.</span></span>
3. <span data-ttu-id="cdac8-114">Seleccione hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="cdac8-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="cdac8-115">Seleccione usuario Hola de hello lista.</span><span class="sxs-lookup"><span data-stu-id="cdac8-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="cdac8-116">Cambiar el dominio de hello para el usuario de hello y, a continuación, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="cdac8-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="cdac8-117">Esto también puede hacerse mediante [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) o hello [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="cdac8-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="cdac8-118">Selección de un dominio personalizado al crear un nuevo usuario</span><span class="sxs-lookup"><span data-stu-id="cdac8-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="cdac8-119">Abra hello Azure portal clásico con una cuenta que sea un administrador global o un administrador del usuario.</span><span class="sxs-lookup"><span data-stu-id="cdac8-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="cdac8-120">Abra el directorio.</span><span class="sxs-lookup"><span data-stu-id="cdac8-120">Open your directory.</span></span>
3. <span data-ttu-id="cdac8-121">Seleccione hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="cdac8-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="cdac8-122">En la barra de comandos de hello, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="cdac8-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="cdac8-123">Cuando se agrega el nombre de usuario de hello, elija dominio personalizado de hello en lista de dominios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdac8-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="cdac8-124">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cdac8-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdac8-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cdac8-125">Next steps</span></span>
* [<span data-ttu-id="cdac8-126">Uso de dominio personalizado nombres toosimplify Hola inicio de sesión experiencia para los usuarios</span><span class="sxs-lookup"><span data-stu-id="cdac8-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="cdac8-127">Managing custom domain names (Administración de nombres de dominio).</span><span class="sxs-lookup"><span data-stu-id="cdac8-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="cdac8-128">Información general conceptual de nombres de dominio personalizado en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cdac8-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

