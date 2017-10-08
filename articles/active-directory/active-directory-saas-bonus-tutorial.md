---
title: "Tutorial: Integración de Azure Active Directory con Bonusly | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="cd3da-103">Tutorial: Integración de Azure Active Directory con Bonusly</span><span class="sxs-lookup"><span data-stu-id="cd3da-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="cd3da-104">En este tutorial, aprenderá cómo toointegrate Bonusly con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cd3da-104">In this tutorial, you learn how toointegrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd3da-105">Integración Bonusly con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cd3da-105">Integrating Bonusly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cd3da-106">Puede controlar en Azure AD que tenga acceso tooBonusly</span><span class="sxs-lookup"><span data-stu-id="cd3da-106">You can control in Azure AD who has access tooBonusly</span></span>
- <span data-ttu-id="cd3da-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBonusly (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd3da-107">You can enable your users tooautomatically get signed-on tooBonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd3da-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cd3da-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cd3da-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cd3da-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd3da-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cd3da-110">Prerequisites</span></span>

<span data-ttu-id="cd3da-111">integración de Azure AD con Bonusly tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cd3da-111">tooconfigure Azure AD integration with Bonusly, you need hello following items:</span></span>

- <span data-ttu-id="cd3da-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd3da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd3da-113">Una suscripción habilitada para el inicio de sesión único en Bonusly</span><span class="sxs-lookup"><span data-stu-id="cd3da-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd3da-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cd3da-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd3da-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cd3da-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd3da-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cd3da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd3da-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd3da-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd3da-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cd3da-118">Scenario description</span></span>
<span data-ttu-id="cd3da-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cd3da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd3da-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cd3da-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd3da-121">Agregar Bonusly desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cd3da-121">Adding Bonusly from hello gallery</span></span>
2. <span data-ttu-id="cd3da-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd3da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-hello-gallery"></a><span data-ttu-id="cd3da-123">Agregar Bonusly desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cd3da-123">Adding Bonusly from hello gallery</span></span>
<span data-ttu-id="cd3da-124">integración de hello tooconfigure de Bonusly en Azure AD, deberá tooadd Bonusly de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="cd3da-124">tooconfigure hello integration of Bonusly into Azure AD, you need tooadd Bonusly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cd3da-125">**tooadd Bonusly de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cd3da-125">**tooadd Bonusly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd3da-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cd3da-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="cd3da-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cd3da-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="cd3da-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cd3da-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="cd3da-133">En el cuadro de búsqueda de hello, escriba **Bonusly**, seleccione **Bonusly** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cd3da-133">In hello search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Bonusly en la lista de resultados de Hola](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cd3da-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd3da-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="cd3da-136">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con Bonusly con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cd3da-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cd3da-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Bonusly es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd3da-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bonusly is tooa user in Azure AD.</span></span> <span data-ttu-id="cd3da-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Bonusly debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="cd3da-138">In other words, a link relationship between an Azure AD user and hello related user in Bonusly needs toobe established.</span></span>

<span data-ttu-id="cd3da-139">En Bonusly, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd3da-139">In Bonusly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cd3da-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Bonusly, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cd3da-140">tooconfigure and test Azure AD single sign-on with Bonusly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cd3da-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cd3da-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cd3da-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd3da-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd3da-143">**[Crear un usuario de prueba Bonusly](#create-a-bonusly-test-user)**  -toohave un equivalente de Britta Simon en Bonusly que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="cd3da-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - toohave a counterpart of Britta Simon in Bonusly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd3da-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cd3da-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd3da-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cd3da-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cd3da-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd3da-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cd3da-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Bonusly.</span><span class="sxs-lookup"><span data-stu-id="cd3da-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="cd3da-148">**inicio de sesión único en Azure AD tooconfigure con Bonusly, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cd3da-148">**tooconfigure Azure AD single sign-on with Bonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd3da-149">En el portal de Azure, en Hola Hola **Bonusly** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-149">In hello Azure portal, on hello **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cd3da-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cd3da-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="cd3da-153">En hello **Bonusly de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cd3da-153">On hello **Bonusly Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="cd3da-155">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="cd3da-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd3da-156">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="cd3da-156">hello value is not real.</span></span> <span data-ttu-id="cd3da-157">Valor de Hola de actualización con Hola dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="cd3da-157">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="cd3da-158">Póngase en contacto con [equipo de soporte técnico Bonusly](https://Bonusly/contact) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="cd3da-158">Contact [Bonusly support team](https://Bonusly/contact) tooget hello value.</span></span>
 
