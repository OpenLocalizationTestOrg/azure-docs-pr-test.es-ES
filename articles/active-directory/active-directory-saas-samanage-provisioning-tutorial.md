---
title: "Tutorial: Configuración de Samanage para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información sobre cómo configurar Azure Active Directory para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Samanage."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 278ebf464fbe815568fbe332f80d5ea6b29e1811
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="f9109-103">Tutorial: Configuración de Samanage para aprovisionar a los usuarios automáticamente</span><span class="sxs-lookup"><span data-stu-id="f9109-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="f9109-104">El objetivo de este tutorial es explicar los pasos que debe realizar en Samanage y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD para Samanage.</span><span class="sxs-lookup"><span data-stu-id="f9109-104">The objective of this tutorial is to show you the steps you need to perform in Samanage and Azure AD to automatically provision and de-provision user accounts from Azure AD to Samanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f9109-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f9109-105">Prerequisites</span></span>

<span data-ttu-id="f9109-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f9109-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="f9109-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9109-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="f9109-108">Un inquilino de Samanage con el [plan Professional](https://www.samanage.com/pricing/) habilitado o uno superior</span><span class="sxs-lookup"><span data-stu-id="f9109-108">A Samanage tenant with the [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="f9109-109">Una cuenta de usuario de Samanage con permisos de administrador</span><span class="sxs-lookup"><span data-stu-id="f9109-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="f9109-110">La integración del aprovisionamiento de Azure AD se basa en la [API de Samanage de REST](https://www.samanage.com/api/), que está disponible para los equipos de Samanage con el plan Professional o uno superior.</span><span class="sxs-lookup"><span data-stu-id="f9109-110">The Azure AD provisioning integration relies on the [Samanage REST API](https://www.samanage.com/api/), which is available to Samanage teams on the Professional plan or better.</span></span>

## <a name="assigning-users-to-samanage"></a><span data-ttu-id="f9109-111">Asignación de usuarios a Samanage</span><span class="sxs-lookup"><span data-stu-id="f9109-111">Assigning users to Samanage</span></span>

<span data-ttu-id="f9109-112">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f9109-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="f9109-113">En el contexto del aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9109-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="f9109-114">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Samanage.</span><span class="sxs-lookup"><span data-stu-id="f9109-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Samanage app.</span></span> <span data-ttu-id="f9109-115">Una vez decidido, puede asignar estos usuarios a la aplicación de Samanage siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="f9109-115">Once decided, you can assign these users to your Samanage app by following the instructions here:</span></span>

[<span data-ttu-id="f9109-116">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="f9109-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-samanage"></a><span data-ttu-id="f9109-117">Sugerencias importantes para asignar usuarios a Samanage</span><span class="sxs-lookup"><span data-stu-id="f9109-117">Important tips for assigning users to Samanage</span></span>

*   <span data-ttu-id="f9109-118">Se recomienda asignar un único usuario de Azure AD a Samanage para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="f9109-118">It is recommended that a single Azure AD user is assigned to Samanage to test the provisioning configuration.</span></span> <span data-ttu-id="f9109-119">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="f9109-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f9109-120">Al asignar un usuario a Samanage, debe seleccionar el rol **Usuario** u otro válido específico de la aplicación (si está disponible) en el cuadro de diálogo de asignación.</span><span class="sxs-lookup"><span data-stu-id="f9109-120">When assigning a user to Samanage, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="f9109-121">El rol **Acceso predeterminado** no funciona para realizar el aprovisionamiento y estos usuarios se omiten.</span><span class="sxs-lookup"><span data-stu-id="f9109-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="f9109-122">Como característica agregada, el servicio de aprovisionamiento lee los roles personalizados definidos en Samanage y los importa en Azure AD, donde se pueden seleccionar en el cuadro de diálogo Seleccionar rol.</span><span class="sxs-lookup"><span data-stu-id="f9109-122">As an added feature, the provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in the Select Role dialog.</span></span> <span data-ttu-id="f9109-123">Estos roles se verán en Azure Portal después de habilitar el servicio de aprovisionamiento y de completarse un ciclo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="f9109-123">These roles will be visible in the Azure portal after the provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-to-samanage"></a><span data-ttu-id="f9109-124">Configuración del aprovisionamiento de usuarios en Samanage</span><span class="sxs-lookup"><span data-stu-id="f9109-124">Configuring user provisioning to Samanage</span></span> 

<span data-ttu-id="f9109-125">Esta sección lo guía a través de los pasos necesarios para conectar la API de aprovisionamiento de su cuenta de usuario de Samanage, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de Samanage en función de la asignación de grupos y usuarios Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9109-125">This section guides you through connecting your Azure AD to Samanage's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="f9109-126">También puede decidir habilitar el inicio de sesión único basado en SAML para Samanage siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9109-126">You may also choose to enabled SAML-based Single Sign-On for Samanage, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f9109-127">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="f9109-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-samanage-in-azure-ad"></a><span data-ttu-id="f9109-128">Para configurar el aprovisionamiento de cuentas de usuario automático para Samanage en Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f9109-128">Configure automatic user account provisioning to Samanage in Azure AD:</span></span>


1. <span data-ttu-id="f9109-129">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f9109-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="f9109-130">Si ya ha configurado Samanage para el inicio de sesión único, busque la instancia de Samanage mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f9109-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using the search field.</span></span> <span data-ttu-id="f9109-131">En caso contrario, seleccione **Agregar** y busque **Samanage** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f9109-131">Otherwise, select **Add** and search for **Samanage** in the application gallery.</span></span> <span data-ttu-id="f9109-132">Seleccione Samanage en los resultados de la búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f9109-132">Select Samanage from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="f9109-133">Seleccione la instancia de Samanage y, después, seleccione la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="f9109-133">Select your instance of Samanage, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="f9109-134">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="f9109-134">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Aprovisionamiento de Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="f9109-136">En la sección **Credenciales de administrador**, escriba **el nombre de usuario y la contraseña de administrador** de la cuenta de Samanage.</span><span class="sxs-lookup"><span data-stu-id="f9109-136">Under the **Admin Credentials** section, input the **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="f9109-137">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación Samanage.</span><span class="sxs-lookup"><span data-stu-id="f9109-137">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Samanage app.</span></span> <span data-ttu-id="f9109-138">Si la conexión no se establece, asegúrese de que la cuenta de Samanage tiene permisos de administrador de equipo e intente el paso 5 de nuevo.</span><span class="sxs-lookup"><span data-stu-id="f9109-138">If the connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="f9109-139">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error de aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla "Enviar una notificación por correo electrónico cuando se produzca un error".</span><span class="sxs-lookup"><span data-stu-id="f9109-139">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="f9109-140">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f9109-140">Click **Save**.</span></span> 

9. <span data-ttu-id="f9109-141">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to** (Sincronizar usuarios de Azure Active Directory con Samanage).</span><span class="sxs-lookup"><span data-stu-id="f9109-141">Under the Mappings section, select **Synchronize Azure Active Directory Users to Samanage**.</span></span>

10. <span data-ttu-id="f9109-142">En la sección **Attribute Mappings** (Asignaciones de atributos), revise los atributos de usuario que se sincronizan entre Azure AD y Samanage.</span><span class="sxs-lookup"><span data-stu-id="f9109-142">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Samanage.</span></span> <span data-ttu-id="f9109-143">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de Samanage con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="f9109-143">The attributes selected as **Matching** properties are used to match the user accounts in Samanage for update operations.</span></span> <span data-ttu-id="f9109-144">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="f9109-144">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="f9109-145">Para habilitar el aprovisionamiento del servicio de aprovisionamiento de Azure AD para Samanage, cambie el **estado de aprovisionamiento** a **Activado** en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="f9109-145">To enable the Azure AD provisioning service for Samanage, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="f9109-146">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f9109-146">Click **Save**.</span></span> 

<span data-ttu-id="f9109-147">Esta operación inicia la sincronización inicial de todos los usuarios y grupos asignados a Samanage en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="f9109-147">This operation starts the initial synchronization of any users and/or groups assigned to Samanage in the Users and Groups section.</span></span> <span data-ttu-id="f9109-148">La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="f9109-148">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="f9109-149">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="f9109-149">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="f9109-150">Para más información sobre cómo leer los registros de aprovisionamiento de Azure AD, consulte [Creación de informes sobre el aprovisionamiento automático de cuentas de usuario](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="f9109-150">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f9109-151">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f9109-151">Additional resources</span></span>

* [<span data-ttu-id="f9109-152">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="f9109-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="f9109-153">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f9109-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="f9109-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9109-154">Next steps</span></span>

* [<span data-ttu-id="f9109-155">Aprenda a revisar los registros y a obtener informes sobre la actividad de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="f9109-155">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
