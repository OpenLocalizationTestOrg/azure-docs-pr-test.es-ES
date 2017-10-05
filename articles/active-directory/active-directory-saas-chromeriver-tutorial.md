---
title: "Tutorial: Integración de Azure Active Directory con Chromeriver | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Chromeriver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 445c5600-e340-4724-a9cb-3cfaf5770b70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 6ee3316a8258ee27e4fa4ec22badbf4fe047a844
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-chromeriver"></a><span data-ttu-id="f3251-103">Tutorial: integración de Azure Active Directory con Chromeriver</span><span class="sxs-lookup"><span data-stu-id="f3251-103">Tutorial: Azure Active Directory integration with Chromeriver</span></span>

<span data-ttu-id="f3251-104">En este tutorial, aprenderá a integrar Chromeriver con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f3251-104">In this tutorial, you learn how to integrate Chromeriver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3251-105">La integración de Chromeriver con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f3251-105">Integrating Chromeriver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f3251-106">En Azure AD puede controlar quién tiene acceso a Chromeriver</span><span class="sxs-lookup"><span data-stu-id="f3251-106">You can control in Azure AD who has access to Chromeriver</span></span>
- <span data-ttu-id="f3251-107">Puede permitir que los usuarios inicien sesión automáticamente en Chromeriver (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3251-107">You can enable your users to automatically get signed-on to Chromeriver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3251-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f3251-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f3251-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3251-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3251-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f3251-110">Prerequisites</span></span>

<span data-ttu-id="f3251-111">Para configurar la integración de Azure AD con Chromeriver, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f3251-111">To configure Azure AD integration with Chromeriver, you need the following items:</span></span>

- <span data-ttu-id="f3251-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3251-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3251-113">Una suscripción habilitada para el inicio de sesión único en Chromeriver</span><span class="sxs-lookup"><span data-stu-id="f3251-113">A Chromeriver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3251-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f3251-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3251-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f3251-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3251-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f3251-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3251-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3251-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3251-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f3251-118">Scenario description</span></span>
<span data-ttu-id="f3251-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f3251-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3251-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f3251-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3251-121">Incorporación de Chromeriver desde la galería</span><span class="sxs-lookup"><span data-stu-id="f3251-121">Adding Chromeriver from the gallery</span></span>
2. <span data-ttu-id="f3251-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3251-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-chromeriver-from-the-gallery"></a><span data-ttu-id="f3251-123">Incorporación de Chromeriver desde la galería</span><span class="sxs-lookup"><span data-stu-id="f3251-123">Adding Chromeriver from the gallery</span></span>
<span data-ttu-id="f3251-124">Para configurar la integración de Chromeriver en Azure AD, deberá agregar Chromeriver desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f3251-124">To configure the integration of Chromeriver into Azure AD, you need to add Chromeriver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f3251-125">**Para agregar Chromeriver desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f3251-125">**To add Chromeriver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f3251-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f3251-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f3251-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f3251-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f3251-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f3251-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f3251-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3251-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f3251-133">En el cuadro de búsqueda, escriba **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="f3251-133">In the search box, type **Chromeriver**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_search.png)

5. <span data-ttu-id="f3251-135">En el panel de resultados, seleccione **Chromeriver** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f3251-135">In the results panel, select **Chromeriver**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3251-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3251-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3251-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Chromeriver con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f3251-138">In this section, you configure and test Azure AD single sign-on with Chromeriver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f3251-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Chromeriver para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3251-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Chromeriver is to a user in Azure AD.</span></span> <span data-ttu-id="f3251-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="f3251-140">In other words, a link relationship between an Azure AD user and the related user in Chromeriver needs to be established.</span></span>

<span data-ttu-id="f3251-141">Para establecer la relación de vínculo, en Chromeriver, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f3251-141">In Chromeriver, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f3251-142">Para configurar y probar el inicio de sesión único de Azure AD con Chromeriver, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f3251-142">To configure and test Azure AD single sign-on with Chromeriver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f3251-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="f3251-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f3251-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3251-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3251-145">**[Creación de un usuario de prueba de Chromeriver](#creating-a-chromeriver-test-user)**: para tener un homólogo de Britta Simon en Chromeriver que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3251-145">**[Creating a Chromeriver test user](#creating-a-chromeriver-test-user)** - to have a counterpart of Britta Simon in Chromeriver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3251-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3251-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3251-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f3251-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3251-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3251-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3251-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="f3251-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Chromeriver application.</span></span>

<span data-ttu-id="f3251-150">**Para configurar el inicio de sesión único de Azure AD con Chromeriver, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f3251-150">**To configure Azure AD single sign-on with Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="f3251-151">En Azure Portal, en la página de integración de la aplicación **Chromeriver**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f3251-151">In the Azure portal, on the **Chromeriver** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f3251-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f3251-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_samlbase.png)

