---
title: "Tutorial: Configuración de Slack para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información sobre cómo configurar Azure Active Directory para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Slack."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: 3cb49a4abb26c34a938c963c4cf326b5ccd490de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="a1918-103">Tutorial: Configuración de Slack para aprovisionar automáticamente usuarios</span><span class="sxs-lookup"><span data-stu-id="a1918-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="a1918-104">El objetivo de este tutorial es explicar los pasos que debe realizar en Slack y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD para Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a1918-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a1918-105">Prerequisites</span></span>

<span data-ttu-id="a1918-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1918-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a1918-107">Un inquilino de directorio de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1918-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="a1918-108">Un inquilino de Slack con el [plan Plus](https://aadsyncfabric.slack.com/pricing) o uno superior habilitado</span><span class="sxs-lookup"><span data-stu-id="a1918-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="a1918-109">Una cuenta de usuario de Slack con permisos de administrador de equipo</span><span class="sxs-lookup"><span data-stu-id="a1918-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="a1918-110">Nota: La integración del aprovisionamiento de Azure AD se basa en la [API de Slack SCIM](https://api.slack.com/scim), que está disponible para los equipos de Slack con el plan Plus o uno superior.</span><span class="sxs-lookup"><span data-stu-id="a1918-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="a1918-111">Asignación de usuarios a Slack</span><span class="sxs-lookup"><span data-stu-id="a1918-111">Assigning users to Slack</span></span>

<span data-ttu-id="a1918-112">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a1918-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a1918-113">En el contexto de aprovisionamiento de cuentas de usuario automático, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1918-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="a1918-114">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceder a la aplicación de Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="a1918-115">Una vez decidido, puede asignar estos usuarios a la aplicación de Slack siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="a1918-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="a1918-116">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="a1918-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="a1918-117">Sugerencias importantes para asignar usuarios a Slack</span><span class="sxs-lookup"><span data-stu-id="a1918-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="a1918-118">Se recomienda asignar un solo usuario de Azure AD a Slack para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="a1918-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="a1918-119">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="a1918-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a1918-120">Al asignar un usuario a Slack, debe seleccionar los roles **Usuario** o Grupo en el cuadro de diálogo de asignación.</span><span class="sxs-lookup"><span data-stu-id="a1918-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="a1918-121">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="a1918-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="a1918-122">Configuración del aprovisionamiento de usuarios en Slack</span><span class="sxs-lookup"><span data-stu-id="a1918-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="a1918-123">Esta sección lo guía a través de los pasos necesarios para conectar la API de aprovisionamiento de su cuenta de usuario de Slack, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de Slack en función de la asignación de grupos y usuarios Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1918-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="a1918-124">**Sugerencia**: También puede decidir habilitar el inicio de sesión único basado en SAML para Slack siguiendo las instrucciones de (Azure Portal)[https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="a1918-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="a1918-125">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="a1918-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="a1918-126">Para configurar el aprovisionamiento de cuentas de usuario automático para Slack en Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a1918-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="a1918-127">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a1918-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="a1918-128">Si ya ha configurado Slack para el inicio de sesión único, busque la instancia de Slack mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="a1918-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="a1918-129">En caso contrario, seleccione **Agregar** y busque **Slack** en la Galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a1918-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="a1918-130">Seleccione Slack en los resultados de búsqueda y agrégalo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a1918-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="a1918-131">Seleccione la instancia de Slack y, después, seleccione la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="a1918-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="a1918-132">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="a1918-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Aprovisionamiento de Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="a1918-134">En **Credenciales de administrador**, haga clic en **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="a1918-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="a1918-135">Se abrirá un cuadro de diálogo de autorización de Slack en una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="a1918-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="a1918-136">En esa nueva ventana, inicie sesión en Slack con su cuenta de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="a1918-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="a1918-137">En el cuadro de diálogo de autorización que aparece, seleccione el equipo de Slack para el que desea habilitar el aprovisionamiento y, luego, seleccione **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="a1918-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="a1918-138">Cuando termina, vuelva a Azure Portal para completar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="a1918-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![Cuadro de diálogo de autorización](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="a1918-140">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación de Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="a1918-141">Si se produce un error de conexión, asegúrese de que su cuenta de Slack tiene permisos de administrador de equipo y vuelva a intentar el paso de "Autorizar".</span><span class="sxs-lookup"><span data-stu-id="a1918-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="a1918-142">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla que aparece a continuación.</span><span class="sxs-lookup"><span data-stu-id="a1918-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="a1918-143">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a1918-143">Click **Save**.</span></span> 

10) <span data-ttu-id="a1918-144">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to** (Sincronizar usuarios de Azure Active Directory con Slack).</span><span class="sxs-lookup"><span data-stu-id="a1918-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="a1918-145">En la sección **Asignaciones de atributos**, revise los atributos de usuario que se sincronizarán de Azure AD a Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="a1918-146">Tenga en cuenta que los atributos seleccionados como propiedades de **Coincidencia** se usarán para establecer coincidencias con las cuentas de usuario de Slack con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="a1918-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="a1918-147">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="a1918-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="a1918-148">Para habilitar el aprovisionamiento del servicio de aprovisionamiento de Azure AD para Slack, cambie el **estado de aprovisionamiento** a **Activado** en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="a1918-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="a1918-149">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a1918-149">Click **Save**.</span></span> 

<span data-ttu-id="a1918-150">Esta acción iniciará la sincronización inicial de todos los usuarios y grupos asignados a Slack en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="a1918-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="a1918-151">Tenga en cuenta que la sincronización inicial tardará más tiempo en realizarse que las posteriores, que se duran aproximadamente cada 10 minutos si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="a1918-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="a1918-152">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="a1918-153">[Opcional] Configuración del aprovisionamiento de objetos de grupo para Slack</span><span class="sxs-lookup"><span data-stu-id="a1918-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="a1918-154">Si lo desea, puede habilitar el aprovisionamiento de objetos de grupo de Azure AD para Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="a1918-155">No es lo mismo que la asignación de grupos de usuarios, en que el objeto de grupo real, además de sus miembros, se replicará desde Azure AD a Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="a1918-156">Por ejemplo, si tiene un grupo denominado "Mi grupo" en Azure AD, se creará un grupo idéntico denominado "Mi grupo" en Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="a1918-157">Para habilitar el aprovisionamiento de objetos de grupo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a1918-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="a1918-158">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Groups to** (Sincronizar grupos de Azure Active Directory con Slack).</span><span class="sxs-lookup"><span data-stu-id="a1918-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="a1918-159">En la hoja Asignación de atributos, establezca Habilitado en Sí.</span><span class="sxs-lookup"><span data-stu-id="a1918-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="a1918-160">En la sección **Asignaciones de atributos**, revise los atributos de grupo que se sincronizarán de Azure AD a Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="a1918-161">Tenga en cuenta que los atributos seleccionados como propiedades de **Coincidencia** se usarán para establecer coincidencias con los grupos de Slack con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="a1918-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="a1918-162">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a1918-162">Click **Save**.</span></span>

<span data-ttu-id="a1918-163">Como resultado, todos los objetos de grupo asignados a Slack en la sección **Usuarios y grupos** se sincronizarán por completo de Azure AD a Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="a1918-164">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de Slack.</span><span class="sxs-lookup"><span data-stu-id="a1918-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a1918-165">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a1918-165">Additional Resources</span></span>

* [<span data-ttu-id="a1918-166">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="a1918-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="a1918-167">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1918-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
