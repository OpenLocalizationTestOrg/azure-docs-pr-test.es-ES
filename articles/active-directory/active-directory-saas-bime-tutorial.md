---
title: "Tutorial: Integración de Azure Active Directory con Bime | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Bime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="01dfc-103">Tutorial: Integración de Azure Active Directory con Bime</span><span class="sxs-lookup"><span data-stu-id="01dfc-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="01dfc-104">En este tutorial, aprenderá cómo toointegrate Bime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="01dfc-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01dfc-105">Integración Bime con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="01dfc-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="01dfc-106">Puede controlar en Azure AD que tenga acceso tooBime</span><span class="sxs-lookup"><span data-stu-id="01dfc-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="01dfc-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBime (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01dfc-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01dfc-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="01dfc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="01dfc-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="01dfc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01dfc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="01dfc-110">Prerequisites</span></span>

<span data-ttu-id="01dfc-111">integración de Azure AD con Bime tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="01dfc-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="01dfc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01dfc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01dfc-113">Una suscripción a Bime con el inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="01dfc-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="01dfc-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="01dfc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="01dfc-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="01dfc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01dfc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="01dfc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="01dfc-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01dfc-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01dfc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="01dfc-118">Scenario description</span></span>
<span data-ttu-id="01dfc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="01dfc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="01dfc-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="01dfc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01dfc-121">Agregar Bime desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="01dfc-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="01dfc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01dfc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="01dfc-123">Agregar Bime desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="01dfc-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="01dfc-124">integración de hello tooconfigure de Bime en Azure AD, deberá tooadd Bime de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="01dfc-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="01dfc-125">**tooadd Bime de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="01dfc-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="01dfc-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="01dfc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="01dfc-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="01dfc-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="01dfc-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01dfc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="01dfc-133">En el cuadro de búsqueda de hello, escriba **Bime**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-133">In hello search box, type **Bime**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="01dfc-135">En el panel de resultados de hello, seleccione **Bime**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="01dfc-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01dfc-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01dfc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="01dfc-138">En esta sección, se configura y prueba el inicio de sesión único de Azure AD con Bime con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="01dfc-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="01dfc-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Bime es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01dfc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="01dfc-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Bime debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="01dfc-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="01dfc-141">En Bime, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="01dfc-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="01dfc-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Bime, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="01dfc-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="01dfc-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="01dfc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="01dfc-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01dfc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="01dfc-145">**[Crear un usuario de prueba de Bime](#creating-a-bime-test-user)**  -toohave un equivalente de Britta Simon en Bime que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="01dfc-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="01dfc-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="01dfc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="01dfc-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="01dfc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01dfc-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01dfc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="01dfc-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Bime.</span><span class="sxs-lookup"><span data-stu-id="01dfc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="01dfc-150">**inicio de sesión único en tooconfigure Azure AD con Bime, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="01dfc-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="01dfc-151">En el portal de Azure, en Hola Hola **Bime** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="01dfc-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="01dfc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="01dfc-155">En hello **Bime dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="01dfc-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="01dfc-157">a.</span><span class="sxs-lookup"><span data-stu-id="01dfc-157">a.</span></span> <span data-ttu-id="01dfc-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="01dfc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="01dfc-159">b.</span><span class="sxs-lookup"><span data-stu-id="01dfc-159">b.</span></span> <span data-ttu-id="01dfc-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="01dfc-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="01dfc-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="01dfc-161">These values are not real.</span></span> <span data-ttu-id="01dfc-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="01dfc-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="01dfc-163">Póngase en contacto con [equipo de soporte técnico de cliente de Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="01dfc-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="01dfc-164">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** valor de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="01dfc-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="01dfc-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="01dfc-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="01dfc-168">En hello **configuración de Bime** sección, haga clic en **configurar Bime** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="01dfc-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="01dfc-169">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="01dfc-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="01dfc-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Bime.</span><span class="sxs-lookup"><span data-stu-id="01dfc-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="01dfc-172">En la barra de herramientas de hello, haga clic en **administración**y, a continuación, **cuenta**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="01dfc-173">![Administración](./media/active-directory-saas-bime-tutorial/ic775558.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="01dfc-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="01dfc-174">En la página de configuración de la cuenta de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="01dfc-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="01dfc-175">![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/ic775559.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="01dfc-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="01dfc-176">a.</span><span class="sxs-lookup"><span data-stu-id="01dfc-176">a.</span></span> <span data-ttu-id="01dfc-177">Seleccione **Enable SAML authentication** (Habilitar autenticación SAML).</span><span class="sxs-lookup"><span data-stu-id="01dfc-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="01dfc-178">b.</span><span class="sxs-lookup"><span data-stu-id="01dfc-178">b.</span></span> <span data-ttu-id="01dfc-179">Hola **dirección URL de inicio de sesión remoto** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="01dfc-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="01dfc-180">c.</span><span class="sxs-lookup"><span data-stu-id="01dfc-180">c.</span></span>  <span data-ttu-id="01dfc-181">Hola pegar **huella digital** valor desde el portal de Azure en hello **huella digital de certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="01dfc-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="01dfc-182">d.</span><span class="sxs-lookup"><span data-stu-id="01dfc-182">d.</span></span> <span data-ttu-id="01dfc-183">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="01dfc-184">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="01dfc-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="01dfc-185">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="01dfc-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="01dfc-186">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="01dfc-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01dfc-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01dfc-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="01dfc-188">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="01dfc-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="01dfc-190">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="01dfc-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="01dfc-191">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="01dfc-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="01dfc-193">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="01dfc-195">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="01dfc-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01dfc-197">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="01dfc-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="01dfc-199">a.</span><span class="sxs-lookup"><span data-stu-id="01dfc-199">a.</span></span> <span data-ttu-id="01dfc-200">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01dfc-201">b.</span><span class="sxs-lookup"><span data-stu-id="01dfc-201">b.</span></span> <span data-ttu-id="01dfc-202">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="01dfc-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="01dfc-203">c.</span><span class="sxs-lookup"><span data-stu-id="01dfc-203">c.</span></span> <span data-ttu-id="01dfc-204">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="01dfc-205">d.</span><span class="sxs-lookup"><span data-stu-id="01dfc-205">d.</span></span> <span data-ttu-id="01dfc-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="01dfc-207">Creación de usuario de prueba de Bime</span><span class="sxs-lookup"><span data-stu-id="01dfc-207">Creating a Bime test user</span></span>

