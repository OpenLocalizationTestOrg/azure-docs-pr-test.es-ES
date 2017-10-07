---
title: "Tutorial: Integración de Azure Active Directory con Small Improvements | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y pequeñas mejoras."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="b67e0-103">Tutorial: Integración de Azure Active Directory con Small Improvements</span><span class="sxs-lookup"><span data-stu-id="b67e0-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="b67e0-104">En este tutorial, aprenderá cómo toointegrate pequeñas mejoras con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b67e0-104">In this tutorial, you learn how toointegrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b67e0-105">Integración pequeñas mejoras con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b67e0-105">Integrating Small Improvements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b67e0-106">Puede controlar en Azure AD que tenga acceso tooSmall mejoras</span><span class="sxs-lookup"><span data-stu-id="b67e0-106">You can control in Azure AD who has access tooSmall Improvements</span></span>
- <span data-ttu-id="b67e0-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSmall mejoras (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67e0-107">You can enable your users tooautomatically get signed-on tooSmall Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b67e0-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b67e0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b67e0-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b67e0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b67e0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b67e0-110">Prerequisites</span></span>

<span data-ttu-id="b67e0-111">integración de Azure AD con pequeñas mejoras tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b67e0-111">tooconfigure Azure AD integration with Small Improvements, you need hello following items:</span></span>

- <span data-ttu-id="b67e0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b67e0-113">Una suscripción habilitada para el inicio de sesión único en Small Improvements</span><span class="sxs-lookup"><span data-stu-id="b67e0-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b67e0-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b67e0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b67e0-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b67e0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b67e0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b67e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b67e0-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes [oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b67e0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b67e0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b67e0-118">Scenario description</span></span>
<span data-ttu-id="b67e0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b67e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b67e0-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="b67e0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b67e0-121">Adición de pequeñas mejoras de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b67e0-121">Adding Small Improvements from hello gallery</span></span>
2. <span data-ttu-id="b67e0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-hello-gallery"></a><span data-ttu-id="b67e0-123">Adición de pequeñas mejoras de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b67e0-123">Adding Small Improvements from hello gallery</span></span>
<span data-ttu-id="b67e0-124">integración de hello tooconfigure de pequeñas mejoras en Azure AD, deberá tooadd pequeñas mejoras en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="b67e0-124">tooconfigure hello integration of Small Improvements into Azure AD, you need tooadd Small Improvements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b67e0-125">**tooadd pequeñas mejoras de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b67e0-125">**tooadd Small Improvements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b67e0-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b67e0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b67e0-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b67e0-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b67e0-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b67e0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b67e0-133">En el cuadro de búsqueda de hello, escriba **pequeñas mejoras**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-133">In hello search box, type **Small Improvements**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="b67e0-135">En el panel de resultados de hello, seleccione **pequeñas mejoras**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b67e0-135">In hello results panel, select **Small Improvements**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b67e0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67e0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b67e0-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Small Improvements utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b67e0-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b67e0-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en pequeñas mejoras es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b67e0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Small Improvements is tooa user in Azure AD.</span></span> <span data-ttu-id="b67e0-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en pequeñas mejoras debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="b67e0-140">In other words, a link relationship between an Azure AD user and hello related user in Small Improvements needs toobe established.</span></span>

