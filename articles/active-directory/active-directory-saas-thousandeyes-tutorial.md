---
title: "Tutorial: integración de Azure Active Directory con ThousandEyes | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 392add7d5f0a55598b8b90760f5c3f2d1e67ac02
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="dbdf9-103">Tutorial: integración de Azure Active Directory con ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="dbdf9-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="dbdf9-104">En este tutorial, obtendrá información sobre cómo integrar ThousandEyes con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dbdf9-104">In this tutorial, you learn how to integrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dbdf9-105">Integrar ThousandEyes con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="dbdf9-105">Integrating ThousandEyes with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dbdf9-106">Puede controlar en Azure AD quién tiene acceso a ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="dbdf9-106">You can control in Azure AD who has access to ThousandEyes</span></span>
- <span data-ttu-id="dbdf9-107">Puede permitir que los usuarios inicien sesión automáticamente en ThousandEyes (Inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbdf9-107">You can enable your users to automatically get signed-on to ThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dbdf9-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dbdf9-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dbdf9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbdf9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dbdf9-110">Prerequisites</span></span>

<span data-ttu-id="dbdf9-111">Para configurar la integración de Azure AD con ThousandEyes, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="dbdf9-111">To configure Azure AD integration with ThousandEyes, you need the following items:</span></span>

- <span data-ttu-id="dbdf9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbdf9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dbdf9-113">Una suscripción habilitada para inicio de sesión único en ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="dbdf9-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dbdf9-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dbdf9-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="dbdf9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dbdf9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dbdf9-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbdf9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dbdf9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="dbdf9-118">Scenario description</span></span>
<span data-ttu-id="dbdf9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dbdf9-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="dbdf9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dbdf9-121">Agregar ThousandEyes desde la galería</span><span class="sxs-lookup"><span data-stu-id="dbdf9-121">Adding ThousandEyes from the gallery</span></span>
2. <span data-ttu-id="dbdf9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbdf9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-the-gallery"></a><span data-ttu-id="dbdf9-123">Agregar ThousandEyes desde la galería</span><span class="sxs-lookup"><span data-stu-id="dbdf9-123">Adding ThousandEyes from the gallery</span></span>
<span data-ttu-id="dbdf9-124">Para configurar la integración de ThousandEyes en Azure AD, será preciso que agregue ThousandEyes desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-124">To configure the integration of ThousandEyes into Azure AD, you need to add ThousandEyes from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dbdf9-125">**Para agregar ThousandEyes desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="dbdf9-125">**To add ThousandEyes from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dbdf9-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dbdf9-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dbdf9-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="dbdf9-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="dbdf9-133">En el cuadro de búsqued, escriba **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-133">In the search box, type **ThousandEyes**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="dbdf9-135">En el panel de resultados, seleccione **ThousandEyes** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-135">In the results panel, select **ThousandEyes**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dbdf9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbdf9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dbdf9-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con ThousandEyes con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dbdf9-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dbdf9-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ThousandEyes para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThousandEyes is to a user in Azure AD.</span></span> <span data-ttu-id="dbdf9-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-140">In other words, a link relationship between an Azure AD user and the related user in ThousandEyes needs to be established.</span></span>

<span data-ttu-id="dbdf9-141">Para establecer la relación de vínculo, en ThousandEyes, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-141">In ThousandEyes, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dbdf9-142">Para configurar y probar el inicio de sesión único de Azure AD con ThousandEyes, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="dbdf9-142">To configure and test Azure AD single sign-on with ThousandEyes, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dbdf9-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dbdf9-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dbdf9-145">**[Creación de un usuario de prueba de ThousandEyes](#creating-a-thousandeyes-test-user)**: para tener un homólogo de Britta Simon en Trakstar vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - to have a counterpart of Britta Simon in ThousandEyes that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dbdf9-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dbdf9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dbdf9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbdf9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dbdf9-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="dbdf9-150">**Para configurar el inicio de sesión único de Azure AD con ThousandEyes, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="dbdf9-150">**To configure Azure AD single sign-on with ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="dbdf9-151">En Azure Portal, en la página de integración de la aplicación **ThousandEyes**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-151">In the Azure portal, on the **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="dbdf9-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="dbdf9-155">En la sección **Dominio y direcciones URL de ThousandEyes**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dbdf9-155">On the **ThousandEyes Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="dbdf9-157">En el cuadro de texto **URL de inicio de sesión**, escriba una URL como: `https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="dbdf9-157">In the **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="dbdf9-158">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="dbdf9-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="dbdf9-160">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dbdf9-162">En la sección **Configuración de ThousandEyes**, haga clic en **Configurar ThousandEyes** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-162">On the **ThousandEyes Configuration** section, click **Configure ThousandEyes** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dbdf9-163">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="dbdf9-165">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de **ThousandEyes** como administrador.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-165">In a different web browser window, sign on to your **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="dbdf9-166">En el menú de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-166">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="dbdf9-167">![Configuración](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="dbdf9-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="dbdf9-168">Haga clic en **Cuenta**</span><span class="sxs-lookup"><span data-stu-id="dbdf9-168">Click **Account**</span></span>
   
    <span data-ttu-id="dbdf9-169">![Cuenta](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Cuenta")</span><span class="sxs-lookup"><span data-stu-id="dbdf9-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="dbdf9-170">Haga clic en la pestaña **Security & Authentication** (Seguridad y autenticación).</span><span class="sxs-lookup"><span data-stu-id="dbdf9-170">Click the **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="dbdf9-171">![Seguridad y autenticación](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Seguridad y autenticación")</span><span class="sxs-lookup"><span data-stu-id="dbdf9-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="dbdf9-172">En la sección **Configurar inicio de sesión único** siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dbdf9-172">In the **Setup Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="dbdf9-173">![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="dbdf9-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="dbdf9-174">a.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-174">a.</span></span> <span data-ttu-id="dbdf9-175">Seleccione **Enable Single Sign-On**(Habilitar inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="dbdf9-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="dbdf9-176">b.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-176">b.</span></span> <span data-ttu-id="dbdf9-177">En el cuadro de texto **IDP Login URL** (Dirección URL de inicio de sesión de IDP), pegue la **dirección URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="dbdf9-178">c.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-178">c.</span></span> <span data-ttu-id="dbdf9-179">Copie el valor de **Sign-out URL** (Dirección URL de cierre de sesión) que copió de Azure Portal en el cuadro de texto **Logout page URL** (Dirección URL de la página de cierre de sesión).</span><span class="sxs-lookup"><span data-stu-id="dbdf9-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="dbdf9-180">d.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-180">d.</span></span> <span data-ttu-id="dbdf9-181">En el cuadro de texto **Emisor de proveedor de identidades**, pegue el valor de **id. de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="dbdf9-182">e.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-182">e.</span></span> <span data-ttu-id="dbdf9-183">En **Certificado de comprobación**, haga clic en **Elegir archivo** y cargue el certificado que ha descargado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-183">In **Verification Certificate**, click **Choose file**, and then upload the certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="dbdf9-184">f.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-184">f.</span></span> <span data-ttu-id="dbdf9-185">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="dbdf9-186">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dbdf9-187">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dbdf9-188">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dbdf9-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dbdf9-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbdf9-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="dbdf9-190">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dbdf9-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="dbdf9-192">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="dbdf9-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dbdf9-193">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dbdf9-195">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dbdf9-197">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dbdf9-199">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="dbdf9-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dbdf9-201">a.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-201">a.</span></span> <span data-ttu-id="dbdf9-202">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dbdf9-203">b.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-203">b.</span></span> <span data-ttu-id="dbdf9-204">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dbdf9-205">c.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-205">c.</span></span> <span data-ttu-id="dbdf9-206">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dbdf9-207">d.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-207">d.</span></span> <span data-ttu-id="dbdf9-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="dbdf9-209">Creación de un usuario de prueba de ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="dbdf9-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="dbdf9-210">Para permitir que los usuarios de Azure AD inicien sesión en ThousandEyes, deben aprovisionarse en ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-210">In order to enable Azure AD users to log into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="dbdf9-211">En el caso de ThousandEyes, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-211">In the case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="dbdf9-212">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de ThousandEyes ofrecida por ThousandEyes para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="dbdf9-213">**Para aprovisionar cuentas de usuario en ThousandEyes, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="dbdf9-213">**To provision a user account to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="dbdf9-214">Inicie sesión en su sitio de la compañía de ThousandEyes como administrador.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="dbdf9-215">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="dbdf9-216">![Configuración](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="dbdf9-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="dbdf9-217">Haga clic en **Cuenta**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-217">Click **Account**.</span></span>
   
    <span data-ttu-id="dbdf9-218">![Cuenta](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Cuenta")</span><span class="sxs-lookup"><span data-stu-id="dbdf9-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="dbdf9-219">Haga clic en la pestaña **Accounts & Users** (Cuentas y usuarios).</span><span class="sxs-lookup"><span data-stu-id="dbdf9-219">Click the **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="dbdf9-220">![Cuentas y usuarios](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Cuentas y usuarios")</span><span class="sxs-lookup"><span data-stu-id="dbdf9-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="dbdf9-221">En la sección **Add Users & Accounts** (Agregar usuarios y cuentas), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="dbdf9-221">In the **Add Users & Accounts** section, perform the following steps:</span></span>
   
    <span data-ttu-id="dbdf9-222">![Agregar cuentas de usuario](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Agregar cuentas de usuario")</span><span class="sxs-lookup"><span data-stu-id="dbdf9-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="dbdf9-223">a.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-223">a.</span></span> <span data-ttu-id="dbdf9-224">En el cuadro de texto **Nombre**, escriba el nombre de un usuario, por ejemplo, **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-224">In **Name** textbox, type the name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="dbdf9-225">b.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-225">b.</span></span> <span data-ttu-id="dbdf9-226">En el cuadro de texto **Correo electrónico**, escriba el correo electrónico del usuario, en el ejemplo **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-226">In **Email** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="dbdf9-227">b.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-227">b.</span></span> <span data-ttu-id="dbdf9-228">Haga clic en **Agregar nuevo usuario a la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-228">Click **Add New User to Account**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="dbdf9-229">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo electrónico con un vínculo para confirmar la cuenta y activarla.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-229">The Azure Active Directory account holder will get an email including a link to confirm and activate the account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dbdf9-230">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbdf9-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dbdf9-231">En esta sección, concederá acceso a Britta Simon a ThousandEyes para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThousandEyes.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="dbdf9-233">**Para asignar Britta Simon a ThousandEyes, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="dbdf9-233">**To assign Britta Simon to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="dbdf9-234">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="dbdf9-236">En la lista de aplicaciones, seleccione **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-236">In the applications list, select **ThousandEyes**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="dbdf9-238">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="dbdf9-240">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-240">Click **Add** button.</span></span> <span data-ttu-id="dbdf9-241">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="dbdf9-243">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dbdf9-244">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dbdf9-245">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dbdf9-246">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="dbdf9-246">Testing single sign-on</span></span>

<span data-ttu-id="dbdf9-247">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dbdf9-248">Al hacer clic en el icono de ThousandEyes en el panel de acceso, debe iniciar sesión automáticamente en su aplicación ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="dbdf9-248">When you click the ThousandEyes tile in the Access Panel, you should get automatically signed-on to your ThousandEyes application.</span></span>

<span data-ttu-id="dbdf9-249">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dbdf9-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dbdf9-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="dbdf9-250">Additional resources</span></span>

* [<span data-ttu-id="dbdf9-251">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dbdf9-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dbdf9-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dbdf9-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

