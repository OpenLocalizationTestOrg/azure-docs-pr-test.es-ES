---
title: "Tutorial: Integración de Azure Active Directory con Citrix GoToMeeting | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="bef63-103">Tutorial: Configuración de Citrix GoToMeeting para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="bef63-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="bef63-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Citrix GoToMeeting y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bef63-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Citrix GoToMeeting and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooCitrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bef63-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bef63-105">Prerequisites</span></span>

<span data-ttu-id="bef63-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bef63-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="bef63-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bef63-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="bef63-108">Una suscripción habilitada para el inicio de sesión único en Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bef63-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="bef63-109">Una cuenta de usuario de Citrix GoToMeeting con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="bef63-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="bef63-110">Asignar usuarios tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="bef63-110">Assigning users tooCitrix GoToMeeting</span></span>

<span data-ttu-id="bef63-111">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bef63-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="bef63-112">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bef63-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="bef63-113">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a tooyour aplicación Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bef63-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="bef63-114">Una vez decidido, puede asignar estas aplicaciones de Citrix GoToMeeting tooyour de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="bef63-114">Once decided, you can assign these users tooyour Citrix GoToMeeting app by following hello instructions here:</span></span>

[<span data-ttu-id="bef63-115">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="bef63-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="bef63-116">Sugerencias importantes para asignar usuarios tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="bef63-116">Important tips for assigning users tooCitrix GoToMeeting</span></span>

*   <span data-ttu-id="bef63-117">Se recomienda que un único usuario de Azure AD se asigna tooCitrix GoToMeeting tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="bef63-117">It is recommended that a single Azure AD user is assigned tooCitrix GoToMeeting tootest hello provisioning configuration.</span></span> <span data-ttu-id="bef63-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="bef63-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bef63-119">Al asignar un tooCitrix usuario GoToMeeting, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="bef63-119">When assigning a user tooCitrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="bef63-120">rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="bef63-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="bef63-121">Habilitación del aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="bef63-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="bef63-122">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de Azure AD tooCitrix GoToMeeting y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas en Citrix GoToMeeting en función de usuario y de grupo de usuario asignado asignación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bef63-122">This section guides you through connecting your Azure AD tooCitrix GoToMeeting's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="bef63-123">También puede elegir tooenabled basado en SAML Single Sign-On para Citrix GoToMeeting, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bef63-123">You may also choose tooenabled SAML-based Single Sign-On for Citrix GoToMeeting, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bef63-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="bef63-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="bef63-125">tooconfigure aprovisionamiento de cuentas de usuario automática:</span><span class="sxs-lookup"><span data-stu-id="bef63-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="bef63-126">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="bef63-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="bef63-127">Si ya has configurado Citrix GoToMeeting para inicio de sesión único, busque la instancia de Citrix GoToMeeting con el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="bef63-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using hello search field.</span></span> <span data-ttu-id="bef63-128">En caso contrario, seleccione **agregar** y busque **Citrix GoToMeeting** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="bef63-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in hello application gallery.</span></span> <span data-ttu-id="bef63-129">Seleccione Citrix GoToMeeting en resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bef63-129">Select Citrix GoToMeeting from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="bef63-130">Seleccione la instancia de Citrix GoToMeeting, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="bef63-130">Select your instance of Citrix GoToMeeting, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="bef63-131">Conjunto hello **Provisioning** modo demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="bef63-131">Set hello **Provisioning** Mode too**Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="bef63-133">En la sección credenciales de administrador de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bef63-133">Under hello Admin Credentials section, perform hello following steps:</span></span>
   
    <span data-ttu-id="bef63-134">a.</span><span class="sxs-lookup"><span data-stu-id="bef63-134">a.</span></span> <span data-ttu-id="bef63-135">Hola **nombre de usuario de administrador de Citrix GoToMeeting** cuadro de texto, escriba el nombre de usuario de Hola de un administrador.</span><span class="sxs-lookup"><span data-stu-id="bef63-135">In hello **Citrix GoToMeeting Admin User Name** textbox, type hello user name of an administrator.</span></span>

    <span data-ttu-id="bef63-136">b.</span><span class="sxs-lookup"><span data-stu-id="bef63-136">b.</span></span> <span data-ttu-id="bef63-137">Hola **contraseña de administrador de Citrix GoToMeeting** cuadro de texto de contraseña del Administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="bef63-137">In hello **Citrix GoToMeeting Admin Password** textbox, hello administrator's password.</span></span>

6. <span data-ttu-id="bef63-138">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectarse tooyour aplicación Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bef63-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="bef63-139">Si se produce un error en la conexión de hello, asegúrese de que su cuenta de Citrix GoToMeeting tiene permisos de administrador de equipo e inténtelo de hello **"Credenciales de administrador"** vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="bef63-139">If hello connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try hello **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="bef63-140">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.</span><span class="sxs-lookup"><span data-stu-id="bef63-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="bef63-141">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bef63-141">Click **Save.**</span></span>

9. <span data-ttu-id="bef63-142">En la sección asignaciones de hello, seleccione **sincronizar Azure Active Directory Users tooCitrix GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="bef63-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooCitrix GoToMeeting.**</span></span>

10. <span data-ttu-id="bef63-143">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bef63-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooCitrix GoToMeeting.</span></span> <span data-ttu-id="bef63-144">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en Citrix GoToMeeting para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="bef63-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="bef63-145">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="bef63-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="bef63-146">tooenable Hola servicio de aprovisionamiento de Azure AD para Citrix GoToMeeting, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración</span><span class="sxs-lookup"><span data-stu-id="bef63-146">tooenable hello Azure AD provisioning service for Citrix GoToMeeting, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="bef63-147">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bef63-147">Click **Save.**</span></span>

<span data-ttu-id="bef63-148">Inicia la sincronización inicial de Hola de los usuarios o grupos asignados tooCitrix GoToMeeting en la sección usuarios y grupos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bef63-148">It starts hello initial synchronization of any users and/or groups assigned tooCitrix GoToMeeting in hello Users and Groups section.</span></span> <span data-ttu-id="bef63-149">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bef63-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="bef63-150">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bef63-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bef63-151">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bef63-151">Additional resources</span></span>

* [<span data-ttu-id="bef63-152">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="bef63-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bef63-153">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bef63-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bef63-154">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="bef63-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


