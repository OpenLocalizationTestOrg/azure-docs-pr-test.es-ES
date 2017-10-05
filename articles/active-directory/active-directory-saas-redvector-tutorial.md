---
title: "Tutorial: Integración de Azure Active Directory con RedVector | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y RedVector."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99042f39-0ab2-475b-8df8-3016d7f875e9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: d7aedd360ba1d4c11da210f8fae7be6035007c22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-redvector"></a><span data-ttu-id="235b2-103">Tutorial: integración de Azure Active Directory con RedVector</span><span class="sxs-lookup"><span data-stu-id="235b2-103">Tutorial: Azure Active Directory integration with RedVector</span></span>

<span data-ttu-id="235b2-104">En este tutorial, aprenderá a integrar RedVector con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="235b2-104">In this tutorial, you learn how to integrate RedVector with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="235b2-105">La integración de RedVector con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="235b2-105">Integrating RedVector with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="235b2-106">Puede controlar en Azure AD quién tiene acceso a RedVector.</span><span class="sxs-lookup"><span data-stu-id="235b2-106">You can control in Azure AD who has access to RedVector</span></span>
- <span data-ttu-id="235b2-107">Puede habilitar que los usuarios inicien sesión automáticamente en RedVector (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="235b2-107">You can enable your users to automatically get signed-on to RedVector (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="235b2-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="235b2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="235b2-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="235b2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="235b2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="235b2-110">Prerequisites</span></span>

<span data-ttu-id="235b2-111">Para configurar la integración de Azure AD con RedVector, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="235b2-111">To configure Azure AD integration with RedVector, you need the following items:</span></span>

- <span data-ttu-id="235b2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="235b2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="235b2-113">Una suscripción habilitada para el inicio de sesión único en RedVector</span><span class="sxs-lookup"><span data-stu-id="235b2-113">A RedVector single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="235b2-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="235b2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="235b2-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="235b2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="235b2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="235b2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="235b2-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="235b2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="235b2-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="235b2-118">Scenario description</span></span>
<span data-ttu-id="235b2-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="235b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="235b2-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="235b2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="235b2-121">Adición de RedVector desde la galería</span><span class="sxs-lookup"><span data-stu-id="235b2-121">Adding RedVector from the gallery</span></span>
2. <span data-ttu-id="235b2-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="235b2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-redvector-from-the-gallery"></a><span data-ttu-id="235b2-123">Adición de RedVector desde la galería</span><span class="sxs-lookup"><span data-stu-id="235b2-123">Adding RedVector from the gallery</span></span>
<span data-ttu-id="235b2-124">Para configurar la integración de RedVector en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="235b2-124">To configure the integration of RedVector into Azure AD, you need to add RedVector from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="235b2-125">**Para agregar RedVector desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="235b2-125">**To add RedVector from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="235b2-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="235b2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="235b2-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="235b2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="235b2-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="235b2-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="235b2-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="235b2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="235b2-133">En el cuadro de búsqueda, escriba **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="235b2-133">In the search box, type **RedVector**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_search.png)

5. <span data-ttu-id="235b2-135">En el panel de resultados, seleccione **RedVector** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="235b2-135">In the results panel, select **RedVector**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="235b2-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="235b2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="235b2-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con RedVector con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="235b2-138">In this section, you configure and test Azure AD single sign-on with RedVector based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="235b2-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de RedVector para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="235b2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RedVector is to a user in Azure AD.</span></span> <span data-ttu-id="235b2-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de RedVector.</span><span class="sxs-lookup"><span data-stu-id="235b2-140">In other words, a link relationship between an Azure AD user and the related user in RedVector needs to be established.</span></span>

<span data-ttu-id="235b2-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de RedVector.</span><span class="sxs-lookup"><span data-stu-id="235b2-141">In RedVector, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="235b2-142">Para configurar y probar el inicio de sesión único de Azure AD con RedVector, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="235b2-142">To configure and test Azure AD single sign-on with RedVector, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="235b2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="235b2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="235b2-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="235b2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="235b2-145">**[Creación de un usuario de prueba en RedVector](#creating-a-redvector-test-user)**: el objetivo es tener un homólogo de Britta Simon en RedVector que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="235b2-145">**[Creating a RedVector test user](#creating-a-redvector-test-user)** - to have a counterpart of Britta Simon in RedVector that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="235b2-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="235b2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="235b2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="235b2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="235b2-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="235b2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="235b2-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación RedVector.</span><span class="sxs-lookup"><span data-stu-id="235b2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RedVector application.</span></span>

<span data-ttu-id="235b2-150">**Para configurar el inicio de sesión único de Azure AD con RedVector, soga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="235b2-150">**To configure Azure AD single sign-on with RedVector, perform the following steps:**</span></span>

1. <span data-ttu-id="235b2-151">En la página de integración de la aplicación **RedVector** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="235b2-151">In the Azure portal, on the **RedVector** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="235b2-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="235b2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_samlbase.png)

