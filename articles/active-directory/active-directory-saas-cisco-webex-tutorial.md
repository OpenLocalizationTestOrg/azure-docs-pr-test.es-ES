---
title: "Tutorial: Integración de Azure Active Directory con Cisco Webex | Microsoft Azure"
description: "Aprenda a usar Cisco Webex con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
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
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="ca891-103">Tutorial: integración de Azure Active Directory con Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="ca891-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="ca891-104">El objetivo de este tutorial es mostrar la integración de Azure y Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="ca891-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="ca891-105">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ca891-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="ca891-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="ca891-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ca891-107">Un inquilino de Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="ca891-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="ca891-108">Después de completar este tutorial, los usuarios de Azure AD que ha asignado a Cisco Webex podrán realizar un inicio de sesión único en la aplicación en el sitio de la compañía de Cisco Webex (inicio de sesión iniciado por el proveedor de servicios) o con la [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca891-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="ca891-109">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ca891-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="ca891-110">Habilitación de la integración de aplicaciones para Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="ca891-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="ca891-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="ca891-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="ca891-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="ca891-112">Configuring user provisioning</span></span>
* <span data-ttu-id="ca891-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="ca891-113">Assigning users</span></span>

<span data-ttu-id="ca891-114">![Escenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="ca891-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="ca891-115">Habilitación de la integración de aplicaciones para Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="ca891-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="ca891-116">El objetivo de esta sección es describir cómo se habilita la integración de aplicaciones para Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="ca891-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="ca891-117">**Siga estos pasos para habilitar la integración de aplicaciones para Cisco Webex:**</span><span class="sxs-lookup"><span data-stu-id="ca891-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="ca891-118">En el panel de navegación izquierdo del Portal de Azure clásico, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ca891-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="ca891-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ca891-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="ca891-120">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="ca891-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ca891-121">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="ca891-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="ca891-122">![Aplicaciones](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="ca891-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ca891-123">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="ca891-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="ca891-124">![Agregar aplicaciones](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="ca891-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ca891-125">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="ca891-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="ca891-126">![Agregar una aplicación de la galería](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="ca891-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ca891-127">En el **cuadro de búsqueda**, escriba **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="ca891-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="ca891-128">![Galería de aplicaciones](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="ca891-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="ca891-129">En el panel de resultados, seleccione **Cisco Webex** y, a continuación, haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ca891-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="ca891-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="ca891-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="ca891-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ca891-131">Configure single sign-on</span></span>

<span data-ttu-id="ca891-132">El objetivo de esta sección es describir cómo habilitar usuarios para que se autentiquen en Cisco Webex con su cuenta de Azure AD mediante federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="ca891-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="ca891-133">Como parte de este procedimiento, es necesario crear un certificado codificado en base 64.</span><span class="sxs-lookup"><span data-stu-id="ca891-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="ca891-134">Si no está familiarizado con este procedimiento, consulte [Conversión de un certificado binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="ca891-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="ca891-135">**Siga estos pasos para configurar el inicio de sesión único:**</span><span class="sxs-lookup"><span data-stu-id="ca891-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="ca891-136">En el Portal de Azure clásico, en la página de integración de aplicaciones de **Cisco Webex**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ca891-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="ca891-137">![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ca891-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="ca891-138">En la página **How would you like users to sign on to Cisco Webex** (¿Cómo desea que los usuarios inicien sesión en Cisco Webex?), seleccione **Inicio de sesión único de Microsoft Azure AD** y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ca891-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="ca891-139">![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ca891-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="ca891-140">En la página **Configurar dirección URL de la aplicación**, realice los pasos siguientes y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ca891-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="ca891-141">![Configurar dirección URL de la aplicación](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="ca891-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="ca891-142">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL de inquilino de Cisco Webex (p. ej.: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="ca891-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="ca891-143">En el cuadro de texto **URL de respuesta de Cisco Webex**, escriba su **dirección URL de Cisco Webex AssertionConsumerService** (por ejemplo: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span><span class="sxs-lookup"><span data-stu-id="ca891-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="ca891-144">En la página **Configurar inicio de sesión único en Cisco Webex**, para descargar el certificado, haga clic en **Descargar certificado** y luego guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ca891-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="ca891-145">![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ca891-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="ca891-146">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="ca891-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="ca891-147">En el menú de la parte superior, haga clic en **Site Administration**(Administración de sitio).</span><span class="sxs-lookup"><span data-stu-id="ca891-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="ca891-148">![Administración de sitios](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Administración de sitios")</span><span class="sxs-lookup"><span data-stu-id="ca891-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="ca891-149">En la sección **Manage Site** (Administrar sitio), haga clic en **SSO Configuration** (Configuración de SSO).</span><span class="sxs-lookup"><span data-stu-id="ca891-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="ca891-150">![Configuración de SSO](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "Configuración de SSO")</span><span class="sxs-lookup"><span data-stu-id="ca891-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="ca891-151">En la sección Federated Web SSO Configuration (configuración de SSO web federado), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ca891-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="ca891-152">![Configuración de SSO federado](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Configuración de SSO federado")</span><span class="sxs-lookup"><span data-stu-id="ca891-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="ca891-153">En la lista de **protocolos de federación**, seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ca891-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="ca891-154">Cree un archivo **codificado en base 64** a partir del certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="ca891-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="ca891-155">Para obtener más información, consulte [Conversión de un certificado binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="ca891-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="ca891-156">Abra el certificado codificado en base 64 en el Bloc de notas y luego copie el contenido del mismo.</span><span class="sxs-lookup"><span data-stu-id="ca891-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="ca891-157">Haga clic en **Import SAML Metadata**(Importar metadatos de SAML) y, a continuación, pegue el certificado codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="ca891-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="ca891-158">En el Portal de Azure clásico, en la página del cuadro de diálogo **Configurar inicio de sesión único en Cisco Webex**, copie el valor de **URL del emisor** y péguelo en el cuadro de texto **Issuer for SAML (IdP ID)** (Emisor para SAML [Id. de IdP]).</span><span class="sxs-lookup"><span data-stu-id="ca891-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="ca891-159">En el Portal de Azure clásico, en la página del cuadro de diálogo **Configurar inicio de sesión único en Cisco Webex**, copie el valor de **Dirección URL de inicio de sesión remoto** y péguelo en el cuadro de texto **Customer SSO Service Login URL** (URL de inicio de sesión de servicio SSO del cliente).</span><span class="sxs-lookup"><span data-stu-id="ca891-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="ca891-160">En la lista **NameID Format** (Formato de NameID), seleccione **Email address** (Dirección de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="ca891-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="ca891-161">En el cuadro de texto **AuthnContextClassRef**, escriba **urn: oasis: nombres: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="ca891-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="ca891-162">En el Portal de Azure clásico, en la página del cuadro de diálogo **Configurar inicio de sesión único en Cisco Webex**, copie el valor de **Dirección URL de cierre de sesión remoto** y péguelo en el cuadro de texto **Customer SSO Service Logout URL** (URL de cierre de sesión de servicio SSO del cliente).</span><span class="sxs-lookup"><span data-stu-id="ca891-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="ca891-163">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="ca891-163">Click **Update**.</span></span>
9. <span data-ttu-id="ca891-164">En el Portal de Azure clásico, en la página del cuadro de diálogo **Configurar inicio de sesión único en Cisco Webex**, seleccione la confirmación de configuración de inicio de sesión único y luego haga clic en **Completa**.</span><span class="sxs-lookup"><span data-stu-id="ca891-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="ca891-165">![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ca891-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="ca891-166">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="ca891-166">Configure user provisioning</span></span>

<span data-ttu-id="ca891-167">Para permitir que los usuarios de Azure AD inicien sesión en Cisco Webex, tienen que aprovisionarse en Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="ca891-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="ca891-168">En el caso de Cisco Webex, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="ca891-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="ca891-169">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="ca891-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="ca891-170">Inicie sesión en su inquilino de **Cisco Webex** .</span><span class="sxs-lookup"><span data-stu-id="ca891-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="ca891-171">Vaya a **Manage Users (Administrar usuarios) \> Add User** (Agregar usuario).</span><span class="sxs-lookup"><span data-stu-id="ca891-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="ca891-172">![Agregar usuarios](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Agregar usuarios")</span><span class="sxs-lookup"><span data-stu-id="ca891-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="ca891-173">En la sección Add User (agregar usuario), realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ca891-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="ca891-174">![Agregar usuario](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="ca891-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="ca891-175">En **Account Type** (Tipo de cuenta) seleccione **Host**.</span><span class="sxs-lookup"><span data-stu-id="ca891-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="ca891-176">Escriba la información de un usuario existente de Azure AD en los cuadros de texto siguientes: **First name, Last name** (Nombre, Apellido), **User name** (Nombre de usuario), **Email** (Correo electrónico), **Password** (Contraseña), **Confirm Password** (Confirmar contraseña).</span><span class="sxs-lookup"><span data-stu-id="ca891-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="ca891-177">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ca891-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="ca891-178">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Cisco Webex ofrecida por Cisco Webex para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="ca891-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="ca891-179">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="ca891-179">Assign users</span></span>
<span data-ttu-id="ca891-180">Para probar la configuración, debe conceder acceso a los usuarios de Azure AD a los que quiere permitir el uso de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="ca891-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="ca891-181">**Para asignar usuarios a Cisco Webex, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="ca891-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="ca891-182">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="ca891-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ca891-183">En la página de integración de la aplicación **Cisco Webex**, haga clic en **Asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ca891-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="ca891-184">![Asignar usuarios](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="ca891-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="ca891-185">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="ca891-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="ca891-186">![Sí](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="ca891-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ca891-187">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ca891-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ca891-188">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca891-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

