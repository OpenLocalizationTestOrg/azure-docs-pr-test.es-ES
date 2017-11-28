---
title: "Tutorial: integración de Azure Active Directory con Concur | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="247f0-103">Tutorial: Configuración de Concur para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="247f0-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="247f0-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Concur y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooConcur.</span><span class="sxs-lookup"><span data-stu-id="247f0-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="247f0-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="247f0-105">Prerequisites</span></span>

<span data-ttu-id="247f0-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="247f0-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="247f0-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="247f0-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="247f0-108">Una suscripción habilitada para el inicio de sesión único en Concur.</span><span class="sxs-lookup"><span data-stu-id="247f0-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="247f0-109">Una cuenta de usuario de Concur con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="247f0-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="247f0-110">Asignar usuarios tooConcur</span><span class="sxs-lookup"><span data-stu-id="247f0-110">Assigning users tooConcur</span></span>

<span data-ttu-id="247f0-111">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="247f0-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="247f0-112">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="247f0-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="247f0-113">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan acceder a la aplicación de Concur de tooyour.</span><span class="sxs-lookup"><span data-stu-id="247f0-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="247f0-114">Una vez decidido, puede asignar estas aplicaciones de Concur de tooyour de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="247f0-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="247f0-115">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="247f0-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="247f0-116">Sugerencias importantes para asignar usuarios tooConcur</span><span class="sxs-lookup"><span data-stu-id="247f0-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="247f0-117">Se recomienda que un único usuario de Azure AD asignarse tooConcur tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="247f0-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="247f0-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="247f0-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="247f0-119">Al asignar una tooConcur de usuario, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="247f0-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="247f0-120">rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="247f0-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="247f0-121">Habilitación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="247f0-121">Enable user provisioning</span></span>

