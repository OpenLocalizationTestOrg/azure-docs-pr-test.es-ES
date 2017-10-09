---
title: "Tutorial: integración de Azure Active Directory con TOPdesk - Secure | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse TOPdesk - Secure con Azure Active Directory tooenable inicio de sesión único, aprovisionamiento automático y mucho más!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="d76ba-103">Tutorial: integración de Azure Active Directory con TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="d76ba-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="d76ba-104">objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="d76ba-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="d76ba-105">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d76ba-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="d76ba-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="d76ba-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d76ba-107">Una suscripción habilitada para el inicio de sesión único en TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="d76ba-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="d76ba-108">Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooTOPdesk - will segura puede toosingle capaz de inicio de sesión en la aplicación hello en TOPdesk - sitio de la compañía seguros (servicio iniciado por el proveedor inicio de sesión), o mediante hello [Introducción Panel de acceso de toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d76ba-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="d76ba-109">escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d76ba-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="d76ba-110">Habilitar la integración de aplicación Hola para TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="d76ba-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="d76ba-111">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d76ba-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="d76ba-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="d76ba-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="d76ba-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="d76ba-113">Assigning users</span></span>

<span data-ttu-id="d76ba-114">![Escenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="d76ba-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="d76ba-115">Habilitar la integración de aplicación Hola para TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="d76ba-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="d76ba-116">objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="d76ba-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="d76ba-117">integración de aplicaciones de hello tooenable para TOPdesk - Secure, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d76ba-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="d76ba-118">Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="d76ba-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d76ba-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="d76ba-120">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="d76ba-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="d76ba-121">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="d76ba-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="d76ba-122">![Aplicaciones](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="d76ba-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="d76ba-123">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="d76ba-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="d76ba-124">![Agregar aplicaciones](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="d76ba-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="d76ba-125">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="d76ba-126">![Agregar una aplicación de la galería](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="d76ba-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="d76ba-127">Hola **cuadro de búsqueda**, tipo **TOPdesk - Secure**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="d76ba-128">![Galería de aplicaciones](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="d76ba-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="d76ba-129">En el panel de resultados de hello, seleccione **TOPdesk - Secure**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d76ba-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="d76ba-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="d76ba-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="d76ba-131">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d76ba-131">Configuring single sign-on</span></span>
<span data-ttu-id="d76ba-132">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooTOPdesk - Secure con su cuenta de Azure AD utilizando federación basada en hello protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="d76ba-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="d76ba-133">Configurar inicio de sesión único para TOPdesk - Secure requiere tooupload un archivo de icono de logotipo.</span><span class="sxs-lookup"><span data-stu-id="d76ba-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="d76ba-134">archivo de icono de hello tooget, equipo de soporte técnico de TOPdesk Hola contacto.</span><span class="sxs-lookup"><span data-stu-id="d76ba-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="d76ba-135">tooconfigure inicio de sesión único, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d76ba-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="d76ba-136">Inicio de sesión tooyour **TOPdesk - Secure** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="d76ba-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="d76ba-137">Hola **TOPdesk** menú, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="d76ba-138">![Configuración](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="d76ba-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="d76ba-139">Haga clic en **Login Settings**(Configuración de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="d76ba-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="d76ba-140">![Configuración de inicio de sesión](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configuración de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="d76ba-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="d76ba-141">Expanda hello **configuración de inicio de sesión** menú y, a continuación, haga clic en **General**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="d76ba-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="d76ba-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="d76ba-143">Hola **seguro** sección de hello **inicio de sesión SAML** configuración sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d76ba-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d76ba-144">![Configuración técnica](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Configuración técnica")</span><span class="sxs-lookup"><span data-stu-id="d76ba-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="d76ba-145">a.</span><span class="sxs-lookup"><span data-stu-id="d76ba-145">a.</span></span> <span data-ttu-id="d76ba-146">Haga clic en **descargar** toodownload Hola archivo de metadatos públicos y, a continuación, guardarlo localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d76ba-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="d76ba-147">b.</span><span class="sxs-lookup"><span data-stu-id="d76ba-147">b.</span></span> <span data-ttu-id="d76ba-148">Abra el archivo de metadatos de hello y, a continuación, busque hello **AssertionConsumerService** nodo.</span><span class="sxs-lookup"><span data-stu-id="d76ba-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="d76ba-149">![Servicio de consumidor de aserciones](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Servicio de consumidor de aserciones")</span><span class="sxs-lookup"><span data-stu-id="d76ba-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="d76ba-150">c.</span><span class="sxs-lookup"><span data-stu-id="d76ba-150">c.</span></span> <span data-ttu-id="d76ba-151">Hola copia **AssertionConsumerService** valor.</span><span class="sxs-lookup"><span data-stu-id="d76ba-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="d76ba-152">Se necesita Hola valor Hola **configurar URL de aplicación** sección más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d76ba-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="d76ba-153">En otra ventana del explorador web, inicie sesión en su **Portal de Azure clásico** como administrador.</span><span class="sxs-lookup"><span data-stu-id="d76ba-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="d76ba-154">En hello **TOPdesk - Secure** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen Hola ** configurar inicio de sesión único ** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d76ba-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="d76ba-155">![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d76ba-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="d76ba-156">En hello **¿cómo quiere como usuarios toosign en tooTOPdesk - Secure** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="d76ba-157">![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d76ba-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="d76ba-158">En hello **configurar URL de aplicación** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d76ba-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="d76ba-159">![Configurar dirección URL de la aplicación](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="d76ba-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="d76ba-160">a.</span><span class="sxs-lookup"><span data-stu-id="d76ba-160">a.</span></span> <span data-ttu-id="d76ba-161">Hola **TOPdesk - Secure URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por su toosign a los usuarios en la aplicación TOPdesk - Secure (p. ej.: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="d76ba-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="d76ba-162">b.</span><span class="sxs-lookup"><span data-stu-id="d76ba-162">b.</span></span> <span data-ttu-id="d76ba-163">Hola **TOPdesk – Public Reply URL** cuadro de texto, pegue hello **TOPdesk - Secure AssertionConsumerService URL** (p. ej.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="d76ba-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="d76ba-164">c.</span><span class="sxs-lookup"><span data-stu-id="d76ba-164">c.</span></span> <span data-ttu-id="d76ba-165">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-165">Click **Next**.</span></span>

10. <span data-ttu-id="d76ba-166">En hello **configurar inicio de sesión único en TOPdesk - Secure** page, toodownload el archivo de metadatos, haga clic en **descargar metadatos**y, a continuación, guardar archivo hello localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d76ba-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="d76ba-167">![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d76ba-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="d76ba-168">toocreate un archivo de certificado, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d76ba-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="d76ba-169">![Certificado](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificado")</span><span class="sxs-lookup"><span data-stu-id="d76ba-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="d76ba-170">a.</span><span class="sxs-lookup"><span data-stu-id="d76ba-170">a.</span></span> <span data-ttu-id="d76ba-171">Archivo de metadatos descargado Hola abierto.</span><span class="sxs-lookup"><span data-stu-id="d76ba-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="d76ba-172">b.</span><span class="sxs-lookup"><span data-stu-id="d76ba-172">b.</span></span> <span data-ttu-id="d76ba-173">Expanda hello **RoleDescriptor** nodo que tenga un **xsi: Type** de **fed: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="d76ba-174">c.</span><span class="sxs-lookup"><span data-stu-id="d76ba-174">c.</span></span> <span data-ttu-id="d76ba-175">Copiar valor de Hola de hello **X509Certificate** nodo.</span><span class="sxs-lookup"><span data-stu-id="d76ba-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="d76ba-176">d.</span><span class="sxs-lookup"><span data-stu-id="d76ba-176">d.</span></span> <span data-ttu-id="d76ba-177">Hola Guardar copia **X509Certificate** valor localmente en el equipo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="d76ba-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="d76ba-178">En TOPdesk - Secure sitio de la empresa, en hello **TOPdesk** menú, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="d76ba-179">![Configuración](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="d76ba-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="d76ba-180">Haga clic en **Login Settings**(Configuración de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="d76ba-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="d76ba-181">![Configuración de inicio de sesión](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configuración de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="d76ba-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="d76ba-182">Expanda hello **configuración de inicio de sesión** menú y, a continuación, haga clic en **General**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="d76ba-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="d76ba-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="d76ba-184">Hola **público** sección, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="d76ba-185">![Agregar](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="d76ba-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="d76ba-186">En hello **Asistente de configuración de SAML** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d76ba-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="d76ba-187">![Asistente para configuración de SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Asistente de configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="d76ba-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="d76ba-188">a.</span><span class="sxs-lookup"><span data-stu-id="d76ba-188">a.</span></span> <span data-ttu-id="d76ba-189">tooupload en los metadatos descargados archivo **metadatos de federación**, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="d76ba-190">b.</span><span class="sxs-lookup"><span data-stu-id="d76ba-190">b.</span></span> <span data-ttu-id="d76ba-191">tooupload archivo su certificado, en **certificado (RSA)**, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="d76ba-192">c.</span><span class="sxs-lookup"><span data-stu-id="d76ba-192">c.</span></span> <span data-ttu-id="d76ba-193">que se obtuvo al equipo de soporte técnico de TOPdesk hello, en el archivo de logotipo de hello tooupload **icono del logotipo de**, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="d76ba-194">d.</span><span class="sxs-lookup"><span data-stu-id="d76ba-194">d.</span></span> <span data-ttu-id="d76ba-195">Hola **atributo de nombre de usuario** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="d76ba-196">e.</span><span class="sxs-lookup"><span data-stu-id="d76ba-196">e.</span></span> <span data-ttu-id="d76ba-197">Hola **nombre para mostrar** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="d76ba-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="d76ba-198">f.</span><span class="sxs-lookup"><span data-stu-id="d76ba-198">f.</span></span> <span data-ttu-id="d76ba-199">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-199">Click **Save**.</span></span>

17. <span data-ttu-id="d76ba-200">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d76ba-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="d76ba-201">![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d76ba-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="d76ba-202">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="d76ba-202">Configuring user provisioning</span></span>
<span data-ttu-id="d76ba-203">En orden tooenable Azure AD a los usuarios toolog en TOPdesk - Secure, debe aprovisionar en TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="d76ba-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="d76ba-204">En caso de hello de TOPdesk - Secure, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d76ba-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="d76ba-205">tooconfigure aprovisionamiento de usuario, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d76ba-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="d76ba-206">Inicio de sesión tooyour **TOPdesk - Secure** como administrador.</span><span class="sxs-lookup"><span data-stu-id="d76ba-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="d76ba-207">En el menú de hello en la parte superior de hello, haga clic en **TOPdesk \> New \> archivos auxiliares \> operador**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="d76ba-208">![Operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operador")</span><span class="sxs-lookup"><span data-stu-id="d76ba-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="d76ba-209">En hello **New (operador)** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d76ba-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="d76ba-210">![New operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "Nuevo operador")</span><span class="sxs-lookup"><span data-stu-id="d76ba-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="d76ba-211">a.</span><span class="sxs-lookup"><span data-stu-id="d76ba-211">a.</span></span> <span data-ttu-id="d76ba-212">Haga clic en la ficha General de Hola.</span><span class="sxs-lookup"><span data-stu-id="d76ba-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="d76ba-213">b.</span><span class="sxs-lookup"><span data-stu-id="d76ba-213">b.</span></span> <span data-ttu-id="d76ba-214">Hola **apellido** cuadro de texto de hello **General** sección, escriba Hola apellidos de una cuenta válida de Azure Active Directory que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="d76ba-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="d76ba-215">c.</span><span class="sxs-lookup"><span data-stu-id="d76ba-215">c.</span></span> <span data-ttu-id="d76ba-216">Seleccione un **sitio** de cuenta de hello en hello **ubicación** sección.</span><span class="sxs-lookup"><span data-stu-id="d76ba-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="d76ba-217">d.</span><span class="sxs-lookup"><span data-stu-id="d76ba-217">d.</span></span> <span data-ttu-id="d76ba-218">Hola **nombre de inicio de sesión** cuadro de texto de hello **inicio de sesión de TOPdesk** sección, escriba un nombre de inicio de sesión para el usuario.</span><span class="sxs-lookup"><span data-stu-id="d76ba-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="d76ba-219">e.</span><span class="sxs-lookup"><span data-stu-id="d76ba-219">e.</span></span> <span data-ttu-id="d76ba-220">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d76ba-221">Puede usar cualquier otra TOPdesk - cuenta de usuario segura herramientas de creación o las API proporcionadas por TOPdesk - Secure tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="d76ba-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="d76ba-222">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="d76ba-222">Assigning users</span></span>
<span data-ttu-id="d76ba-223">tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.</span><span class="sxs-lookup"><span data-stu-id="d76ba-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="d76ba-224">tooassign usuarios tooTOPdesk - Secure, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d76ba-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="d76ba-225">Hola portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="d76ba-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d76ba-226">En Hola ** TOPdesk - Secure ** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d76ba-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="d76ba-227">![Asignar usuarios](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="d76ba-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="d76ba-228">Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.</span><span class="sxs-lookup"><span data-stu-id="d76ba-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="d76ba-229">![Sí](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="d76ba-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d76ba-230">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d76ba-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="d76ba-231">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d76ba-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

