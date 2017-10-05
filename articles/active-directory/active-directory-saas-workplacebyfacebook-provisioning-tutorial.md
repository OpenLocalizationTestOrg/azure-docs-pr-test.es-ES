---
title: "Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Workplace by Facebook."
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
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="ad4ad-103">Tutorial: Configuración de Workplace by Facebook para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="ad4ad-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="ad4ad-104">El objetivo de este tutorial es explicar los pasos que debe realizar en Workplace by Facebook y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD para Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad4ad-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ad4ad-105">Prerequisites</span></span>

<span data-ttu-id="ad4ad-106">Para configurar la integración de Azure AD con Workplace by Facebook, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ad4ad-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="ad4ad-107">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4ad-107">An Azure AD subscription</span></span>
- <span data-ttu-id="ad4ad-108">Una suscripción habilitada para inicio de sesión único de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="ad4ad-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad4ad-109">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad4ad-110">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ad4ad-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad4ad-111">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad4ad-112">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad4ad-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="ad4ad-113">Asignación de usuarios a Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="ad4ad-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="ad4ad-114">Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="ad4ad-115">En el contexto del aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="ad4ad-116">Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="ad4ad-117">Una vez decidido, puede asignar estos usuarios a la aplicación Workplace by Facebook siguiendo estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="ad4ad-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="ad4ad-118">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="ad4ad-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="ad4ad-119">Sugerencias importantes para la asignación de usuarios a Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="ad4ad-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="ad4ad-120">Se recomienda asignar un único usuario de Azure AD a Workplace by Facebook para probar la configuración de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="ad4ad-121">Más tarde, se pueden asignar otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ad4ad-122">Al asignar a un usuario a Workplace by Facebook, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="ad4ad-123">El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ad4ad-124">Habilitación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="ad4ad-124">Enable User Provisioning</span></span>

<span data-ttu-id="ad4ad-125">Esta sección lo guía a través de los pasos necesarios para conectar la API de aprovisionamiento de su cuenta de usuario de Workplace by Facebook, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de Workplace by Facebook en función de la asignación de grupos y usuarios Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="ad4ad-126">También puede habilitar el inicio de sesión único basado en SAML para Workplace by Facebook siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad4ad-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ad4ad-127">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="ad4ad-128">Para configurar el aprovisionamiento de cuentas de usuario para Workplace by Facebook en Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ad4ad-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="ad4ad-129">El objetivo de esta sección es describir cómo habilitar el aprovisionamiento de las cuentas de usuario de Active Directory en Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="ad4ad-130">Azure AD admite la capacidad de sincronizar automáticamente los detalles de la cuenta de usuarios asignados a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="ad4ad-131">Esta sincronización automática permite a Workplace by Facebook obtener los datos que necesita para autorizar a los usuarios a acceder, antes de que intenten iniciar sesión por primera vez.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="ad4ad-132">También desaprovisiona usuarios de Workplace by Facebook cuando se revoque el acceso en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="ad4ad-133">En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory**  > **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="ad4ad-134">Si ya ha configurado Workplace by Facebook para el inicio de sesión único, busque la instancia de Workplace by Facebook mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="ad4ad-135">En caso contrario, seleccione **Agregar** y busque **Workplace by Facebook**  en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="ad4ad-136">Seleccione Workplace by Facebook en los resultados de búsqueda y agrégalo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="ad4ad-137">Seleccione la instancia de Workplace by Facebook y, después, seleccione la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="ad4ad-138">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Aprovisionamiento](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="ad4ad-140">En la sección **Credenciales de administrador**, escriba el token del secreto y la dirección URL del inquilino de su administrador de Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="ad4ad-141">En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="ad4ad-142">Si la conexión no se establece, asegúrese de que la cuenta de Workplace by Facebook tiene permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="ad4ad-143">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error de aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="ad4ad-144">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-144">Click **Save.**</span></span>

9. <span data-ttu-id="ad4ad-145">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to Workplace by Facebook** (Sincronizar usuarios de Azure Active Directory con Workplace by Facebook).</span><span class="sxs-lookup"><span data-stu-id="ad4ad-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="ad4ad-146">En la sección **Attribute Mappings** (Asignaciones de atributos), revise los atributos de usuario que se sincronizan entre Azure AD y Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="ad4ad-147">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de Workplace by Facebook con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="ad4ad-148">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="ad4ad-149">Para habilitar el servicio de aprovisionamiento de Azure AD para Workplace by Facebook, cambie el **Estado de aprovisionamiento** a **Activado** en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="ad4ad-150">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-150">Click **Save.**</span></span>

<span data-ttu-id="ad4ad-151">Para más información sobre cómo configurar el aprovisionamiento automático, consulte [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="ad4ad-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="ad4ad-152">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-152">You can now create a test account.</span></span> <span data-ttu-id="ad4ad-153">Espere 20 minutos para comprobar que la cuenta se ha sincronizado con Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ad4ad-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad4ad-154">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ad4ad-154">Additional resources</span></span>

* [<span data-ttu-id="ad4ad-155">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="ad4ad-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad4ad-156">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad4ad-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ad4ad-157">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ad4ad-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

