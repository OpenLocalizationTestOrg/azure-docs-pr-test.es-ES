---
title: "Tutorial: Integración de Azure Active Directory con Convercent | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Convercent."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 7af33cae7448a212734d327570b5082d0278fa0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="26a2b-103">Tutorial: Integración de Azure Active Directory con Convercent</span><span class="sxs-lookup"><span data-stu-id="26a2b-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="26a2b-104">En este tutorial, aprenderá a integrar Convercent con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26a2b-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26a2b-105">La integración de Convercent con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="26a2b-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="26a2b-106">Puede controlar en Azure AD quién tiene acceso a Convercent.</span><span class="sxs-lookup"><span data-stu-id="26a2b-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="26a2b-107">Puede permitir que los usuarios inicien sesión automáticamente en Convercent (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26a2b-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="26a2b-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="26a2b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="26a2b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26a2b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26a2b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="26a2b-110">Prerequisites</span></span>

<span data-ttu-id="26a2b-111">Para configurar la integración de Azure AD con Convercent, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="26a2b-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="26a2b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26a2b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26a2b-113">Una suscripción habilitada para el inicio de sesión único en Convercent</span><span class="sxs-lookup"><span data-stu-id="26a2b-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26a2b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="26a2b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26a2b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="26a2b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26a2b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="26a2b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26a2b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26a2b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26a2b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="26a2b-118">Scenario description</span></span>
<span data-ttu-id="26a2b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="26a2b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26a2b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="26a2b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26a2b-121">Agregar Convercent desde la galería</span><span class="sxs-lookup"><span data-stu-id="26a2b-121">Adding Convercent from the gallery</span></span>
2. <span data-ttu-id="26a2b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26a2b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-the-gallery"></a><span data-ttu-id="26a2b-123">Agregar Convercent desde la galería</span><span class="sxs-lookup"><span data-stu-id="26a2b-123">Adding Convercent from the gallery</span></span>
<span data-ttu-id="26a2b-124">Para configurar la integración de Convercent en Azure AD, es preciso agregar Convercent desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="26a2b-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26a2b-125">**Para agregar Convercent desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="26a2b-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26a2b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="26a2b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="26a2b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="26a2b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26a2b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="26a2b-133">En el cuadro de búsqueda, escriba **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-133">In the search box, type **Convercent**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="26a2b-135">En el panel de resultados, seleccione **Convercent** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="26a2b-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="26a2b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26a2b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="26a2b-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Convercent con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26a2b-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="26a2b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Convercent para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26a2b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="26a2b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Convercent.</span><span class="sxs-lookup"><span data-stu-id="26a2b-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="26a2b-141">Esta relación de vínculo se establece asignando el valor del **nombre de usuario** en Azure AD como el valor del **Nombre de usuario** en Convercent.</span><span class="sxs-lookup"><span data-stu-id="26a2b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="26a2b-142">Para configurar y probar el inicio de sesión único de Azure AD con Convercent, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="26a2b-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26a2b-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="26a2b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26a2b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26a2b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26a2b-145">**[Creación de un usuario de prueba de Convercent](#creating-a-convercent-test-user)**: para tener un homólogo de Britta Simon en Convercent que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26a2b-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="26a2b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26a2b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26a2b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="26a2b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="26a2b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26a2b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="26a2b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Convercent.</span><span class="sxs-lookup"><span data-stu-id="26a2b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="26a2b-150">**Para configurar el inicio de sesión único de Azure AD con Convercent, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="26a2b-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="26a2b-151">En Azure Portal, en la página de integración de la aplicación **Convercent**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="26a2b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="26a2b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="26a2b-155">En la sección **Dominio y direcciones URL de Convercent**, si quiere configurar la aplicación en **IDP initiated mode** (Modo iniciado por ID), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="26a2b-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="26a2b-157">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="26a2b-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="26a2b-158">Si quiere configurar la aplicación en **SP initiated mode** (Modo iniciado por SP), en la sección **Dominio y direcciones URL de Convercent**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="26a2b-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="26a2b-160">a.</span><span class="sxs-lookup"><span data-stu-id="26a2b-160">a.</span></span> <span data-ttu-id="26a2b-161">Haga clic en **"Mostrar configuración avanzada de URL"**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="26a2b-162">b.</span><span class="sxs-lookup"><span data-stu-id="26a2b-162">b.</span></span> <span data-ttu-id="26a2b-163">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón: `https://<instancename>.convercent.com/`.</span><span class="sxs-lookup"><span data-stu-id="26a2b-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="26a2b-164">c.</span><span class="sxs-lookup"><span data-stu-id="26a2b-164">c.</span></span> <span data-ttu-id="26a2b-165">En el cuadro de texto **Estado de la retransmisión**, escriba un valor con los patrones siguientes: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="26a2b-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26a2b-166">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="26a2b-166">These values are not the real values.</span></span> <span data-ttu-id="26a2b-167">Actualícelos con el identificador real, la dirección URL de inicio de sesión y el estado de la retransmisión.</span><span class="sxs-lookup"><span data-stu-id="26a2b-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="26a2b-168">Póngase en contacto con el [equipo de soporte técnico de cliente de Convercent](http://support.convercent.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="26a2b-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span></span>

5. <span data-ttu-id="26a2b-169">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="26a2b-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="26a2b-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="26a2b-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="26a2b-173">Para configurar SSO para su aplicación, póngase en contacto con el [equipo de soporte técnico de Convercent](mailto:support@convercent.com) y proporcione el **XML de metadatos** descargado.</span><span class="sxs-lookup"><span data-stu-id="26a2b-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="26a2b-174">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="26a2b-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="26a2b-175">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="26a2b-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="26a2b-176">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26a2b-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="26a2b-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26a2b-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="26a2b-178">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26a2b-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="26a2b-180">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="26a2b-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26a2b-181">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="26a2b-183">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="26a2b-185">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26a2b-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26a2b-187">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="26a2b-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="26a2b-189">a.</span><span class="sxs-lookup"><span data-stu-id="26a2b-189">a.</span></span> <span data-ttu-id="26a2b-190">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26a2b-191">b.</span><span class="sxs-lookup"><span data-stu-id="26a2b-191">b.</span></span> <span data-ttu-id="26a2b-192">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26a2b-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="26a2b-193">c.</span><span class="sxs-lookup"><span data-stu-id="26a2b-193">c.</span></span> <span data-ttu-id="26a2b-194">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="26a2b-195">d.</span><span class="sxs-lookup"><span data-stu-id="26a2b-195">d.</span></span> <span data-ttu-id="26a2b-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="26a2b-197">Creación de un usuario de prueba de Convercent</span><span class="sxs-lookup"><span data-stu-id="26a2b-197">Creating a Convercent test user</span></span>

<span data-ttu-id="26a2b-198">Colabore con el [equipo de soporte técnico de Convercent](mailto:support@convercent.com) para agregar los usuarios a la plataforma de Convercent.</span><span class="sxs-lookup"><span data-stu-id="26a2b-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="26a2b-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26a2b-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="26a2b-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Convercent.</span><span class="sxs-lookup"><span data-stu-id="26a2b-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="26a2b-202">**Para asignar a Britta Simon a Convercent, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="26a2b-202">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="26a2b-203">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="26a2b-205">En la lista de aplicaciones, seleccione **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-205">In the applications list, select **Convercent**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="26a2b-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="26a2b-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-209">Click **Add** button.</span></span> <span data-ttu-id="26a2b-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="26a2b-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="26a2b-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="26a2b-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26a2b-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="26a2b-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="26a2b-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="26a2b-215">Testing single sign-on</span></span>

<span data-ttu-id="26a2b-216">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="26a2b-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="26a2b-217">Al hacer clic en el icono de Convercent en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación Convercent.</span><span class="sxs-lookup"><span data-stu-id="26a2b-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>
<span data-ttu-id="26a2b-218">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26a2b-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="26a2b-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="26a2b-219">Additional resources</span></span>

* [<span data-ttu-id="26a2b-220">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26a2b-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26a2b-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26a2b-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

