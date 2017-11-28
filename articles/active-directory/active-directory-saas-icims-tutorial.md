---
title: "Tutorial: integración de Azure Active Directory con ICIMS | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ICIMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3fa970f008e64e84b0a1280f691f0181851b757c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="a0763-103">Tutorial: integración de Azure Active Directory con ICIMS</span><span class="sxs-lookup"><span data-stu-id="a0763-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="a0763-104">En este tutorial, aprenderá cómo toointegrate ICIMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0763-104">In this tutorial, you learn how toointegrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0763-105">Integración ICIMS con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a0763-105">Integrating ICIMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a0763-106">Puede controlar en Azure AD que tenga acceso tooICIMS</span><span class="sxs-lookup"><span data-stu-id="a0763-106">You can control in Azure AD who has access tooICIMS</span></span>
- <span data-ttu-id="a0763-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooICIMS (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0763-107">You can enable your users tooautomatically get signed-on tooICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0763-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a0763-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a0763-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0763-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0763-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a0763-110">Prerequisites</span></span>

<span data-ttu-id="a0763-111">integración de Azure AD con ICIMS tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a0763-111">tooconfigure Azure AD integration with ICIMS, you need hello following items:</span></span>

- <span data-ttu-id="a0763-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0763-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0763-113">Una suscripción habilitada para el inicio de sesión único en ICIMS</span><span class="sxs-lookup"><span data-stu-id="a0763-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0763-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a0763-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0763-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a0763-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0763-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a0763-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0763-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0763-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0763-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a0763-118">Scenario description</span></span>
<span data-ttu-id="a0763-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a0763-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0763-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="a0763-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0763-121">Agregar ICIMS desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a0763-121">Adding ICIMS from hello gallery</span></span>
2. <span data-ttu-id="a0763-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0763-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-hello-gallery"></a><span data-ttu-id="a0763-123">Agregar ICIMS desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a0763-123">Adding ICIMS from hello gallery</span></span>
<span data-ttu-id="a0763-124">integración de hello tooconfigure de ICIMS en Azure AD, deberá tooadd ICIMS de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="a0763-124">tooconfigure hello integration of ICIMS into Azure AD, you need tooadd ICIMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a0763-125">**tooadd ICIMS de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a0763-125">**tooadd ICIMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0763-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a0763-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="a0763-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a0763-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a0763-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a0763-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="a0763-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a0763-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="a0763-133">En el cuadro de búsqueda de hello, escriba **ICIMS**, seleccione **ICIMS** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a0763-133">In hello search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ICIMS en la lista de resultados de Hola](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a0763-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0763-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a0763-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ICIMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a0763-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a0763-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ICIMS es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0763-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ICIMS is tooa user in Azure AD.</span></span> <span data-ttu-id="a0763-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ICIMS debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="a0763-138">In other words, a link relationship between an Azure AD user and hello related user in ICIMS needs toobe established.</span></span>

