---
title: "Tutorial: Configuración de Samanage para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooSamanage."
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="fbf43-103">Tutorial: Configuración de Samanage para aprovisionar a los usuarios automáticamente</span><span class="sxs-lookup"><span data-stu-id="fbf43-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="fbf43-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Samanage y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="fbf43-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Samanage and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSamanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fbf43-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fbf43-105">Prerequisites</span></span>

<span data-ttu-id="fbf43-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fbf43-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="fbf43-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbf43-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="fbf43-108">Un inquilino de Samanage con hello [plan profesional](https://www.samanage.com/pricing/) o mejor habilitado</span><span class="sxs-lookup"><span data-stu-id="fbf43-108">A Samanage tenant with hello [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="fbf43-109">Una cuenta de usuario de Samanage con permisos de administrador</span><span class="sxs-lookup"><span data-stu-id="fbf43-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="fbf43-110">Hello Azure AD aprovisionamiento integración se basa en hello [API de REST de Samanage](https://www.samanage.com/api/), que son los equipos de tooSamanage disponible en hello Professional planear o uno superior.</span><span class="sxs-lookup"><span data-stu-id="fbf43-110">hello Azure AD provisioning integration relies on hello [Samanage REST API](https://www.samanage.com/api/), which is available tooSamanage teams on hello Professional plan or better.</span></span>

## <a name="assigning-users-toosamanage"></a><span data-ttu-id="fbf43-111">Asignar usuarios tooSamanage</span><span class="sxs-lookup"><span data-stu-id="fbf43-111">Assigning users tooSamanage</span></span>

<span data-ttu-id="fbf43-112">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fbf43-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="fbf43-113">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbf43-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="fbf43-114">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan tener acceso a la aplicación de Samanage tooyour.</span><span class="sxs-lookup"><span data-stu-id="fbf43-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Samanage app.</span></span> <span data-ttu-id="fbf43-115">Una vez decidido, puede asignar estas aplicaciones de Samanage tooyour de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="fbf43-115">Once decided, you can assign these users tooyour Samanage app by following hello instructions here:</span></span>

[<span data-ttu-id="fbf43-116">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="fbf43-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a><span data-ttu-id="fbf43-117">Sugerencias importantes para asignar usuarios tooSamanage</span><span class="sxs-lookup"><span data-stu-id="fbf43-117">Important tips for assigning users tooSamanage</span></span>

*   <span data-ttu-id="fbf43-118">Se recomienda que un único usuario de Azure AD se asigna tooSamanage tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="fbf43-118">It is recommended that a single Azure AD user is assigned tooSamanage tootest hello provisioning configuration.</span></span> <span data-ttu-id="fbf43-119">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="fbf43-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fbf43-120">Al asignar una tooSamanage de usuario, debe seleccionar cualquier hello **usuario** u otra válida específica de la aplicación rol (si está disponible) en el cuadro de diálogo de hello asignación.</span><span class="sxs-lookup"><span data-stu-id="fbf43-120">When assigning a user tooSamanage, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="fbf43-121">Hola **acceso predeterminado** rol no funciona para el aprovisionamiento y se omiten estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="fbf43-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="fbf43-122">Como una característica agregada, Hola aprovisionamiento del servicio lee los roles personalizados definidos en Samanage y las importa en Azure AD donde se pueden seleccionar en el cuadro de diálogo de hello Seleccionar rol.</span><span class="sxs-lookup"><span data-stu-id="fbf43-122">As an added feature, hello provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="fbf43-123">Estos roles se verán en hello portal de Azure después de hello aprovisionamiento del servicio está habilitado y ha completado un ciclo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="fbf43-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toosamanage"></a><span data-ttu-id="fbf43-124">Configurar tooSamanage de aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="fbf43-124">Configuring user provisioning tooSamanage</span></span> 

<span data-ttu-id="fbf43-125">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooSamanage de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Samanage en función de asignación de usuario y de grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbf43-125">This section guides you through connecting your Azure AD tooSamanage's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="fbf43-126">También puede elegir tooenabled basado en SAML Single Sign-On para Samanage, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fbf43-126">You may also choose tooenabled SAML-based Single Sign-On for Samanage, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fbf43-127">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="fbf43-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a><span data-ttu-id="fbf43-128">Configurar aprovisionamiento tooSamanage en Azure AD de la cuenta de usuario automática:</span><span class="sxs-lookup"><span data-stu-id="fbf43-128">Configure automatic user account provisioning tooSamanage in Azure AD:</span></span>


1. <span data-ttu-id="fbf43-129">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="fbf43-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="fbf43-130">Si ya ha configurado Samanage para el inicio de sesión único, busque la instancia de Samanage con el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbf43-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using hello search field.</span></span> <span data-ttu-id="fbf43-131">En caso contrario, seleccione **agregar** y busque **Samanage** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbf43-131">Otherwise, select **Add** and search for **Samanage** in hello application gallery.</span></span> <span data-ttu-id="fbf43-132">Seleccione Samanage en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fbf43-132">Select Samanage from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="fbf43-133">Seleccione la instancia de Samanage, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="fbf43-133">Select your instance of Samanage, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="fbf43-134">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="fbf43-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Aprovisionamiento de Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="fbf43-136">En hello **las credenciales de administrador** entrada hello, en una sección **administrador Username & contraseña de administrador** de cuenta de su Samanage.</span><span class="sxs-lookup"><span data-stu-id="fbf43-136">Under hello **Admin Credentials** section, input hello **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="fbf43-137">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de Samanage de tooyour.</span><span class="sxs-lookup"><span data-stu-id="fbf43-137">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Samanage app.</span></span> <span data-ttu-id="fbf43-138">Si se produce un error en la conexión de hello, asegúrese de que su cuenta de Samanage tiene permisos de administrador e inténtelo de nuevo el paso 5.</span><span class="sxs-lookup"><span data-stu-id="fbf43-138">If hello connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="fbf43-139">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y la casilla de verificación Hola "envían una notificación por correo electrónico cuando se produce un error."</span><span class="sxs-lookup"><span data-stu-id="fbf43-139">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="fbf43-140">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fbf43-140">Click **Save**.</span></span> 

9. <span data-ttu-id="fbf43-141">En la sección asignaciones de hello, seleccione **tooSamanage sincronizar Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="fbf43-141">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSamanage**.</span></span>

10. <span data-ttu-id="fbf43-142">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooSamanage de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbf43-142">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSamanage.</span></span> <span data-ttu-id="fbf43-143">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch utilizados en Samanage para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="fbf43-143">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Samanage for update operations.</span></span> <span data-ttu-id="fbf43-144">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="fbf43-144">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="fbf43-145">tooenable Hola servicio de aprovisionamiento de Azure AD para Samanage, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección</span><span class="sxs-lookup"><span data-stu-id="fbf43-145">tooenable hello Azure AD provisioning service for Samanage, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="fbf43-146">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fbf43-146">Click **Save**.</span></span> 

<span data-ttu-id="fbf43-147">Esta operación inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooSamanage Hola a los usuarios y la sección de grupos.</span><span class="sxs-lookup"><span data-stu-id="fbf43-147">This operation starts hello initial synchronization of any users and/or groups assigned tooSamanage in hello Users and Groups section.</span></span> <span data-ttu-id="fbf43-148">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbf43-148">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="fbf43-149">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="fbf43-149">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="fbf43-150">Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="fbf43-150">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fbf43-151">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fbf43-151">Additional resources</span></span>

* [<span data-ttu-id="fbf43-152">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="fbf43-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="fbf43-153">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fbf43-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="fbf43-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fbf43-154">Next steps</span></span>

* [<span data-ttu-id="fbf43-155">Obtenga información acerca de cómo se registra tooreview y obtener informes sobre el aprovisionamiento de actividad</span><span class="sxs-lookup"><span data-stu-id="fbf43-155">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