<span data-ttu-id="b67e0-141">En pequeñas mejoras, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b67e0-141">In Small Improvements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b67e0-142">tooconfigure y prueba de inicio de sesión único en Azure AD con pequeñas mejoras, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b67e0-142">tooconfigure and test Azure AD single sign-on with Small Improvements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b67e0-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="b67e0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b67e0-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b67e0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b67e0-145">**[Crear un usuario de prueba de pequeñas mejoras](#creating-a-small-improvements-test-user) ** -toohave un equivalente de Britta Simon en pequeñas mejoras es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="b67e0-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - toohave a counterpart of Britta Simon in Small Improvements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b67e0-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b67e0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b67e0-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b67e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b67e0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67e0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b67e0-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de pequeñas mejoras.</span><span class="sxs-lookup"><span data-stu-id="b67e0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="b67e0-150">**inicio de sesión único en Azure AD tooconfigure con pequeñas mejoras, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b67e0-150">**tooconfigure Azure AD single sign-on with Small Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="b67e0-151">En el portal de Azure, en Hola Hola **pequeñas mejoras** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-151">In hello Azure portal, on hello **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b67e0-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b67e0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="b67e0-155">En hello **pequeño dominio mejoras y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b67e0-155">On hello **Small Improvements Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="b67e0-157">a.</span><span class="sxs-lookup"><span data-stu-id="b67e0-157">a.</span></span> <span data-ttu-id="b67e0-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="b67e0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="b67e0-159">b.</span><span class="sxs-lookup"><span data-stu-id="b67e0-159">b.</span></span> <span data-ttu-id="b67e0-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="b67e0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b67e0-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="b67e0-161">These values are not real.</span></span> <span data-ttu-id="b67e0-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="b67e0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b67e0-163">Póngase en contacto con [equipo de soporte técnico de cliente de pequeñas mejoras](mailto:support@small-improvements.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="b67e0-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="b67e0-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b67e0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="b67e0-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b67e0-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b67e0-168">En hello **configuración de mejoras pequeño** sección, haga clic en **configurar pequeñas mejoras** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="b67e0-168">On hello **Small Improvements Configuration** section, click **Configure Small Improvements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b67e0-169">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="b67e0-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="b67e0-171">En otra ventana del explorador, inicie sesión en el sitio de empresa de tooyour pequeñas mejoras como administrador.</span><span class="sxs-lookup"><span data-stu-id="b67e0-171">In another browser window, sign on tooyour Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="b67e0-172">En la página del panel principal de hello, haga clic en **administración** botón Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="b67e0-172">From hello main dashboard page, click **Administration** button on hello left.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="b67e0-174">Haga clic en hello **SSO de SAML** botón de **integraciones** sección.</span><span class="sxs-lookup"><span data-stu-id="b67e0-174">Click hello **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="b67e0-176">En la página de configuración de SSO de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b67e0-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="b67e0-178">a.</span><span class="sxs-lookup"><span data-stu-id="b67e0-178">a.</span></span> <span data-ttu-id="b67e0-179">Hola **extremo HTTP** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b67e0-179">In hello **HTTP Endpoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b67e0-180">b.</span><span class="sxs-lookup"><span data-stu-id="b67e0-180">b.</span></span> <span data-ttu-id="b67e0-181">Abra el certificado descargado en el Bloc de notas, Hola copiar contenido y, a continuación, péguelo en hello **x509 certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="b67e0-181">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="b67e0-182">c.</span><span class="sxs-lookup"><span data-stu-id="b67e0-182">c.</span></span> <span data-ttu-id="b67e0-183">Si desea toohave SSO y el inicio de sesión de formulario opción de autenticación disponible para los usuarios, a continuación, compruebe hello **habilitan el acceso mediante inicio de sesión y contraseña demasiado** opción.</span><span class="sxs-lookup"><span data-stu-id="b67e0-183">If you wish toohave SSO and Login form authentication option available for users, then check hello **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="b67e0-184">d.</span><span class="sxs-lookup"><span data-stu-id="b67e0-184">d.</span></span> <span data-ttu-id="b67e0-185">Escriba el botón de inicio de sesión de SSO de hello valor adecuado tooName Hola Hola **SAML Prompt** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="b67e0-185">Enter hello appropriate value tooName hello SSO Login button in hello **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="b67e0-186">e.</span><span class="sxs-lookup"><span data-stu-id="b67e0-186">e.</span></span> <span data-ttu-id="b67e0-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b67e0-188">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="b67e0-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b67e0-189">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="b67e0-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b67e0-190">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b67e0-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b67e0-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67e0-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="b67e0-192">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="b67e0-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b67e0-194">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b67e0-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b67e0-195">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b67e0-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b67e0-197">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b67e0-199">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b67e0-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b67e0-201">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="b67e0-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b67e0-203">a.</span><span class="sxs-lookup"><span data-stu-id="b67e0-203">a.</span></span> <span data-ttu-id="b67e0-204">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b67e0-205">b.</span><span class="sxs-lookup"><span data-stu-id="b67e0-205">b.</span></span> <span data-ttu-id="b67e0-206">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b67e0-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b67e0-207">c.</span><span class="sxs-lookup"><span data-stu-id="b67e0-207">c.</span></span> <span data-ttu-id="b67e0-208">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b67e0-209">d.</span><span class="sxs-lookup"><span data-stu-id="b67e0-209">d.</span></span> <span data-ttu-id="b67e0-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="b67e0-211">Creación de un usuario de prueba de Small Improvements</span><span class="sxs-lookup"><span data-stu-id="b67e0-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="b67e0-212">toolog de los usuarios de Azure AD tooenable en tooSmall mejoras, se les deben aprovisionar en pequeñas mejoras.</span><span class="sxs-lookup"><span data-stu-id="b67e0-212">tooenable Azure AD users toolog in tooSmall Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="b67e0-213">En caso de hello de pequeñas mejoras, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="b67e0-213">In hello case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="b67e0-214">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b67e0-214">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b67e0-215">Sitio de empresa de pequeñas mejoras tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="b67e0-215">Sign-on tooyour Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="b67e0-216">Desde la página de inicio de hello, vaya toohello menú Hola izquierda, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-216">From hello Home page, go toohello menu on hello left, click **Administration**.</span></span>

