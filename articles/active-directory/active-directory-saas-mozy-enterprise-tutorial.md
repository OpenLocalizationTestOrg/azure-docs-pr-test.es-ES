---
title: "Tutorial: Integración de Azure Active Directory con Mozy Enterprise | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="3dbd9-103">Tutorial: Integración de Azure Active Directory con Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="3dbd9-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="3dbd9-104">En este tutorial, aprenderá cómo toointegrate Mozy Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3dbd9-104">In this tutorial, you learn how toointegrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3dbd9-105">Integración de Mozy Enterprise con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3dbd9-105">Integrating Mozy Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3dbd9-106">Puede controlar en Azure AD que tenga acceso tooMozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="3dbd9-106">You can control in Azure AD who has access tooMozy Enterprise</span></span>
- <span data-ttu-id="3dbd9-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMozy Enterprise (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dbd9-107">You can enable your users tooautomatically get signed-on tooMozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3dbd9-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3dbd9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3dbd9-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3dbd9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dbd9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3dbd9-110">Prerequisites</span></span>

<span data-ttu-id="3dbd9-111">tooconfigure integración de Azure AD con Mozy Enterprise, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3dbd9-111">tooconfigure Azure AD integration with Mozy Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="3dbd9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dbd9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3dbd9-113">Una suscripción habilitada para el inicio de sesión único en Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="3dbd9-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3dbd9-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3dbd9-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3dbd9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3dbd9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3dbd9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3dbd9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3dbd9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3dbd9-118">Scenario description</span></span>
<span data-ttu-id="3dbd9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3dbd9-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3dbd9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3dbd9-121">Agregar Mozy Enterprise desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3dbd9-121">Adding Mozy Enterprise from hello gallery</span></span>
2. <span data-ttu-id="3dbd9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dbd9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-hello-gallery"></a><span data-ttu-id="3dbd9-123">Agregar Mozy Enterprise desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3dbd9-123">Adding Mozy Enterprise from hello gallery</span></span>
<span data-ttu-id="3dbd9-124">integración de hello tooconfigure de Mozy Enterprise en Azure AD, deberá tooadd Mozy Enterprise de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-124">tooconfigure hello integration of Mozy Enterprise into Azure AD, you need tooadd Mozy Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3dbd9-125">**tooadd Mozy Enterprise de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3dbd9-125">**tooadd Mozy Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dbd9-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3dbd9-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3dbd9-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3dbd9-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3dbd9-133">En el cuadro de búsqueda de hello, escriba **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-133">In hello search box, type **Mozy Enterprise**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="3dbd9-135">En el panel de resultados de hello, seleccione **Mozy Enterprise**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-135">In hello results panel, select **Mozy Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3dbd9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dbd9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3dbd9-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mozy Enterprise con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3dbd9-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3dbd9-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Mozy Enterprise es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mozy Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="3dbd9-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Mozy Enterprise debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-140">In other words, a link relationship between an Azure AD user and hello related user in Mozy Enterprise needs toobe established.</span></span>

