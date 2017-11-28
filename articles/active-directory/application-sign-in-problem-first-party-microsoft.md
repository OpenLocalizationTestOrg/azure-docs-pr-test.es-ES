---
title: "aaaProblems iniciar sesión en aplicaciones de Microsoft tooa | Documentos de Microsoft"
description: "Solucionar problemas comunes que se enfrentan al iniciar sesión en Applications de Microsoft toofirst terceros mediante Azure AD (por ejemplo, Office 365)"
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="384c8-103">Problemas para iniciar sesión en tooa aplicaciones de Microsoft</span><span class="sxs-lookup"><span data-stu-id="384c8-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="384c8-104">Las aplicaciones de Microsoft (como Office 365 Exchange, SharePoint, Yammer, etc.) se asignan y administran de manera algo diferente que las aplicaciones SaaS de terceros u otras aplicaciones que integra con Azure AD para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="384c8-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="384c8-105">Hay tres maneras principales que un usuario puede obtener acceso tooa aplicación publicada por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="384c8-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="384c8-106">Para las aplicaciones de Office 365 de Hola o de otros conjuntos de pagadas, los usuarios tienen acceso a través de **asignación de licencias** ya sea directamente tootheir cuenta de usuario o a través de un grupo con nuestra capacidad de asignación basado en el grupo de licencias.</span><span class="sxs-lookup"><span data-stu-id="384c8-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="384c8-107">Para las aplicaciones que Microsoft o una tercera entidad publica libremente para todo aquel que toouse, se podrá otorgar a los usuarios acceso a través de **consentimiento del usuario**.</span><span class="sxs-lookup"><span data-stu-id="384c8-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="384c8-108">This0 significa que inicie sesión en la aplicación de toohello con su cuenta de Azure AD empresa o centro educativo y permitir toohave conjunto de toosome limitado de acceso de datos en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="384c8-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="384c8-109">Para las aplicaciones que Microsoft o una entidad 3rd publica libremente para todo aquel que toouse, los usuarios también se podrá otorgar acceso a través de **consentimiento del administrador**.</span><span class="sxs-lookup"><span data-stu-id="384c8-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="384c8-110">Esto significa que un administrador ha determinado la aplicación hello pueden utilizar todas las personas de la organización de hello, para que inicie sesión en la aplicación de toohello con una cuenta de administrador Global y conceder acceso tooeveryone de organización de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="384c8-111">tootroubleshoot su problema, comienzan con hello [áreas con problemas generales con acceso a la aplicación tooconsider](#general-problem-areas-with-application-access-to-consider) y, a continuación, leer hello [Tutorial: pasos tootroubleshoot acceso de Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget en los detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="384c8-112">Áreas de riesgo general tooconsider de acceso a la aplicación</span><span class="sxs-lookup"><span data-stu-id="384c8-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="384c8-113">A continuación se muestra una lista de hello áreas con problemas generales que puede profundizar en si tiene una idea de donde toostart, pero le recomendamos que lea Hola tutorial tooget a trabajar rápidamente: [Tutorial: pasos tootroubleshoot acceso de Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="384c8-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="384c8-114">Problemas con la cuenta de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="384c8-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="384c8-115">Problemas con grupos</span><span class="sxs-lookup"><span data-stu-id="384c8-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="384c8-116">Problemas con las directivas de acceso condicional</span><span class="sxs-lookup"><span data-stu-id="384c8-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="384c8-117">Problemas con el consentimiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="384c8-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="384c8-118">Pasos tootroubleshoot acceso de Microsoft Application</span><span class="sxs-lookup"><span data-stu-id="384c8-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="384c8-119">A continuación se ciertos tipos de problemas comunes surgir cuando los usuarios no pueden iniciar sesión en tooa aplicaciones de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="384c8-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="384c8-120">General emite toocheck primero</span><span class="sxs-lookup"><span data-stu-id="384c8-120">General issues toocheck first</span></span>

  * <span data-ttu-id="384c8-121">Asegúrese de que el usuario de hello es iniciar sesión en toohello **corríjala** y no una dirección URL de aplicación local.</span><span class="sxs-lookup"><span data-stu-id="384c8-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="384c8-122">Asegúrese de que es la cuenta de usuario de hello **no está bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="384c8-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="384c8-123">Asegúrese de hello seguro **cuenta de usuario existe** en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="384c8-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="384c8-124">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="384c8-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="384c8-125">Asegúrese de que es la cuenta de usuario de hello **habilitado** para inicios de sesión. [Comprobar el estado de la cuenta de un usuario](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="384c8-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="384c8-126">Asegúrese de que usuario hello **contraseña no se ha caducado o se olvida.**</span><span class="sxs-lookup"><span data-stu-id="384c8-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="384c8-127">[Restablecer la contraseña del usuario](#reset-a-users-password) o [habilitar el autoservicio de restablecimiento de contraseña](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="384c8-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="384c8-128">Asegurarse de que **Multi-Factor Authentication** no bloquee el acceso del usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="384c8-129">[Comprobar el estado de la autenticación multifactor de un usuario](#check-a-users-multi-factor-authentication-status) o [comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="384c8-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="384c8-130">Asegurarse de que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquee el acceso del usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="384c8-131">[Comprobar una directiva de acceso condicional específica](#problems-with-conditional-access-policies) o [comprobar la directiva de acceso condicional de una aplicación específica](#check-a-specific-applications-conditional-access-policy) o [deshabilitar una directiva de acceso condicional específica](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="384c8-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="384c8-132">Asegúrese de que un usuario **información de contacto de autenticación** es hacia arriba toodate tooallow la autenticación multifactor o acceso condicional directivas toobe aplicada.</span><span class="sxs-lookup"><span data-stu-id="384c8-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="384c8-133">[Comprobar el estado de la autenticación multifactor de un usuario](#check-a-users-multi-factor-authentication-status) o [comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="384c8-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="384c8-134">Para **Microsoft** **las aplicaciones que requieren una licencia** (por ejemplo, Office 365), estos son algunos toocheck problemas específicos una vez que haya descartado problemas generales de hello anteriores:</span><span class="sxs-lookup"><span data-stu-id="384c8-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="384c8-135">Asegúrese de que el usuario de Hola o tiene un **una licencia asignada.**</span><span class="sxs-lookup"><span data-stu-id="384c8-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="384c8-136">[Comprobar las licencias asignadas de un usuario](#check-a-users-assigned-licenses) o [comprobar licencias asignadas de un grupo](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="384c8-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="384c8-137">Si la licencia de hello es **asignado tooa** **grupo estático**, asegúrese de que hello **pertenece un usuario** de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="384c8-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="384c8-138">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="384c8-139">Si la licencia de hello es **asignado tooa** **grupo dinámico**, asegúrese de que hello **regla de grupo dinámico se ha establecido correctamente**.</span><span class="sxs-lookup"><span data-stu-id="384c8-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="384c8-140">Comprobar los criterios de pertenencia de un grupo dinámico</span><span class="sxs-lookup"><span data-stu-id="384c8-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="384c8-141">Si la licencia de hello es **asignado tooa** **grupo dinámico**, asegúrese de ese grupo dinámico hello tiene **haya terminado de procesar** ese hello y su pertenencia a **usuario es un miembro** (Esto puede tardar algún tiempo).</span><span class="sxs-lookup"><span data-stu-id="384c8-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="384c8-142">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="384c8-143">Una vez que asegurarse de que se asignará la licencia de hello, asegúrese de que está licencia hello **no expirado**.</span><span class="sxs-lookup"><span data-stu-id="384c8-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="384c8-144">Asegúrese de que está licencia hello **para la aplicación hello** tienen acceso.</span><span class="sxs-lookup"><span data-stu-id="384c8-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="384c8-145">Para **Microsoft** **aplicaciones que no requieren una licencia**, estos son algunos otro toocheck cosas:</span><span class="sxs-lookup"><span data-stu-id="384c8-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="384c8-146">Si está solicitando la aplicación hello **permisos de usuario** (por ejemplo "acceso a este buzón de usuario"), asegúrese de que ese usuario Hola ha iniciado sesión en la aplicación toohello y ha realizado un **operación de consentimiento de nivel de usuario**  toolet Hola aplicación acceder a sus datos.</span><span class="sxs-lookup"><span data-stu-id="384c8-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="384c8-147">Si está solicitando la aplicación hello **permisos de nivel de administrador** (por ejemplo "obtener acceso a los buzones de correo de todos los usuarios"), asegúrese de que un administrador Global ha realizado una **operación de consentimiento de nivel de administrador en nombre de todos los usuarios** de organización de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="384c8-148">Problemas con la cuenta de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="384c8-148">Problems with hello user’s account</span></span>

<span data-ttu-id="384c8-149">Acceso a la aplicación se puede bloquear debido tooa problema con un usuario que tenga asignada la aplicación toohello.</span><span class="sxs-lookup"><span data-stu-id="384c8-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="384c8-150">A continuación se muestran algunas maneras de solucionar problemas con los usuarios y la configuración de sus cuentas:</span><span class="sxs-lookup"><span data-stu-id="384c8-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="384c8-151">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="384c8-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="384c8-152">Comprobar el estado de la cuenta de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="384c8-153">Restablecer la contraseña de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="384c8-154">Habilitar el autoservicio de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="384c8-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="384c8-155">Comprobar el estado de la autenticación multifactor de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="384c8-156">Comprobar la información de contacto de autenticación de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="384c8-157">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="384c8-158">Comprobar las licencias asignadas de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="384c8-159">Asignar una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="384c8-160">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="384c8-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="384c8-161">toocheck si está presente, una cuenta de usuario siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="384c8-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-162">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-163">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-164">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-165">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-166">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="384c8-166">click **All users**.</span></span>

6.  <span data-ttu-id="384c8-167">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-168">Compruebe las propiedades de Hola de hello usuario objeto toobe seguro de que se muestran como esperaba y no existe ningún dato.</span><span class="sxs-lookup"><span data-stu-id="384c8-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="384c8-169">Comprobar el estado de la cuenta de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-169">Check a user’s account status</span></span>

<span data-ttu-id="384c8-170">toocheck un usuario de estado de la cuenta, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="384c8-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-171">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-172">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-173">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-174">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-175">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="384c8-175">click **All users**.</span></span>

6.  <span data-ttu-id="384c8-176">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-177">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="384c8-177">click **Profile**.</span></span>

8.  <span data-ttu-id="384c8-178">En **configuración** Asegúrese de que **bloque iniciar sesión en** se establece demasiado**No**.</span><span class="sxs-lookup"><span data-stu-id="384c8-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="384c8-179">Restablecer la contraseña de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-179">Reset a user’s password</span></span>

<span data-ttu-id="384c8-180">tooreset contraseña de un usuario, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="384c8-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-181">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-182">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-183">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-184">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-185">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="384c8-185">click **All users**.</span></span>

6.  <span data-ttu-id="384c8-186">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-187">Haga clic en hello **de restablecimiento de contraseña** situado en la parte superior de Hola de hoja de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="384c8-188">Haga clic en hello **de restablecimiento de contraseña** botón en hello **de restablecimiento de contraseña** hoja que aparece.</span><span class="sxs-lookup"><span data-stu-id="384c8-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="384c8-189">Hola copia **contraseña temporal** o **escriba una contraseña nueva** para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="384c8-190">Este nuevo usuario toohello de contraseña se comunican, requiere toochange esta contraseña durante su próximo iniciar sesión en tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="384c8-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="384c8-191">Habilitar el autoservicio de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="384c8-191">Enable self-service password reset</span></span>

<span data-ttu-id="384c8-192">contraseña de autoservicio de tooenable restablecer, siga los pasos de implementación de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="384c8-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="384c8-193">Habilitar usuarios tooreset sus contraseñas de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="384c8-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="384c8-194">Habilitar usuarios tooreset o cambiar sus contraseñas locales de Active Directory</span><span class="sxs-lookup"><span data-stu-id="384c8-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="384c8-195">Comprobar el estado de la autenticación multifactor de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="384c8-196">toocheck un usuario de multifactor estado de autenticación, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="384c8-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-197">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-198">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-199">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-200">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-201">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="384c8-201">click **All users**.</span></span>

6.  <span data-ttu-id="384c8-202">Haga clic en hello **la autenticación multifactor** situado en la parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="384c8-203">Una vez Hola **Portal de administración de Multi-factor Authentication** cargas, asegúrese de que esté en hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="384c8-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="384c8-204">Busque el usuario de hello en lista de Hola de usuarios por búsqueda, el filtrado u ordenación.</span><span class="sxs-lookup"><span data-stu-id="384c8-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="384c8-205">Usuario seleccione Hola Hola usuarios de lista y **habilitar**, **deshabilitar**, o **aplicar** la autenticación multifactor según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="384c8-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="384c8-206">**Tenga en cuenta**: si un usuario pertenece a un **forzado** estado, puede establecerlos demasiado**deshabilitado** temporalmente toolet volverlos a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="384c8-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="384c8-207">Una vez que estén en, a continuación, puede cambiar su estado demasiado**habilitado** nuevo toorequire les toore su información de contacto durante su próximo iniciar sesión en el registro.</span><span class="sxs-lookup"><span data-stu-id="384c8-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="384c8-208">Como alternativa, puede seguir los pasos de Hola Hola [Compruebe la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info) tooverify o establecer estos datos para ellos.</span><span class="sxs-lookup"><span data-stu-id="384c8-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="384c8-209">Comprobar la información de contacto de autenticación de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="384c8-210">toocheck autenticación de un usuario, póngase en contacto con información usada para la autenticación multifactor, acceso condicional, protección de identidad y de restablecimiento de contraseña, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="384c8-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-211">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-212">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-213">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-214">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-215">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="384c8-215">click **All users**.</span></span>

6.  <span data-ttu-id="384c8-216">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-217">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="384c8-217">click **Profile**.</span></span>

8.  <span data-ttu-id="384c8-218">Desplácese hacia abajo demasiado**información de contacto de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="384c8-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="384c8-219">**Revisión** datos Hola registrado para el usuario de Hola y actualizar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="384c8-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="384c8-220">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-220">Check a user’s group memberships</span></span>

<span data-ttu-id="384c8-221">toocheck un usuario de pertenencia a grupos, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="384c8-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-222">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-223">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-224">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-225">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-226">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="384c8-226">click **All users**.</span></span>

6.  <span data-ttu-id="384c8-227">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-228">Haga clic en **grupos** toosee que agrupa usuario hello es un miembro de.</span><span class="sxs-lookup"><span data-stu-id="384c8-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="384c8-229">Comprobar las licencias asignadas de un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="384c8-230">toocheck un usuario había asignado licencias, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="384c8-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-231">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-232">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-233">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-234">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-235">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="384c8-235">click **All users**.</span></span>

6.  <span data-ttu-id="384c8-236">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-237">Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="384c8-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="384c8-238">Asignar una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-238">Assign a user a license</span></span> 

<span data-ttu-id="384c8-239">tooassign un usuario tooa de licencias, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="384c8-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-240">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-241">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-242">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-243">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-244">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="384c8-244">click **All users**.</span></span>

6.  <span data-ttu-id="384c8-245">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-246">Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="384c8-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="384c8-247">Haga clic en hello **asignar** botón.</span><span class="sxs-lookup"><span data-stu-id="384c8-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="384c8-248">Seleccione **uno o más productos** en lista de Hola de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="384c8-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="384c8-249">**Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos.</span><span class="sxs-lookup"><span data-stu-id="384c8-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="384c8-250">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="384c8-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="384c8-251">Haga clic en hello **asignar** botón tooassign estos usuario toothis de licencias.</span><span class="sxs-lookup"><span data-stu-id="384c8-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="384c8-252">Problemas con grupos</span><span class="sxs-lookup"><span data-stu-id="384c8-252">Problems with groups</span></span>

<span data-ttu-id="384c8-253">Acceso a la aplicación se puede bloquear debido tooa problema con un grupo que se asigna la aplicación toohello.</span><span class="sxs-lookup"><span data-stu-id="384c8-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="384c8-254">A continuación se muestran algunas maneras de solucionar problemas con grupos y pertenencias a grupos:</span><span class="sxs-lookup"><span data-stu-id="384c8-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="384c8-255">Comprobar la pertenencia de un grupo</span><span class="sxs-lookup"><span data-stu-id="384c8-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="384c8-256">Comprobar los criterios de pertenencia de un grupo dinámico</span><span class="sxs-lookup"><span data-stu-id="384c8-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="384c8-257">Comprobar las licencias asignadas de un grupo</span><span class="sxs-lookup"><span data-stu-id="384c8-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="384c8-258">Volver a procesar las licencias de un grupo</span><span class="sxs-lookup"><span data-stu-id="384c8-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="384c8-259">Asignar una licencia a un grupo</span><span class="sxs-lookup"><span data-stu-id="384c8-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="384c8-260">Comprobar la pertenencia de un grupo</span><span class="sxs-lookup"><span data-stu-id="384c8-260">Check a group’s membership</span></span>

<span data-ttu-id="384c8-261">toocheck pertenencia de un grupo, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="384c8-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-262">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-263">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-264">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-265">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-266">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="384c8-266">click **All groups**.</span></span>

6.  <span data-ttu-id="384c8-267">**Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-268">Haga clic en **miembros** tooreview lista de Hola de usuarios asignados toothis grupo.</span><span class="sxs-lookup"><span data-stu-id="384c8-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="384c8-269">Comprobar los criterios de pertenencia de un grupo dinámico</span><span class="sxs-lookup"><span data-stu-id="384c8-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="384c8-270">toocheck criterios de pertenencia de un grupo dinámico, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="384c8-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-271">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-272">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-273">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-274">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-275">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="384c8-275">click **All groups**.</span></span>

6.  <span data-ttu-id="384c8-276">**Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-277">Haga clic en **Reglas de pertenencia dinámica**.</span><span class="sxs-lookup"><span data-stu-id="384c8-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="384c8-278">Hola de revisión **simple** o **avanzadas** definida para este grupo de reglas y asegúrese de que ese usuario Hola desea toobe un miembro de este grupo cumple estos criterios.</span><span class="sxs-lookup"><span data-stu-id="384c8-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="384c8-279">Comprobar licencias asignadas de un grupo</span><span class="sxs-lookup"><span data-stu-id="384c8-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="384c8-280">toocheck un grupo había asignado licencias, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="384c8-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-281">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-282">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-283">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-284">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-285">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="384c8-285">click **All groups**.</span></span>

6.  <span data-ttu-id="384c8-286">**Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-287">Haga clic en **licencias** toosee qué grupo de licencias Hola actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="384c8-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="384c8-288">Volver a procesar las licencias de un grupo</span><span class="sxs-lookup"><span data-stu-id="384c8-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="384c8-289">tooreprocess un grupo había asignado licencias, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="384c8-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-290">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-291">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-292">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-293">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-294">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="384c8-294">click **All groups**.</span></span>

6.  <span data-ttu-id="384c8-295">**Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-296">Haga clic en **licencias** toosee qué grupo de licencias Hola actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="384c8-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="384c8-297">Haga clic en hello **volver a procesar** tooensure de botón que Hola miembros del grupo de licencias asignadas toothis están actualizados.</span><span class="sxs-lookup"><span data-stu-id="384c8-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="384c8-298">Esto puede tardar mucho tiempo, en función de hello tamaño y la complejidad del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="384c8-299">toodo esto con mayor rapidez, considere la posibilidad de temporalmente asignar una licencia toohello usuario directamente.</span><span class="sxs-lookup"><span data-stu-id="384c8-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="384c8-300">[Asignar una licencia a un usuario](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="384c8-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="384c8-301">Asignar una licencia a un grupo</span><span class="sxs-lookup"><span data-stu-id="384c8-301">Assign a group a license</span></span>

<span data-ttu-id="384c8-302">tooassign un grupo de tooa licencias, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="384c8-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="384c8-303">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-304">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-305">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-306">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-307">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="384c8-307">click **All groups**.</span></span>

6.  <span data-ttu-id="384c8-308">**Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="384c8-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="384c8-309">Haga clic en **licencias** toosee qué grupo de licencias Hola actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="384c8-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="384c8-310">Haga clic en hello **asignar** botón.</span><span class="sxs-lookup"><span data-stu-id="384c8-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="384c8-311">Seleccione **uno o más productos** en lista de Hola de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="384c8-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="384c8-312">**Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos.</span><span class="sxs-lookup"><span data-stu-id="384c8-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="384c8-313">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="384c8-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="384c8-314">Haga clic en hello **asignar** botón tooassign estos toothis de grupo de licencias.</span><span class="sxs-lookup"><span data-stu-id="384c8-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="384c8-315">Esto puede tardar mucho tiempo, en función de hello tamaño y la complejidad del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="384c8-316">toodo esto con mayor rapidez, considere la posibilidad de temporalmente asignar una licencia toohello usuario directamente.</span><span class="sxs-lookup"><span data-stu-id="384c8-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="384c8-317">[Asignar una licencia a un usuario](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="384c8-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="384c8-318">Problemas con las directivas de acceso condicional</span><span class="sxs-lookup"><span data-stu-id="384c8-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="384c8-319">Comprobar una directiva de acceso condicional específica</span><span class="sxs-lookup"><span data-stu-id="384c8-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="384c8-320">toocheck o validar una directiva de acceso condicional único:</span><span class="sxs-lookup"><span data-stu-id="384c8-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="384c8-321">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-322">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-323">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-324">Haga clic en **aplicaciones empresariales** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-325">Haga clic en hello **acceso condicional** elemento de navegación.</span><span class="sxs-lookup"><span data-stu-id="384c8-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="384c8-326">Haga clic en directiva de hello está interesado en inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="384c8-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="384c8-327">Revise que no haya condiciones, asignaciones u otras configuraciones específicas que puedan estar bloqueando el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="384c8-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="384c8-328">Puede ser conveniente deshabilitar tootemporarily esta tooensure de directiva no afecta a toodo de componentes de inicio de sesión, Hola conjunto **habilitar Directiva de** alternar demasiado**No** y haga clic en hello **guardar** botón .</span><span class="sxs-lookup"><span data-stu-id="384c8-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="384c8-329">Comprobar la directiva de acceso condicional de una aplicación específica</span><span class="sxs-lookup"><span data-stu-id="384c8-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="384c8-330">toocheck ni validar la directiva de acceso condicional configuradas actualmente un único de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="384c8-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="384c8-331">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-332">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-333">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-334">Haga clic en **aplicaciones empresariales** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-335">A continuación, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="384c8-335">click **All applications**.</span></span>

6.  <span data-ttu-id="384c8-336">Búsqueda de aplicación de hello interesa u Hola usuario está intentando toosign en aplicación tooby mostrar Id. de nombre o de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="384c8-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="384c8-337">Si no ve la aplicación hello que está buscando, haga clic en hello **filtro** botón y extiende el ámbito de Hola de lista Hola demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="384c8-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="384c8-338">Si desea toosee más columnas, haga clic en hello **columnas** botón tooadd detalles adicionales para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="384c8-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="384c8-339">Haga clic en hello **acceso condicional** elemento de navegación.</span><span class="sxs-lookup"><span data-stu-id="384c8-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="384c8-340">Haga clic en directiva de hello está interesado en inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="384c8-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="384c8-341">Revise que no haya condiciones, asignaciones u otras configuraciones específicas que puedan estar bloqueando el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="384c8-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="384c8-342">Puede ser conveniente deshabilitar tootemporarily esta tooensure de directiva no afecta a toodo de componentes de inicio de sesión, Hola conjunto **habilitar Directiva de** alternar demasiado**No** y haga clic en hello **guardar** botón .</span><span class="sxs-lookup"><span data-stu-id="384c8-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="384c8-343">Deshabilitar una directiva de acceso condicional específica</span><span class="sxs-lookup"><span data-stu-id="384c8-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="384c8-344">toocheck o validar una directiva de acceso condicional único:</span><span class="sxs-lookup"><span data-stu-id="384c8-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="384c8-345">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="384c8-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="384c8-346">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="384c8-347">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="384c8-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="384c8-348">Haga clic en **aplicaciones empresariales** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="384c8-349">Haga clic en hello **acceso condicional** elemento de navegación.</span><span class="sxs-lookup"><span data-stu-id="384c8-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="384c8-350">Haga clic en directiva de hello está interesado en inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="384c8-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="384c8-351">Deshabilitar directiva Hola Hola establecer **habilitar Directiva de** alternar demasiado**No** y haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="384c8-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="384c8-352">Problemas con el consentimiento de aplicación</span><span class="sxs-lookup"><span data-stu-id="384c8-352">Problems with application consent</span></span>

<span data-ttu-id="384c8-353">Acceso a la aplicación se puede bloquear porque no se ha producido la operación de consentimiento de los permisos adecuados de Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="384c8-354">A continuación se muestran algunas maneras en que puede solucionar problemas relacionados con el consentimiento de aplicación:</span><span class="sxs-lookup"><span data-stu-id="384c8-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="384c8-355">Realizar una operación de consentimiento de nivel de usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="384c8-356">Realizar la operación de consentimiento de nivel de administrador para cualquier aplicación</span><span class="sxs-lookup"><span data-stu-id="384c8-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="384c8-357">Realizar el consentimiento de nivel de administrador para una aplicación de un solo inquilino</span><span class="sxs-lookup"><span data-stu-id="384c8-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="384c8-358">Realizar el consentimiento de nivel de administrador para una aplicación multiinquilino</span><span class="sxs-lookup"><span data-stu-id="384c8-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="384c8-359">Realizar una operación de consentimiento de nivel de usuario</span><span class="sxs-lookup"><span data-stu-id="384c8-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="384c8-360">Para cualquier aplicación habilitada para abrir conectarse de Id. que solicita permisos, navegar por el inicio de sesión de la aplicación toohello en pantalla realiza una aplicación de toohello de nivel de consentimiento de usuario para el usuario que inició sesión Hola.</span><span class="sxs-lookup"><span data-stu-id="384c8-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="384c8-361">Si desea toodo esto mediante programación, vea [solicitar el consentimiento del usuario](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="384c8-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="384c8-362">Realizar la operación de consentimiento de nivel de administrador para cualquier aplicación</span><span class="sxs-lookup"><span data-stu-id="384c8-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="384c8-363">Para **sólo las aplicaciones desarrolladas con el modelo de aplicación Hola V1**, puede forzar este toooccur de nivel de consentimiento del administrador mediante la adición de "**? prompt = admin\_consentimiento**" toohello final de un inicio de sesión de la aplicación en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="384c8-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="384c8-364">Para **cualquier aplicación desarrollada con el modelo de aplicación Hola V2**, puede aplicar este toooccur de consentimiento de nivel de administrador, siga las instrucciones de hello en hello **solicitar permisos de Hola desde un directorio administración** sección de [con el extremo de consentimiento de administración de hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="384c8-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="384c8-365">Realizar el consentimiento de nivel de administrador para una aplicación de un único inquilino</span><span class="sxs-lookup"><span data-stu-id="384c8-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="384c8-366">Para **único inquilino aplicaciones** que solicitan permisos (por ejemplo, aquellas que está desarrollando o el propietario de la organización), puede realizar un **consentimiento de nivel administrativo** operación en nombre de todos los los usuarios iniciar sesión como administrador Global y haciendo clic en hello **conceder permisos** situado en la parte superior de Hola de hello **el registro de aplicación -&gt; todas las aplicaciones -&gt; seleccione una aplicación: &gt; Permisos necesarios** hoja.</span><span class="sxs-lookup"><span data-stu-id="384c8-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="384c8-367">Para **cualquier aplicación desarrollada con Hola V1 o V2 modelo de aplicación**, puede aplicar este toooccur de consentimiento de nivel de administrador, siga las instrucciones de hello en hello **solicitar permisos de Hola a un Administrador de directorio** sección de [con el extremo de consentimiento de administración de hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="384c8-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="384c8-368">Realizar el consentimiento de nivel de administrador para una aplicación multiinquilino</span><span class="sxs-lookup"><span data-stu-id="384c8-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="384c8-369">Para **aplicaciones multiinquilino** que solicitan permisos (como una aplicación que desarrolla un tercero o Microsoft), puede realizar una operación de **consentimiento de nivel administrativo**.</span><span class="sxs-lookup"><span data-stu-id="384c8-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="384c8-370">Inicie sesión como administrador Global y haga clic en hello **conceder permisos** botón en hello **aplicaciones empresariales -&gt; todas las aplicaciones -&gt; seleccionar una aplicación -&gt; Permisos** hoja (disponible próximamente).</span><span class="sxs-lookup"><span data-stu-id="384c8-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="384c8-371">También puede aplicar este toooccur de consentimiento de nivel de administrador siguiendo las instrucciones de hello en hello **solicitar permisos de Hola desde un directorio de administrador** sección de [con el extremo de consentimiento de administración de hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="384c8-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="384c8-372">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="384c8-372">Next steps</span></span>
[<span data-ttu-id="384c8-373">Uso de extremo de consentimiento de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="384c8-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