3. <span data-ttu-id="b67e0-217">Haga clic en hello **directorio usuario** botón desde la sección de administración de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b67e0-217">Click hello **User Directory** button from User Management section.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="b67e0-219">Haga clic en **Agregar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-219">Click **Add users**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="b67e0-221">En hello **agregar usuarios** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b67e0-221">On hello **Add Users** dialog, perform hello following steps:</span></span> 

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="b67e0-223">a.</span><span class="sxs-lookup"><span data-stu-id="b67e0-223">a.</span></span> <span data-ttu-id="b67e0-224">Escriba hello **nombre** del usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-224">Enter hello **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="b67e0-225">b.</span><span class="sxs-lookup"><span data-stu-id="b67e0-225">b.</span></span> <span data-ttu-id="b67e0-226">Escriba hello **apellidos** del usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-226">Enter hello **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="b67e0-227">c.</span><span class="sxs-lookup"><span data-stu-id="b67e0-227">c.</span></span> <span data-ttu-id="b67e0-228">Escriba hello **correo electrónico** del usuario como ** brittasimon@contoso.com **.</span><span class="sxs-lookup"><span data-stu-id="b67e0-228">Enter hello **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="b67e0-229">d.</span><span class="sxs-lookup"><span data-stu-id="b67e0-229">d.</span></span> <span data-ttu-id="b67e0-230">También puede elegir mensaje personal de tooenter Hola Hola **enviar correo electrónico de notificación** cuadro.</span><span class="sxs-lookup"><span data-stu-id="b67e0-230">You can also choose tooenter hello personal message in hello **Send notification email** box.</span></span> <span data-ttu-id="b67e0-231">Si no desea toosend notificación de hello, a continuación, desactive esta casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="b67e0-231">If you do not wish toosend hello notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="b67e0-232">e.</span><span class="sxs-lookup"><span data-stu-id="b67e0-232">e.</span></span> <span data-ttu-id="b67e0-233">Haga clic en **Crear usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-233">Click **Create Users**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b67e0-234">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67e0-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b67e0-235">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSmall mejoras.</span><span class="sxs-lookup"><span data-stu-id="b67e0-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmall Improvements.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b67e0-237">**tooassign Britta Simon tooSmall mejoras, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b67e0-237">**tooassign Britta Simon tooSmall Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="b67e0-238">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b67e0-240">En la lista de aplicaciones de hello, seleccione **pequeñas mejoras**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-240">In hello applications list, select **Small Improvements**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="b67e0-242">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b67e0-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-244">Click **Add** button.</span></span> <span data-ttu-id="b67e0-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b67e0-247">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="b67e0-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b67e0-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b67e0-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b67e0-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b67e0-250">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b67e0-250">Testing single sign-on</span></span>

<span data-ttu-id="b67e0-251">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b67e0-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="b67e0-252">Al hacer clic en icono pequeñas mejoras en el Panel de acceso de Hola de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicaciones pequeñas mejoras.</span><span class="sxs-lookup"><span data-stu-id="b67e0-252">When you click hello Small Improvements tile in hello Access Panel, you should get automatically signed-on tooyour Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b67e0-253">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b67e0-253">Additional resources</span></span>

* [<span data-ttu-id="b67e0-254">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b67e0-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b67e0-255">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b67e0-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

