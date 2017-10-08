---
title: "Tutorial: Configuración de LinkedIn Sales Navigator para el aprovisionamiento automático de usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooLinkedIn navegador de ventas."
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
ms.openlocfilehash: 322c5271535994c13a9fafadbf74f356cdfe865d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-sales-navigator-for-automatic-user-provisioning"></a><span data-ttu-id="94d04-103">Tutorial: Configuración de LinkedIn Sales Navigator para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="94d04-103">Tutorial: Configuring LinkedIn Sales Navigator for Automatic User Provisioning</span></span>


<span data-ttu-id="94d04-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en LinkedIn ventas navegador y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooLinkedIn navegador de ventas.</span><span class="sxs-lookup"><span data-stu-id="94d04-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Sales Navigator and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Sales Navigator.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="94d04-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="94d04-105">Prerequisites</span></span>

<span data-ttu-id="94d04-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="94d04-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="94d04-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94d04-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="94d04-108">Un inquilino de LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="94d04-108">A LinkedIn Sales Navigator tenant</span></span> 
*   <span data-ttu-id="94d04-109">Una cuenta de administrador en el navegador de ventas de LinkedIn con acceso toohello centro de cuentas de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="94d04-109">An administrator account in LinkedIn Sales Navigator with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="94d04-110">Azure Active Directory se integra con el navegador de ventas de LinkedIn con hello [SCIM](http://www.simplecloud.info/) protocolo.</span><span class="sxs-lookup"><span data-stu-id="94d04-110">Azure Active Directory integrates with LinkedIn Sales Navigator using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-sales-navigator"></a><span data-ttu-id="94d04-111">Asignar usuarios tooLinkedIn navegador de ventas</span><span class="sxs-lookup"><span data-stu-id="94d04-111">Assigning users tooLinkedIn Sales Navigator</span></span>

<span data-ttu-id="94d04-112">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="94d04-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="94d04-113">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizarán sólo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94d04-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="94d04-114">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesitará toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a tooLinkedIn navegador de ventas.</span><span class="sxs-lookup"><span data-stu-id="94d04-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Sales Navigator.</span></span> <span data-ttu-id="94d04-115">Una vez decidido, puede asignar estas tooLinkedIn navegador de ventas de los usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="94d04-115">Once decided, you can assign these users tooLinkedIn Sales Navigator by following hello instructions here:</span></span>

[<span data-ttu-id="94d04-116">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="94d04-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-sales-navigator"></a><span data-ttu-id="94d04-117">Sugerencias importantes para asignar usuarios tooLinkedIn navegador de ventas</span><span class="sxs-lookup"><span data-stu-id="94d04-117">Important tips for assigning users tooLinkedIn Sales Navigator</span></span>

*   <span data-ttu-id="94d04-118">Se recomienda que un único usuario de Azure AD asignarse hello tootest tooLinkedIn navegador de ventas que configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="94d04-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Sales Navigator tootest hello provisioning configuration.</span></span> <span data-ttu-id="94d04-119">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="94d04-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="94d04-120">Al asignar un navegador de ventas tooLinkedIn de usuario, debe seleccionar hello **usuario** rol en el cuadro de diálogo de hello asignación.</span><span class="sxs-lookup"><span data-stu-id="94d04-120">When assigning a user tooLinkedIn Sales Navigator, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="94d04-121">rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="94d04-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-sales-navigator"></a><span data-ttu-id="94d04-122">Configurar tooLinkedIn navegador de ventas de aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="94d04-122">Configuring user provisioning tooLinkedIn Sales Navigator</span></span>

<span data-ttu-id="94d04-123">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario del su Azure AD tooLinkedIn ventas de navegación SCIM y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en el navegador de ventas de LinkedIn en función de usuario y la asignación de grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94d04-123">This section guides you through connecting your Azure AD tooLinkedIn Sales Navigator's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Sales Navigator based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="94d04-124">También puede elegir tooenabled basado en SAML Single Sign-On de navegador de ventas de LinkedIn, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="94d04-124">You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Sales Navigator, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="94d04-125">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="94d04-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-sales-navigator-in-azure-ad"></a><span data-ttu-id="94d04-126">cuenta de usuario automática de tooconfigure tooLinkedIn navegador de ventas de aprovisionamiento en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="94d04-126">tooconfigure automatic user account provisioning tooLinkedIn Sales Navigator in Azure AD:</span></span>


<span data-ttu-id="94d04-127">primer paso de Hello es tooretrieve el token de acceso de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="94d04-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="94d04-128">Si es administrador de organización, puede aprovisionar automáticamente un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="94d04-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="94d04-129">En el centro de cuentas, vaya demasiado**configuración &gt; configuración Global** hello abierto y **el programa de instalación de SCIM** panel.</span><span class="sxs-lookup"><span data-stu-id="94d04-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="94d04-130">Si se obtiene acceso a centro de cuentas de hello directamente en lugar de a través de un vínculo, puede llegar a él mediante Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="94d04-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="94d04-131">Inicie sesión en el centro de tooAccount.</span><span class="sxs-lookup"><span data-stu-id="94d04-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="94d04-132">Seleccione **Administración &gt; Configuración de administración**.</span><span class="sxs-lookup"><span data-stu-id="94d04-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="94d04-133">Haga clic en **avanzada integraciones** en barra lateral izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d04-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="94d04-134">Está dirigido toohello centro de cuentas.</span><span class="sxs-lookup"><span data-stu-id="94d04-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="94d04-135">Haga clic en **+ agregar una nueva configuración de SCIM** y siga el procedimiento de hello rellenando en cada campo.</span><span class="sxs-lookup"><span data-stu-id="94d04-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="94d04-136">Si no está habilitada la asignación de licencias automática, solo se sincronizan los datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="94d04-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Aprovisionamiento de LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="94d04-138">Cuando se habilita la asignación de autolicense, necesita toonote la instancia de aplicación y tipo de licencia.</span><span class="sxs-lookup"><span data-stu-id="94d04-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="94d04-139">Se asignan licencias primero en llegar, primero actúan base hasta que se realizan todas las licencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d04-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![Aprovisionamiento de LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="94d04-141">Haga clic en **Generar token**.</span><span class="sxs-lookup"><span data-stu-id="94d04-141">Click **Generate token**.</span></span> <span data-ttu-id="94d04-142">Debería ver la pantalla de token de acceso en hello **token de acceso** campo.</span><span class="sxs-lookup"><span data-stu-id="94d04-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="94d04-143">Guarde el Portapapeles de tooyour de token de acceso o el equipo antes de abandonar la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d04-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="94d04-144">A continuación, inicie sesión en toohello [portal de Azure](https://portal.azure.com)y examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="94d04-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="94d04-145">Si ya has configurado LinkedIn navegador de ventas para el inicio de sesión único, busque la instancia de navegador de ventas de LinkedIn con el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d04-145">If you have already configured LinkedIn Sales Navigator for single sign-on, search for your instance of LinkedIn Sales Navigator using hello search field.</span></span> <span data-ttu-id="94d04-146">En caso contrario, seleccione **agregar** y busque **LinkedIn ventas navegador** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d04-146">Otherwise, select **Add** and search for **LinkedIn Sales Navigator** in hello application gallery.</span></span> <span data-ttu-id="94d04-147">Seleccione LinkedIn ventas navegador de resultados de la búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="94d04-147">Select LinkedIn Sales Navigator from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="94d04-148">Seleccione la instancia de navegador de ventas de LinkedIn, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="94d04-148">Select your instance of LinkedIn Sales Navigator, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="94d04-149">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="94d04-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Aprovisionamiento de LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="94d04-151">Rellene Hola después de campos en **las credenciales de administrador** :</span><span class="sxs-lookup"><span data-stu-id="94d04-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="94d04-152">Hola **dirección URL del inquilino** , escriba https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="94d04-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="94d04-153">Hola **secreto Token** campo, escriba el token de acceso de Hola que generó en el paso 1 y haga clic en **Probar conexión** .</span><span class="sxs-lookup"><span data-stu-id="94d04-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="94d04-154">Verá una notificación de éxito en el lado superior derecho de hello del portal.</span><span class="sxs-lookup"><span data-stu-id="94d04-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="94d04-155">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y comprobar Hola casilla incluida a continuación.</span><span class="sxs-lookup"><span data-stu-id="94d04-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="94d04-156">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="94d04-156">Click **Save**.</span></span> 

14) <span data-ttu-id="94d04-157">Hola **asignaciones de atributos** sección, revise los atributos de usuario y grupo de Hola que se sincronizarán desde Azure AD tooLinkedIn navegador de ventas.</span><span class="sxs-lookup"><span data-stu-id="94d04-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Sales Navigator.</span></span> <span data-ttu-id="94d04-158">Tenga en cuenta que Hola atributos seleccionados como **coincidencia** propiedades será toomatch usado hello las cuentas de usuario y grupos en el navegador de ventas de LinkedIn para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="94d04-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Sales Navigator for update operations.</span></span> <span data-ttu-id="94d04-159">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="94d04-159">Select hello Save button toocommit any changes.</span></span>

![Aprovisionamiento de LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="94d04-161">tooenable Hola servicio de aprovisionamiento de Azure AD para ventas LinkedIn navegador, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección</span><span class="sxs-lookup"><span data-stu-id="94d04-161">tooenable hello Azure AD provisioning service for LinkedIn Sales Navigator, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="94d04-162">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="94d04-162">Click **Save**.</span></span> 

<span data-ttu-id="94d04-163">Esto iniciará la sincronización inicial de Hola de todos los usuarios y grupos asignados tooLinkedIn navegador de ventas en la sección usuarios y grupos de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d04-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Sales Navigator in hello Users and Groups section.</span></span> <span data-ttu-id="94d04-164">Tenga en cuenta que la sincronización inicial de hello surtirá tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d04-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="94d04-165">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de navegador de ventas de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="94d04-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Sales Navigator app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="94d04-166">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="94d04-166">Additional Resources</span></span>

* [<span data-ttu-id="94d04-167">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="94d04-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="94d04-168">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94d04-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
