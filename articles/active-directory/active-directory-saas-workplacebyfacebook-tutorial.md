---
title: "Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Workplace by Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1590a66f215f0c093d24ff602c0ad951ba1e1eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="521d8-103">Tutorial: integración de Azure Active Directory con Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="521d8-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="521d8-104">En este tutorial obtendrá información sobre cómo integrar Workplace by Facebook con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="521d8-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="521d8-105">Integrar Workplace by Facebook con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="521d8-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="521d8-106">Puede controlar en Azure AD quién tiene acceso a Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="521d8-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="521d8-107">Puede permitir que los usuarios inicien sesión automáticamente en Workplace by Facebook (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="521d8-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="521d8-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="521d8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="521d8-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="521d8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="521d8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="521d8-110">Prerequisites</span></span>

<span data-ttu-id="521d8-111">Para configurar la integración de Azure AD con Workplace by Facebook, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="521d8-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="521d8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="521d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="521d8-113">Una suscripción habilitada para inicio de sesión único de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="521d8-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="521d8-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="521d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="521d8-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="521d8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="521d8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="521d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="521d8-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="521d8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="521d8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="521d8-118">Scenario description</span></span>
<span data-ttu-id="521d8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="521d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="521d8-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="521d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="521d8-121">Incorporación de Workplace by Facebook desde la galería</span><span class="sxs-lookup"><span data-stu-id="521d8-121">Adding Workplace by Facebook from the gallery</span></span>
2. <span data-ttu-id="521d8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="521d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="521d8-123">Incorporación de Workplace by Facebook desde la galería</span><span class="sxs-lookup"><span data-stu-id="521d8-123">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="521d8-124">Para configurar la integración de Workplace by Facebook en Azure AD, deberá agregar Workplace by Facebook desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="521d8-124">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="521d8-125">**Para agregar Workplace by Facebook desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="521d8-125">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="521d8-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="521d8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="521d8-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="521d8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="521d8-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="521d8-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="521d8-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="521d8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="521d8-133">En el cuadro de búsqueda, escriba **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="521d8-133">In the search box, type **Workplace by Facebook**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="521d8-135">En el panel de resultados, seleccione **Workplace by Facebook** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="521d8-135">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="521d8-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="521d8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="521d8-138">En esta sección podrá configurar y probar el inicio de sesión único de Azure AD con Workplace by Facebook con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="521d8-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="521d8-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Workplace by Facebook para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="521d8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="521d8-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="521d8-140">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="521d8-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="521d8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="521d8-142">Para configurar y probar el inicio de sesión único de Azure AD con Workplace by Facebook, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="521d8-142">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="521d8-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="521d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="521d8-144">**[Configurar la frecuencia de reautenticación](#configuring-reauthentication-frequency)**: para configurar Workplace para que solicite una comprobación SAML.</span><span class="sxs-lookup"><span data-stu-id="521d8-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
3. <span data-ttu-id="521d8-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="521d8-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="521d8-146">**[Creación de un usuario de prueba de Workplace by Facebook](#creating-a-workplace-by-facebook-test-user)**: para tener un homólogo de Britta Simon en Workplace by Facebook que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="521d8-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="521d8-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="521d8-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="521d8-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="521d8-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="521d8-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="521d8-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="521d8-150">En esta sección habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="521d8-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="521d8-151">**Para configurar el inicio de sesión único de Azure AD con Workplace by Facebook, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="521d8-151">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="521d8-152">En la página de integración de la aplicación **Workplace by Facebook** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="521d8-152">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="521d8-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="521d8-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="521d8-156">En la sección **Dominio y direcciones URL de Workplace by Facebook**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="521d8-156">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="521d8-158">a.</span><span class="sxs-lookup"><span data-stu-id="521d8-158">a.</span></span> <span data-ttu-id="521d8-159">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.facebook.com`.</span><span class="sxs-lookup"><span data-stu-id="521d8-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="521d8-160">b.</span><span class="sxs-lookup"><span data-stu-id="521d8-160">b.</span></span> <span data-ttu-id="521d8-161">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="521d8-161">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="521d8-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="521d8-162">These values are not the real.</span></span> <span data-ttu-id="521d8-163">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="521d8-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="521d8-164">Póngase en contacto con el [equipo de soporte de cliente de Workplace by Facebook](https://workplace.fb.com/faq/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="521d8-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="521d8-165">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="521d8-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="521d8-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="521d8-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="521d8-169">En la sección **Configuración de Workplace by Facebook**, haga clic en **Configurar Workplace by Facebook** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="521d8-169">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="521d8-170">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="521d8-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="521d8-172">En otra ventana del explorador web, inicie sesión en el sitio de empresa de Workplace by Facebook como administrador.</span><span class="sxs-lookup"><span data-stu-id="521d8-172">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="521d8-173">Como parte del proceso de autenticación SAML, es posible que Workplace use cadenas de consulta de hasta 2,5 kilobytes de tamaño para pasar parámetros a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="521d8-173">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="521d8-174">En el **panel de empresa**, vaya a la pestaña **Autenticación**.</span><span class="sxs-lookup"><span data-stu-id="521d8-174">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="521d8-175">En **Autenticación SAML**, seleccione **Solo SSO** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="521d8-175">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="521d8-176">Escriba los valores copiados de la sección **Configuración de Workplace by Facebook** de Azure Portal en los campos correspondientes:</span><span class="sxs-lookup"><span data-stu-id="521d8-176">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="521d8-177">En el cuadro de texto **Dirección URL de SAML**, pegue el valor de **Dirección URL del servicio de inicio de sesión único** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="521d8-177">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="521d8-178">En el cuadro de texto **SAML Issuer URL** (Dirección URL del emisor SAML), pegue el valor de **SAML Entity ID** (Identificador de entidad SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="521d8-178">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="521d8-179">En el cuadro de texto **Logout URL SAML** (Dirección URL de cierre de sesión de SAML), pegue el valor de **Dirección URL de cierre de sesión** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="521d8-179">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="521d8-180">Abra el **certificado codificado en Base 64** descargado de Azure Portal en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado SAML**.</span><span class="sxs-lookup"><span data-stu-id="521d8-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="521d8-181">Es posible que sea necesario escribir la dirección URL del público, la dirección URL del destinatario y la dirección URL de ACS (Servicio de consumidor de aserciones) que aparecen en la sección **Configuración de SAML**.</span><span class="sxs-lookup"><span data-stu-id="521d8-181">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="521d8-182">Desplácese hasta la parte inferior de la sección y haga clic en el botón **Probar SSO**.</span><span class="sxs-lookup"><span data-stu-id="521d8-182">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="521d8-183">Como resultado aparece una ventana emergente en la que se muestra la página de inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="521d8-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="521d8-184">Escriba las credenciales de la forma habitual para autenticarse.</span><span class="sxs-lookup"><span data-stu-id="521d8-184">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="521d8-185">**Solución de problemas:** Asegúrese de que la dirección de correo electrónico que se devuelve desde Azure AD es la misma que la cuenta de Workplace con la que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="521d8-185">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="521d8-186">Una vez que la prueba se ha realizado correctamente, desplácese hasta la parte inferior de la página y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="521d8-186">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

14. <span data-ttu-id="521d8-187">Ahora se presentará a todos los usuarios de Workplace la página de inicio de sesión de Azure AD para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="521d8-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="521d8-188">**Redirigir el cierre de sesión de SAML (opcional)** -</span><span class="sxs-lookup"><span data-stu-id="521d8-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="521d8-189">Puede optar por configurar una dirección URL de cierre de sesión de SAML que puede usarse para apuntar a la página de cierre de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="521d8-189">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="521d8-190">Si esta opción está habilitada y configurada, ya no se dirige al usuario a la página de cierre de sesión de Workplace,</span><span class="sxs-lookup"><span data-stu-id="521d8-190">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="521d8-191">sino que se le redirige a la dirección URL agregada en la opción Redirigir el cierre de sesión de SAML.</span><span class="sxs-lookup"><span data-stu-id="521d8-191">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="521d8-192">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="521d8-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="521d8-193">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="521d8-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="521d8-194">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="521d8-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="521d8-195">Configuración de la frecuencia de reautenticación</span><span class="sxs-lookup"><span data-stu-id="521d8-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="521d8-196">Puede configurar Workplace para que solicite una comprobación SAML cada día, cada tres días, cada semana, cada dos semanas, cada mes o nunca.</span><span class="sxs-lookup"><span data-stu-id="521d8-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="521d8-197">El valor mínimo para la comprobación SAML en aplicaciones móviles se establece en una semana.</span><span class="sxs-lookup"><span data-stu-id="521d8-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="521d8-198">También puede forzar el restablecimiento de SAML para todos los usuarios mediante el botón: Require SAML authentication for all users now (Requerir autenticación de SAML para todos los usuarios ahora).</span><span class="sxs-lookup"><span data-stu-id="521d8-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="521d8-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="521d8-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="521d8-200">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="521d8-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="521d8-202">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="521d8-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="521d8-203">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="521d8-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="521d8-205">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="521d8-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="521d8-207">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="521d8-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="521d8-209">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="521d8-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="521d8-211">a.</span><span class="sxs-lookup"><span data-stu-id="521d8-211">a.</span></span> <span data-ttu-id="521d8-212">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="521d8-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="521d8-213">b.</span><span class="sxs-lookup"><span data-stu-id="521d8-213">b.</span></span> <span data-ttu-id="521d8-214">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="521d8-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="521d8-215">c.</span><span class="sxs-lookup"><span data-stu-id="521d8-215">c.</span></span> <span data-ttu-id="521d8-216">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="521d8-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="521d8-217">d.</span><span class="sxs-lookup"><span data-stu-id="521d8-217">d.</span></span> <span data-ttu-id="521d8-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="521d8-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="521d8-219">Creación de un usuario de prueba de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="521d8-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="521d8-220">En esta sección se crea un usuario llamado Britta Simon en Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="521d8-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="521d8-221">Workplace by Facebook admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="521d8-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="521d8-222">El usuario no tiene que hacer nada en esta sección.</span><span class="sxs-lookup"><span data-stu-id="521d8-222">There is no action for you in this section.</span></span> <span data-ttu-id="521d8-223">Si no existe un usuario en Workplace by Facebook, se crea uno cuando intenta obtener acceso a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="521d8-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="521d8-224">Si necesita crear un usuario de forma manual, póngase en contacto con el [equipo de soporte de cliente de Workplace by Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="521d8-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="521d8-225">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="521d8-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="521d8-226">En esta sección, habilitará a Britta Simon para usar el inicio de sesión único de Azure al concederle acceso a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="521d8-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="521d8-228">**Para asignar a Britta Simon a Workplace by Facebook, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="521d8-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="521d8-229">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="521d8-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="521d8-231">En la lista de aplicaciones, seleccione **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="521d8-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="521d8-233">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="521d8-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="521d8-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="521d8-235">Click **Add** button.</span></span> <span data-ttu-id="521d8-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="521d8-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="521d8-238">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="521d8-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="521d8-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="521d8-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="521d8-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="521d8-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="521d8-241">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="521d8-241">Testing single sign-on</span></span>

<span data-ttu-id="521d8-242">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="521d8-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="521d8-243">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="521d8-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="521d8-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="521d8-244">Additional resources</span></span>

* [<span data-ttu-id="521d8-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="521d8-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="521d8-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="521d8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="521d8-247">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="521d8-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

