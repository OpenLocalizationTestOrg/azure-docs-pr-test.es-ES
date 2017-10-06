---
title: "Tutorial: Configuración de ThousandEyes para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooThousandEyes."
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
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="4ae52-103">Tutorial: Configuración de ThousandEyes para aprovisionar a los usuarios automáticamente</span><span class="sxs-lookup"><span data-stu-id="4ae52-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="4ae52-104">objetivo de Hola de este tutorial es tooshow que Hola pasos necesita tooperform en ThousandEyes y Azure AD tooautomatically el aprovisionamiento y Desaprovisionamiento de cuentas de usuario de Azure AD tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="4ae52-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ThousandEyes and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4ae52-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4ae52-105">Prerequisites</span></span>

<span data-ttu-id="4ae52-106">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4ae52-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="4ae52-107">Un inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ae52-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="4ae52-108">Un inquilino de ThousandEyes con hello [plan estándar](https://www.thousandeyes.com/pricing) o mejor habilitado</span><span class="sxs-lookup"><span data-stu-id="4ae52-108">A ThousandEyes tenant with hello [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="4ae52-109">Una cuenta de usuario de ThousandEyes con permisos de administrador</span><span class="sxs-lookup"><span data-stu-id="4ae52-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="4ae52-110">Hello Azure AD aprovisionamiento integración se basa en hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), que son los equipos de tooThousandEyes disponible en el plan estándar de Hola o superior.</span><span class="sxs-lookup"><span data-stu-id="4ae52-110">hello Azure AD provisioning integration relies on hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available tooThousandEyes teams on hello Standard plan or better.</span></span>

## <a name="assigning-users-toothousandeyes"></a><span data-ttu-id="4ae52-111">Asignar usuarios tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="4ae52-111">Assigning users tooThousandEyes</span></span>

<span data-ttu-id="4ae52-112">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4ae52-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="4ae52-113">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ae52-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="4ae52-114">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan acceder a la aplicación de ThousandEyes de tooyour.</span><span class="sxs-lookup"><span data-stu-id="4ae52-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ThousandEyes app.</span></span> <span data-ttu-id="4ae52-115">Una vez decidido, puede asignar estas aplicaciones de ThousandEyes tooyour de usuarios siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="4ae52-115">Once decided, you can assign these users tooyour ThousandEyes app by following hello instructions here:</span></span>

[<span data-ttu-id="4ae52-116">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="4ae52-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a><span data-ttu-id="4ae52-117">Sugerencias importantes para asignar usuarios tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="4ae52-117">Important tips for assigning users tooThousandEyes</span></span>

*   <span data-ttu-id="4ae52-118">Se recomienda que un único usuario de Azure AD se asigna tooThousandEyes tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="4ae52-118">It is recommended that a single Azure AD user is assigned tooThousandEyes tootest hello provisioning configuration.</span></span> <span data-ttu-id="4ae52-119">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="4ae52-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4ae52-120">Al asignar una tooThousandEyes de usuario, debe seleccionar cualquier hello **usuario** u otra válida específica de la aplicación rol (si está disponible) en el cuadro de diálogo de hello asignación.</span><span class="sxs-lookup"><span data-stu-id="4ae52-120">When assigning a user tooThousandEyes, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="4ae52-121">Hola **acceso predeterminado** rol no funciona para el aprovisionamiento y se omiten estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="4ae52-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toothousandeyes"></a><span data-ttu-id="4ae52-122">Configurar tooThousandEyes de aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="4ae52-122">Configuring user provisioning tooThousandEyes</span></span> 

<span data-ttu-id="4ae52-123">Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooThousandEyes de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en ThousandEyes en función de asignación de usuario y grupo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ae52-123">This section guides you through connecting your Azure AD tooThousandEyes's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="4ae52-124">También puede elegir tooenabled basado en SAML Single Sign-On para ThousandEyes, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4ae52-124">You may also choose tooenabled SAML-based Single Sign-On for ThousandEyes, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4ae52-125">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="4ae52-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a><span data-ttu-id="4ae52-126">Configurar aprovisionamiento tooThousandEyes en Azure AD de la cuenta de usuario automática</span><span class="sxs-lookup"><span data-stu-id="4ae52-126">Configure automatic user account provisioning tooThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="4ae52-127">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="4ae52-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="4ae52-128">Si ya ha configurado ThousandEyes para el inicio de sesión único, busque la instancia de ThousandEyes con el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae52-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using hello search field.</span></span> <span data-ttu-id="4ae52-129">En caso contrario, seleccione **agregar** y busque **ThousandEyes** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae52-129">Otherwise, select **Add** and search for **ThousandEyes** in hello application gallery.</span></span> <span data-ttu-id="4ae52-130">Seleccione ThousandEyes en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4ae52-130">Select ThousandEyes from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="4ae52-131">Seleccione la instancia de ThousandEyes, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="4ae52-131">Select your instance of ThousandEyes, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="4ae52-132">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="4ae52-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Aprovisionamiento de ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="4ae52-134">En hello **las credenciales de administrador** entrada hello, en una sección **secreto del Token** generados por cuenta de su ThousandEyes (puede encontrar el token de hello en su cuenta de ThousandEyes: **seguridad & Autenticación**).</span><span class="sxs-lookup"><span data-stu-id="4ae52-134">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your ThousandEyes's account (you can find hello token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![Aprovisionamiento de ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="4ae52-136">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de ThousandEyes de tooyour.</span><span class="sxs-lookup"><span data-stu-id="4ae52-136">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ThousandEyes app.</span></span> <span data-ttu-id="4ae52-137">Si se produce un error en la conexión de hello, asegúrese de que su cuenta de ThousandEyes tiene permisos de administrador e inténtelo de nuevo el paso 5.</span><span class="sxs-lookup"><span data-stu-id="4ae52-137">If hello connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="4ae52-138">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y la casilla de verificación Hola "envían una notificación por correo electrónico cuando se produce un error."</span><span class="sxs-lookup"><span data-stu-id="4ae52-138">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="4ae52-139">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4ae52-139">Click **Save**.</span></span> 

9. <span data-ttu-id="4ae52-140">En la sección asignaciones de hello, seleccione **tooThousandEyes sincronizar Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="4ae52-140">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooThousandEyes**.</span></span>

10. <span data-ttu-id="4ae52-141">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooThousandEyes de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ae52-141">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooThousandEyes.</span></span> <span data-ttu-id="4ae52-142">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del Hola toomatch utilizados en ThousandEyes para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="4ae52-142">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="4ae52-143">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="4ae52-143">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="4ae52-144">tooenable Hola servicio de aprovisionamiento de Azure AD para ThousandEyes, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección</span><span class="sxs-lookup"><span data-stu-id="4ae52-144">tooenable hello Azure AD provisioning service for ThousandEyes, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="4ae52-145">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4ae52-145">Click **Save**.</span></span> 

<span data-ttu-id="4ae52-146">Esta operación inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooThousandEyes Hola a los usuarios y la sección de grupos.</span><span class="sxs-lookup"><span data-stu-id="4ae52-146">This operation starts hello initial synchronization of any users and/or groups assigned tooThousandEyes in hello Users and Groups section.</span></span> <span data-ttu-id="4ae52-147">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae52-147">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="4ae52-148">Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="4ae52-148">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="4ae52-149">Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="4ae52-149">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4ae52-150">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4ae52-150">Additional resources</span></span>

* [<span data-ttu-id="4ae52-151">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="4ae52-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="4ae52-152">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4ae52-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="4ae52-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ae52-153">Next steps</span></span>

* [<span data-ttu-id="4ae52-154">Obtenga información acerca de cómo se registra tooreview y obtener informes sobre el aprovisionamiento de actividad</span><span class="sxs-lookup"><span data-stu-id="4ae52-154">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
