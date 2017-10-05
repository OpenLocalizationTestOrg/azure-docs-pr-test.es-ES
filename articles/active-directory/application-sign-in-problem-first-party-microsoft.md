---
title: "Problemas de inicio de sesión en una aplicación de Microsoft | Microsoft Docs"
description: "Solución de problemas comunes que aparecen al iniciar sesión en aplicaciones propias de Microsoft mediante Azure AD (por ejemplo, Office 365)"
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
ms.openlocfilehash: 5638434270ee82d2b9737ea8eed8b5a8c62f7121
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
## <a name="problems-signing-in-to-a-microsoft-application"></a><span data-ttu-id="fca34-103">Problemas de inicio de sesión en una aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fca34-103">Problems signing in to a Microsoft application</span></span>

<span data-ttu-id="fca34-104">Las aplicaciones de Microsoft (como Office 365 Exchange, SharePoint, Yammer, etc.) se asignan y administran de manera algo diferente que las aplicaciones SaaS de terceros u otras aplicaciones que integra con Azure AD para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fca34-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="fca34-105">Hay tres maneras principales en que un usuario puede acceder a una aplicación publicada por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fca34-105">There are three main ways that a user can get access to a Microsoft-published application.</span></span>

-   <span data-ttu-id="fca34-106">En el caso de aplicaciones de Office 365 u otros conjuntos de aplicaciones de pago, a los usuarios se les concede acceso mediante la **asignación de licencias** o mediante la funcionalidad de asignación de licencias basada en grupo.</span><span class="sxs-lookup"><span data-stu-id="fca34-106">For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="fca34-107">Para aplicaciones que Microsoft o un tercero publica de manera gratuita para que todo el mundo las use, a los usuarios se les puede conceder acceso mediante **consentimiento del usuario**.</span><span class="sxs-lookup"><span data-stu-id="fca34-107">For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**.</span></span> <span data-ttu-id="fca34-108">Esto significa que inician sesión en la aplicación con su cuenta profesional o educativa de Azure AD, que les permite tener acceso a un conjunto limitado de datos en sus cuentas.</span><span class="sxs-lookup"><span data-stu-id="fca34-108">This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.</span></span>

-   <span data-ttu-id="fca34-109">Además, para aplicaciones que Microsoft o un tercero publica de manera gratuita para que todo el mundo las use, a los usuarios se les puede conceder acceso mediante **consentimiento del administrador**.</span><span class="sxs-lookup"><span data-stu-id="fca34-109">For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="fca34-110">Esto significa que un administrador ha determinado que todos los miembros de la organización pueden usar la aplicación, por lo que inicia sesión en la aplicación con una cuenta de administrador global y concede acceso a todos ellos.</span><span class="sxs-lookup"><span data-stu-id="fca34-110">This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.</span></span>

