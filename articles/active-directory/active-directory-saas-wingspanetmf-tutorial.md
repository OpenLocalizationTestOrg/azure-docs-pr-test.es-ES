---
title: "Tutorial: Integración de Azure Active Directory con Wingspan eTMF | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Wingspan eTMF."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: ed5fda5318a0d3841af8b2db4fb74db550befaea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="7405f-103">Tutorial: Integración de Azure Active Directory con Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="7405f-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="7405f-104">En este tutorial, aprenderá cómo toointegrate Wingspan eTMF con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7405f-104">In this tutorial, you learn how toointegrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7405f-105">Integración Wingspan eTMF con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7405f-105">Integrating Wingspan eTMF with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7405f-106">Puede controlar en Azure AD que tenga acceso tooWingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="7405f-106">You can control in Azure AD who has access tooWingspan eTMF</span></span>
- <span data-ttu-id="7405f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWingspan eTMF (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7405f-107">You can enable your users tooautomatically get signed-on tooWingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7405f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7405f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7405f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7405f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7405f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7405f-110">Prerequisites</span></span>

<span data-ttu-id="7405f-111">integración de Azure AD con Wingspan eTMF tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7405f-111">tooconfigure Azure AD integration with Wingspan eTMF, you need hello following items:</span></span>

- <span data-ttu-id="7405f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7405f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7405f-113">Una suscripción habilitada para inicio de sesión único en Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="7405f-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7405f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7405f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7405f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7405f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7405f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7405f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7405f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7405f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7405f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7405f-118">Scenario description</span></span>
<span data-ttu-id="7405f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7405f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7405f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="7405f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7405f-121">Agregar Wingspan eTMF desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7405f-121">Adding Wingspan eTMF from hello gallery</span></span>
2. <span data-ttu-id="7405f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7405f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-hello-gallery"></a><span data-ttu-id="7405f-123">Agregar Wingspan eTMF desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7405f-123">Adding Wingspan eTMF from hello gallery</span></span>
<span data-ttu-id="7405f-124">integración de hello tooconfigure de Wingspan eTMF en Azure AD, deberá tooadd Wingspan eTMF de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="7405f-124">tooconfigure hello integration of Wingspan eTMF into Azure AD, you need tooadd Wingspan eTMF from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7405f-125">**tooadd Wingspan eTMF de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7405f-125">**tooadd Wingspan eTMF from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7405f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7405f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7405f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7405f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7405f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7405f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7405f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7405f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7405f-133">En el cuadro de búsqueda de hello, escriba **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="7405f-133">In hello search box, type **Wingspan eTMF**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

5. <span data-ttu-id="7405f-135">En el panel de resultados de hello, seleccione **Wingspan eTMF**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7405f-135">In hello results panel, select **Wingspan eTMF**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7405f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7405f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7405f-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Wingspan eTMF con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7405f-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7405f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Wingspan eTMF es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7405f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wingspan eTMF is tooa user in Azure AD.</span></span> <span data-ttu-id="7405f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Wingspan eTMF debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="7405f-140">In other words, a link relationship between an Azure AD user and hello related user in Wingspan eTMF needs toobe established.</span></span>