<span data-ttu-id="247f0-122">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooConcur de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Concur en función de asignación de usuario y de grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="247f0-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="247f0-123">También puede elegir tooenabled basado en SAML Single Sign-On para Concur, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="247f0-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="247f0-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="247f0-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="247f0-125">tooconfigure aprovisionamiento de cuentas de usuario:</span><span class="sxs-lookup"><span data-stu-id="247f0-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="247f0-126">objetivo de Hola de esta sección es toooutline cómo tooenable aprovisionamiento de usuario de Active Directory de cuentas de tooConcur.</span><span class="sxs-lookup"><span data-stu-id="247f0-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="247f0-127">aplicaciones de tooenable en Hola servicio de gastos, tiene la configuración correcta de toobe y el uso de un perfil de administrador de servicios Web.</span><span class="sxs-lookup"><span data-stu-id="247f0-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="247f0-128">No agregue Hola administrador WS rol tooyour perfil de administrador existente que usa para las funciones administrativas de T & E.</span><span class="sxs-lookup"><span data-stu-id="247f0-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="247f0-129">Asesores de concur o administrador de clientes de hello debe crear un perfil de administrador de servicios Web distintos y Administrador de clientes de hello debe utilizar este perfil para las funciones de administrador de servicios Web de hello (por ejemplo, al habilitar aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="247f0-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="247f0-130">Estos perfiles deben estar separados de diaria T & Usar perfil de administrador del administrador del cliente de hello (Hola T & perfil de administrador E no deben tener asignado el rol de hello WSAdmin).</span><span class="sxs-lookup"><span data-stu-id="247f0-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="247f0-131">Cuando creas Hola perfil toobe utilizado para habilitar la aplicación hello, escriba nombre del administrador del cliente de hello en campos de perfil de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="247f0-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="247f0-132">Esto asigna perfil toohello de propiedad.</span><span class="sxs-lookup"><span data-stu-id="247f0-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="247f0-133">Una vez que se crea uno o varios perfiles, cliente hello debe iniciar sesión con esta hello tooclick de perfil "*habilitar*" botón para una aplicación asociada en el menú de servicios Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="247f0-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="247f0-134">Para hello después de motivos, esta acción no debería realizarse con perfil de Hola que utiliza para la administración de T & E normal.</span><span class="sxs-lookup"><span data-stu-id="247f0-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="247f0-135">Hello cliente tiene toobe Hola que hace clic en "*Sí*" en la ventana de cuadro de diálogo de Hola que aparece después de habilita una aplicación.</span><span class="sxs-lookup"><span data-stu-id="247f0-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="247f0-136">Haga clic en confirma cliente Hola considera para tooaccess de aplicación de socio comercial de hello sus datos, por lo que usted u Hola asociado no puede hacer clic que el botón Sí.</span><span class="sxs-lookup"><span data-stu-id="247f0-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="247f0-137">Si un administrador de cliente que ha habilitado una aplicación con hello T & perfil de administrador E deja empresa hello (lo que se desactiva el perfil de hello), las aplicaciones habilitadas con ese perfil no funcionará hasta que se habilite la aplicación hello con otro administrador WS activo perfil.</span><span class="sxs-lookup"><span data-stu-id="247f0-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="247f0-138">Este es el motivo por el que se supone toocreate distintos perfiles de administrador de WS.</span><span class="sxs-lookup"><span data-stu-id="247f0-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="247f0-139">Si un administrador deja la empresa de hello, nombre de hello asociado toohello perfil de administrador WS puede ser administrador de reemplazo de toohello modificadas si lo desea, sin afectar a Hola habilitado, aplicación porque no es necesario que ese perfil no activado.</span><span class="sxs-lookup"><span data-stu-id="247f0-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="247f0-140">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="247f0-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="247f0-141">Inicie sesión en tooyour **Concur** inquilino.</span><span class="sxs-lookup"><span data-stu-id="247f0-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="247f0-142">De hello **administración** menú, seleccione **servicios Web**.</span><span class="sxs-lookup"><span data-stu-id="247f0-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="247f0-143">![Inquilino de Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Inquilino de Concur")</span><span class="sxs-lookup"><span data-stu-id="247f0-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="247f0-144">En hello lado izquierdo, de hello **servicios Web** panel, seleccione **habilitar aplicación de socio**.</span><span class="sxs-lookup"><span data-stu-id="247f0-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="247f0-145">![Habilitar aplicación de asociado](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Habilitar aplicación de asociado")</span><span class="sxs-lookup"><span data-stu-id="247f0-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="247f0-146">De hello **habilitar aplicación** lista, seleccione **Azure Active Directory**y, a continuación, haga clic en **habilitar**.</span><span class="sxs-lookup"><span data-stu-id="247f0-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="247f0-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="247f0-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="247f0-148">Haga clic en **Sí** tooclose hello **Confirmar acción** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="247f0-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="247f0-149">![Confirmar acción](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirmar acción")</span><span class="sxs-lookup"><span data-stu-id="247f0-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="247f0-150">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="247f0-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="247f0-151">Si ya ha configurado Concur para el inicio de sesión único, busque la instancia de Concur con el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="247f0-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="247f0-152">En caso contrario, seleccione **agregar** y busque **Concur** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="247f0-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="247f0-153">Seleccione Concur en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="247f0-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="247f0-154">Seleccione la instancia de Concur, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="247f0-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="247f0-155">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="247f0-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![Aprovisionamiento](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="247f0-157">En hello **las credenciales de administrador** sección, escriba Hola **nombre de usuario** hello y **contraseña** de su administrador de Concur.</span><span class="sxs-lookup"><span data-stu-id="247f0-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="247f0-158">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de Concur de tooyour.</span><span class="sxs-lookup"><span data-stu-id="247f0-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="247f0-159">Si se produce un error en la conexión de hello, asegúrese de que la cuenta de Concur tiene permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="247f0-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="247f0-160">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.</span><span class="sxs-lookup"><span data-stu-id="247f0-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="247f0-161">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="247f0-161">Click **Save.**</span></span>

14. <span data-ttu-id="247f0-162">En la sección asignaciones de hello, seleccione **tooConcur sincronizar Azure usuarios de Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="247f0-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="247f0-163">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooConcur de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="247f0-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="247f0-164">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch utilizados en Concur para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="247f0-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="247f0-165">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="247f0-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="247f0-166">tooenable Hola servicio de aprovisionamiento de Azure AD para Concur, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección</span><span class="sxs-lookup"><span data-stu-id="247f0-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="247f0-167">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="247f0-167">Click **Save.**</span></span>

<span data-ttu-id="247f0-168">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="247f0-168">You can now create a test account.</span></span> <span data-ttu-id="247f0-169">Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooConcur.</span><span class="sxs-lookup"><span data-stu-id="247f0-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="247f0-170">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="247f0-170">Additional resources</span></span>

* [<span data-ttu-id="247f0-171">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="247f0-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="247f0-172">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="247f0-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="247f0-173">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="247f0-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

