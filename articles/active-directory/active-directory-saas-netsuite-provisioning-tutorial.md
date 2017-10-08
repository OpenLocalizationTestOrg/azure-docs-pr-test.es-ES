---
title: "Tutorial: Integración de Azure Active Directory con NetSuite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="9c28f-103">Tutorial: Configuración de Netsuite para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="9c28f-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="9c28f-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Netsuite y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="9c28f-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Netsuite and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooNetsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c28f-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9c28f-105">Prerequisites</span></span>

<span data-ttu-id="9c28f-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9c28f-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="9c28f-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c28f-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="9c28f-108">Una suscripción habilitada para el inicio de sesión único en Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9c28f-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="9c28f-109">Una cuenta de usuario de Netsuite con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="9c28f-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-toonetsuite"></a><span data-ttu-id="9c28f-110">Asignar usuarios tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="9c28f-110">Assigning users tooNetsuite</span></span>

<span data-ttu-id="9c28f-111">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9c28f-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="9c28f-112">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizan sólo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c28f-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="9c28f-113">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan tener acceso a la aplicación de Netsuite tooyour.</span><span class="sxs-lookup"><span data-stu-id="9c28f-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Netsuite app.</span></span> <span data-ttu-id="9c28f-114">Una vez decidido, puede asignar estas aplicaciones de Netsuite tooyour de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="9c28f-114">Once decided, you can assign these users tooyour Netsuite app by following hello instructions here:</span></span>

[<span data-ttu-id="9c28f-115">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="9c28f-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a><span data-ttu-id="9c28f-116">Sugerencias importantes para asignar usuarios tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="9c28f-116">Important tips for assigning users tooNetsuite</span></span>

*   <span data-ttu-id="9c28f-117">Se recomienda que un único usuario de Azure AD se asigna tooNetsuite tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="9c28f-117">It is recommended that a single Azure AD user is assigned tooNetsuite tootest hello provisioning configuration.</span></span> <span data-ttu-id="9c28f-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="9c28f-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9c28f-119">Al asignar una tooNetsuite de usuario, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="9c28f-119">When assigning a user tooNetsuite, you must select a valid user role.</span></span> <span data-ttu-id="9c28f-120">rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="9c28f-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="9c28f-121">Habilitación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="9c28f-121">Enable User Provisioning</span></span>

<span data-ttu-id="9c28f-122">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooNetsuite de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Netsuite en función de asignación de usuario y de grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c28f-122">This section guides you through connecting your Azure AD tooNetsuite's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="9c28f-123">También puede elegir tooenabled basado en SAML Single Sign-On para Netsuite, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c28f-123">You may also choose tooenabled SAML-based Single Sign-On for Netsuite, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9c28f-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="9c28f-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="9c28f-125">tooconfigure aprovisionamiento de cuentas de usuario:</span><span class="sxs-lookup"><span data-stu-id="9c28f-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="9c28f-126">objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuarios de usuario de Active Directory cuentas tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="9c28f-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooNetsuite.</span></span>

1. <span data-ttu-id="9c28f-127">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="9c28f-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="9c28f-128">Si ya ha configurado Netsuite para el inicio de sesión único, busque la instancia de Netsuite con el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c28f-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using hello search field.</span></span> <span data-ttu-id="9c28f-129">En caso contrario, seleccione **agregar** y busque **Netsuite** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c28f-129">Otherwise, select **Add** and search for **Netsuite** in hello application gallery.</span></span> <span data-ttu-id="9c28f-130">Seleccione Netsuite en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9c28f-130">Select Netsuite from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="9c28f-131">Seleccione la instancia de Netsuite, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="9c28f-131">Select your instance of Netsuite, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="9c28f-132">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="9c28f-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="9c28f-134">En hello **las credenciales de administrador** sección, proporcione Hola siguientes opciones de configuración:</span><span class="sxs-lookup"><span data-stu-id="9c28f-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="9c28f-135">a.</span><span class="sxs-lookup"><span data-stu-id="9c28f-135">a.</span></span> <span data-ttu-id="9c28f-136">Hola **nombre de usuario administrador** cuadro de texto, tipo de un Netsuite nombre de cuenta que ha Hola **administrador del sistema** perfil en Netsuite.com asignado.</span><span class="sxs-lookup"><span data-stu-id="9c28f-136">In hello **Admin User Name** textbox, type a Netsuite account name that has hello **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="9c28f-137">b.</span><span class="sxs-lookup"><span data-stu-id="9c28f-137">b.</span></span> <span data-ttu-id="9c28f-138">Hola **contraseña de administrador** cuadro de texto, escriba la contraseña de Hola para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="9c28f-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>
      
6. <span data-ttu-id="9c28f-139">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de Netsuite de tooyour.</span><span class="sxs-lookup"><span data-stu-id="9c28f-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Netsuite app.</span></span>

7. <span data-ttu-id="9c28f-140">Hola **correo electrónico de notificación** , escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir notificaciones de error de aprovisionamiento y active casilla Hola.</span><span class="sxs-lookup"><span data-stu-id="9c28f-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="9c28f-141">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9c28f-141">Click **Save.**</span></span>

9. <span data-ttu-id="9c28f-142">En la sección asignaciones de hello, seleccione **tooNetsuite sincronizar Azure usuarios de Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="9c28f-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooNetsuite.**</span></span>

10. <span data-ttu-id="9c28f-143">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooNetsuite de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c28f-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooNetsuite.</span></span> <span data-ttu-id="9c28f-144">Tenga en cuenta que Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del Hola toomatch utilizados en Netsuite para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="9c28f-144">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="9c28f-145">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="9c28f-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="9c28f-146">tooenable Hola servicio de aprovisionamiento de Azure AD para Netsuite, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración</span><span class="sxs-lookup"><span data-stu-id="9c28f-146">tooenable hello Azure AD provisioning service for Netsuite, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="9c28f-147">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9c28f-147">Click **Save.**</span></span>

<span data-ttu-id="9c28f-148">Inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooNetsuite Hola a los usuarios y la sección de grupos.</span><span class="sxs-lookup"><span data-stu-id="9c28f-148">It starts hello initial synchronization of any users and/or groups assigned tooNetsuite in hello Users and Groups section.</span></span> <span data-ttu-id="9c28f-149">Tenga en cuenta que la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c28f-149">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="9c28f-150">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9c28f-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="9c28f-151">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="9c28f-151">You can now create a test account.</span></span> <span data-ttu-id="9c28f-152">Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="9c28f-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooNetsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9c28f-153">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9c28f-153">Additional resources</span></span>

* [<span data-ttu-id="9c28f-154">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="9c28f-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9c28f-155">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9c28f-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9c28f-156">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="9c28f-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)