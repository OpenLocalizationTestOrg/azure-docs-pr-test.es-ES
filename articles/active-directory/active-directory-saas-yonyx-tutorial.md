---
title: "Tutorial: Integración de Azure Active Directory con Yonyx Interactive Guides | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y guías de Yonyx interactivo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 24e30d243143651b8d32535c76dc300931ae5746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="4e456-103">Tutorial: integración de Azure Active Directory con Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="4e456-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="4e456-104">En este tutorial, aprenderá cómo toointegrate Yonyx Interactive guía con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4e456-104">In this tutorial, you learn how toointegrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e456-105">Integración guías interactivas Yonyx con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4e456-105">Integrating Yonyx Interactive Guides with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4e456-106">Puede controlar en Azure AD que tenga acceso tooYonyx guías interactivas</span><span class="sxs-lookup"><span data-stu-id="4e456-106">You can control in Azure AD who has access tooYonyx Interactive Guides</span></span>
- <span data-ttu-id="4e456-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooYonyx guías interactivas (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e456-107">You can enable your users tooautomatically get signed-on tooYonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e456-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4e456-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4e456-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4e456-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e456-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4e456-110">Prerequisites</span></span>

<span data-ttu-id="4e456-111">integración de Azure AD con guías interactivas Yonyx tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4e456-111">tooconfigure Azure AD integration with Yonyx Interactive Guides, you need hello following items:</span></span>

- <span data-ttu-id="4e456-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e456-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e456-113">Una suscripción habilitada de inicio de sesión único de Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="4e456-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e456-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4e456-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e456-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4e456-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e456-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4e456-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e456-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e456-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e456-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4e456-118">Scenario description</span></span>
<span data-ttu-id="4e456-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4e456-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e456-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="4e456-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e456-121">Agregar guías interactivas Yonyx desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="4e456-121">Adding Yonyx Interactive Guides from hello gallery</span></span>
2. <span data-ttu-id="4e456-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e456-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-hello-gallery"></a><span data-ttu-id="4e456-123">Agregar guías interactivas Yonyx desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="4e456-123">Adding Yonyx Interactive Guides from hello gallery</span></span>
<span data-ttu-id="4e456-124">integración de hello tooconfigure de guías interactivas Yonyx en Azure AD, deberá tooadd Yonyx guías interactivas de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="4e456-124">tooconfigure hello integration of Yonyx Interactive Guides into Azure AD, you need tooadd Yonyx Interactive Guides from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4e456-125">**tooadd Yonyx guías interactivas de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4e456-125">**tooadd Yonyx Interactive Guides from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e456-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4e456-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="4e456-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4e456-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4e456-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4e456-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="4e456-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e456-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="4e456-133">En el cuadro de búsqueda de hello, escriba **guías interactivas Yonyx**, seleccione **guías interactivas Yonyx** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4e456-133">In hello search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Yonyx guías interactivas en la lista de resultados de Hola](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4e456-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e456-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4e456-136">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Yonyx Interactive Guides con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4e456-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4e456-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en guías interactivas Yonyx es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e456-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Yonyx Interactive Guides is tooa user in Azure AD.</span></span> <span data-ttu-id="4e456-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en guías interactivas Yonyx debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="4e456-138">In other words, a link relationship between an Azure AD user and hello related user in Yonyx Interactive Guides needs toobe established.</span></span>

