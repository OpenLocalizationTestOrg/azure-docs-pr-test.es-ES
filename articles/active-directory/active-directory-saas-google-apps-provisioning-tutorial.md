---
title: "Tutorial: Configuración de Google Apps para el aprovisionamiento automático de usuarios en Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooGoogle aplicaciones."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="9d060-103">Tutorial: Configuración de Google Apps para aprovisionar a los usuarios automáticamente</span><span class="sxs-lookup"><span data-stu-id="9d060-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="9d060-104">objetivo de Hola de este tutorial es tooshow que Hola pasos necesita tooperform en Google Apps y Azure AD tooautomatically el aprovisionamiento y Desaprovisionamiento de cuentas de usuario de Azure AD tooGoogle aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d060-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d060-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d060-105">Prerequisites</span></span>

<span data-ttu-id="9d060-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9d060-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="9d060-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d060-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="9d060-108">Debe tener un inquilino válido para Google Apps for Work o Google Apps for Education.</span><span class="sxs-lookup"><span data-stu-id="9d060-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="9d060-109">Puede usar una cuenta de prueba gratuita de cualquiera de los servicios.</span><span class="sxs-lookup"><span data-stu-id="9d060-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="9d060-110">Una cuenta de usuario de Google Apps con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="9d060-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="9d060-111">Asignación de usuarios tooGoogle aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9d060-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="9d060-112">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d060-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="9d060-113">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d060-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="9d060-114">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a la aplicación de Google Apps tooyour.</span><span class="sxs-lookup"><span data-stu-id="9d060-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="9d060-115">Una vez decidido, puede asignar estas aplicaciones de Google Apps tooyour usuarios siguiendo las instrucciones de hello aquí: [asignar una aplicación de empresa de tooan de usuario o grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="9d060-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="9d060-116">Se recomienda que un único usuario de Azure AD asignarse hello tootest tooGoogle aplicaciones que configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="9d060-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="9d060-117">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="9d060-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="9d060-118">Al asignar un usuario tooGoogle aplicaciones, debe seleccionar Hola usuario o rol de "Grupo" en el cuadro de diálogo de hello asignación.</span><span class="sxs-lookup"><span data-stu-id="9d060-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="9d060-119">rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="9d060-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="9d060-120">Habilitación del aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="9d060-120">Enable automated user provisioning</span></span>

<span data-ttu-id="9d060-121">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de las aplicaciones tooGoogle de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Google Apps en función de asignación de usuario y de grupo en Azure AD .</span><span class="sxs-lookup"><span data-stu-id="9d060-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="9d060-122">También puede elegir tooenabled basado en SAML Single Sign-On para Google Apps, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d060-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9d060-123">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="9d060-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="9d060-124">Configurar el aprovisionamiento automático de cuentas de usuario</span><span class="sxs-lookup"><span data-stu-id="9d060-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="9d060-125">Otra opción viable para automatizar aplicaciones de tooGoogle de aprovisionamiento de usuarios es toouse [sincronización de directorio de aplicaciones de Google (GADS)](https://support.google.com/a/answer/106368?hl=en) que aprovisiona la tooGoogle de identidades de Active Directory local las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d060-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="9d060-126">En cambio, solución hello en este tutorial proporciona a los usuarios de Azure Active Directory (nube) y los grupos habilitados para correo tooGoogle aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d060-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="9d060-127">Inicio de sesión en hello [consola de administración de aplicaciones de Google](http://admin.google.com/) con su cuenta de administrador y haga clic en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="9d060-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="9d060-128">Si no ve el vínculo de hello, puede estar oculto bajo hello **más controles** menú situado en la parte inferior de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="9d060-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Haga clic en Seguridad.][10]

2. <span data-ttu-id="9d060-130">En hello **seguridad** página, haga clic en **referencia de la API**.</span><span class="sxs-lookup"><span data-stu-id="9d060-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![Haga clic en la referencia de la API.][15]

3. <span data-ttu-id="9d060-132">Seleccione **Enable API access**.</span><span class="sxs-lookup"><span data-stu-id="9d060-132">Select **Enable API access**.</span></span>
   
    ![Haga clic en la referencia de la API.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="9d060-134">Para cada usuario que piensa tooprovision tooGoogle aplicaciones, su nombre de usuario en Azure Active Directory *debe* ser tooa relacionados de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="9d060-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="9d060-135">Por ejemplo, Google Apps no acepta los nombres de usuario parecidos a bob@contoso.onmicrosoft.com, mientras que bob@contoso.com se acepta.</span><span class="sxs-lookup"><span data-stu-id="9d060-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="9d060-136">Puede cambiar el dominio de un usuario existente editando sus propiedades en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d060-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="9d060-137">Instrucciones de cómo se incluyen tooset un dominio personalizado para Azure Active Directory y Google Apps en lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9d060-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="9d060-138">Si no ha agregado todavía un tooyour de nombre de dominio personalizado Azure Active Directory, a continuación, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9d060-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="9d060-139">a.</span><span class="sxs-lookup"><span data-stu-id="9d060-139">a.</span></span> <span data-ttu-id="9d060-140">Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d060-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="9d060-141">En la lista de directorios de hello, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="9d060-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="9d060-142">b.</span><span class="sxs-lookup"><span data-stu-id="9d060-142">b.</span></span> <span data-ttu-id="9d060-143">Haga clic en **nombre de los dominios** en Hola panel de navegación izquierdo y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="9d060-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![agregar un dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="9d060-146">c.</span><span class="sxs-lookup"><span data-stu-id="9d060-146">c.</span></span> <span data-ttu-id="9d060-147">Escriba el nombre de dominio en hello **nombre de dominio** campo.</span><span class="sxs-lookup"><span data-stu-id="9d060-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="9d060-148">Este nombre de dominio debe ser Hola mismo nombre de dominio que piensa toouse para Google Apps.</span><span class="sxs-lookup"><span data-stu-id="9d060-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="9d060-149">Cuando esté listo, haga clic en hello **Agregar dominio** botón.</span><span class="sxs-lookup"><span data-stu-id="9d060-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![nombre de dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="9d060-151">d.</span><span class="sxs-lookup"><span data-stu-id="9d060-151">d.</span></span> <span data-ttu-id="9d060-152">Haga clic en **siguiente** página de comprobación de toogo toohello.</span><span class="sxs-lookup"><span data-stu-id="9d060-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="9d060-153">tooverify que posee este dominio, debe editar los registros DNS del dominio de hello según los valores de toohello incluidos en esta página.</span><span class="sxs-lookup"><span data-stu-id="9d060-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="9d060-154">Puede elegir tooverify mediante **registros MX** o **registros TXT**, en función de lo que seleccione para hello **tipo de registro** opción.</span><span class="sxs-lookup"><span data-stu-id="9d060-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="9d060-155">Para obtener instrucciones detalladas sobre cómo el nombre de dominio tooverify con Azure AD, consulte [agregar su propios tooAzure de nombre de dominio AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="9d060-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="9d060-157">e.</span><span class="sxs-lookup"><span data-stu-id="9d060-157">e.</span></span> <span data-ttu-id="9d060-158">Repita los pasos para todos los dominios de Hola que piensa tooadd tooyour directory anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d060-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="9d060-159">Ahora que ha comprobado todos los dominios con Azure AD, debe comprobarlos de nuevo con Google Apps.</span><span class="sxs-lookup"><span data-stu-id="9d060-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="9d060-160">Para cada dominio que ya no está registrado con Google Apps, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9d060-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="9d060-161">a.</span><span class="sxs-lookup"><span data-stu-id="9d060-161">a.</span></span> <span data-ttu-id="9d060-162">Hola [consola de administración de aplicaciones de Google](http://admin.google.com/), haga clic en **dominios**.</span><span class="sxs-lookup"><span data-stu-id="9d060-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Haga clic en Dominios][20]

    <span data-ttu-id="9d060-164">b.</span><span class="sxs-lookup"><span data-stu-id="9d060-164">b.</span></span> <span data-ttu-id="9d060-165">Haga clic en **Agregar un dominio o un alias de dominio**.</span><span class="sxs-lookup"><span data-stu-id="9d060-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Adición de un nuevo dominio][21]

    <span data-ttu-id="9d060-167">c.</span><span class="sxs-lookup"><span data-stu-id="9d060-167">c.</span></span> <span data-ttu-id="9d060-168">Seleccione **agregar otro dominio**y escriba Hola nombre de dominio de Hola que desearía tooadd.</span><span class="sxs-lookup"><span data-stu-id="9d060-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![Especificación de un nombre de dominio][22]

    <span data-ttu-id="9d060-170">d.</span><span class="sxs-lookup"><span data-stu-id="9d060-170">d.</span></span> <span data-ttu-id="9d060-171">Haga clic en **Continuar y comprobar la propiedad del dominio**.</span><span class="sxs-lookup"><span data-stu-id="9d060-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="9d060-172">A continuación, siga Hola pasos tooverify si su propio nombre de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d060-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="9d060-173">Para obtener instrucciones completas sobre cómo tooverify su dominio con Google Apps, vea.</span><span class="sxs-lookup"><span data-stu-id="9d060-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="9d060-174">[Verificar que eres el propietario del sitio web](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="9d060-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="9d060-175">e.</span><span class="sxs-lookup"><span data-stu-id="9d060-175">e.</span></span> <span data-ttu-id="9d060-176">Repita los pasos para todos los dominios adicionales que piensa tooadd tooGoogle aplicaciones anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d060-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="9d060-177">Si cambiar dominio principal de hello para el inquilino de Google Apps, y si ya ha configuran el inicio de sesión único con Azure AD, entonces tiene toorepeat paso 3 de # bajo [paso dos: habilitar Single Sign-On](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="9d060-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="9d060-178">Hola [consola de administración de aplicaciones de Google](http://admin.google.com/), haga clic en **Roles de administrador**.</span><span class="sxs-lookup"><span data-stu-id="9d060-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Haga clic en Google Apps][26]

7. <span data-ttu-id="9d060-180">Determinar qué Administrador de cuenta le gustaría toomanage toouse el aprovisionamiento de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9d060-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="9d060-181">Para hello **rol de administrador** de esa cuenta, editar hello **privilegios** para ese rol.</span><span class="sxs-lookup"><span data-stu-id="9d060-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="9d060-182">Asegúrese de que tiene todos los hello **privilegios de administrador API** habilitado para que esta cuenta puede utilizarse para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="9d060-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Haga clic en Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="9d060-184">Si va a configurar un entorno de producción, se recomienda hello es toocreate una cuenta de administrador en Google Apps específicamente para este paso.</span><span class="sxs-lookup"><span data-stu-id="9d060-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="9d060-185">Estas cuentas deben tener asociado un rol de administrador que tenga privilegios de API necesarias de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d060-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="9d060-186">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="9d060-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="9d060-187">Si ya has configurado Google Apps para el inicio de sesión único, busque la instancia de Google Apps con el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d060-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="9d060-188">En caso contrario, seleccione **agregar** y busque **Google Apps** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d060-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="9d060-189">Seleccionar aplicaciones de Google de resultados de la búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d060-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="9d060-190">Seleccione la instancia de Google Apps, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="9d060-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="9d060-191">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="9d060-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![Aprovisionamiento](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="9d060-193">En hello **las credenciales de administrador** sección, haga clic en **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="9d060-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="9d060-194">Se abrirá un cuadro de diálogo de autorización de Google Apps en una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="9d060-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="9d060-195">Confirme que desea que los cambios de toomake toogive Azure Active Directory permiso de inquilinos tooyour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="9d060-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="9d060-196">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9d060-196">Click **Accept**.</span></span>
    
     ![Confirme los permisos.][28]

14. <span data-ttu-id="9d060-198">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de Google Apps tooyour.</span><span class="sxs-lookup"><span data-stu-id="9d060-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="9d060-199">Si se produce un error en la conexión de hello, asegúrese de que su cuenta de Google Apps tiene permisos de administrador de equipo e inténtelo de hello **"Autorizar"** vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="9d060-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="9d060-200">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.</span><span class="sxs-lookup"><span data-stu-id="9d060-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="9d060-201">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9d060-201">Click **Save.**</span></span>

17. <span data-ttu-id="9d060-202">En la sección asignaciones de hello, seleccione **sincronizar Azure Active Directory Users tooGoogle aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="9d060-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="9d060-203">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooGoogle aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d060-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="9d060-204">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en Google Apps para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="9d060-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="9d060-205">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="9d060-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="9d060-206">tooenable Hola servicio de aprovisionamiento de Azure AD para Google Apps, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración</span><span class="sxs-lookup"><span data-stu-id="9d060-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="9d060-207">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9d060-207">Click **Save.**</span></span>

<span data-ttu-id="9d060-208">Inicia la sincronización inicial de Hola de los usuarios o grupos asignados tooGoogle aplicaciones en la sección usuarios y grupos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d060-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="9d060-209">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d060-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="9d060-210">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de Google Apps.</span><span class="sxs-lookup"><span data-stu-id="9d060-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d060-211">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9d060-211">Additional resources</span></span>

* [<span data-ttu-id="9d060-212">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="9d060-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d060-213">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d060-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9d060-214">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="9d060-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png