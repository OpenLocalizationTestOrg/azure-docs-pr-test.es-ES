---
title: "Tutorial: Integración de Azure Active Directory con Google Apps en Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="bf8bc-103">Tutorial: Integración de Azure Active Directory con Google Apps</span><span class="sxs-lookup"><span data-stu-id="bf8bc-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="bf8bc-104">En este tutorial, aprenderá cómo toointegrate Google Apps con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf8bc-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf8bc-105">Integración de Google Apps con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bf8bc-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bf8bc-106">Puede controlar en Azure AD que tenga acceso tooGoogle aplicaciones</span><span class="sxs-lookup"><span data-stu-id="bf8bc-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="bf8bc-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooGoogle aplicaciones (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8bc-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf8bc-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bf8bc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bf8bc-109">Si desea tooknow obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf8bc-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf8bc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bf8bc-110">Prerequisites</span></span>

<span data-ttu-id="bf8bc-111">tooconfigure integración de Azure AD con Google Apps, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bf8bc-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="bf8bc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf8bc-113">Una suscripción habilitada para el inicio de sesión único en Google Apps</span><span class="sxs-lookup"><span data-stu-id="bf8bc-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf8bc-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf8bc-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bf8bc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf8bc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf8bc-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes: [oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf8bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="bf8bc-118">Tutorial en vídeo</span><span class="sxs-lookup"><span data-stu-id="bf8bc-118">Video tutorial</span></span>
<span data-ttu-id="bf8bc-119">¿Cómo tooEnable Single Sign-On tooGoogle aplicaciones en 2 minutos:</span><span class="sxs-lookup"><span data-stu-id="bf8bc-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="bf8bc-120">Preguntas frecuentes</span><span class="sxs-lookup"><span data-stu-id="bf8bc-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="bf8bc-121">**P: ¿Son los Chromebooks y otros dispositivos Chrome compatibles con el inicio de sesión único de Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="bf8bc-122">R: Sí, los usuarios son pueda toosign en sus dispositivos Chromebook con sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="bf8bc-123">Consulte este [artículo de soporte técnico de Google Apps](https://support.google.com/chrome/a/answer/6060880) para información sobre por qué puede que se pidan las credenciales a los usuarios dos veces.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="bf8bc-124">**P: ¿si se habilita el inicio de sesión único, volverá a los usuarios ser capaz de toouse su toosign de credenciales de Azure AD en cualquier producto de Google, como aula de Google, GMail, Google Drive, YouTube etc.?**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="bf8bc-125">R: Sí, dependiendo de [qué aplicaciones de Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) elige tooenable o deshabilitar para su organización.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="bf8bc-126">**P: ¿Puedo habilitar el inicio de sesión único solo para un subconjunto de mis usuarios de Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="bf8bc-127">R: no, activar inmediatamente en el inicio de sesión único requiere que todos los tooauthenticate de los usuarios de Google Apps con sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="bf8bc-128">Dado que Google Apps no admite tener varios proveedores de identidad, proveedor de identidades de Hola para su entorno de Google Apps puede ser Azure AD o Google, pero no ambos al Hola mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="bf8bc-129">**P: ¿si un usuario ha iniciado sesión a través de Windows, son que se autentican automáticamente aplicaciones tooGoogle sin que se le pide una contraseña?**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="bf8bc-130">R: Hay dos opciones para habilitar este escenario.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="bf8bc-131">En primer lugar, los usuarios podrían iniciar sesión en dispositivos Windows 10 a través de [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf8bc-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="bf8bc-132">Como alternativa, podrían iniciar sesión a los usuarios en los dispositivos de Windows que usan tooan Unidos a un dominio de Active Directory que se ha habilitado para único inicio de sesión tooAzure AD a través de local a un [los servicios de federación de Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) implementación.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="bf8bc-133">Ambas opciones requieren pasos de hello tooperform Hola después tutorial tooenable inicio de sesión único entre Azure AD y Google Apps.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf8bc-134">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bf8bc-134">Scenario description</span></span>
<span data-ttu-id="bf8bc-135">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf8bc-136">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="bf8bc-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf8bc-137">Agregar aplicaciones de Google de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bf8bc-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="bf8bc-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8bc-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="bf8bc-139">Agregar aplicaciones de Google de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bf8bc-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="bf8bc-140">integración de hello tooconfigure de Google Apps en Azure AD, deberá tooadd Google Apps en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bf8bc-141">**tooadd Google Apps en Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8bc-142">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bf8bc-144">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bf8bc-145">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-145">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="bf8bc-147">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="bf8bc-149">En el cuadro de búsqueda de hello, escriba **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-149">In hello search box, type **Google Apps**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="bf8bc-151">En el panel de resultados de hello, seleccione **Google Apps**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf8bc-153">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8bc-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf8bc-154">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Google Apps con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bf8bc-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf8bc-155">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Google Apps es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="bf8bc-156">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Google Apps debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="bf8bc-157">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Google Apps.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="bf8bc-158">tooconfigure y prueba de inicio de sesión único en Azure AD con Google Apps, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bf8bc-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bf8bc-159">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bf8bc-160">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf8bc-161">**[Crear un usuario de prueba de Google Apps](#creating-a-google-apps-test-user) ** -toohave un equivalente de Britta Simon en Google Apps que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf8bc-162">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf8bc-163">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf8bc-164">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8bc-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf8bc-165">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Google Apps.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="bf8bc-166">**inicio de sesión único en tooconfigure Azure AD con Google Apps, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8bc-167">En el portal de Azure, en Hola Hola **Google Apps** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bf8bc-169">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="bf8bc-171">En hello **dominio de Google Apps y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bf8bc-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="bf8bc-173">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="bf8bc-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bf8bc-174">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-174">This value is not real.</span></span> <span data-ttu-id="bf8bc-175">Actualice el valor de hello con URL de inicio de sesión real de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="bf8bc-176">Póngase en contacto con hello [equipo de soporte técnico de Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="bf8bc-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="bf8bc-177">En hello **el certificado de firma de SAML** sección, haga clic en **certificado** y, a continuación, guarde el certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="bf8bc-179">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bf8bc-179">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bf8bc-181">En hello **configuración de aplicaciones de Google** sección, haga clic en **configurar Google Apps** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bf8bc-182">Hola copia **dirección URL de cierre de sesión, SAML Single Sign-On dirección URL del servicio y cambio de dirección URL de contraseña** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="bf8bc-184">Abra una nueva pestaña en el explorador e inicie sesión en hello [consola de administración de aplicaciones de Google](http://admin.google.com/) con su cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="bf8bc-185">Haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-185">Click **Security**.</span></span> <span data-ttu-id="bf8bc-186">Si no ve el vínculo de hello, puede estar oculto bajo hello **más controles** menú situado en la parte inferior de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Haga clic en Seguridad.][10]

9. <span data-ttu-id="bf8bc-188">En hello **seguridad** página, haga clic en **configurar el inicio de sesión único (SSO).**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Haga clic en SSO.][11]

10. <span data-ttu-id="bf8bc-190">Lleve a cabo Hola después de los cambios de configuración:</span><span class="sxs-lookup"><span data-stu-id="bf8bc-190">Perform hello following configuration changes:</span></span>
   
    ![Configuración de SSO][12]
   
    <span data-ttu-id="bf8bc-192">a.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-192">a.</span></span> <span data-ttu-id="bf8bc-193">Seleccione **Configurar SSO con un proveedor de identidades de terceros**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="bf8bc-194">b.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-194">b.</span></span> <span data-ttu-id="bf8bc-195">En el **URL de la página de inicio de sesión** en Google Apps, a continuación, pegue el valor de Hola de **URL de servicio de inicio de sesión único**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bf8bc-196">c.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-196">c.</span></span> <span data-ttu-id="bf8bc-197">Hola **URL de la página de cierre de sesión** en Google Apps, a continuación, pegue el valor de Hola de **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="bf8bc-198">d.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-198">d.</span></span> <span data-ttu-id="bf8bc-199">Hola **cambiar dirección URL de contraseña** en Google Apps, a continuación, pegue el valor de Hola de **cambiar dirección URL de contraseña**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="bf8bc-200">e.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-200">e.</span></span> <span data-ttu-id="bf8bc-201">En aplicaciones de Google, para hello **certificado de verificación**, certificado de Hola de carga que ha descargado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="bf8bc-202">f.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-202">f.</span></span> <span data-ttu-id="bf8bc-203">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="bf8bc-204">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="bf8bc-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bf8bc-205">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bf8bc-206">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf8bc-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf8bc-207">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8bc-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf8bc-208">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="bf8bc-210">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8bc-211">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf8bc-213">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf8bc-215">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf8bc-217">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="bf8bc-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf8bc-219">a.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-219">a.</span></span> <span data-ttu-id="bf8bc-220">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf8bc-221">b.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-221">b.</span></span> <span data-ttu-id="bf8bc-222">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf8bc-223">c.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-223">c.</span></span> <span data-ttu-id="bf8bc-224">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bf8bc-225">d.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-225">d.</span></span> <span data-ttu-id="bf8bc-226">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="bf8bc-227">Creación de un usuario de prueba de Google Apps</span><span class="sxs-lookup"><span data-stu-id="bf8bc-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="bf8bc-228">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Software de aplicaciones de Google.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="bf8bc-229">Google Apps admite el aprovisionamiento automático, que está habilitado de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="bf8bc-230">El usuario no tiene que hacer nada en esta sección.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-230">There is no action for you in this section.</span></span> <span data-ttu-id="bf8bc-231">Si un usuario ya no existe en el Software de aplicaciones de Google, se crea uno nuevo si intentas tooaccess Software de aplicaciones de Google.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="bf8bc-232">Si necesita un usuario toocreate manualmente, póngase en contacto con hello [equipo de soporte técnico de Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="bf8bc-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bf8bc-233">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8bc-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bf8bc-234">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooGoogle aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="bf8bc-236">**tooassign Britta Simon tooGoogle aplicaciones, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bf8bc-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8bc-237">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bf8bc-239">En la lista de aplicaciones de hello, seleccione **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-239">In hello applications list, select **Google Apps**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="bf8bc-241">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="bf8bc-243">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-243">Click **Add** button.</span></span> <span data-ttu-id="bf8bc-244">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="bf8bc-246">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bf8bc-247">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf8bc-248">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf8bc-249">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="bf8bc-249">Testing single sign-on</span></span>

<span data-ttu-id="bf8bc-250">En esta sección, tootest Hola de su inicio de sesión configuración de inicio único, abra Panel de acceso en [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), a continuación, inicie sesión en la cuenta de prueba de Hola y haga clic en **Google Apps** el icono Servicios Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bf8bc-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf8bc-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bf8bc-251">Additional resources</span></span>

* [<span data-ttu-id="bf8bc-252">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf8bc-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf8bc-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf8bc-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bf8bc-254">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="bf8bc-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png