<span data-ttu-id="01dfc-208">En orden tooenable toolog de los usuarios de Azure AD en tooBime, se les deben aprovisionar en Bime.</span><span class="sxs-lookup"><span data-stu-id="01dfc-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="01dfc-209">En caso de hello de Bime, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="01dfc-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="01dfc-210">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="01dfc-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="01dfc-211">Inicie sesión en tooyour **Bime** inquilino.</span><span class="sxs-lookup"><span data-stu-id="01dfc-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="01dfc-212">En la barra de herramientas de hello, haga clic en **administración**y, a continuación, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="01dfc-213">![Administración](./media/active-directory-saas-bime-tutorial/ic775561.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="01dfc-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="01dfc-214">Hola **lista de usuarios**, haga clic en **Agregar nuevo usuario** ("+").</span><span class="sxs-lookup"><span data-stu-id="01dfc-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="01dfc-215">![Usuarios](./media/active-directory-saas-bime-tutorial/ic775562.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="01dfc-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="01dfc-216">En hello **detalles del usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="01dfc-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="01dfc-217">![Detalles del usuario](./media/active-directory-saas-bime-tutorial/ic775563.png "Detalles del usuario")</span><span class="sxs-lookup"><span data-stu-id="01dfc-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="01dfc-218">a.</span><span class="sxs-lookup"><span data-stu-id="01dfc-218">a.</span></span> <span data-ttu-id="01dfc-219">Hola **nombre** cuadro de texto, escriba Hola nombre de usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="01dfc-220">b.</span><span class="sxs-lookup"><span data-stu-id="01dfc-220">b.</span></span> <span data-ttu-id="01dfc-221">Hola **apellidos** cuadro de texto, escriba Hola último nombre de usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="01dfc-222">c.</span><span class="sxs-lookup"><span data-stu-id="01dfc-222">c.</span></span> <span data-ttu-id="01dfc-223">Hola **correo electrónico** cuadro de texto, escriba el correo electrónico de saludo del usuario como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="01dfc-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="01dfc-224">d.</span><span class="sxs-lookup"><span data-stu-id="01dfc-224">d.</span></span> <span data-ttu-id="01dfc-225">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="01dfc-226">Puede usar cualquier otra Bime usuario cuenta herramienta de creación o las API proporcionadas por Bime tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="01dfc-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="01dfc-227">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="01dfc-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="01dfc-228">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBime.</span><span class="sxs-lookup"><span data-stu-id="01dfc-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="01dfc-230">**tooassign Britta Simon tooBime, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="01dfc-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="01dfc-231">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="01dfc-233">En la lista de aplicaciones de hello, seleccione **Bime**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-233">In hello applications list, select **Bime**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="01dfc-235">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="01dfc-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-237">Click **Add** button.</span></span> <span data-ttu-id="01dfc-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="01dfc-240">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="01dfc-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="01dfc-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="01dfc-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="01dfc-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="01dfc-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="01dfc-243">Testing single sign-on</span></span>

<span data-ttu-id="01dfc-244">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="01dfc-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="01dfc-245">Al hacer clic en icono de Bime Hola Hola Panel de acceso, deberá obtener aplicaciones de Bime tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="01dfc-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="01dfc-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="01dfc-246">Additional resources</span></span>

* [<span data-ttu-id="01dfc-247">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01dfc-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01dfc-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="01dfc-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