<span data-ttu-id="7405f-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="7405f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="7405f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Wingspan eTMF, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7405f-142">tooconfigure and test Azure AD single sign-on with Wingspan eTMF, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7405f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="7405f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7405f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7405f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7405f-145">**[Crear un usuario de prueba de eTMF Wingspan](#creating-a-wingspan-etmf-test-user)**  -toohave un equivalente de Britta Simon en eTMF Wingspan que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="7405f-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - toohave a counterpart of Britta Simon in Wingspan eTMF that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7405f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7405f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7405f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7405f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7405f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7405f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7405f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de eTMF Wingspan.</span><span class="sxs-lookup"><span data-stu-id="7405f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="7405f-150">**inicio de sesión único en tooconfigure Azure AD con Wingspan eTMF, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7405f-150">**tooconfigure Azure AD single sign-on with Wingspan eTMF, perform hello following steps:**</span></span>

1. <span data-ttu-id="7405f-151">En el portal de Azure, en Hola Hola **Wingspan eTMF** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7405f-151">In hello Azure portal, on hello **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7405f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7405f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

3. <span data-ttu-id="7405f-155">En hello **Wingspan eTMF dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7405f-155">On hello **Wingspan eTMF Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="7405f-157">a.</span><span class="sxs-lookup"><span data-stu-id="7405f-157">a.</span></span> <span data-ttu-id="7405f-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<customer name>.<instance name>.mywingspan.com/saml`</span><span class="sxs-lookup"><span data-stu-id="7405f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="7405f-159">b.</span><span class="sxs-lookup"><span data-stu-id="7405f-159">b.</span></span> <span data-ttu-id="7405f-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="7405f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="7405f-161">c.</span><span class="sxs-lookup"><span data-stu-id="7405f-161">c.</span></span> <span data-ttu-id="7405f-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<customer name>.<instance name>.mywingspan.com/`</span><span class="sxs-lookup"><span data-stu-id="7405f-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7405f-163">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="7405f-163">These values are not hello real.</span></span> <span data-ttu-id="7405f-164">Actualizar estos valores con hello dirección URL de inicio de sesión, el identificador y la respuesta URL real incluidos nombre real del cliente de Hola y el nombre de instancia.</span><span class="sxs-lookup"><span data-stu-id="7405f-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL including hello actual customer name and instance name.</span></span> <span data-ttu-id="7405f-165">Póngase en contacto con [equipo de soporte técnico de cliente de Wingspan eTMF](http://www.wingspan.com/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="7405f-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="7405f-166">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7405f-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

5. <span data-ttu-id="7405f-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7405f-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7405f-170">tooconfigure inicio de sesión único en **Wingspan eTMF** lado, necesita hello toosend descargado **Metadata XML** demasiado[soporte técnico de eTMF Wingspan](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="7405f-170">tooconfigure single sign-on on **Wingspan eTMF** side, you need toosend hello downloaded **Metadata XML** too[Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="7405f-171">Configure toohave Hola configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="7405f-171">They set this up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7405f-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="7405f-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7405f-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="7405f-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7405f-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7405f-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7405f-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7405f-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="7405f-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="7405f-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7405f-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7405f-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7405f-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7405f-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7405f-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7405f-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7405f-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7405f-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7405f-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="7405f-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7405f-187">a.</span><span class="sxs-lookup"><span data-stu-id="7405f-187">a.</span></span> <span data-ttu-id="7405f-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7405f-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7405f-189">b.</span><span class="sxs-lookup"><span data-stu-id="7405f-189">b.</span></span> <span data-ttu-id="7405f-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7405f-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7405f-191">c.</span><span class="sxs-lookup"><span data-stu-id="7405f-191">c.</span></span> <span data-ttu-id="7405f-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7405f-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7405f-193">d.</span><span class="sxs-lookup"><span data-stu-id="7405f-193">d.</span></span> <span data-ttu-id="7405f-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7405f-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="7405f-195">Crear un usuario de prueba de Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="7405f-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="7405f-196">En esta sección, creará un usuario llamado Britta Simon en Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="7405f-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="7405f-197">Trabajar con [soporte técnico de eTMF Wingspan](http://www.wingspan.com/contact-us/) a los usuarios de tooadd Hola Hola aplicación eTMF de Wingspan.</span><span class="sxs-lookup"><span data-stu-id="7405f-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) tooadd hello users in hello Wingspan eTMF application.</span></span> <span data-ttu-id="7405f-198">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7405f-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7405f-199">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7405f-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7405f-200">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="7405f-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWingspan eTMF.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7405f-202">**tooassign Britta Simon tooWingspan eTMF, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7405f-202">**tooassign Britta Simon tooWingspan eTMF, perform hello following steps:**</span></span>

1. <span data-ttu-id="7405f-203">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7405f-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7405f-205">En la lista de aplicaciones de hello, seleccione **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="7405f-205">In hello applications list, select **Wingspan eTMF**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

3. <span data-ttu-id="7405f-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7405f-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7405f-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7405f-209">Click **Add** button.</span></span> <span data-ttu-id="7405f-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7405f-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7405f-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7405f-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7405f-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7405f-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7405f-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7405f-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7405f-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7405f-215">Testing single sign-on</span></span>

<span data-ttu-id="7405f-216">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7405f-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="7405f-217">Haga clic en el icono de hello Wingspan eTMF Hola Panel de acceso, será redirigido tooOrganization inicio de sesión en la página.</span><span class="sxs-lookup"><span data-stu-id="7405f-217">Click hello Wingspan eTMF tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="7405f-218">Después de iniciar sesión correctamente, será tooyour iniciado sesión en aplicaciones de eTMF Wingspan.</span><span class="sxs-lookup"><span data-stu-id="7405f-218">After successful login, you will be signed-on tooyour Wingspan eTMF application.</span></span> <span data-ttu-id="7405f-219">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="7405f-219">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7405f-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7405f-220">Additional resources</span></span>

* [<span data-ttu-id="7405f-221">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7405f-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7405f-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7405f-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_203.png

