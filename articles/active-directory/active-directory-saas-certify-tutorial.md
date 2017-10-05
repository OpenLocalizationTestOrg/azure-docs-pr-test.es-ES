---
title: "Tutorial: integración de Azure Active Directory con Certify | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Certify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bbb2357d17535de438555a0b1f8256b134c8a40e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="07d65-103">Tutorial: integración de Azure Active Directory con Certify</span><span class="sxs-lookup"><span data-stu-id="07d65-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="07d65-104">En este tutorial, aprenderá a integrar Certify con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07d65-104">In this tutorial, you learn how to integrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07d65-105">La integración de Certify con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="07d65-105">Integrating Certify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07d65-106">Puede controlar en Azure AD quién tiene acceso a Certify.</span><span class="sxs-lookup"><span data-stu-id="07d65-106">You can control in Azure AD who has access to Certify</span></span>
- <span data-ttu-id="07d65-107">Puede permitir que los usuarios inicien sesión automáticamente en Certify (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07d65-107">You can enable your users to automatically get signed-on to Certify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07d65-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="07d65-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="07d65-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07d65-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07d65-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="07d65-110">Prerequisites</span></span>

<span data-ttu-id="07d65-111">Para configurar la integración de Azure AD con Certify, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="07d65-111">To configure Azure AD integration with Certify, you need the following items:</span></span>

- <span data-ttu-id="07d65-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07d65-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07d65-113">Una suscripción habilitada para el inicio de sesión único en Certify</span><span class="sxs-lookup"><span data-stu-id="07d65-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07d65-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="07d65-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07d65-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="07d65-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07d65-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="07d65-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07d65-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07d65-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07d65-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="07d65-118">Scenario description</span></span>
<span data-ttu-id="07d65-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="07d65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07d65-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="07d65-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07d65-121">Incorporación de Certify desde la galería</span><span class="sxs-lookup"><span data-stu-id="07d65-121">Adding Certify from the gallery</span></span>
2. <span data-ttu-id="07d65-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07d65-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-the-gallery"></a><span data-ttu-id="07d65-123">Incorporación de Certify desde la galería</span><span class="sxs-lookup"><span data-stu-id="07d65-123">Adding Certify from the gallery</span></span>
<span data-ttu-id="07d65-124">Para configurar la integración de Certify en Azure AD, deberá agregar Certify desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="07d65-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07d65-125">**Para agregar Certify desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="07d65-125">**To add Certify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07d65-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07d65-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07d65-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="07d65-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07d65-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="07d65-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="07d65-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07d65-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="07d65-133">En el cuadro de búsqueda, escriba **Certify**.</span><span class="sxs-lookup"><span data-stu-id="07d65-133">In the search box, type **Certify**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="07d65-135">En el panel de resultados, seleccione **Certify** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07d65-135">In the results panel, select **Certify**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07d65-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07d65-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07d65-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Certify con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07d65-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07d65-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Certify para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07d65-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Certify is to a user in Azure AD.</span></span> <span data-ttu-id="07d65-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Certify.</span><span class="sxs-lookup"><span data-stu-id="07d65-140">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span></span>

<span data-ttu-id="07d65-141">Para establecer la relación de vínculo, en Certify, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="07d65-141">In Certify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="07d65-142">Para configurar y probar el inicio de sesión único de Azure AD con Certify, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="07d65-142">To configure and test Azure AD single sign-on with Certify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07d65-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="07d65-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07d65-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07d65-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07d65-145">**[Creación de un usuario de prueba de Certify](#creating-a-certify-test-user)**: para tener un homólogo de Britta Simon en Certify que esté vinculado a la representación en Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="07d65-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07d65-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07d65-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07d65-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="07d65-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07d65-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07d65-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07d65-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Certify.</span><span class="sxs-lookup"><span data-stu-id="07d65-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="07d65-150">**Para configurar el inicio de sesión único de Azure AD con Certify, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="07d65-150">**To configure Azure AD single sign-on with Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="07d65-151">En Azure Portal, en la página de integración de la aplicación **Certify**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="07d65-151">In the Azure portal, on the **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="07d65-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="07d65-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="07d65-155">En la sección **Dominio y direcciones URL de Certify**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="07d65-155">On the **Certify Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="07d65-157">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="07d65-157">In the **Identifier** textbox, type the URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="07d65-158">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (sin procesar)** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="07d65-158">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="07d65-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="07d65-160">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="07d65-162">En la sección **Configuración de Certify**, haga clic en **Configurar Certify** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="07d65-162">On the **Certify Configuration** section, click **Configure Certify** to open **Configure sign-on** window.</span></span> <span data-ttu-id="07d65-163">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="07d65-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="07d65-165">Para configurar el inicio de sesión único en **Certify**, es preciso enviar los valores descargados de **Certificado (sin procesar)**, **Sign-Out URL (Dirección URL de cierre de sesión), SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="07d65-165">To configure single sign-on on **Certify** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="07d65-166">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="07d65-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="07d65-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="07d65-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07d65-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="07d65-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07d65-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07d65-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07d65-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07d65-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="07d65-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07d65-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="07d65-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="07d65-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07d65-174">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07d65-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07d65-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="07d65-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07d65-178">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07d65-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07d65-180">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="07d65-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07d65-182">a.</span><span class="sxs-lookup"><span data-stu-id="07d65-182">a.</span></span> <span data-ttu-id="07d65-183">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07d65-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07d65-184">b.</span><span class="sxs-lookup"><span data-stu-id="07d65-184">b.</span></span> <span data-ttu-id="07d65-185">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07d65-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="07d65-186">c.</span><span class="sxs-lookup"><span data-stu-id="07d65-186">c.</span></span> <span data-ttu-id="07d65-187">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="07d65-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="07d65-188">d.</span><span class="sxs-lookup"><span data-stu-id="07d65-188">d.</span></span> <span data-ttu-id="07d65-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="07d65-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="07d65-190">Creación de un usuario de prueba de Certify</span><span class="sxs-lookup"><span data-stu-id="07d65-190">Creating a Certify test user</span></span>

<span data-ttu-id="07d65-191">El objetivo de esta sección es crear una usuaria llamada Britta Simon en Certify.</span><span class="sxs-lookup"><span data-stu-id="07d65-191">The objective of this section is to create a user called Britta Simon in Certify.</span></span> <span data-ttu-id="07d65-192">Certify admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="07d65-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="07d65-193">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="07d65-193">There is no action item for you in this section.</span></span> <span data-ttu-id="07d65-194">Durante un intento de acceder a Certify se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="07d65-194">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="07d65-195">Si necesita crear manualmente un usuario, debe ponerse en contacto con el [equipo de soporte técnico de Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="07d65-195">If you need to create an user manually, you need to contact the [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="07d65-196">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="07d65-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="07d65-197">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Certify.</span><span class="sxs-lookup"><span data-stu-id="07d65-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certify.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="07d65-199">**Para asignar a Britta Simon a Certify, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="07d65-199">**To assign Britta Simon to Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="07d65-200">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="07d65-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="07d65-202">En la lista de aplicaciones, seleccione **Certify**.</span><span class="sxs-lookup"><span data-stu-id="07d65-202">In the applications list, select **Certify**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="07d65-204">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="07d65-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="07d65-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="07d65-206">Click **Add** button.</span></span> <span data-ttu-id="07d65-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="07d65-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="07d65-209">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="07d65-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07d65-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="07d65-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07d65-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="07d65-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07d65-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="07d65-212">Testing single sign-on</span></span>

<span data-ttu-id="07d65-213">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="07d65-213">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="07d65-214">Al hacer clic en el icono de Certify en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Certify.</span><span class="sxs-lookup"><span data-stu-id="07d65-214">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07d65-215">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="07d65-215">Additional resources</span></span>

* [<span data-ttu-id="07d65-216">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07d65-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07d65-217">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07d65-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png

