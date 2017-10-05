---
title: "Tutorial: Integración de Azure Active Directory con Blackboard Learn - Shibboleth | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Blackboard Learn - Shibboleth."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 014b0671eb8604235a823c2cf4324a49d94df702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="e7146-103">Tutorial: Integración de Azure Active Directory con Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="e7146-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="e7146-104">En este tutorial, obtendrá información sobre cómo integrar Blackboard Learn - Shibboleth con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7146-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7146-105">La integración de Blackboard Learn - Shibboleth con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e7146-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7146-106">Puede controlar en Azure AD quién tiene acceso a Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="e7146-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="e7146-107">Puede permitir que los usuarios inicien sesión automáticamente en Blackboard Learn - Shibboleth (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7146-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7146-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e7146-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e7146-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7146-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7146-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e7146-110">Prerequisites</span></span>

<span data-ttu-id="e7146-111">Para configurar la integración de Azure AD con Blackboard Learn - Shibboleth, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e7146-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span></span>

- <span data-ttu-id="e7146-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7146-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7146-113">Una suscripción habilitada para el inicio de sesión único de Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="e7146-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7146-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e7146-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7146-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e7146-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7146-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e7146-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7146-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7146-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7146-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e7146-118">Scenario description</span></span>
<span data-ttu-id="e7146-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e7146-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7146-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e7146-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7146-121">Adición de Blackboard Learn - Shibboleth desde la galería</span><span class="sxs-lookup"><span data-stu-id="e7146-121">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
2. <span data-ttu-id="e7146-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7146-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-the-gallery"></a><span data-ttu-id="e7146-123">Adición de Blackboard Learn - Shibboleth desde la galería</span><span class="sxs-lookup"><span data-stu-id="e7146-123">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
<span data-ttu-id="e7146-124">Para configurar la integración de Blackboard Learn - Shibboleth en Azure AD, es preciso agregar Blackboard Learn - Shibboleth desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e7146-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7146-125">**Para agregar Blackboard Learn - Shibboleth desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e7146-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7146-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7146-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7146-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e7146-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7146-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e7146-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e7146-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7146-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e7146-133">En el cuadro de búsqueda, escriba **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="e7146-133">In the search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="e7146-135">En el panel de resultados, seleccione **Blackboard Learn - Shibboleth** y, después, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7146-135">In the results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7146-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7146-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7146-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Blackboard Learn - Shibboleth con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7146-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7146-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Blackboard Learn - Shibboleth para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7146-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span></span> <span data-ttu-id="e7146-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="e7146-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span></span>

<span data-ttu-id="e7146-141">Para establecer la relación de vínculo, en Blackboard Learn - Shibboleth, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e7146-141">In Blackboard Learn - Shibboleth, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e7146-142">Para configurar y probar el inicio de sesión único de Azure AD con Blackboard Learn - Shibboleth, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e7146-142">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7146-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e7146-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e7146-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7146-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7146-145">**[Creación de un usuario de prueba de Blackboard Learn - Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)**: para tener un homólogo de Britta Simon en Blackboard Learn - Shibboleth que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7146-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7146-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7146-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7146-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e7146-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7146-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7146-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7146-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="e7146-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="e7146-150">**Para configurar el inicio de sesión único de Azure AD con Blackboard Learn - Shibboleth, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e7146-150">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="e7146-151">En Azure Portal, en la página de integración de la aplicación **Blackboard Learn - Shibboleth**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e7146-151">In the Azure portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e7146-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e7146-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="e7146-155">En la sección **Dominio y direcciones URL de Blackboard Learn - Shibboleth**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e7146-155">On the **Blackboard Learn - Shibboleth Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="e7146-157">a.</span><span class="sxs-lookup"><span data-stu-id="e7146-157">a.</span></span> <span data-ttu-id="e7146-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`.</span><span class="sxs-lookup"><span data-stu-id="e7146-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="e7146-159">b.</span><span class="sxs-lookup"><span data-stu-id="e7146-159">b.</span></span> <span data-ttu-id="e7146-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="e7146-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="e7146-161">c.</span><span class="sxs-lookup"><span data-stu-id="e7146-161">c.</span></span> <span data-ttu-id="e7146-162">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`.</span><span class="sxs-lookup"><span data-stu-id="e7146-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="e7146-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e7146-163">These values are not real.</span></span> <span data-ttu-id="e7146-164">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e7146-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e7146-165">Póngase en contacto con [el equipo de soporte al cliente de Blackboard Learn - Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="e7146-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) to get these values.</span></span> 

4. <span data-ttu-id="e7146-166">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e7146-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="e7146-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e7146-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="e7146-170">En la sección **Configuración de Blackboard Learn - Shibboleth**, haga clic en **Configurar Blackboard Learn - Shibboleth** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e7146-170">On the **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e7146-171">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="e7146-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="e7146-173">Para configurar el inicio de sesión único en **Blackboard Learn - Shibboleth**, es preciso enviar los valores descargados de **XML de metadatos**, **Sign-Out URL (Dirección URL de cierre de sesión), SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de Blackboard Learn - Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7146-173">To configure single sign-on on **Blackboard Learn - Shibboleth** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="e7146-174">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7146-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e7146-175">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e7146-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e7146-176">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7146-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7146-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7146-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7146-178">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7146-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e7146-180">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e7146-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7146-181">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7146-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7146-183">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e7146-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7146-185">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7146-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7146-187">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e7146-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7146-189">a.</span><span class="sxs-lookup"><span data-stu-id="e7146-189">a.</span></span> <span data-ttu-id="e7146-190">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7146-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7146-191">b.</span><span class="sxs-lookup"><span data-stu-id="e7146-191">b.</span></span> <span data-ttu-id="e7146-192">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7146-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7146-193">c.</span><span class="sxs-lookup"><span data-stu-id="e7146-193">c.</span></span> <span data-ttu-id="e7146-194">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e7146-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7146-195">d.</span><span class="sxs-lookup"><span data-stu-id="e7146-195">d.</span></span> <span data-ttu-id="e7146-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e7146-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="e7146-197">Creación de un usuario de prueba de Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="e7146-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="e7146-198">En esta sección, creará un usuario llamado Britta Simon en Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="e7146-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="e7146-199">Trabaje con el [equipo de soporte técnico de Blackboard Learn - Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) para agregar usuarios a la plataforma de Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="e7146-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) to add the users in the Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7146-200">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7146-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7146-201">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="e7146-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn - Shibboleth.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e7146-203">**Para asignar Britta Simon a Blackboard Learn - Shibboleth, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e7146-203">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="e7146-204">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e7146-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e7146-206">En la lista de aplicaciones, seleccione **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="e7146-206">In the applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="e7146-208">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e7146-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e7146-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e7146-210">Click **Add** button.</span></span> <span data-ttu-id="e7146-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e7146-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e7146-213">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e7146-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e7146-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e7146-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7146-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e7146-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7146-216">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e7146-216">Testing single sign-on</span></span>

<span data-ttu-id="e7146-217">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e7146-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e7146-218">Al hacer clic en el icono de Blackboard Learn - Shibboleth en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="e7146-218">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7146-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e7146-219">Additional resources</span></span>

* [<span data-ttu-id="e7146-220">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7146-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7146-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7146-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

