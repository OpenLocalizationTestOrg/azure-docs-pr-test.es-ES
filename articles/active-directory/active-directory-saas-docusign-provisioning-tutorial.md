---
title: "Tutorial: integración de Azure Active Directory con DocuSign | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 3b509ffa934949200277ae431761d2accd4a02d6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="ffcdb-103">Tutorial: Configuración de DocuSign para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="ffcdb-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="ffcdb-104">El objetivo de este tutorial es explicar los pasos que hay que realizar en DocuSign y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD en DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-104">The objective of this tutorial is to show you the steps you need to perform in DocuSign and Azure AD to automatically provision and de-provision user accounts from Azure AD to DocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffcdb-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ffcdb-105">Prerequisites</span></span>

<span data-ttu-id="ffcdb-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="ffcdb-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="ffcdb-108">Una suscripción habilitada para el inicio de sesión único en DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="ffcdb-109">Una cuenta de usuario de DocuSign con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-to-docusign"></a><span data-ttu-id="ffcdb-110">Asignación de usuarios a DocuSign</span><span class="sxs-lookup"><span data-stu-id="ffcdb-110">Assigning users to DocuSign</span></span>

<span data-ttu-id="ffcdb-111">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="ffcdb-112">En el contexto de aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="ffcdb-113">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your DocuSign app.</span></span> <span data-ttu-id="ffcdb-114">Una vez decidido, puede asignar estos usuarios a la aplicación de DocuSign siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-114">Once decided, you can assign these users to your DocuSign app by following the instructions here:</span></span>

[<span data-ttu-id="ffcdb-115">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="ffcdb-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-docusign"></a><span data-ttu-id="ffcdb-116">Sugerencias importantes para asignar usuarios a DocuSign</span><span class="sxs-lookup"><span data-stu-id="ffcdb-116">Important tips for assigning users to DocuSign</span></span>

*   <span data-ttu-id="ffcdb-117">Se recomienda asignar un único usuario de Azure AD a DocuSign para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-117">It is recommended that a single Azure AD user is assigned to DocuSign to test the provisioning configuration.</span></span> <span data-ttu-id="ffcdb-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ffcdb-119">Al asignar a un usuario a DocuSign, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-119">When assigning a user to DocuSign, you must select a valid user role.</span></span> <span data-ttu-id="ffcdb-120">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ffcdb-121">Habilitación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="ffcdb-121">Enable User Provisioning</span></span>

<span data-ttu-id="ffcdb-122">Esta sección lo guía a través de los pasos necesarios para conectar la API de aprovisionamiento de cuentas de usuario de DocuSign, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas en DocuSign en función de la asignación de grupos y usuarios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-122">This section guides you through connecting your Azure AD to DocuSign's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="ffcdb-123">También puede habilitar el inicio de sesión único basado en SAML para DocuSign siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ffcdb-123">You may also choose to enabled SAML-based Single Sign-On for DocuSign, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ffcdb-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="ffcdb-125">Para configurar el aprovisionamiento automático de cuentas de usuario:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-125">To configure user account provisioning:</span></span>

<span data-ttu-id="ffcdb-126">El objetivo de esta sección es describir cómo habilitar el aprovisionamiento de usuarios de Active Directory para DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.</span></span>

1. <span data-ttu-id="ffcdb-127">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="ffcdb-128">Si ya ha configurado DocuSign para el inicio de sesión único, busque la instancia de DocuSign mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using the search field.</span></span> <span data-ttu-id="ffcdb-129">En caso contrario, seleccione **Agregar** y busque **DocuSign** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-129">Otherwise, select **Add** and search for **DocuSign** in the application gallery.</span></span> <span data-ttu-id="ffcdb-130">Seleccione DocuSign en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-130">Select DocuSign from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="ffcdb-131">Seleccione la instancia de DocuSign y luego, la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-131">Select your instance of DocuSign, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="ffcdb-132">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="ffcdb-134">En la sección **Credenciales de administrador**, proporcione los siguientes valores de configuración:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="ffcdb-135">a.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-135">a.</span></span> <span data-ttu-id="ffcdb-136">En el cuadro de texto **Nombre de usuario administrador**, escriba un nombre de cuenta de DocuSign que tenga asignado el perfil **Administrador del sistema** en DocuSign.com.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-136">In the **Admin User Name** textbox, type a DocuSign account name that has the **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="ffcdb-137">b.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-137">b.</span></span> <span data-ttu-id="ffcdb-138">En el cuadro de texto **Contraseña de administrador**, escriba la contraseña de esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-138">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="ffcdb-139">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación de DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your DocuSign app.</span></span>

7. <span data-ttu-id="ffcdb-140">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="ffcdb-141">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-141">Click **Save.**</span></span>

9. <span data-ttu-id="ffcdb-142">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to DocuSign** (Sincronizar usuarios de Azure Active Directory con DocuSign).</span><span class="sxs-lookup"><span data-stu-id="ffcdb-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to DocuSign.**</span></span>

10. <span data-ttu-id="ffcdb-143">En la sección **Attribute Mappings** (Asignaciones de atributos), revise los atributos de usuario que se sincronizan entre Azure AD y DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to DocuSign.</span></span> <span data-ttu-id="ffcdb-144">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de DocuSign con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-144">The attributes selected as **Matching** properties are used to match the user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="ffcdb-145">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="ffcdb-146">Para habilitar el servicio de aprovisionamiento de Azure AD para DocuSign, cambie el **Estado de aprovisionamiento** a **Activado** en la sección Configuración.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-146">To enable the Azure AD provisioning service for DocuSign, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="ffcdb-147">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-147">Click **Save.**</span></span>

<span data-ttu-id="ffcdb-148">Esta acción inicia la sincronización inicial de todos los usuarios y grupos asignados a DocuSign en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-148">It starts the initial synchronization of any users and/or groups assigned to DocuSign in the Users and Groups section.</span></span> <span data-ttu-id="ffcdb-149">La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos, si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="ffcdb-150">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="ffcdb-151">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-151">You can now create a test account.</span></span> <span data-ttu-id="ffcdb-152">Espere 20 minutos para comprobar que la cuenta se ha sincronizado con DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-152">Wait for up to 20 minutes to verify that the account has been synchronized to DocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ffcdb-153">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ffcdb-153">Additional resources</span></span>

* [<span data-ttu-id="ffcdb-154">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="ffcdb-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ffcdb-155">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ffcdb-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ffcdb-156">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ffcdb-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)