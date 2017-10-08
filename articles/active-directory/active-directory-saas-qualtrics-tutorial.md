---
title: "Tutorial: integración de Azure Active Directory con Qualtrics | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Qualtrics con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
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
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="89507-103">Tutorial: Integración de Azure Active Directory con Qualtrics</span><span class="sxs-lookup"><span data-stu-id="89507-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="89507-104">objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="89507-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="89507-105">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="89507-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="89507-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="89507-106">A valid Azure subscription</span></span>
* <span data-ttu-id="89507-107">Una suscripción habilitada para el inicio de sesión único (SSO) en Qualtrics</span><span class="sxs-lookup"><span data-stu-id="89507-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="89507-108">Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooQualtrics será toosingle capaz de inicio de sesión en la aplicación hello en el sitio de empresa de Qualtrics (servicio iniciado por el proveedor inicio de sesión), o mediante hello [toohello de introducción Obtener acceso al Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89507-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="89507-109">escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="89507-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="89507-110">Habilitar la integración de aplicación Hola para Qualtrics</span><span class="sxs-lookup"><span data-stu-id="89507-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="89507-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="89507-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="89507-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="89507-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="89507-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="89507-113">Assigning users</span></span>

<span data-ttu-id="89507-114">![Escenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="89507-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="89507-115">Habilitar la integración de aplicación Hola para Qualtrics</span><span class="sxs-lookup"><span data-stu-id="89507-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="89507-116">objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="89507-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="89507-117">**integración de aplicaciones de hello tooenable para Qualtrics, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="89507-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="89507-118">Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89507-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="89507-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="89507-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="89507-120">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="89507-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="89507-121">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="89507-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="89507-122">![Aplicaciones](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="89507-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="89507-123">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="89507-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="89507-124">![Agregar aplicaciones](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="89507-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="89507-125">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="89507-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="89507-126">![Agregar una aplicación de la galería](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="89507-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="89507-127">Hola **cuadro de búsqueda**, tipo **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="89507-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="89507-128">![Galería de aplicaciones](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="89507-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="89507-129">En el panel de resultados de hello, seleccione **Qualtrics**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="89507-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="89507-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="89507-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="89507-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="89507-131">Configure single sign-on</span></span>

<span data-ttu-id="89507-132">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooQualtrics con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="89507-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="89507-133">**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="89507-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="89507-134">En el portal de Azure clásico en Hola Hola **Qualtrics** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89507-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="89507-135">![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="89507-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="89507-136">En hello **¿cómo desea que los usuarios toosign en tooQualtrics** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="89507-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="89507-137">![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="89507-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="89507-138">En hello **configurar URL de aplicación** página Hola **Qualtrics inicio de sesión en la URL** cuadro de texto, escriba la dirección URL (p. ej.: "*https://ssotest2ut1.qualtrics.com*") y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="89507-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="89507-139">![Configurar dirección URL de la aplicación](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="89507-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="89507-140">En hello **configurar inicio de sesión único en Qualtrics** página, haga clic en **descargar metadatos**y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="89507-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="89507-141">![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="89507-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="89507-142">Enviar Hola metadatos archivo toohello equipo de soporte técnico de Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="89507-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="89507-143">configuración de SSO de Hello tiene toobe realizada por el equipo de soporte técnico de Qualtrics Hola.</span><span class="sxs-lookup"><span data-stu-id="89507-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="89507-144">Recibirá una notificación en cuanto se ha completado la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="89507-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="89507-145">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89507-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="89507-146">![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="89507-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="89507-147">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="89507-147">Configure user provisioning</span></span>

<span data-ttu-id="89507-148">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooQualtrics.</span><span class="sxs-lookup"><span data-stu-id="89507-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="89507-149">Cuando un usuario asignado intenta toolog en Qualtrics a través de panel de acceso de hello, Qualtrics comprueba si existe el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="89507-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="89507-150">Si no hay cuentas de usuario disponibles, Qualtrics crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="89507-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="89507-151">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="89507-151">Assign users</span></span>
<span data-ttu-id="89507-152">tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.</span><span class="sxs-lookup"><span data-stu-id="89507-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="89507-153">**tooassign tooQualtrics de los usuarios, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="89507-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="89507-154">Hola portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="89507-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="89507-155">En hello **Qualtrics** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="89507-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="89507-156">![Asignar usuarios](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="89507-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="89507-157">Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.</span><span class="sxs-lookup"><span data-stu-id="89507-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="89507-158">![Sí](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="89507-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="89507-159">Si desea tootest la configuración de SSO, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="89507-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="89507-160">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89507-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

