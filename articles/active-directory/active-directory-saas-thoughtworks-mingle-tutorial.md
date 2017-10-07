---
title: "Tutorial: integración de Azure Active Directory con Thoughtworks Mingle | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="baa67-103">Tutorial: Integración de Azure Active Directory con Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="baa67-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="baa67-104">En este tutorial, aprenderá cómo toointegrate Thoughtworks Mingle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="baa67-104">In this tutorial, you learn how toointegrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="baa67-105">Integración de Thoughtworks Mingle con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="baa67-105">Integrating Thoughtworks Mingle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="baa67-106">Puede controlar en Azure AD que tenga acceso tooThoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="baa67-106">You can control in Azure AD who has access tooThoughtworks Mingle</span></span>
- <span data-ttu-id="baa67-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooThoughtworks Mingle (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="baa67-107">You can enable your users tooautomatically get signed-on tooThoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="baa67-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="baa67-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="baa67-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="baa67-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baa67-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="baa67-110">Prerequisites</span></span>

<span data-ttu-id="baa67-111">integración de Azure AD con Thoughtworks Mingle tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="baa67-111">tooconfigure Azure AD integration with Thoughtworks Mingle, you need hello following items:</span></span>

- <span data-ttu-id="baa67-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="baa67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="baa67-113">Una suscripción habilitada para el inicio de sesión único en Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="baa67-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="baa67-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="baa67-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="baa67-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="baa67-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="baa67-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="baa67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="baa67-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="baa67-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="baa67-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="baa67-118">Scenario description</span></span>
<span data-ttu-id="baa67-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="baa67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="baa67-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="baa67-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="baa67-121">Agregar Thoughtworks Mingle desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="baa67-121">Adding Thoughtworks Mingle from hello gallery</span></span>
2. <span data-ttu-id="baa67-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="baa67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a><span data-ttu-id="baa67-123">Agregar Thoughtworks Mingle desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="baa67-123">Adding Thoughtworks Mingle from hello gallery</span></span>
<span data-ttu-id="baa67-124">integración de hello tooconfigure de Thoughtworks Mingle en Azure AD, deberá tooadd Thoughtworks Mingle de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="baa67-124">tooconfigure hello integration of Thoughtworks Mingle into Azure AD, you need tooadd Thoughtworks Mingle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="baa67-125">**tooadd Thoughtworks Mingle de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="baa67-125">**tooadd Thoughtworks Mingle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="baa67-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="baa67-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="baa67-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="baa67-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="baa67-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="baa67-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="baa67-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="baa67-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="baa67-133">En el cuadro de búsqueda de hello, escriba **Thoughtworks Mingle**, seleccione **Thoughtworks Mingle** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="baa67-133">In hello search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de Thoughtworks Mingle Hola](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="baa67-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="baa67-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="baa67-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Thoughtworks Mingle con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="baa67-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="baa67-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Thoughtworks Mingle es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="baa67-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Thoughtworks Mingle is tooa user in Azure AD.</span></span> <span data-ttu-id="baa67-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Thoughtworks Mingle debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="baa67-138">In other words, a link relationship between an Azure AD user and hello related user in Thoughtworks Mingle needs toobe established.</span></span>

<span data-ttu-id="baa67-139">En Thoughtworks Mingle, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="baa67-139">In Thoughtworks Mingle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="baa67-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Thoughtworks Mingle, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="baa67-140">tooconfigure and test Azure AD single sign-on with Thoughtworks Mingle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="baa67-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="baa67-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="baa67-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="baa67-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="baa67-143">**[Crear un usuario de prueba Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user) ** -toohave un equivalente de Britta Simon en Thoughtworks Mingle que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="baa67-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - toohave a counterpart of Britta Simon in Thoughtworks Mingle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="baa67-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="baa67-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="baa67-145">**[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="baa67-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="baa67-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="baa67-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="baa67-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="baa67-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="baa67-148">**inicio de sesión único en Azure AD tooconfigure con Thoughtworks Mingle, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="baa67-148">**tooconfigure Azure AD single sign-on with Thoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="baa67-149">En el portal de Azure, en Hola Hola **Thoughtworks Mingle** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="baa67-149">In hello Azure portal, on hello **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="baa67-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="baa67-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="baa67-153">En hello **Thoughtworks Mingle dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="baa67-153">On hello **Thoughtworks Mingle Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="baa67-155">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="baa67-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="baa67-156">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="baa67-156">hello value is not real.</span></span> <span data-ttu-id="baa67-157">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="baa67-157">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="baa67-158">Póngase en contacto con [equipo de soporte técnico de Thoughtworks Mingle cliente](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="baa67-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello value.</span></span> 
 
4. <span data-ttu-id="baa67-159">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="baa67-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="baa67-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="baa67-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="baa67-163">Inicie sesión en tooyour **Thoughtworks Mingle** como administrador.</span><span class="sxs-lookup"><span data-stu-id="baa67-163">Log in tooyour **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="baa67-164">Haga clic en hello **administración** pestaña y, a continuación, haga clic en **configuración de SSO**.</span><span class="sxs-lookup"><span data-stu-id="baa67-164">Click hello **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="baa67-165">![Pestaña de administrador](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Configuración de SSO")</span><span class="sxs-lookup"><span data-stu-id="baa67-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="baa67-166">Hola **configuración de SSO** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="baa67-166">In hello **SSO Config** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="baa67-167">![Configuración de SSO](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configuración de SSO")</span><span class="sxs-lookup"><span data-stu-id="baa67-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="baa67-168">a.</span><span class="sxs-lookup"><span data-stu-id="baa67-168">a.</span></span> <span data-ttu-id="baa67-169">archivo de metadatos de hello tooupload, haga clic en **Elegir archivo**.</span><span class="sxs-lookup"><span data-stu-id="baa67-169">tooupload hello metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="baa67-170">b.</span><span class="sxs-lookup"><span data-stu-id="baa67-170">b.</span></span> <span data-ttu-id="baa67-171">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="baa67-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="baa67-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="baa67-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="baa67-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="baa67-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="baa67-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="baa67-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="baa67-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="baa67-175">Create an Azure AD test user</span></span>
<span data-ttu-id="baa67-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="baa67-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="baa67-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="baa67-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="baa67-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="baa67-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="baa67-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="baa67-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="baa67-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="baa67-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="baa67-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="baa67-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="baa67-187">a.</span><span class="sxs-lookup"><span data-stu-id="baa67-187">a.</span></span> <span data-ttu-id="baa67-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="baa67-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="baa67-189">b.</span><span class="sxs-lookup"><span data-stu-id="baa67-189">b.</span></span> <span data-ttu-id="baa67-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="baa67-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="baa67-191">c.</span><span class="sxs-lookup"><span data-stu-id="baa67-191">c.</span></span> <span data-ttu-id="baa67-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="baa67-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="baa67-193">d.</span><span class="sxs-lookup"><span data-stu-id="baa67-193">d.</span></span> <span data-ttu-id="baa67-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="baa67-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="baa67-195">Creación de un usuario de prueba de Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="baa67-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="baa67-196">Para Azure AD a los usuarios toobe puede toosign en, deben ser aprovisionado toohello aplicación Thoughtworks Mingle con sus nombres de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baa67-196">For Azure AD users toobe able toosign in, they must be provisioned toohello Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="baa67-197">En caso de hello de Thoughtworks Mingle, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="baa67-197">In hello case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="baa67-198">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="baa67-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="baa67-199">Inicie sesión en tooyour sitio de la compañía de Thoughtworks Mingle como administrador.</span><span class="sxs-lookup"><span data-stu-id="baa67-199">Log in tooyour Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="baa67-200">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="baa67-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="baa67-201">![Su primer proyecto](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Su primer proyecto")</span><span class="sxs-lookup"><span data-stu-id="baa67-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="baa67-202">Haga clic en hello **administración** ficha y, a continuación, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="baa67-202">Click hello **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="baa67-203">![Usuarios](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="baa67-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="baa67-204">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="baa67-204">Click **New User**.</span></span>
   
    <span data-ttu-id="baa67-205">![Nuevo usuario](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="baa67-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="baa67-206">En hello **nuevo usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="baa67-206">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="baa67-207">![Cuadro de diálogo Nuevo usuario](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="baa67-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="baa67-208">a.</span><span class="sxs-lookup"><span data-stu-id="baa67-208">a.</span></span> <span data-ttu-id="baa67-209">Hola de tipo **nombre de inicio de sesión**, **nombre para mostrar**, **elegir contraseña**, **Confirmar contraseña** de un Azure válida que desee tooprovision de cuenta de AD en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="baa67-209">Type hello **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="baa67-210">b.</span><span class="sxs-lookup"><span data-stu-id="baa67-210">b.</span></span> <span data-ttu-id="baa67-211">En **User type** (Tipo de usuario), seleccione **Full user** (Usuario completo).</span><span class="sxs-lookup"><span data-stu-id="baa67-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="baa67-212">c.</span><span class="sxs-lookup"><span data-stu-id="baa67-212">c.</span></span> <span data-ttu-id="baa67-213">Haga clic en **Crear este perfil**.</span><span class="sxs-lookup"><span data-stu-id="baa67-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="baa67-214">Puede usar cualquier otra Thoughtworks Mingle usuario cuenta herramienta de creación o las API proporcionadas por Thoughtworks Mingle tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="baa67-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle tooprovision AAD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="baa67-215">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="baa67-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="baa67-216">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooThoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="baa67-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThoughtworks Mingle.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="baa67-218">**tooassign tooThoughtworks Britta Simon Mingle, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="baa67-218">**tooassign Britta Simon tooThoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="baa67-219">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="baa67-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="baa67-221">En la lista de aplicaciones de hello, seleccione **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="baa67-221">In hello applications list, select **Thoughtworks Mingle**.</span></span>

    ![vínculo de Thoughtworks Mingle de Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="baa67-223">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="baa67-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="baa67-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="baa67-225">Click **Add** button.</span></span> <span data-ttu-id="baa67-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="baa67-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="baa67-228">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="baa67-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="baa67-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="baa67-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="baa67-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="baa67-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="baa67-231">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="baa67-231">Test single sign-on</span></span>

<span data-ttu-id="baa67-232">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="baa67-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="baa67-233">Al hacer clic en icono de Thoughtworks Mingle Hola Hola Panel de acceso, deberá obtener aplicaciones de Thoughtworks Mingle tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="baa67-233">When you click hello Thoughtworks Mingle tile in hello Access Panel, you should get automatically signed-on tooyour Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="baa67-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="baa67-234">Additional resources</span></span>

* [<span data-ttu-id="baa67-235">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="baa67-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="baa67-236">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="baa67-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

