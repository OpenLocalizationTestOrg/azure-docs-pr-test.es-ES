---
title: "Tutorial: Integración de Azure Active Directory con Kiteworks | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="6a1b4-103">Tutorial: Integración de Azure Active Directory con Kiteworks</span><span class="sxs-lookup"><span data-stu-id="6a1b4-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="6a1b4-104">En este tutorial, aprenderá cómo toointegrate Kiteworks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a1b4-104">In this tutorial, you learn how toointegrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a1b4-105">Integración Kiteworks con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6a1b4-105">Integrating Kiteworks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6a1b4-106">Puede controlar en Azure AD que tenga acceso tooKiteworks</span><span class="sxs-lookup"><span data-stu-id="6a1b4-106">You can control in Azure AD who has access tooKiteworks</span></span>
- <span data-ttu-id="6a1b4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKiteworks (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a1b4-107">You can enable your users tooautomatically get signed-on tooKiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a1b4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6a1b4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6a1b4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a1b4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a1b4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6a1b4-110">Prerequisites</span></span>

<span data-ttu-id="6a1b4-111">integración de Azure AD con Kiteworks tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6a1b4-111">tooconfigure Azure AD integration with Kiteworks, you need hello following items:</span></span>

- <span data-ttu-id="6a1b4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a1b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a1b4-113">Una suscripción habilitada para inicio de sesión único en Kiteworks</span><span class="sxs-lookup"><span data-stu-id="6a1b4-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a1b4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a1b4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6a1b4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a1b4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a1b4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a1b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a1b4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6a1b4-118">Scenario description</span></span>
<span data-ttu-id="6a1b4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a1b4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="6a1b4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a1b4-121">Agregar Kiteworks desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6a1b4-121">Adding Kiteworks from hello gallery</span></span>
2. <span data-ttu-id="6a1b4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a1b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-hello-gallery"></a><span data-ttu-id="6a1b4-123">Agregar Kiteworks desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6a1b4-123">Adding Kiteworks from hello gallery</span></span>
<span data-ttu-id="6a1b4-124">integración de hello tooconfigure de Kiteworks en Azure AD, deberá tooadd Kiteworks de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-124">tooconfigure hello integration of Kiteworks into Azure AD, you need tooadd Kiteworks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6a1b4-125">**tooadd Kiteworks de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6a1b4-125">**tooadd Kiteworks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a1b4-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a1b4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6a1b4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="6a1b4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="6a1b4-133">En el cuadro de búsqueda de hello, escriba **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-133">In hello search box, type **Kiteworks**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="6a1b4-135">En el panel de resultados de hello, seleccione **Kiteworks**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-135">In hello results panel, select **Kiteworks**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a1b4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a1b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a1b4-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Kiteworks con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6a1b4-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a1b4-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kiteworks es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kiteworks is tooa user in Azure AD.</span></span> <span data-ttu-id="6a1b4-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kiteworks debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-140">In other words, a link relationship between an Azure AD user and hello related user in Kiteworks needs toobe established.</span></span>