4. <span data-ttu-id="cd3da-159">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** valor de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd3da-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="cd3da-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cd3da-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cd3da-163">En hello **configuración Bonusly** sección, haga clic en **configurar Bonusly** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="cd3da-163">On hello **Bonusly Configuration** section, click **Configure Bonusly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cd3da-164">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="cd3da-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="cd3da-166">En otra ventana del explorador, inicie sesión en tooyour **Bonusly** inquilino.</span><span class="sxs-lookup"><span data-stu-id="cd3da-166">In a different browser window, log in tooyour **Bonusly** tenant.</span></span>

8. <span data-ttu-id="cd3da-167">En la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**y, a continuación, seleccione **integraciones y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-167">In hello toolbar on hello top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="cd3da-168">![Sección Bonusly Social](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="cd3da-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="cd3da-169">En **Inicio de sesión único**, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="cd3da-170">En hello **SAML** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cd3da-170">On hello **SAML** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="cd3da-171">![Página de diálogo Saml Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="cd3da-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="cd3da-172">a.</span><span class="sxs-lookup"><span data-stu-id="cd3da-172">a.</span></span> <span data-ttu-id="cd3da-173">Hola **dirección URL de destino de SSO IdP** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd3da-173">In hello **IdP SSO target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="cd3da-174">b.</span><span class="sxs-lookup"><span data-stu-id="cd3da-174">b.</span></span> <span data-ttu-id="cd3da-175">Hola **emisor IdP** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd3da-175">In hello **IdP Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="cd3da-176">c.</span><span class="sxs-lookup"><span data-stu-id="cd3da-176">c.</span></span> <span data-ttu-id="cd3da-177">Hola **dirección URL de inicio de sesión IdP** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd3da-177">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cd3da-178">d.</span><span class="sxs-lookup"><span data-stu-id="cd3da-178">d.</span></span> <span data-ttu-id="cd3da-179">Pegar la **huella digital** valor copiado del portal de Azure en hello **huella digital de certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="cd3da-179">Paste the **Thumbprint** value copied from Azure portal into hello **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="cd3da-180">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cd3da-181">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="cd3da-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cd3da-182">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="cd3da-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cd3da-183">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cd3da-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cd3da-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd3da-184">Create an Azure AD test user</span></span>
<span data-ttu-id="cd3da-185">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cd3da-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="cd3da-187">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cd3da-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd3da-188">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cd3da-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd3da-190">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd3da-192">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd3da-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd3da-194">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cd3da-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd3da-196">a.</span><span class="sxs-lookup"><span data-stu-id="cd3da-196">a.</span></span> <span data-ttu-id="cd3da-197">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd3da-198">b.</span><span class="sxs-lookup"><span data-stu-id="cd3da-198">b.</span></span> <span data-ttu-id="cd3da-199">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cd3da-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd3da-200">c.</span><span class="sxs-lookup"><span data-stu-id="cd3da-200">c.</span></span> <span data-ttu-id="cd3da-201">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cd3da-202">d.</span><span class="sxs-lookup"><span data-stu-id="cd3da-202">d.</span></span> <span data-ttu-id="cd3da-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="cd3da-204">Creación de un usuario de prueba de Bonusly</span><span class="sxs-lookup"><span data-stu-id="cd3da-204">Create a Bonusly test user</span></span>

