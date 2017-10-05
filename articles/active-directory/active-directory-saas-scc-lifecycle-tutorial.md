---
title: "Tutorial: Integración de Azure Active Directory con SCC LifeCycle | Microsoft Docs"
description: "Aprenda cómo usar SCC LifeCycle con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a30bcca720ff135d0180d73f46e78403e9bca43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="ef8db-103">Tutorial: Integración de Azure Active Directory con SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="ef8db-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="ef8db-104">El objetivo de este tutorial es mostrar la integración de Azure y SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ef8db-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="ef8db-105">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ef8db-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="ef8db-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="ef8db-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ef8db-107">Una suscripción habilitada para el inicio de sesión único (SSO) en SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="ef8db-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="ef8db-108">Después de completar este tutorial, los usuarios de Azure AD que ha asignado a SCC LifeCycle podrán realizar un inicio de sesión único en la aplicación en el sitio de la compañía de SCC LifeCycle (inicio de sesión iniciado por el proveedor de servicios) o con la [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef8db-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="ef8db-109">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ef8db-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="ef8db-110">Habilitación de la integración de aplicaciones para SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="ef8db-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="ef8db-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="ef8db-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="ef8db-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="ef8db-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="ef8db-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="ef8db-113">Assigning users</span></span>

<span data-ttu-id="ef8db-114">![Escenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="ef8db-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="ef8db-115">Habilitación de la integración de aplicaciones para SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="ef8db-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="ef8db-116">El objetivo de esta sección es describir cómo habilitar la integración de las aplicaciones para SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ef8db-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="ef8db-117">**Siga estos pasos con el fin de habilitar la integración de aplicaciones en SCC LifeCycle:**</span><span class="sxs-lookup"><span data-stu-id="ef8db-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="ef8db-118">En el panel de navegación izquierdo del Portal de Azure clásico, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ef8db-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="ef8db-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ef8db-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="ef8db-120">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="ef8db-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ef8db-121">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="ef8db-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="ef8db-122">![Aplicaciones](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="ef8db-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ef8db-123">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="ef8db-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="ef8db-124">![Agregar aplicaciones](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="ef8db-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ef8db-125">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="ef8db-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="ef8db-126">![Agregar una aplicación de la galería](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="ef8db-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ef8db-127">En el **cuadro de búsqueda**, escriba **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="ef8db-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="ef8db-128">![Galería de aplicaciones](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="ef8db-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="ef8db-129">En el panel de resultados, seleccione **SCC LifeCycle** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef8db-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="ef8db-130">![Ciclo de vida de SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "Ciclo de vida de SCC")</span><span class="sxs-lookup"><span data-stu-id="ef8db-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="ef8db-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ef8db-131">Configure single sign-on</span></span>

<span data-ttu-id="ef8db-132">El objetivo de esta sección es describir cómo se habilita la autenticación de los usuarios en SCC LifeCycle con su cuenta de Azure AD usando el protocolo SAML basado en la federación.</span><span class="sxs-lookup"><span data-stu-id="ef8db-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="ef8db-133">**Siga estos pasos para configurar el inicio de sesión único:**</span><span class="sxs-lookup"><span data-stu-id="ef8db-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="ef8db-134">En el Portal de Azure clásico, en la página de integración de aplicaciones de **SCC LifeCycle**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ef8db-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="ef8db-135">![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ef8db-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="ef8db-136">En la página **¿Cómo desea que los usuarios inicien sesión en SCC LifeCycle?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ef8db-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="ef8db-137">![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ef8db-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="ef8db-138">En la página **Configurar dirección URL de la aplicación**, en el cuadro de texto **URL de inicio de sesión** de, escriba la dirección URL utilizada por los usuarios para iniciar sesión en su aplicación de SCC LifeCycle con el patrón "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*" y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ef8db-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="ef8db-139">![Configurar dirección URL de la aplicación](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="ef8db-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="ef8db-140">En la página **Configuración de inicio de sesión único en SCC LifeCycle**, haga clic en **Descargar metadatos** y guarde el archivo de metadatos localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ef8db-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="ef8db-141">![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ef8db-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="ef8db-142">Reenvíe el archivo de metadatos al equipo de soporte técnico de SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ef8db-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="ef8db-143">El equipo de soporte técnico de SCC LifeCycle es el que debe habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ef8db-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="ef8db-144">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ef8db-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="ef8db-145">![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ef8db-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="ef8db-146">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="ef8db-146">Configure user provisioning</span></span>

<span data-ttu-id="ef8db-147">Para permitir que los usuarios de Azure AD inicien sesión en SCC LifeCycle, deben aprovisionarse en SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ef8db-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="ef8db-148">No hay elemento de acción para que configure el aprovisionamiento de usuarios en SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="ef8db-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="ef8db-149">Cuando un usuario asignado intente iniciar sesión en LifeCycle, se creará automáticamente una cuenta de LifeCycle si es necesario.</span><span class="sxs-lookup"><span data-stu-id="ef8db-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="ef8db-150">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de SCC LifeCycle ofrecida por SCC LifeCycle para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="ef8db-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="ef8db-151">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="ef8db-151">Assign users</span></span>
<span data-ttu-id="ef8db-152">Para probar la configuración, debe conceder acceso a los usuarios de Azure AD a los que quiere permitir el uso de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef8db-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="ef8db-153">**Para asignar usuarios a SCC LifeCycle, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="ef8db-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="ef8db-154">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="ef8db-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ef8db-155">En la página de integración de aplicaciones de **SCC LifeCycle**, haga clic en **Asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ef8db-155">On the **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="ef8db-156">![Asignar usuarios](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="ef8db-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="ef8db-157">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="ef8db-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="ef8db-158">![Sí](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="ef8db-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ef8db-159">Si desea probar la configuración de inicio de sesión único (SSO), abra el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ef8db-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="ef8db-160">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef8db-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