<span data-ttu-id="6a1b4-141">En Kiteworks, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-141">In Kiteworks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6a1b4-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Kiteworks, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6a1b4-142">tooconfigure and test Azure AD single sign-on with Kiteworks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6a1b4-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6a1b4-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a1b4-145">**[Crear un usuario de prueba Kiteworks](#creating-a-kiteworks-test-user)**  -toohave un equivalente de Britta Simon en Kiteworks que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - toohave a counterpart of Britta Simon in Kiteworks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a1b4-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a1b4-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a1b4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a1b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a1b4-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="6a1b4-150">**inicio de sesión único en Azure AD tooconfigure con Kiteworks, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6a1b4-150">**tooconfigure Azure AD single sign-on with Kiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a1b4-151">En el portal de Azure, en Hola Hola **Kiteworks** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-151">In hello Azure portal, on hello **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="6a1b4-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="6a1b4-155">En hello **Kiteworks dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6a1b4-155">On hello **Kiteworks Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="6a1b4-157">a.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-157">a.</span></span> <span data-ttu-id="6a1b4-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="6a1b4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="6a1b4-159">b.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-159">b.</span></span> <span data-ttu-id="6a1b4-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="6a1b4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a1b4-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-161">These values are not real.</span></span> <span data-ttu-id="6a1b4-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6a1b4-163">Póngase en contacto con [equipo de soporte técnico de cliente de Kiteworks](http://accellion.com/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-163">Contact [Kiteworks Client support team](http://accellion.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="6a1b4-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="6a1b4-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6a1b4-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a1b4-168">En hello **Kiteworks configuración** sección, haga clic en **configurar Kiteworks** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-168">On hello **Kiteworks Configuration** section, click **Configure Kiteworks** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6a1b4-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="6a1b4-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="6a1b4-171">Inicie sesión en tooyour Kiteworks sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-171">Sign on tooyour Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="6a1b4-172">En la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="6a1b4-174">Hola **autenticación y autorización** sección, haga clic en **el programa de instalación de SSO**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-174">In hello **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="6a1b4-176">En la página de configuración de SSO de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6a1b4-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="6a1b4-178">a.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-178">a.</span></span> <span data-ttu-id="6a1b4-179">Seleccione **Autenticar mediante SSO**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="6a1b4-180">b.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-180">b.</span></span> <span data-ttu-id="6a1b4-181">Seleccione **Iniciar AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="6a1b4-182">c.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-182">c.</span></span> <span data-ttu-id="6a1b4-183">Hola **Id. de entidad IDP** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="6a1b4-184">d.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-184">d.</span></span> <span data-ttu-id="6a1b4-185">Hola **URL de servicio de inicio de sesión único** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-185">In hello **Single Sign-On Service URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6a1b4-186">e.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-186">e.</span></span> <span data-ttu-id="6a1b4-187">Hola **dirección URL del servicio de cierre de sesión único** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-187">In hello **Single Logout Service URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6a1b4-188">f.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-188">f.</span></span> <span data-ttu-id="6a1b4-189">Abra el certificado descargado en el Bloc de notas, Hola copiar contenido y, a continuación, péguelo en hello **certificado de clave pública RSA** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-189">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="6a1b4-190">g.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-190">g.</span></span> <span data-ttu-id="6a1b4-191">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6a1b4-192">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="6a1b4-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6a1b4-193">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6a1b4-194">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a1b4-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a1b4-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a1b4-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a1b4-196">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="6a1b4-198">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6a1b4-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a1b4-199">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a1b4-201">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a1b4-203">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a1b4-205">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="6a1b4-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a1b4-207">a.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-207">a.</span></span> <span data-ttu-id="6a1b4-208">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a1b4-209">b.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-209">b.</span></span> <span data-ttu-id="6a1b4-210">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a1b4-211">c.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-211">c.</span></span> <span data-ttu-id="6a1b4-212">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6a1b4-213">d.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-213">d.</span></span> <span data-ttu-id="6a1b4-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="6a1b4-215">Creación de un usuario de prueba en Kiteworks</span><span class="sxs-lookup"><span data-stu-id="6a1b4-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="6a1b4-216">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Kiteworks toocreate.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-216">hello objective of this section is toocreate a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="6a1b4-217">Kiteworks admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="6a1b4-218">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-218">There is no action item for you in this section.</span></span> <span data-ttu-id="6a1b4-219">Se crea un nuevo usuario durante un tooaccess intento Kitewors si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-219">A new user is created during an attempt tooaccess Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="6a1b4-220">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="6a1b4-220">If you need toocreate a user manually, you need toocontact hello [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6a1b4-221">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a1b4-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6a1b4-222">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKiteworks.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKiteworks.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="6a1b4-224">**tooassign Britta Simon tooKiteworks, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6a1b4-224">**tooassign Britta Simon tooKiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a1b4-225">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6a1b4-227">En la lista de aplicaciones de hello, seleccione **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-227">In hello applications list, select **Kiteworks**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="6a1b4-229">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="6a1b4-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-231">Click **Add** button.</span></span> <span data-ttu-id="6a1b4-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="6a1b4-234">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6a1b4-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a1b4-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a1b4-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="6a1b4-237">Testing single sign-on</span></span>

<span data-ttu-id="6a1b4-238">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-238">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="6a1b4-239">Al hacer clic en hello Kiteworks el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Kiteworks aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a1b4-239">When you click hello Kiteworks tile in hello Access Panel, you should get automatically signed-on tooyour Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a1b4-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6a1b4-240">Additional resources</span></span>

* [<span data-ttu-id="6a1b4-241">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a1b4-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a1b4-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6a1b4-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

