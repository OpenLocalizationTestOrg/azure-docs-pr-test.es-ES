---
title: "Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Workplace by Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="4a77c-103">Tutorial: integración de Azure Active Directory con Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="4a77c-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="4a77c-104">En este tutorial obtendrá información sobre cómo integrar Workplace by Facebook con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a77c-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a77c-105">Integrar Workplace by Facebook con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4a77c-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4a77c-106">Puede controlar en Azure AD quién tiene acceso a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4a77c-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="4a77c-107">Puede permitir que los usuarios inicien sesión automáticamente en Workplace by Facebook (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a77c-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4a77c-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4a77c-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="4a77c-109">Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a77c-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a77c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4a77c-110">Prerequisites</span></span>

<span data-ttu-id="4a77c-111">Para configurar la integración de Azure AD con Workplace by Facebook, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4a77c-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="4a77c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a77c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a77c-113">Una suscripción habilitada para inicio de sesión único (SSO) de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="4a77c-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="4a77c-114">Para probar los pasos de este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4a77c-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="4a77c-115">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4a77c-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a77c-116">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a77c-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a77c-117">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4a77c-117">Scenario description</span></span>
<span data-ttu-id="4a77c-118">En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4a77c-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="4a77c-119">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="4a77c-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a77c-120">Adición de Workplace by Facebook desde la galería.</span><span class="sxs-lookup"><span data-stu-id="4a77c-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="4a77c-121">Configuración y prueba del inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a77c-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="4a77c-122">Adición de Workplace by Facebook desde la galería</span><span class="sxs-lookup"><span data-stu-id="4a77c-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="4a77c-123">Para configurar la integración de Workplace by Facebook en Azure AD, agregue Workplace by Facebook desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="4a77c-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="4a77c-124">En el panel izquierdo de [Azure Portal](https://portal.azure.com), seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="4a77c-126">Vaya a **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="4a77c-128">Para agregar una nueva aplicación, seleccione **Nueva aplicación** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4a77c-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="4a77c-130">En el cuadro de búsqueda, escriba **Workplace by Facebook** y seleccione **Workplace by Facebook** desde los resultados.</span><span class="sxs-lookup"><span data-stu-id="4a77c-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="4a77c-131">Después, seleccione **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4a77c-131">Then select **Add**, to add the application.</span></span>

    ![Workplace by Facebook en la lista de resultados](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4a77c-133">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a77c-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4a77c-134">En esta sección podrá configurar y probar el SSO de Azure AD con Workplace by Facebook con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4a77c-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4a77c-135">Para que el SSO funcione, Azure AD debe saber cuál es el usuario homólogo de Workplace by Facebook para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a77c-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="4a77c-136">Es decir, es necesario establecer una relación vinculada entre un usuario de Azure AD y el usuario relacionado de Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4a77c-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="4a77c-137">Establezca esta relación mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4a77c-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4a77c-138">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a77c-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4a77c-139">En esta sección habilitará el SSO de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4a77c-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="4a77c-140">En la página de integración de la aplicación **Workplace by Facebook** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="4a77c-142">En el cuadro de diálogo **Inicio de sesión único**, seleccione el **Modo** en **Inicio de sesión basado en SAML** para habilitar el SSO.</span><span class="sxs-lookup"><span data-stu-id="4a77c-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="4a77c-144">En la sección **Dominio y direcciones URL de Workplace by Facebook**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4a77c-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="4a77c-145">a.</span><span class="sxs-lookup"><span data-stu-id="4a77c-145">a.</span></span> <span data-ttu-id="4a77c-146">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company subdomain>.facebook.com`.</span><span class="sxs-lookup"><span data-stu-id="4a77c-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="4a77c-147">b.</span><span class="sxs-lookup"><span data-stu-id="4a77c-147">b.</span></span> <span data-ttu-id="4a77c-148">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://www.facebook.com/company/<scim company id>`.</span><span class="sxs-lookup"><span data-stu-id="4a77c-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="4a77c-149">Estos valores son solo un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4a77c-149">These values are an example only.</span></span> <span data-ttu-id="4a77c-150">Debe actualizarlos con la dirección URL de inicio de sesión y el identificador reales.</span><span class="sxs-lookup"><span data-stu-id="4a77c-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="4a77c-151">Póngase en contacto con el [equipo de soporte técnico al cliente de Workplace by Facebook](https://workplace.fb.com/faq/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="4a77c-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="4a77c-152">En la sección **Certificado de firma de SAML**, seleccione **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4a77c-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="4a77c-154">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-154">Select **Save**.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4a77c-156">En la sección **Configuración de Workplace by Facebook**, seleccione **Configurar Workplace by Facebook** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="4a77c-157">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Configuración de Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="4a77c-159">En otra ventana del explorador web, inicie sesión en el sitio de empresa de Workplace by Facebook como administrador.</span><span class="sxs-lookup"><span data-stu-id="4a77c-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="4a77c-160">Como parte del proceso de autenticación SAML, Workplace puede usar cadenas de consulta de hasta 2,5 kilobytes de tamaño para pasar parámetros a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a77c-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="4a77c-161">En el **panel de empresa**, vaya a la pestaña **Autenticación**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="4a77c-162">En **Autenticación SAML**, seleccione **Solo SSO** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="4a77c-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="4a77c-163">Escriba los valores copiados de la sección **Configuración de Workplace by Facebook** de Azure Portal en los campos correspondientes:</span><span class="sxs-lookup"><span data-stu-id="4a77c-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="4a77c-164">En el cuadro de texto **Dirección URL de SAML**, pegue el valor de **Dirección URL del servicio de inicio de sesión único** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4a77c-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="4a77c-165">En el cuadro de texto **SAML Issuer URL** (Dirección URL del emisor SAML), pegue el valor de **SAML Entity ID** (Identificador de entidad SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4a77c-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="4a77c-166">En el cuadro de texto **Logout URL SAML** (Dirección URL de cierre de sesión de SAML), pegue el valor de **Dirección URL de cierre de sesión** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4a77c-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="4a77c-167">Abra su **certificado codificado en base 64** en el Bloc de notas, descargado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4a77c-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="4a77c-168">Copie el contenido del mismo en el Portapapeles y, después, péguelo en el cuadro de texto **Certificado SAML**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="4a77c-169">Es posible que tenga que escribir la dirección URL del público, la dirección URL del destinatario y la dirección URL de ACS (Servicio de consumidor de aserciones) que aparecen en la sección **Configuración de SAML**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="4a77c-170">Desplácese hasta la parte inferior de la sección y seleccione **Probar SSO**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="4a77c-171">Aparece una ventana emergente, con la página de inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a77c-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="4a77c-172">Para autenticarse, escriba las credenciales de la forma habitual.</span><span class="sxs-lookup"><span data-stu-id="4a77c-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="4a77c-173">Asegúrese de que la dirección de correo electrónico que se devuelve desde Azure AD es la misma que la cuenta de Workplace con la que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="4a77c-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="4a77c-174">Si la prueba ha finalizado correctamente, desplácese hasta la parte inferior de la página y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="4a77c-175">A todo el que use Workplace se le presentará la página de inicio de sesión de Azure AD para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="4a77c-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="4a77c-176">Puede optar por configurar una dirección URL de cierre de sesión de SAML, que puede usarse para apuntar a la página de cierre de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a77c-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="4a77c-177">Si esta opción está habilitada y configurada, ya no se dirige al usuario a la página de cierre de sesión de Workplace,</span><span class="sxs-lookup"><span data-stu-id="4a77c-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="4a77c-178">sino que se le redirige a la dirección URL agregada en la opción de redirección del cierre de sesión de SAML.</span><span class="sxs-lookup"><span data-stu-id="4a77c-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="4a77c-179">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4a77c-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="4a77c-180">Después de agregar esta aplicación desde la sección **Active Directory** > **Aplicaciones empresariales**, simplemente seleccione la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4a77c-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4a77c-181">Puede leer más sobre la característica de documentación insertada en el artículo sobre la [documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="4a77c-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="4a77c-182">Configuración de la frecuencia de reautenticación</span><span class="sxs-lookup"><span data-stu-id="4a77c-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="4a77c-183">Puede configurar Workplace para que solicite una comprobación SAML cada día, cada tres días, cada semana, cada dos semanas, cada mes o nunca.</span><span class="sxs-lookup"><span data-stu-id="4a77c-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="4a77c-184">El valor mínimo para la comprobación SAML en aplicaciones móviles se establece en una semana.</span><span class="sxs-lookup"><span data-stu-id="4a77c-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="4a77c-185">También puede forzar un restablecimiento de SAML para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="4a77c-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="4a77c-186">Para ello, use el botón **Require SAML authentication for all users now** (Requerir autenticación de SAML para todos los usuarios ahora).</span><span class="sxs-lookup"><span data-stu-id="4a77c-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4a77c-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a77c-187">Create an Azure AD test user</span></span>
<span data-ttu-id="4a77c-188">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4a77c-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

1. <span data-ttu-id="4a77c-190">En el panel izquierdo de **Azure Portal**, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a77c-192">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y seleccione **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a77c-194">Para abrir el cuadro de diálogo **Usuario**, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a77c-196">En el cuadro de diálogo **Usuario**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4a77c-196">In the **User** dialog box, do the following:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a77c-198">a.</span><span class="sxs-lookup"><span data-stu-id="4a77c-198">a.</span></span> <span data-ttu-id="4a77c-199">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a77c-200">b.</span><span class="sxs-lookup"><span data-stu-id="4a77c-200">b.</span></span> <span data-ttu-id="4a77c-201">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a77c-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a77c-202">c.</span><span class="sxs-lookup"><span data-stu-id="4a77c-202">c.</span></span> <span data-ttu-id="4a77c-203">Seleccione **Mostrar contraseña** y anótela.</span><span class="sxs-lookup"><span data-stu-id="4a77c-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="4a77c-204">d.</span><span class="sxs-lookup"><span data-stu-id="4a77c-204">d.</span></span> <span data-ttu-id="4a77c-205">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="4a77c-206">Creación de un usuario de prueba de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="4a77c-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="4a77c-207">En esta sección se crea un usuario llamado Britta Simon en Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4a77c-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="4a77c-208">Workplace by Facebook admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4a77c-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="4a77c-209">El usuario no tiene que hacer nada en esta sección.</span><span class="sxs-lookup"><span data-stu-id="4a77c-209">There is no action for you in this section.</span></span> <span data-ttu-id="4a77c-210">Si no existe un usuario en Workplace by Facebook, se crea uno cuando intenta obtener acceso a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4a77c-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="4a77c-211">Si tiene que crear un usuario de forma manual, póngase en contacto con el [equipo de soporte técnico al cliente de Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="4a77c-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4a77c-212">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a77c-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="4a77c-213">En esta sección, habilitará a Britta Simon para usar el SSO de Azure al concederle acceso a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4a77c-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![Asignar usuario][200] 

1. <span data-ttu-id="4a77c-215">En Azure Portal, abra la vista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4a77c-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="4a77c-216">Vaya a la vista de directorios, vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4a77c-218">En la lista de aplicaciones, seleccione **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Vínculo de Workplace by Facebook en la lista de aplicaciones](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="4a77c-220">En el menú de la izquierda, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-220">In the menu on the left, select **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="4a77c-222">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-222">Select **Add**.</span></span> <span data-ttu-id="4a77c-223">Después, en el panel **Agregar asignación**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="4a77c-225">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="4a77c-226">En el cuadro de diálogo **Usuarios y grupos**, elija **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="4a77c-227">En el cuadro de diálogo **Agregar asignación**, seleccione **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="4a77c-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4a77c-228">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="4a77c-228">Test single sign-on</span></span>

<span data-ttu-id="4a77c-229">Si desea probar la configuración de inicio de sesión único (SSO), abra el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4a77c-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="4a77c-230">Para más información, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4a77c-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4a77c-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a77c-231">Next steps</span></span>

* <span data-ttu-id="4a77c-232">Consulte la [lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="4a77c-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="4a77c-233">Consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a77c-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="4a77c-234">Más información acerca de cómo [configurar el aprovisionamiento de usuarios](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4a77c-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

