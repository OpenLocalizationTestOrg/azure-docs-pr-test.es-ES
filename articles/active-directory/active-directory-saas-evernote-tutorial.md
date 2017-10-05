---
title: "Tutorial: Integración de Azure Active Directory con Evernote | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: be94152a84bbbeacb623d7dd8b540e3981931a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="2f365-103">Tutorial: Integración de Azure Active Directory con Evernote</span><span class="sxs-lookup"><span data-stu-id="2f365-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="2f365-104">En este tutorial, obtendrá información sobre cómo integrar Evernote con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f365-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f365-105">La integración de Evernote con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2f365-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f365-106">En Azure AD puede controlar quién tiene acceso a Evernote.</span><span class="sxs-lookup"><span data-stu-id="2f365-106">You can control in Azure AD who has access to Evernote.</span></span>
- <span data-ttu-id="2f365-107">Puede permitir que los usuarios inicien sesión automáticamente en Evernote (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f365-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2f365-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2f365-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2f365-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f365-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f365-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2f365-110">Prerequisites</span></span>

<span data-ttu-id="2f365-111">Para configurar la integración de Azure AD con Evernote, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2f365-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="2f365-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f365-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f365-113">Una suscripción habilitada para el inicio de sesión único en Evernote</span><span class="sxs-lookup"><span data-stu-id="2f365-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f365-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2f365-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f365-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2f365-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f365-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2f365-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f365-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f365-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f365-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2f365-118">Scenario description</span></span>
<span data-ttu-id="2f365-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2f365-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f365-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2f365-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f365-121">Incorporación de Evernote desde la galería</span><span class="sxs-lookup"><span data-stu-id="2f365-121">Adding Evernote from the gallery</span></span>
2. <span data-ttu-id="2f365-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f365-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="2f365-123">Incorporación de Evernote desde la galería</span><span class="sxs-lookup"><span data-stu-id="2f365-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="2f365-124">Para configurar la integración de Evernote en Azure AD, es preciso agregar Evernote desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2f365-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f365-125">**Para agregar Evernote desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2f365-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f365-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f365-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="2f365-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2f365-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f365-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2f365-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="2f365-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f365-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="2f365-133">En el cuadro de búsqueda, escriba **Evernote**, seleccione **Evernote** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f365-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span></span>

    ![Evernote en la lista de resultados](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2f365-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f365-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2f365-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Evernote con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2f365-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f365-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Evernote para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f365-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="2f365-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Evernote.</span><span class="sxs-lookup"><span data-stu-id="2f365-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="2f365-139">Para establecer la relación de vínculo, en Evernote, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="2f365-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2f365-140">Para configurar y probar el inicio de sesión único de Azure AD con Evernote, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2f365-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f365-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="2f365-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2f365-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f365-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f365-143">**[Creación de un usuario de prueba de Evernote](#create-an-evernote-test-user)**: para tener un homólogo de Britta Simon en Evernote que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f365-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f365-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f365-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f365-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="2f365-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2f365-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f365-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2f365-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Evernote.</span><span class="sxs-lookup"><span data-stu-id="2f365-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="2f365-148">**Para configurar el inicio de sesión único de Azure AD con Evernote, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2f365-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="2f365-149">En Azure Portal, en la página de integración de la aplicación **Evernote**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2f365-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="2f365-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2f365-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="2f365-153">En la sección **Dominio y direcciones URL de Evernote**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por IDP:</span><span class="sxs-lookup"><span data-stu-id="2f365-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="2f365-155">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="2f365-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="2f365-156">Active **Mostrar configuración avanzada de URL** y siga estos pasos si desea configurar la aplicación en el modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="2f365-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="2f365-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL similar a la siguiente: `https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="2f365-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="2f365-159">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2f365-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="2f365-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2f365-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="2f365-163">En la sección **Configuración de Evernote**, haga clic en **Configurar Evernote** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="2f365-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2f365-164">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="2f365-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="2f365-166">En otra ventana del explorador web, inicie sesión en el sitio de la empresa de Evernote como administrador.</span><span class="sxs-lookup"><span data-stu-id="2f365-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="2f365-167">Vaya a **"Consola de administración"**</span><span class="sxs-lookup"><span data-stu-id="2f365-167">Go to **'Admin Console'**</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="2f365-169">En la **"Consola de administración"**, vaya a **"Seguridad"** y seleccione **"Inicio de sesión único"**</span><span class="sxs-lookup"><span data-stu-id="2f365-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="2f365-171">Configure los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="2f365-171">Configure the following values:</span></span>

    ![Certificate-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="2f365-173">a.</span><span class="sxs-lookup"><span data-stu-id="2f365-173">a.</span></span>  <span data-ttu-id="2f365-174">**Enable SSO:** (Habilitar SSO) el SSO está habilitado de manera predeterminada (haga clic en **Disable Single Sign-on** [Deshabilitar el inicio de sesión único] para quitar el requisito de SSO)</span><span class="sxs-lookup"><span data-stu-id="2f365-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="2f365-175">b.</span><span class="sxs-lookup"><span data-stu-id="2f365-175">b.</span></span> <span data-ttu-id="2f365-176">Pegue el valor de la **dirección URL del servicio de inicio de sesión único** que copió de Azure Portal en el cuadro de texto **SAML HTTP Request URL** (Dirección URL de solicitud HTTP de SAML).</span><span class="sxs-lookup"><span data-stu-id="2f365-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="2f365-177">c.</span><span class="sxs-lookup"><span data-stu-id="2f365-177">c.</span></span> <span data-ttu-id="2f365-178">Abra el certificado que se descargó de Azure AD en un bloc de notas y copie el contenido, incluido "BEGIN CERTIFICATE" y "END CERTIFICATE", y péguelo en el cuadro de texto **X.509 Certificate** (Certificado X.509).</span><span class="sxs-lookup"><span data-stu-id="2f365-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="2f365-179">d. Haga clic en **Guardar cambios**</span><span class="sxs-lookup"><span data-stu-id="2f365-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="2f365-180">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f365-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2f365-181">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2f365-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2f365-182">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f365-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2f365-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f365-183">Create an Azure AD test user</span></span>

<span data-ttu-id="2f365-184">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2f365-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="2f365-186">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2f365-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f365-187">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f365-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2f365-189">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2f365-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2f365-191">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2f365-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2f365-193">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2f365-193">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2f365-195">a.</span><span class="sxs-lookup"><span data-stu-id="2f365-195">a.</span></span> <span data-ttu-id="2f365-196">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f365-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f365-197">b.</span><span class="sxs-lookup"><span data-stu-id="2f365-197">b.</span></span> <span data-ttu-id="2f365-198">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f365-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="2f365-199">c.</span><span class="sxs-lookup"><span data-stu-id="2f365-199">c.</span></span> <span data-ttu-id="2f365-200">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2f365-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="2f365-201">d.</span><span class="sxs-lookup"><span data-stu-id="2f365-201">d.</span></span> <span data-ttu-id="2f365-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2f365-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="2f365-203">Creación de un usuario de prueba de Evernote</span><span class="sxs-lookup"><span data-stu-id="2f365-203">Create an Evernote test user</span></span>

<span data-ttu-id="2f365-204">Para permitir que los usuarios de Azure AD inicien sesión en Evernote, deben aprovisionarse en Evernote.</span><span class="sxs-lookup"><span data-stu-id="2f365-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="2f365-205">En el caso de Evernote, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2f365-205">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="2f365-206">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2f365-206">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="2f365-207">Inicie sesión en el sitio de la empresa de Evernote como administrador.</span><span class="sxs-lookup"><span data-stu-id="2f365-207">Log in to your Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="2f365-208">Haga clic en la **"Consola de administración"**.</span><span class="sxs-lookup"><span data-stu-id="2f365-208">Click the **'Admin Console'**.</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="2f365-210">En la **"Consola de administración"**, vaya a **"Agregar usuarios"**.</span><span class="sxs-lookup"><span data-stu-id="2f365-210">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="2f365-212">**Agregue miembros del equipo** en el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de la cuenta de usuario y haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="2f365-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="2f365-214">Una vez que se envía la invitación, el titular de la cuenta de Azure Active Directory recibirá un correo electrónico para aceptar la invitación.</span><span class="sxs-lookup"><span data-stu-id="2f365-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2f365-215">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f365-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="2f365-216">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Evernote.</span><span class="sxs-lookup"><span data-stu-id="2f365-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="2f365-218">**Para asignar a Britta Simon a Evernote, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2f365-218">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="2f365-219">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2f365-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2f365-221">En la lista de aplicaciones, seleccione **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="2f365-221">In the applications list, select **Evernote**.</span></span>

    ![Vínculo de Evernote en la lista de aplicaciones](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="2f365-223">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2f365-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="2f365-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2f365-225">Click **Add** button.</span></span> <span data-ttu-id="2f365-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2f365-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="2f365-228">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2f365-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2f365-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2f365-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f365-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2f365-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2f365-231">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="2f365-231">Test single sign-on</span></span>

<span data-ttu-id="2f365-232">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2f365-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2f365-233">Cuando hace clic en el icono de Evernote en el Panel de acceso, debería iniciar sesión automáticamente en esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f365-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="2f365-234">Iniciará sesión como una cuenta de organización, pero deberá iniciar sesión con su cuenta personal.</span><span class="sxs-lookup"><span data-stu-id="2f365-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2f365-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2f365-235">Additional resources</span></span>

* [<span data-ttu-id="2f365-236">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f365-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f365-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f365-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

