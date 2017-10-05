---
title: "Tutorial: Integración de Azure Active Directory con 10,000ft Plans | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y 10,000ft Plans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: c81a6adb3abad58af149bbef6f5dff736c142f51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="64a1d-103">Tutorial: integración de Azure Active Directory con 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="64a1d-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="64a1d-104">En este tutorial, aprenderá a integrar 10,000ft Plans con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64a1d-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64a1d-105">Integrar 10,000ft Plans con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="64a1d-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="64a1d-106">Puede controlar en Azure AD quién tiene acceso a 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="64a1d-106">You can control in Azure AD who has access to 10,000ft Plans</span></span>
- <span data-ttu-id="64a1d-107">Puede permitir que los usuarios inicien sesión automáticamente en 10,000ft Plans (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64a1d-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64a1d-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="64a1d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="64a1d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64a1d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64a1d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="64a1d-110">Prerequisites</span></span>

<span data-ttu-id="64a1d-111">Para configurar la integración de Azure AD con 10,000ft Plans, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="64a1d-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span></span>

- <span data-ttu-id="64a1d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a1d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64a1d-113">Una suscripción habilitada para el inicio de sesión único en 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="64a1d-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64a1d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="64a1d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64a1d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="64a1d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64a1d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="64a1d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64a1d-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64a1d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64a1d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="64a1d-118">Scenario description</span></span>
<span data-ttu-id="64a1d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="64a1d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64a1d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="64a1d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64a1d-121">Incorporación de 10,000ft Plans desde la galería</span><span class="sxs-lookup"><span data-stu-id="64a1d-121">Adding 10,000ft Plans from the gallery</span></span>
2. <span data-ttu-id="64a1d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a1d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-the-gallery"></a><span data-ttu-id="64a1d-123">Incorporación de 10,000ft Plans desde la galería</span><span class="sxs-lookup"><span data-stu-id="64a1d-123">Adding 10,000ft Plans from the gallery</span></span>
<span data-ttu-id="64a1d-124">Para configurar la integración de 10,000ft Plans en Azure AD, será preciso que agregue 10,000ft Plans desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="64a1d-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="64a1d-125">**Para agregar 10,000ft Plans desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="64a1d-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="64a1d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="64a1d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="64a1d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="64a1d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64a1d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="64a1d-133">En el cuadro de búsqueda, escriba **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-133">In the search box, type **10,000ft Plans**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="64a1d-135">En el panel de resultados, seleccione **10,000ft Plans** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64a1d-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="64a1d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a1d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="64a1d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con 10,000ft Plans con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="64a1d-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="64a1d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de 10,000ft Plans para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64a1d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span></span> <span data-ttu-id="64a1d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="64a1d-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span></span>

<span data-ttu-id="64a1d-141">Para establecer la relación de vínculo, en 10,000ft Plans, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="64a1d-142">Para configurar y probar el inicio de sesión único de Azure AD con 10,000ft Plans, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="64a1d-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="64a1d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="64a1d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="64a1d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64a1d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64a1d-145">**[Creación de un usuario de prueba de 10,000ft Plans](#creating-a-10000ft-plans-test-user)**: para tener un homólogo de Britta Simon en 10,000ft Plans que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64a1d-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="64a1d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64a1d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64a1d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="64a1d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="64a1d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a1d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="64a1d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="64a1d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="64a1d-150">**Para configurar el inicio de sesión único de Azure AD con 10,000ft Plans, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="64a1d-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="64a1d-151">En Azure Portal, en la página de integración de la aplicación **10,000ft Plans**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="64a1d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="64a1d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="64a1d-155">En la sección **Dominio y direcciones URL de 10,000ft Plans**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="64a1d-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="64a1d-157">a.</span><span class="sxs-lookup"><span data-stu-id="64a1d-157">a.</span></span> <span data-ttu-id="64a1d-158">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="64a1d-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="64a1d-159">b.</span><span class="sxs-lookup"><span data-stu-id="64a1d-159">b.</span></span> <span data-ttu-id="64a1d-160">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="64a1d-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="64a1d-161">El valor de **Identificador** es distinto si tiene un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="64a1d-161">The value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="64a1d-162">Para obtener este valor póngase en contacto con el [equipo de soporte técnico de 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="64a1d-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span></span> 
 
4. <span data-ttu-id="64a1d-163">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (sin procesar)** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="64a1d-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="64a1d-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="64a1d-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="64a1d-167">En la sección **Configuración de 10,000ft Plans**, haga clic en **Configurar 10,000ft Plans** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="64a1d-168">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="64a1d-170">Para configurar el inicio de sesión único en **10,000ft Plans**, es preciso enviar los valores descargados de **Certificado (sin procesar), Sign-Out URL (Dirección URL de cierre de sesión), SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="64a1d-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="64a1d-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64a1d-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="64a1d-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="64a1d-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="64a1d-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64a1d-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="64a1d-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a1d-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="64a1d-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="64a1d-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="64a1d-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="64a1d-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="64a1d-178">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64a1d-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64a1d-182">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64a1d-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64a1d-184">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="64a1d-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64a1d-186">a.</span><span class="sxs-lookup"><span data-stu-id="64a1d-186">a.</span></span> <span data-ttu-id="64a1d-187">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64a1d-188">b.</span><span class="sxs-lookup"><span data-stu-id="64a1d-188">b.</span></span> <span data-ttu-id="64a1d-189">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64a1d-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64a1d-190">c.</span><span class="sxs-lookup"><span data-stu-id="64a1d-190">c.</span></span> <span data-ttu-id="64a1d-191">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="64a1d-192">d.</span><span class="sxs-lookup"><span data-stu-id="64a1d-192">d.</span></span> <span data-ttu-id="64a1d-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="64a1d-194">Creación de un usuario de prueba de 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="64a1d-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="64a1d-195">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="64a1d-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="64a1d-196">10,000ft Plans admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="64a1d-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="64a1d-197">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="64a1d-197">There is no action item for you in this section.</span></span> <span data-ttu-id="64a1d-198">Durante un intento de obtener acceso a 10,000ft Plans se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="64a1d-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="64a1d-199">Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="64a1d-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="64a1d-200">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a1d-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="64a1d-201">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="64a1d-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="64a1d-203">**Para asignar Britta Simon a 10,000ft Plans, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="64a1d-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="64a1d-204">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="64a1d-206">En la lista de aplicaciones, seleccione **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-206">In the applications list, select **10,000ft Plans**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="64a1d-208">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="64a1d-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-210">Click **Add** button.</span></span> <span data-ttu-id="64a1d-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="64a1d-213">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="64a1d-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="64a1d-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64a1d-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="64a1d-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="64a1d-216">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="64a1d-216">Testing single sign-on</span></span>

<span data-ttu-id="64a1d-217">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="64a1d-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="64a1d-218">Al hacer clic en el icono de 10,000ft Plans en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="64a1d-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="64a1d-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="64a1d-219">Additional resources</span></span>

* [<span data-ttu-id="64a1d-220">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64a1d-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64a1d-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64a1d-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

