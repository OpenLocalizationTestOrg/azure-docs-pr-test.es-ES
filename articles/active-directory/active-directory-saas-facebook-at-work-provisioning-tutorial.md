---
title: "Tutorial: Configuración de Workplace by Facebook para el aprovisionamiento de usuarios | Microsoft Docs"
description: "Obtenga información sobre cómo aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD Workplace by Facebook."
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
ms.openlocfilehash: a347eedbf5511dc83e1bc7721667441cfb87cb59
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="ede01-103">Tutorial: Configuración de Workplace by Facebook para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="ede01-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="ede01-104">En este tutorial se muestran los pasos necesarios para aprovisionar y cancelar el aprovisionamiento automáticamente las cuentas de usuario de Azure Active Directory (Azure AD) a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-104">This tutorial shows you the steps necessary to automatically provision and de-provision user accounts from Azure Active Directory (Azure AD) to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ede01-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ede01-105">Prerequisites</span></span>

<span data-ttu-id="ede01-106">Para configurar la integración de Azure AD con Workplace by Facebook, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ede01-106">To configure Azure AD integration with Workplace by Facebook, you need the following:</span></span>

- <span data-ttu-id="ede01-107">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ede01-107">An Azure AD subscription</span></span>
- <span data-ttu-id="ede01-108">Una suscripción habilitada para inicio de sesión único (SSO) de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="ede01-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="ede01-109">Para probar los pasos de este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ede01-109">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="ede01-110">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ede01-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ede01-111">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una oferta de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ede01-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-to-workplace-by-facebook"></a><span data-ttu-id="ede01-112">Asignación de usuarios a Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="ede01-112">Assign users to Workplace by Facebook</span></span>

<span data-ttu-id="ede01-113">Azure AD usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ede01-113">Azure AD uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="ede01-114">En el contexto de aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han asignado a una aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ede01-114">In the context of automatic user account provisioning, only the users and groups that have been assigned to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="ede01-115">Antes de configurar y habilitar el servicio de aprovisionamiento, decida qué usuarios y grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-115">Before configuring and enabling the provisioning service, decide what users and groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="ede01-116">Después, puede asignar estos usuarios a la aplicación de Workplace by Facebook siguiendo las instrucciones de [Asignación de un usuario o un grupo a una aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="ede01-116">You can then assign these users to your Workplace by Facebook app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="ede01-117">Pruebe la configuración de aprovisionamiento mediante la asignación de un único usuario de Azure AD a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-117">Test the provisioning configuration by assigning a single Azure AD user to Workplace by Facebook.</span></span> <span data-ttu-id="ede01-118">Asigne usuarios y grupos adicionales más tarde.</span><span class="sxs-lookup"><span data-stu-id="ede01-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="ede01-119">Al asignar un usuario a Workplace by Facebook, debe seleccionar un rol de usuario válido.</span><span class="sxs-lookup"><span data-stu-id="ede01-119">When you assign a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="ede01-120">El rol Acceso predeterminado no funciona para realizar el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="ede01-120">The Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="ede01-121">Habilitación del aprovisionamiento automático de usuarios</span><span class="sxs-lookup"><span data-stu-id="ede01-121">Enable automated user provisioning</span></span>

<span data-ttu-id="ede01-122">Esta sección le guiará en el proceso de conexión de Azure AD a la API de aprovisionamiento de cuentas de usuario de Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-122">This section guides you through connecting your Azure AD to the user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="ede01-123">También aprenderá a configurar el servicio de aprovisionamiento para crear, actualizar y deshabilitar cuentas de usuario asignado en Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-123">You also learn how to configure the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="ede01-124">Esto se basa en la asignación de grupos y usuarios en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ede01-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="ede01-125">También puede habilitar el SSO basado en SAML para Workplace by Facebook siguiendo las instrucciones de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ede01-125">You can also choose to enabled SAML-based SSO for Workplace by Facebook, by following the instructions provided in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ede01-126">El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.</span><span class="sxs-lookup"><span data-stu-id="ede01-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="ede01-127">Configuración del aprovisionamiento de cuentas de usuario para Workplace by Facebook en Azure AD</span><span class="sxs-lookup"><span data-stu-id="ede01-127">Configure user account provisioning to Workplace by Facebook in Azure AD</span></span>