3. <span data-ttu-id="f3251-155">En la sección **Dominio y direcciones URL de Chromeriver**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f3251-155">On the **Chromeriver Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_url.png)

    <span data-ttu-id="f3251-157">a.</span><span class="sxs-lookup"><span data-stu-id="f3251-157">a.</span></span> <span data-ttu-id="f3251-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.chromeriver.com`</span><span class="sxs-lookup"><span data-stu-id="f3251-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com`</span></span>

    <span data-ttu-id="f3251-159">b.</span><span class="sxs-lookup"><span data-stu-id="f3251-159">b.</span></span> <span data-ttu-id="f3251-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`.</span><span class="sxs-lookup"><span data-stu-id="f3251-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f3251-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="f3251-161">These values are not real.</span></span> <span data-ttu-id="f3251-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="f3251-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="f3251-163">Póngase en contacto con el [equipo de soporte técnico de Chromeriver](https://www.chromeriver.com/services/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="f3251-163">Contact [Chromeriver support team](https://www.chromeriver.com/services/support) to get these values.</span></span>
 


4. <span data-ttu-id="f3251-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f3251-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_certificate.png) 

5. <span data-ttu-id="f3251-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f3251-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-chromeriver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f3251-168">Para configurar el inicio de sesión único en **Chromeriver**, debe enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="f3251-168">To configure single sign-on on **Chromeriver** side, you need to send the downloaded **Metadata XML** to [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span> <span data-ttu-id="f3251-169">Cuando SSO se haya habilitado en su suscripción recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="f3251-169">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="f3251-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f3251-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f3251-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f3251-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f3251-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3251-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3251-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3251-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="f3251-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f3251-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f3251-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f3251-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f3251-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f3251-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3251-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f3251-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f3251-181">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3251-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3251-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f3251-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3251-185">a.</span><span class="sxs-lookup"><span data-stu-id="f3251-185">a.</span></span> <span data-ttu-id="f3251-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3251-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3251-187">b.</span><span class="sxs-lookup"><span data-stu-id="f3251-187">b.</span></span> <span data-ttu-id="f3251-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3251-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3251-189">c.</span><span class="sxs-lookup"><span data-stu-id="f3251-189">c.</span></span> <span data-ttu-id="f3251-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f3251-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f3251-191">d.</span><span class="sxs-lookup"><span data-stu-id="f3251-191">d.</span></span> <span data-ttu-id="f3251-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f3251-192">Click **Create**.</span></span>
 
### <a name="creating-a-chromeriver-test-user"></a><span data-ttu-id="f3251-193">Creación de un usuario de prueba de Chromeriver</span><span class="sxs-lookup"><span data-stu-id="f3251-193">Creating a Chromeriver test user</span></span>

<span data-ttu-id="f3251-194">Para permitir que los usuarios de Azure AD inicien sesión en Chromeriver, deben aprovisionarse en Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="f3251-194">To enable Azure AD users to log in to Chromeriver, they must be provisioned into Chromeriver.</span></span>  

<span data-ttu-id="f3251-195">En el caso de Chromeriver, las cuentas de usuario debe crearlas el [equipo de soporte técnico de Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="f3251-195">In the case of Chromeriver, the user accounts need to be created by your [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span>

>[!NOTE]
><span data-ttu-id="f3251-196">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Chromeriver que proporcione Chromeriver para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f3251-196">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f3251-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3251-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f3251-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="f3251-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Chromeriver.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f3251-200">**Para asignar a Britta Simon a Chromeriver, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f3251-200">**To assign Britta Simon to Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="f3251-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f3251-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f3251-203">En la lista de aplicaciones, seleccione **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="f3251-203">In the applications list, select **Chromeriver**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_app.png) 

3. <span data-ttu-id="f3251-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f3251-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f3251-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f3251-207">Click **Add** button.</span></span> <span data-ttu-id="f3251-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f3251-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f3251-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f3251-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f3251-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f3251-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3251-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f3251-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3251-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f3251-213">Testing single sign-on</span></span>

<span data-ttu-id="f3251-214">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f3251-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f3251-215">Al hacer clic en el icono de Chromeriver en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="f3251-215">When you click the Chromeriver tile in the Access Panel, you should get automatically signed-on to your Chromeriver application.</span></span> <span data-ttu-id="f3251-216">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f3251-216">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3251-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f3251-217">Additional resources</span></span>

* [<span data-ttu-id="f3251-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3251-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3251-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3251-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_203.png
