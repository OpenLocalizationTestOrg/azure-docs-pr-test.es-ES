---
title: "Tutorial: Integración de Azure Active Directory con Learning Seat LMS | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y aprendizaje puestos LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: dc08aa444b85f35a4458768ac560ec663baa1c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="94660-103">Tutorial: Integración de Azure Active Directory con Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="94660-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="94660-104">En este tutorial, aprenderá cómo toointegrate LMS de puestos de aprendizaje con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94660-104">In this tutorial, you learn how toointegrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94660-105">Integración LMS puestos de aprendizaje con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="94660-105">Integrating Learning Seat LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="94660-106">Puede controlar en Azure AD que tenga acceso tooLearning puestos LMS</span><span class="sxs-lookup"><span data-stu-id="94660-106">You can control in Azure AD who has access tooLearning Seat LMS</span></span>
- <span data-ttu-id="94660-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLearning puestos LMS (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94660-107">You can enable your users tooautomatically get signed-on tooLearning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94660-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="94660-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="94660-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte.</span><span class="sxs-lookup"><span data-stu-id="94660-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="94660-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="94660-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94660-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="94660-111">Prerequisites</span></span>

<span data-ttu-id="94660-112">integración de Azure AD con aprendizaje puestos LMS tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="94660-112">tooconfigure Azure AD integration with Learning Seat LMS, you need hello following items:</span></span>

- <span data-ttu-id="94660-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94660-113">An Azure AD subscription</span></span>
- <span data-ttu-id="94660-114">Una suscripción habilitada para el inicio de sesión único en Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="94660-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94660-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="94660-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94660-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="94660-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94660-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="94660-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94660-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94660-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94660-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="94660-119">Scenario description</span></span>
<span data-ttu-id="94660-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="94660-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94660-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="94660-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94660-122">Agregar LMS puestos de aprendizaje de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="94660-122">Adding Learning Seat LMS from hello gallery</span></span>
2. <span data-ttu-id="94660-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94660-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-hello-gallery"></a><span data-ttu-id="94660-124">Agregar LMS puestos de aprendizaje de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="94660-124">Adding Learning Seat LMS from hello gallery</span></span>
<span data-ttu-id="94660-125">integración de hello tooconfigure de aprendizaje puestos LMS en Azure AD, deberá tooadd LMS puestos de aprendizaje de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="94660-125">tooconfigure hello integration of Learning Seat LMS into Azure AD, you need tooadd Learning Seat LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="94660-126">**tooadd LMS de puestos de aprendizaje de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="94660-126">**tooadd Learning Seat LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="94660-127">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="94660-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94660-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="94660-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="94660-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="94660-130">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="94660-132">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="94660-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="94660-134">En el cuadro de búsqueda de hello, escriba **aprendizaje puestos LMS**.</span><span class="sxs-lookup"><span data-stu-id="94660-134">In hello search box, type **Learning Seat LMS**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="94660-136">En el panel de resultados de hello, seleccione **aprendizaje puestos LMS**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="94660-136">In hello results panel, select **Learning Seat LMS**, and then click **Add** button tooadd hello application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94660-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94660-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94660-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Learning Seat LMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="94660-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="94660-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en aprendizaje puestos LMS es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94660-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning Seat LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="94660-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en aprendizaje puestos LMS debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="94660-140">In other words, a link relationship between an Azure AD user and hello related user in Learning Seat LMS needs toobe established.</span></span>