<span data-ttu-id="ede01-128">Azure AD admite la capacidad de sincronizar automáticamente los detalles de la cuenta de usuarios asignados a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-128">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="ede01-129">Esta sincronización automática permite a Workplace by Facebook obtener los datos que necesita para autorizar a los usuarios a acceder, antes de que intenten iniciar sesión por primera vez.</span><span class="sxs-lookup"><span data-stu-id="ede01-129">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="ede01-130">También desaprovisiona usuarios de Workplace by Facebook cuando se revoque el acceso en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ede01-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="ede01-131">En [Azure Portal](https://portal.azure.com), seleccione **Azure Active Directory**  > **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ede01-131">In the [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="ede01-132">Si ya ha configurado Workplace by Facebook para el inicio de sesión único, busque la instancia de Workplace by Facebook mediante el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="ede01-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using the search field.</span></span> <span data-ttu-id="ede01-133">En caso contrario, seleccione **Agregar** y busque **Workplace by Facebook**  en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ede01-133">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="ede01-134">Seleccione **Workplace by Facebook** en los resultados de búsqueda y agrégalo a la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ede01-134">Select **Workplace by Facebook** from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="ede01-135">Seleccione la instancia de Workplace by Facebook y, después, seleccione la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="ede01-135">Select your instance of Workplace by Facebook, and then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="ede01-136">Establezca el **modo de aprovisionamiento** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="ede01-136">Set **Provisioning Mode** to **Automatic**.</span></span> 

    ![Captura de pantalla de las opciones de aprovisionamiento de Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="ede01-138">En la sección **Credenciales de administrador**, escriba el **token del secreto** y la **dirección URL del inquilino** de su administrador de Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-138">Under the **Admin Credentials** section, enter the **Secret Token** and the **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="ede01-139">En Azure Portal, seleccione **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-139">In the Azure portal, select **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="ede01-140">Si la conexión no se establece, asegúrese de que la cuenta de Workplace by Facebook tiene permisos de administrador de equipo.</span><span class="sxs-lookup"><span data-stu-id="ede01-140">If the connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="ede01-141">Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error de aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla.</span><span class="sxs-lookup"><span data-stu-id="ede01-141">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the check box.</span></span>

8. <span data-ttu-id="ede01-142">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ede01-142">Select **Save**.</span></span>

9. <span data-ttu-id="ede01-143">En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to Workplace by Facebook** (Sincronizar usuarios de Azure Active Directory con Workplace by Facebook).</span><span class="sxs-lookup"><span data-stu-id="ede01-143">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook**.</span></span>

10. <span data-ttu-id="ede01-144">En la sección **Attribute Mappings** (Asignaciones de atributos), revise los atributos de usuario que se sincronizan entre Azure AD y Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-144">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="ede01-145">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de Workplace by Facebook con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="ede01-145">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="ede01-146">Para confirmar los cambios, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ede01-146">To commit any changes, select **Save**.</span></span>

11. <span data-ttu-id="ede01-147">Para habilitar el servicio de aprovisionamiento de Azure AD para Workplace by Facebook, en la sección **Configuración**, cambie el **Estado de aprovisionamiento** a **Activado**.</span><span class="sxs-lookup"><span data-stu-id="ede01-147">To enable the Azure AD provisioning service for Workplace by Facebook, in the **Settings** section, change the **Provisioning Status** to **On**.</span></span>

12. <span data-ttu-id="ede01-148">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ede01-148">Select **Save**.</span></span>

<span data-ttu-id="ede01-149">Para más información sobre cómo configurar el aprovisionamiento automático, consulte [la documentación de Facebook](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="ede01-149">For more information on how to configure automatic provisioning, see [the Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="ede01-150">Ahora puede crear una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="ede01-150">You can now create a test account.</span></span> <span data-ttu-id="ede01-151">Espere 20 minutos para comprobar que la cuenta se ha sincronizado con Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="ede01-151">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ede01-152">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ede01-152">Additional resources</span></span>

* [<span data-ttu-id="ede01-153">Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="ede01-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ede01-154">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ede01-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ede01-155">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ede01-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