<span data-ttu-id="3dbd9-141">En Mozy Enterprise, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-141">In Mozy Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3dbd9-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Mozy Enterprise, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3dbd9-142">tooconfigure and test Azure AD single sign-on with Mozy Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3dbd9-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3dbd9-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3dbd9-145">**[Crear un usuario de prueba de Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave un equivalente de Britta Simon en Mozy Enterprise que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - toohave a counterpart of Britta Simon in Mozy Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3dbd9-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3dbd9-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3dbd9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dbd9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3dbd9-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="3dbd9-150">**inicio de sesión único en tooconfigure Azure AD con Mozy Enterprise, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3dbd9-150">**tooconfigure Azure AD single sign-on with Mozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dbd9-151">En el portal de Azure, en Hola Hola **Mozy Enterprise** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-151">In hello Azure portal, on hello **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3dbd9-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="3dbd9-155">En hello **Mozy Enterprise dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3dbd9-155">On hello **Mozy Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="3dbd9-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="3dbd9-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3dbd9-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-158">This value is not real.</span></span> <span data-ttu-id="3dbd9-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3dbd9-160">Póngase en contacto con [equipo de soporte técnico de Mozy Enterprise Client](http://support.mozy.com/) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) tooget this value.</span></span>

4. <span data-ttu-id="3dbd9-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="3dbd9-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3dbd9-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3dbd9-165">En hello **Mozy Enterprise configuración** sección, haga clic en **configurar Mozy Enterprise** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-165">On hello **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3dbd9-166">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="3dbd9-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="3dbd9-168">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="3dbd9-169">Hola **configuración** sección, haga clic en **directiva de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-169">In hello **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="3dbd9-170">![Directiva de autenticación](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Directiva de autenticación")</span><span class="sxs-lookup"><span data-stu-id="3dbd9-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="3dbd9-171">En hello **directiva de autenticación** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3dbd9-171">On hello **Authentication Policy** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="3dbd9-172">![Directiva de autenticación](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Directiva de autenticación")</span><span class="sxs-lookup"><span data-stu-id="3dbd9-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="3dbd9-173">a.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-173">a.</span></span> <span data-ttu-id="3dbd9-174">Seleccione **Servicio de directorio** como **Proveedor**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="3dbd9-175">b.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-175">b.</span></span> <span data-ttu-id="3dbd9-176">Seleccione **Use LDAP Push**(Usar inserción de LDAP).</span><span class="sxs-lookup"><span data-stu-id="3dbd9-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="3dbd9-177">c.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-177">c.</span></span> <span data-ttu-id="3dbd9-178">Haga clic en hello **autenticación SAML** ficha.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-178">Click hello **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="3dbd9-179">d.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-179">d.</span></span> <span data-ttu-id="3dbd9-180">Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **URL autenticación** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-180">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="3dbd9-181">e.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-181">e.</span></span> <span data-ttu-id="3dbd9-182">Pegar **Id. de entidad SAML**, que haya copiado desde Hola portal de Azure en hello **extremo de SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-182">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="3dbd9-183">f.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-183">f.</span></span> <span data-ttu-id="3dbd9-184">Abra el certificado codificado en base 64 descargado en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, pegue Hola certificado completo en **certificado SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-184">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="3dbd9-185">g.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-185">g.</span></span> <span data-ttu-id="3dbd9-186">Seleccione **habilitar SSO para administradores toolog con sus credenciales de red**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-186">Select **Enable SSO for Admins toolog in with their network credentials**.</span></span>
   
   <span data-ttu-id="3dbd9-187">h.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-187">h.</span></span> <span data-ttu-id="3dbd9-188">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3dbd9-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="3dbd9-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3dbd9-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3dbd9-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3dbd9-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3dbd9-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dbd9-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="3dbd9-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3dbd9-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3dbd9-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dbd9-196">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3dbd9-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3dbd9-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3dbd9-202">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3dbd9-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3dbd9-204">a.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-204">a.</span></span> <span data-ttu-id="3dbd9-205">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3dbd9-206">b.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-206">b.</span></span> <span data-ttu-id="3dbd9-207">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3dbd9-208">c.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-208">c.</span></span> <span data-ttu-id="3dbd9-209">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3dbd9-210">d.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-210">d.</span></span> <span data-ttu-id="3dbd9-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="3dbd9-212">Creación de un usuario de prueba de Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="3dbd9-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="3dbd9-213">En orden tooenable toolog de los usuarios de Azure AD en Mozy Enterprise, se les deben aprovisionar en Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-213">In order tooenable Azure AD users toolog into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="3dbd9-214">En caso de hello de Mozy Enterprise, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-214">In hello case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="3dbd9-215">Puede usar cualquier otra Mozy Enterprise usuario cuenta herramienta de creación o las API proporcionadas por Mozy Enterprise tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise tooprovision AAD user accounts.</span></span>

<span data-ttu-id="3dbd9-216">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="3dbd9-216">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dbd9-217">Inicie sesión en tooyour **Mozy Enterprise** inquilino.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-217">Log in tooyour **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="3dbd9-218">Haga clic en **Usuarios** y, luego, en **Agregar nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="3dbd9-219">![Usuarios](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="3dbd9-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="3dbd9-220">Hola **Agregar nuevo usuario** opción solo se muestra solo si **Mozy** se selecciona como proveedor de hello en **directiva de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-220">hello **Add New User** option is only displayed only if **Mozy** is selected as hello provider under **Authentication policy**.</span></span> <span data-ttu-id="3dbd9-221">Si se configura la autenticación de SAML, a continuación, los usuarios de Hola se agregan automáticamente su primer inicio de sesión a través de inicio de sesión único en.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-221">If SAML Authentication is configured, then hello users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="3dbd9-222">Del cuadro de diálogo usuario nuevo de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3dbd9-222">On hello new user dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="3dbd9-223">![Agregar usuarios](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Agregar usuarios")</span><span class="sxs-lookup"><span data-stu-id="3dbd9-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="3dbd9-224">a.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-224">a.</span></span> <span data-ttu-id="3dbd9-225">De hello **elegir un grupo de** lista, seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-225">From hello **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="3dbd9-226">b.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-226">b.</span></span> <span data-ttu-id="3dbd9-227">De hello **qué tipo de usuario** lista, seleccione un tipo.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-227">From hello **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="3dbd9-228">c.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-228">c.</span></span> <span data-ttu-id="3dbd9-229">Hola **nombre de usuario** cuadro de texto, nombre de tipo hello del usuario de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-229">In hello **Username** textbox, type hello name of hello Azure AD user.</span></span>
   
   <span data-ttu-id="3dbd9-230">d.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-230">d.</span></span> <span data-ttu-id="3dbd9-231">Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de usuario de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-231">In hello **Email** textbox, type hello email address of hello Azure AD user.</span></span>
   
   <span data-ttu-id="3dbd9-232">e.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-232">e.</span></span> <span data-ttu-id="3dbd9-233">Seleccione **Send user instruction email**(Enviar correo electrónico al usuario con instrucciones).</span><span class="sxs-lookup"><span data-stu-id="3dbd9-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="3dbd9-234">f.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-234">f.</span></span> <span data-ttu-id="3dbd9-235">Haga clic en **Add User(s)**(Agregar usuarios).</span><span class="sxs-lookup"><span data-stu-id="3dbd9-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="3dbd9-236">Después de crear el usuario de hello, un correo electrónico se enviará toohello usuario de Azure AD que incluye una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-236">After creating hello user, an email will be sent toohello Azure AD user that includes a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3dbd9-237">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dbd9-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3dbd9-238">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMozy Enterprise.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3dbd9-240">**tooassign Britta Simon tooMozy Enterprise, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3dbd9-240">**tooassign Britta Simon tooMozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dbd9-241">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3dbd9-243">En la lista de aplicaciones de hello, seleccione **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-243">In hello applications list, select **Mozy Enterprise**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="3dbd9-245">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3dbd9-247">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-247">Click **Add** button.</span></span> <span data-ttu-id="3dbd9-248">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3dbd9-250">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3dbd9-251">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3dbd9-252">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3dbd9-253">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3dbd9-253">Testing single sign-on</span></span>

<span data-ttu-id="3dbd9-254">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3dbd9-255">Al hacer clic en hello Mozy Enterprise disponer en mosaico en el Panel de acceso de hello, deberá obtener la página de inicio de sesión de aplicación de Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3dbd9-255">When you click hello Mozy Enterprise tile in hello Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="3dbd9-256">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3dbd9-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3dbd9-257">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3dbd9-257">Additional resources</span></span>

* [<span data-ttu-id="3dbd9-258">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dbd9-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3dbd9-259">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3dbd9-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

