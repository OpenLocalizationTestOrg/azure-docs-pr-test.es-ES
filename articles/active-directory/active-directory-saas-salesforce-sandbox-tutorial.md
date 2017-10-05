---
title: "Tutorial: Integración de Azure Active Directory con Salesforce Sandbox | Microsoft Docs"
description: "Aprenda cómo usar Salesforce Sandbox con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="6f03a-103">Tutorial: Integración de Azure Active Directory con Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="6f03a-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="6f03a-104">El objetivo de este tutorial es mostrar la integración de Azure y Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="6f03a-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="6f03a-105">Para enviar comentarios, consulte la [página de soporte técnico de Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="6f03a-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="6f03a-106">Los espacios aislados ofrecen la capacidad de crear varias copias de su organización en entornos independientes para una variedad de propósitos, como desarrollo, pruebas y aprendizaje, sin poner en peligro los datos y las aplicaciones de la organización de producción de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="6f03a-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="6f03a-107">Para obtener más información, vea [Información general del espacio aislado](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="6f03a-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="6f03a-108">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6f03a-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="6f03a-109">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="6f03a-109">A valid Azure subscription</span></span>
* <span data-ttu-id="6f03a-110">Un espacio aislado en Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="6f03a-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="6f03a-111">Si aún no tiene un espacio aislado válido en Salesforce.com, deberá ponerse en contacto con Salesforce.</span><span class="sxs-lookup"><span data-stu-id="6f03a-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="6f03a-112">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6f03a-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="6f03a-113">Habilitación de la integración de aplicaciones para Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="6f03a-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="6f03a-114">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="6f03a-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="6f03a-115">Habilitación de su dominio</span><span class="sxs-lookup"><span data-stu-id="6f03a-115">Enabling your domain</span></span>
4. <span data-ttu-id="6f03a-116">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="6f03a-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="6f03a-117">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="6f03a-117">Assigning users</span></span>

