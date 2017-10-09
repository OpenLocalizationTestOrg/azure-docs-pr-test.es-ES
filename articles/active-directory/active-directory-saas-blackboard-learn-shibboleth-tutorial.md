---
title: "Tutorial: Integración de Azure Active Directory con Blackboard Learn - Shibboleth | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y obtener información Pizarra - Shibboleth."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 40aa3ec5f42b93157af3c56daaadfa66203b21d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="9874f-103">Tutorial: Integración de Azure Active Directory con Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="9874f-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="9874f-104">En este tutorial, aprenderá cómo toointegrate Obtenga información acerca de pizarra - Shibboleth con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9874f-104">In this tutorial, you learn how toointegrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9874f-105">Integración de aprendizaje de pizarra - Shibboleth con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9874f-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9874f-106">Puede controlar en Azure AD que tenga acceso tooBlackboard aprendizaje - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="9874f-106">You can control in Azure AD who has access tooBlackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="9874f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBlackboard aprendizaje - Shibboleth (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9874f-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9874f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9874f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9874f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9874f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9874f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9874f-110">Prerequisites</span></span>

<span data-ttu-id="9874f-111">integración de Azure AD con pizarra aprendizaje: Shibboleth, tooconfigure necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9874f-111">tooconfigure Azure AD integration with Blackboard Learn - Shibboleth, you need hello following items:</span></span>

- <span data-ttu-id="9874f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9874f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9874f-113">Una suscripción habilitada para el inicio de sesión único de Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="9874f-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9874f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9874f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9874f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9874f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9874f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9874f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9874f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9874f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9874f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9874f-118">Scenario description</span></span>
<span data-ttu-id="9874f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9874f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9874f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9874f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9874f-121">Agregar más información de pizarra - Shibboleth de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9874f-121">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
2. <span data-ttu-id="9874f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9874f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-hello-gallery"></a><span data-ttu-id="9874f-123">Agregar más información de pizarra - Shibboleth de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9874f-123">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
<span data-ttu-id="9874f-124">integración de hello tooconfigure de aprendizaje de Pizarra: Shibboleth en Azure AD, deberá tooadd Pizarra aprendizaje: Shibboleth de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9874f-124">tooconfigure hello integration of Blackboard Learn - Shibboleth into Azure AD, you need tooadd Blackboard Learn - Shibboleth from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9874f-125">**tooadd Obtenga información acerca de pizarra - Shibboleth de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9874f-125">**tooadd Blackboard Learn - Shibboleth from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9874f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9874f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9874f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9874f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9874f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9874f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9874f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9874f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9874f-133">En el cuadro de búsqueda de hello, escriba **Pizarra aprendizaje: Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="9874f-133">In hello search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="9874f-135">En el panel de resultados de hello, seleccione **Pizarra aprendizaje: Shibboleth**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9874f-135">In hello results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9874f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9874f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9874f-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Blackboard Learn - Shibboleth con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9874f-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9874f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en aprender Pizarra - Shibboleth es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9874f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn - Shibboleth is tooa user in Azure AD.</span></span> <span data-ttu-id="9874f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en aprender Pizarra - Shibboleth necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9874f-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn - Shibboleth needs toobe established.</span></span>

