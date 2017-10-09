---
title: "Tutorial: Integración de Azure Active Directory con Menlo Security | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la seguridad de Menlo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="e323a-103">Tutorial: Integración de Azure Active Directory con Menlo Security</span><span class="sxs-lookup"><span data-stu-id="e323a-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="e323a-104">En este tutorial, aprenderá cómo toointegrate Menlo seguridad con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e323a-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e323a-105">Integración de seguridad de Menlo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e323a-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e323a-106">Puede controlar en Azure AD que tenga acceso tooMenlo seguridad</span><span class="sxs-lookup"><span data-stu-id="e323a-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="e323a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMenlo seguridad (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e323a-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e323a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e323a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e323a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte.</span><span class="sxs-lookup"><span data-stu-id="e323a-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="e323a-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="e323a-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e323a-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e323a-111">Prerequisites</span></span>

<span data-ttu-id="e323a-112">integración de Azure AD con seguridad Menlo tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e323a-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="e323a-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e323a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="e323a-114">Una suscripción habilitada para el inicio de sesión único en Menlo Security</span><span class="sxs-lookup"><span data-stu-id="e323a-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e323a-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e323a-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e323a-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e323a-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e323a-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e323a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e323a-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e323a-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e323a-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e323a-119">Scenario description</span></span>
<span data-ttu-id="e323a-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e323a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e323a-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e323a-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e323a-122">Agregar seguridad Menlo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e323a-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="e323a-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e323a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="e323a-124">Agregar seguridad Menlo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e323a-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="e323a-125">integración de hello tooconfigure de Menlo seguridad en Azure AD, deberá tooadd seguridad Menlo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e323a-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e323a-126">**tooadd Menlo de seguridad de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e323a-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e323a-127">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e323a-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e323a-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e323a-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e323a-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e323a-130">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e323a-132">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e323a-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e323a-134">En el cuadro de búsqueda de hello, escriba **Menlo seguridad**.</span><span class="sxs-lookup"><span data-stu-id="e323a-134">In hello search box, type **Menlo Security**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="e323a-136">En el panel de resultados de hello, seleccione **Menlo seguridad**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e323a-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e323a-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e323a-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e323a-139">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Menlo Security con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e323a-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e323a-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en seguridad Menlo es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e323a-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="e323a-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en seguridad Menlo debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e323a-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="e323a-142">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Menlo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e323a-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="e323a-143">tooconfigure y prueba de inicio de sesión único en Azure AD con seguridad Menlo, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e323a-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e323a-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e323a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e323a-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e323a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e323a-146">**[Crear un usuario de prueba de seguridad Menlo](#creating-a-menlo-security-test-user)**  -toohave un equivalente de Britta Simon en seguridad Menlo representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="e323a-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e323a-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e323a-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e323a-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e323a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e323a-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e323a-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e323a-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de seguridad de Menlo.</span><span class="sxs-lookup"><span data-stu-id="e323a-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="e323a-151">**inicio de sesión único en tooconfigure Azure AD con seguridad Menlo, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e323a-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="e323a-152">En el portal de Azure, en Hola Hola **Menlo seguridad** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e323a-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e323a-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e323a-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="e323a-156">En hello **Menlo seguridad de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e323a-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="e323a-158">a.</span><span class="sxs-lookup"><span data-stu-id="e323a-158">a.</span></span> <span data-ttu-id="e323a-159">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="e323a-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="e323a-160">b.</span><span class="sxs-lookup"><span data-stu-id="e323a-160">b.</span></span> <span data-ttu-id="e323a-161">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="e323a-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e323a-162">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="e323a-162">These values are not hello real.</span></span> <span data-ttu-id="e323a-163">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="e323a-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e323a-164">Póngase en contacto con [equipo de soporte técnico de cliente de seguridad Menlo](https://www.menlosecurity.com/menlo-contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="e323a-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="e323a-165">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e323a-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="e323a-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e323a-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e323a-169">En hello **configuración de seguridad de Menlo** sección, haga clic en **configurar la seguridad de Menlo** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="e323a-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e323a-170">Hola copia **Id. de entidad SAML**, y **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="e323a-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="e323a-172">tooconfigure inicio de sesión único en **Menlo seguridad** lado, inicio de sesión toohello **Menlo seguridad** sitio Web como administrador.</span><span class="sxs-lookup"><span data-stu-id="e323a-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="e323a-173">En **configuración** vaya demasiado**autenticación** y realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="e323a-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="e323a-175">a.</span><span class="sxs-lookup"><span data-stu-id="e323a-175">a.</span></span> <span data-ttu-id="e323a-176">Casilla de verificación de Hola de graduación **habilitar la autenticación de usuario mediante SAML**.</span><span class="sxs-lookup"><span data-stu-id="e323a-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="e323a-177">b.</span><span class="sxs-lookup"><span data-stu-id="e323a-177">b.</span></span> <span data-ttu-id="e323a-178">Seleccione **permitir el acceso externo a** demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="e323a-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="e323a-179">c.</span><span class="sxs-lookup"><span data-stu-id="e323a-179">c.</span></span> <span data-ttu-id="e323a-180">En **SAML Provider** (Proveedor de SAML), seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e323a-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="e323a-181">d.</span><span class="sxs-lookup"><span data-stu-id="e323a-181">d.</span></span> <span data-ttu-id="e323a-182">**Extremo de SAML 2.0** : Hola pegar **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e323a-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e323a-183">e.</span><span class="sxs-lookup"><span data-stu-id="e323a-183">e.</span></span> <span data-ttu-id="e323a-184">**Identificador de servicio (emisor)** : Hola pegar **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e323a-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e323a-185">f.</span><span class="sxs-lookup"><span data-stu-id="e323a-185">f.</span></span> <span data-ttu-id="e323a-186">**Certificado X.509** : Hola abierto **certificado (Base64)** descargado de hello Portal de Azure en el Bloc de notas y pegue en este cuadro.</span><span class="sxs-lookup"><span data-stu-id="e323a-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="e323a-187">g.</span><span class="sxs-lookup"><span data-stu-id="e323a-187">g.</span></span> <span data-ttu-id="e323a-188">Haga clic en **guardar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="e323a-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="e323a-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e323a-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e323a-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e323a-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e323a-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e323a-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e323a-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e323a-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e323a-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e323a-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e323a-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e323a-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e323a-196">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e323a-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e323a-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e323a-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e323a-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e323a-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e323a-202">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e323a-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e323a-204">a.</span><span class="sxs-lookup"><span data-stu-id="e323a-204">a.</span></span> <span data-ttu-id="e323a-205">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e323a-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e323a-206">b.</span><span class="sxs-lookup"><span data-stu-id="e323a-206">b.</span></span> <span data-ttu-id="e323a-207">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e323a-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e323a-208">c.</span><span class="sxs-lookup"><span data-stu-id="e323a-208">c.</span></span> <span data-ttu-id="e323a-209">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e323a-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e323a-210">d.</span><span class="sxs-lookup"><span data-stu-id="e323a-210">d.</span></span> <span data-ttu-id="e323a-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e323a-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="e323a-212">Creación de un usuario de prueba de Menlo Security</span><span class="sxs-lookup"><span data-stu-id="e323a-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="e323a-213">En esta sección, creará un usuario llamado Britta Simon en Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="e323a-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="e323a-214">Trabajar con [equipo de soporte técnico de cliente de seguridad Menlo](https://www.menlosecurity.com/menlo-contact) tooadd los usuarios de hello en la plataforma de seguridad Menlo Hola.</span><span class="sxs-lookup"><span data-stu-id="e323a-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="e323a-215">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e323a-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e323a-216">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e323a-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e323a-217">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMenlo seguridad.</span><span class="sxs-lookup"><span data-stu-id="e323a-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e323a-219">**tooassign Britta Simon tooMenlo seguridad, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e323a-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="e323a-220">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e323a-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e323a-222">En la lista de aplicaciones de hello, seleccione **Menlo seguridad**.</span><span class="sxs-lookup"><span data-stu-id="e323a-222">In hello applications list, select **Menlo Security**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="e323a-224">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e323a-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e323a-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e323a-226">Click **Add** button.</span></span> <span data-ttu-id="e323a-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e323a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e323a-229">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e323a-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e323a-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e323a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e323a-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e323a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e323a-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e323a-232">Testing single sign-on</span></span>

<span data-ttu-id="e323a-233">En esta sección, probará la configuración de inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e323a-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="e323a-234">Abra una ventana del explorador en un modo "InPrivate" o "Incógnito" tootrigger una nueva autenticación.</span><span class="sxs-lookup"><span data-stu-id="e323a-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="e323a-235">En Internet Explorer, utilice Ctrl + Mayús + P.</span><span class="sxs-lookup"><span data-stu-id="e323a-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="e323a-236">En Chrome, utilice Ctrl + Mayús + N.</span><span class="sxs-lookup"><span data-stu-id="e323a-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="e323a-237">En la ventana de exploración privada de hello, examinar tooa al recurso protegido y realizar un inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e323a-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="e323a-238">Cuando inician sesión correctamente, será el sitio solicitado toohello obtenidos en una sesión de aislamiento.</span><span class="sxs-lookup"><span data-stu-id="e323a-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e323a-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e323a-239">Additional resources</span></span>

* [<span data-ttu-id="e323a-240">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e323a-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e323a-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e323a-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

