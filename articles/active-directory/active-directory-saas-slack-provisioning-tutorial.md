---
title: "Tutorial: Configuración de Slack para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooSlack."
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
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="674dd-103">Tutorial: Configuración de Slack para aprovisionar automáticamente usuarios</span><span class="sxs-lookup"><span data-stu-id="674dd-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="674dd-104">Hola objetivo de este tutorial es tooshow Hola pasos que debe tooperform en Slack y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="674dd-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="674dd-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="674dd-105">Prerequisites</span></span>

<span data-ttu-id="674dd-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="674dd-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="674dd-107">Un inquilino de directorio de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="674dd-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="674dd-108">Una demora de inquilinos con hello [Plus plan](https://aadsyncfabric.slack.com/pricing) o mejor habilitado</span><span class="sxs-lookup"><span data-stu-id="674dd-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="674dd-109">Una cuenta de usuario de Slack con permisos de administrador de equipo</span><span class="sxs-lookup"><span data-stu-id="674dd-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="674dd-110">Nota: Hola aprovisionamiento de integración de Azure AD se basa en hello [Slack SCIM API](https://api.slack.com/scim) que son los equipos de tooSlack disponible en hello además de plan o superior.</span><span class="sxs-lookup"><span data-stu-id="674dd-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="674dd-111">Asignar usuarios tooSlack</span><span class="sxs-lookup"><span data-stu-id="674dd-111">Assigning users tooSlack</span></span>

<span data-ttu-id="674dd-112">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="674dd-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="674dd-113">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizarán sólo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="674dd-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="674dd-114">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesitará toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan acceder a la aplicación de demora de tooyour.</span><span class="sxs-lookup"><span data-stu-id="674dd-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="674dd-115">Una vez decidido, puede asignar estas aplicaciones de demora de tooyour de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="674dd-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="674dd-116">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="674dd-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="674dd-117">Sugerencias importantes para asignar usuarios tooSlack</span><span class="sxs-lookup"><span data-stu-id="674dd-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="674dd-118">Se recomienda que un único usuario de Azure AD asignarse tooSlack tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="674dd-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="674dd-119">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="674dd-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="674dd-120">Al asignar una tooSlack de usuario, debe seleccionar hello **usuario** o el rol de "Grupo" en el cuadro de diálogo de hello asignación.</span><span class="sxs-lookup"><span data-stu-id="674dd-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="674dd-121">rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="674dd-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="674dd-122">Configurar tooSlack de aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="674dd-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="674dd-123">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooSlack de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en demora en función de asignación de usuario y de grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="674dd-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="674dd-124">**Sugerencia:** también puede elegir tooenabled basado en SAML Single Sign-On para Slack, siguiendo instrucciones de hello proporcionadas en (portal de Azure) [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="674dd-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="674dd-125">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="674dd-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="674dd-126">cuenta de usuario automática de tooconfigure tooSlack de aprovisionamiento en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="674dd-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="674dd-127">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="674dd-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="674dd-128">Si ya ha configurado la demora de inicio de sesión único, busque la instancia de demora mediante el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="674dd-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="674dd-129">En caso contrario, seleccione **agregar** y busque **Slack** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="674dd-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="674dd-130">Seleccione demora en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="674dd-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="674dd-131">Seleccione la instancia de demora, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="674dd-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="674dd-132">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="674dd-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Aprovisionamiento de Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="674dd-134">En hello **las credenciales de administrador** sección, haga clic en **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="674dd-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="674dd-135">Se abrirá un cuadro de diálogo de autorización de Slack en una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="674dd-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="674dd-136">En la ventana nueva hello, inicie sesión en Slack con su cuenta de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="674dd-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="674dd-137">cuadro de diálogo de autorización resultante hello, seleccione Hola demora equipo que desea tooenable aprovisionamiento para y, a continuación, seleccione **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="674dd-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="674dd-138">Hola de Azure toocomplete portal toohello una vez finalizado, vuelva aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="674dd-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![Cuadro de diálogo de autorización](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="674dd-140">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de demora de tooyour.</span><span class="sxs-lookup"><span data-stu-id="674dd-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="674dd-141">Si se produce un error en la conexión de hello, asegúrese de que su cuenta de demora tiene permisos de administrador de equipo e intente Hola "Autorizar" vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="674dd-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="674dd-142">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y comprobar Hola casilla incluida a continuación.</span><span class="sxs-lookup"><span data-stu-id="674dd-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="674dd-143">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="674dd-143">Click **Save**.</span></span> 

10) <span data-ttu-id="674dd-144">En la sección asignaciones de hello, seleccione **tooSlack sincronizar Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="674dd-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="674dd-145">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizarán desde tooSlack de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="674dd-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="674dd-146">Tenga en cuenta que Hola atributos seleccionados como **coincidencia** propiedades estarán toomatch usa cuentas de usuario de hello en Slack para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="674dd-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="674dd-147">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="674dd-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="674dd-148">tooenable Hola servicio de aprovisionamiento de Azure AD para Slack, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección</span><span class="sxs-lookup"><span data-stu-id="674dd-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="674dd-149">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="674dd-149">Click **Save**.</span></span> 

<span data-ttu-id="674dd-150">Esto iniciará la sincronización inicial de Hola de todos los usuarios y grupos asignados tooSlack Hola a los usuarios y la sección de grupos.</span><span class="sxs-lookup"><span data-stu-id="674dd-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="674dd-151">Tenga en cuenta que la sincronización inicial de hello surtirá tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 10 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="674dd-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="674dd-152">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de la demora.</span><span class="sxs-lookup"><span data-stu-id="674dd-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="674dd-153">[Opcional] Configuración de aprovisionamiento tooSlack un objeto de grupo</span><span class="sxs-lookup"><span data-stu-id="674dd-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="674dd-154">Si lo desea, puede habilitar Hola de aprovisionamiento de objetos de grupo de tooSlack de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="674dd-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="674dd-155">Esto es diferente de "asignación de grupos de usuarios", en ese objeto de grupo real de hello además tooits miembros se replicarán desde tooSlack de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="674dd-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="674dd-156">Por ejemplo, si tiene un grupo denominado "Mi grupo" en Azure AD, se creará un grupo idéntico denominado "Mi grupo" en Slack.</span><span class="sxs-lookup"><span data-stu-id="674dd-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="674dd-157">tooenable el aprovisionamiento de objetos de grupo:</span><span class="sxs-lookup"><span data-stu-id="674dd-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="674dd-158">En la sección asignaciones de hello, seleccione **tooSlack sincronizar Azure grupos de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="674dd-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="674dd-159">En la hoja de la asignación de atributos de hello, establezca tooYes habilitado.</span><span class="sxs-lookup"><span data-stu-id="674dd-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="674dd-160">Hola **asignaciones de atributos** sección, revise los atributos de grupo de Hola que se sincronizarán desde tooSlack de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="674dd-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="674dd-161">Tenga en cuenta que Hola atributos seleccionados como **coincidencia** propiedades estarán toomatch usa grupos de hello en Slack para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="674dd-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="674dd-162">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="674dd-162">Click **Save**.</span></span>

<span data-ttu-id="674dd-163">Este resultado en cualquier tooSlack de objetos asignados del grupo en hello **usuarios y grupos** sección completa que se sincronizan desde tooSlack de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="674dd-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="674dd-164">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de la demora.</span><span class="sxs-lookup"><span data-stu-id="674dd-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="674dd-165">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="674dd-165">Additional Resources</span></span>

* [<span data-ttu-id="674dd-166">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="674dd-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="674dd-167">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="674dd-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