<span data-ttu-id="fca34-111">Para solucionar el problema, comience con [Áreas problemáticas generales con el acceso a las aplicaciones para tener en cuenta](#general-problem-areas-with-application-access-to-consider) y luego lea el documento [Tutorial: Pasos para solucionar problemas de acceso a las aplicaciones de Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="fca34-111">To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.</span></span>

## <a name="general-problem-areas-with-application-access-to-consider"></a><span data-ttu-id="fca34-112">Áreas problemáticas generales con el acceso a las aplicaciones para tener en cuenta</span><span class="sxs-lookup"><span data-stu-id="fca34-112">General Problem Areas with Application Access to consider</span></span>

<span data-ttu-id="fca34-113">Aquí tiene una lista de las áreas problemáticas generales en las que puede profundizar si sabe por dónde empezar. Para una introducción rápida, le recomendamos que lea [Tutorial: Pasos para solucionar problemas de acceso a las aplicaciones de Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="fca34-113">Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="fca34-114">Problemas con la cuenta del usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-114">Problems with the user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="fca34-115">Problemas con grupos</span><span class="sxs-lookup"><span data-stu-id="fca34-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="fca34-116">Problemas con las directivas de acceso condicional</span><span class="sxs-lookup"><span data-stu-id="fca34-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="fca34-117">Problemas con el consentimiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="fca34-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-to-troubleshoot-microsoft-application-access"></a><span data-ttu-id="fca34-118">Pasos para solucionar problemas de acceso a las aplicaciones de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fca34-118">Steps to troubleshoot Microsoft Application access</span></span>

<span data-ttu-id="fca34-119">Estos son algunos problemas comunes que pueden surgir cuando los usuarios no pueden iniciar sesión en una aplicación de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fca34-119">Below are some common issues folks run into when their users cannot sign in to a Microsoft application.</span></span>

-   <span data-ttu-id="fca34-120">Problemas generales para comprobar primero</span><span class="sxs-lookup"><span data-stu-id="fca34-120">General issues to check first</span></span>

  * <span data-ttu-id="fca34-121">Asegurarse de que el usuario inicia sesión en la **dirección URL correcta** y no en la dirección URL de la aplicación local</span><span class="sxs-lookup"><span data-stu-id="fca34-121">Make sure the user is signing in to the **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="fca34-122">Asegurarse de que la cuenta del usuario **no esté bloqueada**</span><span class="sxs-lookup"><span data-stu-id="fca34-122">Make sure the user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="fca34-123">Asegurarse de que la **cuenta del usuario exista** en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fca34-123">Make sure the **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="fca34-124">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fca34-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="fca34-125">Asegurarse de que la cuenta del usuario está **habilitada** para los inicios de sesión</span><span class="sxs-lookup"><span data-stu-id="fca34-125">Make sure the user’s account is **enabled** for sign ins.</span></span> [<span data-ttu-id="fca34-126">Comprobar el estado de la cuenta de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-126">Check a user’s account status</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="fca34-127">Asegurarse de que la **contraseña del usuario no haya expirado o se haya olvidado**</span><span class="sxs-lookup"><span data-stu-id="fca34-127">Make sure the user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="fca34-128">[Restablecer la contraseña del usuario](#reset-a-users-password) o [habilitar el autoservicio de restablecimiento de contraseña](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="fca34-128">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="fca34-129">Asegurarse de que **Multi-Factor Authentication** no bloquee el acceso del usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-129">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="fca34-130">[Comprobar el estado de la autenticación multifactor de un usuario](#check-a-users-multi-factor-authentication-status) o [comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="fca34-130">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="fca34-131">Asegurarse de que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquee el acceso del usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-131">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="fca34-132">[Comprobar una directiva de acceso condicional específica](#problems-with-conditional-access-policies) o [comprobar la directiva de acceso condicional de una aplicación específica](#check-a-specific-applications-conditional-access-policy) o [deshabilitar una directiva de acceso condicional específica](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="fca34-132">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="fca34-133">Asegurarse de que la **información de contacto de autenticación** del usuario esté actualizada para permitir la aplicación de directivas de Multi-Factor Authentication o de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="fca34-133">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span> <span data-ttu-id="fca34-134">[Comprobar el estado de la autenticación multifactor de un usuario](#check-a-users-multi-factor-authentication-status) o [comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="fca34-134">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="fca34-135">Para aplicaciones de **Microsoft** **que necesitan una licencia** (como Office365), estos son algunos problemas específicos que se deben comprobar una vez que haya descartado los problemas generales mencionados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="fca34-135">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:</span></span>

   * <span data-ttu-id="fca34-136">Asegurarse de que el usuario tenga una **licencia asignada**</span><span class="sxs-lookup"><span data-stu-id="fca34-136">Ensure the user or has a **license assigned.**</span></span> <span data-ttu-id="fca34-137">[Comprobar las licencias asignadas de un usuario](#check-a-users-assigned-licenses) o [comprobar licencias asignadas de un grupo](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="fca34-137">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="fca34-138">Si la licencia está **asignada a un** **grupo estático**, asegúrese de que el **usuario sea miembro** de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="fca34-138">If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group.</span></span> [<span data-ttu-id="fca34-139">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-139">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="fca34-140">Si la licencia está **asignada a un** **grupo dinámico**, asegúrese de que la **regla del grupo dinámico se haya establecido correctamente**.</span><span class="sxs-lookup"><span data-stu-id="fca34-140">If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="fca34-141">Comprobar los criterios de pertenencia de un grupo dinámico</span><span class="sxs-lookup"><span data-stu-id="fca34-141">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="fca34-142">Si la licencia está **asignada a un** **grupo dinámico**, asegúrese de que el grupo dinámico haya **terminado de procesar** su pertenencia y que el **usuario sea miembro** (esta operación puede tardar un rato).</span><span class="sxs-lookup"><span data-stu-id="fca34-142">If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time).</span></span> [<span data-ttu-id="fca34-143">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-143">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="fca34-144">Una vez que se haya asegurado de que la licencia está asignada, compruebe que esta **no haya caducado**.</span><span class="sxs-lookup"><span data-stu-id="fca34-144">Once you make sure the license is assigned, make sure the license is **not expired**.</span></span>

   *  <span data-ttu-id="fca34-145">Asegurarse de que la licencia **corresponde a la aplicación** para la que desean acceso.</span><span class="sxs-lookup"><span data-stu-id="fca34-145">Make sure the license is **for the application** they are accessing.</span></span>

-   <span data-ttu-id="fca34-146">Para aplicaciones de **Microsoft** **que no necesitan licencia**, estos son algunos otros puntos para comprobar:</span><span class="sxs-lookup"><span data-stu-id="fca34-146">For **Microsoft** **applications that don’t require a license**, here are some other things to check:</span></span>

   * <span data-ttu-id="fca34-147">Si la aplicación solicita **permisos de nivel de usuario** (por ejemplo, acceso al buzón de este usuario), asegúrese de que el usuario ha iniciado sesión en la aplicación y ha realizado una **operación de consentimiento de nivel de usuario** para permitir que la aplicación acceda a sus datos.</span><span class="sxs-lookup"><span data-stu-id="fca34-147">If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.</span></span>

   * <span data-ttu-id="fca34-148">Si la aplicación solicita **permisos de nivel de administrador** (por ejemplo, acceso a los buzones de todos los usuarios), asegúrese de que un administrador global haya realizado una **operación de consentimiento de nivel de administrador en nombre de todos los usuarios** de la organización.</span><span class="sxs-lookup"><span data-stu-id="fca34-148">If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.</span></span>

## <a name="problems-with-the-users-account"></a><span data-ttu-id="fca34-149">Problemas con la cuenta del usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-149">Problems with the user’s account</span></span>

<span data-ttu-id="fca34-150">El acceso a la aplicación se puede bloquear debido a un problema con un usuario que se asigna a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fca34-150">Application access can be blocked due to a problem with a user that is assigned to the application.</span></span> <span data-ttu-id="fca34-151">A continuación se muestran algunas maneras de solucionar problemas con los usuarios y la configuración de sus cuentas:</span><span class="sxs-lookup"><span data-stu-id="fca34-151">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="fca34-152">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fca34-152">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="fca34-153">Comprobar el estado de la cuenta de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-153">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="fca34-154">Restablecer la contraseña de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-154">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="fca34-155">Habilitar el autoservicio de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="fca34-155">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="fca34-156">Comprobar el estado de la autenticación multifactor de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-156">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="fca34-157">Comprobar la información de contacto de autenticación de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-157">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="fca34-158">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-158">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="fca34-159">Comprobar las licencias asignadas de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-159">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="fca34-160">Asignar una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-160">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="fca34-161">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fca34-161">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="fca34-162">Para comprobar si una cuenta de usuario existe, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-162">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-163">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-163">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-164">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-164">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-165">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-165">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-166">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-166">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-167">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-167">click **All users**.</span></span>

6.  <span data-ttu-id="fca34-168">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-168">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-169">Compruebe las propiedades del objeto de usuario para asegurarse de que se muestran como esperaba y no falta ningún dato.</span><span class="sxs-lookup"><span data-stu-id="fca34-169">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="fca34-170">Comprobar el estado de la cuenta de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-170">Check a user’s account status</span></span>

<span data-ttu-id="fca34-171">Para comprobar el estado de la cuenta de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-171">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-172">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-172">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-173">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-173">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-174">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-174">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-175">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-175">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-176">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-176">click **All users**.</span></span>

6.  <span data-ttu-id="fca34-177">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-177">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-178">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="fca34-178">click **Profile**.</span></span>

8.  <span data-ttu-id="fca34-179">En **Configuración**, asegúrese de que **Bloquear inicio de sesión** esté establecido en **No**.</span><span class="sxs-lookup"><span data-stu-id="fca34-179">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="fca34-180">Restablecer la contraseña de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-180">Reset a user’s password</span></span>

<span data-ttu-id="fca34-181">Para restablecer la contraseña de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-181">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-182">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-183">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-184">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-185">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-186">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-186">click **All users**.</span></span>

6.  <span data-ttu-id="fca34-187">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-187">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-188">Haga clic en el botón **Restablecer contraseña** situado en la parte superior de la hoja de usuario.</span><span class="sxs-lookup"><span data-stu-id="fca34-188">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="fca34-189">Haga clic en el botón **Restablecer contraseña** en la hoja **Restablecer contraseña** que aparece.</span><span class="sxs-lookup"><span data-stu-id="fca34-189">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="fca34-190">Copie la **contraseña temporal** o **escriba una contraseña nueva** para el usuario.</span><span class="sxs-lookup"><span data-stu-id="fca34-190">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="fca34-191">Comunique esta nueva contraseña al usuario, quien deberá cambiarla durante el siguiente inicio de sesión en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fca34-191">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="fca34-192">Habilitar el autoservicio de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="fca34-192">Enable self-service password reset</span></span>

<span data-ttu-id="fca34-193">Para habilitar el autoservicio de restablecimiento de contraseña, siga estos pasos de implementación:</span><span class="sxs-lookup"><span data-stu-id="fca34-193">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="fca34-194">Permitir que los usuarios restablezcan sus contraseñas de Azure AD
</span><span class="sxs-lookup"><span data-stu-id="fca34-194">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="fca34-195">Permitir que los usuarios restablezcan o cambien sus contraseñas de AD locales</span><span class="sxs-lookup"><span data-stu-id="fca34-195">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="fca34-196">Comprobar el estado de la autenticación multifactor de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-196">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="fca34-197">Para comprobar el estado de la autenticación multifactor de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-197">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-198">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-199">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-200">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-201">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-201">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-202">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-202">click **All users**.</span></span>

6.  <span data-ttu-id="fca34-203">Haga clic en el botón **Multi-Factor Authentication** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="fca34-203">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="fca34-204">Después de que se ha cargado el **Portal de administración de Multi-factor Authentication**, asegúrese de que se encuentra en la pestaña **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-204">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="fca34-205">Para encontrar el usuario, filtre u ordene la lista de usuarios, o realice búsquedas en ella.</span><span class="sxs-lookup"><span data-stu-id="fca34-205">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="fca34-206">Seleccione el usuario en la lista y elija **Habilitar**, **Deshabilitar** o **Forzar** la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="fca34-206">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="fca34-207">**Nota**: Si un usuario se encuentra en un estado **Forzado**, puede establecerlo en **Deshabilitado** temporalmente para permitirle volver a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="fca34-207">**Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="fca34-208">Una vez de vuelta, puede cambiar de nuevo su estado a **Habilitado** para solicitarle que vuelva a registrar su información de contacto durante su siguiente inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="fca34-208">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="fca34-209">Como alternativa, puede seguir los pasos descritos en [Comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info) para comprobar o establecer estos datos por ellos.</span><span class="sxs-lookup"><span data-stu-id="fca34-209">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="fca34-210">Comprobar la información de contacto de autenticación de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-210">Check a user’s authentication contact info</span></span>

<span data-ttu-id="fca34-211">Para comprobar la información de contacto de autenticación de un usuario para Multi-factor Authentication, acceso condicional y protección de identidad, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-211">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-212">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-212">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-213">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-213">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-214">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-214">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-215">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-215">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-216">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-216">click **All users**.</span></span>

6.  <span data-ttu-id="fca34-217">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-217">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-218">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="fca34-218">click **Profile**.</span></span>

8.  <span data-ttu-id="fca34-219">Desplácese hacia abajo hasta **Información de contacto para la autenticación**.</span><span class="sxs-lookup"><span data-stu-id="fca34-219">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="fca34-220">**Revise** los datos registrados para el usuario y actualícelos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="fca34-220">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="fca34-221">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-221">Check a user’s group memberships</span></span>

<span data-ttu-id="fca34-222">Para comprobar la pertenencia a grupos de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-222">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-223">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-223">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-224">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-224">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-225">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-225">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-226">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-226">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-227">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-227">click **All users**.</span></span>

6.  <span data-ttu-id="fca34-228">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-228">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-229">Haga clic en **Grupos** para ver de qué grupos es miembro el usuario.</span><span class="sxs-lookup"><span data-stu-id="fca34-229">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="fca34-230">Comprobar las licencias asignadas de un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-230">Check a user’s assigned licenses</span></span>

<span data-ttu-id="fca34-231">Para comprobar las licencias asignadas de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-231">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-232">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-232">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-233">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-233">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-234">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-234">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-235">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-235">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-236">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-236">click **All users**.</span></span>

6.  <span data-ttu-id="fca34-237">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-237">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-238">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el usuario.</span><span class="sxs-lookup"><span data-stu-id="fca34-238">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="fca34-239">Asignar una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-239">Assign a user a license</span></span> 

<span data-ttu-id="fca34-240">Para asignar una licencia a un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-240">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-241">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-242">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-243">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-244">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-244">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-245">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-245">click **All users**.</span></span>

6.  <span data-ttu-id="fca34-246">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-246">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-247">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el usuario.</span><span class="sxs-lookup"><span data-stu-id="fca34-247">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="fca34-248">Haga clic en el botón **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="fca34-248">click the **Assign** button.</span></span>

9.  <span data-ttu-id="fca34-249">Seleccione **uno o más productos** en la lista de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="fca34-249">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="fca34-250">**Opcional**: Haga clic en el elemento **Opciones de asignación** para asignar productos de forma granular.</span><span class="sxs-lookup"><span data-stu-id="fca34-250">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="fca34-251">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fca34-251">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="fca34-252">Haga clic en el botón **Asignar** para asignar estas licencias a este usuario.</span><span class="sxs-lookup"><span data-stu-id="fca34-252">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="fca34-253">Problemas con grupos</span><span class="sxs-lookup"><span data-stu-id="fca34-253">Problems with groups</span></span>

<span data-ttu-id="fca34-254">El acceso a la aplicación se puede bloquear debido a un problema con un grupo que se asigna a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fca34-254">Application access can be blocked due to a problem with a group that is assigned to the application.</span></span> <span data-ttu-id="fca34-255">A continuación se muestran algunas maneras de solucionar problemas con grupos y pertenencias a grupos:</span><span class="sxs-lookup"><span data-stu-id="fca34-255">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="fca34-256">Comprobar la pertenencia de un grupo</span><span class="sxs-lookup"><span data-stu-id="fca34-256">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="fca34-257">Comprobar los criterios de pertenencia de un grupo dinámico</span><span class="sxs-lookup"><span data-stu-id="fca34-257">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="fca34-258">Comprobar las licencias asignadas de un grupo</span><span class="sxs-lookup"><span data-stu-id="fca34-258">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="fca34-259">Volver a procesar las licencias de un grupo</span><span class="sxs-lookup"><span data-stu-id="fca34-259">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="fca34-260">Asignar una licencia a un grupo</span><span class="sxs-lookup"><span data-stu-id="fca34-260">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="fca34-261">Comprobar la pertenencia de un grupo</span><span class="sxs-lookup"><span data-stu-id="fca34-261">Check a group’s membership</span></span>

<span data-ttu-id="fca34-262">Para comprobar la pertenencia de un grupo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-262">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-263">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-263">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-264">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-264">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-265">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-265">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-266">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-266">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-267">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="fca34-267">click **All groups**.</span></span>

6.  <span data-ttu-id="fca34-268">**Busque** el grupo en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-268">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-269">Haga clic en **Miembros** para revisar la lista de usuarios asignados a este grupo.</span><span class="sxs-lookup"><span data-stu-id="fca34-269">click **Members** to review the list of users assigned to this group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="fca34-270">Comprobar los criterios de pertenencia de un grupo dinámico</span><span class="sxs-lookup"><span data-stu-id="fca34-270">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="fca34-271">Para comprobar los criterios de pertenencia de un grupo dinámico, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-271">To check a dynamic group’s membership criteria, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-272">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-272">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-273">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-273">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-274">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-274">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-275">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-275">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-276">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="fca34-276">click **All groups**.</span></span>

6.  <span data-ttu-id="fca34-277">**Busque** el grupo en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-277">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-278">Haga clic en **Reglas de pertenencia dinámica**.</span><span class="sxs-lookup"><span data-stu-id="fca34-278">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="fca34-279">Revise la regla **simple** o **avanzada** definida para este grupo y asegúrese de que el usuario que va a ser miembro de este grupo cumpla estos criterios.</span><span class="sxs-lookup"><span data-stu-id="fca34-279">Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="fca34-280">Comprobar licencias asignadas de un grupo</span><span class="sxs-lookup"><span data-stu-id="fca34-280">Check a group’s assigned licenses</span></span>

<span data-ttu-id="fca34-281">Para comprobar las licencias asignadas de un grupo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-281">To check a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-282">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-282">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-283">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-283">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-284">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-284">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-285">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-285">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-286">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="fca34-286">click **All groups**.</span></span>

6.  <span data-ttu-id="fca34-287">**Busque** el grupo en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-287">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-288">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el grupo.</span><span class="sxs-lookup"><span data-stu-id="fca34-288">click **Licenses** to see which licenses the group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="fca34-289">Volver a procesar las licencias de un grupo</span><span class="sxs-lookup"><span data-stu-id="fca34-289">Reprocess a group’s licenses</span></span>

<span data-ttu-id="fca34-290">Para volver a procesar las licencias asignadas de un grupo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-290">To reprocess a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-291">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-292">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-293">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-294">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-294">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-295">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="fca34-295">click **All groups**.</span></span>

6.  <span data-ttu-id="fca34-296">**Busque** el grupo en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-296">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-297">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el grupo.</span><span class="sxs-lookup"><span data-stu-id="fca34-297">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="fca34-298">Haga clic en el botón **Reprocesar** para asegurarse de que las licencias asignadas a los miembros de este grupo están actualizadas.</span><span class="sxs-lookup"><span data-stu-id="fca34-298">click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date.</span></span> <span data-ttu-id="fca34-299">Esta operación puede tardar mucho tiempo, en función del tamaño y la complejidad del grupo.</span><span class="sxs-lookup"><span data-stu-id="fca34-299">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fca34-300">Para acelerar el proceso, considere la posibilidad de asignar temporalmente una licencia al usuario directamente.</span><span class="sxs-lookup"><span data-stu-id="fca34-300">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="fca34-301">[Asignar una licencia a un usuario](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="fca34-301">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="fca34-302">Asignar una licencia a un grupo</span><span class="sxs-lookup"><span data-stu-id="fca34-302">Assign a group a license</span></span>

<span data-ttu-id="fca34-303">Para asignar una licencia a un grupo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-303">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="fca34-304">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-304">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-305">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-305">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-306">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-306">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-307">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-307">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-308">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="fca34-308">click **All groups**.</span></span>

6.  <span data-ttu-id="fca34-309">**Busque** el grupo en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="fca34-309">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="fca34-310">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el grupo.</span><span class="sxs-lookup"><span data-stu-id="fca34-310">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="fca34-311">Haga clic en el botón **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="fca34-311">click the **Assign** button.</span></span>

9.  <span data-ttu-id="fca34-312">Seleccione **uno o más productos** en la lista de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="fca34-312">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="fca34-313">**Opcional**: Haga clic en el elemento **Opciones de asignación** para asignar productos de forma granular.</span><span class="sxs-lookup"><span data-stu-id="fca34-313">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="fca34-314">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fca34-314">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="fca34-315">Haga clic en el botón **Asignar** para asignar estas licencias a este grupo.</span><span class="sxs-lookup"><span data-stu-id="fca34-315">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="fca34-316">Esta operación puede tardar mucho tiempo, en función del tamaño y la complejidad del grupo.</span><span class="sxs-lookup"><span data-stu-id="fca34-316">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fca34-317">Para acelerar el proceso, considere la posibilidad de asignar temporalmente una licencia al usuario directamente.</span><span class="sxs-lookup"><span data-stu-id="fca34-317">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="fca34-318">[Asignar una licencia a un usuario](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="fca34-318">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="fca34-319">Problemas con las directivas de acceso condicional</span><span class="sxs-lookup"><span data-stu-id="fca34-319">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="fca34-320">Comprobar una directiva de acceso condicional específica</span><span class="sxs-lookup"><span data-stu-id="fca34-320">Check a specific conditional access policy</span></span>

<span data-ttu-id="fca34-321">Para comprobar o validar una directiva de acceso condicional:</span><span class="sxs-lookup"><span data-stu-id="fca34-321">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="fca34-322">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-322">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-323">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-323">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-324">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-324">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-325">Haga clic en **Aplicaciones empresariales** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-325">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-326">Haga clic en el elemento de navegación **Acceso condicional**.</span><span class="sxs-lookup"><span data-stu-id="fca34-326">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="fca34-327">Haga clic en la directiva que le interese inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="fca34-327">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="fca34-328">Revise que no haya condiciones, asignaciones u otras configuraciones específicas que puedan estar bloqueando el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="fca34-328">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fca34-329">Puede que desee deshabilitar temporalmente esta directiva para asegurarse de que no afecta a los inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="fca34-329">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="fca34-330">Para ello, establezca el botón de alternancia **Habilitar directiva** en **No** y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fca34-330">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="fca34-331">Comprobar la directiva de acceso condicional de una aplicación específica</span><span class="sxs-lookup"><span data-stu-id="fca34-331">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="fca34-332">Para comprobar o validar la directiva de acceso condicional configurada actualmente de una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fca34-332">To check or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="fca34-333">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-333">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-334">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-334">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-335">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-335">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-336">Haga clic en **Aplicaciones empresariales** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-336">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-337">A continuación, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fca34-337">click **All applications**.</span></span>

6.  <span data-ttu-id="fca34-338">Busque la aplicación que le interesa o en la que el usuario intenta iniciar sesión por el nombre para mostrar o el id. de aplicación.</span><span class="sxs-lookup"><span data-stu-id="fca34-338">Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="fca34-339">Si no ve la aplicación que busca, haga clic en el botón **Filtrar** y amplíe el ámbito de la lista a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fca34-339">If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**.</span></span> <span data-ttu-id="fca34-340">Si desea ver más columnas, haga clic en el botón **Columnas** para agregar detalles adicionales para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fca34-340">If you want to see more columns, click the **Columns** button to add additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="fca34-341">Haga clic en el elemento de navegación **Acceso condicional**.</span><span class="sxs-lookup"><span data-stu-id="fca34-341">click the **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="fca34-342">Haga clic en la directiva que le interese inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="fca34-342">click the policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="fca34-343">Revise que no haya condiciones, asignaciones u otras configuraciones específicas que puedan estar bloqueando el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="fca34-343">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="fca34-344">Puede que desee deshabilitar temporalmente esta directiva para asegurarse de que no afecta a los inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="fca34-344">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="fca34-345">Para ello, establezca el botón de alternancia **Habilitar directiva** en **No** y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fca34-345">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="fca34-346">Deshabilitar una directiva de acceso condicional específica</span><span class="sxs-lookup"><span data-stu-id="fca34-346">Disable a specific conditional access policy</span></span>

<span data-ttu-id="fca34-347">Para comprobar o validar una directiva de acceso condicional:</span><span class="sxs-lookup"><span data-stu-id="fca34-347">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="fca34-348">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="fca34-348">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fca34-349">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="fca34-349">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fca34-350">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca34-350">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fca34-351">Haga clic en **Aplicaciones empresariales** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="fca34-351">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="fca34-352">Haga clic en el elemento de navegación **Acceso condicional**.</span><span class="sxs-lookup"><span data-stu-id="fca34-352">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="fca34-353">Haga clic en la directiva que le interese inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="fca34-353">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="fca34-354">Para deshabilitar la directiva, establezca el botón de alternancia **Habilitar directiva** en **No** y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fca34-354">Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="fca34-355">Problemas con el consentimiento de aplicación</span><span class="sxs-lookup"><span data-stu-id="fca34-355">Problems with application consent</span></span>

<span data-ttu-id="fca34-356">El acceso a la aplicación se puede bloquear porque no se haya producido la operación de consentimiento de los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="fca34-356">Application access can be blocked because the proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="fca34-357">A continuación se muestran algunas maneras en que puede solucionar problemas relacionados con el consentimiento de aplicación:</span><span class="sxs-lookup"><span data-stu-id="fca34-357">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="fca34-358">Realizar una operación de consentimiento de nivel de usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-358">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="fca34-359">Realizar la operación de consentimiento de nivel de administrador para cualquier aplicación</span><span class="sxs-lookup"><span data-stu-id="fca34-359">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="fca34-360">Realizar el consentimiento de nivel de administrador para una aplicación de un solo inquilino</span><span class="sxs-lookup"><span data-stu-id="fca34-360">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="fca34-361">Realizar el consentimiento de nivel de administrador para una aplicación multiinquilino</span><span class="sxs-lookup"><span data-stu-id="fca34-361">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="fca34-362">Realizar una operación de consentimiento de nivel de usuario</span><span class="sxs-lookup"><span data-stu-id="fca34-362">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="fca34-363">Para cualquier aplicación compatible con Open ID Connect que solicite permisos, al navegar a la pantalla de inicio de sesión de la aplicación se realiza un consentimiento de nivel de usuario a la aplicación para el usuario que inició sesión.</span><span class="sxs-lookup"><span data-stu-id="fca34-363">For any Open ID Connect-enabled application that requests permissions, navigating to the application’s sign in screen performs a user level consent to the application for the signed-in user.</span></span>

-   <span data-ttu-id="fca34-364">Si desea realizar esto mediante programación, consulte [Solicitud de consentimiento de usuario individual](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="fca34-364">If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="fca34-365">Realizar la operación de consentimiento de nivel de administrador para cualquier aplicación</span><span class="sxs-lookup"><span data-stu-id="fca34-365">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="fca34-366">**Solo para las aplicaciones desarrolladas mediante el modelo de aplicación V1**, puede forzar que se produzca el consentimiento de nivel de administrador si agrega "**?prompt=admin\_consent**" al final de la dirección URL de inicio de sesión de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="fca34-366">For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="fca34-367">Para **todas las aplicaciones desarrolladas mediante el modelo de aplicación V2**, puede forzar que se produzca este consentimiento de nivel de administrador si sigue las instrucciones de la sección **Solicitud de los permisos de un administrador de directorios** de [Uso del punto de conexión de consentimiento del administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="fca34-367">For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="fca34-368">Realizar el consentimiento de nivel de administrador para una aplicación de un único inquilino</span><span class="sxs-lookup"><span data-stu-id="fca34-368">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="fca34-369">Con las **aplicaciones de un único inquilino** que solicitan permisos (por ejemplo, las que desarrolla o posee su organización), puede realizar una operación de **consentimiento de nivel administrativo** en nombre de todos los usuarios. Para ello, inicie sesión como administrador global y haga clic en el botón **Conceder permisos** de la parte superior de la hoja **Application Registry (Registro de aplicación) -&gt; Todas las aplicaciones -&gt; Select an App (Seleccionar una aplicación) - &gt; Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="fca34-369">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="fca34-370">Para **todas las aplicaciones desarrolladas mediante el modelo de aplicación V1 o V2**, puede forzar que se produzca este consentimiento de nivel de administrador si sigue las instrucciones de la sección **Solicitud de los permisos de un administrador de directorios** de [Uso del punto de conexión de consentimiento del administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="fca34-370">For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="fca34-371">Realizar el consentimiento de nivel de administrador para una aplicación multiinquilino</span><span class="sxs-lookup"><span data-stu-id="fca34-371">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="fca34-372">Para **aplicaciones multiinquilino** que solicitan permisos (como una aplicación que desarrolla un tercero o Microsoft), puede realizar una operación de **consentimiento de nivel administrativo**.</span><span class="sxs-lookup"><span data-stu-id="fca34-372">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="fca34-373">Inicie sesión como administrador global y haga clic en el botón **Conceder permisos** situado en la hoja **Aplicaciones empresariales -&gt; Todas las aplicaciones -&gt; Select an App (Seleccionar una aplicación) -&gt; Permisos** (disponible pronto).</span><span class="sxs-lookup"><span data-stu-id="fca34-373">Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="fca34-374">También puede exigir que se produzca este consentimiento de nivel de administrador si sigue las instrucciones que aparecen en la sección **Solicitud de los permisos de un administrador de directorios** de [Uso del punto de conexión de consentimiento del administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="fca34-374">You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fca34-375">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fca34-375">Next steps</span></span>
[<span data-ttu-id="fca34-376">Uso del punto de conexión de consentimiento del administrador</span><span class="sxs-lookup"><span data-stu-id="fca34-376">Using the admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

