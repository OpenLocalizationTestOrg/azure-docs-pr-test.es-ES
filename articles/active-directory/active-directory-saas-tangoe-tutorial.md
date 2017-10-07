---
title: "Tutorial: integración de Azure Active Directory con Tangoe Command Premium Mobile | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Tangoe comando Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="0e067-103">Tutorial: Integración de Azure Active Directory con Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="0e067-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="0e067-104">En este tutorial, aprenderá cómo toointegrate Tangoe comando Premium móviles con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e067-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e067-105">Integración Tangoe comando Premium móviles con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0e067-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e067-106">Puede controlar en Azure AD que tenga acceso tooTangoe comando Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="0e067-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="0e067-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTangoe comando Premium Mobile (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e067-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e067-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0e067-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0e067-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e067-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e067-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e067-110">Prerequisites</span></span>

<span data-ttu-id="0e067-111">integración de Azure AD con Tangoe comando Premium Mobile tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0e067-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="0e067-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e067-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e067-113">Una suscripción habilitada para el inicio de sesión único en Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="0e067-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e067-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0e067-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e067-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0e067-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e067-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0e067-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e067-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e067-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e067-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0e067-118">Scenario description</span></span>
<span data-ttu-id="0e067-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0e067-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e067-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0e067-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e067-121">Agregar Tangoe comando Premium móviles desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0e067-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="0e067-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e067-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="0e067-123">Agregar Tangoe comando Premium móviles desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0e067-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="0e067-124">integración de hello tooconfigure de Tangoe comando Premium Mobile en Azure AD, deberá tooadd Tangoe comando Premium Mobile de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0e067-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e067-125">**tooadd Tangoe comando Premium móviles desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e067-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e067-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0e067-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e067-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0e067-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e067-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0e067-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0e067-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e067-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0e067-133">En el cuadro de búsqueda de hello, escriba **Tangoe comando Premium Mobile**, seleccione **Tangoe comando Premium Mobile** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0e067-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="0e067-134">Incorporación de Tangoe Command Premium Mobile desde la galería</span><span class="sxs-lookup"><span data-stu-id="0e067-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0e067-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e067-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0e067-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Tangoe Command Premium Mobile con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0e067-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e067-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Tangoe comando Premium Mobile es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e067-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="0e067-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Tangoe comando Premium Mobile debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0e067-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="0e067-139">En dispositivos móviles de Tangoe comando Premium, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e067-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e067-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Tangoe comando Premium Mobile, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0e067-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e067-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0e067-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e067-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e067-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e067-143">**[Crear un usuario de prueba de Tangoe comando Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user) ** -toohave un equivalente de Britta Simon en Tangoe comando Premium Mobile que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0e067-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e067-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0e067-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e067-145">**[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0e067-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0e067-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e067-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0e067-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación móvil de Tangoe comando Premium.</span><span class="sxs-lookup"><span data-stu-id="0e067-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="0e067-148">**tooconfigure inicio de sesión único en Azure AD con Tangoe comando Premium Mobile, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e067-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e067-149">En el portal de Azure, en Hola Hola **Tangoe comando Premium Mobile** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0e067-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0e067-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0e067-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="0e067-153">En hello **Tangoe comando Premium Mobile dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0e067-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![Dominio y direcciones URL de Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="0e067-155">a.</span><span class="sxs-lookup"><span data-stu-id="0e067-155">a.</span></span> <span data-ttu-id="0e067-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="0e067-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="0e067-157">b.</span><span class="sxs-lookup"><span data-stu-id="0e067-157">b.</span></span> <span data-ttu-id="0e067-158">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="0e067-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e067-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0e067-159">These values are not real.</span></span> <span data-ttu-id="0e067-160">Actualizar estos valores con la dirección URL de respuesta real hello y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0e067-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="0e067-161">Póngase en contacto con [equipo de soporte técnico de Tangoe comando Premium Mobile Client](https://www.tangoe.com/contact-2/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="0e067-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="0e067-162">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0e067-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="0e067-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0e067-164">Click **Save** button.</span></span>

    ![Botón Guardar](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="0e067-166">En hello **Tangoe comando Premium Mobile configuración** sección, haga clic en **configurar Tangoe comando Premium Mobile** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0e067-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0e067-167">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0e067-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sección de configuración de Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="0e067-169">tooget SSO configurado para la aplicación, póngase en contacto con su [equipo de soporte técnico de Tangoe comando Premium Mobile Client](https://www.tangoe.com/contact-2/) y proporciona Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e067-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="0e067-170">archivo de metadatos descargado Hola</span><span class="sxs-lookup"><span data-stu-id="0e067-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="0e067-171">Hola **Id. de entidad de SAML**</span><span class="sxs-lookup"><span data-stu-id="0e067-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="0e067-172">Hola **SAML Single Sign-On dirección URL del servicio**</span><span class="sxs-lookup"><span data-stu-id="0e067-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="0e067-173">Hola **dirección URL de cierre de sesión**</span><span class="sxs-lookup"><span data-stu-id="0e067-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="0e067-174">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0e067-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e067-175">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0e067-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e067-176">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e067-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0e067-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e067-177">Create an Azure AD test user</span></span>
<span data-ttu-id="0e067-178">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0e067-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0e067-180">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e067-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e067-181">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0e067-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e067-183">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0e067-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Usuarios y grupos -> Todos los usuarios](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e067-185">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e067-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Agregar usuario](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e067-187">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0e067-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Página del cuadro de diálogo Usuario](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e067-189">a.</span><span class="sxs-lookup"><span data-stu-id="0e067-189">a.</span></span> <span data-ttu-id="0e067-190">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e067-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e067-191">b.</span><span class="sxs-lookup"><span data-stu-id="0e067-191">b.</span></span> <span data-ttu-id="0e067-192">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0e067-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e067-193">c.</span><span class="sxs-lookup"><span data-stu-id="0e067-193">c.</span></span> <span data-ttu-id="0e067-194">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0e067-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0e067-195">d.</span><span class="sxs-lookup"><span data-stu-id="0e067-195">d.</span></span> <span data-ttu-id="0e067-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0e067-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="0e067-197">Crear un usuario de prueba de Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="0e067-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="0e067-198">En esta sección, creará un usuario llamado Britta Simon en Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="0e067-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="0e067-199">Aplicación Tangoe comando Premium Mobile debe todos los toobe de los usuarios de hello aprovisionado en aplicación hello antes de realizar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0e067-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="0e067-200">Así pues, el trabajo con hello [equipo de soporte técnico de Tangoe comando Premium Mobile Client](https://www.tangoe.com/contact-2/) tooprovision todos estos usuarios en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0e067-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0e067-201">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e067-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0e067-202">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTangoe comando Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="0e067-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0e067-204">**tooassign Britta Simon tooTangoe comando Premium Mobile, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e067-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e067-205">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0e067-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0e067-207">En la lista de aplicaciones de hello, seleccione **Tangoe comando Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="0e067-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe Command Premium Mobile en la lista de aplicaciones](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="0e067-209">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e067-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0e067-211">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0e067-211">Click **Add** button.</span></span> <span data-ttu-id="0e067-212">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0e067-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0e067-214">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e067-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e067-215">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e067-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e067-216">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0e067-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0e067-217">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="0e067-217">Test single sign-on</span></span>

<span data-ttu-id="0e067-218">En esta sección, probará la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0e067-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0e067-219">Al hacer clic en icono de Tangoe comando Premium Mobile Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Tangoe comando Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="0e067-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="0e067-220">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0e067-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0e067-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0e067-221">Additional resources</span></span>

* [<span data-ttu-id="0e067-222">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e067-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e067-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e067-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

