---
title: "Tutorial: Integración de Azure Active Directory con Voyance | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="57358-103">Tutorial: Integración de Azure Active Directory con Voyance</span><span class="sxs-lookup"><span data-stu-id="57358-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="57358-104">En este tutorial, aprenderá a integrar Voyance con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57358-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57358-105">La integración de Voyance con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="57358-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57358-106">Puede controlar en Azure AD quién tiene acceso a Voyance.</span><span class="sxs-lookup"><span data-stu-id="57358-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="57358-107">Puede permitir que los usuarios inicien sesión automáticamente en Voyance (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57358-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57358-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="57358-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="57358-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57358-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57358-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="57358-110">Prerequisites</span></span>

<span data-ttu-id="57358-111">Para configurar la integración de Azure AD con Voyance, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="57358-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="57358-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57358-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57358-113">Una suscripción habilitada para el inicio de sesión único en Voyance</span><span class="sxs-lookup"><span data-stu-id="57358-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57358-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="57358-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57358-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="57358-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57358-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="57358-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57358-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57358-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57358-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="57358-118">Scenario description</span></span>
<span data-ttu-id="57358-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="57358-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57358-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="57358-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57358-121">Adición de Voyance desde la galería</span><span class="sxs-lookup"><span data-stu-id="57358-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="57358-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57358-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="57358-123">Adición de Voyance desde la galería</span><span class="sxs-lookup"><span data-stu-id="57358-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="57358-124">Para configurar la integración de Voyance en Azure AD, deberá agregar Voyance desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="57358-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57358-125">**Para agregar Voyance desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="57358-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57358-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="57358-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="57358-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="57358-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57358-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="57358-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="57358-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="57358-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="57358-133">En el cuadro de búsqueda, escriba **Voyance**, seleccione **Voyance** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="57358-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![Voyance en la lista de resultados](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="57358-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="57358-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="57358-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Voyance con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="57358-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57358-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Voyance para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57358-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="57358-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Voyance.</span><span class="sxs-lookup"><span data-stu-id="57358-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="57358-139">Para establecer la relación de vínculo, en Voyance, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="57358-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="57358-140">Para configurar y probar el inicio de sesión único de Azure AD con Voyance, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="57358-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57358-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="57358-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57358-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57358-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57358-143">**[Creación de un usuario de prueba de Voyance](#create-a-voyance-test-user)**: para tener un homólogo de Britta Simon en Voyance que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57358-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="57358-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57358-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57358-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="57358-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="57358-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57358-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="57358-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Voyance.</span><span class="sxs-lookup"><span data-stu-id="57358-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="57358-148">**Para configurar el inicio de sesión único de Azure AD con Voyance, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="57358-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="57358-149">En Azure Portal, en la página de integración de la aplicación **Voyance**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="57358-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="57358-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="57358-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="57358-153">En la sección **Dominio y direcciones URL de Voyance**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="57358-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Voyance para IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="57358-155">a.</span><span class="sxs-lookup"><span data-stu-id="57358-155">a.</span></span> <span data-ttu-id="57358-156">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="57358-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="57358-157">b.</span><span class="sxs-lookup"><span data-stu-id="57358-157">b.</span></span> <span data-ttu-id="57358-158">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.nyansa.com/saml/create/`.</span><span class="sxs-lookup"><span data-stu-id="57358-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="57358-159">Active **Mostrar configuración avanzada de URL** y siga estos pasos si desea configurar la aplicación en el modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="57358-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Voyance para SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="57358-161">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.nyansa.com/`.</span><span class="sxs-lookup"><span data-stu-id="57358-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="57358-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="57358-162">These values are not real.</span></span> <span data-ttu-id="57358-163">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="57358-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="57358-164">Póngase en contacto con el [equipo de soporte técnico de Voyance](mailto:support@nyansa.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="57358-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="57358-165">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="57358-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="57358-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="57358-167">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="57358-169">En la sección **Configuración de Voyance**, haga clic en **Configurar Voyance** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="57358-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="57358-170">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="57358-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="57358-172">En otra ventana del explorador web, inicie sesión en el inquilino de Voyance como administrador.</span><span class="sxs-lookup"><span data-stu-id="57358-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="57358-173">Vaya a la esquina superior derecha de la barra de navegación y haga clic en la lista desplegable que dice "**Acme University**".</span><span class="sxs-lookup"><span data-stu-id="57358-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="57358-175">Haga clic en "**Configuración de administración**".</span><span class="sxs-lookup"><span data-stu-id="57358-175">Click "**Admin Settings**".</span></span>

    ![Configuración del inicio de sesión único en la configuración de administrador de la aplicación](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="57358-177">Haga clic en la pestaña "**Acceso de usuarios**".</span><span class="sxs-lookup"><span data-stu-id="57358-177">Click "**User Access**" tab.</span></span>

    ![Configuración del inicio de sesión único en el acceso de usuarios de la aplicación](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="57358-179">Haga clic en el botón "**SSO is disabled**" (SSO está deshabilitado) para configurar Azure AD como IdP mediante SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="57358-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configuración del inicio de sesión único con el botón SSO deshabilitado en la aplicación](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="57358-181">Vaya a la sección **SAML v2** y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="57358-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![Configuración del inicio de sesión único en la configuración SAML v2 de la aplicación](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="57358-183">a.</span><span class="sxs-lookup"><span data-stu-id="57358-183">a.</span></span> <span data-ttu-id="57358-184">Seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="57358-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="57358-185">b.</span><span class="sxs-lookup"><span data-stu-id="57358-185">b.</span></span> <span data-ttu-id="57358-186">Pegue el valor de **Dirección URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal en el cuadro de texto **IdP Login URL** (Dirección URL de inicio de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="57358-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="57358-187">c.</span><span class="sxs-lookup"><span data-stu-id="57358-187">c.</span></span> <span data-ttu-id="57358-188">Abra el certificado descargado con codificación Base64 en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **IdP Cert** (Certificado IdP).</span><span class="sxs-lookup"><span data-stu-id="57358-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="57358-189">d.</span><span class="sxs-lookup"><span data-stu-id="57358-189">d.</span></span> <span data-ttu-id="57358-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="57358-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="57358-191">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="57358-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="57358-192">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="57358-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="57358-193">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57358-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="57358-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57358-194">Create an Azure AD test user</span></span>

<span data-ttu-id="57358-195">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="57358-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="57358-197">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="57358-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57358-198">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="57358-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57358-200">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="57358-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57358-202">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="57358-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57358-204">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="57358-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57358-206">a.</span><span class="sxs-lookup"><span data-stu-id="57358-206">a.</span></span> <span data-ttu-id="57358-207">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57358-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57358-208">b.</span><span class="sxs-lookup"><span data-stu-id="57358-208">b.</span></span> <span data-ttu-id="57358-209">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57358-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57358-210">c.</span><span class="sxs-lookup"><span data-stu-id="57358-210">c.</span></span> <span data-ttu-id="57358-211">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="57358-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57358-212">d.</span><span class="sxs-lookup"><span data-stu-id="57358-212">d.</span></span> <span data-ttu-id="57358-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="57358-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="57358-214">Creación de un usuario de prueba de Voyance</span><span class="sxs-lookup"><span data-stu-id="57358-214">Create a Voyance test user</span></span>

<span data-ttu-id="57358-215">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Voyance.</span><span class="sxs-lookup"><span data-stu-id="57358-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="57358-216">Voyance admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="57358-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="57358-217">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="57358-217">There is no action item for you in this section.</span></span> <span data-ttu-id="57358-218">Al intentar acceder a Voyance, se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="57358-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="57358-219">Si necesita crear manualmente un usuario, es preciso que se ponga en contacto con el [equipo de soporte técnico de Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="57358-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="57358-220">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57358-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="57358-221">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Voyance.</span><span class="sxs-lookup"><span data-stu-id="57358-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![Asignación del rol de usuario][200]

<span data-ttu-id="57358-223">**Para asignar a Britta Simon a Voyance, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="57358-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="57358-224">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="57358-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="57358-226">En la lista de aplicaciones, seleccione **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="57358-226">In the applications list, select **Voyance**.</span></span>

    ![Vínculo a Voyance en la lista de aplicaciones](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="57358-228">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="57358-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="57358-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="57358-230">Click **Add** button.</span></span> <span data-ttu-id="57358-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="57358-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="57358-233">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="57358-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57358-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="57358-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57358-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="57358-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="57358-236">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="57358-236">Test single sign-on</span></span>

<span data-ttu-id="57358-237">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="57358-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="57358-238">Al hacer clic en el icono de Voyance en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Voyance.</span><span class="sxs-lookup"><span data-stu-id="57358-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57358-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="57358-239">Additional resources</span></span>

* [<span data-ttu-id="57358-240">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57358-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57358-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57358-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

