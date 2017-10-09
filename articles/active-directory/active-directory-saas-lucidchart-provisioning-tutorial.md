---
title: "Tutorial: Configuración de LucidChart para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooLucidChart."
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
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="b6c28-103">Tutorial: Configuración de LucidChart para aprovisionar a los usuarios automáticamente</span><span class="sxs-lookup"><span data-stu-id="b6c28-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="b6c28-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en LucidChart y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="b6c28-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b6c28-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b6c28-105">Prerequisites</span></span>

<span data-ttu-id="b6c28-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b6c28-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="b6c28-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6c28-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="b6c28-108">Un inquilino de LucidChart con hello [plan empresarial](https://www.lucidchart.com/user/117598685#/subscriptionLevel) o mejor habilitado</span><span class="sxs-lookup"><span data-stu-id="b6c28-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="b6c28-109">Una cuenta de usuario de LucidChart con permisos de administrador</span><span class="sxs-lookup"><span data-stu-id="b6c28-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="b6c28-110">Asignar usuarios tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="b6c28-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="b6c28-111">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b6c28-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="b6c28-112">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6c28-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="b6c28-113">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan tener acceso a la aplicación de LucidChart tooyour.</span><span class="sxs-lookup"><span data-stu-id="b6c28-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="b6c28-114">Una vez decidido, puede asignar estas aplicaciones de LucidChart tooyour de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="b6c28-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="b6c28-115">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="b6c28-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="b6c28-116">Sugerencias importantes para asignar usuarios tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="b6c28-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="b6c28-117">Se recomienda que un único usuario de Azure AD se asigna tooLucidChart tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="b6c28-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="b6c28-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="b6c28-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b6c28-119">Al asignar una tooLucidChart de usuario, debe seleccionar cualquier hello **usuario** u otra válida específica de la aplicación rol (si está disponible) en el cuadro de diálogo de hello asignación.</span><span class="sxs-lookup"><span data-stu-id="b6c28-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="b6c28-120">Hola **acceso predeterminado** rol no funciona para el aprovisionamiento y se omiten estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="b6c28-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="b6c28-121">Configurar tooLucidChart de aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="b6c28-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="b6c28-122">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooLucidChart de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en LucidChart en función de asignación de usuario y de grupo en Azure AD .</span><span class="sxs-lookup"><span data-stu-id="b6c28-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="b6c28-123">También puede elegir tooenabled basado en SAML Single Sign-On para LucidChart, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6c28-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b6c28-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="b6c28-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="b6c28-125">Configurar aprovisionamiento tooLucidChart en Azure AD de la cuenta de usuario automática</span><span class="sxs-lookup"><span data-stu-id="b6c28-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="b6c28-126">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="b6c28-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="b6c28-127">Si ya ha configurado LucidChart para el inicio de sesión único, busque la instancia de LucidChart con el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6c28-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="b6c28-128">En caso contrario, seleccione **agregar** y busque **LucidChart** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6c28-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="b6c28-129">Seleccione LucidChart en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b6c28-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="b6c28-130">Seleccione la instancia de LucidChart, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="b6c28-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="b6c28-131">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="b6c28-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Aprovisionamiento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="b6c28-133">En hello **credenciales de administrador** entrada hello, en una sección **secreto del Token** generados por cuenta de su LucidChart (puede encontrar el token de hello en su cuenta: **equipo**  >  **Integración de aplicaciones** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="b6c28-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Aprovisionamiento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="b6c28-135">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de LucidChart de tooyour.</span><span class="sxs-lookup"><span data-stu-id="b6c28-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="b6c28-136">Si se produce un error en la conexión de hello, asegúrese de que su cuenta de LucidChart tiene permisos de administrador e inténtelo de nuevo el paso 5.</span><span class="sxs-lookup"><span data-stu-id="b6c28-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="b6c28-137">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y la casilla de verificación Hola "envían una notificación por correo electrónico cuando se produce un error."</span><span class="sxs-lookup"><span data-stu-id="b6c28-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="b6c28-138">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b6c28-138">Click **Save**.</span></span> 

9. <span data-ttu-id="b6c28-139">En la sección asignaciones de hello, seleccione **tooLucidChart sincronizar Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="b6c28-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="b6c28-140">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooLucidChart de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6c28-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="b6c28-141">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del Hola toomatch utilizados en LucidChart para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="b6c28-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="b6c28-142">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="b6c28-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="b6c28-143">tooenable Hola servicio de aprovisionamiento de Azure AD para LucidChart, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección</span><span class="sxs-lookup"><span data-stu-id="b6c28-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="b6c28-144">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b6c28-144">Click **Save**.</span></span> 

<span data-ttu-id="b6c28-145">Esta operación inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooLucidChart Hola a los usuarios y la sección de grupos.</span><span class="sxs-lookup"><span data-stu-id="b6c28-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="b6c28-146">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6c28-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="b6c28-147">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="b6c28-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="b6c28-148">Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="b6c28-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b6c28-149">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b6c28-149">Additional resources</span></span>

* [<span data-ttu-id="b6c28-150">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="b6c28-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="b6c28-151">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b6c28-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="b6c28-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6c28-152">Next steps</span></span>

* [<span data-ttu-id="b6c28-153">Obtenga información acerca de cómo se registra tooreview y obtener informes sobre el aprovisionamiento de actividad</span><span class="sxs-lookup"><span data-stu-id="b6c28-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
