---
title: "Tutorial: Integración de Azure Active Directory con Wingspan eTMF | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Wingspan eTMF."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 8c76fb64229abcad0cabb910e7c170979a79d839
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="64345-103">Tutorial: Integración de Azure Active Directory con Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="64345-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="64345-104">En este tutorial, aprenderá a integrar Wingspan eTMF con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64345-104">In this tutorial, you learn how to integrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64345-105">La integración de Wingspan eTMF con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="64345-105">Integrating Wingspan eTMF with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="64345-106">Puede controlar en Azure AD quién tiene acceso a Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="64345-106">You can control in Azure AD who has access to Wingspan eTMF</span></span>
- <span data-ttu-id="64345-107">Puede permitir que los usuarios inicien sesión automáticamente en Wingspan eTMF (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64345-107">You can enable your users to automatically get signed-on to Wingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64345-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="64345-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="64345-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64345-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64345-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="64345-110">Prerequisites</span></span>

<span data-ttu-id="64345-111">Para configurar la integración de Azure AD con Wingspan eTMF, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="64345-111">To configure Azure AD integration with Wingspan eTMF, you need the following items:</span></span>

- <span data-ttu-id="64345-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64345-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64345-113">Una suscripción habilitada para inicio de sesión único en Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="64345-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64345-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="64345-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64345-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="64345-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64345-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="64345-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64345-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64345-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64345-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="64345-118">Scenario description</span></span>
<span data-ttu-id="64345-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="64345-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64345-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="64345-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64345-121">Agregar Wingspan eTMF desde la galería</span><span class="sxs-lookup"><span data-stu-id="64345-121">Adding Wingspan eTMF from the gallery</span></span>
2. <span data-ttu-id="64345-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64345-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-the-gallery"></a><span data-ttu-id="64345-123">Agregar Wingspan eTMF desde la galería</span><span class="sxs-lookup"><span data-stu-id="64345-123">Adding Wingspan eTMF from the gallery</span></span>
<span data-ttu-id="64345-124">Para configurar la integración de Wingspan eTMF en Azure AD, debe agregar Wingspan eTMF desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="64345-124">To configure the integration of Wingspan eTMF into Azure AD, you need to add Wingspan eTMF from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="64345-125">**Para agregar Wingspan eTMF desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="64345-125">**To add Wingspan eTMF from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="64345-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64345-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="64345-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="64345-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="64345-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="64345-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="64345-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64345-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="64345-133">En el cuadro de búsqueda, escriba **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="64345-133">In the search box, type **Wingspan eTMF**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

5. <span data-ttu-id="64345-135">En el panel de resultados, seleccione **Wingspan eTMF** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64345-135">In the results panel, select **Wingspan eTMF**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="64345-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64345-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="64345-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Wingspan eTMF con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="64345-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="64345-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Wingspan eTMF para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64345-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wingspan eTMF is to a user in Azure AD.</span></span> <span data-ttu-id="64345-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="64345-140">In other words, a link relationship between an Azure AD user and the related user in Wingspan eTMF needs to be established.</span></span>

<span data-ttu-id="64345-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="64345-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="64345-142">Para configurar y probar el inicio de sesión único de Azure AD con Wingspan eTMF, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="64345-142">To configure and test Azure AD single sign-on with Wingspan eTMF, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="64345-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="64345-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="64345-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64345-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64345-145">**[Creación de un usuario de prueba de Wingspan eTMF](#creating-a-wingspan-etmf-test-user)**: para tener un homólogo de Britta Simon en Wingspan eTMF que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="64345-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - to have a counterpart of Britta Simon in Wingspan eTMF that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="64345-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64345-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64345-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="64345-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="64345-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64345-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="64345-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="64345-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="64345-150">**Para configurar el inicio de sesión único de Azure AD con Wingspan eTMF, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="64345-150">**To configure Azure AD single sign-on with Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="64345-151">En Azure Portal, en la página de integración de la aplicación **Wingspan eTMF**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="64345-151">In the Azure portal, on the **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="64345-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="64345-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

3. <span data-ttu-id="64345-155">En la sección **Dominio y direcciones URL de Wingspan eTMF**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="64345-155">On the **Wingspan eTMF Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="64345-157">a.</span><span class="sxs-lookup"><span data-stu-id="64345-157">a.</span></span> <span data-ttu-id="64345-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<customer name>.<instance name>.mywingspan.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="64345-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="64345-159">b.</span><span class="sxs-lookup"><span data-stu-id="64345-159">b.</span></span> <span data-ttu-id="64345-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="64345-160">In the **Identifier** textbox, type a URL using the following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="64345-161">c.</span><span class="sxs-lookup"><span data-stu-id="64345-161">c.</span></span> <span data-ttu-id="64345-162">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<customer name>.<instance name>.mywingspan.com/`.</span><span class="sxs-lookup"><span data-stu-id="64345-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="64345-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="64345-163">These values are not the real.</span></span> <span data-ttu-id="64345-164">Actualice estos valores con los valores reales de la dirección URL de inicio de sesión, el identificador y la dirección URL de respuesta, incluidos el nombre de cliente y el nombre de instancia reales.</span><span class="sxs-lookup"><span data-stu-id="64345-164">Update these values with the actual Sign-On URL, Identifier and Reply URL including the actual customer name and instance name.</span></span> <span data-ttu-id="64345-165">Póngase en contacto con el [equipo de soporte técnico de Wingspan eTMF](http://www.wingspan.com/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="64345-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="64345-166">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="64345-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

5. <span data-ttu-id="64345-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="64345-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="64345-170">Para configurar el inicio de sesión único en el lado de **Wingspan eTMF**, debe enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Wingspan eTMF](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="64345-170">To configure single sign-on on **Wingspan eTMF** side, you need to send the downloaded **Metadata XML** to [Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="64345-171">Ellos lo configuran para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="64345-171">They set this up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="64345-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64345-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="64345-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="64345-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="64345-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64345-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="64345-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64345-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="64345-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="64345-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="64345-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="64345-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="64345-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64345-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64345-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="64345-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64345-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64345-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64345-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="64345-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64345-187">a.</span><span class="sxs-lookup"><span data-stu-id="64345-187">a.</span></span> <span data-ttu-id="64345-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64345-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64345-189">b.</span><span class="sxs-lookup"><span data-stu-id="64345-189">b.</span></span> <span data-ttu-id="64345-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64345-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64345-191">c.</span><span class="sxs-lookup"><span data-stu-id="64345-191">c.</span></span> <span data-ttu-id="64345-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="64345-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="64345-193">d.</span><span class="sxs-lookup"><span data-stu-id="64345-193">d.</span></span> <span data-ttu-id="64345-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="64345-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="64345-195">Crear un usuario de prueba de Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="64345-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="64345-196">En esta sección, creará un usuario llamado Britta Simon en Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="64345-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="64345-197">Trabaje con el [equipo de soporte técnico de Wingspan eTMF](http://www.wingspan.com/contact-us/) para agregar los usuarios a la aplicación de Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="64345-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) to add the users in the Wingspan eTMF application.</span></span> <span data-ttu-id="64345-198">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="64345-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="64345-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64345-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="64345-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="64345-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wingspan eTMF.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="64345-202">**Para asignar a Britta Simon a Wingspan eTMF, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="64345-202">**To assign Britta Simon to Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="64345-203">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="64345-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="64345-205">En la lista de aplicaciones, seleccione **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="64345-205">In the applications list, select **Wingspan eTMF**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

3. <span data-ttu-id="64345-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="64345-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="64345-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="64345-209">Click **Add** button.</span></span> <span data-ttu-id="64345-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="64345-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="64345-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="64345-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="64345-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="64345-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64345-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="64345-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="64345-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="64345-215">Testing single sign-on</span></span>

<span data-ttu-id="64345-216">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="64345-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="64345-217">Haga clic en el icono de Wingspan eTMF en el panel de acceso y después se le redirigirá a la página de inicio de sesión de la organización.</span><span class="sxs-lookup"><span data-stu-id="64345-217">Click the Wingspan eTMF tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="64345-218">Después de registrarse correctamente, iniciará sesión en la aplicación Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="64345-218">After successful login, you will be signed-on to your Wingspan eTMF application.</span></span> <span data-ttu-id="64345-219">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="64345-219">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64345-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="64345-220">Additional resources</span></span>

* [<span data-ttu-id="64345-221">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64345-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64345-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64345-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_203.png

