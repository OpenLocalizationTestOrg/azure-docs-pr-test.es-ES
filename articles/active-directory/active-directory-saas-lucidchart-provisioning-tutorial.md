---
title: "Tutorial: Configuración de LucidChart para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información sobre cómo configurar Azure Active Directory para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de LucidChart."
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
ms.openlocfilehash: 1f9344a5e750360e21ed7dc8e3ed013c2c2e1a45
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="9f860-103">Tutorial: Configuración de LucidChart para aprovisionar a los usuarios automáticamente</span><span class="sxs-lookup"><span data-stu-id="9f860-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="9f860-104">El objetivo de este tutorial es explicar los pasos que hay que realizar en LucidChart y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD en LucidChart.</span><span class="sxs-lookup"><span data-stu-id="9f860-104">The objective of this tutorial is to show you the steps you need to perform in LucidChart and Azure AD to automatically provision and de-provision user accounts from Azure AD to LucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9f860-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9f860-105">Prerequisites</span></span>

<span data-ttu-id="9f860-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f860-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="9f860-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f860-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="9f860-108">Un inquilino de LucidChart con el [plan Enterprise](https://www.lucidchart.com/user/117598685#/subscriptionLevel) o uno superior habilitado</span><span class="sxs-lookup"><span data-stu-id="9f860-108">A LucidChart tenant with the [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="9f860-109">Una cuenta de usuario de LucidChart con permisos de administrador</span><span class="sxs-lookup"><span data-stu-id="9f860-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-to-lucidchart"></a><span data-ttu-id="9f860-110">Asignación de usuarios a LucidChart</span><span class="sxs-lookup"><span data-stu-id="9f860-110">Assigning users to LucidChart</span></span>

<span data-ttu-id="9f860-111">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9f860-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9f860-112">En el contexto del aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f860-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="9f860-113">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación LucidChart.</span><span class="sxs-lookup"><span data-stu-id="9f860-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your LucidChart app.</span></span> <span data-ttu-id="9f860-114">Una vez decidido, puede asignar estos usuarios a la aplicación LucidChart siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="9f860-114">Once decided, you can assign these users to your LucidChart app by following the instructions here:</span></span>

[<span data-ttu-id="9f860-115">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="9f860-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-lucidchart"></a><span data-ttu-id="9f860-116">Sugerencias importantes para asignar usuarios a LucidChart</span><span class="sxs-lookup"><span data-stu-id="9f860-116">Important tips for assigning users to LucidChart</span></span>

*   <span data-ttu-id="9f860-117">Se recomienda asignar un único usuario de Azure AD a LucidChart para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="9f860-117">It is recommended that a single Azure AD user is assigned to LucidChart to test the provisioning configuration.</span></span> <span data-ttu-id="9f860-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="9f860-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9f860-119">Al asignar un usuario a LucidChart, debe seleccionar el rol **Usuario** u otro válido específico de la aplicación (si está disponible) en el cuadro de diálogo de asignación.</span><span class="sxs-lookup"><span data-stu-id="9f860-119">When assigning a user to LucidChart, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="9f860-120">El rol **Acceso predeterminado** no funciona para realizar el aprovisionamiento y estos usuarios se omiten.</span><span class="sxs-lookup"><span data-stu-id="9f860-120">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-lucidchart"></a><span data-ttu-id="9f860-121">Configuración del aprovisionamiento de usuarios en LucidChart</span><span class="sxs-lookup"><span data-stu-id="9f860-121">Configuring user provisioning to LucidChart</span></span> 

<span data-ttu-id="9f860-122">Esta sección le guía en la conexión de Azure AD a la API de aprovisionamiento de cuentas de usuario de LucidChart, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de LucidChart en función de la asignación de grupos y usuarios Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f860-122">This section guides you through connecting your Azure AD to LucidChart's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="9f860-123">También puede habilitar el inicio de sesión único basado en SAML para LucidChart siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9f860-123">You may also choose to enabled SAML-based Single Sign-On for LucidChart, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9f860-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="9f860-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-lucidchart-in-azure-ad"></a><span data-ttu-id="9f860-125">Configuración del aprovisionamiento de cuentas de usuario automático para LucidChart en Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f860-125">Configure automatic user account provisioning to LucidChart in Azure AD</span></span>


1. <span data-ttu-id="9f860-126">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9f860-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="9f860-127">Si ya ha configurado LucidChart para el inicio de sesión único, busque la instancia de LucidChart mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9f860-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using the search field.</span></span> <span data-ttu-id="9f860-128">En caso contrario, seleccione **Agregar** y busque **LucidChart** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9f860-128">Otherwise, select **Add** and search for **LucidChart** in the application gallery.</span></span> <span data-ttu-id="9f860-129">Seleccione LucidChart en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9f860-129">Select LucidChart from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="9f860-130">Seleccione la instancia de LucidChart y luego, la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="9f860-130">Select your instance of LucidChart, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="9f860-131">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="9f860-131">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Aprovisionamiento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="9f860-133">En la sección **Credenciales de administrador**, escriba el **Token secreto** generado por la cuenta de LucidChart (puede encontrar el token en su cuenta: **Equipo** > **Integración de la aplicación** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="9f860-133">Under the **Admin Credentials** section, input the **Secret Token** generated by your LucidChart's account (you can find the token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Aprovisionamiento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="9f860-135">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación de LucidChart.</span><span class="sxs-lookup"><span data-stu-id="9f860-135">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your LucidChart app.</span></span> <span data-ttu-id="9f860-136">Si la conexión no se establece, asegúrese de que la cuenta de LucidChart tiene permisos de administrador e intente el paso 5 de nuevo.</span><span class="sxs-lookup"><span data-stu-id="9f860-136">If the connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="9f860-137">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error de aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla "Enviar una notificación por correo electrónico cuando se produzca un error".</span><span class="sxs-lookup"><span data-stu-id="9f860-137">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="9f860-138">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9f860-138">Click **Save**.</span></span> 

9. <span data-ttu-id="9f860-139">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to LucidChart** (Sincronizar usuarios de Azure Active Directory con LucidChart).</span><span class="sxs-lookup"><span data-stu-id="9f860-139">Under the Mappings section, select **Synchronize Azure Active Directory Users to LucidChart**.</span></span>

10. <span data-ttu-id="9f860-140">En la sección **Attribute Mappings** (Asignaciones de atributos), revise los atributos de usuario que se sincronizan entre Azure AD y LucidChart.</span><span class="sxs-lookup"><span data-stu-id="9f860-140">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to LucidChart.</span></span> <span data-ttu-id="9f860-141">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de LucidChart con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="9f860-141">The attributes selected as **Matching** properties are used to match the user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="9f860-142">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="9f860-142">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="9f860-143">Para habilitar el servicio de aprovisionamiento de Azure AD para LucidChart, cambie el **Estado de aprovisionamiento** a **Activado** en la sección **Configuración**</span><span class="sxs-lookup"><span data-stu-id="9f860-143">To enable the Azure AD provisioning service for LucidChart, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="9f860-144">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9f860-144">Click **Save**.</span></span> 

<span data-ttu-id="9f860-145">Esta operación inicia la sincronización inicial de todos los usuarios y grupos asignados a LucidChart en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="9f860-145">This operation starts the initial synchronization of any users and/or groups assigned to LucidChart in the Users and Groups section.</span></span> <span data-ttu-id="9f860-146">La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos, si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="9f860-146">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="9f860-147">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="9f860-147">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="9f860-148">Para más información sobre cómo leer los registros de aprovisionamiento de Azure AD, consulte [Creación de informes sobre el aprovisionamiento automático de cuentas de usuario](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="9f860-148">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9f860-149">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9f860-149">Additional resources</span></span>

* [<span data-ttu-id="9f860-150">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="9f860-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="9f860-151">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f860-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="9f860-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f860-152">Next steps</span></span>

* [<span data-ttu-id="9f860-153">Aprenda a revisar los registros y a obtener informes sobre la actividad de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="9f860-153">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
