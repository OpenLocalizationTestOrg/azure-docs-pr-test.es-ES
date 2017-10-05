---
title: "Tutorial: configuración de LinkedIn Lookup para el aprovisionamiento automático de usuarios con Azure Active Directory | Microsoft Docs"
description: "Aprenda a configurar Azure Active Directory para aprovisionar y cancelar el aprovisionamiento de cuentas de usuario de LinkedIn Lookup automáticamente."
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
ms.openlocfilehash: 085a68cfe8f9e08b8722e8613994ee300a015776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="bae3f-103">Tutorial: configuración de LinkedIn Lookup para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="bae3f-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="bae3f-104">El objetivo de este tutorial es explicar los pasos que debe realizar en LinkedIn Lookup y Azure AD para aprovisionar y cancelar el aprovisionamiento de cuentas de usuario de Azure AD para LinkedIn Lookup automáticamente.</span><span class="sxs-lookup"><span data-stu-id="bae3f-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Lookup and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bae3f-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bae3f-105">Prerequisites</span></span>

<span data-ttu-id="bae3f-106">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bae3f-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="bae3f-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bae3f-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="bae3f-108">Un inquilino de LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="bae3f-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="bae3f-109">Una cuenta de administrador en LinkedIn Lookup con acceso al Centro de cuentas de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="bae3f-109">An administrator account in LinkedIn Lookup with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="bae3f-110">Azure Active Directory se integra con LinkedIn Lookup mediante el protocolo [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="bae3f-110">Azure Active Directory integrates with LinkedIn Lookup using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-lookup"></a><span data-ttu-id="bae3f-111">Asignación de usuarios a LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="bae3f-111">Assigning users to LinkedIn Lookup</span></span>

<span data-ttu-id="bae3f-112">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bae3f-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="bae3f-113">En el contexto de aprovisionamiento de cuentas de usuario automático, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bae3f-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="bae3f-114">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceder a LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="bae3f-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Lookup.</span></span> <span data-ttu-id="bae3f-115">Una vez decidido, puede asignar estos usuarios a LinkedIn Lookup siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="bae3f-115">Once decided, you can assign these users to LinkedIn Lookup by following the instructions here:</span></span>

[<span data-ttu-id="bae3f-116">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="bae3f-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-lookup"></a><span data-ttu-id="bae3f-117">Sugerencias importantes para asignar usuarios a LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="bae3f-117">Important tips for assigning users to LinkedIn Lookup</span></span>

*   <span data-ttu-id="bae3f-118">Se recomienda asignar un solo usuario de Azure AD a LinkedIn Lookup para probar la configuración del aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="bae3f-118">It is recommended that a single Azure AD user be assigned to LinkedIn Lookup to test the provisioning configuration.</span></span> <span data-ttu-id="bae3f-119">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="bae3f-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bae3f-120">Al asignar un usuario a LinkedIn Lookup, debe seleccionar el rol **Usuario** en el cuadro de diálogo de asignación.</span><span class="sxs-lookup"><span data-stu-id="bae3f-120">When assigning a user to LinkedIn Lookup, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="bae3f-121">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="bae3f-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-lookup"></a><span data-ttu-id="bae3f-122">Configuración del aprovisionamiento de usuarios en LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="bae3f-122">Configuring user provisioning to LinkedIn Lookup</span></span>

<span data-ttu-id="bae3f-123">Esta sección le guía a través de los pasos necesarios para conectar la API de aprovisionamiento de su cuenta de usuario de SCIM de LinkedIn Lookup, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de LinkedIn Lookup en función de la asignación de grupos y usuarios en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bae3f-123">This section guides you through connecting your Azure AD to LinkedIn Lookup's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="bae3f-124">También puede decidir habilitar el inicio de sesión único basado en SAML para LinkedIn Lookup siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bae3f-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Lookup, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bae3f-125">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="bae3f-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-lookup-in-azure-ad"></a><span data-ttu-id="bae3f-126">Para configurar el aprovisionamiento de cuentas de usuario automático para LinkedIn Lookup en Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bae3f-126">To configure automatic user account provisioning to LinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="bae3f-127">El primer paso consiste en recuperar el token de acceso de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="bae3f-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="bae3f-128">Si es administrador de organización, puede aprovisionar automáticamente un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="bae3f-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="bae3f-129">En el centro de cuentas, vaya a **Configuración &gt; Configuración global** y abra el panel **SCIM Setup** (Configuración de SCIM).</span><span class="sxs-lookup"><span data-stu-id="bae3f-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="bae3f-130">Si obtiene acceso al centro de cuentas directamente en lugar de a través de un vínculo, puede llegar a este panel mediante los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="bae3f-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="bae3f-131">Inicie sesión en el centro de cuentas.</span><span class="sxs-lookup"><span data-stu-id="bae3f-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="bae3f-132">Seleccione **Administración &gt; Configuración de administración**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="bae3f-133">Haga clic en **Advanced Integrations** (Integraciones avanzadas) en la barra lateral izquierda.</span><span class="sxs-lookup"><span data-stu-id="bae3f-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="bae3f-134">Se le dirigirá al centro de cuentas.</span><span class="sxs-lookup"><span data-stu-id="bae3f-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="bae3f-135">Haga clic en **+ Add new SCIM configuration** (+ Agregar nueva configuración de SCIM) y rellene cada campo del procedimiento.</span><span class="sxs-lookup"><span data-stu-id="bae3f-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="bae3f-136">Si no está habilitada la asignación de licencias automática, solo se sincronizan los datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="bae3f-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Aprovisionamiento de LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="bae3f-138">Si está habilitada la asignación de licencias automática, debe tomar nota de la instancia de la aplicación y del tipo de licencia.</span><span class="sxs-lookup"><span data-stu-id="bae3f-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="bae3f-139">Las licencias se asignan por orden de llegada hasta que se obtienen todas las licencias.</span><span class="sxs-lookup"><span data-stu-id="bae3f-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![Aprovisionamiento de LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="bae3f-141">Haga clic en **Generar token**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-141">Click **Generate token**.</span></span> <span data-ttu-id="bae3f-142">El token de acceso debería aparecer en el campo **Token de acceso**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="bae3f-143">Guarde el token de acceso en el Portapapeles o en el equipo antes de abandonar la página.</span><span class="sxs-lookup"><span data-stu-id="bae3f-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="bae3f-144">Después, inicie sesión en [Azure Portal](https://portal.azure.com) y vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="bae3f-145">Si ya ha configurado LinkedIn Lookup para el inicio de sesión único, busque la instancia de LinkedIn Lookup con el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="bae3f-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using the search field.</span></span> <span data-ttu-id="bae3f-146">En caso contrario, seleccione **Agregar** y busque **LinkedIn Lookup** en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bae3f-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in the application gallery.</span></span> <span data-ttu-id="bae3f-147">Seleccione LinkedIn Lookup en los resultados de búsqueda y agréguelo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bae3f-147">Select LinkedIn Lookup from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="bae3f-148">Seleccione la instancia de LinkedIn Lookup y la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-148">Select your instance of LinkedIn Lookup, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="bae3f-149">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Aprovisionamiento de LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="bae3f-151">Rellene los campos siguientes en **Credenciales de administrador**:</span><span class="sxs-lookup"><span data-stu-id="bae3f-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="bae3f-152">En el campo **URL de inquilino**, escriba https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="bae3f-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="bae3f-153">En el campo **Token secreto**, escriba el token de acceso que ha generado en el paso 1 y haga clic en **Probar conexión**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="bae3f-154">Debería ver una notificación que le indica que el proceso se ha realizado correctamente en el lado superior derecho del portal.</span><span class="sxs-lookup"><span data-stu-id="bae3f-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="bae3f-155">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla que aparece a continuación.</span><span class="sxs-lookup"><span data-stu-id="bae3f-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="bae3f-156">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-156">Click **Save**.</span></span> 

14) <span data-ttu-id="bae3f-157">En la sección **Asignaciones de atributos**, revise los atributos de usuario y de grupo de Azure AD que se sincronizarán con LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="bae3f-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Lookup.</span></span> <span data-ttu-id="bae3f-158">Tenga en cuenta que los atributos seleccionados como propiedades **Matching** se usarán para establecer coincidencias con las cuentas de usuario y los grupos de LinkedIn Lookup para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="bae3f-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="bae3f-159">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="bae3f-159">Select the Save button to commit any changes.</span></span>

![Aprovisionamiento de LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="bae3f-161">Para habilitar el servicio de aprovisionamiento de Azure AD para LinkedIn Lookup, cambie el **Estado de aprovisionamiento** a **Activado** en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-161">To enable the Azure AD provisioning service for LinkedIn Lookup, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="bae3f-162">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bae3f-162">Click **Save**.</span></span> 

<span data-ttu-id="bae3f-163">Esta acción iniciará la sincronización inicial de todos los usuarios y grupos asignados a LinkedIn Lookup en la sección Usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="bae3f-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Lookup in the Users and Groups section.</span></span> <span data-ttu-id="bae3f-164">Tenga en cuenta que la sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="bae3f-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="bae3f-165">Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación de LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="bae3f-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bae3f-166">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bae3f-166">Additional Resources</span></span>

* [<span data-ttu-id="bae3f-167">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="bae3f-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="bae3f-168">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bae3f-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
