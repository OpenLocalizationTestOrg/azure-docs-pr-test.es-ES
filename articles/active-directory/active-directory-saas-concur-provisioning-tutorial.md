---
title: "Tutorial: integración de Azure Active Directory con Concur | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="4d099-103">Tutorial: Configuración de Concur para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="4d099-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="4d099-104">El objetivo de este tutorial es explicar los pasos que hay que realizar en Concur y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD en Concur.</span><span class="sxs-lookup"><span data-stu-id="4d099-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d099-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4d099-105">Prerequisites</span></span>

<span data-ttu-id="4d099-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4d099-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="4d099-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4d099-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="4d099-108">Una suscripción habilitada para el inicio de sesión único en Concur.</span><span class="sxs-lookup"><span data-stu-id="4d099-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="4d099-109">Una cuenta de usuario de Concur con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="4d099-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="4d099-110">Asignación de usuarios a Concur</span><span class="sxs-lookup"><span data-stu-id="4d099-110">Assigning users to Concur</span></span>

<span data-ttu-id="4d099-111">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4d099-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4d099-112">En el contexto del aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d099-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="4d099-113">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Concur.</span><span class="sxs-lookup"><span data-stu-id="4d099-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="4d099-114">Una vez decidido, puede asignar estos usuarios a la aplicación de Concur siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="4d099-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="4d099-115">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="4d099-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="4d099-116">Sugerencias importantes para asignar usuarios a Concur</span><span class="sxs-lookup"><span data-stu-id="4d099-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="4d099-117">Se recomienda asignar un solo usuario de Azure AD a Concur para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="4d099-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="4d099-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="4d099-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4d099-119">Al asignar a un usuario a Concur, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="4d099-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="4d099-120">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="4d099-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="4d099-121">Habilitación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="4d099-121">Enable user provisioning</span></span>

<span data-ttu-id="4d099-122">Esta sección lo guía a través de los pasos necesarios para conectar la API de aprovisionamiento de cuentas de usuario de Concur, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas en Concur en función de la asignación de grupos y usuarios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d099-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="4d099-123">También puede habilitar el inicio de sesión único basado en Concur para Concur siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d099-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4d099-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="4d099-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="4d099-125">Para configurar el aprovisionamiento automático de cuentas de usuario:</span><span class="sxs-lookup"><span data-stu-id="4d099-125">To configure user account provisioning:</span></span>

