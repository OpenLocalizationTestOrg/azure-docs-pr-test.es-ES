---
title: "Tutorial: Integración de Azure Active Directory con Dropbox for Business | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6f7616e47322242f01a13d763f71c93d4ac06a92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="07368-103">Tutorial: Configuración de Dropbox for Business para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="07368-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="07368-104">El objetivo de este tutorial es explicar los pasos que hay que realizar en Dropbox for Business y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD en Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="07368-104">The objective of this tutorial is to show you the steps you need to perform in Dropbox for Business and Azure AD to automatically provision and de-provision user accounts from Azure AD to Dropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07368-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="07368-105">Prerequisites</span></span>

<span data-ttu-id="07368-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="07368-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="07368-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07368-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="07368-108">Una suscripción a Dropbox for Business con inicio de sesión único habilitado.</span><span class="sxs-lookup"><span data-stu-id="07368-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="07368-109">Una cuenta de usuario de Dropbox for Business con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="07368-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-to-dropbox-for-business"></a><span data-ttu-id="07368-110">Asignación de usuarios a Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="07368-110">Assigning users to Dropbox for Business</span></span>

<span data-ttu-id="07368-111">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="07368-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="07368-112">En el contexto del aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07368-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="07368-113">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="07368-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Dropbox for Business app.</span></span> <span data-ttu-id="07368-114">Una vez decidido, puede asignar estos usuarios a la aplicación Dropbox for Business siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="07368-114">Once decided, you can assign these users to your Dropbox for Business app by following the instructions here:</span></span>

[<span data-ttu-id="07368-115">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="07368-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-dropbox-for-business"></a><span data-ttu-id="07368-116">Sugerencias importantes para asignar usuarios a Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="07368-116">Important tips for assigning users to Dropbox for Business</span></span>

*   <span data-ttu-id="07368-117">Se recomienda asignar un único usuario de Azure AD a Dropbox for Business para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="07368-117">It is recommended that a single Azure AD user is assigned to Dropbox for Business to test the provisioning configuration.</span></span> <span data-ttu-id="07368-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="07368-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="07368-119">Al asignar a un usuario a Dropbox for Business, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="07368-119">When assigning a user to Dropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="07368-120">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="07368-120">The "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="07368-121">Habilitación del aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="07368-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="07368-122">Esta sección lo guía a través de los pasos necesarios para conectar la API de aprovisionamiento de cuentas de usuario de Dropbox for Business, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas en Dropbox for Business en función de la asignación de grupos y usuarios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07368-122">This section guides you through connecting your Azure AD to Dropbox for Business's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="07368-123">Puede elegir también habilitar el inicio de sesión único basado en SAML para Dropbox for Business, mediante las instrucciones que se proporcionan en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07368-123">You may also choose to enabled SAML-based Single Sign-On for Dropbox for Business, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="07368-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="07368-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="07368-125">Para configurar el aprovisionamiento automático de cuentas de usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="07368-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="07368-126">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="07368-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="07368-127">Si ya ha configurado Dropbox for Business para el inicio de sesión único, busque su instancia de Dropbox for Business mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="07368-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using the search field.</span></span> <span data-ttu-id="07368-128">En caso contrario, seleccione **Agregar** y busque **Dropbox for Business** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="07368-128">Otherwise, select **Add** and search for **Dropbox for Business** in the application gallery.</span></span> <span data-ttu-id="07368-129">Seleccione Dropbox for Business en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="07368-129">Select Dropbox for Business from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="07368-130">Seleccione la instancia de Dropbox for Business y luego, la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="07368-130">Select your instance of Dropbox for Business, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="07368-131">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="07368-131">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="07368-133">En **Credenciales de administrador**, haga clic en **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="07368-133">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="07368-134">Se abre un cuadro de diálogo de inicio de sesión de Dropbox for Business en una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="07368-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="07368-135">En el cuadro de diálogo **Sign in to Dropbox to link with Azure AD** (Iniciar sesión en Dropbox para vincularlo a Azure AD), inicie sesión en su inquilino de Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="07368-135">On the **Sign-in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span></span>

     <span data-ttu-id="07368-136">![Aprovisionamiento de usuarios](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Aprovisionamiento de usuarios")</span><span class="sxs-lookup"><span data-stu-id="07368-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="07368-137">Confirme que desea conceder permiso de Azure Active Directory para realizar cambios en el inquilino de Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="07368-137">Confirm that you would like to give Azure Active Directory permission to make changes to your Dropbox for Business tenant.</span></span> <span data-ttu-id="07368-138">Haga clic en **Permitir**.</span><span class="sxs-lookup"><span data-stu-id="07368-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="07368-139">![Aprovisionamiento de usuarios](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Aprovisionamiento de usuarios")</span><span class="sxs-lookup"><span data-stu-id="07368-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="07368-140">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="07368-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Dropbox for Business app.</span></span> <span data-ttu-id="07368-141">Si se produce un error de conexión, asegúrese de que su cuenta de Dropbox for Business tiene permisos de administrador de equipo y vuelva a intentar el paso de **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="07368-141">If the connection fails, ensure your Dropbox for Business account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="07368-142">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error de aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla.</span><span class="sxs-lookup"><span data-stu-id="07368-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="07368-143">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="07368-143">Click **Save.**</span></span>

11. <span data-ttu-id="07368-144">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to Dropbox for Business** (Sincronizar usuarios de Azure Active Directory con Dropbox for Business).</span><span class="sxs-lookup"><span data-stu-id="07368-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Dropbox for Business.**</span></span>

12. <span data-ttu-id="07368-145">En la sección **Attribute Mappings** (Asignaciones de atributos), revise los atributos de usuario que se sincronizan entre Azure AD y Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="07368-145">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Dropbox for Business.</span></span> <span data-ttu-id="07368-146">Tenga en cuenta que los atributos seleccionados como propiedades de **Coincidencia** se usarán para buscar coincidencias con las cuentas de usuario de Dropbox for Business con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="07368-146">The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="07368-147">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="07368-147">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="07368-148">Para habilitar el servicio de aprovisionamiento de Azure AD para Dropbox for Business, cambie el **Estado de aprovisionamiento** a **Activado** en la sección Configuración.</span><span class="sxs-lookup"><span data-stu-id="07368-148">To enable the Azure AD provisioning service for Dropbox for Business, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="07368-149">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="07368-149">Click **Save.**</span></span>

<span data-ttu-id="07368-150">Comienza la sincronización inicial de todos los usuarios y grupos asignados a Dropbox for Business en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="07368-150">It starts the initial synchronization of any users and/or groups assigned to Dropbox for Business in the Users and Groups section.</span></span> <span data-ttu-id="07368-151">La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="07368-151">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="07368-152">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y seguir los vínculos a los informes de actividad de aprovisionamiento, donde se describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="07368-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="07368-153">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="07368-153">You can now create a test account.</span></span> <span data-ttu-id="07368-154">Espere 20 minutos para comprobar que la cuenta se ha sincronizado con Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="07368-154">Wait for up to 20 minutes to verify that the account has been synchronized to Dropbox for Business.</span></span>

<span data-ttu-id="07368-155">Un ciclo de aprovisionamiento de usuarios completado correctamente se indica con un estado relacionado:</span><span class="sxs-lookup"><span data-stu-id="07368-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="07368-156">![Asignar usuarios](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="07368-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="07368-157">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="07368-157">Additional resources</span></span>

* [<span data-ttu-id="07368-158">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="07368-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07368-159">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07368-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="07368-160">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="07368-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)