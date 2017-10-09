---
title: "Tutorial: Integración de Azure Active Directory con Dropbox for Business | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Dropbox para empresas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="8fa60-103">Tutorial: Integración de Azure Active Directory con Dropbox para Empresas</span><span class="sxs-lookup"><span data-stu-id="8fa60-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="8fa60-104">En este tutorial, aprenderá cómo toointegrate Dropbox para empresas con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8fa60-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8fa60-105">Integración de Dropbox para empresas con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8fa60-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8fa60-106">Puede controlar en Azure AD que tenga acceso tooDropbox para la empresa</span><span class="sxs-lookup"><span data-stu-id="8fa60-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="8fa60-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDropbox para la empresa (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa60-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8fa60-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8fa60-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8fa60-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8fa60-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fa60-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8fa60-110">Prerequisites</span></span>

<span data-ttu-id="8fa60-111">tooconfigure integración de Azure AD con Dropbox para empresas, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8fa60-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="8fa60-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa60-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8fa60-113">Una suscripción a Dropbox for Business con inicio de sesión único habilitado.</span><span class="sxs-lookup"><span data-stu-id="8fa60-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8fa60-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8fa60-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8fa60-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8fa60-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8fa60-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8fa60-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8fa60-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8fa60-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8fa60-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8fa60-118">Scenario description</span></span>
<span data-ttu-id="8fa60-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8fa60-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8fa60-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8fa60-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8fa60-121">Adición de Dropbox para empresas de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8fa60-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="8fa60-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa60-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="8fa60-123">Adición de Dropbox para empresas de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8fa60-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="8fa60-124">integración de hello tooconfigure de Dropbox para empresas en Azure AD, necesita tooadd Dropbox para empresas de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8fa60-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8fa60-125">**tooadd Dropbox para empresas de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8fa60-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fa60-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8fa60-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8fa60-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8fa60-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8fa60-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8fa60-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8fa60-133">En el cuadro de búsqueda de hello, escriba **Dropbox para empresas**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="8fa60-135">En el panel de resultados de hello, seleccione **Dropbox para empresas**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8fa60-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8fa60-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa60-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8fa60-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con Dropbox for Business con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8fa60-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8fa60-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Dropbox para empresas es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fa60-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="8fa60-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Dropbox para empresas necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8fa60-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="8fa60-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Dropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="8fa60-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="8fa60-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Dropbox para empresas, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8fa60-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8fa60-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8fa60-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8fa60-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fa60-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8fa60-145">**[Crear una lista desplegable para el usuario de prueba empresarial](#creating-a-dropbox-for-business-test-user)**  -toohave un equivalente de Britta Simon en Dropbox para empresas que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8fa60-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8fa60-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8fa60-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8fa60-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8fa60-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8fa60-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa60-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8fa60-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en Dropbox para aplicaciones de negocios.</span><span class="sxs-lookup"><span data-stu-id="8fa60-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="8fa60-150">**inicio de sesión único en tooconfigure Azure AD con Dropbox para empresas, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8fa60-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fa60-151">En el portal de Azure, en Hola Hola **Dropbox para empresas** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8fa60-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8fa60-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="8fa60-155">En hello **Dropbox para el dominio de negocio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8fa60-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="8fa60-156">a.</span><span class="sxs-lookup"><span data-stu-id="8fa60-156">a.</span></span> <span data-ttu-id="8fa60-157">Inicie sesión en tooyour Dropbox para el inquilino de negocios.</span><span class="sxs-lookup"><span data-stu-id="8fa60-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="8fa60-158">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="8fa60-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8fa60-159">b.</span><span class="sxs-lookup"><span data-stu-id="8fa60-159">b.</span></span> <span data-ttu-id="8fa60-160">En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **consola de administración de**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="8fa60-161">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="8fa60-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8fa60-162">c.</span><span class="sxs-lookup"><span data-stu-id="8fa60-162">c.</span></span> <span data-ttu-id="8fa60-163">En hello **consola de administración de**, haga clic en **autenticación** en el panel de navegación izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8fa60-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="8fa60-164">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="8fa60-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8fa60-165">d.</span><span class="sxs-lookup"><span data-stu-id="8fa60-165">d.</span></span> <span data-ttu-id="8fa60-166">Hola **inicio de sesión único** sección, seleccione **habilitar inicio de sesión único**y, a continuación, haga clic en **más** tooexpand en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8fa60-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="8fa60-167">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="8fa60-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8fa60-168">e.</span><span class="sxs-lookup"><span data-stu-id="8fa60-168">e.</span></span> <span data-ttu-id="8fa60-169">Copiar dirección URL de Hola a continuación demasiado**a los usuarios pueden iniciar sesión escribiendo su dirección de correo electrónico o pueden ir directamente a**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="8fa60-171">f.</span><span class="sxs-lookup"><span data-stu-id="8fa60-171">f.</span></span> <span data-ttu-id="8fa60-172">En el portal de Azure, en Hola Hola **dirección URL de inicio de sesión** cuadro de texto dirección URL de Hola de pegar.</span><span class="sxs-lookup"><span data-stu-id="8fa60-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="8fa60-174">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="8fa60-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8fa60-175">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="8fa60-175">This value is not real value.</span></span> <span data-ttu-id="8fa60-176">Actualice el valor de hello con hello sesión URL real se obtiene de su sección de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8fa60-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="8fa60-177">Póngase en contacto con [Dropbox para el equipo de soporte técnico de cliente empresarial](https://www.dropbox.com/business/contact) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="8fa60-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="8fa60-178">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8fa60-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="8fa60-180">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8fa60-180">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8fa60-182">En hello **Dropbox para configuración de negocios** sección, haga clic en **configurar Dropbox para empresas** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="8fa60-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8fa60-183">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="8fa60-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="8fa60-185">tooconfigure inicio de sesión único en **Dropbox para empresas** en paralelo, vaya el inquilino Dropbox para empresas, Hola **inicio de sesión único** sección de hello **autenticación** página, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8fa60-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="8fa60-186">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="8fa60-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8fa60-187">a.</span><span class="sxs-lookup"><span data-stu-id="8fa60-187">a.</span></span> <span data-ttu-id="8fa60-188">Haga clic en **Required**(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="8fa60-188">Click **Required**.</span></span>
   
    <span data-ttu-id="8fa60-189">b.</span><span class="sxs-lookup"><span data-stu-id="8fa60-189">b.</span></span> <span data-ttu-id="8fa60-190">En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **SAML Single Sign-On dirección URL del servicio** valor y, a continuación, péguelo en hello **dirección URL de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8fa60-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="8fa60-191">c.</span><span class="sxs-lookup"><span data-stu-id="8fa60-191">c.</span></span> <span data-ttu-id="8fa60-192">Haga clic en **Seleccionar certificado**y, a continuación, busque tooyour **archivo de certificado codificado en Base64**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="8fa60-193">d.</span><span class="sxs-lookup"><span data-stu-id="8fa60-193">d.</span></span> <span data-ttu-id="8fa60-194">Haga clic en **guardar cambios** toocomplete configuración de hello en el inquilino DropBox para empresas.</span><span class="sxs-lookup"><span data-stu-id="8fa60-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="8fa60-195">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8fa60-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8fa60-196">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8fa60-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8fa60-197">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8fa60-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8fa60-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa60-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="8fa60-199">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8fa60-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8fa60-201">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8fa60-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fa60-202">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8fa60-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="8fa60-204">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8fa60-206">En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8fa60-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8fa60-208">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8fa60-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8fa60-210">a.</span><span class="sxs-lookup"><span data-stu-id="8fa60-210">a.</span></span> <span data-ttu-id="8fa60-211">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8fa60-212">b.</span><span class="sxs-lookup"><span data-stu-id="8fa60-212">b.</span></span> <span data-ttu-id="8fa60-213">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8fa60-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8fa60-214">c.</span><span class="sxs-lookup"><span data-stu-id="8fa60-214">c.</span></span> <span data-ttu-id="8fa60-215">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8fa60-216">d.</span><span class="sxs-lookup"><span data-stu-id="8fa60-216">d.</span></span> <span data-ttu-id="8fa60-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="8fa60-218">Creación de un usuario de prueba de Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="8fa60-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="8fa60-219">En esta sección, creará un usuario llamado a Britta Simon en Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="8fa60-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="8fa60-220">Dropbox for Business admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8fa60-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="8fa60-221">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8fa60-221">There is no action item for you in this section.</span></span> <span data-ttu-id="8fa60-222">Si un usuario ya no existe en Dropbox para empresas, se crea uno nuevo cuando intente tooaccess Dropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="8fa60-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="8fa60-223">Si necesita toocreate manualmente, póngase en contacto con en un usuario [Dropbox para el equipo de soporte técnico de cliente empresarial](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="8fa60-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8fa60-224">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa60-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8fa60-225">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooDropbox para la empresa.</span><span class="sxs-lookup"><span data-stu-id="8fa60-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8fa60-227">**tooassign Britta Simon tooDropbox para la empresa, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8fa60-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fa60-228">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8fa60-230">En la lista de aplicaciones de hello, seleccione **Dropbox para empresas**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="8fa60-232">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8fa60-234">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-234">Click **Add** button.</span></span> <span data-ttu-id="8fa60-235">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8fa60-237">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8fa60-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8fa60-238">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8fa60-239">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8fa60-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8fa60-240">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8fa60-240">Testing single sign-on</span></span>

<span data-ttu-id="8fa60-241">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8fa60-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8fa60-242">Al hacer clic en hello Dropbox de icono de negocios en el Panel de acceso de hello, obtendrá la página de inicio de sesión de la lista desplegable para aplicaciones de negocios.</span><span class="sxs-lookup"><span data-stu-id="8fa60-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8fa60-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8fa60-243">Additional resources</span></span>

* [<span data-ttu-id="8fa60-244">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fa60-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8fa60-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8fa60-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8fa60-246">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="8fa60-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

