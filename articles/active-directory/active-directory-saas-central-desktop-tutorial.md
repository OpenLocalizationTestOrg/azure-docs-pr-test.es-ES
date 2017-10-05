---
title: "Tutorial: Integración de Azure Active Directory con Central Desktop | Microsoft Docs"
description: "Aprenda cómo usar Central Desktop con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
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
ms.openlocfilehash: fe32c1d68040ceb9d9de2ad6c4a6dc9ea93f5aef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="1e7b7-103">Tutorial: integración de Azure Active Directory con Central Desktop</span><span class="sxs-lookup"><span data-stu-id="1e7b7-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="1e7b7-104">El objetivo de este tutorial es mostrar la integración de Azure y Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="1e7b7-105">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e7b7-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="1e7b7-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="1e7b7-106">A valid Azure subscription</span></span>
* <span data-ttu-id="1e7b7-107">Una suscripción de Central Desktop con inicio de sesión único habilitado / Inquilino de Central Desktop</span><span class="sxs-lookup"><span data-stu-id="1e7b7-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="1e7b7-108">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1e7b7-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="1e7b7-109">Habilitación de la integración de aplicaciones para Central Desktop</span><span class="sxs-lookup"><span data-stu-id="1e7b7-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="1e7b7-110">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="1e7b7-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="1e7b7-111">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="1e7b7-111">Configuring user provisioning</span></span>
* <span data-ttu-id="1e7b7-112">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="1e7b7-112">Assigning users</span></span>