<span data-ttu-id="4e456-139">En Yonyx guías interactivas, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e456-139">In Yonyx Interactive Guides, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4e456-140">tooconfigure y prueba de inicio de sesión único en Azure AD con guías interactivas Yonyx, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4e456-140">tooconfigure and test Azure AD single sign-on with Yonyx Interactive Guides, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4e456-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="4e456-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4e456-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4e456-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e456-143">**[Crear un usuario de prueba de guías interactivas Yonyx](#create-a-yonyx-interactive-guides-test-user)**  -toohave un equivalente de Britta Simon en Yonyx guías interactivas que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="4e456-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - toohave a counterpart of Britta Simon in Yonyx Interactive Guides that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e456-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4e456-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e456-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4e456-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4e456-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e456-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4e456-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de guías de Yonyx interactivo.</span><span class="sxs-lookup"><span data-stu-id="4e456-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="4e456-148">**tooconfigure inicio de sesión único en Azure AD con Yonyx guías interactivas, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4e456-148">**tooconfigure Azure AD single sign-on with Yonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e456-149">En el portal de Azure, en Hola Hola **guías interactivas Yonyx** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4e456-149">In hello Azure portal, on hello **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="4e456-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4e456-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="4e456-153">En hello **Yonyx interactivo guías de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4e456-153">On hello **Yonyx Interactive Guides Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de inicio de sesión único de Dominio y direcciones URL de Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="4e456-155">a.</span><span class="sxs-lookup"><span data-stu-id="4e456-155">a.</span></span> <span data-ttu-id="4e456-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="4e456-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="4e456-157">b.</span><span class="sxs-lookup"><span data-stu-id="4e456-157">b.</span></span> <span data-ttu-id="4e456-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="4e456-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e456-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4e456-159">These values are not real.</span></span> <span data-ttu-id="4e456-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="4e456-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4e456-161">Póngase en contacto con [equipo de soporte técnico de cliente interactivo de guías de Yonyx](mailto:support@yonyx.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="4e456-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="4e456-162">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4e456-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="4e456-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4e456-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4e456-166">En hello **Yonyx interactivo guías de configuración** sección, haga clic en **guías interactivas Yonyx configurar** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="4e456-166">On hello **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4e456-167">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="4e456-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="4e456-169">tooconfigure inicio de sesión único en **guías interactivas Yonyx** lado, necesita hello toosend descargado **Certificate(Base64)**, **dirección URL de cierre de sesión**, **SAML Solo la dirección URL del servicio Inicio de sesión** **Id. de entidad SAML** demasiado[equipo de soporte técnico de guías interactivas Yonyx](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="4e456-169">tooconfigure single sign-on on **Yonyx Interactive Guides** side, you need toosend hello downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** too[Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="4e456-170">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="4e456-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4e456-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="4e456-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4e456-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="4e456-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4e456-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4e456-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4e456-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e456-174">Create an Azure AD test user</span></span>

<span data-ttu-id="4e456-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4e456-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

  ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="4e456-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4e456-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e456-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4e456-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4e456-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4e456-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e456-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e456-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e456-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4e456-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e456-186">a.</span><span class="sxs-lookup"><span data-stu-id="4e456-186">a.</span></span> <span data-ttu-id="4e456-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e456-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e456-188">b.</span><span class="sxs-lookup"><span data-stu-id="4e456-188">b.</span></span> <span data-ttu-id="4e456-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4e456-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4e456-190">c.</span><span class="sxs-lookup"><span data-stu-id="4e456-190">c.</span></span> <span data-ttu-id="4e456-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4e456-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4e456-192">d.</span><span class="sxs-lookup"><span data-stu-id="4e456-192">d.</span></span> <span data-ttu-id="4e456-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4e456-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="4e456-194">Creación de un usuario de prueba de Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="4e456-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="4e456-195">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en guías interactivas Yonyx toocreate.</span><span class="sxs-lookup"><span data-stu-id="4e456-195">hello objective of this section is toocreate a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="4e456-196">Yonyx Interactive Guides admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4e456-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4e456-197">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="4e456-197">There is no action item for you in this section.</span></span> <span data-ttu-id="4e456-198">Si no existe todavía, se crea un usuario nuevo durante un tooaccess intento guías interactivas Yonyx.</span><span class="sxs-lookup"><span data-stu-id="4e456-198">A new user is created during an attempt tooaccess Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="4e456-199">Si necesita un usuario toocreate manualmente, necesita hello toocontact equipo a través de soporte técnico de guías interactivas Yonyx < mailto:support@yonyx.com >.</span><span class="sxs-lookup"><span data-stu-id="4e456-199">If you need toocreate a user manually, you need toocontact hello Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4e456-200">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e456-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4e456-201">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooYonyx guías interactivas.</span><span class="sxs-lookup"><span data-stu-id="4e456-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYonyx Interactive Guides.</span></span>

![Asigne el rol de usuario de Hola][200]

<span data-ttu-id="4e456-203">**tooassign guías interactivas de Britta Simon tooYonyx, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4e456-203">**tooassign Britta Simon tooYonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e456-204">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4e456-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4e456-206">En la lista de aplicaciones de hello, seleccione **Yonyx interactivo guías**.</span><span class="sxs-lookup"><span data-stu-id="4e456-206">In hello applications list, select **Yonyx Interactive Guides**.</span></span>

    ![Hola guías interactivas Yonyx vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="4e456-208">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4e456-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="4e456-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4e456-210">Click **Add** button.</span></span> <span data-ttu-id="4e456-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4e456-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="4e456-213">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e456-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4e456-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4e456-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e456-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4e456-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4e456-216">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="4e456-216">Test single sign-on</span></span>

<span data-ttu-id="4e456-217">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4e456-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4e456-218">Al hacer clic en hello guías interactivas Yonyx el icono Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación guías interactivas Yonyx.</span><span class="sxs-lookup"><span data-stu-id="4e456-218">When you click hello Yonyx Interactive Guides tile in hello Access Panel, you should get automatically signed-on tooyour Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="4e456-219">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4e456-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4e456-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4e456-220">Additional resources</span></span>

* [<span data-ttu-id="4e456-221">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e456-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e456-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4e456-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