<span data-ttu-id="4d099-126">El objetivo de esta sección es describir cómo habilitar el aprovisionamiento de las cuentas de usuario de Active Directory en Concur.</span><span class="sxs-lookup"><span data-stu-id="4d099-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="4d099-127">Para habilitar las aplicaciones en el servicio de gastos, debe tener la configuración correcta y el uso de un perfil de administrador de servicio web.</span><span class="sxs-lookup"><span data-stu-id="4d099-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="4d099-128">No agregue el rol de administrador de servicio web al perfil de administrador existente que se usa para las funciones administrativas de tiempo y gastos.</span><span class="sxs-lookup"><span data-stu-id="4d099-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="4d099-129">Los asesores de Concur o el administrador de cliente deben crear un perfil de administrador de servicios web distinto y el administrador de cliente debe usar este perfil para las funciones de administrador de servicios web (por ejemplo, para habilitar aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="4d099-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="4d099-130">Estos perfiles deben mantenerse separados a diario del perfil de administración de tiempos y gastos del administrador de cliente (el perfil de administrador de tiempos y gastos no debe tener el rol de administrador de servicios web asignado).</span><span class="sxs-lookup"><span data-stu-id="4d099-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="4d099-131">Al crear el perfil que se usará para habilitar la aplicación, escriba el nombre del administrador de cliente en los campos de perfil de usuario.</span><span class="sxs-lookup"><span data-stu-id="4d099-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="4d099-132">Así se asigna la propiedad al perfil.</span><span class="sxs-lookup"><span data-stu-id="4d099-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="4d099-133">Una vez creado el perfil, el cliente debe iniciar sesión con este perfil para hacer clic en el botón *Habilitar* para una aplicación asociada en el menú de servicios web.</span><span class="sxs-lookup"><span data-stu-id="4d099-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="4d099-134">Por las siguientes razones, esta acción no debe realizarse con el perfil que se usa en la administración normal de tiempo y gastos.</span><span class="sxs-lookup"><span data-stu-id="4d099-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="4d099-135">El cliente tiene que ser el que hace clic en "*Sí*" en la ventana de cuadro de diálogo que aparece después de la habilitación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d099-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="4d099-136">Este clic confirma que el cliente está autorizado por la aplicación asociada a tener acceso a sus datos, por lo que usted o el asociado no pueden hacer clic en el botón Sí.</span><span class="sxs-lookup"><span data-stu-id="4d099-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="4d099-137">Si un administrador de cliente que ha habilitado una aplicación mediante el perfil de administrador de tiempo y gastos abandona la empresa (lo que da lugar a la desactivación del perfil), las aplicaciones habilitadas mediante ese perfil no funcionarán hasta que la aplicación se habilite con otro perfil de administrador de servicios web activo.</span><span class="sxs-lookup"><span data-stu-id="4d099-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="4d099-138">Es por este motivo por lo hay que crear distintos perfiles de administrador servicios web.</span><span class="sxs-lookup"><span data-stu-id="4d099-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="4d099-139">Si un administrador deja la compañía, el nombre asociado al perfil de administrador de servicios web puede cambiarse si se quiere por el del administrador de sustitución sin afectar a la aplicación habilitada, porque no necesita ese perfil desactivado.</span><span class="sxs-lookup"><span data-stu-id="4d099-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="4d099-140">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="4d099-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="4d099-141">Inicie sesión en el inquilino de **Concur**.</span><span class="sxs-lookup"><span data-stu-id="4d099-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="4d099-142">En el menú **Administración**, seleccione **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="4d099-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="4d099-143">![Inquilino de Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Inquilino de Concur")</span><span class="sxs-lookup"><span data-stu-id="4d099-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="4d099-144">En el lado izquierdo, en el panel **Servicios web**, seleccione **Habilitar aplicación de asociado**.</span><span class="sxs-lookup"><span data-stu-id="4d099-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="4d099-145">![Habilitar aplicación de asociado](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Habilitar aplicación de asociado")</span><span class="sxs-lookup"><span data-stu-id="4d099-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="4d099-146">En la lista **Habilitar aplicación**, seleccione **Azure Active Directory** y después haga clic en **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="4d099-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="4d099-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4d099-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="4d099-148">Haga clic en **Sí** para cerrar el cuadro de diálogo **Confirmar acción**.</span><span class="sxs-lookup"><span data-stu-id="4d099-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="4d099-149">![Confirmar acción](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirmar acción")</span><span class="sxs-lookup"><span data-stu-id="4d099-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="4d099-150">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4d099-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="4d099-151">Si ya ha configurado Concur para el inicio de sesión único, busque la instancia de Concur mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4d099-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="4d099-152">En caso contrario, seleccione **Agregar** y busque **Concur** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4d099-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="4d099-153">Seleccione Concur en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4d099-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="4d099-154">Seleccione la instancia de Concur y luego, la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="4d099-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="4d099-155">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="4d099-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![Aprovisionamiento](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="4d099-157">En la sección **Credenciales de administrador**, escriba el **nombre de usuario** y la **contraseña** del administrador de Concur.</span><span class="sxs-lookup"><span data-stu-id="4d099-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="4d099-158">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación de Concur.</span><span class="sxs-lookup"><span data-stu-id="4d099-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="4d099-159">Si la conexión no se establece, asegúrese de que la cuenta de Concur tiene permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="4d099-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="4d099-160">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error de aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla.</span><span class="sxs-lookup"><span data-stu-id="4d099-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="4d099-161">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4d099-161">Click **Save.**</span></span>

14. <span data-ttu-id="4d099-162">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to Concur** (Sincronizar usuarios de Azure Active Directory con Concur).</span><span class="sxs-lookup"><span data-stu-id="4d099-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="4d099-163">En la sección **Attribute Mappings** (Asignaciones de atributos), revise los atributos de usuario que se sincronizan entre Azure AD y Concur.</span><span class="sxs-lookup"><span data-stu-id="4d099-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="4d099-164">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de Concur con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="4d099-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="4d099-165">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="4d099-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="4d099-166">Para habilitar el servicio de aprovisionamiento de Azure AD para Concur, cambie el **Estado de aprovisionamiento** a **Activado** en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="4d099-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="4d099-167">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4d099-167">Click **Save.**</span></span>

<span data-ttu-id="4d099-168">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="4d099-168">You can now create a test account.</span></span> <span data-ttu-id="4d099-169">Espere 20 minutos para comprobar que la cuenta se ha sincronizado con Concur.</span><span class="sxs-lookup"><span data-stu-id="4d099-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4d099-170">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4d099-170">Additional resources</span></span>

* [<span data-ttu-id="4d099-171">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="4d099-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d099-172">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d099-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4d099-173">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="4d099-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