<span data-ttu-id="a0763-139">En ICIMS, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0763-139">In ICIMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a0763-140">tooconfigure y prueba de inicio de sesión único en Azure AD con ICIMS, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a0763-140">tooconfigure and test Azure AD single sign-on with ICIMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a0763-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="a0763-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a0763-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0763-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0763-143">**[Crear un usuario de prueba ICIMS](#create-an-icims-test-user) ** -toohave un equivalente de Britta Simon en ICIMS que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="a0763-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - toohave a counterpart of Britta Simon in ICIMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0763-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a0763-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0763-145">**[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a0763-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a0763-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0763-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a0763-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación ICIMS.</span><span class="sxs-lookup"><span data-stu-id="a0763-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="a0763-148">**inicio de sesión único en Azure AD tooconfigure con ICIMS, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a0763-148">**tooconfigure Azure AD single sign-on with ICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0763-149">En el portal de Azure, en Hola Hola **ICIMS** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a0763-149">In hello Azure portal, on hello **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a0763-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a0763-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="a0763-153">En hello **ICIMS dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a0763-153">On hello **ICIMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="a0763-155">a.</span><span class="sxs-lookup"><span data-stu-id="a0763-155">a.</span></span> <span data-ttu-id="a0763-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="a0763-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="a0763-157">b.</span><span class="sxs-lookup"><span data-stu-id="a0763-157">b.</span></span> <span data-ttu-id="a0763-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="a0763-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0763-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="a0763-159">These values are not real.</span></span> <span data-ttu-id="a0763-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="a0763-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a0763-161">Póngase en contacto con [equipo de soporte técnico de cliente de ICIMS](https://www.icims.com/contact-us) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="a0763-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="a0763-162">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a0763-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="a0763-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a0763-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0763-166">En hello **ICIMS configuración** sección, haga clic en **configurar ICIMS** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="a0763-166">On hello **ICIMS Configuration** section, click **Configure ICIMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a0763-167">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="a0763-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="a0763-169">tooconfigure inicio de sesión único en **ICIMS** lado, necesita hello toosend descargado **Metadata XML**, **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** demasiado [Equipo de soporte técnico ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="a0763-169">tooconfigure single sign-on on **ICIMS** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="a0763-170">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="a0763-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a0763-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="a0763-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a0763-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="a0763-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a0763-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a0763-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a0763-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0763-174">Create an Azure AD test user</span></span>
<span data-ttu-id="a0763-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="a0763-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="a0763-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a0763-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0763-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a0763-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0763-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a0763-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0763-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0763-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0763-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="a0763-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0763-186">a.</span><span class="sxs-lookup"><span data-stu-id="a0763-186">a.</span></span> <span data-ttu-id="a0763-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0763-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0763-188">b.</span><span class="sxs-lookup"><span data-stu-id="a0763-188">b.</span></span> <span data-ttu-id="a0763-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0763-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0763-190">c.</span><span class="sxs-lookup"><span data-stu-id="a0763-190">c.</span></span> <span data-ttu-id="a0763-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a0763-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a0763-192">d.</span><span class="sxs-lookup"><span data-stu-id="a0763-192">d.</span></span> <span data-ttu-id="a0763-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a0763-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="a0763-194">Creación de un usuario de prueba de ICIMS</span><span class="sxs-lookup"><span data-stu-id="a0763-194">Create an ICIMS test user</span></span>

<span data-ttu-id="a0763-195">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en ICIMS toocreate.</span><span class="sxs-lookup"><span data-stu-id="a0763-195">hello objective of this section is toocreate a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="a0763-196">Trabajar con [equipo de soporte técnico ICIMS](https://www.icims.com/contact-us) a los usuarios de tooadd Hola Hola cuenta ICIMS.</span><span class="sxs-lookup"><span data-stu-id="a0763-196">Work with [ICIMS support team](https://www.icims.com/contact-us) tooadd hello users in hello ICIMS account.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a0763-197">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0763-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a0763-198">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooICIMS.</span><span class="sxs-lookup"><span data-stu-id="a0763-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooICIMS.</span></span>

![Asigne el rol de usuario de Hola][200]

<span data-ttu-id="a0763-200">**tooassign Britta Simon tooICIMS, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a0763-200">**tooassign Britta Simon tooICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0763-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a0763-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a0763-203">En la lista de aplicaciones de hello, seleccione **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="a0763-203">In hello applications list, select **ICIMS**.</span></span>

    ![Hola ICIMS vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="a0763-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a0763-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="a0763-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a0763-207">Click **Add** button.</span></span> <span data-ttu-id="a0763-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a0763-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="a0763-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0763-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a0763-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a0763-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0763-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a0763-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a0763-213">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a0763-213">Test single sign-on</span></span>

<span data-ttu-id="a0763-214">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a0763-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="a0763-215">Al hacer clic en hello ICIMS el icono Panel de acceso de hello, deberá obtener la aplicación de ICIMS tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="a0763-215">When you click hello ICIMS tile in hello Access Panel, you should get automatically signed-on tooyour ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0763-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a0763-216">Additional resources</span></span>

* [<span data-ttu-id="a0763-217">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0763-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0763-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a0763-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

