---
title: "Tutorial: Integración de Azure Active Directory con Bime | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Bime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 8f46ff1265d302ab114747b4b45227e58718166b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="9ec14-103">Tutorial: Integración de Azure Active Directory con Bime</span><span class="sxs-lookup"><span data-stu-id="9ec14-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="9ec14-104">En este tutorial, obtendrá información sobre cómo integrar Bime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9ec14-104">In this tutorial, you learn how to integrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ec14-105">La integración de Bime con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9ec14-105">Integrating Bime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9ec14-106">Puede controlar en Azure AD quién tiene acceso a Bime</span><span class="sxs-lookup"><span data-stu-id="9ec14-106">You can control in Azure AD who has access to Bime</span></span>
- <span data-ttu-id="9ec14-107">Puede permitir que los usuarios inicien sesión automáticamente en Bime (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ec14-107">You can enable your users to automatically get signed-on to Bime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ec14-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9ec14-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9ec14-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ec14-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ec14-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9ec14-110">Prerequisites</span></span>

<span data-ttu-id="9ec14-111">Para configurar la integración de Azure AD con Bime, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9ec14-111">To configure Azure AD integration with Bime, you need the following items:</span></span>

- <span data-ttu-id="9ec14-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ec14-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9ec14-113">Una suscripción a Bime con el inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="9ec14-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ec14-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9ec14-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ec14-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9ec14-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ec14-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9ec14-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9ec14-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ec14-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ec14-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9ec14-118">Scenario description</span></span>
<span data-ttu-id="9ec14-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9ec14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ec14-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9ec14-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ec14-121">Adición de Bime desde la galería</span><span class="sxs-lookup"><span data-stu-id="9ec14-121">Adding Bime from the gallery</span></span>
2. <span data-ttu-id="9ec14-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ec14-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-the-gallery"></a><span data-ttu-id="9ec14-123">Adición de Bime desde la galería</span><span class="sxs-lookup"><span data-stu-id="9ec14-123">Adding Bime from the gallery</span></span>
<span data-ttu-id="9ec14-124">Para configurar la integración de Bime en Azure AD, es preciso agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9ec14-124">To configure the integration of Bime into Azure AD, you need to add Bime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9ec14-125">**Para agregar Bime desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9ec14-125">**To add Bime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9ec14-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9ec14-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9ec14-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9ec14-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ec14-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9ec14-133">En el cuadro de búsqueda, escriba **Bime**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-133">In the search box, type **Bime**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="9ec14-135">En el panel de resultados, seleccione **Bime** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ec14-135">In the results panel, select **Bime**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9ec14-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ec14-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9ec14-138">En esta sección, se configura y prueba el inicio de sesión único de Azure AD con Bime con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9ec14-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ec14-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Bime para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ec14-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bime is to a user in Azure AD.</span></span> <span data-ttu-id="9ec14-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Bime.</span><span class="sxs-lookup"><span data-stu-id="9ec14-140">In other words, a link relationship between an Azure AD user and the related user in Bime needs to be established.</span></span>

<span data-ttu-id="9ec14-141">Para establecer la relación de vínculo, en Bime, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-141">In Bime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9ec14-142">Para configurar y probar el inicio de sesión único de Azure AD con Bime, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9ec14-142">To configure and test Azure AD single sign-on with Bime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9ec14-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9ec14-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9ec14-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ec14-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ec14-145">**[Creación de un usuario de prueba de Bime](#creating-a-bime-test-user)**: para tener un homólogo de Britta Simon en Bime que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="9ec14-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - to have a counterpart of Britta Simon in Bime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ec14-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ec14-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ec14-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9ec14-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9ec14-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ec14-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9ec14-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Bime.</span><span class="sxs-lookup"><span data-stu-id="9ec14-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="9ec14-150">**Para configurar el inicio de sesión único de Azure AD con Bime, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9ec14-150">**To configure Azure AD single sign-on with Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="9ec14-151">En Azure Portal, en la página de integración de la aplicación **Bime**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-151">In the Azure portal, on the **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9ec14-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9ec14-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="9ec14-155">En la sección **Dominio y direcciones URL de Bime**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9ec14-155">On the **Bime Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="9ec14-157">a.</span><span class="sxs-lookup"><span data-stu-id="9ec14-157">a.</span></span> <span data-ttu-id="9ec14-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.Bimeapp.com`.</span><span class="sxs-lookup"><span data-stu-id="9ec14-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="9ec14-159">b.</span><span class="sxs-lookup"><span data-stu-id="9ec14-159">b.</span></span> <span data-ttu-id="9ec14-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="9ec14-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9ec14-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9ec14-161">These values are not real.</span></span> <span data-ttu-id="9ec14-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9ec14-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9ec14-163">Póngase en contacto con el [equipo de soporte de cliente de Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="9ec14-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) to get these values.</span></span> 
 
4. <span data-ttu-id="9ec14-164">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="9ec14-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="9ec14-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9ec14-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9ec14-168">En la sección **Configuración de Bime**, haga clic en **Configurar Bime** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-168">On the **Bime Configuration** section, click **Configure Bime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9ec14-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="9ec14-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Bime.</span><span class="sxs-lookup"><span data-stu-id="9ec14-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="9ec14-172">En la barra de herramientas, haga clic en **Admin** y, luego, en **Account** (Cuenta).</span><span class="sxs-lookup"><span data-stu-id="9ec14-172">In the toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="9ec14-173">![Administración](./media/active-directory-saas-bime-tutorial/ic775558.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="9ec14-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="9ec14-174">En la página de configuración de la cuenta, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9ec14-174">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="9ec14-175">![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/ic775559.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="9ec14-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="9ec14-176">a.</span><span class="sxs-lookup"><span data-stu-id="9ec14-176">a.</span></span> <span data-ttu-id="9ec14-177">Seleccione **Enable SAML authentication** (Habilitar autenticación SAML).</span><span class="sxs-lookup"><span data-stu-id="9ec14-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="9ec14-178">b.</span><span class="sxs-lookup"><span data-stu-id="9ec14-178">b.</span></span> <span data-ttu-id="9ec14-179">En el cuadro de texto **Remote Login URL** (Dirección URL de inicio de sesión remoto), pegue el valor de **Dirección URL de servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9ec14-179">In the **Remote Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9ec14-180">c.</span><span class="sxs-lookup"><span data-stu-id="9ec14-180">c.</span></span>  <span data-ttu-id="9ec14-181">Pegue el valor de **Huella digital** de Azure Portal en el cuadro de texto **Certificate fingerprint** (Huella digital de certificado).</span><span class="sxs-lookup"><span data-stu-id="9ec14-181">Paste the **Thumbprint** value from Azure portal into the **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="9ec14-182">d.</span><span class="sxs-lookup"><span data-stu-id="9ec14-182">d.</span></span> <span data-ttu-id="9ec14-183">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9ec14-184">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9ec14-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9ec14-185">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9ec14-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9ec14-186">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9ec14-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9ec14-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ec14-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9ec14-188">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9ec14-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9ec14-190">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9ec14-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9ec14-191">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ec14-193">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ec14-195">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ec14-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ec14-197">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9ec14-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ec14-199">a.</span><span class="sxs-lookup"><span data-stu-id="9ec14-199">a.</span></span> <span data-ttu-id="9ec14-200">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ec14-201">b.</span><span class="sxs-lookup"><span data-stu-id="9ec14-201">b.</span></span> <span data-ttu-id="9ec14-202">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ec14-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ec14-203">c.</span><span class="sxs-lookup"><span data-stu-id="9ec14-203">c.</span></span> <span data-ttu-id="9ec14-204">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9ec14-205">d.</span><span class="sxs-lookup"><span data-stu-id="9ec14-205">d.</span></span> <span data-ttu-id="9ec14-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="9ec14-207">Creación de usuario de prueba de Bime</span><span class="sxs-lookup"><span data-stu-id="9ec14-207">Creating a Bime test user</span></span>

<span data-ttu-id="9ec14-208">Para permitir que los usuarios de Azure AD inicien sesión en Bime, tienen que aprovisionarse en Bime.</span><span class="sxs-lookup"><span data-stu-id="9ec14-208">In order to enable Azure AD users to log in to Bime, they must be provisioned into Bime.</span></span> <span data-ttu-id="9ec14-209">En el caso de Bime, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9ec14-209">In the case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="9ec14-210">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="9ec14-210">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="9ec14-211">Inicie sesión en su inquilino de **Bime** .</span><span class="sxs-lookup"><span data-stu-id="9ec14-211">Log in to your **Bime** tenant.</span></span>

2. <span data-ttu-id="9ec14-212">En la barra de herramientas, haga clic en **Admin** y, luego, en **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="9ec14-212">In the toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="9ec14-213">![Administración](./media/active-directory-saas-bime-tutorial/ic775561.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="9ec14-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="9ec14-214">En **Users List** (Lista de usuarios), haga clic en **Agregar nuevo usuario** (+).</span><span class="sxs-lookup"><span data-stu-id="9ec14-214">In the **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="9ec14-215">![Usuarios](./media/active-directory-saas-bime-tutorial/ic775562.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="9ec14-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="9ec14-216">En la página de diálogo **User Details** (Detalles del usuario), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9ec14-216">On the **User Details** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="9ec14-217">![Detalles del usuario](./media/active-directory-saas-bime-tutorial/ic775563.png "Detalles del usuario")</span><span class="sxs-lookup"><span data-stu-id="9ec14-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="9ec14-218">a.</span><span class="sxs-lookup"><span data-stu-id="9ec14-218">a.</span></span> <span data-ttu-id="9ec14-219">En el cuadro de texto **Nombre**, escriba el nombre de usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-219">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="9ec14-220">b.</span><span class="sxs-lookup"><span data-stu-id="9ec14-220">b.</span></span> <span data-ttu-id="9ec14-221">En el cuadro de texto **Apellidos**, escriba el apellido del usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-221">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="9ec14-222">c.</span><span class="sxs-lookup"><span data-stu-id="9ec14-222">c.</span></span> <span data-ttu-id="9ec14-223">En el cuadro de texto **E-mail** (Correo electrónico), escriba el correo electrónico del usuario con el siguiente formato **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-223">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="9ec14-224">d.</span><span class="sxs-lookup"><span data-stu-id="9ec14-224">d.</span></span> <span data-ttu-id="9ec14-225">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="9ec14-226">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Bime que proporcione Bime para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="9ec14-226">You can use any other Bime user account creation tools or APIs provided by Bime to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9ec14-227">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ec14-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9ec14-228">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Bime.</span><span class="sxs-lookup"><span data-stu-id="9ec14-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bime.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9ec14-230">**Para asignar Britta Simon a Bime, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="9ec14-230">**To assign Britta Simon to Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="9ec14-231">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9ec14-233">En la lista de aplicaciones, seleccione **Bime**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-233">In the applications list, select **Bime**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="9ec14-235">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9ec14-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-237">Click **Add** button.</span></span> <span data-ttu-id="9ec14-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9ec14-240">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9ec14-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9ec14-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ec14-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9ec14-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9ec14-243">Testing single sign-on</span></span>

<span data-ttu-id="9ec14-244">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9ec14-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9ec14-245">Al hacer clic en el icono de Bime en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Bime.</span><span class="sxs-lookup"><span data-stu-id="9ec14-245">When you click the Bime tile in the Access Panel, you should get automatically signed-on to your Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ec14-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9ec14-246">Additional resources</span></span>

* [<span data-ttu-id="9ec14-247">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ec14-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ec14-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9ec14-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

