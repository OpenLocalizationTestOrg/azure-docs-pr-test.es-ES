---
title: "Tutorial: Integración de Azure Active Directory con Jive | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Active Directory de Azure y Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="9d195-103">Tutorial: Configuración de Jive para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="9d195-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="9d195-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Jive y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooJive.</span><span class="sxs-lookup"><span data-stu-id="9d195-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Jive and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooJive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d195-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d195-105">Prerequisites</span></span>

<span data-ttu-id="9d195-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9d195-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="9d195-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d195-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="9d195-108">Una suscripción habilitada para inicio de sesión único en Jive.</span><span class="sxs-lookup"><span data-stu-id="9d195-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="9d195-109">Una cuenta de usuario de Jive con permisos de Team Admin (administrador de equipo).</span><span class="sxs-lookup"><span data-stu-id="9d195-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-toojive"></a><span data-ttu-id="9d195-110">Asignar usuarios tooJive</span><span class="sxs-lookup"><span data-stu-id="9d195-110">Assigning users tooJive</span></span>

<span data-ttu-id="9d195-111">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d195-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="9d195-112">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d195-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="9d195-113">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a la aplicación de Jive tooyour.</span><span class="sxs-lookup"><span data-stu-id="9d195-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Jive app.</span></span> <span data-ttu-id="9d195-114">Una vez decidido, puede asignar estas aplicaciones de Jive tooyour de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="9d195-114">Once decided, you can assign these users tooyour Jive app by following hello instructions here:</span></span>

