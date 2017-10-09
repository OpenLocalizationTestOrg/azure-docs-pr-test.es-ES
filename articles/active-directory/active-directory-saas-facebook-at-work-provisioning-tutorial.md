---
title: "Tutorial: Configuración de Workplace by Facebook para el aprovisionamiento de usuarios | Microsoft Docs"
description: "Obtenga información acerca de cómo tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooWorkplace Facebook."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="13c92-103">Tutorial: Configuración de Workplace by Facebook para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="13c92-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="13c92-104">Este tutorial muestra Hola tooautomatically necesarios pasos aprovisionar y desaprovisionar cuentas de usuario de Azure Active Directory (Azure AD) tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13c92-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="13c92-105">Prerequisites</span></span>

<span data-ttu-id="13c92-106">integración de Azure AD con un área de trabajo Facebook tooconfigure, necesita siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="13c92-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="13c92-107">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="13c92-107">An Azure AD subscription</span></span>
- <span data-ttu-id="13c92-108">Una suscripción habilitada para inicio de sesión único (SSO) de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="13c92-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="13c92-109">pasos de hello tootest en este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="13c92-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="13c92-110">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="13c92-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="13c92-111">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una oferta de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13c92-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="13c92-112">Asignar usuarios tooWorkplace Facebook</span><span class="sxs-lookup"><span data-stu-id="13c92-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="13c92-113">Azure AD usa un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="13c92-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="13c92-114">En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizan sólo los usuarios de Hola y grupos que se han asignado tooan aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13c92-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="13c92-115">Antes de configurar y habilitar Hola aprovisionamiento del servicio, decida qué usuarios y grupos en Azure AD representan a usuarios de Hola que necesitan tener acceso al área de trabajo de tooyour por aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="13c92-116">A continuación, puede asignar estas tooyour al área de trabajo de usuarios por aplicación de Facebook siguiendo Hola instrucciones [asignar una aplicación de empresa de tooan de usuario o grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="13c92-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="13c92-117">Hola prueba configuración de aprovisionamiento mediante la asignación de una sola tooWorkplace de usuario de Azure AD Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="13c92-118">Asigne usuarios y grupos adicionales más tarde.</span><span class="sxs-lookup"><span data-stu-id="13c92-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="13c92-119">Cuando se asigna un tooWorkplace usuario Facebook, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="13c92-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="13c92-120">rol de acceso predeterminado de Hello no funciona para el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="13c92-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="13c92-121">Habilitación del aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="13c92-121">Enable automated user provisioning</span></span>

<span data-ttu-id="13c92-122">En esta sección le guiará en el proceso de conexión de su cuenta de usuario de Azure AD toohello aprovisionamiento API del área de trabajo Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="13c92-123">También aprenderá cómo tooconfigure Hola aprovisionamiento toocreate de servicio, actualizar y deshabilitar cuentas de usuario asignado en lugar de trabajo Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="13c92-124">Esto se basa en la asignación de grupos y usuarios en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13c92-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="13c92-125">También puede elegir tooenabled SSO basado en SAML para Facebook, al área de trabajo por siguiendo las instrucciones de hello proporcionadas en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13c92-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="13c92-126">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="13c92-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="13c92-127">Configurar aprovisionamiento tooWorkplace Facebook en Azure AD de la cuenta de usuario</span><span class="sxs-lookup"><span data-stu-id="13c92-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="13c92-128">Azure admite AD Hola capacidad tooautomatically sincronizar los detalles de la cuenta de hello de asigna usuarios tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="13c92-129">Esta sincronización automática permite al área de trabajo mediante datos de Facebook tooget Hola debe tooauthorize a los usuarios para tener acceso, antes de implementarlos intentar toosign en para hello primera vez.</span><span class="sxs-lookup"><span data-stu-id="13c92-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="13c92-130">También desaprovisiona usuarios de Workplace by Facebook cuando se revoque el acceso en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13c92-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="13c92-131">Hola [portal de Azure](https://portal.azure.com), seleccione **Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="13c92-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="13c92-132">Si ya ha configurado un área de trabajo Facebook para SSO, buscar la instancia de un área de trabajo Facebook mediante el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="13c92-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="13c92-133">En caso contrario, seleccione **agregar** y busque **al área de trabajo Facebook** en Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="13c92-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="13c92-134">Seleccione **al área de trabajo Facebook** de hello resultados de búsqueda y agregarlo a tooyour lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="13c92-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="13c92-135">Seleccione la instancia de un área de trabajo Facebook y, a continuación, seleccione hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="13c92-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="13c92-136">Establecer **modo de aprovisionamiento** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="13c92-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Captura de pantalla de las opciones de aprovisionamiento de Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="13c92-138">En hello **las credenciales de administrador** sección, escriba Hola **secreto Token** hello y **dirección URL del inquilino** su área de trabajo mediante el Administrador de Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="13c92-139">Hola portal de Azure, seleccione **Probar conexión** tooensure Azure AD puede conectarse tooyour al área de trabajo por la aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="13c92-140">Si se produce un error en la conexión de hello, asegúrese de que el área de trabajo por cuenta de Facebook tiene permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="13c92-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="13c92-141">Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y la casilla de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="13c92-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="13c92-142">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="13c92-142">Select **Save**.</span></span>

9. <span data-ttu-id="13c92-143">En la sección asignaciones de hello, seleccione **tooWorkplace sincronizar Azure Active Directory Users Facebook**.</span><span class="sxs-lookup"><span data-stu-id="13c92-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="13c92-144">Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde Azure AD tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="13c92-145">Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en lugar de trabajo Facebook para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="13c92-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="13c92-146">toocommit todos los cambios, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="13c92-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="13c92-147">tooenable Hola servicio de aprovisionamiento de Azure AD para Facebook, al área de trabajo en hello **configuración** sección, cambie hello **estado de aprovisionamiento** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="13c92-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="13c92-148">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="13c92-148">Select **Save**.</span></span>

<span data-ttu-id="13c92-149">Para obtener más información acerca de cómo tooconfigure automática de aprovisionamiento, vea [Hola documentación de Facebook](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="13c92-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="13c92-150">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="13c92-150">You can now create a test account.</span></span> <span data-ttu-id="13c92-151">Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="13c92-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="13c92-152">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="13c92-152">Additional resources</span></span>

* [<span data-ttu-id="13c92-153">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="13c92-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13c92-154">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13c92-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="13c92-155">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="13c92-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

