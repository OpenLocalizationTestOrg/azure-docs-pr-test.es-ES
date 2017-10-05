---
title: "Tutorial: Integración de Azure Active Directory con Pantheon | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3f4ac1db2ee83d9f9fcb375d0fb7c40ad21c4688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="2a49e-103">Tutorial: Integración de Azure Active Directory con Pantheon</span><span class="sxs-lookup"><span data-stu-id="2a49e-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="2a49e-104">En este tutorial, aprenderá a integrar Pantheon con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2a49e-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a49e-105">La integración de Pantheon con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2a49e-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2a49e-106">Puede controlar en Azure AD quién tiene acceso a Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-106">You can control in Azure AD who has access to Pantheon</span></span>
- <span data-ttu-id="2a49e-107">Puede permitir que los usuarios inicien sesión automáticamente en Pantheon (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a49e-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2a49e-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2a49e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2a49e-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2a49e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a49e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a49e-110">Prerequisites</span></span>

<span data-ttu-id="2a49e-111">Para configurar la integración de Azure AD con Pantheon, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2a49e-111">To configure Azure AD integration with Pantheon, you need the following items:</span></span>

- <span data-ttu-id="2a49e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a49e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2a49e-113">Una suscripción habilitada para el inicio de sesión único en Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2a49e-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2a49e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2a49e-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2a49e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2a49e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2a49e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2a49e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a49e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2a49e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2a49e-118">Scenario description</span></span>
<span data-ttu-id="2a49e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2a49e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a49e-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2a49e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a49e-121">Adición de Pantheon desde la galería</span><span class="sxs-lookup"><span data-stu-id="2a49e-121">Adding Pantheon from the gallery</span></span>
2. <span data-ttu-id="2a49e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a49e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-the-gallery"></a><span data-ttu-id="2a49e-123">Adición de Pantheon desde la galería</span><span class="sxs-lookup"><span data-stu-id="2a49e-123">Adding Pantheon from the gallery</span></span>
<span data-ttu-id="2a49e-124">Para configurar la integración de Pantheon en Azure AD, es preciso agregar Pantheon desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2a49e-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2a49e-125">**Para agregar Pantheon desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2a49e-125">**To add Pantheon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2a49e-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2a49e-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2a49e-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2a49e-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a49e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2a49e-133">En el cuadro de búsqueda, escriba **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-133">In the search box, type **Pantheon**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="2a49e-135">En el panel de resultados, seleccione **Pantheon** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a49e-135">In the results panel, select **Pantheon**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2a49e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a49e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2a49e-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Pantheon con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2a49e-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2a49e-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Pantheon para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a49e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span></span> <span data-ttu-id="2a49e-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-140">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span></span>

<span data-ttu-id="2a49e-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-141">In Pantheon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2a49e-142">Para configurar y probar el inicio de sesión único de Azure AD con Pantheon, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2a49e-142">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2a49e-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="2a49e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2a49e-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2a49e-145">**[Creación de un usuario de prueba de Pantheon](#creating-a-pantheon-test-user)**: el objetivo es tener un homólogo de Britta Simon en Pantheon que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a49e-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2a49e-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a49e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2a49e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2a49e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2a49e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a49e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2a49e-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="2a49e-150">**Para configurar el inicio de sesión único de Azure AD con Pantheon, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2a49e-150">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="2a49e-151">En la página de integración de la aplicación **Pantheon** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-151">In the Azure portal, on the **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2a49e-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2a49e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="2a49e-155">En la sección **Dominio y direcciones URL de Pantheon**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2a49e-155">On the **Pantheon Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="2a49e-157">a.</span><span class="sxs-lookup"><span data-stu-id="2a49e-157">a.</span></span> <span data-ttu-id="2a49e-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="2a49e-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="2a49e-159">b.</span><span class="sxs-lookup"><span data-stu-id="2a49e-159">b.</span></span> <span data-ttu-id="2a49e-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`.</span><span class="sxs-lookup"><span data-stu-id="2a49e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2a49e-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2a49e-161">These values are not real.</span></span> <span data-ttu-id="2a49e-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="2a49e-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2a49e-163">Póngase en contacto con el [equipo de soporte técnico de Pantheon](https://pantheon.io/docs/getting-support/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="2a49e-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) to get these values.</span></span>

4. <span data-ttu-id="2a49e-164">La aplicación Pantheon espera la aserción de SAML en un formato específico, lo que requiere establecer el valor del atributo UserIdentifier con la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="2a49e-164">Pantheon application expects the SAML assertion in specific format, which requires you to set the UserIdentifier attribute value with the user’s email address.</span></span> <span data-ttu-id="2a49e-165">De forma predeterminada, Azure AD usa el valor de UserPrincipalName para el atributo UserIdentifier.</span><span class="sxs-lookup"><span data-stu-id="2a49e-165">By default Azure AD uses the UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="2a49e-166">Para una correcta integración, deberá ajustar este valor para que coincida con la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="2a49e-166">But for successful integration you need to adjust this value to match with user’s email address.</span></span> <span data-ttu-id="2a49e-167">La integración solo funcionará después de realizar la asignación correcta.</span><span class="sxs-lookup"><span data-stu-id="2a49e-167">The integration will only work after doing the correct mapping.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="2a49e-169">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2a49e-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="2a49e-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2a49e-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="2a49e-173">En la sección **Configuración de Pantheon**, haga clic en **Configurar Pantheon** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-173">On the **Pantheon Configuration** section, click **Configure Pantheon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2a49e-174">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="2a49e-176">Para configurar el inicio de sesión único en **Pantheon**, es preciso enviar el **certificado** descargado y la **dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Pantheon](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="2a49e-176">To configure single sign-on on **Pantheon** side, you need to send the downloaded **Certificate** and **SAML Single Sign-On Service URL** to [Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="2a49e-177">También debe proporcionar la información del dominio de correo electrónico y la fecha y hora en que quiere habilitar esta conexión.</span><span class="sxs-lookup"><span data-stu-id="2a49e-177">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span></span> <span data-ttu-id="2a49e-178">Puede encontrar más detalles al respecto [aquí](https://pantheon.io/docs/sso-organizations/).</span><span class="sxs-lookup"><span data-stu-id="2a49e-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="2a49e-179">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a49e-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2a49e-180">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2a49e-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2a49e-181">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2a49e-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2a49e-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a49e-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="2a49e-183">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2a49e-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2a49e-185">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2a49e-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2a49e-186">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2a49e-188">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2a49e-190">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a49e-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2a49e-192">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2a49e-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2a49e-194">a.</span><span class="sxs-lookup"><span data-stu-id="2a49e-194">a.</span></span> <span data-ttu-id="2a49e-195">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2a49e-196">b.</span><span class="sxs-lookup"><span data-stu-id="2a49e-196">b.</span></span> <span data-ttu-id="2a49e-197">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2a49e-198">c.</span><span class="sxs-lookup"><span data-stu-id="2a49e-198">c.</span></span> <span data-ttu-id="2a49e-199">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2a49e-200">d.</span><span class="sxs-lookup"><span data-stu-id="2a49e-200">d.</span></span> <span data-ttu-id="2a49e-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="2a49e-202">Creación de un usuario de prueba de Pantheon</span><span class="sxs-lookup"><span data-stu-id="2a49e-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="2a49e-203">En esta sección, creará un usuario llamado Britta Simon en Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="2a49e-204">Siga los pasos siguientes para agregar el usuario en Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-204">Please follow the below steps to add the user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="2a49e-205">Para que funcione el inicio de sesión único, primero es necesario crear el usuario en Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-205">For SSO to work user needs to be created first in Pantheon.</span></span>

1. <span data-ttu-id="2a49e-206">Inicie sesión en Pantheon con credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="2a49e-206">Login to Pantheon with admin credentials.</span></span>

2. <span data-ttu-id="2a49e-207">Vaya a la página del panel **Organization** (Organización).</span><span class="sxs-lookup"><span data-stu-id="2a49e-207">Navigate to **Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="2a49e-208">Haga clic en **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-208">Click **People**.</span></span>

4. <span data-ttu-id="2a49e-209">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-209">Click **Add user**.</span></span>

5. <span data-ttu-id="2a49e-210">Escriba la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="2a49e-210">Enter the user's email address.</span></span>

6. <span data-ttu-id="2a49e-211">Elija el rol del usuario.</span><span class="sxs-lookup"><span data-stu-id="2a49e-211">Choose the user's role.</span></span>

7. <span data-ttu-id="2a49e-212">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-212">Click **Add user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2a49e-213">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a49e-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2a49e-214">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pantheon.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2a49e-216">**Para asignar a Britta Simon a Pantheon, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2a49e-216">**To assign Britta Simon to Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="2a49e-217">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2a49e-219">En la lista de aplicaciones, seleccione **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-219">In the applications list, select **Pantheon**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="2a49e-221">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2a49e-223">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-223">Click **Add** button.</span></span> <span data-ttu-id="2a49e-224">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2a49e-226">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2a49e-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2a49e-227">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2a49e-228">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2a49e-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2a49e-229">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2a49e-229">Testing single sign-on</span></span>

<span data-ttu-id="2a49e-230">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2a49e-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2a49e-231">Al hacer clic en el icono de Pantheon en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Pantheon.</span><span class="sxs-lookup"><span data-stu-id="2a49e-231">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span></span>
<span data-ttu-id="2a49e-232">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2a49e-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2a49e-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2a49e-233">Additional resources</span></span>

* [<span data-ttu-id="2a49e-234">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a49e-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a49e-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2a49e-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

