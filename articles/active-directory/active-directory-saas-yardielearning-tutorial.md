---
title: "Tutorial: Integración de Azure Active Directory con Yardi eLearning | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y eLearning Yardi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7ea58b54-ec5b-4576-8586-814b11d0f4fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 47c95fe024e76a67aa5c5b3ee6f81cbafc50ff07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yardi-elearning"></a><span data-ttu-id="5fff0-103">Tutorial: Integración de Azure Active Directory con Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="5fff0-103">Tutorial: Azure Active Directory integration with Yardi eLearning</span></span>

<span data-ttu-id="5fff0-104">En este tutorial, aprenderá cómo toointegrate Yardi eLearning con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fff0-104">In this tutorial, you learn how toointegrate Yardi eLearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fff0-105">Integrar Yardi eLearning con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5fff0-105">Integrating Yardi eLearning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5fff0-106">Puede controlar en Azure AD que tenga acceso tooYardi eLearning</span><span class="sxs-lookup"><span data-stu-id="5fff0-106">You can control in Azure AD who has access tooYardi eLearning</span></span>
- <span data-ttu-id="5fff0-107">Puede habilitar los usuarios tooautomatically get tooYardi ha iniciado sesión eLearning (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fff0-107">You can enable your users tooautomatically get signed-on tooYardi eLearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5fff0-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5fff0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5fff0-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fff0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fff0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5fff0-110">Prerequisites</span></span>

<span data-ttu-id="5fff0-111">integración de Azure AD con Yardi eLearning tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5fff0-111">tooconfigure Azure AD integration with Yardi eLearning, you need hello following items:</span></span>

- <span data-ttu-id="5fff0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fff0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fff0-113">Una suscripción habilitada para el inicio de sesión único en Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="5fff0-113">A Yardi eLearning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fff0-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5fff0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fff0-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5fff0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fff0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5fff0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fff0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fff0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fff0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5fff0-118">Scenario description</span></span>
<span data-ttu-id="5fff0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5fff0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fff0-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="5fff0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fff0-121">Agregar Yardi eLearning desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5fff0-121">Adding Yardi eLearning from hello gallery</span></span>
2. <span data-ttu-id="5fff0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fff0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yardi-elearning-from-hello-gallery"></a><span data-ttu-id="5fff0-123">Agregar Yardi eLearning desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5fff0-123">Adding Yardi eLearning from hello gallery</span></span>
<span data-ttu-id="5fff0-124">integración de hello tooconfigure de eLearning Yardi en Azure AD, deberá tooadd Yardi eLearning de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="5fff0-124">tooconfigure hello integration of Yardi eLearning into Azure AD, you need tooadd Yardi eLearning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5fff0-125">**tooadd Yardi eLearning de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5fff0-125">**tooadd Yardi eLearning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fff0-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5fff0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5fff0-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5fff0-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5fff0-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5fff0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5fff0-133">En el cuadro de búsqueda de hello, escriba **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-133">In hello search box, type **Yardi eLearning**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_search.png)

5. <span data-ttu-id="5fff0-135">En el panel de resultados de hello, seleccione **Yardi eLearning**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5fff0-135">In hello results panel, select **Yardi eLearning**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5fff0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fff0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5fff0-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Yardi eLearning utilizando usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fff0-138">In this section, you configure and test Azure AD single sign-on with Yardi eLearning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5fff0-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Yardi eLearning es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fff0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Yardi eLearning is tooa user in Azure AD.</span></span> <span data-ttu-id="5fff0-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Yardi eLearning debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="5fff0-140">In other words, a link relationship between an Azure AD user and hello related user in Yardi eLearning needs toobe established.</span></span>