3. <span data-ttu-id="235b2-155">En la sección **Dominio y direcciones URL de RedVector**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="235b2-155">On the **RedVector Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_url.png)

    <span data-ttu-id="235b2-157">a.</span><span class="sxs-lookup"><span data-stu-id="235b2-157">a.</span></span> <span data-ttu-id="235b2-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://sso2.redvector.com/adfs/<Companyname>`.</span><span class="sxs-lookup"><span data-stu-id="235b2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso2.redvector.com/adfs/<Companyname>`</span></span>

    <span data-ttu-id="235b2-159">b.</span><span class="sxs-lookup"><span data-stu-id="235b2-159">b.</span></span> <span data-ttu-id="235b2-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<Companyname>.redvector.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="235b2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Companyname>.redvector.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="235b2-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="235b2-161">These values are not real.</span></span> <span data-ttu-id="235b2-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="235b2-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="235b2-163">Póngase en contacto con el [equipo de atención al cliente de RedVector](mailto:sso@redvector.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="235b2-163">Contact [RedVector Client support team](mailto:sso@redvector.com) to get these values.</span></span> 
 
4. <span data-ttu-id="235b2-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="235b2-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_certificate.png) 

5. <span data-ttu-id="235b2-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="235b2-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-redvector-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="235b2-168">En la sección **Configuración de RedVector**, haga clic en **Configurar RedVector** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="235b2-168">On the **RedVector Configuration** section, click **Configure RedVector** to open **Configure sign-on** window.</span></span> <span data-ttu-id="235b2-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="235b2-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_configure.png) 

7. <span data-ttu-id="235b2-171">Para configurar el inicio de sesión único en **RedVector**, es preciso enviar el **certificado (Base64)** descargado y la **dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de RedVector](mailto:sso@redvector.com).</span><span class="sxs-lookup"><span data-stu-id="235b2-171">To configure single sign-on on **RedVector** side, you need to send the downloaded **Certificate (Base64)** and **SAML Single Sign-On Service URL** to [RedVector support team](mailto:sso@redvector.com).</span></span> <span data-ttu-id="235b2-172">Ellos se encargan de realizar esta configuración para que la conexión de SSO de SAML esté establecida correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="235b2-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="235b2-173">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="235b2-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="235b2-174">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="235b2-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="235b2-175">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="235b2-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="235b2-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="235b2-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="235b2-177">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="235b2-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="235b2-179">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="235b2-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="235b2-180">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="235b2-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="235b2-182">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="235b2-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="235b2-184">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="235b2-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="235b2-186">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="235b2-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="235b2-188">a.</span><span class="sxs-lookup"><span data-stu-id="235b2-188">a.</span></span> <span data-ttu-id="235b2-189">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="235b2-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="235b2-190">b.</span><span class="sxs-lookup"><span data-stu-id="235b2-190">b.</span></span> <span data-ttu-id="235b2-191">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="235b2-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="235b2-192">c.</span><span class="sxs-lookup"><span data-stu-id="235b2-192">c.</span></span> <span data-ttu-id="235b2-193">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="235b2-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="235b2-194">d.</span><span class="sxs-lookup"><span data-stu-id="235b2-194">d.</span></span> <span data-ttu-id="235b2-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="235b2-195">Click **Create**.</span></span>
 
### <a name="creating-a-redvector-test-user"></a><span data-ttu-id="235b2-196">Creación de un usuario de prueba en RedVector</span><span class="sxs-lookup"><span data-stu-id="235b2-196">Creating a RedVector test user</span></span>

<span data-ttu-id="235b2-197">En esta sección, se crea un usuario denominado Britta Simon en RedVector.</span><span class="sxs-lookup"><span data-stu-id="235b2-197">In this section, you create a user called Britta Simon in RedVector.</span></span> <span data-ttu-id="235b2-198">Si no sabe cómo agregar Britta Simon en RedVector, colabore con el [equipo de soporte técnico de RedVector](mailto:sso@redvector.com) para agregar el usuario de prueba y habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="235b2-198">If you don't know how to add Britta Simon in RedVector, Work with [RedVector support team](mailto:sso@redvector.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="235b2-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="235b2-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="235b2-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a RedVector.</span><span class="sxs-lookup"><span data-stu-id="235b2-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RedVector.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="235b2-202">**Para asignar a Britta Simon a RedVector, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="235b2-202">**To assign Britta Simon to RedVector, perform the following steps:**</span></span>

1. <span data-ttu-id="235b2-203">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="235b2-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="235b2-205">En la lista de aplicaciones, seleccione **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="235b2-205">In the applications list, select **RedVector**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_app.png) 

3. <span data-ttu-id="235b2-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="235b2-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="235b2-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="235b2-209">Click **Add** button.</span></span> <span data-ttu-id="235b2-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="235b2-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="235b2-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="235b2-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="235b2-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="235b2-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="235b2-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="235b2-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="235b2-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="235b2-215">Testing single sign-on</span></span>

<span data-ttu-id="235b2-216">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="235b2-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="235b2-217">Al hacer clic en el icono de RedVector en el Panel de acceso, debería iniciar sesión automáticamente en dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="235b2-217">When you click the RedVector tile in the Access Panel, you should get automatically signed-on to your RedVector application..</span></span>

## <a name="additional-resources"></a><span data-ttu-id="235b2-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="235b2-218">Additional resources</span></span>

* [<span data-ttu-id="235b2-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="235b2-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="235b2-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="235b2-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_203.png