<span data-ttu-id="94660-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en aprendizaje puestos LMS.</span><span class="sxs-lookup"><span data-stu-id="94660-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="94660-142">tooconfigure y prueba de inicio de sesión único en Azure AD con aprendizaje puestos LMS, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="94660-142">tooconfigure and test Azure AD single sign-on with Learning Seat LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="94660-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="94660-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="94660-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94660-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94660-145">**[Crear un usuario de prueba de aprendizaje puestos LMS](#creating-a-learnconnect-test-user)**  -toohave un equivalente de Britta Simon en aprendizaje puestos LMS que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="94660-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - toohave a counterpart of Britta Simon in Learning Seat LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="94660-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="94660-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94660-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="94660-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94660-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94660-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94660-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de aprendizaje puestos LMS.</span><span class="sxs-lookup"><span data-stu-id="94660-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="94660-150">**tooconfigure inicio de sesión único en Azure AD con LMS puestos de aprendizaje, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="94660-150">**tooconfigure Azure AD single sign-on with Learning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="94660-151">En el portal de Azure, en Hola Hola **aprendizaje puestos LMS** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="94660-151">In hello Azure portal, on hello **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="94660-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="94660-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="94660-155">En hello **aprendizaje puestos LMS dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="94660-155">On hello **Learning Seat LMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="94660-157">a.</span><span class="sxs-lookup"><span data-stu-id="94660-157">a.</span></span> <span data-ttu-id="94660-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="94660-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="94660-159">b.</span><span class="sxs-lookup"><span data-stu-id="94660-159">b.</span></span> <span data-ttu-id="94660-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="94660-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="94660-161">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="94660-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="94660-163">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="94660-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="94660-164">Estos valores no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="94660-164">These values are not hello real values.</span></span> <span data-ttu-id="94660-165">Actualizar estos valores con hello real identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="94660-165">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="94660-166">Póngase en contacto con [equipo de soporte técnico de aprendizaje puestos](http://help.learningseatlms.com/help) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="94660-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) tooget these values.</span></span> 

5. <span data-ttu-id="94660-167">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="94660-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="94660-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="94660-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="94660-171">tooconfigure inicio de sesión único en **aprendizaje puestos LMS** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de aprendizaje puesto](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="94660-171">tooconfigure single sign-on on **Learning Seat LMS** side, you need toosend hello downloaded **Metadata XML** too[Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="94660-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="94660-172">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="94660-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="94660-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="94660-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="94660-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94660-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94660-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="94660-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="94660-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="94660-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="94660-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="94660-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="94660-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94660-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="94660-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94660-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="94660-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94660-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="94660-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94660-187">a.</span><span class="sxs-lookup"><span data-stu-id="94660-187">a.</span></span> <span data-ttu-id="94660-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94660-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94660-189">b.</span><span class="sxs-lookup"><span data-stu-id="94660-189">b.</span></span> <span data-ttu-id="94660-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="94660-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94660-191">c.</span><span class="sxs-lookup"><span data-stu-id="94660-191">c.</span></span> <span data-ttu-id="94660-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="94660-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="94660-193">d.</span><span class="sxs-lookup"><span data-stu-id="94660-193">d.</span></span> <span data-ttu-id="94660-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="94660-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="94660-195">Creación de un usuario de prueba de Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="94660-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="94660-196">En esta sección, creará un usuario llamado Britta Simon en Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="94660-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="94660-197">Póngase en contacto con [equipo de soporte técnico de aprendizaje puestos](http://help.learningseatlms.com/help) con todos los Hola usuario información tooadd Hola usuarios Hola aplicación LMS puestos de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="94660-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all hello user information tooadd hello users in hello Learning Seat LMS application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="94660-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="94660-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="94660-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLearning LMS puestos.</span><span class="sxs-lookup"><span data-stu-id="94660-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning Seat LMS.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="94660-201">**tooassign Britta Simon tooLearning LMS de puestos, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="94660-201">**tooassign Britta Simon tooLearning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="94660-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="94660-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="94660-204">En la lista de aplicaciones de hello, seleccione **aprendizaje puestos LMS**.</span><span class="sxs-lookup"><span data-stu-id="94660-204">In hello applications list, select **Learning Seat LMS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="94660-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="94660-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="94660-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="94660-208">Click **Add** button.</span></span> <span data-ttu-id="94660-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="94660-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="94660-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="94660-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="94660-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="94660-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94660-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="94660-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94660-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="94660-214">Testing single sign-on</span></span>

<span data-ttu-id="94660-215">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="94660-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="94660-216">Haga clic en hello aprendizaje puestos LMS disponer en mosaico en hello Panel de acceso, podrá aplicación de aprendizaje puestos LMS tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="94660-216">Click hello Learning Seat LMS tile in hello Access Panel, you will be automatically signed-on tooyour Learning Seat LMS application.</span></span> <span data-ttu-id="94660-217">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="94660-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94660-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="94660-218">Additional resources</span></span>

* [<span data-ttu-id="94660-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94660-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94660-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94660-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

