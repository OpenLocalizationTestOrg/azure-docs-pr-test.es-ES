---
title: "Tutorial: Integración de Azure Active Directory con Cornerstone OnDemand | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Cornerstone OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 8bb32588579a0d40b9ae7e0f823c6daab21c856e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="0a420-103">Tutorial: Integración de Azure Active Directory con Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="0a420-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="0a420-104">En este tutorial, aprenderá a integrar Cornerstone OnDemand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a420-104">In this tutorial, you learn how to integrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a420-105">Integrar Cornerstone OnDemand con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0a420-105">Integrating Cornerstone OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a420-106">Puede controlar en Azure AD quién tiene acceso a Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="0a420-106">You can control in Azure AD who has access to Cornerstone OnDemand</span></span>
- <span data-ttu-id="0a420-107">Puede permitir que los usuarios inicien sesión automáticamente en Cornerstone OnDemand (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a420-107">You can enable your users to automatically get signed-on to Cornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a420-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0a420-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a420-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a420-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a420-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0a420-110">Prerequisites</span></span>

<span data-ttu-id="0a420-111">Para configurar la integración de Azure AD con Cornerstone OnDemand, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0a420-111">To configure Azure AD integration with Cornerstone OnDemand, you need the following items:</span></span>

- <span data-ttu-id="0a420-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a420-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a420-113">Una suscripción habilitada para el inicio de sesión único en Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="0a420-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a420-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0a420-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a420-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0a420-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a420-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0a420-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a420-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a420-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a420-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0a420-118">Scenario description</span></span>
<span data-ttu-id="0a420-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0a420-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a420-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="0a420-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a420-121">Adición de Cornerstone OnDemand desde la galería</span><span class="sxs-lookup"><span data-stu-id="0a420-121">Adding Cornerstone OnDemand from the gallery</span></span>
2. <span data-ttu-id="0a420-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a420-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-the-gallery"></a><span data-ttu-id="0a420-123">Adición de Cornerstone OnDemand desde la galería</span><span class="sxs-lookup"><span data-stu-id="0a420-123">Adding Cornerstone OnDemand from the gallery</span></span>
<span data-ttu-id="0a420-124">Para configurar la integración de Cornerstone OnDemand en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="0a420-124">To configure the integration of Cornerstone OnDemand into Azure AD, you need to add Cornerstone OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a420-125">**Para agregar Cornerstone OnDemand desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0a420-125">**To add Cornerstone OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a420-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a420-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a420-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0a420-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a420-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0a420-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0a420-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a420-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0a420-133">En el cuadro de búsqueda, escriba **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="0a420-133">In the search box, type **Cornerstone OnDemand**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="0a420-135">En el panel de resultados, seleccione **Cornerstone OnDemand** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a420-135">In the results panel, select **Cornerstone OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a420-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a420-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a420-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Cornerstone OnDemand con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0a420-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a420-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Cornerstone OnDemand para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a420-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cornerstone OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="0a420-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="0a420-140">In other words, a link relationship between an Azure AD user and the related user in Cornerstone OnDemand needs to be established.</span></span>

<span data-ttu-id="0a420-141">Para establecer la relación de vínculo, en Cornerstone OnDemand, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="0a420-141">In Cornerstone OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0a420-142">Para configurar y probar el inicio de sesión único de Azure AD con Cornerstone OnDemand, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0a420-142">To configure and test Azure AD single sign-on with Cornerstone OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a420-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="0a420-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a420-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a420-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a420-145">**[Creación de un usuario de prueba de Cornerstone OnDemand](#creating-a-cornerstone-ondemand-test-user)**: para tener un homólogo de Britta Simon en Cornerstone OnDemand que esté vinculado a la representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0a420-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - to have a counterpart of Britta Simon in Cornerstone OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a420-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a420-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a420-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0a420-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a420-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a420-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a420-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="0a420-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="0a420-150">**Para configurar el inicio de sesión único de Azure AD con Cornerstone OnDemand, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0a420-150">**To configure Azure AD single sign-on with Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="0a420-151">En Azure Portal, en la página de integración de la aplicación **Cornerstone OnDemand**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0a420-151">In the Azure portal, on the **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0a420-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0a420-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="0a420-155">En la sección **Dominio y direcciones URL de Cornerstone OnDemand**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0a420-155">On the **Cornerstone OnDemand Domain and URLs** section, perform the following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="0a420-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a420-157">a.</span></span> <span data-ttu-id="0a420-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company>.csod.com`.</span><span class="sxs-lookup"><span data-stu-id="0a420-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="0a420-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a420-159">b.</span></span> <span data-ttu-id="0a420-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="0a420-160">In **Identifier** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a420-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0a420-161">These values are not real.</span></span> <span data-ttu-id="0a420-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0a420-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0a420-163">Póngase en contacto con el [equipo de soporte técnico de Cornerstone OnDemand](mailTo:moreinfo@csod.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="0a420-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) to get these values.</span></span> 
 
4. <span data-ttu-id="0a420-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0a420-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="0a420-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0a420-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a420-168">En la sección **Configuración de Cornerstone OnDemand**, haga clic en **Configurar Cornerstone OnDemand** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="0a420-168">On the **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a420-169">Copie las **direcciones URL del servicio de inicio de sesión único de SAML y de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="0a420-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="0a420-171">Para configurar el inicio de sesión único en **Cornerstone OnDemand**, es preciso enviar el **certificado** descargado, la **dirección URL de cierre de sesión** y la **dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="0a420-171">To configure single sign-on on **Cornerstone OnDemand** side, you need to send the downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  to [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="0a420-172">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="0a420-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0a420-173">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a420-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a420-174">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0a420-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a420-175">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a420-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a420-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a420-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a420-177">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0a420-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0a420-179">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="0a420-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a420-180">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a420-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a420-182">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0a420-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a420-184">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a420-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a420-186">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0a420-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a420-188">a.</span><span class="sxs-lookup"><span data-stu-id="0a420-188">a.</span></span> <span data-ttu-id="0a420-189">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a420-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a420-190">b.</span><span class="sxs-lookup"><span data-stu-id="0a420-190">b.</span></span> <span data-ttu-id="0a420-191">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a420-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a420-192">c.</span><span class="sxs-lookup"><span data-stu-id="0a420-192">c.</span></span> <span data-ttu-id="0a420-193">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0a420-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a420-194">d.</span><span class="sxs-lookup"><span data-stu-id="0a420-194">d.</span></span> <span data-ttu-id="0a420-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0a420-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="0a420-196">Creación de un usuario de prueba de Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="0a420-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="0a420-197">Para permitir que los usuarios de Azure AD inicien sesión en Cornerstone OnDemand, deben aprovisionarse a Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="0a420-197">In order to enable Azure AD users to log into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="0a420-198">En el caso de Cornerstone OnDemand, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="0a420-198">In the case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="0a420-199">Para configurar el aprovisionamiento de usuarios, envíe la información (p. ej.: nombre, correo electrónico) sobre el usuario de Azure AD que desee aprovisionar al [equipo de soporte técnico de Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="0a420-199">To configure user provisioning, send the information (e.g.: Name, Email) about the Azure AD user you want to provision to the [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="0a420-200">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Cornerstone OnDemand ofrecida por Cornerstone OnDemand para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="0a420-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a420-201">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a420-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a420-202">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="0a420-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cornerstone OnDemand.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0a420-204">**Para asignar a Britta Simon a Cornerstone OnDemand, lleve a cabo los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0a420-204">**To assign Britta Simon to Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="0a420-205">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0a420-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0a420-207">En la lista de aplicaciones, seleccione **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="0a420-207">In the applications list, select **Cornerstone OnDemand**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="0a420-209">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0a420-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0a420-211">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0a420-211">Click **Add** button.</span></span> <span data-ttu-id="0a420-212">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0a420-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0a420-214">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0a420-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a420-215">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0a420-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a420-216">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0a420-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a420-217">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0a420-217">Testing single sign-on</span></span>

<span data-ttu-id="0a420-218">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0a420-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0a420-219">Al hacer clic en el icono de Cornerstone OnDemand en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="0a420-219">When you click the Cornerstone OnDemand tile in the Access Panel, you should get automatically signed-on to your Cornerstone OnDemand application.</span></span>
<span data-ttu-id="0a420-220">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a420-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0a420-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0a420-221">Additional resources</span></span>

* [<span data-ttu-id="0a420-222">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a420-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a420-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a420-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png

