---
title: "Tutorial: Configuración de Google Apps para el aprovisionamiento automático de usuarios en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD para Google Apps."
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
ms.openlocfilehash: b061f0ddad70be4a5ca48d48d1a737d6af8afa8d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="19be9-103">Tutorial: Configuración de Google Apps para aprovisionar a los usuarios automáticamente</span><span class="sxs-lookup"><span data-stu-id="19be9-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="19be9-104">El objetivo de este tutorial es explicar los pasos que debe realizar en Google Apps y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD para Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-104">The objective of this tutorial is to show you the steps you need to perform in Google Apps and Azure AD to automatically provision and de-provision user accounts from Azure AD to Google Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19be9-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="19be9-105">Prerequisites</span></span>

<span data-ttu-id="19be9-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="19be9-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="19be9-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="19be9-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="19be9-108">Debe tener un inquilino válido para Google Apps for Work o Google Apps for Education.</span><span class="sxs-lookup"><span data-stu-id="19be9-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="19be9-109">Puede usar una cuenta de prueba gratuita de cualquiera de los servicios.</span><span class="sxs-lookup"><span data-stu-id="19be9-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="19be9-110">Una cuenta de usuario de Google Apps con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="19be9-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-to-google-apps"></a><span data-ttu-id="19be9-111">Asignación de usuarios a Google Apps</span><span class="sxs-lookup"><span data-stu-id="19be9-111">Assigning users to Google Apps</span></span>

<span data-ttu-id="19be9-112">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="19be9-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="19be9-113">En el contexto del aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19be9-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="19be9-114">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Google Apps app.</span></span> <span data-ttu-id="19be9-115">Una vez decididos, puede asignar estos usuarios a la aplicación de Google Apps siguiendo las instrucciones de: [Asignación de un usuario o un grupo a una aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="19be9-115">Once decided, you can assign these users to your Google Apps app by following the instructions here: [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="19be9-116">Se recomienda asignar un solo usuario de Azure AD a Google Apps para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="19be9-116">It is recommended that a single Azure AD user be assigned to Google Apps to test the provisioning configuration.</span></span> <span data-ttu-id="19be9-117">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="19be9-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="19be9-118">Al asignar un usuario a Google Apps, debe seleccionar los roles Usuario o "Grupo" en el cuadro de diálogo de asignación.</span><span class="sxs-lookup"><span data-stu-id="19be9-118">When assigning a user to Google Apps, you must select the User or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="19be9-119">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="19be9-119">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="19be9-120">Habilitar el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="19be9-120">Enable automated user provisioning</span></span>

<span data-ttu-id="19be9-121">En esta sección se describen los pasos necesarios para conectar Azure AD a la API de aprovisionamiento de cuentas de usuario de Google Apps, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de Google Apps en función de la asignación de grupos y usuarios en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19be9-121">This section guides you through connecting your Azure AD to Google Apps's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="19be9-122">También puede decidir habilitar el inicio de sesión único basado en SAML para Google Apps siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19be9-122">You may also choose to enabled SAML-based Single Sign-On for Google Apps, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="19be9-123">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="19be9-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="19be9-124">Configurar el aprovisionamiento automático de cuentas de usuario</span><span class="sxs-lookup"><span data-stu-id="19be9-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="19be9-125">Otra opción viable para la automatización del aprovisionamiento de usuarios en Google Apps es usar [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) , que aprovisiona las identidades de Active Directory locales en Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-125">Another viable option for automating user provisioning to Google Apps is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities to Google Apps.</span></span> <span data-ttu-id="19be9-126">En cambio, la solución en este tutorial realiza el aprovisionamiento de los usuarios de Azure Active Directory (nube) y a los grupos habilitados para correo en Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-126">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups to Google Apps.</span></span> 

