---
title: "Tutorial: Integración de Azure Active Directory con UserEcho | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y UserEcho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="c739f-103">Tutorial: integración de Azure Active Directory con UserEcho</span><span class="sxs-lookup"><span data-stu-id="c739f-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="c739f-104">En este tutorial, aprenderá cómo toointegrate UserEcho con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c739f-104">In this tutorial, you learn how toointegrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c739f-105">Integración UserEcho con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c739f-105">Integrating UserEcho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c739f-106">Puede controlar en Azure AD que tenga acceso tooUserEcho</span><span class="sxs-lookup"><span data-stu-id="c739f-106">You can control in Azure AD who has access tooUserEcho</span></span>
- <span data-ttu-id="c739f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooUserEcho (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c739f-107">You can enable your users tooautomatically get signed-on tooUserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c739f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c739f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c739f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c739f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c739f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c739f-110">Prerequisites</span></span>

<span data-ttu-id="c739f-111">integración de Azure AD con UserEcho tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c739f-111">tooconfigure Azure AD integration with UserEcho, you need hello following items:</span></span>

- <span data-ttu-id="c739f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c739f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c739f-113">Una suscripción a UserEcho habilitada para inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="c739f-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c739f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c739f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c739f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c739f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c739f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c739f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c739f-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c739f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c739f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c739f-118">Scenario description</span></span>
<span data-ttu-id="c739f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c739f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c739f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c739f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c739f-121">Agregar UserEcho desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c739f-121">Adding UserEcho from hello gallery</span></span>
2. <span data-ttu-id="c739f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c739f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-hello-gallery"></a><span data-ttu-id="c739f-123">Agregar UserEcho desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c739f-123">Adding UserEcho from hello gallery</span></span>
<span data-ttu-id="c739f-124">integración de hello tooconfigure de UserEcho en Azure AD, deberá tooadd UserEcho de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c739f-124">tooconfigure hello integration of UserEcho into Azure AD, you need tooadd UserEcho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c739f-125">**tooadd UserEcho de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c739f-125">**tooadd UserEcho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c739f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c739f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c739f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c739f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c739f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c739f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c739f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c739f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c739f-133">En el cuadro de búsqueda de hello, escriba **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="c739f-133">In hello search box, type **UserEcho**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="c739f-135">En el panel de resultados de hello, seleccione **UserEcho**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c739f-135">In hello results panel, select **UserEcho**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c739f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c739f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c739f-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con UserEcho con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c739f-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c739f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en UserEcho es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c739f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserEcho is tooa user in Azure AD.</span></span> <span data-ttu-id="c739f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en UserEcho debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c739f-140">In other words, a link relationship between an Azure AD user and hello related user in UserEcho needs toobe established.</span></span>

<span data-ttu-id="c739f-141">En UserEcho, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c739f-141">In UserEcho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c739f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con UserEcho, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c739f-142">tooconfigure and test Azure AD single sign-on with UserEcho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c739f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c739f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c739f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c739f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c739f-145">**[Crear un usuario de prueba UserEcho](#creating-a-userecho-test-user)**  -toohave un equivalente de Britta Simon en UserEcho que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c739f-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - toohave a counterpart of Britta Simon in UserEcho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c739f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c739f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c739f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c739f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c739f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c739f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c739f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación UserEcho.</span><span class="sxs-lookup"><span data-stu-id="c739f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="c739f-150">**inicio de sesión único en Azure AD tooconfigure con UserEcho, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c739f-150">**tooconfigure Azure AD single sign-on with UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="c739f-151">En el portal de Azure, en Hola Hola **UserEcho** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c739f-151">In hello Azure portal, on hello **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c739f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c739f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="c739f-155">En hello **UserEcho dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c739f-155">On hello **UserEcho Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="c739f-157">a.</span><span class="sxs-lookup"><span data-stu-id="c739f-157">a.</span></span> <span data-ttu-id="c739f-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="c739f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="c739f-159">b.</span><span class="sxs-lookup"><span data-stu-id="c739f-159">b.</span></span> <span data-ttu-id="c739f-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="c739f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c739f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c739f-161">These values are not real.</span></span> <span data-ttu-id="c739f-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="c739f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c739f-163">Póngase en contacto con [equipo de soporte técnico de cliente de UserEcho](https://feedback.userecho.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="c739f-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) tooget these values.</span></span> 

