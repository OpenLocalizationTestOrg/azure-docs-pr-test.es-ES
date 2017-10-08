---
title: "Tutorial: Integración de Azure Active Directory con Sprinklr | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="46815-103">Tutorial: integración de Azure Active Directory con Sprinklr</span><span class="sxs-lookup"><span data-stu-id="46815-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="46815-104">En este tutorial, aprenderá cómo toointegrate Sprinklr con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46815-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46815-105">Integración Sprinklr con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="46815-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="46815-106">Puede controlar en Azure AD que tenga acceso tooSprinklr</span><span class="sxs-lookup"><span data-stu-id="46815-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="46815-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSprinklr (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46815-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46815-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="46815-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="46815-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="46815-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46815-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="46815-110">Prerequisites</span></span>

<span data-ttu-id="46815-111">integración de Azure AD con Sprinklr tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="46815-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="46815-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46815-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46815-113">Una suscripción habilitada para el inicio de sesión único en Sprinklr</span><span class="sxs-lookup"><span data-stu-id="46815-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46815-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="46815-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46815-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="46815-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46815-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="46815-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46815-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46815-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46815-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="46815-118">Scenario description</span></span>
<span data-ttu-id="46815-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="46815-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46815-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="46815-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46815-121">Agregar Sprinklr desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="46815-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="46815-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46815-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="46815-123">Agregar Sprinklr desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="46815-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="46815-124">integración de hello tooconfigure de Sprinklr en Azure AD, deberá tooadd Sprinklr de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="46815-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="46815-125">**tooadd Sprinklr de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="46815-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="46815-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="46815-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="46815-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="46815-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="46815-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="46815-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="46815-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46815-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="46815-133">En el cuadro de búsqueda de hello, escriba **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="46815-133">In hello search box, type **Sprinklr**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="46815-135">En el panel de resultados de hello, seleccione **Sprinklr**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="46815-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="46815-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46815-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="46815-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Sprinklr con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46815-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="46815-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Sprinklr es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46815-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="46815-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Sprinklr debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="46815-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="46815-141">En Sprinklr, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46815-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="46815-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Sprinklr, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="46815-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="46815-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="46815-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="46815-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46815-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="46815-145">**[Crear un usuario de prueba de Sprinklr](#creating-a-sprinklr-test-user)**  -toohave un equivalente de Britta Simon en Sprinklr que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="46815-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="46815-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="46815-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="46815-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="46815-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="46815-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46815-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="46815-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="46815-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="46815-150">**inicio de sesión único en tooconfigure Azure AD con Sprinklr, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="46815-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="46815-151">En el portal de Azure, en Hola Hola **Sprinklr** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="46815-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="46815-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="46815-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="46815-155">En hello **Sprinklr dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="46815-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="46815-157">a.</span><span class="sxs-lookup"><span data-stu-id="46815-157">a.</span></span> <span data-ttu-id="46815-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="46815-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="46815-159">b.</span><span class="sxs-lookup"><span data-stu-id="46815-159">b.</span></span> <span data-ttu-id="46815-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="46815-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="46815-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="46815-161">These values are not real.</span></span> <span data-ttu-id="46815-162">Actualice el valor de hello con hello real dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="46815-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="46815-163">Póngase en contacto con [equipo de soporte técnico de cliente de Sprinklr](https://www.sprinklr.com/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="46815-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="46815-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="46815-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="46815-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="46815-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="46815-168">En hello **configuración de Sprinklr** sección, haga clic en **configurar Sprinklr** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="46815-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="46815-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="46815-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="46815-170">En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa Sprinklr tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="46815-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="46815-171">Vaya demasiado**administración \> configuración**.</span><span class="sxs-lookup"><span data-stu-id="46815-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="46815-172">![Administración](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="46815-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="46815-173">Vaya demasiado**administrar socios \> inicio de sesión único** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46815-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="46815-174">![Administración de asociado](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Administración de asociados")</span><span class="sxs-lookup"><span data-stu-id="46815-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="46815-175">Haga clic en **+Add Single Sign On**(+ Agregar inicios de sesión únicos).</span><span class="sxs-lookup"><span data-stu-id="46815-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="46815-176">![Inicios de sesión únicos](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Inicios de sesión únicos")</span><span class="sxs-lookup"><span data-stu-id="46815-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="46815-177">En hello **inicio de sesión único** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="46815-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="46815-178">![Inicios de sesión únicos](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Inicios de sesión únicos")</span><span class="sxs-lookup"><span data-stu-id="46815-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="46815-179">a.</span><span class="sxs-lookup"><span data-stu-id="46815-179">a.</span></span> <span data-ttu-id="46815-180">Hola **nombre** cuadro de texto, escriba un nombre para la configuración (por ejemplo: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="46815-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="46815-181">b.</span><span class="sxs-lookup"><span data-stu-id="46815-181">b.</span></span> <span data-ttu-id="46815-182">Seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="46815-182">Select **Enabled**.</span></span>

    <span data-ttu-id="46815-183">c.</span><span class="sxs-lookup"><span data-stu-id="46815-183">c.</span></span> <span data-ttu-id="46815-184">Seleccione **Use new SSO Certificate**(Usar el nuevo certificado de SSO).</span><span class="sxs-lookup"><span data-stu-id="46815-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="46815-185">e.</span><span class="sxs-lookup"><span data-stu-id="46815-185">e.</span></span> <span data-ttu-id="46815-186">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="46815-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="46815-187">f.</span><span class="sxs-lookup"><span data-stu-id="46815-187">f.</span></span> <span data-ttu-id="46815-188">Hola pegar **Id. de entidad SAML** valor que ha copiado desde el Portal de Azure en hello **Id. de entidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="46815-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="46815-189">g.</span><span class="sxs-lookup"><span data-stu-id="46815-189">g.</span></span> <span data-ttu-id="46815-190">Hola pegar **SAML Single Sign-On dirección URL del servicio** valor que ha copiado desde el Portal de Azure en hello **URL de inicio de sesión del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="46815-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="46815-191">h.</span><span class="sxs-lookup"><span data-stu-id="46815-191">h.</span></span> <span data-ttu-id="46815-192">Hola pegar **dirección URL de cierre de sesión** valor que ha copiado desde el Portal de Azure en hello **URL de cierre de sesión del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="46815-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="46815-193">i.</span><span class="sxs-lookup"><span data-stu-id="46815-193">i.</span></span> <span data-ttu-id="46815-194">Como **Tipo de Id. de usuario de SAML**, seleccione **La aserción contiene el nombre de usuario de sprinklr.com del usuario**.</span><span class="sxs-lookup"><span data-stu-id="46815-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="46815-195">j.</span><span class="sxs-lookup"><span data-stu-id="46815-195">j.</span></span> <span data-ttu-id="46815-196">Como **ubicación de Id. de usuario de SAML**, seleccione **Id. de usuario está en el elemento de identificador de nombre de Hola de hello instrucción Subject**.</span><span class="sxs-lookup"><span data-stu-id="46815-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="46815-197">k.</span><span class="sxs-lookup"><span data-stu-id="46815-197">k.</span></span> <span data-ttu-id="46815-198">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="46815-198">Click **Save**.</span></span>
       
    <span data-ttu-id="46815-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="46815-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="46815-200">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="46815-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="46815-201">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="46815-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="46815-202">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46815-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="46815-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46815-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="46815-204">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="46815-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="46815-206">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="46815-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="46815-207">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="46815-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="46815-209">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="46815-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="46815-211">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46815-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="46815-213">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="46815-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46815-215">a.</span><span class="sxs-lookup"><span data-stu-id="46815-215">a.</span></span> <span data-ttu-id="46815-216">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46815-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46815-217">b.</span><span class="sxs-lookup"><span data-stu-id="46815-217">b.</span></span> <span data-ttu-id="46815-218">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="46815-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46815-219">c.</span><span class="sxs-lookup"><span data-stu-id="46815-219">c.</span></span> <span data-ttu-id="46815-220">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="46815-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="46815-221">d.</span><span class="sxs-lookup"><span data-stu-id="46815-221">d.</span></span> <span data-ttu-id="46815-222">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="46815-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="46815-223">Creación de un usuario de prueba de Sprinklr</span><span class="sxs-lookup"><span data-stu-id="46815-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="46815-224">Inicie sesión en tooyour sitio de la empresa Sprinklr como administrador.</span><span class="sxs-lookup"><span data-stu-id="46815-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="46815-225">Vaya demasiado**administración \> configuración**.</span><span class="sxs-lookup"><span data-stu-id="46815-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="46815-226">![Administración](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="46815-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="46815-227">Vaya demasiado**cliente administrar \> usuarios** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46815-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="46815-228">![Configuración](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="46815-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="46815-229">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="46815-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="46815-230">![Configuración](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="46815-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="46815-231">En hello **Editar usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="46815-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="46815-232">![Edición de usuarios](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edición de usuarios")</span><span class="sxs-lookup"><span data-stu-id="46815-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="46815-233">a.</span><span class="sxs-lookup"><span data-stu-id="46815-233">a.</span></span> <span data-ttu-id="46815-234">Hola **correo electrónico**, **nombre** y **Last Name** cuadros de texto, información de tipo hello de una cuenta de usuario de Azure AD que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="46815-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="46815-235">b.</span><span class="sxs-lookup"><span data-stu-id="46815-235">b.</span></span> <span data-ttu-id="46815-236">Seleccione **Password Disabled**(Contraseña deshabilitada).</span><span class="sxs-lookup"><span data-stu-id="46815-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="46815-237">c.</span><span class="sxs-lookup"><span data-stu-id="46815-237">c.</span></span> <span data-ttu-id="46815-238">Seleccione **Language** (Lenguaje).</span><span class="sxs-lookup"><span data-stu-id="46815-238">Select **Language**.</span></span>

    <span data-ttu-id="46815-239">d.</span><span class="sxs-lookup"><span data-stu-id="46815-239">d.</span></span> <span data-ttu-id="46815-240">Seleccione **User Type**(Tipo de usuario).</span><span class="sxs-lookup"><span data-stu-id="46815-240">Select **User Type**.</span></span>

    <span data-ttu-id="46815-241">e.</span><span class="sxs-lookup"><span data-stu-id="46815-241">e.</span></span> <span data-ttu-id="46815-242">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="46815-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="46815-243">**Contraseña deshabilitada** debe ser tooenable seleccionado un toolog de usuario en a través de un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="46815-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="46815-244">Vaya demasiado**rol**y, a continuación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="46815-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="46815-245">![Roles de asociados](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Roles de asociados")</span><span class="sxs-lookup"><span data-stu-id="46815-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="46815-246">a.</span><span class="sxs-lookup"><span data-stu-id="46815-246">a.</span></span> <span data-ttu-id="46815-247">De hello **Global** lista, seleccione **todos los\_permisos**.</span><span class="sxs-lookup"><span data-stu-id="46815-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="46815-248">b.</span><span class="sxs-lookup"><span data-stu-id="46815-248">b.</span></span> <span data-ttu-id="46815-249">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="46815-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="46815-250">Puede usar cualquier otra Sprinklr usuario cuenta herramienta de creación o las API proporcionadas por Sprinklr tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46815-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="46815-251">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="46815-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="46815-252">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSprinklr.</span><span class="sxs-lookup"><span data-stu-id="46815-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="46815-254">**tooassign Britta Simon tooSprinklr, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="46815-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="46815-255">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="46815-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="46815-257">En la lista de aplicaciones de hello, seleccione **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="46815-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="46815-259">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="46815-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="46815-261">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="46815-261">Click **Add** button.</span></span> <span data-ttu-id="46815-262">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="46815-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="46815-264">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="46815-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="46815-265">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="46815-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="46815-266">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="46815-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="46815-267">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="46815-267">Testing single sign-on</span></span>

<span data-ttu-id="46815-268">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="46815-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="46815-269">Al hacer clic en icono de Sprinklr de Hola Hola Panel de acceso, debe obtener automáticamente ha iniciado sesión tooyour Sprinklr aplicación para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="46815-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="46815-270">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="46815-270">Additional resources</span></span>

* [<span data-ttu-id="46815-271">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46815-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="46815-272">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46815-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

