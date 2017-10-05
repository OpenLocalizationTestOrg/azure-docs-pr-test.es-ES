---
title: "Asignación de usuarios a un dominio personalizado en Azure Active Directory | Microsoft Docs"
description: "Cómo rellenar un dominio personalizado en Azure Active Directory con cuentas de usuario."
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
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="065a7-103">Asignación de usuarios a un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="065a7-103">Assign users to a custom domain</span></span>
<span data-ttu-id="065a7-104">Una vez que haya agregado el dominio personalizado a Azure Active Directory, debe agregar las cuentas de usuario de este dominio para que pueda comenzar a autenticarlas.</span><span class="sxs-lookup"><span data-stu-id="065a7-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="065a7-105">Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="065a7-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="065a7-106">Para saber cómo administrar los nombres de dominio en el centro de administración de Azure AD, vea [Administración de los nombres de dominio personalizados en Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="065a7-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="065a7-107">Usuarios sincronizados desde un directorio local</span><span class="sxs-lookup"><span data-stu-id="065a7-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="065a7-108">Si ya estableció una conexión entre su instancia de Active Directory local y Azure Active Directory, puede rellenar las cuentas mediante la sincronización.</span><span class="sxs-lookup"><span data-stu-id="065a7-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="065a7-109">Para más información sobre cómo sincronizar Azure Active Directory con su Active Directory local, consulte [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="065a7-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="065a7-110">Usuarios que se agregan y administran en la nube</span><span class="sxs-lookup"><span data-stu-id="065a7-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="065a7-111">Para cambiar el dominio de una cuenta de usuario existente:</span><span class="sxs-lookup"><span data-stu-id="065a7-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="065a7-112">Abra el Portal de Azure clásico con una cuenta de administrador global o administrador de usuarios.</span><span class="sxs-lookup"><span data-stu-id="065a7-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="065a7-113">Abra el directorio.</span><span class="sxs-lookup"><span data-stu-id="065a7-113">Open your directory.</span></span>
3. <span data-ttu-id="065a7-114">Seleccione la pestaña **Usuarios** .</span><span class="sxs-lookup"><span data-stu-id="065a7-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="065a7-115">Seleccione el usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="065a7-115">Select the user from the list.</span></span>
5. <span data-ttu-id="065a7-116">Cambie el dominio del usuario y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="065a7-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="065a7-117">Esto también puede hacerse con [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) o la [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="065a7-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="065a7-118">Selección de un dominio personalizado al crear un nuevo usuario</span><span class="sxs-lookup"><span data-stu-id="065a7-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="065a7-119">Abra el Portal de Azure clásico con una cuenta de administrador global o administrador de usuarios.</span><span class="sxs-lookup"><span data-stu-id="065a7-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="065a7-120">Abra el directorio.</span><span class="sxs-lookup"><span data-stu-id="065a7-120">Open your directory.</span></span>
3. <span data-ttu-id="065a7-121">Seleccione la pestaña **Usuarios** .</span><span class="sxs-lookup"><span data-stu-id="065a7-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="065a7-122">En la barra de comandos, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="065a7-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="065a7-123">Cuando agregue el nombre de usuario, elija el dominio personalizado de la lista de dominios.</span><span class="sxs-lookup"><span data-stu-id="065a7-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="065a7-124">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="065a7-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="065a7-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="065a7-125">Next steps</span></span>
* [<span data-ttu-id="065a7-126">Using custom domain names to simplify the sign-in experience for your users (Uso de nombres de dominio personalizado para simplificar la experiencia de inicio de sesión para los usuarios)</span><span class="sxs-lookup"><span data-stu-id="065a7-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="065a7-127">Managing custom domain names (Administración de nombres de dominio).</span><span class="sxs-lookup"><span data-stu-id="065a7-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="065a7-128">Información general conceptual de nombres de dominio personalizado en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="065a7-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

