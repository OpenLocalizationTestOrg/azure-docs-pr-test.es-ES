---
title: "Tutorial: Integración de Azure Active Directory con Adobe Creative Cloud | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Adobe Creative Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="2a2c9-103">Tutorial: Integración de Azure Active Directory con Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="2a2c9-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="2a2c9-104">En este tutorial, aprenderá a integrar Adobe Creative Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2a2c9-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a2c9-105">La integración de Adobe Creative Cloud con Azure AD ofrece las ventajas siguientes:</span><span class="sxs-lookup"><span data-stu-id="2a2c9-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2a2c9-106">En Azure AD se puede controlar quién tiene acceso a Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="2a2c9-107">Puede permitir que los usuarios inicien sesión automáticamente en Adobe Creative Cloud (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2a2c9-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2a2c9-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2a2c9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a2c9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a2c9-110">Prerequisites</span></span>

<span data-ttu-id="2a2c9-111">Para configurar la integración de Azure AD con Adobe Creative Cloud, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a2c9-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="2a2c9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a2c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2a2c9-113">Una suscripción habilitada para el inicio de sesión único en Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="2a2c9-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2a2c9-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2a2c9-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2a2c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2a2c9-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2a2c9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a2c9-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2a2c9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2a2c9-118">Scenario description</span></span>
<span data-ttu-id="2a2c9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a2c9-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2a2c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a2c9-121">Agregar Adobe Creative Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="2a2c9-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="2a2c9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a2c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="2a2c9-123">Agregar Adobe Creative Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="2a2c9-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="2a2c9-124">Para configurar la integración de Adobe Creative Cloud en Azure AD, necesita agregar Adobe Creative Cloud desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2a2c9-125">**Para agregar Adobe Creative Cloud desde la galería, siga este procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="2a2c9-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2a2c9-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2a2c9-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2a2c9-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2a2c9-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2a2c9-133">En el cuadro de búsqueda, escriba **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="2a2c9-135">En el panel de resultados, seleccione **Adobe Creative Cloud** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2a2c9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a2c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2a2c9-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Adobe Creative Cloud utilizando usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2a2c9-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2a2c9-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Adobe Creative Cloud para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="2a2c9-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="2a2c9-141">Esta relación de vínculo se establece mediante la asignación del valor de **nombre de usuario** en Azure AD como valor de **Username** (Nombre de usuario) en Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="2a2c9-142">Para configurar y probar el inicio de sesión único de Azure AD con Adobe Creative Cloud, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2a2c9-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2a2c9-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2a2c9-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2a2c9-145">**[Creación de un usuario de prueba de Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user)**: para tener un homólogo de Britta Simon en Adobe Creative Cloud que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2a2c9-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2a2c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2a2c9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a2c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2a2c9-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="2a2c9-150">**Para configurar el inicio de sesión único de Azure AD con Adobe Creative Cloud, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2a2c9-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="2a2c9-151">En el Portal de administración de Azure, en la página de integración de aplicaciones de **Adobe Creative Cloud**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2a2c9-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="2a2c9-155">En la sección **Dominio y direcciones URL de Adobe Creative Cloud**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="2a2c9-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="2a2c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-157">a.</span></span> <span data-ttu-id="2a2c9-158">En el cuadro de texto **Identificador**, escriba el valor como `https://www.okta.com/saml2/service-provider/<token>`.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="2a2c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-159">b.</span></span> <span data-ttu-id="2a2c9-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<company name>.okta.com/auth/saml20/accauthlinktest`.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2a2c9-161">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-161">Please note that these are not the real values.</span></span> <span data-ttu-id="2a2c9-162">Estos valores se tienen que actualizar con los valores reales de Identificador y URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2a2c9-163">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="2a2c9-164">Si necesita crear manualmente un usuario, es preciso que se ponga en contacto con el equipo de soporte técnico de Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="2a2c9-165">En la sección **Dominio y direcciones URL de Adobe Creative Cloud**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="2a2c9-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="2a2c9-167">a.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-167">a.</span></span> <span data-ttu-id="2a2c9-168">Haga clic en la opción **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="2a2c9-169">b.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-169">b.</span></span> <span data-ttu-id="2a2c9-170">En el cuadro de texto **URL de inicio de sesión**, escriba el valor como: `https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="2a2c9-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="2a2c9-171">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="2a2c9-173">En la sección **Configuración de Adobe Creative Cloud**, haga clic en **Configurar Adobe Creative Cloud** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2a2c9-174">Copie la **SAML Entity ID and SAML Single Sign-On Service URL** (URL del servicio de SSO de SAML e Id. de entidad de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="2a2c9-176">En otra ventana del explorador web, inicie sesión como administrador en el inquilino de Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="2a2c9-177">Vaya a **Identity** (Identidad) en el panel de navegación izquierdo y haga clic en su dominio.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="2a2c9-178">Realice los pasos siguientes en la sección **Single Sign On Configuration Required** (Configuración de inicio de sesión único necesaria).</span><span class="sxs-lookup"><span data-stu-id="2a2c9-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="2a2c9-179">![Configuración](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="2a2c9-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="2a2c9-180">Haga clic en **Browse** (Examinar) para cargar el certificado descargado de Azure AD en **IDP Certificate** (Certificado IDP).</span><span class="sxs-lookup"><span data-stu-id="2a2c9-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="2a2c9-181">En el cuadro de texto **IDP issuer** (Emisor de IDP), pegue el **Id. de entidad de SAML** que copió de la sección **Configurar inicio de sesión** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="2a2c9-182">En el cuadro de texto **IDP Login URL** (URL de inicio de sesión IDP), pegue la **URL del servicio de SSO de SAML** que copió de la sección **Configurar inicio de sesión** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="2a2c9-183">Seleccione **HTTP - Redirect** (HTTP - Redireccionamiento) como **IDP Binding** (Enlace IDP).</span><span class="sxs-lookup"><span data-stu-id="2a2c9-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="2a2c9-184">Seleccione **Email Address** (Dirección de correo electrónico) como **User Login Setting** (Configuración de inicio de sesión de usuario).</span><span class="sxs-lookup"><span data-stu-id="2a2c9-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="2a2c9-185">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2a2c9-185">Click **Save** button.</span></span>

15. <span data-ttu-id="2a2c9-186">El panel presentará ahora el archivo XML **"Download Metadata"** (Descargar metadatos).</span><span class="sxs-lookup"><span data-stu-id="2a2c9-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="2a2c9-187">Contiene la URL de EntityDescriptor y la URL de AssertionConsumerService de Adobe.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="2a2c9-188">Abra el archivo y configúrelas en la aplicación Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="2a2c9-191">a.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-191">a.</span></span> <span data-ttu-id="2a2c9-192">Use el valor de EntityDescriptor que le proporciona Adobe como **Identificador** en el cuadro de diálogo **Configurar las opciones de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="2a2c9-193">b.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-193">b.</span></span> <span data-ttu-id="2a2c9-194">Use el valor de AssertionConsumerService que le proporciona Adobe como **URL de respuesta** en el cuadro de diálogo **Configurar las opciones de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2a2c9-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a2c9-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="2a2c9-196">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2a2c9-198">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2a2c9-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2a2c9-199">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2a2c9-201">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2a2c9-203">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2a2c9-205">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2a2c9-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2a2c9-207">a.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-207">a.</span></span> <span data-ttu-id="2a2c9-208">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2a2c9-209">b.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-209">b.</span></span> <span data-ttu-id="2a2c9-210">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2a2c9-211">c.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-211">c.</span></span> <span data-ttu-id="2a2c9-212">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2a2c9-213">d.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-213">d.</span></span> <span data-ttu-id="2a2c9-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="2a2c9-215">Creación de un usuario de prueba de Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="2a2c9-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="2a2c9-216">Para permitir que los usuarios de Azure AD inicien sesión en Adobe Creative Cloud, deben aprovisionarse en Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="2a2c9-217">En el caso de Adobe Creative Cloud, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="2a2c9-218">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2a2c9-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="2a2c9-219">Inicie sesión como administrador en su sitio de la compañía de Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="2a2c9-220">Haga clic en **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-220">Click **People**.</span></span>

    <span data-ttu-id="2a2c9-221">![Personas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="2a2c9-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="2a2c9-222">Haga clic en **Invitar a usuario**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-222">Click **Invite User**.</span></span>

    <span data-ttu-id="2a2c9-223">![Invitación de usuarios](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invitación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="2a2c9-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="2a2c9-224">En la página de diálogo **Invitar a personas**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2a2c9-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="2a2c9-225">![Invitar a personas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="2a2c9-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="2a2c9-226">a.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-226">a.</span></span> <span data-ttu-id="2a2c9-227">En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de la cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="2a2c9-228">b.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-228">b.</span></span> <span data-ttu-id="2a2c9-229">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2a2c9-230">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2a2c9-231">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a2c9-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2a2c9-232">En esta sección, se habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2a2c9-234">**Para asignar a Britta Simon a Adobe Creative Cloud, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2a2c9-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="2a2c9-235">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="2a2c9-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2a2c9-237">En la lista de aplicaciones, seleccione **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="2a2c9-239">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2a2c9-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-241">Click **Add** button.</span></span> <span data-ttu-id="2a2c9-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2a2c9-244">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2a2c9-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2a2c9-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2a2c9-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2a2c9-247">Testing single sign-on</span></span>

<span data-ttu-id="2a2c9-248">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2a2c9-249">Al hacer clic en el icono de Adobe Creative Cloud del panel de acceso, debería iniciar sesión automáticamente en la aplicación Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="2a2c9-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2a2c9-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2a2c9-250">Additional resources</span></span>

* [<span data-ttu-id="2a2c9-251">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a2c9-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a2c9-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2a2c9-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png