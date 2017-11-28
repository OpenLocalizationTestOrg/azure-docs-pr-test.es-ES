---
title: "Tutorial: integración de Azure Active Directory con ThousandEyes | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ThousandEyes."
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
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="fcd75-103">Tutorial: integración de Azure Active Directory con ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="fcd75-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="fcd75-104">En este tutorial, aprenderá cómo toointegrate ThousandEyes con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fcd75-104">In this tutorial, you learn how toointegrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fcd75-105">Integración ThousandEyes con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fcd75-105">Integrating ThousandEyes with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fcd75-106">Puede controlar en Azure AD que tenga acceso tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="fcd75-106">You can control in Azure AD who has access tooThousandEyes</span></span>
- <span data-ttu-id="fcd75-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooThousandEyes (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcd75-107">You can enable your users tooautomatically get signed-on tooThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fcd75-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fcd75-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fcd75-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fcd75-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcd75-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fcd75-110">Prerequisites</span></span>

<span data-ttu-id="fcd75-111">integración de Azure AD con ThousandEyes tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fcd75-111">tooconfigure Azure AD integration with ThousandEyes, you need hello following items:</span></span>

- <span data-ttu-id="fcd75-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcd75-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fcd75-113">Una suscripción habilitada para inicio de sesión único en ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="fcd75-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fcd75-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fcd75-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fcd75-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fcd75-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fcd75-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fcd75-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fcd75-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fcd75-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fcd75-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fcd75-118">Scenario description</span></span>
<span data-ttu-id="fcd75-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fcd75-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fcd75-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="fcd75-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fcd75-121">Agregar ThousandEyes desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fcd75-121">Adding ThousandEyes from hello gallery</span></span>
2. <span data-ttu-id="fcd75-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcd75-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-hello-gallery"></a><span data-ttu-id="fcd75-123">Agregar ThousandEyes desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fcd75-123">Adding ThousandEyes from hello gallery</span></span>
<span data-ttu-id="fcd75-124">integración de hello tooconfigure de ThousandEyes en Azure AD, deberá tooadd ThousandEyes de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="fcd75-124">tooconfigure hello integration of ThousandEyes into Azure AD, you need tooadd ThousandEyes from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fcd75-125">**tooadd ThousandEyes de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fcd75-125">**tooadd ThousandEyes from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcd75-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fcd75-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fcd75-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fcd75-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="fcd75-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fcd75-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="fcd75-133">En el cuadro de búsqueda de hello, escriba **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-133">In hello search box, type **ThousandEyes**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="fcd75-135">En el panel de resultados de hello, seleccione **ThousandEyes**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fcd75-135">In hello results panel, select **ThousandEyes**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fcd75-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcd75-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fcd75-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con ThousandEyes con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fcd75-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fcd75-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ThousandEyes es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcd75-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThousandEyes is tooa user in Azure AD.</span></span> <span data-ttu-id="fcd75-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ThousandEyes debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="fcd75-140">In other words, a link relationship between an Azure AD user and hello related user in ThousandEyes needs toobe established.</span></span>

