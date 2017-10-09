---
title: "Tutorial: Integración de Azure Active Directory con Cisco Webex | Microsoft Azure"
description: "¡Obtenga información acerca de cómo toouse Cisco Webex con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="820b3-103">Tutorial: integración de Azure Active Directory con Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="820b3-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="820b3-104">objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="820b3-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="820b3-105">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="820b3-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="820b3-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="820b3-106">A valid Azure subscription</span></span>
* <span data-ttu-id="820b3-107">Un inquilino de Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="820b3-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="820b3-108">Después de completar este tutorial, Hola usuarios de Azure AD que haya asignado tooCisco Webex será capaz de toosingle inicio de sesión en la aplicación hello en el sitio de la compañía de Cisco Webex (servicio iniciado por el proveedor inicio de sesión), o mediante hello [toohello de introducción Obtener acceso al Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="820b3-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="820b3-109">escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="820b3-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="820b3-110">Habilitar la integración de aplicación Hola para Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="820b3-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="820b3-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="820b3-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="820b3-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="820b3-112">Configuring user provisioning</span></span>
* <span data-ttu-id="820b3-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="820b3-113">Assigning users</span></span>

<span data-ttu-id="820b3-114">![Escenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="820b3-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="820b3-115">Habilitar la integración de aplicación Hola para Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="820b3-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="820b3-116">objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="820b3-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="820b3-117">**integración de aplicaciones de hello tooenable para Cisco Webex, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="820b3-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="820b3-118">Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="820b3-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="820b3-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="820b3-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="820b3-120">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="820b3-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="820b3-121">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="820b3-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="820b3-122">![Aplicaciones](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="820b3-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="820b3-123">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="820b3-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="820b3-124">![Agregar aplicaciones](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="820b3-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="820b3-125">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="820b3-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="820b3-126">![Agregar una aplicación de la galería](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="820b3-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="820b3-127">Hola **cuadro de búsqueda**, tipo **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="820b3-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="820b3-128">![Galería de aplicaciones](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="820b3-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="820b3-129">En el panel de resultados de hello, seleccione **Cisco Webex**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="820b3-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="820b3-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="820b3-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="820b3-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="820b3-131">Configure single sign-on</span></span>

<span data-ttu-id="820b3-132">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooCisco Webex con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="820b3-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="820b3-133">Como parte de este procedimiento, se le toocreate requiere un certificado codificado en base 64.</span><span class="sxs-lookup"><span data-stu-id="820b3-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="820b3-134">Si no está familiarizado con este procedimiento, vea [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="820b3-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="820b3-135">**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="820b3-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="820b3-136">En el portal de Azure clásico en Hola Hola **Cisco Webex** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="820b3-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="820b3-137">![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="820b3-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="820b3-138">En hello **¿cómo desea que los usuarios toosign en tooCisco Webex** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="820b3-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="820b3-139">![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="820b3-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="820b3-140">En hello **configurar URL de aplicación** página realizar pasos de Hola y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="820b3-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="820b3-141">![Configurar dirección URL de la aplicación](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="820b3-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="820b3-142">Hola **cantar URL** cuadro de texto, escriba la dirección URL de inquilino de Cisco Webex (p. ej.: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="820b3-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="820b3-143">Hola **dirección URL de respuesta de Cisco Webex** cuadro de texto, tipo de su **dirección URL de AssertionConsumerService de Cisco Webex** (p. ej.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="820b3-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="820b3-144">En hello **configurar inicio de sesión único en Cisco Webex** page, toodownload su certificado, haga clic en **Descargar certificado**y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="820b3-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="820b3-145">![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="820b3-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="820b3-146">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="820b3-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="820b3-147">En el menú de hello en la parte superior de hello, haga clic en **administración de sitios**.</span><span class="sxs-lookup"><span data-stu-id="820b3-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="820b3-148">![Administración de sitios](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Administración de sitios")</span><span class="sxs-lookup"><span data-stu-id="820b3-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="820b3-149">Hola **Administrar sitio** sección, haga clic en **configuración de SSO**.</span><span class="sxs-lookup"><span data-stu-id="820b3-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="820b3-150">![Configuración de SSO](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "Configuración de SSO")</span><span class="sxs-lookup"><span data-stu-id="820b3-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="820b3-151">En la sección de configuración de SSO Web federado hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="820b3-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="820b3-152">![Configuración de SSO federado](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Configuración de SSO federado")</span><span class="sxs-lookup"><span data-stu-id="820b3-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="820b3-153">De hello **protocolo Federation** lista, seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="820b3-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="820b3-154">Cree un archivo **codificado en base 64** a partir del certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="820b3-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="820b3-155">Para obtener más información, vea [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="820b3-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="820b3-156">Abra el certificado codificado en base 64 en el Bloc de notas y, a continuación, Hola copia contenido del mismo.</span><span class="sxs-lookup"><span data-stu-id="820b3-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="820b3-157">Haga clic en **Import SAML Metadata**(Importar metadatos de SAML) y, a continuación, pegue el certificado codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="820b3-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="820b3-158">En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Cisco Webex** página de diálogo, Hola copia **dirección URL del emisor** valor y, a continuación, péguelo en hello **emisor de SAML (Id. de IdP)** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="820b3-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="820b3-159">En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Cisco Webex** página de diálogo, Hola copia **dirección URL de inicio de sesión remoto** valor y, a continuación, péguelo en hello **inicio de sesión del servicio de SSO de cliente Dirección URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="820b3-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="820b3-160">De hello **NameID Format** lista, seleccione **dirección de correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="820b3-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="820b3-161">Hola **AuthnContextClassRef** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="820b3-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="820b3-162">En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Cisco Webex** página de diálogo, Hola copia **dirección URL de cierre de sesión remoto** valor y, a continuación, péguelo en hello **cierre de sesión del servicio de SSO de cliente Dirección URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="820b3-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="820b3-163">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="820b3-163">Click **Update**.</span></span>
9. <span data-ttu-id="820b3-164">En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Cisco Webex** página del cuadro de diálogo, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="820b3-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="820b3-165">![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="820b3-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="820b3-166">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="820b3-166">Configure user provisioning</span></span>

<span data-ttu-id="820b3-167">En orden tooenable toolog de los usuarios de Azure AD en Cisco Webex, se les deben aprovisionar en Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="820b3-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="820b3-168">En caso de hello de Cisco Webex, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="820b3-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="820b3-169">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="820b3-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="820b3-170">Inicie sesión en tooyour **Cisco Webex** inquilino.</span><span class="sxs-lookup"><span data-stu-id="820b3-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="820b3-171">Vaya demasiado**administrar usuarios \> Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="820b3-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="820b3-172">![Agregar usuarios](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Agregar usuarios")</span><span class="sxs-lookup"><span data-stu-id="820b3-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="820b3-173">En la sección Agregar usuario hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="820b3-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="820b3-174">![Agregar usuario](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="820b3-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="820b3-175">En **Account Type** (Tipo de cuenta) seleccione **Host**.</span><span class="sxs-lookup"><span data-stu-id="820b3-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="820b3-176">Escribir información de Hola de un usuario de Azure AD existente en hello siguientes cuadros de texto: **nombre, apellido**, **nombre de usuario**, **correo electrónico**, **contraseña**, **Confirmar contraseña**.</span><span class="sxs-lookup"><span data-stu-id="820b3-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="820b3-177">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="820b3-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="820b3-178">Puede usar cualquier otra Cisco Webex usuario cuenta herramienta de creación o las API proporcionadas por Cisco Webex tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="820b3-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="820b3-179">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="820b3-179">Assign users</span></span>
<span data-ttu-id="820b3-180">tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.</span><span class="sxs-lookup"><span data-stu-id="820b3-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="820b3-181">**tooassign usuarios tooCisco Webex, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="820b3-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="820b3-182">Hola portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="820b3-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="820b3-183">En hello **Cisco Webex** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="820b3-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="820b3-184">![Asignar usuarios](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="820b3-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="820b3-185">Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.</span><span class="sxs-lookup"><span data-stu-id="820b3-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="820b3-186">![Sí](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="820b3-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="820b3-187">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="820b3-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="820b3-188">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="820b3-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

