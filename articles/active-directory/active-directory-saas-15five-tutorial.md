---
title: "Tutorial: integración de Azure Active Directory con 15Five | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y 15Five."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 9e531615c16331ce000e285d13d9adce13735a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="8395a-103">Tutorial: integración de Azure Active Directory con 15Five</span><span class="sxs-lookup"><span data-stu-id="8395a-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="8395a-104">En este tutorial, aprenderá cómo toointegrate 15Five con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8395a-104">In this tutorial, you learn how toointegrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8395a-105">Integración de 15Five con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8395a-105">Integrating 15Five with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8395a-106">Puede controlar en Azure AD que tenga acceso too15Five</span><span class="sxs-lookup"><span data-stu-id="8395a-106">You can control in Azure AD who has access too15Five</span></span>
- <span data-ttu-id="8395a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión too15Five (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8395a-107">You can enable your users tooautomatically get signed-on too15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8395a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8395a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8395a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8395a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8395a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8395a-110">Prerequisites</span></span>

<span data-ttu-id="8395a-111">integración de Azure AD con 15Five tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8395a-111">tooconfigure Azure AD integration with 15Five, you need hello following items:</span></span>

- <span data-ttu-id="8395a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8395a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8395a-113">Una suscripción habilitada para el inicio de sesión único en 15Five</span><span class="sxs-lookup"><span data-stu-id="8395a-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8395a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8395a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8395a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8395a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8395a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8395a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8395a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8395a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8395a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8395a-118">Scenario description</span></span>
<span data-ttu-id="8395a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8395a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8395a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8395a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8395a-121">Agregar 15Five desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8395a-121">Adding 15Five from hello gallery</span></span>
2. <span data-ttu-id="8395a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8395a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-hello-gallery"></a><span data-ttu-id="8395a-123">Agregar 15Five desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8395a-123">Adding 15Five from hello gallery</span></span>
<span data-ttu-id="8395a-124">integración de hello tooconfigure de 15Five en Azure AD, deberá tooadd 15Five de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8395a-124">tooconfigure hello integration of 15Five into Azure AD, you need tooadd 15Five from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8395a-125">**tooadd 15Five de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8395a-125">**tooadd 15Five from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8395a-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8395a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8395a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8395a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8395a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8395a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8395a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8395a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8395a-133">En el cuadro de búsqueda de hello, escriba **15Five**.</span><span class="sxs-lookup"><span data-stu-id="8395a-133">In hello search box, type **15Five**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="8395a-135">En el panel de resultados de hello, seleccione **15Five**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8395a-135">In hello results panel, select **15Five**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8395a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8395a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8395a-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con 15Five con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8395a-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8395a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en 15Five es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8395a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 15Five is tooa user in Azure AD.</span></span> <span data-ttu-id="8395a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en 15Five debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8395a-140">In other words, a link relationship between an Azure AD user and hello related user in 15Five needs toobe established.</span></span>

