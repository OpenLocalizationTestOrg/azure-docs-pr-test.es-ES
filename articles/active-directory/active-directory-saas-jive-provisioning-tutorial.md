---
title: "Tutorial: Integración de Azure Active Directory con Jive | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 957b152fdd40d08a867e788b0cb9f7d57ed481e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="0210c-103">Tutorial: Configuración de Jive para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="0210c-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="0210c-104">El objetivo de este tutorial es explicar los pasos que debe realizar en Jive y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD para Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0210c-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0210c-105">Prerequisites</span></span>

<span data-ttu-id="0210c-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0210c-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="0210c-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0210c-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="0210c-108">Una suscripción habilitada para inicio de sesión único en Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="0210c-109">Una cuenta de usuario de Jive con permisos de Team Admin (administrador de equipo).</span><span class="sxs-lookup"><span data-stu-id="0210c-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="0210c-110">Asignación de usuarios a Jive</span><span class="sxs-lookup"><span data-stu-id="0210c-110">Assigning users to Jive</span></span>

<span data-ttu-id="0210c-111">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0210c-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="0210c-112">En el contexto del aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0210c-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="0210c-113">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="0210c-114">Una vez decidido, puede asignar estos usuarios a la aplicación de Jive siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="0210c-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="0210c-115">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="0210c-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="0210c-116">Sugerencias importantes para asignar usuarios a Jive</span><span class="sxs-lookup"><span data-stu-id="0210c-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="0210c-117">Se recomienda asignar un único usuario de Azure AD a Jive para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="0210c-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="0210c-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="0210c-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0210c-119">Al asignar a un usuario a Jive, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="0210c-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="0210c-120">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="0210c-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="0210c-121">Habilitación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="0210c-121">Enable User Provisioning</span></span>

<span data-ttu-id="0210c-122">Esta sección le guía en la conexión de Azure AD a la API de aprovisionamiento de cuentas de usuario de Jive, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de Jive en función de la asignación de grupos y usuarios Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0210c-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="0210c-123">También puede habilitar el inicio de sesión único basado en SAML para Jive siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0210c-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0210c-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="0210c-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="0210c-125">Para configurar el aprovisionamiento automático de cuentas de usuario:</span><span class="sxs-lookup"><span data-stu-id="0210c-125">To configure user account provisioning:</span></span>

<span data-ttu-id="0210c-126">El objetivo de esta sección es describir cómo habilitar el aprovisionamiento de cuentas de usuario de Active Directory para Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="0210c-127">Como parte de este procedimiento, es necesario proporcionar un token de seguridad de usuario que deberá solicitar a Jive.com.</span><span class="sxs-lookup"><span data-stu-id="0210c-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="0210c-128">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0210c-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="0210c-129">Si ya ha configurado Jive para el inicio de sesión único, busque la instancia de Jive mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0210c-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="0210c-130">En caso contrario, seleccione **Agregar** y busque **Jive** en la Galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0210c-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="0210c-131">Seleccione Jive en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0210c-131">Select Jive from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="0210c-132">Seleccione la instancia de Jive y, después, seleccione la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="0210c-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="0210c-133">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="0210c-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="0210c-135">En la sección **Credenciales de administrador**, proporcione los siguientes valores de configuración:</span><span class="sxs-lookup"><span data-stu-id="0210c-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="0210c-136">a.</span><span class="sxs-lookup"><span data-stu-id="0210c-136">a.</span></span> <span data-ttu-id="0210c-137">En el cuadro de texto **Nombre de usuario del administrador de Jive**, escriba un nombre de cuenta de Jive que tenga asignado el perfil **Administrador del sistema** en Jive.com.</span><span class="sxs-lookup"><span data-stu-id="0210c-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="0210c-138">b.</span><span class="sxs-lookup"><span data-stu-id="0210c-138">b.</span></span> <span data-ttu-id="0210c-139">En el cuadro de texto **Contraseña de administrador de Jive** , escriba la contraseña para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="0210c-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="0210c-140">c.</span><span class="sxs-lookup"><span data-stu-id="0210c-140">c.</span></span> <span data-ttu-id="0210c-141">En el cuadro de texto **Dirección URL de inquilino de Jive** , escriba la dirección URL del inquilino de Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="0210c-142">La dirección URL del inquilino de Jive es la que se usa en su organización para iniciar sesión en Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="0210c-143">Normalmente, la dirección URL tiene el formato siguiente: **www.\<organización\>.jive.com**.</span><span class="sxs-lookup"><span data-stu-id="0210c-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="0210c-144">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación de Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

7. <span data-ttu-id="0210c-145">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla que aparece a continuación.</span><span class="sxs-lookup"><span data-stu-id="0210c-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

8. <span data-ttu-id="0210c-146">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0210c-146">Click **Save.**</span></span>

9. <span data-ttu-id="0210c-147">En la sección Asignaciones, seleccione **Sincronizar usuarios de Azure Active Directory con Jive.**</span><span class="sxs-lookup"><span data-stu-id="0210c-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

10. <span data-ttu-id="0210c-148">En la sección **Asignaciones de atributos**, revise los atributos de usuario que se sincronizan entre Azure AD y Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="0210c-149">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de Jive con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="0210c-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="0210c-150">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="0210c-150">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="0210c-151">Para habilitar el servicio de aprovisionamiento de Azure AD para Jive, cambie el **Estado de aprovisionamiento** a **Activado** en la sección Configuración</span><span class="sxs-lookup"><span data-stu-id="0210c-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="0210c-152">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0210c-152">Click **Save.**</span></span>

<span data-ttu-id="0210c-153">Esta acción inicia la sincronización inicial de todos los usuarios y grupos asignados a Jive en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="0210c-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="0210c-154">La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos, si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="0210c-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="0210c-155">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="0210c-156">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="0210c-156">You can now create a test account.</span></span> <span data-ttu-id="0210c-157">Espere 20 minutos para comprobar que la cuenta se ha sincronizado con Jive.</span><span class="sxs-lookup"><span data-stu-id="0210c-157">Wait for up to 20 minutes to verify that the account has been synchronized to Jive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0210c-158">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0210c-158">Additional resources</span></span>

* [<span data-ttu-id="0210c-159">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="0210c-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0210c-160">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0210c-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0210c-161">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="0210c-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)