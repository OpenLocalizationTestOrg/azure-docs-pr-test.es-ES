---
title: "Tutorial: Integración de Azure Active Directory con WORKS MOBILE | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y WORKS MOBILE."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 139a1968a59424eae278de3e7fa227ad340a1eb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="207c8-103">Tutorial: Integración de Azure Active Directory con WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="207c8-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="207c8-104">En este tutorial, obtendrá información sobre cómo integrar WORKS MOBILE con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="207c8-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="207c8-105">La integración de WORKS MOBILE con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="207c8-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="207c8-106">Puede controlar en Azure AD quién tiene acceso a WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="207c8-106">You can control in Azure AD who has access to WORKS MOBILE</span></span>
- <span data-ttu-id="207c8-107">Puede permitir que los usuarios inicien sesión automáticamente en WORKS MOBILE (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="207c8-107">You can enable your users to automatically get signed-on to WORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="207c8-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="207c8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="207c8-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="207c8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="207c8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="207c8-110">Prerequisites</span></span>

<span data-ttu-id="207c8-111">Para configurar la integración de Azure AD con WORKS MOBILE, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="207c8-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span></span>

- <span data-ttu-id="207c8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="207c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="207c8-113">Una suscripción habilitada para el inicio de sesión único en WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="207c8-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="207c8-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="207c8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="207c8-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="207c8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="207c8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="207c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="207c8-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="207c8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="207c8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="207c8-118">Scenario description</span></span>
<span data-ttu-id="207c8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="207c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="207c8-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="207c8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="207c8-121">Incorporación de WORKS MOBILE desde la galería</span><span class="sxs-lookup"><span data-stu-id="207c8-121">Adding WORKS MOBILE from the gallery</span></span>
2. <span data-ttu-id="207c8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="207c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-the-gallery"></a><span data-ttu-id="207c8-123">Incorporación de WORKS MOBILE desde la galería</span><span class="sxs-lookup"><span data-stu-id="207c8-123">Adding WORKS MOBILE from the gallery</span></span>
<span data-ttu-id="207c8-124">Para configurar la integración de WORKS MOBILE en Azure AD, deberá agregar WORKS MOBILE desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="207c8-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="207c8-125">**Para agregar WORKS MOBILE desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="207c8-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="207c8-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="207c8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="207c8-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="207c8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="207c8-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="207c8-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="207c8-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="207c8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="207c8-133">En el cuadro de búsqueda, escriba **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="207c8-133">In the search box, type **WORKS MOBILE**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="207c8-135">En el panel de resultados, seleccione **WORKS MOBILE** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="207c8-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="207c8-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="207c8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="207c8-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con WORKS MOBILE con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="207c8-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="207c8-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de WORKS MOBILE para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="207c8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span></span> <span data-ttu-id="207c8-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="207c8-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span></span>

<span data-ttu-id="207c8-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="207c8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="207c8-142">Para configurar y probar el inicio de sesión único de Azure AD con WORKS MOBILE, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="207c8-142">To configure and test Azure AD single sign-on with WORKS MOBILE, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="207c8-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="207c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="207c8-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="207c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="207c8-145">**[Creación de un usuario de prueba de WORKS MOBILE](#creating-a-works-mobile-test-user)**: para tener un homólogo de Britta Simon en WORKS MOBILE vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="207c8-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="207c8-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="207c8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="207c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="207c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="207c8-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="207c8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="207c8-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="207c8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="207c8-150">**Para configurar el inicio de sesión único de Azure AD con WORKS MOBILE, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="207c8-150">**To configure Azure AD single sign-on with WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="207c8-151">En Azure Portal, en la página de integración de la aplicación **WORKS MOBILE**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="207c8-151">In the Azure portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="207c8-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="207c8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="207c8-155">En la sección **Dominio y direcciones URL de WORKS MOBILE**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="207c8-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="207c8-157">a.</span><span class="sxs-lookup"><span data-stu-id="207c8-157">a.</span></span> <span data-ttu-id="207c8-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.worksmobile.com/jp/myservice`.</span><span class="sxs-lookup"><span data-stu-id="207c8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="207c8-159">b.</span><span class="sxs-lookup"><span data-stu-id="207c8-159">b.</span></span> <span data-ttu-id="207c8-160">En el cuadro de texto **Identificador**, escriba el valor como `worksmobile.com`.</span><span class="sxs-lookup"><span data-stu-id="207c8-160">In the **Identifier** textbox, type the value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="207c8-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="207c8-161">This value is not real.</span></span> <span data-ttu-id="207c8-162">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="207c8-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="207c8-163">Póngase en contacto con el [equipo de soporte técnico de WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="207c8-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span></span> 
 
4. <span data-ttu-id="207c8-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="207c8-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="207c8-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="207c8-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="207c8-168">En la sección **Configuración de WORKS MOBILE**, haga clic en **Configurar WORKS MOBILE** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="207c8-168">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span></span> <span data-ttu-id="207c8-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="207c8-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="207c8-171">Para configurar el inicio de sesión único para su aplicación, póngase en contacto con el [equipo de soporte técnico de WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) y proporcione la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="207c8-171">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following information:</span></span> 

    <span data-ttu-id="207c8-172">• El **archivo de certificado** descargado</span><span class="sxs-lookup"><span data-stu-id="207c8-172">• The downloaded **Certificate file**</span></span>

    <span data-ttu-id="207c8-173">• La **URL del servicio de inicio de sesión único de SAML**</span><span class="sxs-lookup"><span data-stu-id="207c8-173">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="207c8-174">• El **identificador de entidad de SAML**</span><span class="sxs-lookup"><span data-stu-id="207c8-174">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="207c8-175">• La **dirección URL de cierre de sesión**</span><span class="sxs-lookup"><span data-stu-id="207c8-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="207c8-176">Ahora puede leer una versión concisa de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="207c8-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="207c8-177">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="207c8-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="207c8-178">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="207c8-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="207c8-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="207c8-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="207c8-180">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="207c8-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="207c8-182">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="207c8-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="207c8-183">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="207c8-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="207c8-185">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="207c8-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="207c8-187">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="207c8-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="207c8-189">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="207c8-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="207c8-191">a.</span><span class="sxs-lookup"><span data-stu-id="207c8-191">a.</span></span> <span data-ttu-id="207c8-192">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="207c8-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="207c8-193">b.</span><span class="sxs-lookup"><span data-stu-id="207c8-193">b.</span></span> <span data-ttu-id="207c8-194">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="207c8-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="207c8-195">c.</span><span class="sxs-lookup"><span data-stu-id="207c8-195">c.</span></span> <span data-ttu-id="207c8-196">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="207c8-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="207c8-197">d.</span><span class="sxs-lookup"><span data-stu-id="207c8-197">d.</span></span> <span data-ttu-id="207c8-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="207c8-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="207c8-199">Crear un usuario de prueba de WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="207c8-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="207c8-200">En esta sección, creará un usuario llamado Britta Simon en WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="207c8-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="207c8-201">Trabaje con el [equipo de soporte técnico de WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) para agregar los usuarios a la plataforma de WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="207c8-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="207c8-202">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="207c8-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="207c8-203">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="207c8-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to WORKS MOBILE.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="207c8-205">**Para asignar a Britta Simon a WORKS MOBILE, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="207c8-205">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="207c8-206">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="207c8-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="207c8-208">En la lista de aplicaciones, seleccione **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="207c8-208">In the applications list, select **WORKS MOBILE**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="207c8-210">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="207c8-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="207c8-212">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="207c8-212">Click **Add** button.</span></span> <span data-ttu-id="207c8-213">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="207c8-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="207c8-215">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="207c8-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="207c8-216">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="207c8-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="207c8-217">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="207c8-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="207c8-218">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="207c8-218">Testing single sign-on</span></span>

<span data-ttu-id="207c8-219">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="207c8-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="207c8-220">Al hacer clic en el icono de WORKS MOBILE en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="207c8-220">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span></span>
<span data-ttu-id="207c8-221">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="207c8-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="207c8-222">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="207c8-222">Additional resources</span></span>

* [<span data-ttu-id="207c8-223">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="207c8-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="207c8-224">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="207c8-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