<span data-ttu-id="1e7b7-113">![Escenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="1e7b7-114">Habilitación de la integración de aplicaciones para Central Desktop</span><span class="sxs-lookup"><span data-stu-id="1e7b7-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="1e7b7-115">El objetivo de esta sección es describir cómo habilitar la integración de las aplicaciones para Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="1e7b7-116">**Siga estos pasos para habilitar la integración de aplicaciones para Central Desktop:**</span><span class="sxs-lookup"><span data-stu-id="1e7b7-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7b7-117">En el panel de navegación izquierdo del Portal de Azure clásico, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="1e7b7-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="1e7b7-119">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1e7b7-120">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="1e7b7-121">![Aplicaciones](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="1e7b7-122">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="1e7b7-123">![Agregar aplicaciones](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="1e7b7-124">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="1e7b7-125">![Agregar una aplicación de la galería](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="1e7b7-126">En el **cuadro de búsqueda**, escriba **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="1e7b7-127">![Galería de aplicaciones](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="1e7b7-128">En el panel de resultados, seleccione **Central Desktop** y, luego, haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="1e7b7-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="1e7b7-130">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="1e7b7-130">Configure single sign-on</span></span>

<span data-ttu-id="1e7b7-131">El objetivo de esta sección es describir cómo habilitar usuarios para que se autentiquen en Central Desktop con su cuenta de Azure AD mediante federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="1e7b7-132">Como parte de este procedimiento, se requiere cargar un certificado codificado en base 64 en el inquilino de Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="1e7b7-133">Si no está familiarizado con este procedimiento, consulte [Conversión de un certificado binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="1e7b7-134">**Siga estos pasos para configurar el inicio de sesión único:**</span><span class="sxs-lookup"><span data-stu-id="1e7b7-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7b7-135">En el portal de Azure clásico, en la **Central Desktop** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** para abrir el ** configurar inicio de sesión único ** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="1e7b7-136">![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="1e7b7-137">En la página **¿Cómo desea que los usuarios inicien sesión en Central Desktop?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="1e7b7-138">![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="1e7b7-139">En la página **Configurar dirección URL de la aplicación**, realice los pasos siguientes y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="1e7b7-140">En el cuadro de texto **URL de inicio de sesión de Central Desktop**, escriba la dirección URL de su inquilino de Central Desktop (por ejemplo, *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="1e7b7-141">En el cuadro de texto dirección URL de respuesta de Central Desktop, escriba la dirección URL de AssertionConsumerService de Central Desktop (por ejemplo, https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1e7b7-142">Puede obtener el valor de los metadatos de Central Desktop (por ejemplo, *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="1e7b7-143">![Configurar dirección URL de la aplicación](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="1e7b7-144">En la página **Configuración de inicio de sesión único en Central Desktop**, para descargar el certificado, haga clic en **Descargar certificado** y luego guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="1e7b7-145">![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="1e7b7-146">Inicie sesión en su inquilino de **Central Desktop** .</span><span class="sxs-lookup"><span data-stu-id="1e7b7-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="1e7b7-147">Vaya a **Configuración**, haga clic en **Avanzadas** y, luego en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="1e7b7-148">![Programa de instalación: avanzado](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Programa de instalación: avanzado")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="1e7b7-149">En la página **Configuración de inicio de sesión único** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1e7b7-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="1e7b7-150">![Configuración de inicio de sesión único ](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="1e7b7-151">Seleccione **Enable SAML v2 Single Sign On**(Habilitar inicio de sesión único de SAML).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="1e7b7-152">En el Portal de Azure clásico, en la página **Configurar inicio de sesión único en Central Desktop**, copie el valor de **Dirección URL de emisor** y péguelo en el cuadro de texto **Dirección URL de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="1e7b7-153">En el Portal de Azure clásico, en la página **Configurar inicio de sesión único en Central Desktop**, copie el valor de **Dirección URL de inicio de sesión remoto** y péguelo en el cuadro de texto **Dirección URL de inicio de sesión SSO**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="1e7b7-154">En el Portal de Azure clásico, en la página **Configurar inicio de sesión único en Central Desktop**, copie el valor de **Dirección URL del servicio de cierre de sesión único** y péguelo en el cuadro de texto **Dirección URL de cierre de sesión SSO**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="1e7b7-155">En la sección **Método de autenticación de firma de mensaje** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e7b7-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="1e7b7-156">![Método de autenticación de firma de mensaje](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Método de autenticación de firma de mensaje")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="1e7b7-157">Seleccione **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="1e7b7-158">En la lista **Certificado SSO**, seleccione **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="1e7b7-159">Cree un archivo de texto a partir del certificado descargado, copie el contenido del archivo de texto y, a continuación, péguelo en el campo **SSO Certificate** (certificado SSO).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="1e7b7-160">Para obtener más información, consulte [Conversión de un certificado binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="1e7b7-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="1e7b7-161">Seleccione **Mostrar un vínculo a la página de inicio de sesión SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="1e7b7-162">Haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-162">Click **Update**.</span></span>
10. <span data-ttu-id="1e7b7-163">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="1e7b7-164">![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="1e7b7-165">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="1e7b7-165">Configure user provisioning</span></span>

<span data-ttu-id="1e7b7-166">Para que los usuarios de AAD puedan iniciar sesión, deben aprovisionarse a Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="1e7b7-167">En esta sección se describe cómo crear cuentas de usuario de AAD en Central Desktop .</span><span class="sxs-lookup"><span data-stu-id="1e7b7-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="1e7b7-168">**Para el aprovisionamiento de cuentas de usuario a Central Desktop:**</span><span class="sxs-lookup"><span data-stu-id="1e7b7-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="1e7b7-169">Inicie sesión en su inquilino de Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="1e7b7-170">Vaya a **Contactos \> Miembros internos**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="1e7b7-171">Haga clic en **Agregar miembros internos**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="1e7b7-172">![Personas](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="1e7b7-173">En el cuadro de texto **Dirección de correo electrónico de nuevos miembros**, escriba una cuenta AAD que quiera aprovisionar y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="1e7b7-174">![Direcciones de correo electrónico de los nuevos miembros](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Direcciones de correo electrónico de los nuevos miembros")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="1e7b7-175">Haga clic en **Agregar miembros internos**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="1e7b7-176">![Agregar miembros internos](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Agregar miembros internos")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1e7b7-177">Los usuarios que ha agregado recibirán un correo electrónico que incluye un vínculo de confirmación en el que tienen que hacer clic para activar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="1e7b7-178">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Central Desktop ofrecida por Central Desktop para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="1e7b7-179">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="1e7b7-179">Assign users</span></span>
<span data-ttu-id="1e7b7-180">Para probar la configuración, debe conceder acceso a los usuarios de Azure AD a los que quiere permitir el uso de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="1e7b7-181">**Para asignar usuarios a Central Desktop, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="1e7b7-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7b7-182">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="1e7b7-183">En la página de integración de aplicaciones de **Central Desktop**, haga clic en **Asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="1e7b7-184">![Asignar usuarios](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="1e7b7-185">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="1e7b7-186">![Sí](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="1e7b7-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1e7b7-187">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1e7b7-188">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