<span data-ttu-id="cd3da-205">En orden tooenable toolog de los usuarios de Azure AD en tooBonusly, se les deben aprovisionar en Bonusly.</span><span class="sxs-lookup"><span data-stu-id="cd3da-205">In order tooenable Azure AD users toolog in tooBonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="cd3da-206">En caso de hello de Bonusly, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="cd3da-206">In hello case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="cd3da-207">Puede usar cualquier otra herramienta de creación de cuentas de usuario Bonusly o las API proporcionadas por tooprovision Bonusly AAD cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="cd3da-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly tooprovision AAD user accounts.</span></span>
>  

<span data-ttu-id="cd3da-208">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cd3da-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd3da-209">En una ventana del explorador web, inicie sesión en el inquilino Bonusly tooyour.</span><span class="sxs-lookup"><span data-stu-id="cd3da-209">In a web browser window, log in tooyour Bonusly tenant.</span></span>

2. <span data-ttu-id="cd3da-210">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="cd3da-211">![Configuración](./media/active-directory-saas-bonus-tutorial/ic781041.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="cd3da-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="cd3da-212">Haga clic en hello **usuarios y bonificaciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="cd3da-212">Click hello **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="cd3da-213">![Usuarios y bonificaciones](./media/active-directory-saas-bonus-tutorial/ic781042.png "Usuarios y bonificaciones")</span><span class="sxs-lookup"><span data-stu-id="cd3da-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="cd3da-214">Haga clic en **Administrar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="cd3da-215">![Administración de usuarios](./media/active-directory-saas-bonus-tutorial/ic781043.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="cd3da-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="cd3da-216">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="cd3da-217">![Agregar usuario](./media/active-directory-saas-bonus-tutorial/ic781044.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="cd3da-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="cd3da-218">En hello **Agregar usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cd3da-218">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="cd3da-219">![Agregar usuario](./media/active-directory-saas-bonus-tutorial/ic781045.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="cd3da-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="cd3da-220">a.</span><span class="sxs-lookup"><span data-stu-id="cd3da-220">a.</span></span> <span data-ttu-id="cd3da-221">Hola **nombre** cuadro de texto, escriba Hola nombre de usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-221">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="cd3da-222">b.</span><span class="sxs-lookup"><span data-stu-id="cd3da-222">b.</span></span> <span data-ttu-id="cd3da-223">Hola **apellidos** cuadro de texto, escriba Hola último nombre de usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-223">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="cd3da-224">c.</span><span class="sxs-lookup"><span data-stu-id="cd3da-224">c.</span></span> <span data-ttu-id="cd3da-225">Hola **correo electrónico** cuadro de texto, escriba el correo electrónico de saludo del usuario como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="cd3da-225">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="cd3da-226">d.</span><span class="sxs-lookup"><span data-stu-id="cd3da-226">d.</span></span> <span data-ttu-id="cd3da-227">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="cd3da-228">titular de la cuenta de Hello Azure AD recibe un correo electrónico que incluye una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="cd3da-228">hello Azure AD account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span>
     >  

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cd3da-229">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd3da-229">Assign hello Azure AD test user</span></span>

<span data-ttu-id="cd3da-230">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBonusly.</span><span class="sxs-lookup"><span data-stu-id="cd3da-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBonusly.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="cd3da-232">**tooassign Britta Simon tooBonusly, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cd3da-232">**tooassign Britta Simon tooBonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd3da-233">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cd3da-235">En la lista de aplicaciones de hello, seleccione **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-235">In hello applications list, select **Bonusly**.</span></span>

    ![Hola Bonusly vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="cd3da-237">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="cd3da-239">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-239">Click **Add** button.</span></span> <span data-ttu-id="cd3da-240">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="cd3da-242">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd3da-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cd3da-243">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd3da-244">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cd3da-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cd3da-245">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="cd3da-245">Test single sign-on</span></span>

<span data-ttu-id="cd3da-246">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cd3da-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cd3da-247">Al hacer clic en icono Bonusly hello en Hola Panel de acceso, deberá obtener la aplicación Bonusly tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="cd3da-247">When you click hello Bonusly tile in hello Access Panel, you should get automatically signed-on tooyour Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd3da-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cd3da-248">Additional resources</span></span>

* [<span data-ttu-id="cd3da-249">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd3da-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd3da-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cd3da-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