<span data-ttu-id="6f03a-118">![Escenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="6f03a-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="6f03a-119">Habilitación de la integración de aplicaciones para Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="6f03a-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="6f03a-120">El objetivo de esta sección es describir cómo habilitar la integración de las aplicaciones para el espacio aislado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="6f03a-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="6f03a-121">**Siga estos pasos para habilitar la integración de aplicaciones para Salesforce Sandbox:**</span><span class="sxs-lookup"><span data-stu-id="6f03a-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="6f03a-122">En el panel de navegación izquierdo del Portal de Azure clásico, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="6f03a-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6f03a-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="6f03a-124">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="6f03a-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6f03a-125">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="6f03a-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="6f03a-126">![Aplicaciones](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="6f03a-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="6f03a-127">Para abrir la **Galería de aplicaciones**, haga clic en **Agregar una aplicación** y en **Agregar una aplicación que mi organización use**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="6f03a-128">![¿Qué quiere hacer? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "¿Qué quiere hacer?")</span><span class="sxs-lookup"><span data-stu-id="6f03a-128">![What do you want to do?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="6f03a-129">En el **cuadro de búsqueda**, escriba **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="6f03a-130">![Galería de aplicaciones](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="6f03a-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="6f03a-131">En el panel de resultados, seleccione **Salesforce Sandbox** y, luego, haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6f03a-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="6f03a-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="6f03a-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="6f03a-133">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="6f03a-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="6f03a-134">El objetivo de esta sección es describir cómo habilitar usuarios para que se autentiquen en Salesforce con su cuenta de Azure AD a través de la federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="6f03a-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="6f03a-135">**Siga estos pasos para configurar el inicio de sesión único:**</span><span class="sxs-lookup"><span data-stu-id="6f03a-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="6f03a-136">En el Portal de Azure clásico, en la página de integración de aplicaciones de **Salesforce Sandbox**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="6f03a-137">![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="6f03a-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="6f03a-138">En la página **¿Cómo desea que los usuarios inicien sesión en Salesforce Sandbox?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="6f03a-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="6f03a-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="6f03a-140">En la página **Configurar dirección URL de la aplicación**, en el cuadro de texto **URL de inicio de sesión**, escriba su dirección URL con el siguiente patrón `http://company.my.salesforce.com` y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="6f03a-141">![Configurar dirección URL de la aplicación](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="6f03a-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="6f03a-142">Si ya configuró un inicio de sesión único para otra instancia de Salesforce Sandbox en su directorio, también debe configurar el **Identificador** para que tenga el mismo valor que la **URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="6f03a-143">El campo **Identificador** puede encontrarse al activar la casilla **Mostrar la configuración avanzada** en la página **Configurar dirección URL de la aplicación** del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f03a-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="6f03a-144">En la página **Configurar inicio de sesión único en Salesforce Sandbox**, haga clic en **Descargar certificado** y después guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6f03a-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="6f03a-145">![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="6f03a-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="6f03a-146">En otra ventana del explorador web, inicie sesión en su sitio de la compañía del espacio aislado de Salesforce como administrador.</span><span class="sxs-lookup"><span data-stu-id="6f03a-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="6f03a-147">En el menú de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="6f03a-148">![Instalación](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="6f03a-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="6f03a-149">En el panel de navegación de la izquierda, haga clic en **Controles de seguridad** y luego haga clic en **Configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="6f03a-150">![Configuración de inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="6f03a-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="6f03a-151">En la sección Configuración del inicio de sesión único, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6f03a-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="6f03a-152">![Configuración de inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="6f03a-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="6f03a-153">Seleccione **SAML habilitado**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="6f03a-154">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-154">Click **New**.</span></span>
10. <span data-ttu-id="6f03a-155">En la sección Configuración del inicio de sesión único de SAML siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6f03a-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="6f03a-156">![Configuración de inicio de sesión único de SAML](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "Configuración de inicio de sesión único de SAML")</span><span class="sxs-lookup"><span data-stu-id="6f03a-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="6f03a-157">En el cuadro de texto Nombre, escriba el nombre de la configuración (por ejemplo, *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="6f03a-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="6f03a-158">En el Portal de Azure clásico, en la página de diálogo **Configurar inicio de sesión único en Salesforce Sandbox**, copie el valor de **URL del emisor** y péguelo en el cuadro de texto **Emisor**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="6f03a-159">En el cuadro de texto **Id. de entidad**, escriba **https://test.salesforce.com** si se trata de la primera instancia de Salesforce Sandbox que va a agregar a su directorio.</span><span class="sxs-lookup"><span data-stu-id="6f03a-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="6f03a-160">Si ya agregó una instancia de Salesforce Sandbox, para el **Id. de entidad** escriba la **URL de inicio de sesión**, que debe tener este formato: `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="6f03a-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="6f03a-161">Haga clic en **Examinar** para cargar el certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="6f03a-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="6f03a-162">Como **SAML Identity Type** (Tipo de identidad SAML), seleccione **Assertion contains the Federation ID from the User object** (La aserción contiene el id. de federación del objeto Usuario).</span><span class="sxs-lookup"><span data-stu-id="6f03a-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="6f03a-163">Como **SAML Identity Location**(Ubicación de identidad de SAML), seleccione **Identity is in the NameIdentifier element of the Subject statement** (La identidad está en el elemento NameIdentifier de la instrucción de sujeto).</span><span class="sxs-lookup"><span data-stu-id="6f03a-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="6f03a-164">En el Portal de Azure clásico, en la página de diálogo **Configurar inicio de sesión único en Salesforce Sandbox**, copie el valor de **URL de inicio de sesión remoto** y péguelo en el cuadro de texto **Identity Provider Login URL** (Dirección URL de inicio de sesión de proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="6f03a-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="6f03a-165">SFDC no admite el cierre de sesión SAML.</span><span class="sxs-lookup"><span data-stu-id="6f03a-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="6f03a-166">Como alternativa, pegue 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' en el cuadro de texto **Identity Provider Logout URL** (Dirección URL de cierre de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="6f03a-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="6f03a-167">Para **Service Provider Initiated Request Binding** (Enlace de solicitud iniciada por el proveedor de servicio), seleccione **HTTP POST** (Método HTTP POST).</span><span class="sxs-lookup"><span data-stu-id="6f03a-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="6f03a-168">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-168">Click **Save**.</span></span>
11. <span data-ttu-id="6f03a-169">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="6f03a-170">![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="6f03a-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="6f03a-171">Habilitación del dominio</span><span class="sxs-lookup"><span data-stu-id="6f03a-171">Enable your domain</span></span>
<span data-ttu-id="6f03a-172">En esta sección se supone que ya ha creado un dominio.</span><span class="sxs-lookup"><span data-stu-id="6f03a-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="6f03a-173">Para obtener más información, vea [Definición de su nombre de dominio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="6f03a-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="6f03a-174">**Realice los pasos siguientes para habilitar su dominio:**</span><span class="sxs-lookup"><span data-stu-id="6f03a-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="6f03a-175">En el panel de navegación de la izquierda, haga clic en **Administración de dominios** y, luego, en **Mi dominio**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="6f03a-176">![Mi dominio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="6f03a-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="6f03a-177">Asegúrese de que su dominio se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="6f03a-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="6f03a-178">En la sección **Configuración de la página de inicio de sesión**, haga clic en**Editar**, luego, como **Servicio de autenticación**, seleccione el nombre de la configuración de inicio de sesión único de SAML en la sección anterior y finalmente haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="6f03a-179">![Mi dominio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="6f03a-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="6f03a-180">Tan pronto como tenga un dominio configurado, los usuarios deberán usar la dirección URL de dominio para iniciar sesión en el espacio aislado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="6f03a-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="6f03a-181">Para obtener el valor de la dirección URL, haga clic en el perfil de SSO que haya creado en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="6f03a-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="6f03a-182">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="6f03a-182">Configure user provisioning</span></span>
<span data-ttu-id="6f03a-183">El objetivo de esta sección es describir cómo habilitar el aprovisionamiento de cuentas de usuario de Active Directory para Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="6f03a-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="6f03a-184">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="6f03a-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="6f03a-185">En el portal de Salesforce, en la barra de navegación superior, seleccione el nombre para expandir su menú de usuario:</span><span class="sxs-lookup"><span data-stu-id="6f03a-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="6f03a-186">![Mi configuración](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Mi configuración")</span><span class="sxs-lookup"><span data-stu-id="6f03a-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="6f03a-187">En el menú del usuario, seleccione **Mi configuración** para abrir la página **Mi configuración**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="6f03a-188">En el panel izquierdo, haga clic en **Personal** para expandir la sección relacionada y luego haga clic en **Restablecer mi token de seguridad**:</span><span class="sxs-lookup"><span data-stu-id="6f03a-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="6f03a-189">![Mi configuración](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Mi configuración")</span><span class="sxs-lookup"><span data-stu-id="6f03a-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="6f03a-190">En la página **Restablecer mi token de seguridad**, haga clic en **Restablecer token de seguridad** para solicitar un mensaje de correo electrónico que contenga el token de seguridad de Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="6f03a-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="6f03a-191">![Nuevo token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "Nuevo token")</span><span class="sxs-lookup"><span data-stu-id="6f03a-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="6f03a-192">Compruebe en su bandeja de entrada de correo electrónico si le ha llegado un correo electrónico de Salesforce.com con el asunto "**salesforce.com.com security confirmation**" (confirmación de seguridad de salesforce.com.com).</span><span class="sxs-lookup"><span data-stu-id="6f03a-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="6f03a-193">Revise este mensaje de correo electrónico y copie el valor del token de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6f03a-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="6f03a-194">En el Portal de Azure clásico, en la página de integración de aplicaciones de **Salesforce Sandbox**, haga clic en **Configurar aprovisionamiento de usuarios** para abrir el cuadro de diálogo **Configurar aprovisionamiento de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="6f03a-195">![Configurar aprovisionamiento de usuarios](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configurar aprovisionamiento de usuarios")</span><span class="sxs-lookup"><span data-stu-id="6f03a-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="6f03a-196">En la página **Especifique sus credenciales de Salesforce Sandbox para habilitar el aprovisionamiento automático de usuarios** , proporcione los valores de configuración siguientes:</span><span class="sxs-lookup"><span data-stu-id="6f03a-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="6f03a-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="6f03a-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="6f03a-198">En **Nombre de usuario de administrador de Salesforce Sandbox**, escriba un nombre de cuenta de espacio aislado de Salesforce que tenga el perfil **Administrador del sistema** asignado en Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="6f03a-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="6f03a-199">En el cuadro de texto **Contraseña de administrador de Salesforce Sandbox** , escriba la contraseña para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="6f03a-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="6f03a-200">En el cuadro de texto **Token de seguridad del usuario** , pegue el valor del token de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6f03a-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="6f03a-201">Haga clic en **Validar** para comprobar la configuración.</span><span class="sxs-lookup"><span data-stu-id="6f03a-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="6f03a-202">Haga clic en el botón **Siguiente** para abrir la página **Confirmación**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="6f03a-203">En la página **Confirmación**, haga clic en **Completar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="6f03a-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="6f03a-204">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="6f03a-204">Assigning users</span></span>

<span data-ttu-id="6f03a-205">Para probar la configuración, debe conceder acceso a los usuarios de Azure AD a los que quiere permitir el uso de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="6f03a-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="6f03a-206">**Para asignar usuarios a Salesforce Sandbox, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="6f03a-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="6f03a-207">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="6f03a-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6f03a-208">En la página de integración de aplicaciones de **Salesforce Sandbox**, haga clic en **Asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6f03a-208">On the **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="6f03a-209">![Asignar usuarios](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="6f03a-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="6f03a-210">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="6f03a-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="6f03a-211">![Sí](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="6f03a-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6f03a-212">Ahora debería esperar 10 minutos y comprobar si la cuenta se ha sincronizado en Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="6f03a-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="6f03a-213">Si desea probar la configuración de inicio de sesión único (SSO), abra el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6f03a-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="6f03a-214">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="6f03a-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