<span data-ttu-id="5fff0-141">En Yardi eLearning, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5fff0-141">In Yardi eLearning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5fff0-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Yardi eLearning, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5fff0-142">tooconfigure and test Azure AD single sign-on with Yardi eLearning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5fff0-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="5fff0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5fff0-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fff0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fff0-145">**[Crear un usuario de prueba de eLearning Yardi](#creating-a-yardi-elearning-test-user)**  -toohave un equivalente de Britta Simon en eLearning Yardi que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="5fff0-145">**[Creating a Yardi eLearning test user](#creating-a-yardi-elearning-test-user)** - toohave a counterpart of Britta Simon in Yardi eLearning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fff0-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5fff0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fff0-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5fff0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5fff0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fff0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5fff0-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de eLearning Yardi.</span><span class="sxs-lookup"><span data-stu-id="5fff0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Yardi eLearning application.</span></span>

<span data-ttu-id="5fff0-150">**inicio de sesión único en tooconfigure Azure AD con Yardi eLearning, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5fff0-150">**tooconfigure Azure AD single sign-on with Yardi eLearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fff0-151">En el portal de Azure, en Hola Hola **Yardi eLearning** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-151">In hello Azure portal, on hello **Yardi eLearning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5fff0-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5fff0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_samlbase.png)

3. <span data-ttu-id="5fff0-155">En hello **Yardi eLearning dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5fff0-155">On hello **Yardi eLearning Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_url.png)

    <span data-ttu-id="5fff0-157">a.</span><span class="sxs-lookup"><span data-stu-id="5fff0-157">a.</span></span> <span data-ttu-id="5fff0-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.yardielearning.com/login`</span><span class="sxs-lookup"><span data-stu-id="5fff0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.yardielearning.com/login`</span></span>

    <span data-ttu-id="5fff0-159">b.</span><span class="sxs-lookup"><span data-stu-id="5fff0-159">b.</span></span> <span data-ttu-id="5fff0-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.yardielearning.com/trust`</span><span class="sxs-lookup"><span data-stu-id="5fff0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.yardielearning.com/trust`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5fff0-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="5fff0-161">These values are not real.</span></span> <span data-ttu-id="5fff0-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="5fff0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5fff0-163">Póngase en contacto con [equipo de soporte técnico de cliente de eLearning Yardi](mailto:elearning@yardi.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="5fff0-163">Contact [Yardi eLearning Client support team](mailto:elearning@yardi.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="5fff0-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5fff0-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_certificate.png) 

5. <span data-ttu-id="5fff0-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5fff0-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-yardielearning-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5fff0-168">tooconfigure inicio de sesión único en **Yardi eLearning** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de eLearning Yardi](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="5fff0-168">tooconfigure single sign-on on **Yardi eLearning** side, you need toosend hello downloaded **Metadata XML** too[Yardi eLearning support team](mailto:elearning@yardi.com).</span></span> 

> [!TIP]
> <span data-ttu-id="5fff0-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="5fff0-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5fff0-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="5fff0-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5fff0-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fff0-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5fff0-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fff0-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="5fff0-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="5fff0-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5fff0-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5fff0-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fff0-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5fff0-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5fff0-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5fff0-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5fff0-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5fff0-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="5fff0-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5fff0-184">a.</span><span class="sxs-lookup"><span data-stu-id="5fff0-184">a.</span></span> <span data-ttu-id="5fff0-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5fff0-186">b.</span><span class="sxs-lookup"><span data-stu-id="5fff0-186">b.</span></span> <span data-ttu-id="5fff0-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5fff0-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5fff0-188">c.</span><span class="sxs-lookup"><span data-stu-id="5fff0-188">c.</span></span> <span data-ttu-id="5fff0-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5fff0-190">d.</span><span class="sxs-lookup"><span data-stu-id="5fff0-190">d.</span></span> <span data-ttu-id="5fff0-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-191">Click **Create**.</span></span>
 
### <a name="creating-a-yardi-elearning-test-user"></a><span data-ttu-id="5fff0-192">Creación de un usuario de prueba de Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="5fff0-192">Creating a Yardi eLearning test user</span></span>

<span data-ttu-id="5fff0-193">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en eLearning Yardi toocreate.</span><span class="sxs-lookup"><span data-stu-id="5fff0-193">hello objective of this section is toocreate a user called Britta Simon in Yardi eLearning.</span></span> <span data-ttu-id="5fff0-194">Yardi eLearning admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5fff0-194">Yardi eLearning supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5fff0-195">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="5fff0-195">There is no action item for you in this section.</span></span> <span data-ttu-id="5fff0-196">Si no existe todavía, se crea un usuario nuevo durante un tooaccess de intento de eLearning Yardi.</span><span class="sxs-lookup"><span data-stu-id="5fff0-196">A new user is created during an attempt tooaccess Yardi eLearning if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="5fff0-197">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de eLearning Yardi](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="5fff0-197">If you need toocreate a user manually, you need toocontact hello [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5fff0-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fff0-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5fff0-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooYardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="5fff0-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYardi eLearning.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5fff0-201">**tooassign Britta Simon tooYardi eLearning, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5fff0-201">**tooassign Britta Simon tooYardi eLearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fff0-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5fff0-204">En la lista de aplicaciones de hello, seleccione **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-204">In hello applications list, select **Yardi eLearning**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_app.png) 

3. <span data-ttu-id="5fff0-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5fff0-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-208">Click **Add** button.</span></span> <span data-ttu-id="5fff0-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5fff0-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5fff0-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5fff0-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fff0-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5fff0-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5fff0-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="5fff0-214">Testing single sign-on</span></span>

<span data-ttu-id="5fff0-215">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5fff0-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5fff0-216">Al hacer clic en icono de eLearning Yardi de Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Yardi eLearning aplicación.</span><span class="sxs-lookup"><span data-stu-id="5fff0-216">When you click hello Yardi eLearning tile in hello Access Panel, you should get automatically signed-on tooyour Yardi eLearning application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5fff0-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5fff0-217">Additional resources</span></span>

* [<span data-ttu-id="5fff0-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fff0-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fff0-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5fff0-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_203.png