1. <span data-ttu-id="19be9-127">Inicie sesión en la [Consola de administración de Google Apps](http://admin.google.com/) con su cuenta de administrador y haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="19be9-127">Sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="19be9-128">Si no ve el vínculo, puede estar oculto debajo del menú **Más controles** en la parte inferior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="19be9-128">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Haga clic en Seguridad.][10]

2. <span data-ttu-id="19be9-130">En la página **Seguridad**, haga clic en **Referencia de API**.</span><span class="sxs-lookup"><span data-stu-id="19be9-130">On the **Security** page, click **API Reference**.</span></span>
   
    ![Haga clic en la referencia de la API.][15]

3. <span data-ttu-id="19be9-132">Seleccione **Enable API access**.</span><span class="sxs-lookup"><span data-stu-id="19be9-132">Select **Enable API access**.</span></span>
   
    ![Haga clic en la referencia de la API.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="19be9-134">El nombre en Active Directory de todos los usuarios desee aprovisionar en Google Apps *debe* estar enlazado con un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="19be9-134">For every user that you intend to provision to Google Apps, their username in Azure Active Directory *must* be tied to a custom domain.</span></span> <span data-ttu-id="19be9-135">Por ejemplo, Google Apps no acepta los nombres de usuario parecidos a bob@contoso.onmicrosoft.com, mientras que bob@contoso.com se acepta.</span><span class="sxs-lookup"><span data-stu-id="19be9-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="19be9-136">Puede cambiar el dominio de un usuario existente editando sus propiedades en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19be9-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="19be9-137">En los pasos siguientes se incluyen instrucciones sobre cómo establecer un dominio personalizado para Azure Active Directory y Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-137">Instructions for how to set a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="19be9-138">Si todavía no ha agregado un nombre de dominio personalizado para Azure Active Directory, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="19be9-138">If you haven't added a custom domain name to your Azure Active Directory yet, then follow the following steps:</span></span>
  
    <span data-ttu-id="19be9-139">a.</span><span class="sxs-lookup"><span data-stu-id="19be9-139">a.</span></span> <span data-ttu-id="19be9-140">En [Azure Portal](https://portal.azure.com), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19be9-140">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="19be9-141">En la lista de directorios, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="19be9-141">In the directory list, select your directory.</span></span> 

    <span data-ttu-id="19be9-142">b.</span><span class="sxs-lookup"><span data-stu-id="19be9-142">b.</span></span> <span data-ttu-id="19be9-143">Haga clic en **Nombre de dominio** en el panel de navegación izquierdo y, después, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="19be9-143">Click **Domains name** on the left navigation pane, and then click **Add**.</span></span>
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![agregar un dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="19be9-146">c.</span><span class="sxs-lookup"><span data-stu-id="19be9-146">c.</span></span> <span data-ttu-id="19be9-147">Escriba el nombre del dominio en el campo **Nombre de dominio** .</span><span class="sxs-lookup"><span data-stu-id="19be9-147">Type your domain name into the **Domain name** field.</span></span> <span data-ttu-id="19be9-148">Este nombre de dominio debe ser el mismo que piensa usar para Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-148">This domain name should be the same domain name that you intend to use for Google Apps.</span></span> <span data-ttu-id="19be9-149">Cuando esté listo, haga clic en el botón **Agregar dominio**.</span><span class="sxs-lookup"><span data-stu-id="19be9-149">When ready, click the **Add Domain** button.</span></span>
     
     ![nombre de dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="19be9-151">d.</span><span class="sxs-lookup"><span data-stu-id="19be9-151">d.</span></span> <span data-ttu-id="19be9-152">Haga clic en **Siguiente** para ir a la página de comprobación.</span><span class="sxs-lookup"><span data-stu-id="19be9-152">Click **Next** to go to the verification page.</span></span> <span data-ttu-id="19be9-153">Para comprobar que es propietario de este dominio, debe editar los registros DNS del dominio según los valores proporcionados en esta página.</span><span class="sxs-lookup"><span data-stu-id="19be9-153">To verify that you own this domain, you must edit the domain's DNS records according to the values provided on this page.</span></span> <span data-ttu-id="19be9-154">Puede optar por realizar la comprobación con **registros MX** o **registros TXT** según lo que seleccione en la opción **Tipo de registro**.</span><span class="sxs-lookup"><span data-stu-id="19be9-154">You may choose to verify using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span></span> <span data-ttu-id="19be9-155">Para obtener instrucciones detalladas sobre cómo comprobar el nombre de dominio con Azure AD, consulte [Agregar su propio nombre de dominio a Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="19be9-155">For more comprehensive instructions on how to verify domain name with Azure AD, refer [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="19be9-157">e.</span><span class="sxs-lookup"><span data-stu-id="19be9-157">e.</span></span> <span data-ttu-id="19be9-158">Repita los pasos anteriores para todos los dominios que quiera agregar a su directorio.</span><span class="sxs-lookup"><span data-stu-id="19be9-158">Repeat the preceding steps for all the domains that you intend to add to your directory.</span></span>

5. <span data-ttu-id="19be9-159">Ahora que ha comprobado todos los dominios con Azure AD, debe comprobarlos de nuevo con Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="19be9-160">Para cada dominio que no esté registrado aún con Google Apps, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="19be9-160">For each domain that isn't already registered with Google Apps, perform the following steps:</span></span>
   
    <span data-ttu-id="19be9-161">a.</span><span class="sxs-lookup"><span data-stu-id="19be9-161">a.</span></span> <span data-ttu-id="19be9-162">En la [Consola de administración de Google Apps](http://admin.google.com/), haga clic en **Dominios**.</span><span class="sxs-lookup"><span data-stu-id="19be9-162">In the [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Haga clic en Dominios][20]

    <span data-ttu-id="19be9-164">b.</span><span class="sxs-lookup"><span data-stu-id="19be9-164">b.</span></span> <span data-ttu-id="19be9-165">Haga clic en **Agregar un dominio o un alias de dominio**.</span><span class="sxs-lookup"><span data-stu-id="19be9-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Adición de un nuevo dominio][21]

    <span data-ttu-id="19be9-167">c.</span><span class="sxs-lookup"><span data-stu-id="19be9-167">c.</span></span> <span data-ttu-id="19be9-168">Seleccione **Añadir otro dominio**y escriba el nombre del dominio que desee agregar.</span><span class="sxs-lookup"><span data-stu-id="19be9-168">Select **Add another domain**, and type in the name of the domain that you would like to add.</span></span>
     
     ![Especificación de un nombre de dominio][22]

    <span data-ttu-id="19be9-170">d.</span><span class="sxs-lookup"><span data-stu-id="19be9-170">d.</span></span> <span data-ttu-id="19be9-171">Haga clic en **Continuar y comprobar la propiedad del dominio**.</span><span class="sxs-lookup"><span data-stu-id="19be9-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="19be9-172">A continuación, siga los pasos para comprobar que posee el nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="19be9-172">Then follow the steps to verify that you own the domain name.</span></span> <span data-ttu-id="19be9-173">Para obtener instrucciones completas sobre cómo comprobar un dominio con Google Apps, vea</span><span class="sxs-lookup"><span data-stu-id="19be9-173">For comprehensive instructions on how to verify your domain with Google Apps, see.</span></span> <span data-ttu-id="19be9-174">[Verificar que eres el propietario del sitio web](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="19be9-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="19be9-175">e.</span><span class="sxs-lookup"><span data-stu-id="19be9-175">e.</span></span> <span data-ttu-id="19be9-176">Repita los pasos anteriores para todos los dominios adicionales que se van a agregar a Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-176">Repeat the preceding steps for any additional domains that you intend to add to Google Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="19be9-177">Si cambia el dominio principal del inquilino de Google Apps y ya ha configurado el inicio de sesión único con Azure AD, tendrá que repetir el paso 3 en [Paso 2: Habilitar el inicio de sesión único](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="19be9-177">If you change the primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have to repeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="19be9-178">En la [Consola de administración de Google Apps](http://admin.google.com/), haga clic en **Funciones de administrador**.</span><span class="sxs-lookup"><span data-stu-id="19be9-178">In the [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Haga clic en Google Apps][26]

7. <span data-ttu-id="19be9-180">Determine qué cuenta de administrador le gustaría usar para administrar el aprovisionamiento de usuarios.</span><span class="sxs-lookup"><span data-stu-id="19be9-180">Determine which admin account you would like to use to manage user provisioning.</span></span> <span data-ttu-id="19be9-181">Para el **rol administrativo** de esa cuenta, edite los **privilegios** para ese rol.</span><span class="sxs-lookup"><span data-stu-id="19be9-181">For the **admin role** of that account, edit the **Privileges** for that role.</span></span> <span data-ttu-id="19be9-182">Asegúrese de que tiene todos los **privilegios de la API de administración** habilitados para que esta cuenta pueda usarse para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="19be9-182">Make sure it has all the **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Haga clic en Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="19be9-184">Si va a configurar un entorno de producción, la práctica recomendada es crear una nueva cuenta de administrador en Google Apps específicamente para este paso.</span><span class="sxs-lookup"><span data-stu-id="19be9-184">If you are configuring a production environment, the best practice is to create an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="19be9-185">Estas cuentas deben tener un rol de administrador asociado que tenga los privilegios necesarios de la API.</span><span class="sxs-lookup"><span data-stu-id="19be9-185">These accounts must have an admin role associated with it that has the necessary API privileges.</span></span>
     
8. <span data-ttu-id="19be9-186">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="19be9-186">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="19be9-187">Si ya ha configurado Google Apps para el inicio de sesión único, busque la instancia de Google Apps mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="19be9-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using the search field.</span></span> <span data-ttu-id="19be9-188">En caso contrario, haga clic en **Agregar** y busque **Google Apps** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="19be9-188">Otherwise, select **Add** and search for **Google Apps** in the application gallery.</span></span> <span data-ttu-id="19be9-189">Seleccione Google Apps en los resultados de la búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="19be9-189">Select Google Apps from the search results, and add it to your list of applications.</span></span>

10. <span data-ttu-id="19be9-190">Seleccione la instancia de Google Apps y, después, haga clic en la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="19be9-190">Select your instance of Google Apps, then select the **Provisioning** tab.</span></span>

11. <span data-ttu-id="19be9-191">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="19be9-191">Set the **Provisioning Mode** to **Automatic**.</span></span> 

     ![Aprovisionamiento](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="19be9-193">En **Credenciales de administrador**, haga clic en **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="19be9-193">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="19be9-194">Se abrirá un cuadro de diálogo de autorización de Google Apps en una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="19be9-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="19be9-195">Confirme que desea conceder permiso de Azure Active Directory para realizar cambios en el inquilino de Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-195">Confirm that you would like to give Azure Active Directory permission to make changes to your Google Apps tenant.</span></span> <span data-ttu-id="19be9-196">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="19be9-196">Click **Accept**.</span></span>
    
     ![Confirme los permisos.][28]

14. <span data-ttu-id="19be9-198">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-198">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Google Apps app.</span></span> <span data-ttu-id="19be9-199">Si se produce un error de conexión, asegúrese de que su cuenta de Google Apps tiene permisos de administrador de equipo y vuelva a intentar el paso de **"Autorizar"**.</span><span class="sxs-lookup"><span data-stu-id="19be9-199">If the connection fails, ensure your Google Apps account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

15. <span data-ttu-id="19be9-200">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla.</span><span class="sxs-lookup"><span data-stu-id="19be9-200">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

16. <span data-ttu-id="19be9-201">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="19be9-201">Click **Save.**</span></span>

17. <span data-ttu-id="19be9-202">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to Google Apps** (Sincronizar usuarios de Azure Active Directory con Google Apps).</span><span class="sxs-lookup"><span data-stu-id="19be9-202">Under the Mappings section, select **Synchronize Azure Active Directory Users to Google Apps.**</span></span>

18. <span data-ttu-id="19be9-203">En la sección **Asignaciones de atributos**, revise los atributos de usuario que se sincronizarán entre Azure AD y Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-203">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Google Apps.</span></span> <span data-ttu-id="19be9-204">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de Google Apps con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="19be9-204">The attributes selected as **Matching** properties are used to match the user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="19be9-205">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="19be9-205">Select the Save button to commit any changes.</span></span>

19. <span data-ttu-id="19be9-206">Para habilitar el servicio de aprovisionamiento de Azure AD para Google Apps, cambie el **Estado de aprovisionamiento** a **Activado** en la sección Configuración.</span><span class="sxs-lookup"><span data-stu-id="19be9-206">To enable the Azure AD provisioning service for Google Apps, change the **Provisioning Status** to **On** in the Settings section</span></span>

20. <span data-ttu-id="19be9-207">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="19be9-207">Click **Save.**</span></span>

<span data-ttu-id="19be9-208">Esta acción inicia la sincronización inicial de todos los usuarios y grupos asignados a Google Apps en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="19be9-208">It starts the initial synchronization of any users and/or groups assigned to Google Apps in the Users and Groups section.</span></span> <span data-ttu-id="19be9-209">La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="19be9-209">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="19be9-210">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y seguir los vínculos a los informes de actividad de aprovisionamiento, donde se describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de Google Apps.</span><span class="sxs-lookup"><span data-stu-id="19be9-210">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19be9-211">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="19be9-211">Additional resources</span></span>

* [<span data-ttu-id="19be9-212">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="19be9-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19be9-213">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="19be9-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="19be9-214">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="19be9-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



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