<span data-ttu-id="fcd75-141">En ThousandEyes, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fcd75-141">In ThousandEyes, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fcd75-142">tooconfigure y prueba de inicio de sesión único en Azure AD con ThousandEyes, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fcd75-142">tooconfigure and test Azure AD single sign-on with ThousandEyes, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fcd75-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="fcd75-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fcd75-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fcd75-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fcd75-145">**[Crear un usuario de prueba de ThousandEyes](#creating-a-thousandeyes-test-user) ** -toohave un equivalente de Britta Simon en ThousandEyes que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="fcd75-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - toohave a counterpart of Britta Simon in ThousandEyes that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fcd75-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fcd75-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fcd75-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fcd75-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fcd75-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcd75-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fcd75-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="fcd75-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="fcd75-150">**inicio de sesión único en Azure AD tooconfigure con ThousandEyes, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fcd75-150">**tooconfigure Azure AD single sign-on with ThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcd75-151">En el portal de Azure, en Hola Hola **ThousandEyes** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-151">In hello Azure portal, on hello **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="fcd75-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fcd75-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="fcd75-155">En hello **ThousandEyes dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fcd75-155">On hello **ThousandEyes Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="fcd75-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="fcd75-157">In hello **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="fcd75-158">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fcd75-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="fcd75-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fcd75-160">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fcd75-162">En hello **configuración de ThousandEyes** sección, haga clic en **configurar ThousandEyes** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="fcd75-162">On hello **ThousandEyes Configuration** section, click **Configure ThousandEyes** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fcd75-163">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="fcd75-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="fcd75-165">En una ventana del explorador web diferente, inicie sesión en tooyour **ThousandEyes** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="fcd75-165">In a different web browser window, sign on tooyour **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="fcd75-166">En el menú de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-166">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="fcd75-167">![Configuración](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="fcd75-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="fcd75-168">Haga clic en **Cuenta**</span><span class="sxs-lookup"><span data-stu-id="fcd75-168">Click **Account**</span></span>
   
    <span data-ttu-id="fcd75-169">![Cuenta](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Cuenta")</span><span class="sxs-lookup"><span data-stu-id="fcd75-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="fcd75-170">Haga clic en hello **seguridad y autenticación** ficha.</span><span class="sxs-lookup"><span data-stu-id="fcd75-170">Click hello **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="fcd75-171">![Seguridad y autenticación](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Seguridad y autenticación")</span><span class="sxs-lookup"><span data-stu-id="fcd75-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="fcd75-172">Hola **el programa de instalación Single Sign-On** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fcd75-172">In hello **Setup Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fcd75-173">![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="fcd75-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="fcd75-174">a.</span><span class="sxs-lookup"><span data-stu-id="fcd75-174">a.</span></span> <span data-ttu-id="fcd75-175">Seleccione **Enable Single Sign-On**(Habilitar inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="fcd75-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="fcd75-176">b.</span><span class="sxs-lookup"><span data-stu-id="fcd75-176">b.</span></span> <span data-ttu-id="fcd75-177">En el cuadro de texto **IDP Login URL** (Dirección URL de inicio de sesión de IDP), pegue la **dirección URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fcd75-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="fcd75-178">c.</span><span class="sxs-lookup"><span data-stu-id="fcd75-178">c.</span></span> <span data-ttu-id="fcd75-179">Copie el valor de **Sign-out URL** (Dirección URL de cierre de sesión) que copió de Azure Portal en el cuadro de texto **Logout page URL** (Dirección URL de la página de cierre de sesión).</span><span class="sxs-lookup"><span data-stu-id="fcd75-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="fcd75-180">d.</span><span class="sxs-lookup"><span data-stu-id="fcd75-180">d.</span></span> <span data-ttu-id="fcd75-181">En el cuadro de texto **Emisor de proveedor de identidades**, pegue el valor de **id. de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fcd75-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="fcd75-182">e.</span><span class="sxs-lookup"><span data-stu-id="fcd75-182">e.</span></span> <span data-ttu-id="fcd75-183">En **certificado de comprobación**, haga clic en **Elegir archivo**y, a continuación, cargar el certificado de Hola que ha descargado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fcd75-183">In **Verification Certificate**, click **Choose file**, and then upload hello certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="fcd75-184">f.</span><span class="sxs-lookup"><span data-stu-id="fcd75-184">f.</span></span> <span data-ttu-id="fcd75-185">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="fcd75-186">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="fcd75-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fcd75-187">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="fcd75-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fcd75-188">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fcd75-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fcd75-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcd75-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="fcd75-190">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="fcd75-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="fcd75-192">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fcd75-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcd75-193">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fcd75-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fcd75-195">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fcd75-197">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fcd75-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fcd75-199">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="fcd75-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fcd75-201">a.</span><span class="sxs-lookup"><span data-stu-id="fcd75-201">a.</span></span> <span data-ttu-id="fcd75-202">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fcd75-203">b.</span><span class="sxs-lookup"><span data-stu-id="fcd75-203">b.</span></span> <span data-ttu-id="fcd75-204">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fcd75-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fcd75-205">c.</span><span class="sxs-lookup"><span data-stu-id="fcd75-205">c.</span></span> <span data-ttu-id="fcd75-206">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fcd75-207">d.</span><span class="sxs-lookup"><span data-stu-id="fcd75-207">d.</span></span> <span data-ttu-id="fcd75-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="fcd75-209">Creación de un usuario de prueba de ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="fcd75-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="fcd75-210">En orden tooenable toolog de los usuarios de Azure AD en ThousandEyes, se les deben aprovisionar en ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="fcd75-210">In order tooenable Azure AD users toolog into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="fcd75-211">En caso de hello de ThousandEyes, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="fcd75-211">In hello case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="fcd75-212">Puede usar cualquier otra ThousandEyes usuario cuenta herramienta de creación o las API proporcionadas por ThousandEyes tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="fcd75-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="fcd75-213">**tooprovision un tooThousandEyes de cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fcd75-213">**tooprovision a user account tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcd75-214">Inicie sesión en su sitio de la compañía de ThousandEyes como administrador.</span><span class="sxs-lookup"><span data-stu-id="fcd75-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="fcd75-215">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="fcd75-216">![Configuración](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="fcd75-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="fcd75-217">Haga clic en **Cuenta**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-217">Click **Account**.</span></span>
   
    <span data-ttu-id="fcd75-218">![Cuenta](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Cuenta")</span><span class="sxs-lookup"><span data-stu-id="fcd75-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="fcd75-219">Haga clic en hello **cuentas y usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="fcd75-219">Click hello **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="fcd75-220">![Cuentas y usuarios](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Cuentas y usuarios")</span><span class="sxs-lookup"><span data-stu-id="fcd75-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="fcd75-221">Hola **agregar usuarios y cuentas** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fcd75-221">In hello **Add Users & Accounts** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fcd75-222">![Agregar cuentas de usuario](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Agregar cuentas de usuario")</span><span class="sxs-lookup"><span data-stu-id="fcd75-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="fcd75-223">a.</span><span class="sxs-lookup"><span data-stu-id="fcd75-223">a.</span></span> <span data-ttu-id="fcd75-224">En **nombre** cuadro de texto Nombre de usuario como Hola de tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-224">In **Name** textbox, type hello name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="fcd75-225">b.</span><span class="sxs-lookup"><span data-stu-id="fcd75-225">b.</span></span> <span data-ttu-id="fcd75-226">En **correo electrónico** Hola de tipo de correo electrónico del usuario, cuadro de texto, como ** brittasimon@contoso.com **.</span><span class="sxs-lookup"><span data-stu-id="fcd75-226">In **Email** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="fcd75-227">b.</span><span class="sxs-lookup"><span data-stu-id="fcd75-227">b.</span></span> <span data-ttu-id="fcd75-228">Haga clic en **tooAccount Agregar nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-228">Click **Add New User tooAccount**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="fcd75-229">obtendrá un correo electrónico con un vínculo tooconfirm y activar la cuenta de hello titular de la cuenta de Hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fcd75-229">hello Azure Active Directory account holder will get an email including a link tooconfirm and activate hello account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fcd75-230">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcd75-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fcd75-231">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="fcd75-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThousandEyes.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="fcd75-233">**tooassign Britta Simon tooThousandEyes, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fcd75-233">**tooassign Britta Simon tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcd75-234">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fcd75-236">En la lista de aplicaciones de hello, seleccione **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-236">In hello applications list, select **ThousandEyes**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="fcd75-238">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="fcd75-240">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-240">Click **Add** button.</span></span> <span data-ttu-id="fcd75-241">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="fcd75-243">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="fcd75-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fcd75-244">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fcd75-245">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fcd75-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fcd75-246">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="fcd75-246">Testing single sign-on</span></span>

<span data-ttu-id="fcd75-247">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fcd75-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fcd75-248">Al hacer clic en hello ThousandEyes disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="fcd75-248">When you click hello ThousandEyes tile in hello Access Panel, you should get automatically signed-on tooyour ThousandEyes application.</span></span>

<span data-ttu-id="fcd75-249">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fcd75-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fcd75-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fcd75-250">Additional resources</span></span>

* [<span data-ttu-id="fcd75-251">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fcd75-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fcd75-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fcd75-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

