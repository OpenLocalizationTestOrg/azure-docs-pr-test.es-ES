---
title: "Tutorial: integración de Azure Active Directory con 8x8 Virtual Office | Microsoft Azure"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y 8 x 8 Virtual Office."
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
ms.openlocfilehash: df5c5de77285cd3912b68cc3b1e3eee274aa951c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="8bfa5-103">Tutorial: Integración de Azure Active Directory con 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="8bfa5-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="8bfa5-104">En este tutorial, aprenderá cómo toointegrate 8 x 8 Office Virtual con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8bfa5-104">In this tutorial, you learn how toointegrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8bfa5-105">Integración de 8 x 8 proporciona Office Virtual con Azure AD con hello siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8bfa5-105">Integrating 8x8 Virtual Office with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8bfa5-106">Puede controlar en Azure AD que tenga acceso too8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="8bfa5-106">You can control in Azure AD who has access too8x8 Virtual Office</span></span>
- <span data-ttu-id="8bfa5-107">Puede habilitar a los usuarios obtener tooautomatically ha iniciado sesión too8x8 Office Virtual (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bfa5-107">You can enable your users tooautomatically get signed-on too8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8bfa5-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8bfa5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8bfa5-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8bfa5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bfa5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8bfa5-110">Prerequisites</span></span>

<span data-ttu-id="8bfa5-111">integración de Azure AD con 8 x 8 Virtual Office tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8bfa5-111">tooconfigure Azure AD integration with 8x8 Virtual Office, you need hello following items:</span></span>

- <span data-ttu-id="8bfa5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bfa5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8bfa5-113">Una suscripción habilitada para inicio de sesión único en 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="8bfa5-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8bfa5-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8bfa5-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8bfa5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8bfa5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8bfa5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8bfa5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8bfa5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8bfa5-118">Scenario description</span></span>
<span data-ttu-id="8bfa5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8bfa5-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8bfa5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8bfa5-121">Agregar 8 x 8 Virtual Office desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8bfa5-121">Adding 8x8 Virtual Office from hello gallery</span></span>
2. <span data-ttu-id="8bfa5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bfa5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-hello-gallery"></a><span data-ttu-id="8bfa5-123">Agregar 8 x 8 Virtual Office desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8bfa5-123">Adding 8x8 Virtual Office from hello gallery</span></span>
<span data-ttu-id="8bfa5-124">integración de hello tooconfigure de Office de 8 x 8 Virtual en Azure AD, necesita tooadd 8 x 8 oficina Virtual desde la lista de tooyour de hello Galería de aplicaciones de SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-124">tooconfigure hello integration of 8x8 Virtual Office into Azure AD, you need tooadd 8x8 Virtual Office from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8bfa5-125">**tooadd 8 x 8 oficina Virtual desde la Galería de hello, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="8bfa5-125">**tooadd 8x8 Virtual Office from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bfa5-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8bfa5-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8bfa5-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8bfa5-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8bfa5-133">En el cuadro de búsqueda de hello, escriba **8 x 8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-133">In hello search box, type **8x8 Virtual Office**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="8bfa5-135">En el panel de resultados de hello, seleccione **8 x 8 Virtual Office**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-135">In hello results panel, select **8x8 Virtual Office**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8bfa5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bfa5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8bfa5-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con 8x8 Virtual Office con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8bfa5-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8bfa5-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en 8 x 8 Virtual Office es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 8x8 Virtual Office is tooa user in Azure AD.</span></span> <span data-ttu-id="8bfa5-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en 8 x 8 Office Virtual debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-140">In other words, a link relationship between an Azure AD user and hello related user in 8x8 Virtual Office needs toobe established.</span></span>

<span data-ttu-id="8bfa5-141">De 8 x 8 Virtual oficina, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-141">In 8x8 Virtual Office, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8bfa5-142">tooconfigure y prueba de inicio de sesión único en Azure AD con 8 x 8 Virtual Office, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8bfa5-142">tooconfigure and test Azure AD single sign-on with 8x8 Virtual Office, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8bfa5-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8bfa5-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8bfa5-145">**[Crear un usuario de prueba de Office Virtual 8 x 8](#creating-a-8x8-virtual-office-test-user)**  -toohave un equivalente de Britta Simon en 8 x 8 Virtual Office que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - toohave a counterpart of Britta Simon in 8x8 Virtual Office that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8bfa5-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8bfa5-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8bfa5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bfa5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8bfa5-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Office Virtual 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="8bfa5-150">**tooconfigure inicio de sesión único en Azure AD con 8 x 8 Virtual Office, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8bfa5-150">**tooconfigure Azure AD single sign-on with 8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bfa5-151">En el portal de Azure, en Hola Hola **8 x 8 Virtual Office** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-151">In hello Azure portal, on hello **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8bfa5-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="8bfa5-155">En hello **8 x 8 Virtual Office dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8bfa5-155">On hello **8x8 Virtual Office Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="8bfa5-157">a.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-157">a.</span></span> <span data-ttu-id="8bfa5-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="8bfa5-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="8bfa5-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="8bfa5-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="8bfa5-160">b.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-160">b.</span></span> <span data-ttu-id="8bfa5-161">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="8bfa5-161">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="8bfa5-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="8bfa5-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8bfa5-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-163">These values are not real.</span></span> <span data-ttu-id="8bfa5-164">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-164">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8bfa5-165">Póngase en contacto con [equipo de soporte técnico de Office Virtual 8 x 8](https://www.8x8.com/about-us/contact-us) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) tooget these values.</span></span>
 


4. <span data-ttu-id="8bfa5-166">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-166">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="8bfa5-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8bfa5-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8bfa5-170">En hello **8 x 8 Virtual Office configuración** sección, haga clic en **Office Virtual configurar 8 x 8** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-170">On hello **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8bfa5-171">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="8bfa5-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="8bfa5-173">Inquilino de Office Virtual de inicio de sesión tooyour 8 x 8 como administrador.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-173">Sign-on tooyour 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="8bfa5-174">Seleccione el **administrador de cuentas de Virtual Office** en el panel de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="8bfa5-176">Seleccione **Business** toomanage de la cuenta y haga clic en **inicio de sesión** botón.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-176">Select **Business** account toomanage and click **Sign In** button.</span></span>
   
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="8bfa5-178">Haga clic en **cuentas** pestaña en la lista de menús de Hola.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-178">Click **Accounts** tab in hello menu list.</span></span>
   
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="8bfa5-180">Haga clic en **Single Sign On** en lista de Hola de cuentas.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-180">Click **Single Sign On** in hello list of Accounts.</span></span>
   
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="8bfa5-182">Seleccione **Inicio de sesión único** en el método de autenticación y haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="8bfa5-184">Copia **dirección URL SSO SAML**, **cantar Out URL de servicio único** y **dirección URL del emisor** de Azure AD demasiado**dirección URL de inicio de sesión**, **URL de cierre de sesión**  y **dirección URL del emisor** en Office Virtual 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD too**Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configurar en la aplicación](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="8bfa5-186">Haga clic en **explorador** certificado de hello tooupload que descargó desde Azure AD y haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-186">Click **Browser** button tooupload hello certificate which you downloaded from Azure AD, and click hello **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="8bfa5-187">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8bfa5-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8bfa5-188">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8bfa5-189">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8bfa5-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8bfa5-190">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bfa5-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="8bfa5-191">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8bfa5-193">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8bfa5-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bfa5-194">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8bfa5-196">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8bfa5-198">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8bfa5-200">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8bfa5-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8bfa5-202">a.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-202">a.</span></span> <span data-ttu-id="8bfa5-203">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8bfa5-204">b.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-204">b.</span></span> <span data-ttu-id="8bfa5-205">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8bfa5-206">c.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-206">c.</span></span> <span data-ttu-id="8bfa5-207">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8bfa5-208">d.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-208">d.</span></span> <span data-ttu-id="8bfa5-209">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="8bfa5-210">Creación de un usuario de prueba de 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="8bfa5-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="8bfa5-211">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en 8 x 8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-211">hello objective of this section is toocreate a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="8bfa5-212">8x8 Virtual Office admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8bfa5-213">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-213">There is no action item for you in this section.</span></span> <span data-ttu-id="8bfa5-214">Un nuevo usuario se crea durante una tooaccess de intento de 8 x 8 Virtual Office si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-214">A new user is created during an attempt tooaccess 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="8bfa5-215">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de 8 x 8 Office Virtual](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="8bfa5-215">If you need toocreate a user manually, you need toocontact hello [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8bfa5-216">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bfa5-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8bfa5-217">En esta sección, se habilita las Britta Simon toouse Azure inicio de sesión único mediante la concesión de acceso a Office Virtual too8x8.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too8x8 Virtual Office.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8bfa5-219">**tooassign Britta Simon too8x8 Virtual Office, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8bfa5-219">**tooassign Britta Simon too8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bfa5-220">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8bfa5-222">En la lista de aplicaciones de hello, seleccione **8 x 8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-222">In hello applications list, select **8x8 Virtual Office**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="8bfa5-224">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8bfa5-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-226">Click **Add** button.</span></span> <span data-ttu-id="8bfa5-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8bfa5-229">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8bfa5-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8bfa5-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8bfa5-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8bfa5-232">Testing single sign-on</span></span>

<span data-ttu-id="8bfa5-233">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8bfa5-234">Al hacer clic en icono de Office Virtual Hola 8 x 8 Hola Panel de acceso, deberá obtener la aplicación de Office Virtual automáticamente ha iniciado sesión tooyour 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="8bfa5-234">When you click hello 8x8 Virtual Office tile in hello Access Panel, you should get automatically signed-on tooyour 8x8 Virtual Office application.</span></span>
<span data-ttu-id="8bfa5-235">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8bfa5-235">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8bfa5-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8bfa5-236">Additional resources</span></span>

* [<span data-ttu-id="8bfa5-237">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bfa5-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8bfa5-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8bfa5-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