4. <span data-ttu-id="c739f-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c739f-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="c739f-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c739f-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c739f-168">En hello **UserEcho configuración** sección, haga clic en **configurar UserEcho** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="c739f-168">On hello **UserEcho Configuration** section, click **Configure UserEcho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c739f-169">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="c739f-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="c739f-171">En otra ventana del explorador, inicie sesión en el sitio de empresa de tooyour UserEcho como administrador.</span><span class="sxs-lookup"><span data-stu-id="c739f-171">In another browser window, sign on tooyour UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="c739f-172">En la barra de herramientas de hello en la parte superior de hello, haga clic en el menú de hello tooexpand del nombre de usuario y, a continuación, haga clic en **el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="c739f-172">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="c739f-174">Haga clic en **Integraciones**.</span><span class="sxs-lookup"><span data-stu-id="c739f-174">Click **Integrations**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="c739f-176">Haga clic en **Sitio web** y, después, en **Inicio de sesión único (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="c739f-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="c739f-178">En hello **inicio de sesión único (SAML)** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c739f-178">On hello **Single sign-on (SAML)** page, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="c739f-180">a.</span><span class="sxs-lookup"><span data-stu-id="c739f-180">a.</span></span> <span data-ttu-id="c739f-181">En **Habilitado para SAML**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="c739f-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="c739f-182">b.</span><span class="sxs-lookup"><span data-stu-id="c739f-182">b.</span></span> <span data-ttu-id="c739f-183">Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **dirección URL SSO SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c739f-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="c739f-184">c.</span><span class="sxs-lookup"><span data-stu-id="c739f-184">c.</span></span> <span data-ttu-id="c739f-185">Pegar **dirección URL de cierre de sesión**, que haya copiado desde Hola portal de Azure en hello **logoout remoto URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c739f-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="c739f-186">d.</span><span class="sxs-lookup"><span data-stu-id="c739f-186">d.</span></span> <span data-ttu-id="c739f-187">Abra el certificado descargado en el Bloc de notas, Hola copiar contenido y, a continuación, péguelo en hello **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c739f-187">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="c739f-188">e.</span><span class="sxs-lookup"><span data-stu-id="c739f-188">e.</span></span> <span data-ttu-id="c739f-189">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c739f-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c739f-190">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c739f-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c739f-191">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c739f-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c739f-192">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c739f-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c739f-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c739f-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c739f-194">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c739f-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c739f-196">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c739f-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c739f-197">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c739f-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c739f-199">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c739f-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c739f-201">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c739f-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c739f-203">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c739f-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c739f-205">a.</span><span class="sxs-lookup"><span data-stu-id="c739f-205">a.</span></span> <span data-ttu-id="c739f-206">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c739f-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c739f-207">b.</span><span class="sxs-lookup"><span data-stu-id="c739f-207">b.</span></span> <span data-ttu-id="c739f-208">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c739f-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c739f-209">c.</span><span class="sxs-lookup"><span data-stu-id="c739f-209">c.</span></span> <span data-ttu-id="c739f-210">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c739f-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c739f-211">d.</span><span class="sxs-lookup"><span data-stu-id="c739f-211">d.</span></span> <span data-ttu-id="c739f-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c739f-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="c739f-213">Creación de un usuario de prueba de UserEcho</span><span class="sxs-lookup"><span data-stu-id="c739f-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="c739f-214">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en UserEcho toocreate.</span><span class="sxs-lookup"><span data-stu-id="c739f-214">hello objective of this section is toocreate a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="c739f-215">**toocreate un usuario llamado Britta Simon en UserEcho, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c739f-215">**toocreate a user called Britta Simon in UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="c739f-216">Sitio de empresa de UserEcho tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="c739f-216">Sign-on tooyour UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="c739f-217">En la barra de herramientas de hello en la parte superior de hello, haga clic en el menú de hello tooexpand del nombre de usuario y, a continuación, haga clic en **el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="c739f-217">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="c739f-219">Haga clic en **usuarios**, hello tooexpand **usuarios** sección.</span><span class="sxs-lookup"><span data-stu-id="c739f-219">Click **Users**, tooexpand hello **Users** section.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="c739f-221">Haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c739f-221">Click **Users**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="c739f-223">Haga clic en **Invitar a un nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="c739f-223">Click **Invite a new user**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="c739f-225">En hello **invitar a un nuevo usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c739f-225">On hello **Invite a new user** dialog, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="c739f-227">a.</span><span class="sxs-lookup"><span data-stu-id="c739f-227">a.</span></span> <span data-ttu-id="c739f-228">Hola **nombre** cuadro de texto, nombre de tipo de usuario de hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c739f-228">In hello **Name** textbox, type name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="c739f-229">b.</span><span class="sxs-lookup"><span data-stu-id="c739f-229">b.</span></span>  <span data-ttu-id="c739f-230">Hola **correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c739f-230">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="c739f-231">c.</span><span class="sxs-lookup"><span data-stu-id="c739f-231">c.</span></span> <span data-ttu-id="c739f-232">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="c739f-232">Click **Invite**.</span></span>

<span data-ttu-id="c739f-233">Se envía una invitación tooBritta, lo que permite su toostart con UserEcho.</span><span class="sxs-lookup"><span data-stu-id="c739f-233">An invitation is sent tooBritta, which enables her toostart using UserEcho.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c739f-234">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c739f-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c739f-235">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooUserEcho.</span><span class="sxs-lookup"><span data-stu-id="c739f-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserEcho.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c739f-237">**tooassign Britta Simon tooUserEcho, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c739f-237">**tooassign Britta Simon tooUserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="c739f-238">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c739f-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c739f-240">En la lista de aplicaciones de hello, seleccione **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="c739f-240">In hello applications list, select **UserEcho**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="c739f-242">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c739f-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c739f-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c739f-244">Click **Add** button.</span></span> <span data-ttu-id="c739f-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c739f-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c739f-247">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c739f-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c739f-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c739f-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c739f-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c739f-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c739f-250">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c739f-250">Testing single sign-on</span></span>

<span data-ttu-id="c739f-251">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c739f-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="c739f-252">Al hacer clic en icono de UserEcho Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour UserEcho aplicación.</span><span class="sxs-lookup"><span data-stu-id="c739f-252">When you click hello UserEcho tile in hello Access Panel, you should get automatically signed-on tooyour UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c739f-253">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c739f-253">Additional resources</span></span>

* [<span data-ttu-id="c739f-254">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c739f-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c739f-255">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c739f-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

