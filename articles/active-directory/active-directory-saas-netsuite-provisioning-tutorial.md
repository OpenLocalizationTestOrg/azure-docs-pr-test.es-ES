---
title: "Tutorial: Integración de Azure Active Directory con NetSuite | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 277c393536615fc8bfe8af0bc6d487115f04776c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="440cb-103">Tutorial: Configuración de Netsuite para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="440cb-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="440cb-104">El objetivo de este tutorial es explicar los pasos que hay que realizar en Netsuite y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD en Netsuite.</span><span class="sxs-lookup"><span data-stu-id="440cb-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="440cb-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="440cb-105">Prerequisites</span></span>

<span data-ttu-id="440cb-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="440cb-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="440cb-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="440cb-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="440cb-108">Una suscripción habilitada para el inicio de sesión único en Netsuite.</span><span class="sxs-lookup"><span data-stu-id="440cb-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="440cb-109">Una cuenta de usuario de Netsuite con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="440cb-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-to-netsuite"></a><span data-ttu-id="440cb-110">Asignación de usuarios a Netsuite</span><span class="sxs-lookup"><span data-stu-id="440cb-110">Assigning users to Netsuite</span></span>

<span data-ttu-id="440cb-111">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="440cb-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="440cb-112">En el contexto de aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440cb-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="440cb-113">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Netsuite.</span><span class="sxs-lookup"><span data-stu-id="440cb-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span></span> <span data-ttu-id="440cb-114">Una vez decidido, puede asignar estos usuarios a la aplicación Netsuite siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="440cb-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span></span>

[<span data-ttu-id="440cb-115">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="440cb-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-netsuite"></a><span data-ttu-id="440cb-116">Sugerencias importantes para asignar usuarios a Netsuite</span><span class="sxs-lookup"><span data-stu-id="440cb-116">Important tips for assigning users to Netsuite</span></span>

*   <span data-ttu-id="440cb-117">Se recomienda asignar un único usuario de Azure AD a Netsuite para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="440cb-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span></span> <span data-ttu-id="440cb-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="440cb-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="440cb-119">Al asignar a un usuario a Netsuite, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="440cb-119">When assigning a user to Netsuite, you must select a valid user role.</span></span> <span data-ttu-id="440cb-120">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="440cb-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="440cb-121">Habilitación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="440cb-121">Enable User Provisioning</span></span>

<span data-ttu-id="440cb-122">Esta sección le guía en la conexión de Azure AD a la API de aprovisionamiento de cuentas de usuario de Netsuite, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de Netsuite en función de la asignación de grupos y usuarios Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440cb-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="440cb-123">También puede habilitar el inicio de sesión único basado en SAML para Netsuite siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="440cb-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="440cb-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="440cb-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="440cb-125">Para configurar el aprovisionamiento automático de cuentas de usuario:</span><span class="sxs-lookup"><span data-stu-id="440cb-125">To configure user account provisioning:</span></span>

<span data-ttu-id="440cb-126">El objetivo de esta sección es describir cómo habilitar el aprovisionamiento de cuentas de usuario de Active Directory para Netsuite.</span><span class="sxs-lookup"><span data-stu-id="440cb-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span></span>

1. <span data-ttu-id="440cb-127">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="440cb-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="440cb-128">Si ya ha configurado Netsuite para el inicio de sesión único, busque la instancia de Netsuite mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="440cb-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span></span> <span data-ttu-id="440cb-129">En caso contrario, seleccione **Agregar** y busque **Netsuite** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="440cb-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span></span> <span data-ttu-id="440cb-130">Seleccione Netsuite en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="440cb-130">Select Netsuite from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="440cb-131">Seleccione la instancia de Netsuite y luego, la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="440cb-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="440cb-132">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="440cb-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="440cb-134">En la sección **Credenciales de administrador**, proporcione los siguientes valores de configuración:</span><span class="sxs-lookup"><span data-stu-id="440cb-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="440cb-135">a.</span><span class="sxs-lookup"><span data-stu-id="440cb-135">a.</span></span> <span data-ttu-id="440cb-136">En el cuadro de texto **Nombre de usuario administrador**, escriba un nombre de cuenta de Netsuite que tenga asignado el perfil **Administrador del sistema** en Netsuite.com.</span><span class="sxs-lookup"><span data-stu-id="440cb-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="440cb-137">b.</span><span class="sxs-lookup"><span data-stu-id="440cb-137">b.</span></span> <span data-ttu-id="440cb-138">En el cuadro de texto **Contraseña de administrador**, escriba la contraseña de esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="440cb-138">In the **Admin Password** textbox, type the password for this account.</span></span>
      
6. <span data-ttu-id="440cb-139">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación Netsuite.</span><span class="sxs-lookup"><span data-stu-id="440cb-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span></span>

7. <span data-ttu-id="440cb-140">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla.</span><span class="sxs-lookup"><span data-stu-id="440cb-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="440cb-141">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="440cb-141">Click **Save.**</span></span>

9. <span data-ttu-id="440cb-142">En la sección Asignaciones, seleccione **Sincronizar usuarios de Azure Active Directory con Netsuite.**</span><span class="sxs-lookup"><span data-stu-id="440cb-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span></span>

10. <span data-ttu-id="440cb-143">En la sección **Asignaciones de atributos**, revise los atributos de usuario que se sincronizan entre Azure AD y Netsuite.</span><span class="sxs-lookup"><span data-stu-id="440cb-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span></span> <span data-ttu-id="440cb-144">Tenga en cuenta que los atributos seleccionados como propiedades de **Coincidencia** se usarán para buscar coincidencias con las cuentas de usuario de Netsuite con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="440cb-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="440cb-145">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="440cb-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="440cb-146">Para habilitar el servicio de aprovisionamiento de Azure AD para Netsuite, cambie el **Estado de aprovisionamiento** a **Activado** en la sección Configuración</span><span class="sxs-lookup"><span data-stu-id="440cb-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="440cb-147">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="440cb-147">Click **Save.**</span></span>

<span data-ttu-id="440cb-148">Esta acción inicia la sincronización inicial de todos los usuarios y grupos asignados a Netsuite en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="440cb-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span></span> <span data-ttu-id="440cb-149">Tenga en cuenta que la sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="440cb-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="440cb-150">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de Netsuite.</span><span class="sxs-lookup"><span data-stu-id="440cb-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="440cb-151">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="440cb-151">You can now create a test account.</span></span> <span data-ttu-id="440cb-152">Espere 20 minutos para comprobar que la cuenta se ha sincronizado con Netsuite.</span><span class="sxs-lookup"><span data-stu-id="440cb-152">Wait for up to 20 minutes to verify that the account has been synchronized to Netsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="440cb-153">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="440cb-153">Additional resources</span></span>

* [<span data-ttu-id="440cb-154">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="440cb-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="440cb-155">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="440cb-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="440cb-156">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="440cb-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)