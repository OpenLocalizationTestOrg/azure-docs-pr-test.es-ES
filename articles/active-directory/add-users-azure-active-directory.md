---
title: aaaAdd nuevos usuarios tooAzure Active Directory | Documentos de Microsoft
description: "Explica cómo tooadd nuevos usuarios en Azure Active Directory."
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
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="40465-103">Inicio rápido: Agregar nuevos usuarios tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40465-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="40465-104">Este artículo explica cómo tooadd nuevos usuarios de su organización en Azure Active Directory (Azure AD) Hola uno a la vez mediante el portal de Azure de Hola o mediante la sincronización, el usuario de Windows Server AD local datos de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="40465-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="40465-105">Adición de usuarios basados en la nube</span><span class="sxs-lookup"><span data-stu-id="40465-105">Add cloud-based users</span></span>
1. <span data-ttu-id="40465-106">Inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="40465-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="40465-107">Seleccione **Azure Active Directory** y, después, **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="40465-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="40465-108">En hello **usuarios y grupos** hoja, seleccione **todos los usuarios**y, a continuación, seleccione **nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="40465-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="40465-109">![Al seleccionar el comando Add Hola](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="40465-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="40465-110">Escriba los detalles de usuario de hello, como **nombre** y **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="40465-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="40465-111">Hello parte del nombre de dominio del nombre de usuario de hello debe estar Hola predeterminado inicial dominio nombre ".onmicrosoft.com [nombre de dominio]" o comprobado, no federadas [nombre de dominio personalizado](add-custom-domain.md) como "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="40465-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="40465-112">Copia o en caso contrario hello de nota contraseña generada por el usuario para que puede proporcionarlo toohello usuario una vez completado este proceso.</span><span class="sxs-lookup"><span data-stu-id="40465-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="40465-113">Si lo desea, puede abrir y rellene la información de Hola Hola **perfil** hoja, hello **grupos** hoja o hello **rol del directorio** hoja para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="40465-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="40465-114">Para obtener más información acerca de los roles del usuario y el administrador, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="40465-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="40465-115">En hello **usuario** hoja, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="40465-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="40465-116">Distribuir segura Hola genera contraseña toohello nuevo usuario, para que hello usuario puede iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="40465-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="40465-117">También puede sincronizar datos de las cuentas de usuario desde una instancia local de Windows Server AD.</span><span class="sxs-lookup"><span data-stu-id="40465-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="40465-118">Soluciones de identidad de Microsoft abarcan local y capacidades en la nube, crear una identidad de usuario único para la autenticación y autorización de recursos de tooall, independientemente de su ubicación.</span><span class="sxs-lookup"><span data-stu-id="40465-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="40465-119">A esto le llamamos identidad híbrida.</span><span class="sxs-lookup"><span data-stu-id="40465-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="40465-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) puede ser usado toointegrate sus directorios locales con Azure Active Directory para los escenarios de identidad híbrida.</span><span class="sxs-lookup"><span data-stu-id="40465-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="40465-121">Esto le permite tooprovide una identidad común para los usuarios para las aplicaciones de Office 365, Azure y SaaS integrada con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40465-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="40465-122">Eliminación de usuarios desde Azure AD</span><span class="sxs-lookup"><span data-stu-id="40465-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="40465-123">Inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="40465-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="40465-124">Seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="40465-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="40465-125">En hello **usuarios y grupos** hoja, seleccione Hola usuario toodelete de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="40465-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="40465-126">En la hoja de hello para el usuario seleccionado de hello, seleccione **Introducción**y, a continuación, en la barra de comandos de hello, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="40465-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="40465-127">![Al seleccionar el comando Add Hola](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="40465-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="40465-128">Más información</span><span class="sxs-lookup"><span data-stu-id="40465-128">Learn more</span></span> 
* [<span data-ttu-id="40465-129">Agregar un usuario externo</span><span class="sxs-lookup"><span data-stu-id="40465-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="40465-130">Asignar un rol de usuario tooa en Azure AD</span><span class="sxs-lookup"><span data-stu-id="40465-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="40465-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="40465-131">Next steps</span></span>
<span data-ttu-id="40465-132">En este tutorial, ha aprendido cómo tooadd nuevos usuarios tooAzure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="40465-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="40465-133">Puede usar Hola siguiendo el vínculo toocreate un nuevo usuario en Azure AD de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="40465-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="40465-134">Agregar usuarios tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="40465-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
