---
title: "Tutorial: Integración de Azure Active Directory con Dropbox for Business | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Dropbox para empresas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="1980d-103">Tutorial: Configuración de Dropbox for Business para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="1980d-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="1980d-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Dropbox para negocios y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooDropbox para la empresa.</span><span class="sxs-lookup"><span data-stu-id="1980d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1980d-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1980d-105">Prerequisites</span></span>

<span data-ttu-id="1980d-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1980d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="1980d-107">Un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1980d-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="1980d-108">Una suscripción a Dropbox for Business con inicio de sesión único habilitado.</span><span class="sxs-lookup"><span data-stu-id="1980d-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="1980d-109">Una cuenta de usuario de Dropbox for Business con permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="1980d-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="1980d-110">Asignar usuarios tooDropbox para la empresa</span><span class="sxs-lookup"><span data-stu-id="1980d-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="1980d-111">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1980d-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="1980d-112">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1980d-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="1980d-113">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a tooyour Dropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="1980d-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="1980d-114">Una vez decidido, puede asignar estas tooyour usuarios Dropbox para empresas siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="1980d-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="1980d-115">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="1980d-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="1980d-116">Sugerencias importantes para asignar usuarios tooDropbox para la empresa</span><span class="sxs-lookup"><span data-stu-id="1980d-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="1980d-117">Se recomienda que un único usuario de Azure AD se asigna tooDropbox para hello tootest de negocios aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="1980d-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="1980d-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="1980d-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1980d-119">Al asignar una tooDropbox de usuario para la empresa, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="1980d-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="1980d-120">rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento de...</span><span class="sxs-lookup"><span data-stu-id="1980d-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="1980d-121">Habilitación del aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="1980d-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="1980d-122">Esta sección le guía a través de conectar su tooDropbox de Azure AD para la API de aprovisionamiento de cuentas de usuario de la empresa y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Dropbox para empresas en función de usuario y de grupo asignación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1980d-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="1980d-123">También puede elegir tooenabled basado en SAML Single Sign-On para Dropbox para empresas, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1980d-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1980d-124">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="1980d-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="1980d-125">tooconfigure aprovisionamiento de cuentas de usuario automática:</span><span class="sxs-lookup"><span data-stu-id="1980d-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="1980d-126">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="1980d-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="1980d-127">Si ya has configurado Dropbox para empresas para el inicio de sesión único, busque la instancia de Dropbox para empresas mediante el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="1980d-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="1980d-128">En caso contrario, seleccione **agregar** y busque **Dropbox para empresas** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="1980d-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="1980d-129">Seleccione Dropbox para empresas en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1980d-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="1980d-130">Seleccione la instancia de Dropbox para empresas, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="1980d-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="1980d-131">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="1980d-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="1980d-133">En hello **las credenciales de administrador** sección, haga clic en **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="1980d-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="1980d-134">Se abre un cuadro de diálogo de inicio de sesión de Dropbox for Business en una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="1980d-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="1980d-135">En hello **toolink inicio de sesión tooDropbox con Azure AD** cuadro de diálogo de inicio de sesión tooyour Dropbox para el inquilino de negocios.</span><span class="sxs-lookup"><span data-stu-id="1980d-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="1980d-136">![Aprovisionamiento de usuarios](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Aprovisionamiento de usuarios")</span><span class="sxs-lookup"><span data-stu-id="1980d-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="1980d-137">Confirme que desea toogive Azure Active Directory permiso toomake cambios tooyour Dropbox para el inquilino de negocios.</span><span class="sxs-lookup"><span data-stu-id="1980d-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="1980d-138">Haga clic en **Permitir**.</span><span class="sxs-lookup"><span data-stu-id="1980d-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="1980d-139">![Aprovisionamiento de usuarios](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Aprovisionamiento de usuarios")</span><span class="sxs-lookup"><span data-stu-id="1980d-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="1980d-140">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectarse tooyour Dropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="1980d-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="1980d-141">Si se produce un error en la conexión de hello, asegúrese de la lista desplegable para la cuenta de empresa tiene permisos de administrador de equipo e inténtelo de hello **"Autorizar"** vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="1980d-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="1980d-142">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.</span><span class="sxs-lookup"><span data-stu-id="1980d-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="1980d-143">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1980d-143">Click **Save.**</span></span>

11. <span data-ttu-id="1980d-144">En la sección asignaciones de hello, seleccione **tooDropbox sincronizar Azure usuarios de Active Directory para la empresa.**</span><span class="sxs-lookup"><span data-stu-id="1980d-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="1980d-145">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooDropbox de Azure AD para la empresa.</span><span class="sxs-lookup"><span data-stu-id="1980d-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="1980d-146">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en Dropbox para empresas para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="1980d-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="1980d-147">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="1980d-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="1980d-148">tooenable Hola servicio de aprovisionamiento de Azure AD para Dropbox para empresas, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración</span><span class="sxs-lookup"><span data-stu-id="1980d-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="1980d-149">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1980d-149">Click **Save.**</span></span>

<span data-ttu-id="1980d-150">Inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooDropbox para la empresa en los usuarios de Hola y sección de grupos.</span><span class="sxs-lookup"><span data-stu-id="1980d-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="1980d-151">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1980d-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="1980d-152">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la lista desplegable para aplicaciones de negocio.</span><span class="sxs-lookup"><span data-stu-id="1980d-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="1980d-153">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="1980d-153">You can now create a test account.</span></span> <span data-ttu-id="1980d-154">Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooDropbox para la empresa.</span><span class="sxs-lookup"><span data-stu-id="1980d-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="1980d-155">Un ciclo de aprovisionamiento de usuarios completado correctamente se indica con un estado relacionado:</span><span class="sxs-lookup"><span data-stu-id="1980d-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="1980d-156">![Asignar usuarios](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="1980d-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1980d-157">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1980d-157">Additional resources</span></span>

* [<span data-ttu-id="1980d-158">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="1980d-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1980d-159">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1980d-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1980d-160">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="1980d-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)