---
title: "Tutorial: integración de Azure Active Directory con Qualtrics | Microsoft Docs"
description: "Aprenda cómo usar Qualtrics con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="4fc3c-103">Tutorial: Integración de Azure Active Directory con Qualtrics</span><span class="sxs-lookup"><span data-stu-id="4fc3c-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="4fc3c-104">El objetivo de este tutorial es mostrar la integración de Azure y Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="4fc3c-105">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4fc3c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="4fc3c-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="4fc3c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="4fc3c-107">Una suscripción habilitada para el inicio de sesión único (SSO) en Qualtrics</span><span class="sxs-lookup"><span data-stu-id="4fc3c-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="4fc3c-108">Después de completar este tutorial, los usuarios de Azure AD asignados a Qualtrics podrán realizar un inicio de sesión único en la aplicación en el sitio de la compañía Qualtrics (inicio de sesión iniciado por el proveedor de servicios) o con la [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4fc3c-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="4fc3c-109">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4fc3c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="4fc3c-110">Habilitación de la integración de aplicaciones para Qualtrics</span><span class="sxs-lookup"><span data-stu-id="4fc3c-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="4fc3c-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="4fc3c-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="4fc3c-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="4fc3c-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="4fc3c-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="4fc3c-113">Assigning users</span></span>

<span data-ttu-id="4fc3c-114">![Escenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="4fc3c-115">Habilitación de la integración de aplicaciones para Qualtrics</span><span class="sxs-lookup"><span data-stu-id="4fc3c-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="4fc3c-116">El objetivo de esta sección es describir cómo habilitar la integración de las aplicaciones para Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="4fc3c-117">**Siga estos pasos con el fin de habilitar la integración de aplicaciones para Qualtrics:**</span><span class="sxs-lookup"><span data-stu-id="4fc3c-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc3c-118">En el panel de navegación izquierdo del Portal de Azure clásico, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="4fc3c-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="4fc3c-120">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4fc3c-121">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="4fc3c-122">![Aplicaciones](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="4fc3c-123">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="4fc3c-124">![Agregar aplicaciones](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="4fc3c-125">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="4fc3c-126">![Agregar una aplicación de la galería](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="4fc3c-127">En el **cuadro de búsqueda**, escriba **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="4fc3c-128">![Galería de aplicaciones](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="4fc3c-129">En el panel de resultados, seleccione **Qualtrics** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="4fc3c-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="4fc3c-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="4fc3c-131">Configure single sign-on</span></span>

<span data-ttu-id="4fc3c-132">El objetivo de esta sección es describir cómo se habilita la autenticación de los usuarios en Qualtrics con su cuenta de Azure AD usando el protocolo SAML basado en la federación.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="4fc3c-133">**Siga estos pasos para configurar el inicio de sesión único:**</span><span class="sxs-lookup"><span data-stu-id="4fc3c-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc3c-134">En el Portal de Azure clásico, en la página de integración de aplicaciones de **Qualtrics**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4fc3c-135">![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="4fc3c-136">En la página **¿Cómo desea que los usuarios inicien sesión en Qualtrics?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="4fc3c-137">![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="4fc3c-138">En la página **Configurar dirección URL de la aplicación**, en el cuadro de texto de **URL de inicio de sesión de Qualtrics**, escriba su dirección URL (por ejemplo, “*https://ssotest2ut1.qualtrics.com*") y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="4fc3c-139">![Configurar dirección URL de la aplicación](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="4fc3c-140">En la página **Configuración de inicio de sesión único en Qualtrics**, haga clic en **Descargar metadatos** y guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="4fc3c-141">![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="4fc3c-142">Envíe el archivo de metadatos al equipo de soporte técnico de Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="4fc3c-143">La configuración del inicio de sesión único la debe realizar el equipo de soporte técnico de Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="4fc3c-144">Tan pronto como se complete la configuración, recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="4fc3c-145">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4fc3c-146">![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="4fc3c-147">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="4fc3c-147">Configure user provisioning</span></span>

<span data-ttu-id="4fc3c-148">No hay elemento de acción para que configure el aprovisionamiento de usuarios en Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="4fc3c-149">Cuando un usuario asignado intenta iniciar sesión en Qualtrics desde el panel de acceso, Qualtrics comprueba si el usuario existe.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="4fc3c-150">Si no hay cuentas de usuario disponibles, Qualtrics crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="4fc3c-151">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="4fc3c-151">Assign users</span></span>
<span data-ttu-id="4fc3c-152">Para probar la configuración, debe conceder acceso a los usuarios de Azure AD a los que quiere permitir el uso de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="4fc3c-153">**Para asignar usuarios a Qualtrics, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="4fc3c-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc3c-154">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="4fc3c-155">En la página de integración de aplicaciones de **Qualtrics**, haga clic en **Asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="4fc3c-156">![Asignar usuarios](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="4fc3c-157">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="4fc3c-158">![Sí](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="4fc3c-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="4fc3c-159">Si desea probar la configuración de inicio de sesión único (SSO), abra el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4fc3c-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="4fc3c-160">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4fc3c-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

