---
title: "Tutorial: Integración de Azure Active Directory con Central Desktop | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Central Desktop con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="98b4d-103">Tutorial: integración de Azure Active Directory con Central Desktop</span><span class="sxs-lookup"><span data-stu-id="98b4d-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="98b4d-104">objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="98b4d-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="98b4d-105">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="98b4d-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="98b4d-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="98b4d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="98b4d-107">Una suscripción de Central Desktop con inicio de sesión único habilitado / Inquilino de Central Desktop</span><span class="sxs-lookup"><span data-stu-id="98b4d-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="98b4d-108">escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="98b4d-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="98b4d-109">Habilitar la integración de aplicación Hola para Central Desktop</span><span class="sxs-lookup"><span data-stu-id="98b4d-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="98b4d-110">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="98b4d-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="98b4d-111">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="98b4d-111">Configuring user provisioning</span></span>
* <span data-ttu-id="98b4d-112">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="98b4d-112">Assigning users</span></span>

<span data-ttu-id="98b4d-113">![Escenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="98b4d-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="98b4d-114">Habilitar la integración de aplicación Hola para Central Desktop</span><span class="sxs-lookup"><span data-stu-id="98b4d-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="98b4d-115">objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="98b4d-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="98b4d-116">**integración de aplicaciones de hello tooenable para Central Desktop, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="98b4d-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="98b4d-117">Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="98b4d-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="98b4d-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="98b4d-119">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="98b4d-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="98b4d-120">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="98b4d-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="98b4d-121">![Aplicaciones](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="98b4d-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="98b4d-122">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="98b4d-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="98b4d-123">![Agregar aplicaciones](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="98b4d-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="98b4d-124">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="98b4d-125">![Agregar una aplicación de la galería](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="98b4d-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="98b4d-126">Hola **cuadro de búsqueda**, tipo **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="98b4d-127">![Galería de aplicaciones](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="98b4d-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="98b4d-128">En el panel de resultados de hello, seleccione **Central Desktop**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="98b4d-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="98b4d-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="98b4d-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="98b4d-130">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="98b4d-130">Configure single sign-on</span></span>

<span data-ttu-id="98b4d-131">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooCentral escritorio con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="98b4d-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="98b4d-132">Como parte de este procedimiento, es necesario tooupload un inquilino de Central Desktop tooyour certificado codificado en base 64.</span><span class="sxs-lookup"><span data-stu-id="98b4d-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="98b4d-133">Si no está familiarizado con este procedimiento, consulte [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="98b4d-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="98b4d-134">**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="98b4d-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="98b4d-135">En el portal de Azure clásico en Hola Hola **Central Desktop** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen Hola ** configurar inicio de sesión único ** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="98b4d-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="98b4d-136">![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="98b4d-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="98b4d-137">En hello **¿cómo desea que los usuarios toosign en tooCentral Desktop** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="98b4d-138">![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="98b4d-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="98b4d-139">En hello **configurar URL de aplicación** página realizar pasos de Hola y, a continuación, haga clic en **siguiente**:</span><span class="sxs-lookup"><span data-stu-id="98b4d-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="98b4d-140">Hola **inicio de sesión en dirección URL Central Desktop** cuadro de texto, escriba la dirección URL Hola de su inquilino de Central Desktop (p. ej.: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="98b4d-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="98b4d-141">En el cuadro de texto de dirección URL de respuesta de Central Desktop hello, escriba la dirección URL AssertionConsumerService de Central Desktop (p. ej.: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="98b4d-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="98b4d-142">Puede obtener valor de Hola desde metadatos de central desktop hello (p. ej.: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="98b4d-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="98b4d-143">![Configurar dirección URL de la aplicación](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="98b4d-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="98b4d-144">En hello **configurar inicio de sesión único en Central Desktop** page, toodownload su certificado, haga clic en **Descargar certificado**y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="98b4d-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="98b4d-145">![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="98b4d-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="98b4d-146">Inicie sesión en tooyour **Central Desktop** inquilino.</span><span class="sxs-lookup"><span data-stu-id="98b4d-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="98b4d-147">Vaya demasiado**configuración**, haga clic en **avanzadas**y, a continuación, haga clic en **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="98b4d-148">![Programa de instalación: avanzado](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Programa de instalación: avanzado")</span><span class="sxs-lookup"><span data-stu-id="98b4d-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="98b4d-149">En hello **inicio de sesión único en la configuración** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="98b4d-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="98b4d-150">![Configuración de inicio de sesión único ](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="98b4d-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="98b4d-151">Seleccione **Enable SAML v2 Single Sign On**(Habilitar inicio de sesión único de SAML).</span><span class="sxs-lookup"><span data-stu-id="98b4d-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="98b4d-152">En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Central Desktop** page, Hola copia **dirección URL del emisor** valor y, a continuación, péguelo en hello **dirección URL SSO** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="98b4d-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="98b4d-153">En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Central Desktop** page, Hola copia **dirección URL de inicio de sesión remoto** valor y, a continuación, péguelo en hello **dirección URL de inicio de sesión SSO**cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="98b4d-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="98b4d-154">En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Central Desktop** page, Hola copia **dirección URL del servicio de cierre de sesión único** valor y, a continuación, péguelo en hello **SSO Logout URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="98b4d-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="98b4d-155">Hola **método de comprobación de firmas de mensajes** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="98b4d-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="98b4d-156">![Método de autenticación de firma de mensaje](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Método de autenticación de firma de mensaje")</span><span class="sxs-lookup"><span data-stu-id="98b4d-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="98b4d-157">Seleccione **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="98b4d-158">De hello **certificado SSO** lista, seleccione **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="98b4d-159">Crear un archivo de texto del certificado de hello descargado, Hola copia contenido del archivo de texto hello y, a continuación, péguelo en hello **certificado SSO** campo.</span><span class="sxs-lookup"><span data-stu-id="98b4d-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="98b4d-160">Para obtener más información, vea [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="98b4d-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="98b4d-161">Seleccione **mostrar una página de inicio de sesión de vínculo tooyour SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="98b4d-162">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="98b4d-162">Click **Update**.</span></span>
10. <span data-ttu-id="98b4d-163">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="98b4d-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="98b4d-164">![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="98b4d-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="98b4d-165">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="98b4d-165">Configure user provisioning</span></span>

<span data-ttu-id="98b4d-166">Para AAD a los usuarios toobe puede toosign en, deben ser aprovisionado toohello aplicación Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="98b4d-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="98b4d-167">Esta sección describe cómo las cuentas de usuario AAD de toocreate en Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="98b4d-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="98b4d-168">**tooCentral de cuentas de usuario de tooprovision escritorio:**</span><span class="sxs-lookup"><span data-stu-id="98b4d-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="98b4d-169">Inicie sesión en tooyour inquilino de Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="98b4d-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="98b4d-170">Vaya demasiado**personas \> miembros internos**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="98b4d-171">Haga clic en **Agregar miembros internos**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="98b4d-172">![Personas](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="98b4d-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="98b4d-173">Hola **dirección de correo electrónico de nuevos miembros** cuadro de texto, escriba una cuenta AAD que desee tooprovision y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="98b4d-174">![Direcciones de correo electrónico de los nuevos miembros](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Direcciones de correo electrónico de los nuevos miembros")</span><span class="sxs-lookup"><span data-stu-id="98b4d-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="98b4d-175">Haga clic en **Agregar miembros internos**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="98b4d-176">![Agregar miembros internos](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Agregar miembros internos")</span><span class="sxs-lookup"><span data-stu-id="98b4d-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="98b4d-177">los usuarios de Hello que ha agregado recibirán un correo electrónico que incluye un vínculo de confirmación que necesitan cuenta de hello tooactivate tooclick.</span><span class="sxs-lookup"><span data-stu-id="98b4d-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="98b4d-178">Puede usar cualquier otra Central Desktop usuario cuenta herramienta de creación o las API proporcionadas por Central Desktop tooprovision cuentas de usuario AAD</span><span class="sxs-lookup"><span data-stu-id="98b4d-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="98b4d-179">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="98b4d-179">Assign users</span></span>
<span data-ttu-id="98b4d-180">tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.</span><span class="sxs-lookup"><span data-stu-id="98b4d-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="98b4d-181">**tooassign usuarios tooCentral escritorio, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="98b4d-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="98b4d-182">Hola portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="98b4d-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="98b4d-183">En hello **Central Desktop** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="98b4d-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="98b4d-184">![Asignar usuarios](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="98b4d-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="98b4d-185">Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.</span><span class="sxs-lookup"><span data-stu-id="98b4d-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="98b4d-186">![Sí](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="98b4d-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="98b4d-187">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="98b4d-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="98b4d-188">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="98b4d-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

