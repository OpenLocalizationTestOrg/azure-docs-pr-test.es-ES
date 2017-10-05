---
title: "Tutorial: integración de Azure Active Directory con ClickTime | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 0e0123a40d52dfd7a2e29c29cb2239e979089ca9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="a7916-103">Tutorial: integración de Azure Active Directory con ClickTime</span><span class="sxs-lookup"><span data-stu-id="a7916-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="a7916-104">En este tutorial, aprenderá a integrar ClickTime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7916-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7916-105">La integración de ClickTime con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a7916-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7916-106">Puede controlar en Azure AD quién tiene acceso a ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7916-106">You can control in Azure AD who has access to ClickTime</span></span>
- <span data-ttu-id="a7916-107">Puede habilitar que los usuarios inicien sesión automáticamente en ClickTime (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7916-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7916-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a7916-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7916-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7916-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7916-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a7916-110">Prerequisites</span></span>

<span data-ttu-id="a7916-111">Para configurar la integración de Azure AD con ClickTime, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a7916-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

- <span data-ttu-id="a7916-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7916-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7916-113">Una suscripción habilitada para el inicio de sesión único en ClickTime</span><span class="sxs-lookup"><span data-stu-id="a7916-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7916-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a7916-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7916-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a7916-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7916-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a7916-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7916-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7916-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7916-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a7916-118">Scenario description</span></span>
<span data-ttu-id="a7916-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a7916-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7916-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="a7916-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7916-121">Agregar ClickTime desde la galería</span><span class="sxs-lookup"><span data-stu-id="a7916-121">Adding ClickTime from the gallery</span></span>
2. <span data-ttu-id="a7916-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7916-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="a7916-123">Agregar ClickTime desde la galería</span><span class="sxs-lookup"><span data-stu-id="a7916-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="a7916-124">Para configurar la integración de ClickTime en Azure AD, debe agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="a7916-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7916-125">**Para agregar ClickTime desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a7916-125">**To add ClickTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7916-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7916-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="a7916-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a7916-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7916-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a7916-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="a7916-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7916-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="a7916-133">En el cuadro de búsqueda, escriba **ClickTime**, seleccione **ClickTime** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7916-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span></span>

    ![ClickTime en la lista de resultados](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a7916-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7916-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a7916-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ClickTime con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a7916-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7916-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ClickTime para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7916-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="a7916-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7916-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="a7916-139">Para establecer la relación de vínculo, en ClickTime, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="a7916-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a7916-140">Para configurar y probar el inicio de sesión único de Azure AD con ADP ClickTime, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a7916-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7916-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="a7916-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a7916-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7916-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7916-143">**[Creación de un usuario de prueba de ClickTime](#create-a-clicktime-test-user)**: para tener un homólogo de Britta Simon en ClickTime que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7916-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7916-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7916-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7916-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="a7916-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a7916-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7916-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a7916-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7916-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="a7916-148">**Para configurar el inicio de sesión único de Azure AD con ClickTime, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="a7916-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="a7916-149">En Azure Portal, en la página de integración de la aplicación **ClickTime**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a7916-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="a7916-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a7916-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="a7916-153">En la sección **Dominio y direcciones URL de ClickTime**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a7916-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="a7916-155">a.</span><span class="sxs-lookup"><span data-stu-id="a7916-155">a.</span></span> <span data-ttu-id="a7916-156">En el cuadro de texto **Identificador**, escriba una dirección URL como: `https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="a7916-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="a7916-157">b.</span><span class="sxs-lookup"><span data-stu-id="a7916-157">b.</span></span> <span data-ttu-id="a7916-158">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con los siguientes patrones:</span><span class="sxs-lookup"><span data-stu-id="a7916-158">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="a7916-159">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a7916-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="a7916-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a7916-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a7916-163">En la sección **Configuración de ClickTime**, haga clic en **Configurar ClickTime** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="a7916-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a7916-164">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="a7916-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="a7916-166">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de ClickTime como administrador.</span><span class="sxs-lookup"><span data-stu-id="a7916-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="a7916-167">En la barra de herramientas de la parte superior, haga clic en**Preferencias** y luego haga clic en **Configuración de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="a7916-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="a7916-168">En la sección de configuración **Preferencias de inicio de sesión único** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a7916-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="a7916-169">![Configuración de seguridad](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Configuración de seguridad")</span><span class="sxs-lookup"><span data-stu-id="a7916-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="a7916-170">a.</span><span class="sxs-lookup"><span data-stu-id="a7916-170">a.</span></span>  <span data-ttu-id="a7916-171">Seleccione **Allow** sign-in using Single Sign-On (SSO) with **Azure AD** [Permitir inicio de sesión mediante inicio de sesión único (SSO) con Azure AD].</span><span class="sxs-lookup"><span data-stu-id="a7916-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="a7916-172">b.</span><span class="sxs-lookup"><span data-stu-id="a7916-172">b.</span></span> <span data-ttu-id="a7916-173">En el cuadro de texto **Identity Provider Endpoint** (Punto de conexión del proveedor de identidades), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a7916-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="a7916-174">c.</span><span class="sxs-lookup"><span data-stu-id="a7916-174">c.</span></span>  <span data-ttu-id="a7916-175">Abra el **certificado codificado en Base 64** que descargó de Azure Portal en el **Bloc de notas**, copie el contenido y, luego, péguelo en el cuadro de texto **X.509 Certificate** (Certificado X.509).</span><span class="sxs-lookup"><span data-stu-id="a7916-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="a7916-176">d.</span><span class="sxs-lookup"><span data-stu-id="a7916-176">d.</span></span>  <span data-ttu-id="a7916-177">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a7916-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a7916-178">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7916-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7916-179">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a7916-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7916-180">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7916-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a7916-181">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7916-181">Create an Azure AD test user</span></span>
<span data-ttu-id="a7916-182">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a7916-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="a7916-184">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="a7916-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7916-185">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7916-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7916-187">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a7916-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7916-189">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a7916-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7916-191">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a7916-191">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7916-193">a.</span><span class="sxs-lookup"><span data-stu-id="a7916-193">a.</span></span> <span data-ttu-id="a7916-194">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7916-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7916-195">b.</span><span class="sxs-lookup"><span data-stu-id="a7916-195">b.</span></span> <span data-ttu-id="a7916-196">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7916-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7916-197">c.</span><span class="sxs-lookup"><span data-stu-id="a7916-197">c.</span></span> <span data-ttu-id="a7916-198">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a7916-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7916-199">d.</span><span class="sxs-lookup"><span data-stu-id="a7916-199">d.</span></span> <span data-ttu-id="a7916-200">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a7916-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="a7916-201">Creación de un usuario de prueba de ClickTime</span><span class="sxs-lookup"><span data-stu-id="a7916-201">Create a ClickTime test user</span></span>

<span data-ttu-id="a7916-202">Para permitir que los usuarios de Azure AD inicien sesión en ClickTime, deben aprovisionarse en ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7916-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="a7916-203">En el caso de ClickTime, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="a7916-203">In the case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="a7916-204">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de ClickTime ofrecida por ClickTime para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7916-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>

<span data-ttu-id="a7916-205">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="a7916-205">**To provision a user account, perform the following steps:**</span></span>
1. <span data-ttu-id="a7916-206">Inicie sesión en su inquilino de **ClickTime** .</span><span class="sxs-lookup"><span data-stu-id="a7916-206">Log in to your **ClickTime** tenant.</span></span>
2. <span data-ttu-id="a7916-207">En la barra de herramientas de la parte superior, haga clic en **Compañía** y, luego, en **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="a7916-207">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="a7916-208">![Personas](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="a7916-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="a7916-209">Haga clic en **Add Person**(Agregar persona).</span><span class="sxs-lookup"><span data-stu-id="a7916-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="a7916-210">![Agregar persona](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Agregar persona")</span><span class="sxs-lookup"><span data-stu-id="a7916-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="a7916-211">En la sección New Person (Nueva persona), lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a7916-211">In the New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="a7916-212">![Personas](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="a7916-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="a7916-213">a.</span><span class="sxs-lookup"><span data-stu-id="a7916-213">a.</span></span>  <span data-ttu-id="a7916-214">En el cuadro de texto de **nombre completo**, escriba el nombre completo de un usuario, por ejemplo, **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a7916-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="a7916-215">b.</span><span class="sxs-lookup"><span data-stu-id="a7916-215">b.</span></span>  <span data-ttu-id="a7916-216">En el cuadro de texto de **correo electrónico**, escriba la dirección de correo electrónico de un usuario, por ejemplo, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a7916-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="a7916-217">Si lo desea, puede establecer propiedades adicionales del nuevo objeto persona.</span><span class="sxs-lookup"><span data-stu-id="a7916-217">If you want to, you can set additional properties of the new person object.</span></span>
   
    <span data-ttu-id="a7916-218">c.</span><span class="sxs-lookup"><span data-stu-id="a7916-218">c.</span></span>  <span data-ttu-id="a7916-219">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a7916-219">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a7916-220">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7916-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="a7916-221">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7916-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="a7916-223">**Para asignar a Britta Simon a ClickTime, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="a7916-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="a7916-224">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a7916-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a7916-226">En la lista de aplicaciones, seleccione **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="a7916-226">In the applications list, select **ClickTime**.</span></span>

    ![Vínculo a ClickTime en la lista de aplicaciones](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="a7916-228">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a7916-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="a7916-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a7916-230">Click **Add** button.</span></span> <span data-ttu-id="a7916-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a7916-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="a7916-233">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="a7916-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a7916-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a7916-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7916-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a7916-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a7916-236">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a7916-236">Test single sign-on</span></span>

<span data-ttu-id="a7916-237">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a7916-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a7916-238">Al hacer clic en el icono de ClickTime en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación ClickTime.</span><span class="sxs-lookup"><span data-stu-id="a7916-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>
<span data-ttu-id="a7916-239">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a7916-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7916-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a7916-240">Additional resources</span></span>

* [<span data-ttu-id="a7916-241">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7916-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7916-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7916-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

