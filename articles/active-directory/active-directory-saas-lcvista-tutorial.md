---
title: "Tutorial: Integración de Azure Active Directory con LCVista | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c19f81da495eb7116b62797d1755d312a23f3805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="7112e-103">Tutorial: Integración de Azure Active Directory con LCVista</span><span class="sxs-lookup"><span data-stu-id="7112e-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="7112e-104">En este tutorial, obtendrá información sobre cómo integrar LCVista con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7112e-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7112e-105">Integrar LCVista con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7112e-105">Integrating LCVista with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7112e-106">Puede controlar en Azure AD quién tiene acceso a LCVista.</span><span class="sxs-lookup"><span data-stu-id="7112e-106">You can control in Azure AD who has access to LCVista</span></span>
- <span data-ttu-id="7112e-107">Puede permitir que los usuarios inicien sesión automáticamente en LCVista (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7112e-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7112e-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7112e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7112e-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7112e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7112e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7112e-110">Prerequisites</span></span>

<span data-ttu-id="7112e-111">Para configurar la integración de Azure AD con LCVista, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7112e-111">To configure Azure AD integration with LCVista, you need the following items:</span></span>

- <span data-ttu-id="7112e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7112e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7112e-113">Una suscripción habilitada para el inicio de sesión único en LCVista</span><span class="sxs-lookup"><span data-stu-id="7112e-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7112e-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7112e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7112e-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7112e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7112e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7112e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7112e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7112e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7112e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7112e-118">Scenario description</span></span>
<span data-ttu-id="7112e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7112e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7112e-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="7112e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7112e-121">Adición de LCVista desde la galería</span><span class="sxs-lookup"><span data-stu-id="7112e-121">Adding LCVista from the gallery</span></span>
2. <span data-ttu-id="7112e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7112e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-the-gallery"></a><span data-ttu-id="7112e-123">Adición de LCVista desde la galería</span><span class="sxs-lookup"><span data-stu-id="7112e-123">Adding LCVista from the gallery</span></span>
<span data-ttu-id="7112e-124">Para configurar la integración de LCVista en Azure AD, debe agregar LCVista desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="7112e-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7112e-125">**Para agregar LCVista desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7112e-125">**To add LCVista from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7112e-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7112e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7112e-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7112e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7112e-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7112e-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7112e-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7112e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7112e-133">En el cuadro de búsqueda, escriba **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="7112e-133">In the search box, type **LCVista**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="7112e-135">En el panel de resultados, seleccione **LCVista** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7112e-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7112e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7112e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7112e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con LCVista con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7112e-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7112e-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de LCVista para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7112e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span></span> <span data-ttu-id="7112e-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de LCVista.</span><span class="sxs-lookup"><span data-stu-id="7112e-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span></span>

<span data-ttu-id="7112e-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en LCVista.</span><span class="sxs-lookup"><span data-stu-id="7112e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span></span>

<span data-ttu-id="7112e-142">Para configurar y probar el inicio de sesión único de Azure AD con LCVista, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7112e-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7112e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="7112e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7112e-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7112e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7112e-145">**[Creación de un usuario de prueba de LCVista](#creating-a-lcvista-test-user)**: para tener un homólogo de Britta Simon en LCVista que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7112e-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7112e-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7112e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7112e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7112e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7112e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7112e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7112e-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación LCVista.</span><span class="sxs-lookup"><span data-stu-id="7112e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="7112e-150">**Para configurar el inicio de sesión único de Azure AD con LCVista, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7112e-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="7112e-151">En Azure Portal, en la página de integración de la aplicación **LCVista**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7112e-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7112e-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7112e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="7112e-155">En la sección **Dominio y direcciones URL de LCVista**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7112e-155">On the **LCVista Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="7112e-157">a.</span><span class="sxs-lookup"><span data-stu-id="7112e-157">a.</span></span> <span data-ttu-id="7112e-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.lcvista.com/rainier/login`.</span><span class="sxs-lookup"><span data-stu-id="7112e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="7112e-159">b.</span><span class="sxs-lookup"><span data-stu-id="7112e-159">b.</span></span> <span data-ttu-id="7112e-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="7112e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="7112e-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="7112e-161">These values are not the real.</span></span> <span data-ttu-id="7112e-162">Actualice estos valores con el identificador y la dirección URL de inicio de sesión reales.</span><span class="sxs-lookup"><span data-stu-id="7112e-162">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="7112e-163">Póngase en contacto con el [equipo de soporte de cliente de LCVista](https://lcvista.com/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="7112e-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span></span> 

4. <span data-ttu-id="7112e-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7112e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="7112e-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7112e-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="7112e-168">En la sección **Configuración de LCVista**, haga clic en **Configurar LCVista** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="7112e-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7112e-169">Copie **SAML Entity ID** y **SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="7112e-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="7112e-171">Inicie sesión en su aplicación de LCVista como administrador.</span><span class="sxs-lookup"><span data-stu-id="7112e-171">Sign on to your LCVista application as an administrator.</span></span>

8. <span data-ttu-id="7112e-172">En la sección **SAML Config** (Configuración de SAML), active **Enable SAML login** (Habilitar registro de SAML) y escriba los detalles según se mencionan en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="7112e-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="7112e-174">a.</span><span class="sxs-lookup"><span data-stu-id="7112e-174">a.</span></span> <span data-ttu-id="7112e-175">Pegue la **dirección URL del emisor** que ha copiado de Azure AD en la sección **Entity ID** (Id. de entidad).</span><span class="sxs-lookup"><span data-stu-id="7112e-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span></span> 

    <span data-ttu-id="7112e-176">b.</span><span class="sxs-lookup"><span data-stu-id="7112e-176">b.</span></span> <span data-ttu-id="7112e-177">Pegue la **dirección URL del servicio de inicio de sesión único** que ha copiado de Azure AD en la sección **URL**.</span><span class="sxs-lookup"><span data-stu-id="7112e-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span></span>

    <span data-ttu-id="7112e-178">c.</span><span class="sxs-lookup"><span data-stu-id="7112e-178">c.</span></span> <span data-ttu-id="7112e-179">En el archivo de metadatos (XML) que ha descargado de Azure Portal, copie el valor **X509Certificate** y péguelo en la sección **x509 Certificate** (Certificado x509).</span><span class="sxs-lookup"><span data-stu-id="7112e-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span></span>

    <span data-ttu-id="7112e-180">d.</span><span class="sxs-lookup"><span data-stu-id="7112e-180">d.</span></span> <span data-ttu-id="7112e-181">En el cuadro de texto **First name attribute** (Atributo de nombre), escriba el valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="7112e-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="7112e-182">e.</span><span class="sxs-lookup"><span data-stu-id="7112e-182">e.</span></span> <span data-ttu-id="7112e-183">En el cuadro de texto **Last name attribute** (Atributo de apellido), escriba el valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="7112e-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="7112e-184">f.</span><span class="sxs-lookup"><span data-stu-id="7112e-184">f.</span></span> <span data-ttu-id="7112e-185">En el cuadro de texto **Email attribute** (Atributo de correo electrónico), escriba el valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="7112e-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="7112e-186">g.</span><span class="sxs-lookup"><span data-stu-id="7112e-186">g.</span></span> <span data-ttu-id="7112e-187">En el cuadro de texto **Username attribute** (Atributo de nombre de usuario), escriba el valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="7112e-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="7112e-188">e.</span><span class="sxs-lookup"><span data-stu-id="7112e-188">e.</span></span> <span data-ttu-id="7112e-189">Haga clic en **Guardar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="7112e-189">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="7112e-190">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7112e-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7112e-191">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7112e-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7112e-192">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7112e-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7112e-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7112e-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="7112e-194">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7112e-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7112e-196">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="7112e-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7112e-197">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7112e-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7112e-199">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7112e-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7112e-201">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7112e-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7112e-203">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7112e-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7112e-205">a.</span><span class="sxs-lookup"><span data-stu-id="7112e-205">a.</span></span> <span data-ttu-id="7112e-206">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7112e-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7112e-207">b.</span><span class="sxs-lookup"><span data-stu-id="7112e-207">b.</span></span> <span data-ttu-id="7112e-208">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7112e-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7112e-209">c.</span><span class="sxs-lookup"><span data-stu-id="7112e-209">c.</span></span> <span data-ttu-id="7112e-210">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7112e-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7112e-211">d.</span><span class="sxs-lookup"><span data-stu-id="7112e-211">d.</span></span> <span data-ttu-id="7112e-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7112e-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="7112e-213">Creación de un usuario de prueba de LCVista</span><span class="sxs-lookup"><span data-stu-id="7112e-213">Creating a LCVista test user</span></span>

<span data-ttu-id="7112e-214">En esta sección, creará un usuario llamado Britta Simon en LCVista.</span><span class="sxs-lookup"><span data-stu-id="7112e-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="7112e-215">Póngase en contacto con el [equipo de soporte de cliente de LCVista](https://lcvista.com/contact) para agregar los usuarios a la aplicación LCVista.</span><span class="sxs-lookup"><span data-stu-id="7112e-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7112e-216">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7112e-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7112e-217">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a LCVista.</span><span class="sxs-lookup"><span data-stu-id="7112e-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7112e-219">**Para asignar Britta Simon a LCVista, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="7112e-219">**To assign Britta Simon to LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="7112e-220">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7112e-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7112e-222">En la lista de aplicaciones, seleccione **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="7112e-222">In the applications list, select **LCVista**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="7112e-224">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7112e-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7112e-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7112e-226">Click **Add** button.</span></span> <span data-ttu-id="7112e-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7112e-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7112e-229">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7112e-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7112e-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7112e-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7112e-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7112e-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7112e-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7112e-232">Testing single sign-on</span></span>

<span data-ttu-id="7112e-233">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7112e-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="7112e-234">Haga clic en el icono de LCVista en el panel de acceso y después se le redirigirá a la página de inicio de sesión de la organización.</span><span class="sxs-lookup"><span data-stu-id="7112e-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="7112e-235">Después de registrarse correctamente, iniciará sesión en la aplicación LCVista.</span><span class="sxs-lookup"><span data-stu-id="7112e-235">After successful login, you will be signed-on to your LCVista application.</span></span> <span data-ttu-id="7112e-236">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="7112e-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7112e-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7112e-237">Additional resources</span></span>

* [<span data-ttu-id="7112e-238">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7112e-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7112e-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7112e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

