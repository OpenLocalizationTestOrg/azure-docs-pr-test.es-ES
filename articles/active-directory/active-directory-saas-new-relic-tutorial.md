---
title: "Tutorial: Integración de Azure Active Directory con New Relic | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="31dd6-103">Tutorial: Integración de Azure Active Directory con New Relic</span><span class="sxs-lookup"><span data-stu-id="31dd6-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="31dd6-104">En este tutorial, aprenderá cómo toointegrate New Relic con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31dd6-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31dd6-105">Integración de New Relic con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="31dd6-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="31dd6-106">Puede controlar en Azure AD que tenga acceso tooNew Relic</span><span class="sxs-lookup"><span data-stu-id="31dd6-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="31dd6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooNew Relic (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31dd6-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31dd6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="31dd6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="31dd6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31dd6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31dd6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="31dd6-110">Prerequisites</span></span>

<span data-ttu-id="31dd6-111">integración de Azure AD con New Relic tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="31dd6-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="31dd6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31dd6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31dd6-113">Una suscripción habilitada para el inicio de sesión único en New Relic</span><span class="sxs-lookup"><span data-stu-id="31dd6-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31dd6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="31dd6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31dd6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="31dd6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31dd6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="31dd6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31dd6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31dd6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31dd6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="31dd6-118">Scenario description</span></span>
<span data-ttu-id="31dd6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="31dd6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31dd6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="31dd6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31dd6-121">Adición de New Relic de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="31dd6-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="31dd6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31dd6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="31dd6-123">Adición de New Relic de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="31dd6-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="31dd6-124">integración de hello tooconfigure de New Relic en Azure AD, deberá tooadd New Relic de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="31dd6-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="31dd6-125">**tooadd New Relic de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31dd6-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="31dd6-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="31dd6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31dd6-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="31dd6-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="31dd6-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31dd6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="31dd6-133">En el cuadro de búsqueda de hello, escriba **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-133">In hello search box, type **New Relic**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="31dd6-135">En el panel de resultados de hello, seleccione **New Relic**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="31dd6-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31dd6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31dd6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31dd6-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con New Relic con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="31dd6-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31dd6-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en New Relic es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31dd6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="31dd6-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en New Relic debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="31dd6-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="31dd6-141">En New Relic, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="31dd6-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="31dd6-142">tooconfigure y prueba de inicio de sesión único en Azure AD con New Relic, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="31dd6-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="31dd6-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="31dd6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="31dd6-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31dd6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31dd6-145">**[Crear un usuario de prueba de New Relic](#creating-a-new-relic-test-user)**  -toohave un equivalente de Britta Simon en New Relic es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="31dd6-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="31dd6-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="31dd6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31dd6-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="31dd6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31dd6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31dd6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31dd6-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de New Relic.</span><span class="sxs-lookup"><span data-stu-id="31dd6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="31dd6-150">**inicio de sesión único en Azure AD tooconfigure con New Relic, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31dd6-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="31dd6-151">En el portal de Azure, en Hola Hola **New Relic** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="31dd6-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="31dd6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="31dd6-155">En hello **nuevo dominio Relic y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="31dd6-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="31dd6-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="31dd6-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31dd6-158">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="31dd6-158">hello value is not real.</span></span> <span data-ttu-id="31dd6-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="31dd6-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="31dd6-160">Póngase en contacto con [equipo de soporte técnico de nuevo cliente Relic](https://support.newrelic.com/) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="31dd6-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="31dd6-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="31dd6-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="31dd6-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="31dd6-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31dd6-165">En hello **nueva configuración de Relic** sección, haga clic en **configurar New Relic** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="31dd6-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="31dd6-166">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="31dd6-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="31dd6-168">En una ventana del explorador web diferente, inicie sesión en tooyour **New Relic** como administrador.</span><span class="sxs-lookup"><span data-stu-id="31dd6-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="31dd6-169">En el menú de hello en la parte superior de hello, haga clic en **configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="31dd6-170">![Configuración de la cuenta](./media/active-directory-saas-new-relic-tutorial/ic797036.png "configuración de la cuenta")</span><span class="sxs-lookup"><span data-stu-id="31dd6-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="31dd6-171">Haga clic en hello **seguridad y autenticación** ficha y, a continuación, haga clic en hello **inicio de sesión único** ficha.</span><span class="sxs-lookup"><span data-stu-id="31dd6-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="31dd6-172">![Inicio de sesión único](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="31dd6-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="31dd6-173">En la página de diálogo de hello SAML, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="31dd6-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="31dd6-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="31dd6-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="31dd6-175">a.</span><span class="sxs-lookup"><span data-stu-id="31dd6-175">a.</span></span> <span data-ttu-id="31dd6-176">Haga clic en **Elegir archivo** tooupload el certificado de Azure Active Directory descargado.</span><span class="sxs-lookup"><span data-stu-id="31dd6-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="31dd6-177">b.</span><span class="sxs-lookup"><span data-stu-id="31dd6-177">b.</span></span> <span data-ttu-id="31dd6-178">Hola **dirección URL de inicio de sesión remoto** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="31dd6-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="31dd6-179">c.</span><span class="sxs-lookup"><span data-stu-id="31dd6-179">c.</span></span> <span data-ttu-id="31dd6-180">Hola **dirección URL de destino de cierre de sesión** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="31dd6-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="31dd6-181">d.</span><span class="sxs-lookup"><span data-stu-id="31dd6-181">d.</span></span> <span data-ttu-id="31dd6-182">Haga clic en **Guardar los cambios**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="31dd6-183">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="31dd6-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="31dd6-184">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="31dd6-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="31dd6-185">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31dd6-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31dd6-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31dd6-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="31dd6-187">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="31dd6-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="31dd6-189">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31dd6-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="31dd6-190">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="31dd6-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31dd6-192">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31dd6-194">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="31dd6-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31dd6-196">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="31dd6-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31dd6-198">a.</span><span class="sxs-lookup"><span data-stu-id="31dd6-198">a.</span></span> <span data-ttu-id="31dd6-199">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31dd6-200">b.</span><span class="sxs-lookup"><span data-stu-id="31dd6-200">b.</span></span> <span data-ttu-id="31dd6-201">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="31dd6-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31dd6-202">c.</span><span class="sxs-lookup"><span data-stu-id="31dd6-202">c.</span></span> <span data-ttu-id="31dd6-203">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="31dd6-204">d.</span><span class="sxs-lookup"><span data-stu-id="31dd6-204">d.</span></span> <span data-ttu-id="31dd6-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="31dd6-206">Creación de un usuario de prueba de New Relic</span><span class="sxs-lookup"><span data-stu-id="31dd6-206">Creating a New Relic test user</span></span>

<span data-ttu-id="31dd6-207">En orden tooenable toolog de los usuarios de Azure Active Directory en tooNew Relic, se les deben aprovisionar en New Relic.</span><span class="sxs-lookup"><span data-stu-id="31dd6-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="31dd6-208">En caso de hello de New Relic, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="31dd6-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="31dd6-209">**tooprovision un tooNew de cuenta de usuario Relic, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31dd6-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="31dd6-210">Inicie sesión en tooyour **New Relic** como administrador.</span><span class="sxs-lookup"><span data-stu-id="31dd6-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="31dd6-211">En el menú de hello en la parte superior de hello, haga clic en **configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="31dd6-212">![Configuración de la cuenta](./media/active-directory-saas-new-relic-tutorial/ic797040.png "configuración de la cuenta")</span><span class="sxs-lookup"><span data-stu-id="31dd6-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="31dd6-213">Hola **cuenta** panel Hola lado izquierdo, haga clic en **resumen**y, a continuación, haga clic en **para agregar un usuario**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="31dd6-214">![Configuración de la cuenta](./media/active-directory-saas-new-relic-tutorial/ic797041.png "configuración de la cuenta")</span><span class="sxs-lookup"><span data-stu-id="31dd6-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="31dd6-215">En hello **usuarios activos** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="31dd6-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="31dd6-216">![Usuarios activos](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Usuarios activos")</span><span class="sxs-lookup"><span data-stu-id="31dd6-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="31dd6-217">a.</span><span class="sxs-lookup"><span data-stu-id="31dd6-217">a.</span></span> <span data-ttu-id="31dd6-218">Hola **correo electrónico** cuadro de texto, hello de tipo dirección de correo electrónico de un usuario válido de Azure Active Directory que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="31dd6-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="31dd6-219">b.</span><span class="sxs-lookup"><span data-stu-id="31dd6-219">b.</span></span> <span data-ttu-id="31dd6-220">Como **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="31dd6-221">c.</span><span class="sxs-lookup"><span data-stu-id="31dd6-221">c.</span></span> <span data-ttu-id="31dd6-222">Haga clic en **Agregar este usuario**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="31dd6-223">Puede usar cualquier otra New Relic usuario cuenta herramienta de creación o las API proporcionadas por New Relic tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="31dd6-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="31dd6-224">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="31dd6-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="31dd6-225">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooNew Relic.</span><span class="sxs-lookup"><span data-stu-id="31dd6-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="31dd6-227">**tooassign tooNew Britta Simon Relic, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31dd6-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="31dd6-228">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="31dd6-230">En la lista de aplicaciones de hello, seleccione **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-230">In hello applications list, select **New Relic**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="31dd6-232">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="31dd6-234">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-234">Click **Add** button.</span></span> <span data-ttu-id="31dd6-235">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="31dd6-237">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="31dd6-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="31dd6-238">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31dd6-239">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31dd6-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31dd6-240">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="31dd6-240">Testing single sign-on</span></span>

<span data-ttu-id="31dd6-241">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="31dd6-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="31dd6-242">Al hacer clic en icono de New Relic Hola Hola Panel de acceso, deberá obtener la aplicación de New Relic tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="31dd6-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31dd6-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="31dd6-243">Additional resources</span></span>

* [<span data-ttu-id="31dd6-244">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31dd6-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31dd6-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31dd6-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

