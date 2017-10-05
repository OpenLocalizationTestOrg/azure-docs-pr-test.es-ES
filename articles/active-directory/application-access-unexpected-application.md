---
title: "Aplicación inesperada en mi lista de aplicaciones | Microsoft Docs"
description: "Cómo ver todas las aplicaciones de su inquilino y comprender cómo aparecen estas en la lista Todas las aplicaciones en Aplicaciones empresariales"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0f8136cb066fa6e3e4a8dd06e34b9f866e3916f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="e272c-103">Aplicación inesperada en mi lista de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e272c-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="e272c-104">Este artículo le ayudará comprender cómo aparecen las aplicaciones en la lista **Todas las aplicaciones** en **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e272c-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="e272c-105">Visualización de todas las aplicaciones del inquilino</span><span class="sxs-lookup"><span data-stu-id="e272c-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="e272c-106">Para ver todas las aplicaciones de su inquilino, debe usar el **Filtro** control para que aparezcan **todas las aplicaciones** en la lista **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e272c-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="e272c-107">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e272c-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="e272c-108">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="e272c-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e272c-109">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="e272c-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e272c-110">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e272c-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e272c-111">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e272c-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e272c-112">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e272c-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="e272c-113">Haga clic en el control **Filtro** en la parte superior de la **lista Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e272c-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="e272c-114">En la hoja **Filtrar**, establezca la opción **Mostrar** en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e272c-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="e272c-115">¿Por qué aparece una aplicación específica en mi lista de todas las aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="e272c-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="e272c-116">Cuando se filtra por **todas las aplicaciones**, la **lista** **Todas las aplicaciones** muestra todos los objetos de entidad de servicio del inquilino.</span><span class="sxs-lookup"><span data-stu-id="e272c-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="e272c-117">Los objetos de entidad de servicio pueden aparecer en esta lista de varias formas:</span><span class="sxs-lookup"><span data-stu-id="e272c-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="e272c-118">Cuando agrega cualquier aplicación desde la galería de aplicaciones, incluidas:</span><span class="sxs-lookup"><span data-stu-id="e272c-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="e272c-119">**Aplicaciones de la Galería de Azure AD**: una aplicación que se ha integrado previamente para el inicio de sesión único con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e272c-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="e272c-120">**Aplicaciones de proxy de aplicación**: una aplicación que se ejecuta en su entorno local en la que quiere que se proporcione inicio de sesión seguro externamente.</span><span class="sxs-lookup"><span data-stu-id="e272c-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="e272c-121">**Aplicaciones personalizadas**: una aplicación que su organización desea desarrollar en la plataforma de desarrollo de aplicaciones de Azure AD, pero que no existe aún.</span><span class="sxs-lookup"><span data-stu-id="e272c-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="e272c-122">**Aplicaciones que no son de la Galería**: ¡traiga sus propias aplicaciones!</span><span class="sxs-lookup"><span data-stu-id="e272c-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="e272c-123">Cualquier vínculo web, o cualquier aplicación que represente un campo de nombre de usuario y contraseña, admita los protocolos SAML u OpenID Connect, o admita SCIM, que quiera integrar para el inicio de sesión único con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e272c-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="e272c-124">Al registrarse o iniciar sesión en una aplicación de <sup>terceros</sup> integrada con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e272c-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="e272c-125">Un ejemplo de esto es [Smartsheet](https://app.smartsheet.com/b/home) o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="e272c-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="e272c-126">Al registrarse o agregar una licencia a un usuario o un grupo para una aplicación original de Microsoft, como puede ser [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="e272c-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="e272c-127">Al agregar un nuevo registro de aplicación mediante la creación de una aplicación desarrollada de forma personalizada con el [Registro de aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="e272c-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="e272c-128">Al agregar un nuevo registro de aplicación mediante la creación de una aplicación desarrollada de forma personalizada con el [Portal de registro de aplicaciones V2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="e272c-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="e272c-129">Al agregar una aplicación que está desarrollando con los [métodos de autenticación de ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) o los [servicios conectados](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e272c-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="e272c-130">Al crear un objeto de entidad de servicio mediante el [módulo de PowerShell de Azure AD](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="e272c-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="e272c-131">Al [dar su consentimiento a una aplicación](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) como administrador para utilizar datos de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="e272c-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="e272c-132">Cuando un [usuario da su consentimiento a una aplicación](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) para utilizar datos de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="e272c-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="e272c-133">Al habilitar determinados servicios que almacenan datos en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="e272c-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="e272c-134">Un ejemplo de esto es Password Reset, que se modela como entidad de servicio para almacenar la directiva de restablecimiento de contraseña de forma segura.</span><span class="sxs-lookup"><span data-stu-id="e272c-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="e272c-135">Para obtener más detalles sobre cómo las aplicaciones se agregan a su directorio, lea [Cómo y por qué se agregan aplicaciones a Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="e272c-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="e272c-136">Deseo quitar la asignación de un usuario o grupo específicos a una aplicación</span><span class="sxs-lookup"><span data-stu-id="e272c-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="e272c-137">Para quitar la asignación de un usuario o grupo a una aplicación, siga los pasos indicados en el artículo [Eliminación de asignaciones de usuario o grupo de una aplicación empresarial en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="e272c-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="e272c-138">Quiero deshabilitar el acceso a una aplicación para todos los usuarios</span><span class="sxs-lookup"><span data-stu-id="e272c-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="e272c-139">Para deshabilitar todos los inicios de sesión de usuarios a una aplicación, siga los pasos indicados en el artículo [Deshabilitación de los inicios de sesión de usuario de una aplicación empresarial en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="e272c-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="e272c-140">Quiero eliminar una aplicación por completo</span><span class="sxs-lookup"><span data-stu-id="e272c-140">I want to delete an application entirely</span></span>

<span data-ttu-id="e272c-141">Para **eliminar una aplicación**, siga las instrucciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="e272c-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="e272c-142">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="e272c-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e272c-143">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="e272c-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e272c-144">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e272c-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e272c-145">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e272c-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e272c-146">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e272c-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e272c-147">Si no ve que la aplicación que desea aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e272c-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e272c-148">Seleccione la aplicación que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="e272c-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="e272c-149">Una vez que se carga la aplicación, haga clic en el icono **Eliminar** de la hoja **Introducción** de la aplicación situada en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="e272c-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="e272c-150">Quiero deshabilitar todas las operaciones de consentimiento de usuario futuras para todas las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e272c-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="e272c-151">Deshabilitar el consentimiento del usuario para todo el directorio impide que los usuarios finales den consentimiento a cualquier aplicación.</span><span class="sxs-lookup"><span data-stu-id="e272c-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="e272c-152">A pesar de ello, los administradores podrán seguir dando el consentimiento en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e272c-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="e272c-153">Para más información sobre el consentimiento de aplicación y los motivos por los que es posible que quiera o no quiera hacer esto, lea el artículo [Descripción del consentimiento de usuario y administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="e272c-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="e272c-154">Para **deshabilitar todas las operaciones de consentimiento de usuario futuras en todo el directorio**, siga las instrucciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="e272c-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="e272c-155">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="e272c-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e272c-156">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="e272c-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e272c-157">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e272c-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e272c-158">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="e272c-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="e272c-159">Haga clic en **Configuración de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e272c-159">click **User settings**.</span></span>

6.  <span data-ttu-id="e272c-160">Deshabilite todas las operaciones de consentimiento de usuario futuras estableciendo la opción **Los usuarios pueden permitir que las aplicaciones accedan a sus datos** en **No**. Después, haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e272c-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e272c-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e272c-161">Next steps</span></span>
[<span data-ttu-id="e272c-162">Administración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e272c-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
