---
title: "Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y un área de trabajo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="a896b-103">Tutorial: Configuración de Workplace by Facebook para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="a896b-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="a896b-104">objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en lugar de trabajo por Facebook y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="a896b-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a896b-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a896b-105">Prerequisites</span></span>

<span data-ttu-id="a896b-106">integración de Azure AD con un área de trabajo Facebook tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a896b-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="a896b-107">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a896b-107">An Azure AD subscription</span></span>
- <span data-ttu-id="a896b-108">Una suscripción habilitada para inicio de sesión único de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="a896b-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a896b-109">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a896b-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a896b-110">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a896b-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a896b-111">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a896b-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a896b-112">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a896b-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="a896b-113">Asignar usuarios tooWorkplace Facebook</span><span class="sxs-lookup"><span data-stu-id="a896b-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="a896b-114">Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a896b-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="a896b-115">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a896b-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="a896b-116">Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso al área de trabajo de tooyour por aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="a896b-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="a896b-117">Una vez decidido, puede asignar estas tooyour al área de trabajo de usuarios por aplicación de Facebook siguiendo las instrucciones de hello aquí:</span><span class="sxs-lookup"><span data-stu-id="a896b-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="a896b-118">Asignar un usuario o grupo tooan su aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="a896b-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="a896b-119">Sugerencias importantes para asignar usuarios tooWorkplace Facebook</span><span class="sxs-lookup"><span data-stu-id="a896b-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="a896b-120">Se recomienda que un único usuario de Azure AD asignada tooWorkplace por Facebook tootest Hola aprovisionamiento de configuración.</span><span class="sxs-lookup"><span data-stu-id="a896b-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="a896b-121">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="a896b-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a896b-122">Al asignar un tooWorkplace usuario Facebook, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="a896b-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="a896b-123">rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="a896b-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="a896b-124">Habilitación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="a896b-124">Enable User Provisioning</span></span>

<span data-ttu-id="a896b-125">Esta sección le guía a través de conectarse la tooWorkplace de Azure AD mediante la API de aprovisionamiento de cuentas de usuario de Facebook y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en lugar de trabajo en función de usuario y grupo de Facebook asignación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a896b-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="a896b-126">También puede elegir tooenabled basado en SAML Single Sign-On para Facebook, siguiendo las instrucciones Hola proporcionadas en el área de trabajo [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a896b-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a896b-127">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="a896b-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="a896b-128">cuenta de usuario de tooconfigure tooWorkplace Facebook de aprovisionamiento en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a896b-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="a896b-129">objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuario de Active Directory cuentas tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="a896b-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="a896b-130">Azure admite AD Hola capacidad tooautomatically sincronizar los detalles de la cuenta de hello de asigna usuarios tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="a896b-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="a896b-131">Esta sincronización automática permite al área de trabajo mediante datos de Facebook tooget Hola debe tooauthorize a los usuarios para tener acceso, antes de implementarlos intentar toosign en para hello primera vez.</span><span class="sxs-lookup"><span data-stu-id="a896b-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="a896b-132">También desaprovisiona usuarios de Workplace by Facebook cuando se revoque el acceso en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a896b-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="a896b-133">Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory** > **aplicaciones empresariales** > **detodaslasaplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="a896b-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="a896b-134">Si ya ha configurado un área de trabajo Facebook para inicio de sesión único, busque la instancia de un área de trabajo mediante el campo de búsqueda de Hola de Facebook.</span><span class="sxs-lookup"><span data-stu-id="a896b-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="a896b-135">En caso contrario, seleccione **agregar** y busque **al área de trabajo Facebook** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a896b-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="a896b-136">Seleccione un área de trabajo Facebook en resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a896b-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="a896b-137">Seleccione la instancia de un área de trabajo Facebook, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="a896b-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="a896b-138">Conjunto hello **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="a896b-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="a896b-140">En hello **las credenciales de administrador** sección, escriba el secreto del Token de Hola y Hola URL de inquilino de su área de trabajo mediante el Administrador de Facebook.</span><span class="sxs-lookup"><span data-stu-id="a896b-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="a896b-141">Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectarse tooyour al área de trabajo por la aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="a896b-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="a896b-142">Si se produce un error en la conexión de hello, asegúrese de que el área de trabajo por cuenta de Facebook tiene permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="a896b-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="a896b-143">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.</span><span class="sxs-lookup"><span data-stu-id="a896b-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="a896b-144">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a896b-144">Click **Save.**</span></span>

9. <span data-ttu-id="a896b-145">En la sección asignaciones de hello, seleccione **tooWorkplace sincronizar Azure Active Directory Users Facebook.**</span><span class="sxs-lookup"><span data-stu-id="a896b-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="a896b-146">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde Azure AD tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="a896b-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="a896b-147">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en lugar de trabajo Facebook para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="a896b-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="a896b-148">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="a896b-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="a896b-149">tooenable Hola servicio de aprovisionamiento de Azure AD para un área de trabajo Facebook, Hola de cambio **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección</span><span class="sxs-lookup"><span data-stu-id="a896b-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="a896b-150">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a896b-150">Click **Save.**</span></span>

<span data-ttu-id="a896b-151">Para obtener más información acerca de cómo tooconfigure automática de aprovisionamiento, vea [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="a896b-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="a896b-152">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="a896b-152">You can now create a test account.</span></span> <span data-ttu-id="a896b-153">Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="a896b-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a896b-154">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a896b-154">Additional resources</span></span>

* [<span data-ttu-id="a896b-155">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="a896b-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a896b-156">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a896b-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a896b-157">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a896b-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