[<span data-ttu-id="9d195-115">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="9d195-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a><span data-ttu-id="9d195-116">Sugerencias importantes para asignar usuarios tooJive</span><span class="sxs-lookup"><span data-stu-id="9d195-116">Important tips for assigning users tooJive</span></span>

*   <span data-ttu-id="9d195-117">Se recomienda que un único usuario de Azure AD asignarse tooJive tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="9d195-117">It is recommended that a single Azure AD user be assigned tooJive tootest hello provisioning configuration.</span></span> <span data-ttu-id="9d195-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="9d195-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9d195-119">Al asignar una tooJive de usuario, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="9d195-119">When assigning a user tooJive, you must select a valid user role.</span></span> <span data-ttu-id="9d195-120">rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="9d195-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="9d195-121">Habilitación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="9d195-121">Enable User Provisioning</span></span>

<span data-ttu-id="9d195-122">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooJive de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Jive en función de asignación de usuario y de grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d195-122">This section guides you through connecting your Azure AD tooJive's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="9d195-123">También puede elegir tooenabled basado en SAML Single Sign-On para Jive, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d195-123">You may also choose tooenabled SAML-based Single Sign-On for Jive, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9d195-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="9d195-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="9d195-125">tooconfigure aprovisionamiento de cuentas de usuario:</span><span class="sxs-lookup"><span data-stu-id="9d195-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="9d195-126">objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuarios de usuario de Active Directory cuentas tooJive.</span><span class="sxs-lookup"><span data-stu-id="9d195-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooJive.</span></span>
<span data-ttu-id="9d195-127">Como parte de este procedimiento, se le tooprovide requiere un token de seguridad de usuario que deberá toorequest jive.com.</span><span class="sxs-lookup"><span data-stu-id="9d195-127">As part of this procedure, you are required tooprovide a user security token you need toorequest from Jive.com.</span></span>

1. <span data-ttu-id="9d195-128">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="9d195-128">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="9d195-129">Si ya ha configurado Jive para el inicio de sesión único, busque la instancia de Jive mediante el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d195-129">If you have already configured Jive for single sign-on, search for your instance of Jive using hello search field.</span></span> <span data-ttu-id="9d195-130">En caso contrario, seleccione **agregar** y busque **Jive** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d195-130">Otherwise, select **Add** and search for **Jive** in hello application gallery.</span></span> <span data-ttu-id="9d195-131">Seleccione Jive de resultados de la búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d195-131">Select Jive from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="9d195-132">Seleccione la instancia de Jive, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="9d195-132">Select your instance of Jive, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="9d195-133">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="9d195-133">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="9d195-135">En hello **las credenciales de administrador** sección, proporcione Hola siguientes opciones de configuración:</span><span class="sxs-lookup"><span data-stu-id="9d195-135">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="9d195-136">a.</span><span class="sxs-lookup"><span data-stu-id="9d195-136">a.</span></span> <span data-ttu-id="9d195-137">Hola **nombre de usuario de administrador de Jive** cuadro de texto, tipo de un Jive nombre de cuenta que ha Hola **administrador del sistema** perfil en Jive.com asignado.</span><span class="sxs-lookup"><span data-stu-id="9d195-137">In hello **Jive Admin User Name** textbox, type a Jive account name that has hello **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="9d195-138">b.</span><span class="sxs-lookup"><span data-stu-id="9d195-138">b.</span></span> <span data-ttu-id="9d195-139">Hola **contraseña de administrador de Jive** cuadro de texto, escriba la contraseña de Hola para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="9d195-139">In hello **Jive Admin Password** textbox, type hello password for this account.</span></span>
   
    <span data-ttu-id="9d195-140">c.</span><span class="sxs-lookup"><span data-stu-id="9d195-140">c.</span></span> <span data-ttu-id="9d195-141">Hola **URL del inquilino de Jive** cuadro de texto URL de inquilino de Jive de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="9d195-141">In hello **Jive Tenant URL** textbox, type hello Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="9d195-142">URL del inquilino de Jive Hello es la dirección URL que se usa por su toolog de organización en tooJive.</span><span class="sxs-lookup"><span data-stu-id="9d195-142">hello Jive tenant URL is URL that is used by your organization toolog in tooJive.</span></span>  
      > <span data-ttu-id="9d195-143">Normalmente, la dirección URL de hello tiene Hola siguiendo el formato: **www.\< organización\>. jive.com**.</span><span class="sxs-lookup"><span data-stu-id="9d195-143">Typically, hello URL has hello following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="9d195-144">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de Jive de tooyour.</span><span class="sxs-lookup"><span data-stu-id="9d195-144">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Jive app.</span></span>

7. <span data-ttu-id="9d195-145">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y comprobar Hola casilla incluida a continuación.</span><span class="sxs-lookup"><span data-stu-id="9d195-145">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

8. <span data-ttu-id="9d195-146">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9d195-146">Click **Save.**</span></span>

9. <span data-ttu-id="9d195-147">En la sección asignaciones de hello, seleccione **tooJive sincronizar Azure usuarios de Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="9d195-147">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooJive.**</span></span>

10. <span data-ttu-id="9d195-148">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooJive de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d195-148">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooJive.</span></span> <span data-ttu-id="9d195-149">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del Hola toomatch utilizados en Jive para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="9d195-149">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Jive for update operations.</span></span> <span data-ttu-id="9d195-150">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="9d195-150">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="9d195-151">tooenable Hola servicio de aprovisionamiento de Azure AD para Jive, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración</span><span class="sxs-lookup"><span data-stu-id="9d195-151">tooenable hello Azure AD provisioning service for Jive, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="9d195-152">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9d195-152">Click **Save.**</span></span>

<span data-ttu-id="9d195-153">Inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooJive Hola a los usuarios y la sección de grupos.</span><span class="sxs-lookup"><span data-stu-id="9d195-153">It starts hello initial synchronization of any users and/or groups assigned tooJive in hello Users and Groups section.</span></span> <span data-ttu-id="9d195-154">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d195-154">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="9d195-155">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de Jive.</span><span class="sxs-lookup"><span data-stu-id="9d195-155">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Jive app.</span></span>

<span data-ttu-id="9d195-156">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="9d195-156">You can now create a test account.</span></span> <span data-ttu-id="9d195-157">Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooJive.</span><span class="sxs-lookup"><span data-stu-id="9d195-157">Wait for up too20 minutes tooverify that hello account has been synchronized tooJive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d195-158">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9d195-158">Additional resources</span></span>

* [<span data-ttu-id="9d195-159">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="9d195-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d195-160">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d195-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9d195-161">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="9d195-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)