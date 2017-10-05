---
title: "Tutorial: integración de Azure Active Directory con 8x8 Virtual Office | Microsoft Azure"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y 8x8 Virtual Office."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d8dcf0171b93fec15347e810a1b525bd815dbf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="666c0-103">Tutorial: Integración de Azure Active Directory con 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="666c0-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="666c0-104">En este tutorial, obtendrá información sobre cómo integrar 8x8 Virtual Office con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="666c0-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="666c0-105">La integración de 8x8 Virtual Office con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="666c0-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="666c0-106">Puede controlar en Azure AD quién tiene acceso a 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="666c0-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="666c0-107">Puede permitir que los usuarios inicien sesión automáticamente en 8x8 Virtual Office (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="666c0-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="666c0-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="666c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="666c0-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="666c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="666c0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="666c0-110">Prerequisites</span></span>

<span data-ttu-id="666c0-111">Para configurar la integración de Azure AD con 8x8 Virtual Office, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="666c0-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="666c0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="666c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="666c0-113">Una suscripción habilitada para inicio de sesión único en 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="666c0-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="666c0-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="666c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="666c0-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="666c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="666c0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="666c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="666c0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="666c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="666c0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="666c0-118">Scenario description</span></span>
<span data-ttu-id="666c0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="666c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="666c0-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="666c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="666c0-121">Incorporación de 8x8 Virtual Office desde la galería</span><span class="sxs-lookup"><span data-stu-id="666c0-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="666c0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="666c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="666c0-123">Incorporación de 8x8 Virtual Office desde la galería</span><span class="sxs-lookup"><span data-stu-id="666c0-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="666c0-124">Para configurar la integración de 8x8 Virtual Office en Azure AD, es preciso agregar 8x8 Virtual Office desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="666c0-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="666c0-125">**Para agregar 8x8 Virtual Office desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="666c0-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="666c0-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="666c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="666c0-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="666c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="666c0-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="666c0-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="666c0-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="666c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="666c0-133">En el cuadro de búsqueda, escriba **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="666c0-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="666c0-135">En el panel de resultados, seleccione **8x8 Virtual Office** y, después, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="666c0-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="666c0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="666c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="666c0-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con 8x8 Virtual Office con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="666c0-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="666c0-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de 8x8 Virtual Office para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="666c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="666c0-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="666c0-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="666c0-141">Para establecer la relación de vínculo, en 8x8 Virtual Office, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="666c0-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="666c0-142">Para configurar y probar el inicio de sesión único de Azure AD con 8x8 Virtual Office, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="666c0-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="666c0-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="666c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="666c0-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="666c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="666c0-145">**[Creación de un usuario de prueba de 8x8 Virtual Office](#creating-a-8x8-virtual-office-test-user)**: para tener un homólogo de Britta Simon en 8x8 Virtual Office que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="666c0-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="666c0-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="666c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="666c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="666c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="666c0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="666c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="666c0-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="666c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="666c0-150">**Para configurar el inicio de sesión único de Azure AD con 8x8 Virtual Office, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="666c0-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="666c0-151">En Azure Portal, en la página de integración de la aplicación **8x8 Virtual Office**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="666c0-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="666c0-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="666c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="666c0-155">En la sección **Dominio y direcciones URL de 8x8 Virtual Office**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="666c0-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="666c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="666c0-157">a.</span></span> <span data-ttu-id="666c0-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="666c0-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="666c0-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="666c0-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="666c0-160">b.</span><span class="sxs-lookup"><span data-stu-id="666c0-160">b.</span></span> <span data-ttu-id="666c0-161">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="666c0-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="666c0-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="666c0-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="666c0-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="666c0-163">These values are not real.</span></span> <span data-ttu-id="666c0-164">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="666c0-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="666c0-165">Póngase en contacto con el [equipo de soporte técnico de 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="666c0-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="666c0-166">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (sin procesar)** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="666c0-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="666c0-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="666c0-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="666c0-170">En la sección **Configuración de 8x8 Virtual Office**, haga clic en **Configurar 8x8 Virtual Office** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="666c0-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="666c0-171">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="666c0-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="666c0-173">Inicie la sesión en el inquilino de 8x8 Virtual Office como administrador.</span><span class="sxs-lookup"><span data-stu-id="666c0-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="666c0-174">Seleccione el **administrador de cuentas de Virtual Office** en el panel de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="666c0-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="666c0-176">Seleccione la cuenta **empresarial** que se va a administrar y haga clic en el botón **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="666c0-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="666c0-178">Haga clic en la pestaña **Cuentas** en la lista de menús.</span><span class="sxs-lookup"><span data-stu-id="666c0-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="666c0-180">Haga clic en **Inicio de sesión único** en la lista de cuentas.</span><span class="sxs-lookup"><span data-stu-id="666c0-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="666c0-182">Seleccione **Inicio de sesión único** en el método de autenticación y haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="666c0-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="666c0-184">Copie la **dirección URL de inicio de sesión único de SAML**, la **dirección URL del servicio de cierre de sesión único** y la **dirección URL del emisor** de Azure AD a **Sign In URL** (URL de inicio de sesión), **Sign Out URL** (URL de cierre de sesión) e **Issuer URL** (URL de emisor) en 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="666c0-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="666c0-186">Haga clic en el botón **Explorador** para cargar el certificado que descargó de Azure AD y luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="666c0-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="666c0-187">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="666c0-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="666c0-188">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="666c0-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="666c0-189">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="666c0-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="666c0-190">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="666c0-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="666c0-191">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="666c0-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="666c0-193">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="666c0-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="666c0-194">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="666c0-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="666c0-196">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="666c0-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="666c0-198">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="666c0-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="666c0-200">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="666c0-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="666c0-202">a.</span><span class="sxs-lookup"><span data-stu-id="666c0-202">a.</span></span> <span data-ttu-id="666c0-203">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="666c0-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="666c0-204">b.</span><span class="sxs-lookup"><span data-stu-id="666c0-204">b.</span></span> <span data-ttu-id="666c0-205">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="666c0-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="666c0-206">c.</span><span class="sxs-lookup"><span data-stu-id="666c0-206">c.</span></span> <span data-ttu-id="666c0-207">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="666c0-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="666c0-208">d.</span><span class="sxs-lookup"><span data-stu-id="666c0-208">d.</span></span> <span data-ttu-id="666c0-209">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="666c0-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="666c0-210">Creación de un usuario de prueba de 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="666c0-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="666c0-211">El objetivo de esta sección es crear un usuario llamado Britta Simon en 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="666c0-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="666c0-212">8x8 Virtual Office admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="666c0-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="666c0-213">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="666c0-213">There is no action item for you in this section.</span></span> <span data-ttu-id="666c0-214">Durante un intento de acceder a 8x8 Virtual Office se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="666c0-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="666c0-215">Si necesita crear manualmente un usuario, es preciso que se ponga en contacto con el [equipo de soporte técnico de 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="666c0-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="666c0-216">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="666c0-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="666c0-217">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="666c0-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="666c0-219">**Para asignar a Britta Simon a 8x8 Virtual Office, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="666c0-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="666c0-220">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="666c0-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="666c0-222">En la lista de aplicaciones, seleccione **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="666c0-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="666c0-224">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="666c0-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="666c0-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="666c0-226">Click **Add** button.</span></span> <span data-ttu-id="666c0-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="666c0-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="666c0-229">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="666c0-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="666c0-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="666c0-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="666c0-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="666c0-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="666c0-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="666c0-232">Testing single sign-on</span></span>

<span data-ttu-id="666c0-233">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="666c0-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="666c0-234">Al hacer clic en el icono de 8x8 Virtual Office en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="666c0-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="666c0-235">Para más información sobre el Panel de acceso, consulte la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="666c0-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="666c0-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="666c0-236">Additional resources</span></span>

* [<span data-ttu-id="666c0-237">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="666c0-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="666c0-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="666c0-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

