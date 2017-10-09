---
title: "Tutorial: Integración de Azure Active Directory con Learning at Work | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y aprendizaje en el trabajo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: fa09d585d57932a95cadba9a66029765d7df3694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="cc36c-103">Tutorial: integración de Azure Active Directory con Learning at Work</span><span class="sxs-lookup"><span data-stu-id="cc36c-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="cc36c-104">En este tutorial, aprenderá cómo toointegrate de aprendizaje en el trabajo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc36c-104">In this tutorial, you learn how toointegrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc36c-105">Integración de aprendizaje en el trabajo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cc36c-105">Integrating Learning at Work with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc36c-106">Puede controlar en Azure AD que tenga acceso tooLearning en el trabajo</span><span class="sxs-lookup"><span data-stu-id="cc36c-106">You can control in Azure AD who has access tooLearning at Work</span></span>
- <span data-ttu-id="cc36c-107">Puede habilitar la get ha iniciado sesión tooLearning de usuarios tooautomatically en el trabajo (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36c-107">You can enable your users tooautomatically get signed-on tooLearning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc36c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cc36c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cc36c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc36c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc36c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cc36c-110">Prerequisites</span></span>

<span data-ttu-id="cc36c-111">tooconfigure integración de Azure AD con aprendizaje en el trabajo, deberá Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cc36c-111">tooconfigure Azure AD integration with Learning at Work, you need hello following items:</span></span>

- <span data-ttu-id="cc36c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc36c-113">Una suscripción habilitada para el inicio de sesión único en Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="cc36c-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc36c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cc36c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc36c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cc36c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc36c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cc36c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc36c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc36c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc36c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cc36c-118">Scenario description</span></span>
<span data-ttu-id="cc36c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cc36c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc36c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cc36c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc36c-121">Adición de aprendizaje en el trabajo de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cc36c-121">Adding Learning at Work from hello gallery</span></span>
2. <span data-ttu-id="cc36c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-hello-gallery"></a><span data-ttu-id="cc36c-123">Adición de aprendizaje en el trabajo de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cc36c-123">Adding Learning at Work from hello gallery</span></span>
<span data-ttu-id="cc36c-124">integración de hello tooconfigure de aprendizaje en el trabajo en Azure AD, deberá tooadd en el trabajo de aprendizaje de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="cc36c-124">tooconfigure hello integration of Learning at Work into Azure AD, you need tooadd Learning at Work from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc36c-125">**tooadd de aprendizaje en el trabajo de la Galería de hello, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc36c-125">**tooadd Learning at Work from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc36c-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cc36c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc36c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc36c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="cc36c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cc36c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="cc36c-133">En el cuadro de búsqueda de hello, escriba **en el trabajo de aprendizaje**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-133">In hello search box, type **Learning at Work**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="cc36c-135">En el panel de resultados de hello, seleccione **en el trabajo de aprendizaje**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cc36c-135">In hello results panel, select **Learning at Work**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc36c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc36c-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Learning at Work con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc36c-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc36c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el aprendizaje en el trabajo es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc36c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning at Work is tooa user in Azure AD.</span></span> <span data-ttu-id="cc36c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el aprendizaje en el trabajo debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="cc36c-140">In other words, a link relationship between an Azure AD user and hello related user in Learning at Work needs toobe established.</span></span>

<span data-ttu-id="cc36c-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en aprendizaje en el trabajo.</span><span class="sxs-lookup"><span data-stu-id="cc36c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning at Work.</span></span>

<span data-ttu-id="cc36c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con aprendizaje en el trabajo, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cc36c-142">tooconfigure and test Azure AD single sign-on with Learning at Work, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc36c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cc36c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc36c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc36c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc36c-145">**[Crear un aprendizaje en usuario de prueba de trabajo](#creating-a-learning-at-work-test-user)**  -toohave un equivalente de Britta Simon en aprendizaje en el trabajo que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="cc36c-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - toohave a counterpart of Britta Simon in Learning at Work that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc36c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cc36c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc36c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cc36c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc36c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc36c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su aprendizaje en la aplicación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cc36c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="cc36c-150">**inicio de sesión único en Azure AD tooconfigure con aprendizaje en el trabajo, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc36c-150">**tooconfigure Azure AD single sign-on with Learning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc36c-151">En el portal de Azure, en Hola Hola **en el trabajo de aprendizaje** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-151">In hello Azure portal, on hello **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cc36c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cc36c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="cc36c-155">En hello **de aprendizaje en el dominio de trabajo y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cc36c-155">On hello **Learning at Work Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="cc36c-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc36c-157">a.</span></span> <span data-ttu-id="cc36c-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="cc36c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="cc36c-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc36c-159">b.</span></span> <span data-ttu-id="cc36c-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="cc36c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc36c-161">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="cc36c-161">These values are not hello real.</span></span> <span data-ttu-id="cc36c-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="cc36c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cc36c-163">Póngase en contacto con [de aprendizaje en el equipo de soporte técnico de trabajo cliente](https://www.learninga-z.com/site/contact/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="cc36c-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="cc36c-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="cc36c-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="cc36c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cc36c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc36c-168">En hello **al configurar el trabajo de aprendizaje** sección, haga clic en **configurar aprendizaje en el trabajo** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="cc36c-168">On hello **Learning at Work Configuration** section, click **Configure Learning at Work** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc36c-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="cc36c-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="cc36c-171">tooconfigure inicio de sesión único en **en el trabajo de aprendizaje** lado, necesita hello toosend descargado **Metadata XML**, **Id. de entidad SAML**, **SAML Single Sign-On Dirección URL del servicio**, y **dirección URL de cierre de sesión** demasiado[de aprendizaje en el soporte técnico de trabajo](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="cc36c-171">tooconfigure single sign-on on **Learning at Work** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** too[Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="cc36c-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="cc36c-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc36c-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="cc36c-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc36c-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc36c-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc36c-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36c-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc36c-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cc36c-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="cc36c-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc36c-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc36c-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cc36c-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc36c-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc36c-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc36c-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc36c-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cc36c-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc36c-187">a.</span><span class="sxs-lookup"><span data-stu-id="cc36c-187">a.</span></span> <span data-ttu-id="cc36c-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc36c-189">b.</span><span class="sxs-lookup"><span data-stu-id="cc36c-189">b.</span></span> <span data-ttu-id="cc36c-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc36c-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc36c-191">c.</span><span class="sxs-lookup"><span data-stu-id="cc36c-191">c.</span></span> <span data-ttu-id="cc36c-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cc36c-193">d.</span><span class="sxs-lookup"><span data-stu-id="cc36c-193">d.</span></span> <span data-ttu-id="cc36c-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="cc36c-195">Creación de un usuario de prueba de Learning at Work</span><span class="sxs-lookup"><span data-stu-id="cc36c-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="cc36c-196">En esta sección, creará un usuario llamado Britta Simon en Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="cc36c-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="cc36c-197">Trabajar con [en el soporte técnico de trabajo de aprendizaje](https://www.learninga-z.com/site/contact/support) a los usuarios de tooadd hello en Hola aprendizaje en la plataforma de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cc36c-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) tooadd hello users in hello Learning at Work platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc36c-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36c-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc36c-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLearning en el trabajo.</span><span class="sxs-lookup"><span data-stu-id="cc36c-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning at Work.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cc36c-201">**tooassign Britta Simon tooLearning en el trabajo, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc36c-201">**tooassign Britta Simon tooLearning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc36c-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cc36c-204">En la lista de aplicaciones de hello, seleccione **en el trabajo de aprendizaje**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-204">In hello applications list, select **Learning at Work**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="cc36c-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="cc36c-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-208">Click **Add** button.</span></span> <span data-ttu-id="cc36c-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="cc36c-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc36c-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc36c-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc36c-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cc36c-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc36c-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cc36c-214">Testing single sign-on</span></span>

<span data-ttu-id="cc36c-215">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cc36c-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc36c-216">Al hacer clic en Hola de aprendizaje en el icono de trabajo en Hola Panel de acceso, deberá obtener tooyour automáticamente ha iniciado sesión en la aplicación de trabajo de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="cc36c-216">When you click hello Learning at Work tile in hello Access Panel, you should get automatically signed-on tooyour Learning at Work application.</span></span>
<span data-ttu-id="cc36c-217">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc36c-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc36c-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cc36c-218">Additional resources</span></span>

* [<span data-ttu-id="cc36c-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc36c-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc36c-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc36c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

