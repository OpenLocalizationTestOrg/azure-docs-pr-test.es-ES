---
title: "Tutorial: Configuración de GitHub para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooGitHub."
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
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="04243-103">Tutorial: Configuración de GitHub para aprovisionar automáticamente usuarios</span><span class="sxs-lookup"><span data-stu-id="04243-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="04243-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en GitHub y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="04243-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in GitHub and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="04243-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="04243-105">Prerequisites</span></span>

<span data-ttu-id="04243-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="04243-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="04243-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04243-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="04243-108">Un inquilino de Github con hello [plan de negocio](https://help.github.com/articles/organization-billing-plans/#business-plan) o mejor habilitado</span><span class="sxs-lookup"><span data-stu-id="04243-108">A Github tenant with hello [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="04243-109">Una cuenta de usuario de GitHub con permisos de administrador</span><span class="sxs-lookup"><span data-stu-id="04243-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="04243-110">Hello Azure AD aprovisionamiento integración se basa en hello [GitHub SCIM API](https://developer.github.com/v3/scim/), que son los equipos de tooGithub disponible en el plan de negocio de Hola o superior.</span><span class="sxs-lookup"><span data-stu-id="04243-110">hello Azure AD provisioning integration relies on hello [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available tooGithub teams on hello Business plan or better.</span></span>

## <a name="assigning-users-toogithub"></a><span data-ttu-id="04243-111">Asignar usuarios tooGitHub</span><span class="sxs-lookup"><span data-stu-id="04243-111">Assigning users tooGitHub</span></span>

<span data-ttu-id="04243-112">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="04243-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="04243-113">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04243-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="04243-114">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan tener acceso a la aplicación de GitHub de tooyour.</span><span class="sxs-lookup"><span data-stu-id="04243-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour GitHub app.</span></span> <span data-ttu-id="04243-115">Una vez decidido, puede asignar estas aplicaciones de GitHub de tooyour de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="04243-115">Once decided, you can assign these users tooyour GitHub app by following hello instructions here:</span></span>

[<span data-ttu-id="04243-116">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="04243-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a><span data-ttu-id="04243-117">Sugerencias importantes para asignar usuarios tooGitHub</span><span class="sxs-lookup"><span data-stu-id="04243-117">Important tips for assigning users tooGitHub</span></span>

*   <span data-ttu-id="04243-118">Se recomienda que un único usuario de Azure AD se asigna tooGitHub tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="04243-118">It is recommended that a single Azure AD user is assigned tooGitHub tootest hello provisioning configuration.</span></span> <span data-ttu-id="04243-119">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="04243-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="04243-120">Al asignar una tooGitHub de usuario, debe seleccionar cualquier hello **usuario** u otra válida específica de la aplicación rol (si está disponible) en el cuadro de diálogo de hello asignación.</span><span class="sxs-lookup"><span data-stu-id="04243-120">When assigning a user tooGitHub, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="04243-121">Hola **acceso predeterminado** rol no funciona para el aprovisionamiento y se omiten estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="04243-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toogithub"></a><span data-ttu-id="04243-122">Configurar tooGitHub de aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="04243-122">Configuring user provisioning tooGitHub</span></span> 

<span data-ttu-id="04243-123">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooGitHub de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en GitHub en función de asignación de usuario y de grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04243-123">This section guides you through connecting your Azure AD tooGitHub's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="04243-124">También puede elegir tooenabled basado en SAML Single Sign-On para GitHub, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="04243-124">You may also choose tooenabled SAML-based Single Sign-On for GitHub, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="04243-125">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="04243-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a><span data-ttu-id="04243-126">Configurar aprovisionamiento tooGitHub en Azure AD de la cuenta de usuario automática</span><span class="sxs-lookup"><span data-stu-id="04243-126">Configure automatic user account provisioning tooGitHub in Azure AD</span></span>


1. <span data-ttu-id="04243-127">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="04243-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="04243-128">Si ya ha configurado GitHub para el inicio de sesión único, busque la instancia de GitHub con el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="04243-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using hello search field.</span></span> <span data-ttu-id="04243-129">En caso contrario, seleccione **agregar** y busque **GitHub** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="04243-129">Otherwise, select **Add** and search for **GitHub** in hello application gallery.</span></span> <span data-ttu-id="04243-130">Seleccione GitHub de resultados de la búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="04243-130">Select GitHub from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="04243-131">Seleccione la instancia de GitHub, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="04243-131">Select your instance of GitHub, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="04243-132">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="04243-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Aprovisionamiento de GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="04243-134">En hello **las credenciales de administrador** sección, haga clic en **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="04243-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="04243-135">Con esta operación se abre un cuadro de diálogo de autorización de GitHub en una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="04243-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="04243-136">En la ventana nueva hello, inicie sesión en GitHub con su cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="04243-136">In hello new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="04243-137">Cuadro de diálogo de autorización resultante hello, seleccione el equipo de GitHub de Hola que desee tooenable aprovisionamiento para y, a continuación, seleccione **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="04243-137">In hello resulting authorization dialog, select hello GitHub team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="04243-138">Hola de Azure toocomplete portal toohello una vez finalizado, vuelva aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="04243-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

    ![Cuadro de diálogo de autorización](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="04243-140">En el portal de Azure hello, entrada **dirección URL del inquilino** y haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de GitHub de tooyour.</span><span class="sxs-lookup"><span data-stu-id="04243-140">In hello Azure portal, input **Tenant URL** and click **Test Connection** tooensure Azure AD can connect tooyour GitHub app.</span></span> <span data-ttu-id="04243-141">Si se produce un error en la conexión de hello, asegúrese de que la cuenta de GitHub tiene permisos de administrador y **dirección URl del inquilino** se especifica correctamente, a continuación, intente Hola "Autorizar" vuelva a intentarlo (pueden constituir **dirección URL del inquilino** regla: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", puede encontrar su organización en su cuenta de GitHub: **configuración** > **organizaciones**).</span><span class="sxs-lookup"><span data-stu-id="04243-141">If hello connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try hello "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Cuadro de diálogo de autorización](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="04243-143">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y la casilla de verificación Hola "envían una notificación por correo electrónico cuando se produce un error."</span><span class="sxs-lookup"><span data-stu-id="04243-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="04243-144">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="04243-144">Click **Save**.</span></span> 

10. <span data-ttu-id="04243-145">En la sección asignaciones de hello, seleccione **tooGitHub sincronizar Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="04243-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGitHub**.</span></span>

11. <span data-ttu-id="04243-146">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooGitHub de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04243-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGitHub.</span></span> <span data-ttu-id="04243-147">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch utilizados en GitHub para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="04243-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in GitHub for update operations.</span></span> <span data-ttu-id="04243-148">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="04243-148">Select hello Save button toocommit any changes.</span></span>

12. <span data-ttu-id="04243-149">tooenable Hola servicio de aprovisionamiento de Azure AD para GitHub, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección</span><span class="sxs-lookup"><span data-stu-id="04243-149">tooenable hello Azure AD provisioning service for GitHub, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13. <span data-ttu-id="04243-150">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="04243-150">Click **Save**.</span></span> 

<span data-ttu-id="04243-151">Esta operación inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooGitHub Hola a los usuarios y la sección de grupos.</span><span class="sxs-lookup"><span data-stu-id="04243-151">This operation starts hello initial synchronization of any users and/or groups assigned tooGitHub in hello Users and Groups section.</span></span> <span data-ttu-id="04243-152">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="04243-152">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="04243-153">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="04243-153">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="04243-154">Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="04243-154">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="04243-155">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="04243-155">Additional resources</span></span>

* [<span data-ttu-id="04243-156">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="04243-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="04243-157">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="04243-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="04243-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04243-158">Next steps</span></span>

* [<span data-ttu-id="04243-159">Obtenga información acerca de cómo se registra tooreview y obtener informes sobre el aprovisionamiento de actividad</span><span class="sxs-lookup"><span data-stu-id="04243-159">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
