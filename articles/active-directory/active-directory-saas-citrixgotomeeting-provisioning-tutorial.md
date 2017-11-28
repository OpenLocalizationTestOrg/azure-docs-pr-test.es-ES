---
title: "Tutorial: Integración de Azure Active Directory con Citrix GoToMeeting | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="bd43f-103">Tutorial: Configuración de Citrix GoToMeeting para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="bd43f-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="bd43f-104">El objetivo de este tutorial es explicar los pasos que debe realizar en Citrix GoToMeeting y Azure AD para aprovisionar y cancelar el aprovisionamiento de cuentas de usuario de Azure AD para Citrix GoToMeeting automáticamente.</span><span class="sxs-lookup"><span data-stu-id="bd43f-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd43f-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bd43f-105">Prerequisites</span></span>

<span data-ttu-id="bd43f-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bd43f-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="bd43f-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bd43f-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="bd43f-108">Una suscripción habilitada para el inicio de sesión único en Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bd43f-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="bd43f-109">Una cuenta de usuario de Citrix GoToMeeting con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="bd43f-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="bd43f-110">Asignación de usuarios a Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="bd43f-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="bd43f-111">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bd43f-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="bd43f-112">En el contexto del aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd43f-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="bd43f-113">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bd43f-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="bd43f-114">Una vez decidido, puede asignar estos usuarios a la aplicación de Citrix GoToMeeting siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="bd43f-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="bd43f-115">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="bd43f-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="bd43f-116">Sugerencias importantes para asignar usuarios a Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="bd43f-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="bd43f-117">Se recomienda asignar un único usuario de Azure AD a Citrix GoToMeeting para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="bd43f-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="bd43f-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="bd43f-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bd43f-119">Al asignar a un usuario a Citrix GoToMeeting, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="bd43f-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="bd43f-120">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="bd43f-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="bd43f-121">Habilitación del aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="bd43f-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="bd43f-122">Esta sección lo guía a través de los pasos necesarios para conectar la API de aprovisionamiento de cuentas de usuario de Citrix GoToMeeting, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas en Citrix GoToMeeting en función de la asignación de grupos y usuarios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd43f-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="bd43f-123">También puede decidir habilitar el inicio de sesión único basado en SAML para Citrix GoToMeeting siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd43f-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bd43f-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="bd43f-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="bd43f-125">Para configurar el aprovisionamiento automático de cuentas de usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bd43f-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="bd43f-126">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bd43f-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="bd43f-127">Si ya ha configurado Citrix GoToMeeting para el inicio de sesión único, busque la instancia de Citrix GoToMeeting con el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="bd43f-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="bd43f-128">En caso contrario, seleccione **Agregar** y busque **Citrix GoToMeeting** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bd43f-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="bd43f-129">Seleccione Citrix GoToMeeting en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bd43f-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="bd43f-130">Seleccione la instancia de Citrix GoToMeeting y seleccione la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="bd43f-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="bd43f-131">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="bd43f-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="bd43f-133">En la sección Credenciales de administración, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bd43f-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="bd43f-134">a.</span><span class="sxs-lookup"><span data-stu-id="bd43f-134">a.</span></span> <span data-ttu-id="bd43f-135">En el cuadro de texto **Nombre de usuario de administrador de Citrix GoToMeeting** , escriba el nombre de usuario de un administrador.</span><span class="sxs-lookup"><span data-stu-id="bd43f-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="bd43f-136">b.</span><span class="sxs-lookup"><span data-stu-id="bd43f-136">b.</span></span> <span data-ttu-id="bd43f-137">En el cuadro de texto **Contraseña de administrador de Citrix GoToMeeting** , escriba la contraseña del administrador.</span><span class="sxs-lookup"><span data-stu-id="bd43f-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="bd43f-138">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación de Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bd43f-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="bd43f-139">Si se produce un error de conexión, asegúrese de que su cuenta de Citrix GoToMeeting tiene permisos de administrador de equipo y vuelva a intentar el paso de **"Credenciales de administración"**.</span><span class="sxs-lookup"><span data-stu-id="bd43f-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="bd43f-140">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error de aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla.</span><span class="sxs-lookup"><span data-stu-id="bd43f-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="bd43f-141">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bd43f-141">Click **Save.**</span></span>

9. <span data-ttu-id="bd43f-142">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to Citrix GoToMeeting** (Sincronizar usuarios de Azure Active Directory con Citrix GoToMeeting).</span><span class="sxs-lookup"><span data-stu-id="bd43f-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="bd43f-143">En la sección **Attribute Mappings** (Asignaciones de atributos), revise los atributos de usuario que se sincronizan entre Azure AD y Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bd43f-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="bd43f-144">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de Citrix GoToMeeting con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="bd43f-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="bd43f-145">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="bd43f-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="bd43f-146">Para habilitar el servicio de aprovisionamiento de Azure AD para Citrix GoToMeeting, cambie el **Estado de aprovisionamiento** a **Activado** en la sección Configuración.</span><span class="sxs-lookup"><span data-stu-id="bd43f-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="bd43f-147">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bd43f-147">Click **Save.**</span></span>

<span data-ttu-id="bd43f-148">Comienza la sincronización inicial de todos los usuarios y grupos asignados a Citrix GoToMeeting en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="bd43f-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="bd43f-149">La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos, si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="bd43f-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="bd43f-150">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bd43f-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd43f-151">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bd43f-151">Additional resources</span></span>

* [<span data-ttu-id="bd43f-152">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="bd43f-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd43f-153">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd43f-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bd43f-154">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="bd43f-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


