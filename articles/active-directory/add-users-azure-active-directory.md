---
title: "Incorporación de nuevos usuarios en Azure Active Directory | Microsoft Docs"
description: Describe como agregar usuarios nuevos en Azure Active Directory.
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="4a402-103">Inicio rápido: incorporación de nuevos usuarios a Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a402-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="4a402-104">En este artículo se explica cómo agregar nuevos usuarios de su organización en Azure Active Directory (Azure AD) de uno en uno mediante Azure Portal o mediante la sincronización de los datos de las cuentas de usuario de Windows Server AD locales.</span><span class="sxs-lookup"><span data-stu-id="4a402-104">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) one at a time using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="4a402-105">Adición de usuarios basados en la nube</span><span class="sxs-lookup"><span data-stu-id="4a402-105">Add cloud-based users</span></span>
1. <span data-ttu-id="4a402-106">Inicie sesión en el [Centro de administración de Azure Active Directory](https://aad.portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="4a402-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="4a402-107">Seleccione **Azure Active Directory** y, después, **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4a402-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="4a402-108">En la hoja **Usuarios y grupos**, seleccione **Todos los grupos** y, luego, **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="4a402-108">On the **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="4a402-109">![Selección del comando Agregar](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="4a402-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="4a402-110">Especifique los detalles del usuario, como el **nombre** y el **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="4a402-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="4a402-111">La parte del nombre de dominio del nombre de usuario debe ser el nombre de dominio del nombre de dominio predeterminado inicial "[nombre de dominio].onmicrosoft.com" o un [nombre de dominio personalizado](add-custom-domain.md) comprobado y no federado, como "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="4a402-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="4a402-112">Copie o anote la contraseña de usuario generada para poder proporcionársela al usuario cuando finalice este proceso.</span><span class="sxs-lookup"><span data-stu-id="4a402-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="4a402-113">También puede abrir y rellenar la información de las hojas **Perfil**, **Grupos** o **Rol del directorio** del usuario.</span><span class="sxs-lookup"><span data-stu-id="4a402-113">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="4a402-114">Para obtener más información acerca de los roles del usuario y el administrador, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4a402-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="4a402-115">En la hoja **Usuario**, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4a402-115">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="4a402-116">Distribuya de manera segura la contraseña generada al nuevo usuario para que pueda iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="4a402-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="4a402-117">También puede sincronizar datos de las cuentas de usuario desde una instancia local de Windows Server AD.</span><span class="sxs-lookup"><span data-stu-id="4a402-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="4a402-118">Las soluciones de identidad de Microsoft abarcan funcionalidades locales y de nube, de forma que se crea una sola identidad de usuario para la autenticación y la autorización en todos los recursos, sin importar su ubicación.</span><span class="sxs-lookup"><span data-stu-id="4a402-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="4a402-119">A esto le llamamos identidad híbrida.</span><span class="sxs-lookup"><span data-stu-id="4a402-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="4a402-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) se puede usar para integrar directorios locales con Azure Active Directory para obtener escenarios de identidad híbridos.</span><span class="sxs-lookup"><span data-stu-id="4a402-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="4a402-121">Esto le permite proporcionar una identidad común para los usuarios de aplicaciones de Office 365, Azure y SaaS integradas con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a402-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="4a402-122">Eliminación de usuarios desde Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a402-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="4a402-123">Inicie sesión en el [Centro de administración de Azure Active Directory](https://aad.portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="4a402-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="4a402-124">Seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4a402-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="4a402-125">En la hoja **Usuarios y grupos**, seleccione el usuarios que va a eliminar de la lista.</span><span class="sxs-lookup"><span data-stu-id="4a402-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="4a402-126">En la hoja del usuario seleccionado, seleccione **Información general** y, después, en la barra de comandos, seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="4a402-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="4a402-127">![Selección del comando Agregar](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="4a402-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="4a402-128">Más información</span><span class="sxs-lookup"><span data-stu-id="4a402-128">Learn more</span></span> 
* [<span data-ttu-id="4a402-129">Agregar un usuario externo</span><span class="sxs-lookup"><span data-stu-id="4a402-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="4a402-130">Asignar a un usuario a un rol de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a402-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="4a402-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a402-131">Next steps</span></span>
<span data-ttu-id="4a402-132">En esta guía de inicio rápido, ha aprendido a agregar usuarios nuevos a Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="4a402-132">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="4a402-133">Puede usar el vínculo siguiente para crear un usuario nuevo en Azure AD desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4a402-133">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a402-134">Adición de usuarios a Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a402-134">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 