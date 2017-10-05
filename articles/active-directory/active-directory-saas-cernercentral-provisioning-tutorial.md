---
title: "Tutorial: Configuración de Cerner Central para el aprovisionamiento automático de usuarios con Azure Active Directory | Microsoft Docs"
description: "Aprenda a configurar Azure Active Directory para aprovisionar usuarios en una lista de Cerner Central automáticamente."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: 84613b7f8d7bd031d492a62da0bc53be96ac45a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="2ded7-103">Tutorial: configuración de Cerner Central para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="2ded7-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="2ded7-104">El objetivo de este tutorial es explicar los pasos que debe realizar en Cerner Central y Azure AD para aprovisionar y cancelar el aprovisionamiento de cuentas de usuario de Azure AD en una lista de Cerner Central automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2ded7-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="2ded7-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2ded7-105">Prerequisites</span></span>

<span data-ttu-id="2ded7-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2ded7-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="2ded7-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ded7-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="2ded7-108">Un inquilino de Cerner Central</span><span class="sxs-lookup"><span data-stu-id="2ded7-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="2ded7-109">Azure Active Directory se integra con Cerner Central mediante el protocolo [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="2ded7-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="2ded7-110">Asignación de usuarios a Cerner Central</span><span class="sxs-lookup"><span data-stu-id="2ded7-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="2ded7-111">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2ded7-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="2ded7-112">En el contexto de aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ded7-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="2ded7-113">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios y/o grupos de Azure AD representan a los usuarios que necesitan acceso a Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="2ded7-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="2ded7-114">Una vez decidido, puede asignar estos usuarios a la aplicación Cerner Central siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="2ded7-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="2ded7-115">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="2ded7-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="2ded7-116">Sugerencias importantes para asignar usuarios a Cerner Central</span><span class="sxs-lookup"><span data-stu-id="2ded7-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="2ded7-117">Se recomienda asignar un solo usuario de Azure AD a Cerner Central para probar la configuración del aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="2ded7-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="2ded7-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="2ded7-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="2ded7-119">Una vez completada la prueba inicial para un solo usuario, Cerner Central recomienda que se aprovisione en la lista de usuarios de Cerner la asignación de toda la lista de usuarios para que tengan acceso a cualquier solución de Cerner (no solo Cerner Central).</span><span class="sxs-lookup"><span data-stu-id="2ded7-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="2ded7-120">Otras soluciones de Cerner aprovechan esta lista de usuarios en la lista de usuarios de Cerner.</span><span class="sxs-lookup"><span data-stu-id="2ded7-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="2ded7-121">Al asignar un usuario a Cerner Central, debe seleccionar el rol **Usuario** en el cuadro de diálogo de asignación.</span><span class="sxs-lookup"><span data-stu-id="2ded7-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="2ded7-122">Los usuarios con el rol de "Acceso predeterminado" quedan excluidos del aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="2ded7-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="2ded7-123">Configuración del aprovisionamiento de usuarios en Cerner Central</span><span class="sxs-lookup"><span data-stu-id="2ded7-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="2ded7-124">Esta sección le guía a través de los pasos necesarios para conectar Azure AD con la lista de usuarios de Cerner Central mediante la API de aprovisionamiento de la cuenta de usuario SCIM de Cerner Central, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas en Cerner Central en función de la asignación de grupos y usuarios en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ded7-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="2ded7-125">También puede decidir habilitar el inicio de sesión único basado en SAML para Cerner Central siguiendo las instrucciones de Azure Portal [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="2ded7-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="2ded7-126">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="2ded7-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="2ded7-127">Para más información, vea el [Tutorial: Integración de Azure Active Directory con Cerner Central](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2ded7-127">For more information, see the [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="2ded7-128">Para configurar el aprovisionamiento de cuentas de usuario automático para Cerner Central en Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2ded7-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="2ded7-129">Para aprovisionar cuentas de usuario en Cerner Central, debe crear una cuenta del sistema de Cerner Central en Cerner y generar un token de portador de OAuth que Azure AD puede usar para conectarse al punto de conexión SCIM de Cerner.</span><span class="sxs-lookup"><span data-stu-id="2ded7-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="2ded7-130">También se recomienda realizar la integración en un entorno de espacio aislado de Cerner antes de su implementación en producción.</span><span class="sxs-lookup"><span data-stu-id="2ded7-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="2ded7-131">El primer paso consiste en asegurarse de que las personas que administran la integración de Cerner y Azure AD tienen una cuenta de CernerCare, obligatoria para acceder a la documentación necesaria para llevar a cabo las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="2ded7-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="2ded7-132">Si es necesario, utilice las direcciones URL siguientes para crear cuentas de CernerCare en los entornos correspondientes.</span><span class="sxs-lookup"><span data-stu-id="2ded7-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="2ded7-133">Espacio aislado: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="2ded7-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="2ded7-134">Producción: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="2ded7-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="2ded7-135">A continuación, se debe crear una cuenta de sistema para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ded7-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="2ded7-136">Siga estas instrucciones para solicitar una cuenta del sistema para los entornos de producción y de espacio aislado.</span><span class="sxs-lookup"><span data-stu-id="2ded7-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="2ded7-137">Instrucciones: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="2ded7-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="2ded7-138">Espacio aislado: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="2ded7-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="2ded7-139">Producción: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="2ded7-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="2ded7-140">A continuación, genere un token de portador de OAuth para cada una de las cuentas del sistema.</span><span class="sxs-lookup"><span data-stu-id="2ded7-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="2ded7-141">Para ello, siga las instrucciones que se describen a continuación.</span><span class="sxs-lookup"><span data-stu-id="2ded7-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="2ded7-142">Instrucciones: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="2ded7-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="2ded7-143">Espacio aislado: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="2ded7-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="2ded7-144">Producción: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="2ded7-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="2ded7-145">Por último, para completar la configuración, tiene que adquirir identificadores de dominio kerberos de lista de usuarios tanto para el espacio aislado como para los entornos de producción en Cerner.</span><span class="sxs-lookup"><span data-stu-id="2ded7-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="2ded7-146">Para información sobre cómo adquirirlo, consulte: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="2ded7-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="2ded7-147">Ahora puede configurar Azure AD para aprovisionar cuentas de usuario para Cerner.</span><span class="sxs-lookup"><span data-stu-id="2ded7-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="2ded7-148">Inicie sesión en [Azure Portal](https://portal.azure.com) y vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ded7-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="2ded7-149">Si ya ha configurado Cerner Central para el inicio de sesión único, busque la instancia de Cerner Central con el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="2ded7-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="2ded7-150">En caso contrario, seleccione **Agregar** y busque **Cerner Central** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2ded7-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="2ded7-151">Seleccione Cerner Central en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2ded7-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="2ded7-152">Seleccione la instancia de Cerner Central y la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="2ded7-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="2ded7-153">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="2ded7-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Aprovisionamiento de Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="2ded7-155">Rellene los campos siguientes en **Credenciales de administrador**:</span><span class="sxs-lookup"><span data-stu-id="2ded7-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="2ded7-156">En el campo **URL de inquilino**, escriba una dirección URL en el formato siguiente y sustituya "User-Roster-Realm-ID" por el identificador de dominio kerberos que obtuvo en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="2ded7-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="2ded7-157">Espacio aislado: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="2ded7-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="2ded7-158">Producción: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="2ded7-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="2ded7-159">En el campo **Token secreto**, escriba el token de portador de OAuth que generó en el paso 3 y haga clic en **Prueba de conexión**.</span><span class="sxs-lookup"><span data-stu-id="2ded7-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="2ded7-160">Debería ver una notificación que le indica que el proceso se ha realizado correctamente en el lado superior derecho del portal.</span><span class="sxs-lookup"><span data-stu-id="2ded7-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="2ded7-161">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla que aparece a continuación.</span><span class="sxs-lookup"><span data-stu-id="2ded7-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="2ded7-162">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2ded7-162">Click **Save**.</span></span> 

12. <span data-ttu-id="2ded7-163">En la sección **Asignaciones de atributos**, revise los atributos de usuario y de grupo que se van a sincronizar desde Azure AD con Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="2ded7-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="2ded7-164">Los atributos seleccionados como propiedades **Matching** se usarán para establecer coincidencias con las cuentas de usuario y los grupos de Cerner Central para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="2ded7-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="2ded7-165">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="2ded7-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="2ded7-166">Para habilitar el servicio de aprovisionamiento de Azure AD para Cerner Central, cambie el **Estado de aprovisionamiento** a **Activado** en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="2ded7-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="2ded7-167">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2ded7-167">Click **Save**.</span></span> 

<span data-ttu-id="2ded7-168">Esta acción inicia la sincronización inicial de todos los usuarios y grupos asignados a Cerner Central en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="2ded7-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="2ded7-169">La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos si el servicio de aprovisionamiento de Azure AD está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="2ded7-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="2ded7-170">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="2ded7-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="2ded7-171">Para más información sobre cómo leer los registros de aprovisionamiento de Azure AD, consulte el tutorial de [Creación de informes sobre el aprovisionamiento automático de cuentas de usuario](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="2ded7-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ded7-172">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2ded7-172">Additional resources</span></span>

* <span data-ttu-id="2ded7-173">[Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD) (Cerner Central: Publicación de datos de identidad mediante Azure AD)</span><span class="sxs-lookup"><span data-stu-id="2ded7-173">[Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)</span></span>
* [<span data-ttu-id="2ded7-174">Tutorial: configuración de Cerner Central para el inicio de sesión único con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ded7-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="2ded7-175">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="2ded7-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="2ded7-176">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ded7-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="2ded7-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2ded7-177">Next steps</span></span>
* <span data-ttu-id="2ded7-178">[Aprenda a revisar los registros y a obtener informes sobre la actividad de aprovisionamiento](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="2ded7-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