<span data-ttu-id="8395a-141">En 15Five, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8395a-141">In 15Five, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8395a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con 15Five, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8395a-142">tooconfigure and test Azure AD single sign-on with 15Five, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8395a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8395a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8395a-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8395a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8395a-145">**[Crear un usuario de prueba de 15Five](#creating-a-15five-test-user)**  -toohave un equivalente de Britta Simon en 15Five que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8395a-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - toohave a counterpart of Britta Simon in 15Five that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8395a-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8395a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8395a-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8395a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8395a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8395a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8395a-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de 15Five.</span><span class="sxs-lookup"><span data-stu-id="8395a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="8395a-150">**inicio de sesión único en Azure AD tooconfigure con 15Five, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8395a-150">**tooconfigure Azure AD single sign-on with 15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="8395a-151">En el portal de Azure, en Hola Hola **15Five** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8395a-151">In hello Azure portal, on hello **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8395a-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8395a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="8395a-155">En hello **15Five dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8395a-155">On hello **15Five Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="8395a-157">a.</span><span class="sxs-lookup"><span data-stu-id="8395a-157">a.</span></span> <span data-ttu-id="8395a-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="8395a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="8395a-159">b.</span><span class="sxs-lookup"><span data-stu-id="8395a-159">b.</span></span> <span data-ttu-id="8395a-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="8395a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8395a-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="8395a-161">These values are not real.</span></span> <span data-ttu-id="8395a-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="8395a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8395a-163">Póngase en contacto con [equipo de soporte técnico de 15Five cliente](https://www.15five.com/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="8395a-163">Contact [15Five Client support team](https://www.15five.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="8395a-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8395a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="8395a-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8395a-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8395a-168">inicio de sesión único en tooconfigure en **15Five** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="8395a-168">tooconfigure single sign-on on **15Five** side, you need toosend hello downloaded **Metadata XML** too[15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="8395a-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8395a-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8395a-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8395a-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8395a-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8395a-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8395a-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8395a-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="8395a-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8395a-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8395a-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8395a-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8395a-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8395a-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8395a-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8395a-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8395a-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8395a-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8395a-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8395a-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8395a-184">a.</span><span class="sxs-lookup"><span data-stu-id="8395a-184">a.</span></span> <span data-ttu-id="8395a-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8395a-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8395a-186">b.</span><span class="sxs-lookup"><span data-stu-id="8395a-186">b.</span></span> <span data-ttu-id="8395a-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8395a-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8395a-188">c.</span><span class="sxs-lookup"><span data-stu-id="8395a-188">c.</span></span> <span data-ttu-id="8395a-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8395a-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8395a-190">d.</span><span class="sxs-lookup"><span data-stu-id="8395a-190">d.</span></span> <span data-ttu-id="8395a-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8395a-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="8395a-192">Creación de un usuario de prueba de 15Five</span><span class="sxs-lookup"><span data-stu-id="8395a-192">Creating a 15Five test user</span></span>

<span data-ttu-id="8395a-193">toolog de los usuarios de Azure AD tooenable en too15Five, se les deben aprovisionar en 15Five.</span><span class="sxs-lookup"><span data-stu-id="8395a-193">tooenable Azure AD users toolog in too15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="8395a-194">En el caso de 15Five, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="8395a-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="8395a-195">tooconfigure aprovisionamiento de usuario, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8395a-195">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="8395a-196">Inicie sesión en tooyour **15Five** como administrador.</span><span class="sxs-lookup"><span data-stu-id="8395a-196">Log in tooyour **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="8395a-197">Vaya demasiado**administrar compañía**.</span><span class="sxs-lookup"><span data-stu-id="8395a-197">Go too**Manage Company**.</span></span>
   
    <span data-ttu-id="8395a-198">![Administrar compañía](./media/active-directory-saas-15five-tutorial/IC784675.png "Administrar compañía")</span><span class="sxs-lookup"><span data-stu-id="8395a-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="8395a-199">Vaya demasiado**personas \> agregar personas**.</span><span class="sxs-lookup"><span data-stu-id="8395a-199">Go too**People \> Add People**.</span></span>
   
    <span data-ttu-id="8395a-200">![Personas](./media/active-directory-saas-15five-tutorial/IC784676.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="8395a-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="8395a-201">En la sección Agregar nueva persona hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8395a-201">In hello Add New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8395a-202">![Agregar nueva persona](./media/active-directory-saas-15five-tutorial/IC784677.png "Agregar nueva persona")</span><span class="sxs-lookup"><span data-stu-id="8395a-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="8395a-203">a.</span><span class="sxs-lookup"><span data-stu-id="8395a-203">a.</span></span> <span data-ttu-id="8395a-204">Hola de tipo **nombre**, **Last Name**, **título**, **dirección de correo electrónico** de una cuenta válida de Azure Active Directory que desee tooprovision en Hola relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="8395a-204">Type hello **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="8395a-205">b.</span><span class="sxs-lookup"><span data-stu-id="8395a-205">b.</span></span> <span data-ttu-id="8395a-206">Haga clic en **Done**(Listo).</span><span class="sxs-lookup"><span data-stu-id="8395a-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="8395a-207">Hola cuenta de Azure AD titular recibe un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="8395a-207">hello Azure AD account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8395a-208">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8395a-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8395a-209">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso too15Five.</span><span class="sxs-lookup"><span data-stu-id="8395a-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too15Five.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8395a-211">**tooassign Britta Simon too15Five, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8395a-211">**tooassign Britta Simon too15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="8395a-212">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8395a-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8395a-214">En la lista de aplicaciones de hello, seleccione **15Five**.</span><span class="sxs-lookup"><span data-stu-id="8395a-214">In hello applications list, select **15Five**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="8395a-216">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8395a-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8395a-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8395a-218">Click **Add** button.</span></span> <span data-ttu-id="8395a-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8395a-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8395a-221">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8395a-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8395a-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8395a-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8395a-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8395a-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8395a-224">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8395a-224">Testing single sign-on</span></span>

<span data-ttu-id="8395a-225">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8395a-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8395a-226">Al hacer clic en icono de 15Five Hola Hola Panel de acceso, deberá obtener la página de inicio de sesión de aplicación de 15Five.</span><span class="sxs-lookup"><span data-stu-id="8395a-226">When you click hello 15Five tile in hello Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="8395a-227">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8395a-227">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8395a-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8395a-228">Additional resources</span></span>

* [<span data-ttu-id="8395a-229">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8395a-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8395a-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8395a-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

