---
title: "Tutorial: Configuración de Cerner Central para el aprovisionamiento automático de usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar lista tooa de usuarios en el centro de Cerner."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="ab337-103">Tutorial: configuración de Cerner Central para el aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="ab337-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="ab337-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform Cerner Central y Azure AD tooautomatically aprovisionar y eliminación de aprovisionamiento en cuentas de usuario de la lista de usuarios de Azure AD tooa en Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="ab337-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="ab337-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ab337-105">Prerequisites</span></span>

<span data-ttu-id="ab337-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ab337-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="ab337-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab337-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="ab337-108">Un inquilino de Cerner Central</span><span class="sxs-lookup"><span data-stu-id="ab337-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="ab337-109">Azure Active Directory se integra con el centro de Cerner con hello [SCIM](http://www.simplecloud.info/) protocolo.</span><span class="sxs-lookup"><span data-stu-id="ab337-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="ab337-110">Asignar usuarios tooCerner Central</span><span class="sxs-lookup"><span data-stu-id="ab337-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="ab337-111">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ab337-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ab337-112">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizan sólo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab337-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="ab337-113">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, debe decidir qué usuarios o grupos en Azure AD representan a usuarios de Hola que necesitan tener acceso a tooCerner Central.</span><span class="sxs-lookup"><span data-stu-id="ab337-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="ab337-114">Una vez decidido, puede asignar estas tooCerner centro de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="ab337-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="ab337-115">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="ab337-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="ab337-116">Sugerencias importantes para asignar usuarios tooCerner Central</span><span class="sxs-lookup"><span data-stu-id="ab337-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="ab337-117">Se recomienda que un único usuario de Azure AD asignarse tooCerner tootest Central Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="ab337-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="ab337-118">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="ab337-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="ab337-119">Una vez completada para un solo usuario la comprobación inicial, Cerner Central recomienda asignar Hola toda la lista de usuarios crea tooaccess lista de usuarios de la tooCerner de cualquier toobe aprovisionado de soluciones (no solo Cerner Central) Cerner.</span><span class="sxs-lookup"><span data-stu-id="ab337-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="ab337-120">Otras soluciones de Cerner aprovechan esta lista de usuarios en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab337-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="ab337-121">Al asignar un centro de tooCerner de usuario, debe seleccionar hello **usuario** rol en el cuadro de diálogo de hello asignación.</span><span class="sxs-lookup"><span data-stu-id="ab337-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="ab337-122">Los usuarios con el rol de "Acceso predeterminado" Hola se excluyen de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="ab337-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="ab337-123">Configuración de aprovisionamiento tooCerner centro de usuarios</span><span class="sxs-lookup"><span data-stu-id="ab337-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="ab337-124">Esta sección le guía a través de conexión de lista de usuarios de su Azure AD tooCerner Central mediante la API de aprovisionamiento de cuentas de usuario del Cerner SCIM y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas en el centro de Cerner en función de usuario asignado en la asignación de usuario y de grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab337-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="ab337-125">También puede elegir tooenabled basado en SAML Single Sign-On para Cerner Central, siguiendo instrucciones de hello proporcionadas en [portal de Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ab337-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="ab337-126">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="ab337-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="ab337-127">Para obtener más información, vea hello [tutorial de inicio de sesión único de centro de Cerner](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ab337-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="ab337-128">cuenta de usuario automática de tooconfigure tooCerner Central de aprovisionamiento en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ab337-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="ab337-129">En orden tooprovision usuario cuentas tooCerner Central, podrá necesita una cuenta de sistema Cerner centro de Cerner toorequest y generar un token de portador de OAuth que Azure AD puede utilizar el punto de conexión del tooconnect tooCerner SCIM.</span><span class="sxs-lookup"><span data-stu-id="ab337-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="ab337-130">También se recomienda que la integración de Hola se realizan en un entorno de espacio aislado de Cerner antes de implementar tooproduction.</span><span class="sxs-lookup"><span data-stu-id="ab337-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="ab337-131">Hola primer paso es personas de hello tooensure administrar Hola Cerner e integración de Azure AD tiene una cuenta de CernerCare, que es necesario tooaccess Hola documentación necesarios toocomplete Hola instrucciones.</span><span class="sxs-lookup"><span data-stu-id="ab337-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="ab337-132">Si es necesario, usar direcciones URL de hello debajo toocreate CernerCare cuentas en cada entorno es aplicable.</span><span class="sxs-lookup"><span data-stu-id="ab337-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="ab337-133">Espacio aislado: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="ab337-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="ab337-134">Producción: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="ab337-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="ab337-135">A continuación, se debe crear una cuenta de sistema para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab337-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="ab337-136">Use las instrucciones de hello debajo toorequest una cuenta de sistema para los entornos de producción y de espacio aislado.</span><span class="sxs-lookup"><span data-stu-id="ab337-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="ab337-137">Instrucciones: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="ab337-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="ab337-138">Espacio aislado: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="ab337-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="ab337-139">Producción: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="ab337-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="ab337-140">A continuación, genere un token de portador de OAuth para cada una de las cuentas del sistema.</span><span class="sxs-lookup"><span data-stu-id="ab337-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="ab337-141">toodo this, follow Hola estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="ab337-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="ab337-142">Instrucciones: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="ab337-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="ab337-143">Espacio aislado: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="ab337-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="ab337-144">Producción: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="ab337-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="ab337-145">Por último, debe tooacquire usuario lista territorio identificadores para ambos entornos de espacio aislado y de producción de hello en la configuración de Cerner toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="ab337-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="ab337-146">Para obtener información acerca de cómo tooacquire, vea: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="ab337-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="ab337-147">Ahora puede configurar tooCerner de cuentas de usuario de Azure AD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="ab337-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="ab337-148">Inicie sesión en toohello [portal de Azure](https://portal.azure.com)y examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="ab337-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="ab337-149">Si ya has configurado Cerner Central para el inicio de sesión único, busque la instancia del centro de Cerner mediante el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab337-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="ab337-150">En caso contrario, seleccione **agregar** y busque **Cerner Central** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab337-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="ab337-151">Seleccione Cerner Central en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ab337-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="ab337-152">Seleccione la instancia del centro de Cerner, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="ab337-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="ab337-153">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="ab337-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Aprovisionamiento de Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="ab337-155">Rellene Hola después de campos en **las credenciales de administrador**:</span><span class="sxs-lookup"><span data-stu-id="ab337-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="ab337-156">Hola **dirección URL del inquilino** , a continuación, escriba una dirección URL en formato de hello siguiente, reemplazando "User-lista-dominio-ID" con el Id. de dominio Kerberos de hello adquiridos en el paso 4 de #.</span><span class="sxs-lookup"><span data-stu-id="ab337-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="ab337-157">Espacio aislado: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="ab337-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="ab337-158">Producción: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="ab337-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="ab337-159">Hola **secreto Token** campo, escriba el token de portador de OAuth de Hola que generó en el paso 3 de # y haga clic en **Probar conexión**.</span><span class="sxs-lookup"><span data-stu-id="ab337-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="ab337-160">Verá una notificación de éxito en el lado superior derecho de hello del portal.</span><span class="sxs-lookup"><span data-stu-id="ab337-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="ab337-161">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y comprobar Hola casilla incluida a continuación.</span><span class="sxs-lookup"><span data-stu-id="ab337-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="ab337-162">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ab337-162">Click **Save**.</span></span> 

12. <span data-ttu-id="ab337-163">Hola **asignaciones de atributos** sección, revise el usuario de Hola y toobe de atributos de grupo sincronizado desde Azure AD tooCerner Central.</span><span class="sxs-lookup"><span data-stu-id="ab337-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="ab337-164">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario de hello toomatch utilizado y los grupos en Cerner Central para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="ab337-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="ab337-165">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="ab337-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="ab337-166">tooenable Hola servicio de aprovisionamiento de Azure AD para Cerner Central, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección</span><span class="sxs-lookup"><span data-stu-id="ab337-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="ab337-167">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ab337-167">Click **Save**.</span></span> 

<span data-ttu-id="ab337-168">Esto inicia la sincronización inicial de Hola de los usuarios o grupos asignados tooCerner Central en la sección usuarios y grupos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab337-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="ab337-169">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se esté ejecutando Hola servicio de aprovisionamiento de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab337-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="ab337-170">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de centro de Cerner.</span><span class="sxs-lookup"><span data-stu-id="ab337-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="ab337-171">Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="ab337-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab337-172">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ab337-172">Additional resources</span></span>

* <span data-ttu-id="ab337-173">[Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD) (Cerner Central: Publicación de datos de identidad mediante Azure AD)</span><span class="sxs-lookup"><span data-stu-id="ab337-173">[Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)</span></span>
* [<span data-ttu-id="ab337-174">Tutorial: configuración de Cerner Central para el inicio de sesión único con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab337-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="ab337-175">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="ab337-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="ab337-176">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ab337-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="ab337-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab337-177">Next steps</span></span>
* <span data-ttu-id="ab337-178">[Obtenga información acerca de cómo se registra tooreview y get informa sobre el aprovisionamiento de actividad](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="ab337-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
