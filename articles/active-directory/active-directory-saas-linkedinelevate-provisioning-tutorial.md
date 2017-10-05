---
title: "Tutorial: Configuración de LinkedIn Elevate para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información sobre cómo configurar Azure Active Directory para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de LinkedIn Elevate."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 526666301aad1e5284c621024649d9cd52c92d18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-elevate-for-automatic-user-provisioning"></a><span data-ttu-id="4e11c-103">Tutorial: Configuración de LinkedIn Elevate para aprovisionar automáticamente usuarios</span><span class="sxs-lookup"><span data-stu-id="4e11c-103">Tutorial: Configuring LinkedIn Elevate for Automatic User Provisioning</span></span>


<span data-ttu-id="4e11c-104">El objetivo de este tutorial es explicar los pasos que debe realizar en LinkedIn Elevate y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD para LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="4e11c-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Elevate and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Elevate.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4e11c-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4e11c-105">Prerequisites</span></span>

<span data-ttu-id="4e11c-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4e11c-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="4e11c-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e11c-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="4e11c-108">Un inquilino de LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="4e11c-108">A LinkedIn Elevate tenant</span></span> 
*   <span data-ttu-id="4e11c-109">Una cuenta de administrador en LinkedIn Elevate con acceso al Centro de cuentas de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="4e11c-109">An administrator account in LinkedIn Elevate with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="4e11c-110">Azure Active Directory se integra con LinkedIn Elevate mediante el protocolo [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="4e11c-110">Azure Active Directory integrates with LinkedIn Elevate using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-elevate"></a><span data-ttu-id="4e11c-111">Asignar usuarios a LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="4e11c-111">Assigning users to LinkedIn Elevate</span></span>

<span data-ttu-id="4e11c-112">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4e11c-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4e11c-113">En el contexto de aprovisionamiento de cuentas de usuario automático, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e11c-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="4e11c-114">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan obtener acceso a LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="4e11c-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Elevate.</span></span> <span data-ttu-id="4e11c-115">Una vez decidido, puede asignar estos usuarios a LinkedIn Elevate siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="4e11c-115">Once decided, you can assign these users to LinkedIn Elevate by following the instructions here:</span></span>

[<span data-ttu-id="4e11c-116">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="4e11c-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-elevate"></a><span data-ttu-id="4e11c-117">Sugerencias importantes para asignar usuarios a LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="4e11c-117">Important tips for assigning users to LinkedIn Elevate</span></span>

*   <span data-ttu-id="4e11c-118">Se recomienda asignar un solo usuario de Azure AD a LinkedIn Elevate para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="4e11c-118">It is recommended that a single Azure AD user be assigned to LinkedIn Elevate to test the provisioning configuration.</span></span> <span data-ttu-id="4e11c-119">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="4e11c-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4e11c-120">Al asignar un usuario a LinkedIn Elevate, debe seleccionar el rol **Usuario** en el cuadro de diálogo de asignación.</span><span class="sxs-lookup"><span data-stu-id="4e11c-120">When assigning a user to LinkedIn Elevate, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="4e11c-121">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="4e11c-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-elevate"></a><span data-ttu-id="4e11c-122">Configuración del aprovisionamiento de usuarios en LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="4e11c-122">Configuring user provisioning to LinkedIn Elevate</span></span>

<span data-ttu-id="4e11c-123">Esta sección lo guía a través de los pasos necesarios para conectar la API de aprovisionamiento de su cuenta de usuario de SCIM de LinkedIn Elevate, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de LinkedIn Elevate en función de la asignación de grupos y usuarios en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e11c-123">This section guides you through connecting your Azure AD to LinkedIn Elevate's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Elevate based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="4e11c-124">**Sugerencia**: También puede decidir habilitar el inicio de sesión único basado en SAML para LinkedIn Elevate siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e11c-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for LinkedIn Elevate, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e11c-125">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="4e11c-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-elevate-in-azure-ad"></a><span data-ttu-id="4e11c-126">Para configurar el aprovisionamiento de cuentas de usuario automático para LinkedIn Elevate en Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4e11c-126">To configure automatic user account provisioning to LinkedIn Elevate in Azure AD:</span></span>


<span data-ttu-id="4e11c-127">El primer paso consiste en recuperar el token de acceso de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="4e11c-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="4e11c-128">Si es administrador de organización, puede aprovisionar automáticamente un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="4e11c-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="4e11c-129">En el centro de cuentas, vaya a **Configuración &gt; Configuración global** y abra el panel **SCIM Setup** (Configuración de SCIM).</span><span class="sxs-lookup"><span data-stu-id="4e11c-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="4e11c-130">Si obtiene acceso al centro de cuentas directamente en lugar de a través de un vínculo, puede llegar a este panel mediante los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="4e11c-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="4e11c-131">Inicie sesión en el centro de cuentas.</span><span class="sxs-lookup"><span data-stu-id="4e11c-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="4e11c-132">Seleccione **Administración &gt; Configuración de administración**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="4e11c-133">Haga clic en **Advanced Integrations** (Integraciones avanzadas) en la barra lateral izquierda.</span><span class="sxs-lookup"><span data-stu-id="4e11c-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="4e11c-134">Se le dirigirá al centro de cuentas.</span><span class="sxs-lookup"><span data-stu-id="4e11c-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="4e11c-135">Haga clic en **+ Add new SCIM configuration** (+ Agregar nueva configuración de SCIM) y rellene cada campo del procedimiento.</span><span class="sxs-lookup"><span data-stu-id="4e11c-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="4e11c-136">Si no está habilitada la asignación de licencias automática, solo se sincronizan los datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="4e11c-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Aprovisionamiento de LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate1.PNG)

> <span data-ttu-id="4e11c-138">Si está habilitada la asignación de licencias automática, debe tomar nota de la instancia de la aplicación y del tipo de licencia.</span><span class="sxs-lookup"><span data-stu-id="4e11c-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="4e11c-139">Las licencias se asignan por orden de llegada hasta que se obtienen todas las licencias.</span><span class="sxs-lookup"><span data-stu-id="4e11c-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![Aprovisionamiento de LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate2.PNG)

5)  <span data-ttu-id="4e11c-141">Haga clic en **Generar token**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-141">Click **Generate token**.</span></span> <span data-ttu-id="4e11c-142">El token de acceso debería aparecer en el campo **Token de acceso**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="4e11c-143">Guarde el token de acceso en el Portapapeles o en el equipo antes de abandonar la página.</span><span class="sxs-lookup"><span data-stu-id="4e11c-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="4e11c-144">Después, inicie sesión en [Azure Portal](https://portal.azure.com) y vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="4e11c-145">Si ya ha configurado LinkedIn Elevate para el inicio de sesión único, busque la instancia de LinkedIn Elevate mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4e11c-145">If you have already configured LinkedIn Elevate for single sign-on, search for your instance of LinkedIn Elevate using the search field.</span></span> <span data-ttu-id="4e11c-146">En caso contrario, seleccione **Agregar** y busque **LinkedIn Elevate** en la Galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4e11c-146">Otherwise, select **Add** and search for **LinkedIn Elevate** in the application gallery.</span></span> <span data-ttu-id="4e11c-147">Seleccione LinkedIn Elevate en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4e11c-147">Select LinkedIn Elevate from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="4e11c-148">Seleccione la instancia de LinkedIn Elevate y, después, seleccione la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-148">Select your instance of LinkedIn Elevate, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="4e11c-149">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Aprovisionamiento de LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate3.PNG)

11)  <span data-ttu-id="4e11c-151">Rellene los campos siguientes en **Credenciales de administrador**:</span><span class="sxs-lookup"><span data-stu-id="4e11c-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="4e11c-152">En el campo **URL de inquilino**, escriba https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="4e11c-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="4e11c-153">En el campo **Token secreto**, escriba el token de acceso que ha generado en el paso 1 y haga clic en **Probar conexión**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="4e11c-154">Debería ver una notificación que le indica que el proceso se ha realizado correctamente en el lado superior derecho del portal.</span><span class="sxs-lookup"><span data-stu-id="4e11c-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="4e11c-155">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla que aparece a continuación.</span><span class="sxs-lookup"><span data-stu-id="4e11c-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="4e11c-156">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-156">Click **Save**.</span></span> 

14) <span data-ttu-id="4e11c-157">En la sección **Asignaciones de atributos**, revise los atributos de usuario y de grupo que se sincronizarán de Azure AD a LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="4e11c-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Elevate.</span></span> <span data-ttu-id="4e11c-158">Tenga en cuenta que los atributos seleccionados como propiedades de **Coincidencia** se usarán para establecer coincidencias con las cuentas de usuario y grupos de LinkedIn Elevate con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="4e11c-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Elevate for update operations.</span></span> <span data-ttu-id="4e11c-159">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="4e11c-159">Select the Save button to commit any changes.</span></span>

![Aprovisionamiento de LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate4.PNG)

15) <span data-ttu-id="4e11c-161">Para habilitar el servicio de aprovisionamiento de Azure AD para LinkedIn Elevate, cambie el **Estado de aprovisionamiento** a **Activado** en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-161">To enable the Azure AD provisioning service for LinkedIn Elevate, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="4e11c-162">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-162">Click **Save**.</span></span> 

<span data-ttu-id="4e11c-163">Esta acción iniciará la sincronización inicial de todos los usuarios y grupos asignados a LinkedIn Elevate en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="4e11c-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Elevate in the Users and Groups section.</span></span> <span data-ttu-id="4e11c-164">Tenga en cuenta que la sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="4e11c-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="4e11c-165">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="4e11c-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Elevate app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4e11c-166">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4e11c-166">Additional Resources</span></span>

* [<span data-ttu-id="4e11c-167">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="4e11c-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="4e11c-168">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4e11c-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