<span data-ttu-id="9874f-141">En aprendizaje Pizarra - Shibboleth, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9874f-141">In Blackboard Learn - Shibboleth, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9874f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con pizarra aprendizaje: Shibboleth, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9874f-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9874f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9874f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9874f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9874f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9874f-145">**[Crear un aprendizaje Pizarra: usuario de prueba de Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)**  - toohave un equivalente de Britta Simon en aprender Pizarra - Shibboleth que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9874f-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9874f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9874f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9874f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9874f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9874f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9874f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9874f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el aprendizaje de Pizarra: aplicación de Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="9874f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="9874f-150">**inicio de sesión único en tooconfigure Azure AD con pizarra aprendizaje: Shibboleth, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9874f-150">**tooconfigure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="9874f-151">En el portal de Azure, en Hola Hola **Pizarra aprendizaje: Shibboleth** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9874f-151">In hello Azure portal, on hello **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9874f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9874f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="9874f-155">En hello **Pizarra aprendizaje: dominio Shibboleth y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9874f-155">On hello **Blackboard Learn - Shibboleth Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="9874f-157">a.</span><span class="sxs-lookup"><span data-stu-id="9874f-157">a.</span></span> <span data-ttu-id="9874f-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="9874f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="9874f-159">b.</span><span class="sxs-lookup"><span data-stu-id="9874f-159">b.</span></span> <span data-ttu-id="9874f-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="9874f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="9874f-161">c.</span><span class="sxs-lookup"><span data-stu-id="9874f-161">c.</span></span> <span data-ttu-id="9874f-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="9874f-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="9874f-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9874f-163">These values are not real.</span></span> <span data-ttu-id="9874f-164">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9874f-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9874f-165">Póngase en contacto con [Pizarra aprendizaje: el equipo de soporte técnico de cliente de Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="9874f-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="9874f-166">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9874f-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="9874f-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9874f-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="9874f-170">En hello **Pizarra aprendizaje: configuración de Shibboleth** sección, haga clic en **configurar Pizarra aprendizaje: Shibboleth** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9874f-170">On hello **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9874f-171">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9874f-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="9874f-173">tooconfigure inicio de sesión único en **Pizarra aprendizaje: Shibboleth** lado, necesita hello toosend descargado **Metadata XML** y **dirección URL de cierre de sesión, Id. de entidad de SAML y servicio de inicio de sesión único de SAML Dirección URL** demasiado[Pizarra aprendizaje: el equipo de soporte técnico de Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="9874f-173">tooconfigure single sign-on on **Blackboard Learn - Shibboleth** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="9874f-174">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9874f-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9874f-175">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9874f-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9874f-176">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9874f-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9874f-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9874f-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="9874f-178">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9874f-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9874f-180">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9874f-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9874f-181">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9874f-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9874f-183">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9874f-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9874f-185">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9874f-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9874f-187">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9874f-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9874f-189">a.</span><span class="sxs-lookup"><span data-stu-id="9874f-189">a.</span></span> <span data-ttu-id="9874f-190">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9874f-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9874f-191">b.</span><span class="sxs-lookup"><span data-stu-id="9874f-191">b.</span></span> <span data-ttu-id="9874f-192">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9874f-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9874f-193">c.</span><span class="sxs-lookup"><span data-stu-id="9874f-193">c.</span></span> <span data-ttu-id="9874f-194">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9874f-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9874f-195">d.</span><span class="sxs-lookup"><span data-stu-id="9874f-195">d.</span></span> <span data-ttu-id="9874f-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9874f-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="9874f-197">Creación de un usuario de prueba de Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="9874f-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="9874f-198">En esta sección, creará un usuario llamado Britta Simon en Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="9874f-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="9874f-199">Trabajar con su [Pizarra aprendizaje: el equipo de soporte técnico de Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) a los usuarios de tooadd Hola Hola Pizarra aprendizaje: plataforma de Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="9874f-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd hello users in hello Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9874f-200">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9874f-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9874f-201">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBlackboard aprendizaje - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="9874f-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn - Shibboleth.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9874f-203">**tooassign Britta Simon tooBlackboard aprendizaje - Shibboleth, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9874f-203">**tooassign Britta Simon tooBlackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="9874f-204">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9874f-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9874f-206">En la lista de aplicaciones de hello, seleccione **Pizarra aprendizaje: Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="9874f-206">In hello applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="9874f-208">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9874f-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9874f-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9874f-210">Click **Add** button.</span></span> <span data-ttu-id="9874f-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9874f-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9874f-213">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9874f-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9874f-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9874f-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9874f-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9874f-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9874f-216">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9874f-216">Testing single sign-on</span></span>

<span data-ttu-id="9874f-217">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9874f-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9874f-218">Al hacer clic en hello Pizarra aprendizaje: icono de Shibboleth Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Pizarra aprendizaje: aplicación de Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="9874f-218">When you click hello Blackboard Learn - Shibboleth tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9874f-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9874f-219">Additional resources</span></span>

* [<span data-ttu-id="9874f-220">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9874f-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9874f-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9874f-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

